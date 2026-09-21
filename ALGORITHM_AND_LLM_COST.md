# Recommendation algorithm, LLM role, and cost
**Snapshot:** September 2026  
**Status:** Research finding (not a coded engine)  
**Rule:** Storefront recs are **not** an LLM call. LLM is an offline helper. Conflicts → [DECISIONS.md](DECISIONS.md) + [COMPARISON.md](COMPARISON.md).

**Sources:** CBB live waterfall ([competitors/CBB_FREQUENTLY_BOUGHT_TOGETHER.md](competitors/CBB_FREQUENTLY_BOUGHT_TOGETHER.md)); Nosto algorithm catalog ([competitors/NOSTO.md](competitors/NOSTO.md)); Cloudflare Workers / D1 / KV / Vectorize / Workers AI pricing (docs, Sept 2026); OpenAI list prices (gpt-4o-mini, gpt-5, text-embedding-3-small, Aug–Sept 2026).

---

## 1. What “AI” means in this category (competitor fact)

CBB’s live admin calls the middle tier “Automatic AI.” On install it processed **32 orders → 4 pairings**. That is **association-rule / co-occurrence mining** (they name Apriori / collaborative filtering), not a large language model.

Nosto’s 13 types (personalized, VisualAI, replenish, geo, bestsellers) are also **precomputed campaign slots**, not a GPT call on every product page.

LimeSpot boxes (Bought Together, Related, Most Popular, You May Like) are the same family: rules + history + popularity, served from cache.

**Finding:** Shopify FBT winners do **not** ask an LLM “what should we show?” on the hot path. They precompute a short list, then render HTML/JSON in a few milliseconds.

---

## 2. How our engine should work (online path)

Match CBB, with a **complement map** instead of same-leaf category / random-collection as last resort.

```
orders/create|cancelled + refunds/create
  → HMAC + claimWebhookDelivery (D1: event_id + webhook_id)
  → hygiene filter (skip test / unpaid / cancelled / _cr_src lines)
  → Queue.send(order line-items)
  → HTTP 200 (target p99 < 500ms; Shopify limit 5s)

queue consumer
  → upsert pair_count + ProductOrderStats.order_count + ShopOrderStats
  → confidence is NOT stored: pair_count / ProductOrderStats[A]
  → write $app.recs_top3 product metafield (+ KV RecCache optional)
  → never call an LLM

PDP widget
  → Liquid reads metafield (zero extra RTT). Unpublished skipped.
  → optional App Proxy stock ping (signed). Public GET /api/recs?shop= forbidden.
```

`ctx.waitUntil` after ACK is **not** a queue: Shopify already got 200, so a crashed isolate drops the order with no retry. Queues (or a D1 `OrderIngest` row written **before** ACK + cron sweeper) is the durability layer. BFCM lock contention is a later scale problem; silent loss on Fast-ACK is a v1 problem.

### Waterfall (serve 3 in-stock items)

| Tier | Name | Logic | When it fires |
| :--- | :--- | :--- | :--- |
| 1 | Manual | `RecommendationRules` for this `base_product_id`. Also ingest Search & Discovery `shopify--discovery--product_recommendation.complementary_products` if the merchant already curated them. | Merchant / native Shopify complementary always wins |
| 2 | Co-purchase | `confidence = pair_count / ProductOrderStats.order_count` (derived, not a stored column). Render-time stock: hide iff tracked + DENY + available≤0 | **Serve** if `pair_count >= 1`. **Percent badge** only if `pair_count >= 5` **and** `orders(A) >= 20` |
| 3 | Complement map | Static vertical JSON: source taxonomy GID → complementary GIDs (phone case → protector/charger, not another case). Then `ProductCatalog` in those target categories, in-stock, not self. | Cold start / new SKU. **Never same-leaf category** |
| 4 | Bestseller | `ProductCatalog.sales_count` in-stock | Last fill so the widget is never empty |

Do **not** use Shopify `productRecommendations(intent: RELATED)` or Vectorize similarity inside the FBT widget. Shopify documents RELATED as **substitutable** (“You may also like”). Complementary (`intent: COMPLEMENTARY`) is **manual-only** via Search & Discovery — empty on a new store unless the merchant set it. Taxonomy itself has categories + attributes, **no native complement edges**.

CBB live extra (keep as merchant toggles): **Exclusive Manual** mode; **Global** pin list; outbound exclusion (gift cards, warranties).

Widget copy must match the tier that filled the slot: “Frequently bought together” only for Tier 2; “Goes with” / “Pair it with” for Tier 3; “Popular in this store” for Tier 4. Lying about FBT on a 0-order store is the actual churn mechanism, not “no embeddings.”

### Scores (no neural net required)

For product A recommending B:

