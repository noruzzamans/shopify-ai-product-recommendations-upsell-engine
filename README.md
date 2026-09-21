# Shopify AI Product Recommendations & Upsell Engine

Research pack (not a coded app). **Conflicts:** [DECISIONS.md](DECISIONS.md) + [COMPARISON.md](COMPARISON.md) win.

## Leadership

| Member | Role |
| :--- | :--- |
| এনামুল ভাই | Team Lead & Strategic Director |
| নুরুজ্জামান রুবেল | Lead Engineer & Product Manager |

## Index

### Frozen
* [DECISIONS.md](DECISIONS.md) — decisions, status, last-verified date
* [COMPARISON.md](COMPARISON.md) — live competitor prices, ratings, Shopify surfaces (Sept 2026)

### Architecture & strategy
* [ALGORITHM_AND_LLM_COST.md](ALGORITHM_AND_LLM_COST.md) — waterfall, LLM (offline only), cost, schema/proxy freeze
* [MASTER_ARCHITECTURE_AND_ROADMAP.md](MASTER_ARCHITECTURE_AND_ROADMAP.md) — extensions, D1, phases (implementation hypothesis)
* [PROJECT_STRATEGY_AND_DATA_ANALYSIS.md](PROJECT_STRATEGY_AND_DATA_ANALYSIS.md) — positioning; unsourced TAM/ARR stripped
* [ENGINEERING_STANDARDS_AND_PATTERNS.md](ENGINEERING_STANDARDS_AND_PATTERNS.md) — coding patterns; per-widget gzip; webhook p99 &lt; 500ms
* [ENAMUL_SUGGEST_SHOPIFY_PRODUCT_RECOMMENDATIONS_COMPETITIVE_STRATEGY.md](ENAMUL_SUGGEST_SHOPIFY_PRODUCT_RECOMMENDATIONS_COMPETITIVE_STRATEGY.md) — original memo; COMPARISON wins on conflict

### Competitor teardowns (`competitors/`)
* [LIMESPOT.md](competitors/LIMESPOT.md)
* [CBB_FREQUENTLY_BOUGHT_TOGETHER.md](competitors/CBB_FREQUENTLY_BOUGHT_TOGETHER.md) (was misnamed `JULIUS.md`)
* [NOSTO.md](competitors/NOSTO.md)
* [WISER.md](competitors/WISER.md) — listing + demo only

**MVP (D8):** MASTER phases 1–7 + Discount Function + billing. Drawer / checkout / post-purchase later. BFS after launch.
