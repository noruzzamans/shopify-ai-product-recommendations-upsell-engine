# Frozen decisions
**Last verified:** 21 September 2026  
**Rule:** Product/architecture conflicts → this file + [COMPARISON.md](COMPARISON.md) win (live competitor numbers stay in COMPARISON). Enamul memo is the original brief only.

| ID | Decision | Status | Last verified | Do not write |
| :--- | :--- | :--- | :--- | :--- |
| D1 | Price hypothesis **$0 / $19 / $49 / $99**. Caps = attributed `_cr_src` GMV. Scale = **no GMV cap**. Cap hit → upgrade request, widget stays on | Frozen | 21 Sep 2026 | Enamul $0/99/249/499; “unlimited fair capped” |
| D2 | Beat **CBB FBT**, not Julius. Waterfall: Manual → co-purchase → **complement map** → bestseller | Frozen | 21 Sep 2026 | Same-leaf category as FBT; Julius AI |
| D3 | Storefront recs are **not** an LLM call. Optional LLM = offline JSON / one vertical map draft | Frozen | 21 Sep 2026 | GPT on PDP; “powered by GPT” on the widget |
| D4 | Recs transport: `$app.recs_top3` metafield, else signed **App Proxy**. Public `GET /api/recs?shop=` forbidden | Frozen | 21 Sep 2026 | Unauthenticated recs API |
| D5 | Discount = Shopify **Discount Function** (`cart.lines.discounts.generate.run`, `write_discounts`) | Frozen | 21 Sep 2026 | “Automatic discount” REST as the FBT discount |
| D6 | Confidence derived: `pair_count / ProductOrderStats`. Percent badge iff pair≥5 **and** orders(A)≥20. Product-level, not variant | Frozen | 21 Sep 2026 | Stored-only `confidence_score`; “87% this size” |
| D7 | Inventory: `inventory_item_id` map; hide at render iff tracked+DENY+qty≤0. No `InventoryShield` table | Frozen | 21 Sep 2026 | Webhook has product_id; hide CONTINUE/untracked |
| D8 | **MVP ship list:** Phase 1–7 + Function + billing. Cart drawer, carousel, checkout bump, post-purchase = later. VisualAI/A/B = Scale hypothesis | Frozen | 21 Sep 2026 | STRATEGY old 4-phase / 8–9 week calendar; README 12-phase as the ship list |
| D9 | Admin API pin **`2026-07`** (latest stable). Bump each quarter. Not `2026-10` RC, not `2026-01` | Frozen | 21 Sep 2026 | Pin 2025-07 / 2026-01 as “current” |
| D10 | Webhook idempotency: persist **`X-Shopify-Event-Id`** (same merchant action — do not double-count pairs) **and** **`X-Shopify-Webhook-Id`** (per-delivery skip). [Official](https://shopify.dev/docs/apps/build/webhooks/verify-deliveries): delivery duplicates → Webhook-Id; Event-Id correlates one action across subscriptions | Frozen | 21 Sep 2026 | Dedup on Webhook-Id only if that would double-count retries of the same event |
| D11 | Install order mine = **last 60 days** (default Admin access). `read_all_orders` = Partner approval, not v1 | Frozen | 21 Sep 2026 | “60–90 days” as default |
| D12 | Admin UI = **Polaris web components** (React Router app-home default). Storefront widgets stay Liquid + vanilla custom elements | Frozen | 21 Sep 2026 | Polaris React as the admin system |
| D13 | App Store submit = **BFS-ready**. BFS badge = **post-launch** (install/review thresholds). Lighthouse: app must not drop storefront score **>10 points** — not “100/100” | Frozen | 21 Sep 2026 | Phase 12 = BFS on launch day |
| D14 | Explainer badge is a **hypothesis** (CTR not measured). Category demand is CBB/Wiser ratings, not this USP | Frozen | 21 Sep 2026 | “73% CTR lift” as a finding |
| D15 | Listing copy: association-rule engine. “AI” like CBB uses the word. No fabricated stats | Frozen | 21 Sep 2026 | LLM social-proof sentences |
| D16 | **Smart Stock Swap:** If a rec product is OOS at render time (`tracked + DENY + available <= 0`), swap in next in-stock candidate from Tier 3/4 to keep bundle intact | Frozen | 21 Sep 2026 | Leave blank slot or collapse 3-item bundle |
| D17 | **2-Min Catalog Scanner:** Background async LLM worker auto-classifies store vertical (Fashion, Beauty, Home, Electronics, Food) and initializes complement rules | Frozen | 21 Sep 2026 | Force merchant manual rule setup on Day 1 |
| D18 | **Cold-Start pgvector:** Products with 0 order history use PostgreSQL `pgvector` text embeddings for style/semantic matching before co-purchase data builds | Frozen | 21 Sep 2026 | Show completely unrelated generic bestsellers |
| D19 | **Localization & Markets:** Multi-currency formatting via Shopify Markets; Explainer badge translations via Shopify Locales | Frozen | 21 Sep 2026 | English-only single currency storefront |

**Repo:** GitHub remote is **public** (`noruzzamans/shopify-ai-product-recommendations-upsell-engine`). Make private before a real product bet — not done in this pass.

**Where to read more:** engine/cost → [ALGORITHM_AND_LLM_COST.md](ALGORITHM_AND_LLM_COST.md); schema/phases → [MASTER_ARCHITECTURE_AND_ROADMAP.md](MASTER_ARCHITECTURE_AND_ROADMAP.md); competitor numbers → [COMPARISON.md](COMPARISON.md).