* `pair_count(A,B)` = **hygienic** paid orders containing both (not test, not cancelled, not refunded, lines without `_cr_src`)  
* `orders_containing(A)` from `ProductOrderStats` — **required table**; without it stored confidence goes stale when A sells again  
* `confidence(A→B) = pair_count(A,B) / orders_containing(A)`  (compute at rank time)  
* `lift(A→B) = confidence(A→B) / (orders_containing(B) / ShopOrderStats.order_count)`  
* Rank by `confidence`, break ties with `lift` then `pair_count`  
* Optional recency decay at rank time only: `pair_count * exp(-λ * days_since last_purchased_at)`  
* Optional filters: rec price 0.2×–3× of A; exclude `gift_card`; `ProductCatalog.status = ACTIVE`

### Explainer badge (the USP) — also no LLM

Split two thresholds that were previously conflated:

* **Serve** a co-purchase pair at `pair_count >= 1` (optionally 2).  
* **Print a percent** only if `pair_count >= 5` **and** `orders(A) >= 20`. Six orders of A with five pairs = 83% is a lie; `pair_count >= 5` alone is not enough.  
* Matrix is **product-level**, not variant. Never print “87% bought this size.”  
* Else if Tier 2 but weak support: `"Often bought together"` or **count** `"12 customers also bought"` — no invented percent.  
* Tier 3: `"Goes with this"` from the static map.  
* Else hide the badge.

That is the LimeSpot/CBB gap: they have the stats in admin; they do not print them on the storefront. LLM prose badges are the same App Store risk as fake percents.

---

## 3. Where an LLM actually belongs (offline / rare)

| Job | LLM? | Why |
| :--- | :---: | :--- |
| Pick the 3 PDP items | **No** | Latency 300ms–2s; cost scales with traffic; worse than co-purchase for FBT |
| Storefront explainer percent | **No** | Hallucinates rates; stats already exist |
| Chat “shopping assistant” as the recs product | **No** | Saturated; competes with Sidekick |
| Extract attributes from title/body (skin type, compatibility, color) | **Yes, batch, v1.5** | Filter on the complement map; **must not return product IDs**. Skip in v1 if the static map is shipping |
| Compile Fashion / Beauty / Electronics **complement** JSON | **Yes, once, humans edit** | LimeSpot-style vertical pick (they ship 12). Not a per-SKU LLM job |
| Per-SKU complementary product IDs | **No** | Hallucinated SKUs; join still needed. Use the map + catalog |
| Admin “why this pair?” paragraph | **Yes, on click** | 1 merchant action, not 50k shoppers. Prompt must include `pair_count` / `confidence` |
| LLM storefront social-proof sentence | **No** | Unauditable claim; App Store risk |
| “AI Store Audit” auto-publishes 10 bundles | **No** | Silent merchandising change. On install: mine last **60 days** of orders (default Admin; `read_all_orders` is Partner-approved, not v1) and offer **drafts** |
| Nightly QA: gift cards in recs, same-item dupes | **Optional** | Cheap classifier / rules first |
| VisualAI look-alike | **Later** | Nosto already sells it; image embeddings ≠ v1 |

### Offline catalog pass (v1.5, not required to ship the widget)

On `products/create` and `products/update`:

1. Send title + description + vendor + tags (trimmed, ~300–500 tokens).  
2. Ask a **small** model for **structured JSON only**: `{ color, category_guess, complementary_types[], exclude_as_rec, size_system }`.  
3. Store on `ProductCatalog` / metafields.  
4. Vertical template uses those fields (Beauty: don’t pair retinol + AHA without a caution flag; Electronics: accessory type ∈ compatible_with).

Do **not** let the model return product IDs. It may only return **attributes**. IDs still come from the waterfall.

---

## 4. Cost model (September 2026 list prices)

Assumptions for **one Growth-sized shop** (used as the unit):

* 2,000 SKUs  
* 50,000 rec widget fetches / month  
* 500 orders / month  
* ~2.5 line items / order  

Workers Paid is **one Cloudflare account** for the whole SaaS ($5/mo + usage), not $5 per shop.

### Unit prices used

| Meter | Price | Source |
| :--- | :--- | :--- |
| Workers Paid base | $5 / account / mo; 10M requests included; then $0.30 / M | Cloudflare Workers pricing |
| KV reads | 10M included; then $0.50 / M | KV pricing |
| D1 | 25B rows read / 50M rows written included | D1 pricing |
| gpt-4o-mini | $0.15 / M input, $0.60 / M output | OpenAI (Aug 2026 trackers) |
| gpt-5 | $1.25 / M input, $10 / M output | OpenAI |
| CF Llama 3.2 3B | $0.051 / M in, $0.335 / M out | Workers AI pricing (17 Sep 2026) |
| CF bge-m3 embed | $0.012 / M input tokens | Workers AI embeddings |
| Vectorize | 50M queried dims + 10M stored dims included on Paid | Vectorize pricing |
| Cloudflare Queues | 1M ops / mo included on Paid; then $0.40 / M ops (~3 ops per delivered message) | Queues pricing |
| text-embedding-3-small | $0.02 / M tokens | OpenAI |

