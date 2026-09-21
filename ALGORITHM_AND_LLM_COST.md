# Recommendation algorithm, LLM role, and cost
**Snapshot:** September 2026  
**Status:** Research finding (not a coded engine)  
**Rule:** Storefront recs are **not** an LLM call. LLM is an offline helper. If STRATEGY/MASTER say otherwise, this file + [COMPARISON.md](COMPARISON.md) win.

**Sources:** CBB live waterfall ([competitors/CBB_FREQUENTLY_BOUGHT_TOGETHER.md](competitors/CBB_FREQUENTLY_BOUGHT_TOGETHER.md)); Nosto algorithm catalog ([competitors/NOSTO.md](competitors/NOSTO.md)); Cloudflare Workers / D1 / KV / Vectorize / Workers AI pricing (docs, Sept 2026); OpenAI list prices (gpt-4o-mini, gpt-5, text-embedding-3-small, Aug–Sept 2026).

---

## 1. What “AI” means in this category (competitor fact)

CBB’s live admin calls the middle tier “Automatic AI.” On install it processed **32 orders → 4 pairings**. That is **association-rule / co-occurrence mining** (they name Apriori / collaborative filtering), not a large language model.

Nosto’s 13 types (personalized, VisualAI, replenish, geo, bestsellers) are also **precomputed campaign slots**, not a GPT call on every product page.

LimeSpot boxes (Bought Together, Related, Most Popular, You May Like) are the same family: rules + history + popularity, served from cache.

**Finding:** Shopify FBT winners do **not** ask an LLM “what should we show?” on the hot path. They precompute a short list, then render HTML/JSON in a few milliseconds.

---

## 2. How our engine should work (online path)

Match CBB, with taxonomy instead of random-collection as last resort (already in MASTER).

```
orders/create webhook
  → Fast-ACK
  → increment CoPurchaseMatrix pairs for every line-item pair in the order
  → recompute top-K for those product_ids
  → write RecCache (KV): shop + product_id → { items[], badges[], stock }

PDP widget GET /api/recs?shop=&product_id=
  → KV lookup (miss: D1 waterfall, then fill KV)
  → never call an LLM
```

### Waterfall (serve 3 in-stock items)

| Tier | Name | Logic | When it fires |
| :--- | :--- | :--- | :--- |
| 1 | Manual | `RecommendationRules` for this `base_product_id` | Merchant override always wins |
| 2 | Co-purchase | Top `confidence_score` from `CoPurchaseMatrix`, join `InventoryShield` | Enough pairs with `pair_count >= min_support` (suggest **5** so badges are not “100% of 1 buyer”) |
| 3 | Catalog / taxonomy | Same Shopify taxonomy category / collection, exclude self + gift-card tags | Cold start / new SKU |
| 4 | Bestseller | `ProductCatalog.sales_count` in-stock | Last fill so the widget is never empty |

CBB live extra (we should keep as merchant toggles, not drop silently): **Exclusive Manual** mode; **Global** pin list; outbound exclusion (gift cards, warranties).

### Scores (no neural net required)

For product A recommending B:

* `pair_count(A,B)` = orders containing both  
* `confidence(A→B) = pair_count(A,B) / orders_containing(A)`  
* `lift(A→B) = confidence(A→B) / P(B)`  
* Rank by `confidence`, break ties with `lift` then `pair_count`  
* Optional filters: rec price between **0.2× and 3×** of A; same vendor optional; exclude `gift_card`

### Explainer badge (the USP) — also no LLM

Fill a **template from the same numbers**:

* `"{{pct}}% of customers who bought this also bought {{title}}"` where `pct = round(100 * confidence)` and `pair_count >= 5`  
* Else `"Often bought together"`  
* Else hide the badge (do not invent a percent)

That is the LimeSpot/CBB gap: they have the stats in admin; they do not print them on the storefront.

---

## 3. Where an LLM actually belongs (offline / rare)

| Job | LLM? | Why |
| :--- | :---: | :--- |
| Pick the 3 PDP items | **No** | Latency 300ms–2s; cost scales with traffic; worse than co-purchase for FBT |
| Storefront explainer percent | **No** | Hallucinates rates; stats already exist |
| Chat “shopping assistant” as the recs product | **No** | Saturated; competes with Sidekick |
| Extract attributes from title/body (skin type, compatibility, color) | **Yes, batch** | Feeds Tier 3 vertical templates; once per product create/update |
| Compile Fashion / Beauty / Electronics rule JSON | **Yes, once** | Merchant picks a vertical; LLM writes filter specs, humans can edit |
| Admin “why this pair?” paragraph | **Yes, on click** | 1 merchant action, not 50k shoppers |
| Nightly QA: gift cards in recs, same-item dupes | **Optional** | Cheap classifier / rules first |
| VisualAI look-alike | **Later** | Nosto already sells it; image embeddings ≠ v1 |

### Offline catalog pass (recommended)

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
| text-embedding-3-small | $0.02 / M tokens | OpenAI |

Token assumptions for an online “ask the model to pick 3 products” call: **~600 input + ~100 output** tokens (catalog stub + instruction). Real catalogs are larger → **these are lower bounds**.

### Per shop / month (50k widget views)

| Path | What runs on the PDP request | Est. LLM/embed $ | Latency | Fit on $19 plan? |
| :--- | :--- | ---: | :--- | :--- |
| **A. Waterfall + KV cache** | KV get | **~$0** | &lt;50 ms cached | Yes — this is v1 |
| **B. Offline LLM enrich** (2k SKUs / mo) | Still KV get; LLM only on product webhooks | **~$0.30** (mini, 400 in / 150 out × 2k) | PDP unchanged | Yes |
| **C. Embeddings cold-start** (CF bge-m3 + Vectorize) | KV first; ~10% miss → vector query | **&lt;$0.02** | +20–80 ms on miss | Optional v1.5 |
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

1. **v1 engine = CBB math + cache + printed confidence.** Call it “AI” in App Store copy the same way CBB does (association rules). Do not put “powered by GPT” on the widget.  
2. **LLM budget: batch catalog JSON + optional admin explain.** Default model: gpt-4o-mini or Cloudflare `llama-3.2-3b` / `glm-4.7-flash` for structured extract. Cap: **&lt;$0.50 / shop / month**.  
3. **Never block PDP render on an LLM.** Timeout = empty widget = bounce.  
4. **VisualAI / gpt-5 ranking = Scale hypothesis**, not the $0–$49 wedge.  
5. Explainer percents **must** be computed from `CoPurchaseMatrix`, with a minimum support — otherwise the USP becomes a lie and an App Store risk.

---

## 6. Open items (not claimed as fact)

* Exact min_support / min_confidence for fashion vs electronics (tune after 50 beta stores).  
* Whether Shopify Search & Discovery already covers Tier 3 well enough that we should skip embeddings in v1.  
* Image-embedding cost for VisualAI (Workers AI ResNet is priced per million images — not modeled here).

---
*File: `ALGORITHM_AND_LLM_COST.md` · prices will move; re-check Cloudflare + OpenAI pages before a board cost slide.*
