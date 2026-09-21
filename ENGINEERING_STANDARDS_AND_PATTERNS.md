# 💎 Engineering Principles, Structural Patterns & Quality Standards

আমাদের শপিফাই অ্যাপটি যেন বিশ্বমানের (World-Class), অত্যন্ত দ্রুতগতির এবং দীর্ঘমেয়াদে স্কেলেবল হয়—সেজন্য পুরো টিম এই আর্কিটেকচার, ডিজাইন প্যাটার্ন ও ইঞ্জিনিয়ারিং মূলনীতিগুলো কঠোরভাবে অনুসরণ করবে।

---

## Terminology: Principles vs. Patterns vs. Checklists

In professional software engineering, our architecture is divided into four distinct layers:
1. **Core Principles (The "Why"):** Foundational philosophies and laws of software design (e.g., SRP, Co-location, Separation of Concerns, Postel's Law).
2. **Design Patterns (The "How"):** Proven structural blueprints used to solve concrete code problems (e.g., Controller-View, Fast-ACK & Async Offload, Declarative Gating).
3. **Engineering Checklists (The "What to Verify"):** Step-by-step verification rules applied before committing code to ensure quality and prevent regressions.
4. **Code Smells (The "What to Avoid"):** Surface symptoms indicating structural design flaws or principle violations that require refactoring.

---

# Part I: Core Software Engineering Principles (মূলনীতিসমূহ)

### 1. Co-location Principle (Locality of Behavior)
- **Concept:** Code and assets that change together should live together.
- **In Our App:** 
  - FBT widget sub-components live inside `app/components/fbt/` (`VariantDropdown.jsx`, `BundleCheckbox.jsx`, `BundlePriceSummary.jsx`) rather than dumped into a generic global components folder.
  - Smart Cart Drawer sub-components live inside `app/components/cart-drawer/` (`TierProgressBar.jsx`, `InCartCrossSell.jsx`, `DrawerFooter.jsx`).
- **Rule:** *Start local. Only promote to global when 2+ independent consumers require it.*

### 2. Separation of Concerns (SoC)
- **Concept:** Every distinct layer of the app should handle one aspect of functionality.
- **In Our App:**
  - **Server / Controller Layer (`routes/app.*.jsx`):** Fetches data (`loader`), processes mutations (`action`), checks billing plans.
  - **Presentation Layer (`*View.jsx`):** Renders Shopify Polaris UI, handles user interaction, formats badges.
  - **Database Layer (`app/db/*.js`):** Interacts with Cloudflare D1 edge database (`sessions.js`, `webhooks.js`, `analytics.js`).
  - **Engine Services (`app/services/*`):** Executes 4-tier waterfall recommendation logic, co-purchase scoring, and zero-stock webhook events.
  - **Storefront Client Engine (`extensions/theme-extension/assets/*`):** Native Liquid + Vanilla JS Custom Elements (< 5KB, 0 dependencies).
  - **Checkout Extensions (`extensions/checkout-upsell/src/*`):** Built with `@shopify/ui-extensions` and `root.createComponent` (Native UI Extension pattern).

### 3. Single Responsibility Principle (SRP — from SOLID)
- **Concept:** A module or component should have only one reason to change.
- **In Our App:**
  - `waterfall.server.js` changes *only* if the recommendation fallback ordering logic changes.
  - `zero-stock.server.js` changes *only* if out-of-stock webhook handling changes.
  - `BundleExplorerView.jsx` changes *only* if the algorithm debugger UI changes.

### 4. DRY (Don't Repeat Yourself) vs. AHA (Avoid Hasty Abstractions)
- **Concept:** Duplicate logic should have a single source of truth (DRY), but premature abstraction is more costly than temporary duplication (AHA).
- **In Our App:**
  - **Shared (DRY):** Global components used across admin: `<MetricCard />`, `<StatusBadge />`, `<PlanGate />`, and `@utils/formatCurrency`.
  - **Local (AHA):** Discount pill formatting for FBT bundles is kept local to `app/components/fbt/`, avoiding an over-engineered universal badge that tries to format cart drawers, checkout bumps, and FBT all at once.

### 5. Idempotency Principle (Webhook Deduplication)
- **Concept:** An operation can be executed multiple times without changing the result beyond the initial execution.
- **In Our App:**
  - **Webhook Deduplication & Idempotency Pattern:** Shopify retries webhooks on network drops. We record the `X-Shopify-Webhook-Id` header in Cloudflare D1 `WebhookDeliveries` table (`claimWebhookDelivery`). Repeated webhooks return HTTP 200 immediately without re-calculating co-purchase graphs or duplicating analytics logs.
  - **In-Place Inventory Update:** Syncing inventory levels multiple times updates the existing product's `is_available` flag idempotently.

### 6. Fast-ACK & Asynchronous Offload Pattern (<25ms Webhooks)
- **Concept:** Acknowledging webhook requests within milliseconds while offloading heavy AI/ML calculations to background execution contexts.
- **In Our App:**
  - Shopify requires webhooks to return HTTP 200 within 5 seconds or risks endpoint throttling.
  - When `orders/create` or `inventory_levels/update` fires, Cloudflare Worker verifies the HMAC signature, checks `claimWebhookDelivery` in D1, returns HTTP 200 in **<25ms**, and offloads co-purchase graph updates asynchronously.

### 7. Cognitive Load Minimization (Information Architecture)
- **Concept:** Software interfaces should minimize the mental effort required for merchants to understand and configure settings.
- **In Our App:**
  - Instead of LimeSpot’s external dashboard plus a long Personalization / Optimization module list, or Nosto’s three-cloud enterprise nav, our app groups features into 4 clean hubs:
    1. **Overview:** Direct ROI metrics ($ Made, AOV Lift, 5-Stage Funnel).
    2. **Recommendation Hub:** 1-Click toggles and live visual customizer for PDP, Cart Drawer, Checkout, and Carousels.
    3. **Bundle Explorer:** Search any product and visually inspect / override AI pairings.
    4. **Settings:** Zero-stock shield, plan tier, and theme embed controls.

### 8. Accessibility (a11y) & Semantic HTML First
- **Concept:** Software interfaces must be usable by everyone, including screen readers and keyboard users (WCAG AA).
- **In Our App:**
  - Storefront FBT checkboxes and variant dropdowns are fully keyboard-navigable (`Tab`, `Space`, `Enter`).
  - Color contrast for all CTA buttons and badges meets WCAG AA 4.5:1 minimum ratios.
  - Screen readers are provided with descriptive `aria-live="polite"` announcements when bundles are added to cart.

### 9. YAGNI & Dead Code Elimination (অব্যবহৃত কোড বর্জন নীতি)
- **Concept:** *"You Aren't Gonna Need It."* Code that is unreachable, deprecated, commented-out, or superseded by newer architecture must be deleted immediately.
- **Rule:** *Trust Git history for archival. Never leave zombie components, dead routes, or commented-out code blocks in the active codebase.*
- **Chesterton's Fence:** *Before deleting any defensive check or fallback rule, understand why it was introduced.* Verify edge cases and historical tests first.

### 10. Dependency Inversion Rule (Clean Architecture)
- **Concept:** High-level business rules must never depend on low-level delivery mechanisms. Both must depend on abstractions. Dependencies must strictly point inward.
- **In Our App:**
  - **Pure Business Logic Isolation:** `@services/recs-engine/*` contains pure algorithmic logic (collaborative filtering, scoring, fallback cascade) and NEVER imports React, Polaris, or Storefront UI state.
  - **Server-Client Boundary:** Server-only modules (`*.server.js/ts`) are strictly isolated to `loader` and `action`. They must never be imported into client components (`export default function`), preventing server credentials, database connections, and secrets from leaking into client bundles.

### 11. Postel's Law (The Robustness Principle / Defensive Ingestion)
- **Concept:** *"Be conservative in what you send, be liberal in what you accept."*
- **In Our App:**
  - **Defensive Ingestion:** Shopify product and order payloads vary wildly across stores (missing product images, null vendor, zero variants, empty line-item SKUs, deleted collection IDs).
  - Our API handlers and storefront renderers must NEVER throw uncaught `TypeError` on nullish properties. Always use optional chaining (`product?.images?.[0]?.url`), fallback SVG placeholders, and strict type coercion (`Number(price) || 0`).
- **Rule:** *External payloads are untrusted and unpredictable. Ingest liberally with safe fallbacks; emit conservatively with strictly validated rows.*

---

# Part II: Architectural & UI/UX Design Patterns (কাঠামোগত প্যাটার্ন)

### 12. Controller-View Pattern (React Router v7)
- **Concept:** Separating backend request coordination from UI rendering.
- **In Our App:** The route file (`routes/app.bundle-explorer.jsx`) acts as the Controller orchestrating `loader` and `action`, while purely presentational views (`BundleExplorerView.jsx`) render the UI declaratively.

### 13. Barrel Pattern (Façade Pattern — Gang of Four)
- **Concept:** A single entry point (`index.js`) that re-exports multiple sub-modules, hiding internal directory complexity behind a unified façade.
- **In Our App:** Consumers write `import { MetricCard, StatusBadge, PlanGate } from "@components";` without needing to know internal directory structures.

### 14. Declarative Feature Gating (`<PlanGate />`) Pattern
- **Concept:** Seamlessly communicating plan limits without crashing or throwing 404s.
- **In Our App:** Instead of hiding advanced features (e.g. checkout UI or VisualAI) or returning an error, Free / Starter users see the UI with a soft blur and an upgrade banner. **A/B testing is not a unique gap:** LimeSpot Max already has A/B/n; Nosto has a statistical engine; CBB FBT does not.

### 15. Storefront Isolation Pattern (Shadow DOM / Strict BEM)
- **Concept:** Storefront widgets must never conflict with merchant themes or break theme styles.
- **In Our App:**
  - Storefront CSS uses strict BEM prefixing (`.rec-widget__*`) or Shadow DOM encapsulation.
  - Widget styles are completely self-contained so merchant CSS resets never corrupt bundle layouts.

### 16. Edge-to-Local Currency & Timezone Fidelity Pattern
- **Concept:** Storing monetary values and timestamps in unified base units, but rendering in store currency and local timezone.
- **In Our App:** Prices are calculated in cents/base currency and formatted on the storefront using Shopify's native currency formatter (`Shopify.formatMoney`). Timestamps are stored as UTC Unix integers and formatted according to the merchant store's IANA timezone.

---

# Part III: Pre-Flight Developer Checklist (কোড করার পূর্বে চেকলিস্ট)

Before adding a new feature or refactoring code in any of the 12 Micro-Phases, run through this 6-step checklist:

| Step | Focus | Question to Ask Yourself | Codebase Standard |
|---|---|---|---|
| **1** | **Placement** | Where does this code belong? | Route (Controller) vs `app/components/` (View) vs `app/services/` (Engine) |
| **2** | **Reuse** | Is this used in 1 place or 3+ places? | If 1 place: Keep it local. If 3+ places: Promote to `@components` or `@utils`. |
| **3** | **Cleanliness** | Are there duplicate helpers, dead imports, or zombie code? | Run `npx tsc --noEmit` and delete all unreachable code. Follow YAGNI. |
| **4** | **UX & Fidelity** | Is data immediately formatted for the merchant? | Format in store currency and timezone, zero UI clipping, mobile-responsive. |
| **5** | **Performance** | Will this slow down storefront or edge execution? | **Targets (not measured in this research pack):** storefront JS budget < 5KB *per widget*; serve rec JSON from cache. D1 SQL-time at the primary can be low-ms; it is not a global sub-15ms SLO. |
| **6** | **Integrity** | Did I break any existing functionality? | Run automated unit tests and `npm run build` before deploying or pushing. |

---

# Part IV: Code Smells & Anti-patterns to Avoid (বর্জনীয় কোড স্মেলসমূহ)

| Code Smell | Diagnostic Symptom | Violated Principle | Architectural Cure |
|---|---|---|---|
| **1. Dead Code (Zombie Code)** | Unreachable functions, obsolete components, or commented-out blocks left in files. | **YAGNI** (Principle 9) | Delete unreachable code and obsolete routes immediately. Trust Git history for archival. |
| **2. Fat File (God Object)** | A single route, service, or component exceeding 800+ lines with multiple mixed concerns. | **Single Responsibility** (Principle 3) | Apply Controller-View separation and co-located sub-views (e.g., split FBT into `VariantDropdown`, `BundleCheckbox`, etc.). |
| **3. Duplicated Code (Copy-Paste)** | Identical badge styling, price formatting, or error handling copied across files. | **DRY** (Principle 4) | Promote repeated logic to global `@components` (`<MetricCard />`, `<StatusBadge />`) or `@utils`. |
| **4. Shotgun Surgery** | A single schema or pricing tweak requires editing 6+ separate, disconnected files. | **Separation of Concerns** (Principle 2) | Centralize business logic into dedicated edge services (`@services/*`) and database models (`app/db/*`). |
| **5. Magic Numbers & Hardcoded Strings** | Raw inline hex colors (`#008060`), hardcoded discount quotas (`15`), or plan prices typed directly in JSX. | **Design Token First** & **Single Source of Truth** | Use Shopify Polaris design tokens, CSS custom properties, and central plan constants in `billing.server.js`. |
| **6. Speculative Generality** | Over-abstracted helper functions or universal wrappers created for hypothetical future use cases that don't exist yet. | **AHA over DRY** (Principle 4) | Keep logic local first. Only promote to shared utilities when 2+ independent consumers explicitly require it. |

---
*ডকুমেন্টটি সফলভাবে সংরক্ষিত হয়েছে:* `ENGINEERING_STANDARDS_AND_PATTERNS.md`