Token assumptions for an online “ask the model to pick 3 products” call: **~600 input + ~100 output** tokens (catalog stub + instruction). Real catalogs are larger → **these are lower bounds**.

### Per shop / month (50k widget views)

| Path | What runs on the PDP request | Est. LLM/embed $ | Latency | Fit on $19 plan? |
| :--- | :--- | ---: | :--- | :--- |
| **A. Metafield + complement map** | Liquid metafield (0 extra RTT) | **~$0** LLM | metafield = 0 RTT; App Proxy p99 < 500ms | Yes — this is v1 |
| **B. Offline LLM enrich** (2k SKUs / mo) | Still KV get; LLM only on product webhooks | **~$0.30** (mini, 400 in / 150 out × 2k) | PDP unchanged | Yes |
| **C. Embeddings / Vectorize** | Do **not** put on the FBT widget (nearest-neighbor ≈ substitute). Optional later for a separate “Similar items” row; Shopify `intent: RELATED` already does this for free | **&lt;$0.02** if we ever run it | +20–80 ms | **Not v1** |
| **D. Llama 3.2 3B every view** | LLM ranks live | **~$3.21** | 300–800 ms | Tight vs $19 after other costs |
| **E. gpt-4o-mini every view** | LLM ranks live | **~$7.50** | 400–1200 ms | No — eats the plan |
| **F. gpt-5 every view** | LLM ranks live | **~$194** | 1–3 s | Company-killing |

**Path A math (LLM):** $0.  
**Path D math:** 50k × 600 = 30M in × $0.051/M = $1.53; 50k × 100 = 5M out × $0.335/M = $1.68; **$3.21**.  
**Path E math:** 30M × $0.15 = $4.50; 5M × $0.60 = $3.00; **$7.50**.  
**Path F math:** 50k × 1,500 in × $1.25/M ≈ $94; 50k × 200 out × $10/M = $100; **~$194** (uses a fatter prompt; still a floor).

### SaaS-scale (500 shops, same mix) — infra + LLM, not Shopify fees

| Path | Cloudflare (shared) | LLM | Total / mo | vs 500 × $19 ARPU ($9,500) |
| :--- | ---: | ---: | ---: | :--- |
| A. Cache waterfall | ~$5–20 (requests+KV after included) | $0 | **~$20** | Fine |
| A + B offline mini | ~$20 | ~$150 | **~$170** | Fine |
| E mini on every view | ~$20 | **$3,750** | **~$3,770** | 40% of revenue gone before Shopify cut / support |
| F gpt-5 on every view | ~$20 | **~$97,000** | Dead | |

500 × 50k = 25M Worker requests → 15M extra × $0.30 = $4.50 plus $5 base. KV 25M reads → 15M extra × $0.50 = $7.50. D1 pair updates stay inside included writes at this volume. **The dangerous line item is LLM-on-request, not D1.**

---

## 5. Recommendation for this pack

1. **v1 engine = CBB math + cache + printed confidence + complement map.** Call it “AI” in App Store copy the same way CBB does (association rules). Do not put “powered by GPT” on the widget.  
2. **Cold-start ≠ Vectorize.** Day-1: (a) mine last **60 days** of orders; (b) serve Tier 2 at support 1–2; (c) Tier 3 = vertical complement GIDs; (d) label the widget by source.  
3. **LLM budget: optional.** v1 can ship with **zero LLM** if the 12-vertical complement JSON is hand-authored (or LLM-drafted once, humans edit). If we add catalog JSON extract later: cap **&lt;$0.50 / shop / month**.  
4. **Never block PDP render on an LLM.** Timeout = empty widget = bounce.  
5. **Durable Fast-ACK:** Queue.send (or D1 ingest row before 200) in Phase 2. Do not increment 10–45 pairs inside the webhook request. Do not sell 10–30s “micro-batch architecture” as a v1 epic.  
6. **VisualAI / gpt-5 ranking / Vectorize = Scale hypothesis**, not the $0–$19 wedge.  
7. Explainer percents **must** use `pair_count >= 5` **and** `orders(A) >= 20`. Else show a count. Product-level only.  
8. **Discount Function** is in the v1 FBT path (not “automatic discount” REST). Attribution = line-item `_cr_src` → `AttributedLineItems`; cap never silently kills the widget.  
9. Recs delivery = metafield or signed App Proxy. Public `GET /api/recs?shop=` is out.

---

## 6. Open items (not claimed as fact)

