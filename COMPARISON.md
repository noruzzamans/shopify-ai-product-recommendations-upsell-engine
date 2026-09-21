# Frozen competitor comparison
**Snapshot date:** September 2026  
**Rule:** If STRATEGY, MASTER, or Enamul’s memo disagree with this file or [DECISIONS.md](DECISIONS.md), **those two win** (this file = competitor numbers; DECISIONS = our product freeze). README is an index only.  
**Sources:** live App Store listings and admin/storefront teardowns in `competitors/`.

---

## Who we actually studied

| Name in older docs | Real product | Teardown file | Depth |
| :--- | :--- | :--- | :--- |
| LimeSpot | LimeSpot AI Bundles & Upsells | [competitors/LIMESPOT.md](competitors/LIMESPOT.md) | Live admin + designer |
| Julius | **Not Julius AI.** Code Black Belt · Frequently Bought Together | [competitors/CBB_FREQUENTLY_BOUGHT_TOGETHER.md](competitors/CBB_FREQUENTLY_BOUGHT_TOGETHER.md) | Live admin |
| Wiser | Wiser - Upsell & Cross Sell | [competitors/WISER.md](competitors/WISER.md) | Listing + demo storefront only (admin waterfall not torn down) |
| Nosto | Nosto \| AI Search & Discovery | [competitors/NOSTO.md](competitors/NOSTO.md) | Live `my.nosto.com` |

Not in this pack (named by LimeSpot chat as a migration target): **Rebuy**. Shopify’s free native recs (**Search & Discovery**) also not torn down. Post-purchase **incumbents not torn down:** ReConvert, AfterSell, Zipify — they occupy the single post-purchase app slot.

---

## Live listing snapshot (September 2026)

| | LimeSpot | CBB FBT | Wiser | Nosto |
| :--- | :--- | :--- | :--- | :--- |
| App Store | [limespot](https://apps.shopify.com/limespot) | [frequently-bought-together](https://apps.shopify.com/frequently-bought-together) | [recommended-products-wiser](https://apps.shopify.com/recommended-products-wiser) | [nosto-personalization-for-shopify](https://apps.shopify.com/nosto-personalization-for-shopify) |
| Rating | 4.6 ★ (507) | 4.9 ★ (1,200+) | 4.9 ★ (559) | 4.7 ★ (61) |
| Built for Shopify | No (not recorded) | Yes | Not recorded | No |
| Live price | **Turbo** $0 (10 orders) / $9.99 → up to ~$400 by order volume. **Max** $50–$1,700 by store revenue | $0 (3 manual bundles, no AI) / $14.99 (50 orders) / $19.99 (500) / $39.99 unlimited | $0 (≤50 orders) / $9 / $19 / $49 (up to 500 orders) | “Free to install”; billed outside Shopify; teardown range $500–$2,500+/mo or % of GMV — not a public SKU |
| Admin | External `app.limespot.com` | Embedded Shopify admin | Not fully reverse-engineered | External `my.nosto.com` |
| FBT / bundles | Yes | Yes (core) | Yes | Yes |
| 4-tier waterfall | Complex box cascade + FBT fallback | **Yes** (Manual → Auto AI → Global → Random by collection) | Unknown (admin not torn down) | Campaign + fallback fill/replace |
| Slide cart drawer | No (theme cart conflicts warned) | No | **Yes** (demo) | No |
| Checkout UI blocks | Yes (9 blocks) | No | Yes (demo) | Recs on checkout **Shopify Plus only** (per Nosto wizard) |
| 1-click post-purchase (add to original order) | **Yes** — Settings → Checkout → Post-purchase page; card/Shop Pay only; default currency; $0.50 min; 120s timer | No | Yes (demo) | Yes (native post-purchase module) |
| Thank-you / order-status blocks | Yes | No | Yes (demo) | Thank-you slot yes |
| Storefront “why this item” explainer | No | No (Bundle explorer is admin-only) | No | No |
| A/B testing | **Yes** — A/B/n on Max / Optimization | No | Not verified | **Yes** — statistical engine |
| Inventory / OOS | Live preview recommended “The Out of Stock Snowboard” | Outbound exclusion + widget disable | Not verified | Merchandising / stock rules |
| Onboarding | Industry pick (12 verticals) + billing; then 7-step guide | 3-step wizard (~60s) + theme embed deep-link | Spending-limit approval; card-on-file friction | Sales-led; no self-serve |

Discarded numbers (do not reuse in STRATEGY/MASTER): LimeSpot “$500–$1,200/mo” as the SMB price; LimeSpot “30–45 day setup” for Turbo; Julius 8% share / $3M ARR; Wiser 50% 30-day churn; Enamul packaging $0 / $99 / $249 / $499 (kept only as an old memo).

---

## Our frozen decisions (from STRATEGY + MASTER, not Enamul)

| Decision | Frozen value | Notes |
| :--- | :--- | :--- |
| Our price hypothesis | **$0 / $19 / $49 / $99** | GMV caps on Free/Starter/Growth are **attributed** line items (`_cr_src`), not all store sales. Scale = **no GMV cap** (do not say “unlimited fair capped”). Cap hit → upgrade request, widget stays on |
| FBT benchmark to beat | **CBB**, not Julius AI | Copy waterfall + inline variants + 5-stage funnel |
| Cart drawer | Wiser-inspired, **later** | Separate gzip budget; not in the FBT 5KB envelope |
| Checkout product offers | Plus-gated | **Not** the $49 Growth headline for SMB |
| 1-click 120s upsell | Post-purchase extension | One app slot; ReConvert/AfterSell/Zipify incumbents — optional, not default Growth |
| Explainer badges | Storefront USP | Percent only if pair≥5 **and** orders(A)≥20; product-level, not variant |
| Zero-stock shield | Render-time + inventory_item map | Webhook payload has no product_id; CONTINUE/untracked must not hide |
| Recs transport | Product metafield or App Proxy | Public `GET /api/recs?shop=` forbidden |
| A/B testing | Not unique | LimeSpot Max + Nosto already sell it |
| VisualAI | Nosto has it; Scale-tier hypothesis only | Not a researched v1 differentiator |

---

## Shopify surfaces (do not flatten)

| Surface | Target / slot | Can add line to original order? |
| :--- | :--- | :--- |
| Checkout block | `purchase.checkout.block.render` | Cart/checkout offer; product offers on checkout steps are Plus-gated |
| Post-purchase page | `Checkout::PostPurchase::ShouldRender` + `Render` | **Yes** (signed changeset). One app owns Settings → Checkout → Post-purchase page |
| Thank-you page | `purchase.thank-you.block.render` | **No** — new checkout / content only |
| Order status | `customer-account.order-status.block.render` | Customer Account UI extension, not the checkout package |

---

## Unsourced claims (appendix — not findings)

These appear in Enamul’s memo and were copied into STRATEGY. They have **no URL, date, or method** in this repo:

- Global recs TAM $2.3B / 18% YoY
- LimeSpot 28% share / ~$18M ARR; Wiser 22% / $12M; Julius 8% / $3M
- 2x–5x conversion lift; 250–400% ROI
- Wiser ~50% drop in 30–60 days
- AI-search orders 15x since January 2025
- 12-month $250K MRR / 5,000 stores

Do not put these in executive “data-driven justification” until cited.

---
*Canonical snapshot for the research pack. Update the date when any live listing is re-checked.*