* Exact `serve_min_support` (1 vs 2) per vertical — tune after ~50 beta stores. `badge_min_support` frozen at pair≥5 **and** orders(A)≥20 until then.  
* How complete merchant-assigned Shopify taxonomy GIDs are on $0/$19 stores.  
* Image-embedding cost for VisualAI (not modeled).  
* Post-purchase slot vs ReConvert/AfterSell/Zipify — not torn down; do not sell as default Growth headline.

---

## 8. Architecture gaps freeze (Claude review B, Sept 2026)

Accepted into MASTER v1.3. This file + [COMPARISON.md](COMPARISON.md) win on conflict.

| Gap | v1 spec |
| :--- | :--- |
| Discount Function missing | `cart.lines.discounts.generate.run`; scope `write_discounts`. Phase 6. Not Automatic Discount REST. |
| Schema cannot compute confidence | `ProductOrderStats` + `ShopOrderStats`; derive confidence/lift at rank time. Decay at rank time only. |
| Order hygiene | Skip test / unpaid / cancelled / refunded; skip lines with `_cr_src` (no self-feedback). Decrement on cancel/refund. |
| Inventory payload | `InventoryItemMap` + `LocationInventory`. Webhook invalidates cache. Render-time hide only if tracked+DENY+qty≤0. Drop `InventoryShield`. |
| Attribution / billing | `_cr_src` on cart add → `AttributedLineItems`. Cap = that sum. At 100%: upgrade request, widget stays on. Scale = no GMV cap. |
| Growth $49 checkout | Plus-gated; not SMB headline. Post-purchase is one-app slot; incumbents unnamed in competitor pack. |
| Public recs GET | Forbidden. Metafield first; App Proxy signed. Filter unpublished. |
| Latency copy | Not worldwide sub-15ms / $0 infra. Webhook p99 < 500ms ACK. |
| Badge % | pair≥5 **and** orders(A)≥20; never variant-size claims. |
| Token / GDPR / pixel | AES-GCM session token. Mandatory GDPR webhooks in Phase 2. Analytics `session_id` TTL 90d. Protected customer data for orders. |
| 5KB | Per-widget gzip. FBT <5KB. Drawer is a separate later budget. |

---

## 7. Architecture peer-review freeze (Sept 2026)

Challenge from Antigravity (DeepMind-style review). Verdicts below are research decisions; this file + [COMPARISON.md](COMPARISON.md) win on conflict.

| # | Challenge | Verdict | Why |
| :--- | :--- | :--- | :--- |
| 1 | Vectorize + `bge-*` for $0/$19 cold-start | **YAGNI v1** | Cost was never the issue (~$0.01). Geometry is: cosine-similar ≠ complementary. Shopify `RELATED` already auto-generates substitutes from sales + descriptions + collections ([docs](https://shopify.dev/docs/storefronts/themes/product-merchandising/recommendations)). CBB ships Global + random-collection on sparse data and still sits at 4.9★. Fix: split support thresholds, historical order mine on install, source-honest widget titles. |
| 2 | Same-category fallback is substitutes | **Must-fix v1** | Correct trap. Shopify taxonomy has **no** complement graph; `intent: complementary` is **merchant-manual** metafields, empty on new stores. Do **not** wait for an LLM per SKU. Ship a static vertical complement map (LimeSpot’s 12-industry pick is the pattern) + import S&D complementary metafields when present. LLM may draft the JSON **once**. |
| 3 | D1 write contention → Queues in Phase 2 | **Thin queue = must-have; BFCM theater = YAGNI** | D1 is single-threaded ([limits](https://developers.cloudflare.com/d1/platform/limits/)). &lt;500 orders/mo will not lock-starve D1. Fast-ACK **without** durable offload **will** drop orders (`waitUntil` dies after 200, Shopify will not retry). Queues Paid: 1M ops included, then $0.40/M (~3 ops/message). 500 orders/mo is noise vs the included 1M. Implement: webhook → `Queue.send` → consumer `db.batch()`. Skip 10–30s “micro-batch platform” stories until 10k+ orders/mo or multi-tenant BFCM. |
| 4a | LLM dynamic social-proof badges | **Drop** | Vanity + misleading-claim risk. Templates from stats already are the USP. |
| 4b | 1-click “AI Store Audit” auto 10 bundles | **Must-have as order mining + drafts; drop as generative auto-publish** | CBB’s wizard already async-mines history. That is high-ROI. GPT inventing 10 bundles from titles is merchandising vandalism. |

**v1 USP vs CBB (not “we also have Apriori”):** storefront source label + printed confidence when support exists; complement-not-clone fallback; inventory hide; free plan does not lock the engine (CBB free = 3 manual, no AI); post-purchase 1-click (CBB has none). That is enough. Do not invent a second AI story for App Store screenshots.

---
*File: `ALGORITHM_AND_LLM_COST.md` · prices will move; re-check Cloudflare + OpenAI pages before a board cost slide.*
