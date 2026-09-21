# 💎 Shopify AI Product Recommendations & Upsell Engine — Master Architecture & Roadmap
**টিম লিড (Team Lead & Strategy):** এনামুল ভাই  
**লিড ইঞ্জিনিয়ার ও প্রোডাক্ট ম্যানেজার (Lead Engineer & Product Manager):** নুরুজ্জামান রুবেল  
**স্ট্যাটাস:** চূড়ান্ত মাস্টার ব্লুপ্রিন্ট (Final Master Blueprint)  
**ভার্সন:** ১.৩ (সেপ্টেম্বর ২০২৬) — B-রিভিউ: Discount Function, কো-পারচেজ কাউন্ট, অর্ডার হাইজিন, ইনভেন্টরি ম্যাপ, অ্যাট্রিবিউশন, App Proxy  
**নোট:** অ্যাপের অফিশিয়াল নাম বোর্ড মিটিংয়ে চূড়ান্ত হবে। আপাতত টেকনিক্যাল স্পেক্সে এটিকে **[আমাদের অ্যাপ / The App]** হিসেবে উল্লেখ করা হয়েছে।  
**লাইভ স্ন্যাপশট:** [COMPARISON.md](COMPARISON.md) জিতবে যেখানে এই ফাইল পুরনো নাম/সারফেস/প্রাইস লেখে। অ্যালগরিদম/LLM/খরচ: [ALGORITHM_AND_LLM_COST.md](ALGORITHM_AND_LLM_COST.md)। এই ডক ইমপ্লিমেন্টেশন হাইপোথিসিস; কম্পিটিটর ফোল্ডার প্রাইমারি রিসার্চ।

---

## 👥 টিম লিডারশিপ ও গভর্নেন্স (Leadership & Execution Roles)

প্রজেক্টের সুষ্ঠু বাস্তবায়ন ও সফলতার জন্য টিম রোলস সুস্পষ্টভাবে নির্ধারিত:

| টিম মেম্বার | ভূমিকা (Official Role) | দায়িত্ব ও কার্যপরিধি (Core Responsibilities) |
| :--- | :--- | :--- |
| **এনামুল ভাই** | **Team Lead & Strategic Director** | • **কোর ভিশন ও দিকনির্দেশনা:** ইনিশিয়াল প্রজেক্ট স্ট্র্যাটেজি গাইডলাইন প্রদান এবং হাই-লেভেল প্রোডাক্ট ভিশন পরিচালনা।<br>• **স্কোপ ও প্রায়োরিটাইজেশন:** কোন মার্কেট সেগমেন্ট টার্গেট করা হবে এবং কোন কোন ফিচার আগে আসবে তা চূড়ান্ত অনুমোদন।<br>• **স্ট্র্যাটেজিক রিভিউ ও মেন্টরশিপ:** রিসার্চ, সিস্টেম ডিজাইন ও ইঞ্জিনিয়ারিং মাইলস্টোন নিয়মিত যাচাই এবং কৌশলগত ফিডব্যাক প্রদান।<br>• **বিজনেস ও জিটিএম (GTM):** প্রোডাক্টের প্রাইসিং পলিসি, মার্কেট-ফিট এবং বিজনেস অ্যালাইনমেন্ট নিশ্চিতকরণ। |
| **নুরুজ্জামান রুবেল** | **Lead Engineer & Product Manager (PM)** | • **প্রোডাক্ট ও কম্পিটিটর রিসার্চ:** এনামুল ভাইয়ের স্ট্র্যাটেজিক গাইডের ওপর ভিত্তি করে শীর্ষ ৪ প্রতিদ্বন্দীর (LimeSpot, Wiser, CBB Frequently Bought Together, Nosto) মেকানিক্স ও দুর্বলতার বিস্তারিত রিভার্স-ইঞ্জিনিয়ারিং ও সুযোগ চিহ্নিতকরণ।<br>• **সিস্টেম আর্কিটেকচার প্রণয়ন:** শপিফাই নেটিভ এক্সটেনশন স্যুট, ক্লাউডফ্লেয়ার এজ আর্কিটেকচার (Cloudflare Workers + D1) এবং ৪-টিয়ার ওয়াটারফল রিকমেন্ডেশন ইঞ্জিনের টেকনিক্যাল ডিজাইন।<br>• **ফুল-স্ট্যাক সফটওয়্যার ডেভেলপমেন্ট:** React Router v7, Shopify Polaris, Native Vanilla JS Custom Elements (< ৫KB), Cloudflare Edge Workers ও শপিফাই ওয়েবহুকের সম্পূর্ণ হ্যান্ডস-অন কোডিং ও ডেভেলপমেন্ট।<br>• **ইঞ্জিনিয়ারিং এক্সিলেন্স ও কোয়ালিটি কন্ট্রোল:** [ENGINEERING_STANDARDS_AND_PATTERNS.md](ENGINEERING_STANDARDS_AND_PATTERNS.md) অনুযায়ী বিশ্বমানের কোড স্ট্যান্ডার্ড, ১০০/১০০ লাইটহাউস স্কোর ও "Built for Shopify" কমপ্লায়েন্স বাস্তবায়ন। |

---

## ১. নির্বাহী পরিচিতি ও প্রোডাক্ট ভিশন (Executive Vision)

আমাদের অ্যাপটি হলো শপিফাই ইকোসিস্টেমের পরবর্তী প্রজন্মের অল-ইন-ওয়ান **AI Product Recommendations, Smart Cart & Upsell Engine**। 

বাজারের চারটি প্রতিদ্বন্দীর লাইভ টিয়ারডাউনের পর (LimeSpot ও CBB FBT: ফুল অ্যাডমিন; Nosto: `my.nosto.com`; Wiser: লিস্টিং + ডেমো স্টোরফ্রন্ট — অ্যাডমিন ওয়াটারফল এখনো ভাঙা হয়নি) যে গ্যাপ দাঁড়ায়:
* **ছোট মার্চেন্টরা (SMBs):** সাধারণ ও সস্তা অপশন খোঁজে কিন্তু কার্যকর AI রিকমেন্ডেশন পায় না।
* **বড় মার্চেন্টরা (Plus/Enterprise):** দামী অ্যাপ ব্যবহার করে কিন্তু অতিরিক্ত মাসিক খরচ ও স্লো পেজ স্পিডে ভোগে।
* **আমাদের সমাধান:** সাশ্রয়ী মূল্যে এন্টারপ্রাইজ গ্রেড AI পার্সোনালাইজেশন ও আল্ট্রা-ফাস্ট লাইটওয়েট এক্সপেরিয়েন্স।

---

## ২. শপিফাই এক্সটেনশন আর্কিটেকচার (Shopify Extensions Architecture)

বিশ্বমানের শীর্ষস্থানীয় (World-Class Tier-1) শপিফাই অ্যাপগুলোতে যেভাবে পেজ স্পিড অক্ষুণ্ণ রেখে এক্সটেনশন লোড করা হয়, আমাদের এক্সটেনশন স্যুটটি হুবহু সেই নেটিভ আর্কিটেকচার কঠোরভাবে অনুসরণ করে তৈরি করা হয়েছে। এখানে কোনো অপ্রয়োজনীয় ভারী ফ্রেমওয়ার্ক ব্যবহার করা হবে না:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    Shopify Extensions Architecture                          │
│                                                                             │
│  [1. Customer Storefront: Theme App Extension] (All Shopify 2.0 Themes)     │
│  ├── blocks/pdp-fbt.liquid ──────► <clearrecs-fbt> Native Custom Element    │
│  ├── blocks/smart-cart.liquid ───► <clearrecs-cart-drawer> Drawer + Bar     │
│  ├── blocks/carousel.liquid ─────► <clearrecs-carousel> Grid / Slider Block │
│  └── assets/clearrecs-*.js/css ──► Liquid + Vanilla JS (< 5KB, 0 Depend.)   │
│                                                                             │
│  [2. Checkout, Post-Purchase, Thank-you, Customer Account]                  │
│  ├── api_version: "2026-01" (current stable; do not pin 2025-07)            │
│  ├── purchase.checkout.block.render ──► checkout bump (Plus-gated offers)   │
│  ├── Checkout::PostPurchase::ShouldRender/Render ──► 120s 1-click add-to-order │
│  ├── purchase.thank-you.block.render ──► recs/content (NOT add-to-order)    │
│  └── customer-account.order-status.block.render ──► Customer Account UI     │
│                                                                             │
│  [3. Shopify Function — Discount]                                           │
│  └── cart.lines.discounts.generate.run ──► FBT bundle % when widget lines   │
│                                                                             │
│  [4. Web Pixel Extension] (Zero Site-Lag Tracking)                          │
│  └── app-pixel ──────────────────► Sandbox Browser Events (View, Cart, Buy) │
└─────────────────────────────────────────────────────────────────────────────┘
```

### এক্সটেনশন ডোমেন ও টেকনিক্যাল স্পেসিফিকেশন:

| এক্সটেনশন নাম | ফ্রেমওয়ার্ক ও লাইব্রেরি | শপিফাই টার্গেট / অবস্থান | আর্কিটেকচারাল মেকানিক্স (Native Architecture) |
| :--- | :--- | :--- | :--- |
| **১. Storefront FBT Bundle** | `Liquid + Vanilla JS Custom Element` | `PDP: blocks/pdp-fbt.liquid` | `<clearrecs-fbt>` কাস্টম এলিমেন্ট। কোনো React/Preact নেই। বিশ্বমানের লাইটওয়েট অ্যাপের স্ট্যান্ডার্ড অনুযায়ী সরাসরি ডমে মাউন্ট হয়, সাইজ < ৫KB, জিরো থিম স্লোডাউন। |
| **২. Smart Slide Cart Drawer** | `Liquid + Vanilla JS Custom Element` | `Global: blocks/smart-cart.liquid` | স্লাইড ড্রয়ার ও মাল্টি-টিয়ার প্রগ্রেস বার ($৫০=ফ্রি শিপিং, $১০০=গিফট)। শপিফাই কার্ট এজাক্স এপিআই (`/cart/add.js`) ইন্টিগ্রেশন। |
| **৩. Multi-Page Carousel** | `Liquid + Vanilla JS Custom Element` | `Home/Collection: blocks/carousel.liquid` | ড্র্যাগ-অ্যান্ড-ড্রপ হরাইজন্টাল ক্যারোসেল ও কার্ড গ্রিড। |
| **৪. Checkout Upsell Bump** | `@shopify/ui-extensions/checkout` | `purchase.checkout.block.render` | চেকআউট সামারিতে অফার। চেকআউট স্টেপে প্রোডাক্ট অফার **Shopify Plus-গেটেড** (Nosto উইজার্ডেও লক)। |
| **৫. Post-Purchase 1-click** | Post-purchase checkout extension | `Checkout::PostPurchase::ShouldRender` + `Render` | Settings → Checkout → Post-purchase page; **এক অ্যাপের স্লট**। সাইনড চেঞ্জসেট দিয়ে মূল অর্ডারে লাইন যোগ। কার্ড/Shop Pay only; ডিফল্ট কারেন্সি; min $0.50; ১২০s টাইমার (LimeSpot)। |
| **৬. Thank-you recs** | `@shopify/ui-extensions/checkout` | `purchase.thank-you.block.render` | পেমেন্টের পর কনটেন্ট/রেকস। **মূল অর্ডারে ১-ক্লিক অ্যাড নয়** (নতুন চেকআউট লাগে)। |
| **৭. Customer Account Reorder** | Customer Account UI extension | `customer-account.order-status.block.render` | চেকআউট প্যাকেজ নয়। অর্ডার স্ট্যাটাস পেজ রিপ্লেনিশমেন্ট। |
| **৮. Web Pixel Tracker** | `Web Pixels API (Sandbox)` | `Global Web Pixel` | স্যান্ডবক্সড পিক্সেলে সাইট স্পিড অক্ষুণ্ণ রেখে ব্রাউজিং, কার্ট অ্যাড ও কনভার্সন ট্র্যাক করে এজ ডিবিতে পাঠানো। |
| **৯. FBT Bundle Discount Function** | Shopify Function · Discount API | `cart.lines.discounts.generate.run` | উইজেট থেকে আসা লাইন (line-item property `_cr_src`) একসাথে থাকলে % ছাড়। **Shopify Automatic Discounts REST নয়** — Function ছাড়া বান্ডেল ডিসকাউন্ট v1 নয়। Scopes: `write_discounts` (+ ক্যাটালগ `read_products` / `read_inventory`)। Cart Transform শুধু লাইন মার্জ UI-এর জন্য; ডিসকাউন্টের জন্য Discount Function। |

---

---

## ৩. পূর্ণাঙ্গ এজ টেকনিক্যাল স্ট্যাক (World-Class Edge Architecture)

বিশ্বমানের শীর্ষস্থানীয় (World-Class Tier-1) শপিফাই অ্যাপগুলোতে যেভাবে আল্ট্রা-ফাস্ট এজ কম্পিউটিং, জিরো কোল্ড-স্টার্ট এবং সাব-৩০ms রেসপন্স নিশ্চিত করা হয়, আমাদের পূর্ণাঙ্গ টেকনিক্যাল স্ট্যাক হুবহু সেই আন্তর্জাতিক স্ট্যান্ডার্ড অনুযায়ী আর্কিটেক্ট করা হয়েছে:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                 Shopify AI Recommendations Tech Stack                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │ Merchant Admin Dashboard (100% Embedded in admin.shopify.com)         │  │
│  │ • Framework: React Router v7 (@shopify/shopify-app-react-router)      │  │
│  │ • UI System: Shopify Polaris React + App Bridge v4 (@shopify/app-bridge)│
│  │ • Styling: Sass / SCSS (BEM, _tokens.scss, _base.scss)                │  │
│  │ • Architecture: Controller-View Pattern (Route loader/action vs View) │  │
│  └──────────────────────────────────┬────────────────────────────────────┘  │
│                                     │ GraphQL, REST & HMAC Webhooks         │
│                                     ▼                                       │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │ High-Speed Edge Engine (Cloudflare Workers Edge Architecture)          │  │
│  │ • Runtime: Cloudflare Workers (workers/app.js, nodejs_compat)         │  │
│  │ • Global Latency: recs metafield = 0 extra RTT; App Proxy p99 < 500ms   │
│  │   (not a worldwide sub-15ms SLO; Workers Paid is not $0)                │
│  │ • Webhook ACK target: p99 < 500ms (Shopify hard limit 5s)               │
│  │ • Webhook Ingestion: Fast-ACK + Cloudflare Queue (durable)              │  │
│  │ • Deduplication: X-Shopify-Webhook-Id দিয়ে D1-এ claimWebhookDelivery │  │
│  │ • Cron Triggers: wrangler.toml crons = ["*/5 * * * *"]                │  │
│  └──────────────────────────────────┬────────────────────────────────────┘  │
│                                     │ Direct Edge SQL (Binding = "DB")      │
│                                     ▼                                       │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │ Edge Relational Database (Cloudflare D1 — SQLite Engine)              │  │
│  │ • Database: Cloudflare D1 (wrangler d1 migrations apply)              │  │
│  │ • Connection Pooling: জিরো কানেকশন পুলিং ইস্যু, সরাসরি এজ-লোকেশন কোয়েরি│
│  │ • Domain Modules: app/db/*.js (sessions, webhooks, analytics, dlq)    │  │
│  └──────────────────────────────────┬────────────────────────────────────┘  │
│                                     │ App Proxy (signed) or product metafield │
│                                     ▼                                       │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │ Storefront & Checkout Extensions Engine (Zero-Lag Edge Extensions)              │  │
│  │ • Storefront: Liquid + Native Custom Elements (gzip budget **per widget**) │
│  │ • Recs: `$app` product metafield top-3 (preferred) or App Proxy         │
│  │ • Checkout/Post-Purchase: @shopify/ui-extensions; Discount Function     │
│  └───────────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ৪. ডেটাবেস আর্কিটেকচার ও D1 স্কিমা মডেল (World-Class Edge Database Architecture)

বিশ্বমানের হাই-স্কেল SaaS ও ইকমার্স অ্যাপগুলোতে যেভাবে ডেটাবেস ল্যাটেন্সি দূর করতে আধুনিক সার্ভারলেস এজ এসকিউএল (Cloudflare D1) ব্যবহার করা হয়, আমাদের সিস্টেমেও সেই আর্কিটেকচার গ্রহণ করা হয়েছে। **সাব-১৫ms গ্লোবাল কোয়েরি SLO নয়** — প্রাইমারি রিজিয়নের SQL টাইম লো-ms হতে পারে। স্টোরফ্রন্ট রেকস মেটাফিল্ড বা সাইনড App Proxy দিয়ে সার্ভ হবে; পাবলিক `GET /api/recs?shop=` নয়।

### ১. `Session` টেবিল (Shopify OAuth Session Storage)

`accessToken` **প্লেইনটেক্সট নয়** — AES-GCM (`access_token_enc`, `access_token_iv`, `access_token_tag`)। ডিক্রিপ্ট শুধু Worker সিক্রেট দিয়ে।
```sql
CREATE TABLE IF NOT EXISTS "Session" (
  "id" TEXT PRIMARY KEY,
  "shop" TEXT NOT NULL,
  "state" TEXT NOT NULL,
  "isOnline" INTEGER NOT NULL DEFAULT 0,
  "scope" TEXT,
  "expires" INTEGER,
  "access_token_enc" BLOB NOT NULL,
  "access_token_iv" BLOB NOT NULL,
  "access_token_tag" BLOB NOT NULL,
  "userId" BIGINT,
  "firstName" TEXT,
  "lastName" TEXT,
  "email" TEXT,
  "accountOwner" INTEGER NOT NULL DEFAULT 0,
  "locale" TEXT,
  "collaborator" INTEGER DEFAULT 0,
  "emailVerified" INTEGER DEFAULT 0
);
CREATE INDEX IF NOT EXISTS "Session_shop_idx" ON "Session" ("shop");
```

### ২. `WebhookDeliveries` টেবিল (Fast-ACK & Idempotency Pipeline)
```sql
CREATE TABLE IF NOT EXISTS "WebhookDeliveries" (
  "webhook_id" TEXT PRIMARY KEY,
  "shop" TEXT NOT NULL,
  "topic" TEXT NOT NULL,
  "received_at" INTEGER NOT NULL
);
CREATE INDEX IF NOT EXISTS "idx_webhook_deliveries_shop" ON "WebhookDeliveries" ("shop");
CREATE INDEX IF NOT EXISTS "idx_webhook_deliveries_received_at" ON "WebhookDeliveries" ("received_at");
```

### ৩. `Subscriptions` টেবিল (Shopify Billing & Capped Usage)
```sql
CREATE TABLE IF NOT EXISTS "Subscriptions" (
  "id" TEXT PRIMARY KEY,
  "shop" TEXT NOT NULL UNIQUE,
  "plan_name" TEXT NOT NULL DEFAULT 'FREE', -- 'FREE', 'STARTER', 'GROWTH', 'SCALE'
  "charge_id" TEXT,
  "status" TEXT NOT NULL DEFAULT 'ACTIVE',
  "capped_amount" REAL DEFAULT 0.0,
  "current_period_attributed_cents" INTEGER NOT NULL DEFAULT 0,
  "created_at" INTEGER NOT NULL DEFAULT (strftime('%s', 'now')),
  "updated_at" INTEGER NOT NULL DEFAULT (strftime('%s', 'now'))
);
CREATE INDEX IF NOT EXISTS "idx_subscriptions_shop" ON "Subscriptions" ("shop");
```

### ৪. `WidgetConfigs` টেবিল (উইজেট সেটিংস ও থিম অপশনস)
```sql
CREATE TABLE IF NOT EXISTS "WidgetConfigs" (
  "id" TEXT PRIMARY KEY,
  "shop" TEXT NOT NULL,
  "widget_type" TEXT NOT NULL, -- 'PDP_FBT', 'SMART_CART', 'CAROUSEL', 'CHECKOUT_UPSELL', 'POST_PURCHASE'
  "title" TEXT NOT NULL,
  "subtitle" TEXT,
  "discount_percentage" REAL DEFAULT 0.0,
  "theme_settings_json" TEXT NOT NULL, -- Colors, button radius, badge text
  "is_enabled" INTEGER NOT NULL DEFAULT 1,
  "created_at" INTEGER NOT NULL DEFAULT (strftime('%s', 'now')),
  "updated_at" INTEGER NOT NULL DEFAULT (strftime('%s', 'now')),
  UNIQUE("shop", "widget_type")
);
CREATE INDEX IF NOT EXISTS "idx_widget_configs_shop" ON "WidgetConfigs" ("shop");
```

### ৫. `RecommendationRules` টেবিল (ম্যানুয়াল ও মার্চেন্ট কিউরেটেড রুলস — Tier 1)
```sql
CREATE TABLE IF NOT EXISTS "RecommendationRules" (
  "id" TEXT PRIMARY KEY,
  "shop" TEXT NOT NULL,
  "base_product_id" TEXT NOT NULL,
  "recommended_product_ids" TEXT NOT NULL, -- JSON Array: ["gid://shopify/Product/123", "gid://shopify/Product/456"]
  "discount_percentage" REAL DEFAULT 0.0,
  "priority" INTEGER NOT NULL DEFAULT 1,
  "is_active" INTEGER NOT NULL DEFAULT 1,
  "created_at" INTEGER NOT NULL DEFAULT (strftime('%s', 'now')),
  "updated_at" INTEGER NOT NULL DEFAULT (strftime('%s', 'now')),
  UNIQUE("shop", "base_product_id")
);
CREATE INDEX IF NOT EXISTS "idx_rules_lookup" ON "RecommendationRules" ("shop", "base_product_id", "is_active");
```

### ৬. `CoPurchaseMatrix` + `ProductOrderStats` (স্কোর সোর্স অফ ট্রুথ)

`confidence_score` স্টোর করবে না ক্যাশ হিসেবে-মাত্র — **ডিরাইভ** করবে: `pair_count / ProductOrderStats.order_count`। `A`-এর অর্ডার বাড়লে পুরনো কনফিডেন্স স্টেল হয়; তাই ডিনমিনেটর আলাদা টেবিল। `lift = confidence / (orders(B) / ShopOrderStats.order_count)`। Decay র‍্যাঙ্ক টাইমে: `pair_count * exp(-λ * days_since last_purchased_at)` — স্টোরড কলাম নয়।

```sql
CREATE TABLE IF NOT EXISTS "CoPurchaseMatrix" (
  "id" TEXT PRIMARY KEY,
  "shop" TEXT NOT NULL,
  "base_product_id" TEXT NOT NULL,
  "recommended_product_id" TEXT NOT NULL,
  "pair_count" INTEGER NOT NULL DEFAULT 1,
  "last_purchased_at" INTEGER NOT NULL DEFAULT (strftime('%s', 'now')),
  UNIQUE("shop", "base_product_id", "recommended_product_id")
);
CREATE INDEX IF NOT EXISTS "idx_copurchase_lookup" ON "CoPurchaseMatrix" ("shop", "base_product_id", "pair_count" DESC);

CREATE TABLE IF NOT EXISTS "ProductOrderStats" (
  "shop" TEXT NOT NULL,
  "product_id" TEXT NOT NULL,
  "order_count" INTEGER NOT NULL DEFAULT 0,
  PRIMARY KEY ("shop", "product_id")
);

CREATE TABLE IF NOT EXISTS "ShopOrderStats" (
  "shop" TEXT PRIMARY KEY,
  "order_count" INTEGER NOT NULL DEFAULT 0
);
```

### ৭. ইনভেন্টরি ম্যাপ (ওয়েবহুক পেয়লোড ≠ product_id)

`inventory_levels/update` দেয় `inventory_item_id`, `location_id`, `available` — **product/variant ID নয়**। আগের `InventoryShield` + `ProductVariants.is_available` + ক্যাটালগ — তিন জায়গায় ডুপ্লিকেট। সোর্স অফ ট্রুথ নিচে। ওয়েবহুক শুধু qty আপডেট + **KV RecCache invalidate**। উইজেট রেন্ডার টাইমে `available` + `inventory_policy` + `tracked` চেক। `CONTINUE` / untracked ভ্যারিয়েন্ট হাইড করবে না।

```sql
CREATE TABLE IF NOT EXISTS "InventoryItemMap" (
  "shop" TEXT NOT NULL,
  "inventory_item_id" TEXT NOT NULL,
  "variant_id" TEXT NOT NULL,
  "product_id" TEXT NOT NULL,
  PRIMARY KEY ("shop", "inventory_item_id")
);
CREATE INDEX IF NOT EXISTS "idx_inv_map_variant" ON "InventoryItemMap" ("shop", "variant_id");

CREATE TABLE IF NOT EXISTS "LocationInventory" (
  "shop" TEXT NOT NULL,
  "inventory_item_id" TEXT NOT NULL,
  "location_id" TEXT NOT NULL,
  "available" INTEGER NOT NULL DEFAULT 0,
  "updated_at" INTEGER NOT NULL DEFAULT (strftime('%s', 'now')),
  PRIMARY KEY ("shop", "inventory_item_id", "location_id")
);
```

`ProductVariants` holds `inventory_item_id`, `tracked`, `inventory_policy`. `available` = SUM(`LocationInventory`). **InventoryShield টেবিল নেই।**

### ৭খ. `ProductCatalog` + `ProductVariants` (ওয়াটারফল Tier 3–4)
আগের ডায়াগ্রাম `Products` টেবিল কোয়েরি করত কিন্তু DDL-এ সেই টেবিল ছিল না। ক্যাটালগ সিঙ্ক ছাড়া টাইটেল, ইমেজ, ক্যাটাগরি ও `sales_count` সার্ভ করা যায় না।

```sql
CREATE TABLE IF NOT EXISTS "ProductCatalog" (
  "id" TEXT PRIMARY KEY,
  "shop" TEXT NOT NULL,
  "product_id" TEXT NOT NULL,
  "title" TEXT NOT NULL,
  "image_url" TEXT,
  "price_cents" INTEGER NOT NULL DEFAULT 0,
  "category" TEXT,
  "taxonomy_category_id" TEXT,
  "sales_count" INTEGER NOT NULL DEFAULT 0,
  "status" TEXT NOT NULL DEFAULT 'ACTIVE',
  "updated_at" INTEGER NOT NULL DEFAULT (strftime('%s', 'now')),
  UNIQUE("shop", "product_id")
);
CREATE INDEX IF NOT EXISTS "idx_catalog_category" ON "ProductCatalog" ("shop", "taxonomy_category_id", "status");
CREATE INDEX IF NOT EXISTS "idx_catalog_sales" ON "ProductCatalog" ("shop", "sales_count" DESC);

-- App-global complement edges (also ship as Worker JSON). Not per-SKU LLM output.
CREATE TABLE IF NOT EXISTS "ComplementMap" (
  "id" TEXT PRIMARY KEY,
  "vertical" TEXT NOT NULL,
  "source_taxonomy_id" TEXT NOT NULL,
  "target_taxonomy_id" TEXT NOT NULL,
  UNIQUE("vertical", "source_taxonomy_id", "target_taxonomy_id")
);
CREATE INDEX IF NOT EXISTS "idx_complement_source" ON "ComplementMap" ("vertical", "source_taxonomy_id");

CREATE TABLE IF NOT EXISTS "ProductVariants" (
  "id" TEXT PRIMARY KEY,
  "shop" TEXT NOT NULL,
  "product_id" TEXT NOT NULL,
  "variant_id" TEXT NOT NULL,
  "inventory_item_id" TEXT,
  "options_json" TEXT,
  "price_cents" INTEGER NOT NULL DEFAULT 0,
  "tracked" INTEGER NOT NULL DEFAULT 1,
  "inventory_policy" TEXT NOT NULL DEFAULT 'DENY',
  "available" INTEGER NOT NULL DEFAULT 0,
  UNIQUE("shop", "variant_id")
);
```

### ৮. `AnalyticsEvents` টেবিল (৫-স্টেজ কনভার্সন ফানেল)

`session_id` **৯০ দিন** রাখবে, তারপর ক্রন ডিলিট (GDPR)। অ্যাট্রিবিউশনের সোর্স অফ ট্রুথ অর্ডার লাইন-আইটেম প্রপার্টি, পিক্সেল নয়।

```sql
CREATE TABLE IF NOT EXISTS "AnalyticsEvents" (
  "id" TEXT PRIMARY KEY,
  "shop" TEXT NOT NULL,
  "session_id" TEXT NOT NULL,
  "event_type" TEXT NOT NULL, -- 'RENDERED', 'VIEWED', 'CLICKED', 'CART_ADD', 'CONVERTED'
  "widget_type" TEXT NOT NULL,
  "product_id" TEXT,
  "order_value" REAL DEFAULT 0.0,
  "created_at" INTEGER NOT NULL DEFAULT (strftime('%s', 'now'))
);
CREATE INDEX IF NOT EXISTS "idx_analytics_funnel" ON "AnalyticsEvents" ("shop", "event_type", "created_at");
CREATE INDEX IF NOT EXISTS "idx_analytics_created" ON "AnalyticsEvents" ("created_at");
```

### ৮খ. `AttributedLineItems` (সেলস ক্যাপের ভিত্তি)

ক্যাপ = এই টেবিলের `line_price_cents` সাম, পিক্সেল অনুমান নয়।

```sql
CREATE TABLE IF NOT EXISTS "AttributedLineItems" (
  "shop" TEXT NOT NULL,
  "order_id" TEXT NOT NULL,
  "line_id" TEXT NOT NULL,
  "product_id" TEXT NOT NULL,
  "widget_type" TEXT NOT NULL, -- 'pdp_fbt' | 'post_purchase' | ...
  "line_price_cents" INTEGER NOT NULL,
  "period_yyyymm" TEXT NOT NULL,
  PRIMARY KEY ("shop", "order_id", "line_id")
);
CREATE INDEX IF NOT EXISTS "idx_attr_period" ON "AttributedLineItems" ("shop", "period_yyyymm");
```

### ৯. `DeadLetterQueue` টেবিল (DLQ — Resilience & Retry Pattern)
```sql
CREATE TABLE IF NOT EXISTS "DeadLetterQueue" (
  "id" TEXT PRIMARY KEY,
  "shop" TEXT NOT NULL,
  "topic" TEXT NOT NULL,
  "payload" TEXT NOT NULL,
  "error_message" TEXT,
  "retry_count" INTEGER NOT NULL DEFAULT 0,
  "created_at" INTEGER NOT NULL DEFAULT (strftime('%s', 'now'))
);
```

---

## ৪গ. স্টোরফ্রন্ট ডেলিভারি, অর্ডার হাইজিন, অ্যাট্রিবিউশন, কমপ্লায়েন্স (v1.3 freeze)

### Recs কীভাবে পৌঁছাবে (পাবলিক GET নয়)

পাবলিক `GET /api/recs?shop=` → আনঅথেন্টিকেটেড, CORS, কস্ট অ্যাবিউজ। **নিষেধ।**

1. **Preferred v1:** ওয়াটারফল আউটপুট `$app.recs_top3` প্রোডাক্ট মেটাফিল্ডে লিখো (JSON)। Liquid সরাসরি রেন্ডার — জিরো নেটওয়ার্ক, CLS কম। `status != ACTIVE` / unpublished বাদ।  
2. **App Proxy** (`/apps/<handle>/recs`): HMAC সাইনড, সেম-অরিজিন, অ্যাড-ব্লকার-সেফ — শুধু লাইভ স্টক রিফ্রেশ বা কার্ট-অ্যাট্রিবিউশন পিং। p99 < 500ms টার্গেট।

### অর্ডার হাইজিন (ম্যাট্রিক্সে কী ঢুকবে)

শুধু `orders/create` নয়। কাউন্ট **শুধু** যদি:

* `test != true`
* `cancelled_at` খালি
* `financial_status` ∈ {`paid`, `partially_paid`, `authorized`} — `pending` / `voided` / `refunded` বাদ
* লাইনে `_cr_src` **নেই** (উইজেট নিজে বানানো বান্ডেল ফিডব্যাক লুপ — নিজের রেকসকে “সহ-ক্রয়” বানাবে না)

`orders/cancelled` + `refunds/create`: আগে কাউন্ট করা অর্ডার হলে `pair_count` / `ProductOrderStats` ডিক্রিমেন্ট (idempotent on order_id)। Partner Dashboard: order webhooks = **protected customer data** অ্যাক্সেস চেক।

### অ্যাট্রিবিউশন ও ক্যাপ

1. `/cart/add.js`-এ লাইন প্রপার্টি `_cr_src=<widget>` + `_cr_base=<product_id>`।  
2. Discount Function একই প্রপার্টি দেখে বান্ডেল % দেয়।  
3. `orders/create`-এ সেই প্রপার্টি (বা আমাদের ডিসকাউন্ট অ্যালোকেশন) থাকলে `AttributedLineItems` লিখো। পিক্সেল শুধু ফানেল, বিল নয়।  
4. **ক্যাপ ছাড়ালে উইজেট বন্ধ নয়** (রিভিউ-কিলার)। ৮০%-এ অ্যাডমিন ব্যানার; ১০০%-এ Shopify subscription update (মার্চেন্ট অ্যাপ্রুভাল লাগে) — উইজেট চালু থাকে গ্রেস পিরিয়ডে।  
5. Pro/Scale = **কোনো GMV ক্যাপ নেই**। “আনলিমিটেড (fair capped)” ফেলে দাও — স্ববিরোধী।

### GDPR / সাবমিশন (Phase 12 নয়)

অ্যাপ স্টোর সাবমিশনের **আগেই** ম্যান্ডেটরি: `customers/data_request`, `customers/redact`, `shop/redact`। Phase 2-এ ওয়্যার করো।

### gzip বাজেট (প্রতি উইজেট)

একটা গ্লোবাল `<5KB` সব উইজেট মিলে নয়। মাপতে হবে:

| অ্যাসেট | gzip টার্গেট | ফেজ |
| :--- | :--- | :--- |
| `pdp-fbt.js` + css | **< 5KB** | v1 |
| `cart-drawer.js` + progress + a11y | আলাদা বাজেট; ৫KB-তে ধরা কঠিন | পরে |
| `carousel.js` | আলাদা | পরে |

---
> **VisualAI কী এবং কীভাবে কাজ করে (Scale Tier Feature)?**  
> ফ্যাশন, অ্যাপারেল ও লাইফস্টাইল মার্চেন্টদের জন্য VisualAI প্রোডাক্ট ছবির ভিজ্যুয়াল ফিচারস, কাট ও কালার প্যালেট বিশ্লেষণ করে লুক-অ্যালাইক (Complete The Look) বান্ডেল তৈরি করে। ক্লাউডফ্লেয়ার এম্বেডিংস মেকানিক্সের মাধ্যমে শপিফাই ট্যাক্সোনমি ক্যাটাগরি ও ভিজ্যুয়াল অ্যাট্রিবিউট ম্যাচ করে সাব-১৫ms-এ ভিজ্যুয়াল রেকমেন্ডেশন সার্ভ করা হয়।

---

## ৫. কোর রিকমেন্ডেশন অ্যালগরিদম ও ৪-টিয়ার এজ ওয়াটারফল চেইন

কখনোই যেন কোনো স্টোরে খালি উইজেট না থাকে। **CBB লাইভ ওয়াটারফল:** Manual → Automatic AI → Global products → Random by collection (পার-টিয়ার টগল + exclusive-manual মোড)। নিচের চেইন সেই প্যাটার্নের অ্যাডাপ্টেশন। **Tier 3 same-leaf category নয়** (কেস দেখলে আরেকটা কেস = substitute)। স্ট্যাটিক ভার্টিক্যাল complement map + Search & Discovery complementary metafield ইমপোর্ট। **Vectorize / bge embeddings v1 নয়** — nearest-neighbor FBT নয়। স্টোরফ্রন্ট রেসপন্স ক্যাশড JSON; চারটা লাইভ D1 রাউন্ড-ট্রিপ গ্লোবাল সাব-১৫ms SLO নয়। **LLM PDP-তে নয়** — স্কোর/খরচ/পিয়ার-রিভিউ: [ALGORITHM_AND_LLM_COST.md](ALGORITHM_AND_LLM_COST.md)।

```
[Precompute → $app.recs_top3 metafield; optional App Proxy stock ping]
                                   │
                                   ▼
[Tier 1: Manual / S&D complementary] ► RecommendationRules + shopify--discovery complementary metafields
                                   │ (ফলাফল না পেলে বা < ৩টি আইটেম হলে)
                                   ▼
[Tier 2: Co-Purchase Matrix] ─────► pair_count / ProductOrderStats.order_count
                                   │    serve ≥1; percent iff pair≥5 AND orders(A)≥20
                                   │    render-time: tracked+DENY+available<=0 → skip
                                   │ (নতুন SKU / সাপোর্ট ০ হলে)
                                   ▼
[Tier 3: Complement map] ─────────► ComplementMap: source taxonomy GID → complementary GIDs
                                   │    SELECT ProductCatalog WHERE taxonomy_category_id IN (...)
                                   │    AND status = 'ACTIVE' (unpublished বাদ)
                                   │    NOT same-leaf (phone case ↛ another phone case)
                                   │ (< ৩টি আইটেম হলে)
                                   ▼
[Tier 4: Global Bestseller Fallback] ProductCatalog ORDER BY sales_count DESC
                                   │
                                   ▼
[Metafield JSON + source label (FBT / Goes with / Popular) + render-time stock]
```

---

## ৬. ১২টি অ্যাজাইল মাইক্রো-ফেজ এক্সিকিউশন প্ল্যান (The 12 Agile Micro-Phases)

বড় ফেজের ঝুঁকি এড়িয়ে সহজে টেস্ট ও মনিটর করার জন্য পুরো প্রজেক্টটিকে **১২টি সুনির্দিষ্ট মাইক্রো-ফেজে** ভাগ করা হয়েছে। প্রতিটি ফেজের সময়সীমা **৩ থেকে ৫ দিন** এবং প্রতিটি ফেজেই একটি **স্বাধীন টেস্টেবল ডেলিভারেবল** পাওয়া যাবে:

```
[Phase 1: Edge Shell & Auth] ─────► [Phase 2: D1 Database & Webhooks] ─► [Phase 3: Theme Custom Elements]
       (৩-৪ দিন)                             (৩-৪ দিন)                             (৩ দিন)
          │                                     │                                     │
          ▼                                     ▼                                     ▼
[Phase 4: PDP FBT Web Component] ─► [Phase 5: 4-Tier Edge Waterfall] ──► [Phase 6: Multi-Add & Discounts]
       (৪-৫ দিন)                             (৪-৫ দিন)                             (৩-৪ দিন)
          │                                     │                                     │
          ▼                                     ▼                                     ▼
[Phase 7: Explainable Badges] ────► [Phase 8: Smart Slide Cart Drawer] ─► [Phase 9: Multi-Page Carousels]
       (৩ দিন)                               (৫-৬ দিন)                             (৪-৫ দিন)
          │                                     │                                     │
          ▼                                     ▼                                     ▼
[Phase 10: Checkout & Post-Upsell]► [Phase 11: Polaris Admin & Funnel] ─► [Phase 12: Audit & Launch 💎]
       (৪-৫ দিন)                             (৪-৫ দিন)                             (৫-৬ দিন)
```

### ফেজ ১: প্রজেক্ট সেটআপ ও ক্লাউডফ্লেয়ার এজ শেল (সপ্তাহ ১ | ৩-৪ দিন)
* **টাস্ক:** বিশ্বমানের এন্টারপ্রাইজ শপিফাই অ্যাপের আর্কিটেকচার অনুযায়ী React Router v7 (`@shopify/shopify-app-react-router`) + Cloudflare Workers (`@react-router/cloudflare`, `wrangler.toml`), শপিফাই সিএলআই v4 কনফিগারেশন, ও-অথ (OAuth) অথেনটিকেশন ও টানেল সেটআপ।
* **টেস্টেবল ডেলিভারেবল:** শপিফাই টেস্ট স্টোরে অ্যাপটি ১-ক্লিকে ইনস্টল হবে এবং শপিফাই অ্যাডমিন প্যানেলে নেটিভ এজ-পাওয়ার্ড ড্যাশবোর্ড দেখা যাবে।

### ফেজ ২: ক্লাউডফ্লেয়ার ডি১ (D1) স্কিমা ও ফাস্ট-এক ওয়েবহুক পাইপলাইন (সপ্তাহ ১-২ | ৩-৪ দিন)
* **টাস্ক:** D1 মাইগ্রেশন (`Session` encrypted token, `WebhookDeliveries`, `CoPurchaseMatrix`, `ProductOrderStats`, `InventoryItemMap`, `LocationInventory`, `ComplementMap`, `AttributedLineItems`)। Queue Fast-ACK। **GDPR** `customers/data_request|redact`, `shop/redact` এখানেই। Hygiene ফিল্টার consumer-এ। ACK টার্গেট p99 < 500ms।
* **টেস্টেবল ডেলিভারেবল:** টেস্ট/ক্যান্সেল অর্ডার ম্যাট্রিক্সে ঢোকে না; GDPR webhook 200 দেয়; টোকেন প্লেইনটেক্সট D1-এ নেই।

### ফেজ ৩: থিম অ্যাপ এক্সটেনশন ও কোর কাস্টম এলিমেন্ট স্ক্রিপ্ট (সপ্তাহ ২ | ৩ দিন)
* **টাস্ক:** শপিফাই সিএলআই দিয়ে Theme App Extension তৈরি (`extensions/theme-extension/`)। নেটিভ লিকুইড ও ভ্যানিলা জেএস কাস্টম এলিমেন্ট আর্কিটেকচার (< ৫KB, জিরো ডিপেন্ডেন্সি)।
* **টেস্টেবল ডেলিভারেবল:** শপিফাই থিম এডিটরে অ্যাপ ব্লক ড্র্যাগ-অ্যান্ড-ড্রপ করা যাবে এবং স্টোরফ্রন্টের ব্রাউজার কনসোলে জিরো সাইট-ল্যাগে ইঞ্জিন অ্যাক্টিভ দেখা যাবে।

### ফেজ ৪: পিডিপি Frequently Bought Together (FBT) ব্লক (সপ্তাহ ৩ | ৪-৫ দিন)
* **টাস্ক:** `blocks/pdp-fbt.liquid` + `<clearrecs-fbt>`। gzip **এই উইজেট** < 5KB। রেকস `$app.recs_top3` মেটাফিল্ড থেকে; পাবলিক recs API নয়। `_cr_src` লাইন প্রপার্টি কার্ট অ্যাডে।
* **টেস্টেবল ডেলিভারেবল:** নেটওয়ার্ক ট্যাবে `/api/recs?shop=` নেই; অ্যাড-টু-কার্ট পেয়লোডে `_cr_src=pdp_fbt` আছে।

### ফেজ ৫: ৪-টিয়ার ওয়াটারফল (ক্যাশড মেটাফিল্ড)
* **টাস্ক:** ক্যাশড ওয়াটারফল + মেটাফিল্ড রাইট। Percent ব্যাজ: `pair_count >= 5` **এবং** `orders(A) >= 20`; নাহলে কাউন্ট ("12 customers")। ভ্যারিয়েন্ট-% নয় (ম্যাট্রিক্স প্রোডাক্ট-লেভেল)।
* **টেস্টেবল ডেলিভারেবল:** ৬ অর্ডারের স্টোরে ৮৩% ব্যাজ ছাপাবে না; unpublished প্রোডাক্ট উইজেটে আসবে না।

### ফেজ ৬: ১-ক্লিক মাল্টি-অ্যাড + Discount Function (সপ্তাহ ৪-৫ | ৩-৪ দিন)
* **টাস্ক:** `/cart/add.js` মাল্টি-অ্যাড + **Shopify Discount Function** (`cart.lines.discounts.generate.run`)। Automatic Discount REST দিয়ে বান্ডেল ছাড় ভাবা যাবে না। Scope: `write_discounts`।
* **টেস্টেবল ডেলিভারেবল:** উইজেট থেকে ৩ লাইন কার্টে গেলে Function % দেয়; ম্যানুয়াল কার্ট অ্যাডে (প্রপার্টি ছাড়া) দেয় না।

### ফেজ ৭: Explainable AI ব্যাজ ও জিরো-স্টক রিয়েল-টাইম শিল্ড (সপ্তাহ ৫ | ৩ দিন)
* **টাস্ক:** ব্যাজ টেমপ্লেট (প্রোডাক্ট-লেভেল; “এই সাইজ” নয়)। `inventory_levels/update` → `InventoryItemMap` দিয়ে variant খুঁজে `LocationInventory` আপডেট + RecCache/metafield invalidate। CONTINUE/untracked হাইড নয়।
* **টেস্টেবল ডেলিভারেবল:** স্টক ০ + DENY হলে হাইড; CONTINUE সেলিং চালু থাকলে দেখাবে।

### ফেজ ৮: স্মার্ট স্লাইড কার্ট ড্রয়ার ও প্রগ্রেস বার (সপ্তাহ ৬ | ৫-৬ দিন)
* **টাস্ক:** `blocks/smart-cart.liquid` ও `<clearrecs-cart-drawer>` কাস্টম এলিমেন্ট। মাল্টি-টিয়ার প্রগ্রেস বার ($৫০=ফ্রি শিপিং, $১০০=১০% ছাড়, $১৫০=ফ্রি গিফট) ও ইন-কার্ট ১-ক্লিক ক্রস-সেল উইজেট।
* **টেস্টেবল ডেলিভারেবল:** স্টোরে কোনো প্রোডাক্ট কার্টে যোগ করলে সুন্দর স্লাইড ড্রয়ার খুলে যাবে এবং প্রগ্রেস বার রিয়েল-টাইমে আপডেট হবে।

### ফেজ ৯: ওমনিচ্যানেল ক্যারোসেল ও ৫-মিনিট ভার্টিক্যাল টেমপ্লেটস (সপ্তাহ ৭ | ৪-৫ দিন)
* **টাস্ক:** হোমপেজ ও কালেকশনের জন্য `blocks/carousel.liquid` ব্লক এবং ফ্যাশন, বিউটি ও ইলেকট্রনিক্সের জন্য ১-ক্লিক প্রি-বিল্ট ইন্ডাস্ট্রি রুলস টেমপ্লেট।
* **টেস্টেবল ডেলিভারেবল:** থিম এডিটর দিয়ে স্টোরের যেকোনো পেজে ড্র্যাগ-অ্যান্ড-ড্রপ করে রেকমেন্ডেশন ক্যারোসেল বসানো যাবে।

### ফেজ ১০: চেকআউট এক্সটেনশন ও ১২০ সেকেন্ড পোস্ট-পারচেজ আপসেল (সপ্তাহ ৮ | ৪-৫ দিন)
* **টাস্ক:** পোস্ট-পারচেজ ১-ক্লিক (এক অ্যাপ স্লট — ReConvert/AfterSell/Zipify ইনকাম্বেন্ট; টিয়ারডাউন নেই)। চেকআউট প্রোডাক্ট অফার **Plus-গেটেড** — SMB Growth হেডলাইন নয়। অ্যাট্রিবিউশন `_cr_src` + `AttributedLineItems`।
* **টেস্টেবল ডেলিভারেবল:** পোস্ট-পারচেজ লাইন মূল অর্ডারে যোগ; অ্যাট্রিবিউটেড সেন্ট বিলিং পিরিয়ডে বাড়ে।

### ফেজ ১১: পোলারিস মার্চেন্ট ড্যাশবোর্ড ও ৫-স্টেজ ফানেল অ্যানালিটিক্স (সপ্তাহ ৮-৯ | ৪-৫ দিন)
* **টাস্ক:** বিশ্বমানের লার্জ-স্কেল শপিফাই অ্যাপগুলোতে যেভাবে কোড মেইনটেইনেবল রাখা হয়, সেই আন্তর্জাতিক কন্ট্রোলার-ভিউ আর্কিটেকচারে React Router v7 + Shopify Polaris দিয়ে ড্যাশবোর্ড, বান্ডেল এডিটর এবং ৫-স্টেজ ফানেল অ্যানালিটিক্স (`Rendered` ➔ `Viewed` ➔ `Clicked` ➔ `Added` ➔ `Converted`) তৈরি।
* **টেস্টেবল ডেলিভারেবল:** মার্চেন্ট ড্যাশবোর্ডে প্রতিদিন কত ডলার সেলস জেনারেট হলো এবং সম্পূর্ণ কনভার্সন ফানেল গ্রাফ দেখতে পারবে।

### ফেজ ১২: "Built for Shopify" 💎 অডিট, পারফরম্যান্স টিউন ও লঞ্চ (সপ্তাহ ৯-১০ | ৫-৬ দিন)
* **টাস্ক:** সাবমিশন চেকলিস্ট (GDPR আগেই Phase 2-এ)। Lighthouse: অ্যাপের জন্য স্টোরফ্রন্ট **১০ পয়েন্টের বেশি নামবে না** — ১০০/১০০ দাবি নয়। BFS পোস্ট-লঞ্চ।
* **টেস্টেবল ডেলিভারেবল:** অ্যাপ স্টোর সাবমিশন প্যাকেজ; BFS ব্যাজ লঞ্চ-ডে গ্যারান্টি নয়।

---

## ৭. প্রাইসিং ও গো-টু-মার্কেট স্ট্র্যাটেজি (Fair Capped Pricing Model)

মার্কেট ও কম্পিটিটর প্রাইসিং রিসার্চ করে আমরা একটি স্বচ্ছ ও ফেয়ার-ক্যাপড প্রাইসিং টিয়ার নির্ধারণ করেছি যা শপিফাই রিকারিং অ্যাপ্লিকেশন চার্জেস (Billing API v2) দিয়ে বাস্তবায়ন করা যাবে:

| প্ল্যান | মাসিক ফি | কী কী অন্তর্ভুক্ত |
| :--- | :--- | :--- |
| **Free Tier** | **$০ / মাস** | • প্রতি মাসে $৫০০ **অ্যাট্রিবিউটেড** সেলস (`AttributedLineItems`)<br>• পিডিপি FBT + ওয়াটারফল। ক্যাপ ছাড়ালে উইজেট বন্ধ নয় — আপগ্রেড অ্যাপ্রুভাল |
| **Starter** | **$১৯ / মাস** | • $২,০০০ অ্যাট্রিবিউটেড সেলস<br>• FBT বান্ডেল + Discount Function। কার্ট ড্রয়ার **পরে** (৫KB বাজেট আলাদা) |
| **Growth** | **$৪৯ / মাস** | • $৭,৫০০ অ্যাট্রিবিউটেড সেলস<br>• Explainer ব্যাজ + ভার্টিক্যাল ম্যাপ। পোস্ট-পারচেজ **অপশনাল** (এক স্লট; ReConvert ইত্যাদি থাকলে নেবে না)। চেকআউট প্রোডাক্ট অফার এখানে নয় (Plus) |
| **Pro / Scale** | **$৯৯ / মাস** | • **GMV ক্যাপ নেই** (fair-capped বলা যাবে না)<br>• Plus checkout bump অপশন + A/B/VisualAI হাইপোথিসিস |

---

## ৮. ইঞ্জিনিয়ারিং প্রিন্সিপালস ও আর্কিটেকচারাল রুলস (World-Class Engineering Standards)

বিশ্বমানের টপ-টিয়ার শপিফাই ও হাই-স্কেল SaaS অ্যাপ্লিকেশনগুলোতে যে গোল্ড-স্ট্যান্ডার্ড ইঞ্জিনিয়ারিং প্রিন্সিপাল ব্যবহার করা হয়, পুরো কোডবেসে সেই বিশ্বমানের প্যাটার্ন কঠোরভাবে মেনে চলা হবে:

* 📜 **পূর্ণাঙ্গ ইঞ্জিনিয়ারিং ম্যানুয়াল:** [ENGINEERING_STANDARDS_AND_PATTERNS.md](ENGINEERING_STANDARDS_AND_PATTERNS.md)
* **কোর প্রিন্সিপালসমূহ (গ্লোবাল ওয়ার্ল্ড-ক্লাস অ্যাপস যেভাবে আর্কিটেক্ট করে):**
  * **Co-location Principle:** বিশ্বমানের ফ্রন্টএন্ড কোডবেসের মতো প্রতিটি উইজেটের সাব-ভিউ ও লজিক ফোল্ডার-লেভেলে কো-লোকেটেড থাকবে (`app/components/fbt/`, `app/components/cart-drawer/`)।
  * **Controller-View Pattern:** হাই-স্কেল এন্টারপ্রাইজ অ্যাপের মতো React Router Route (`loader`/`action`) বনাম প্রেজেন্টেশনাল View (`*View.jsx`) সম্পূর্ণ আলাদা থাকবে।
  * **Fast-ACK & Idempotency:** `X-Shopify-Webhook-Id` claim → Queue.send → **< ২৫ms HTTP 200**। পেয়ার ইনক্রিমেন্ট কনজিউমারে; `waitUntil`-only নয়।
  * **UI Extension Primitives:** টপ-পারফর্মিং শপিফাই এক্সটেনশনের মতো কোনো ভারী ফ্রেমওয়ার্ক নয়; সরাসরি নেটিভ `@shopify/ui-extensions` ও `root.createComponent` ব্যবহার করতে হবে।
  * **Zero-Weight Storefront:** `pdp-fbt` gzip < 5KB **per widget**; কার্ট ড্রয়ার আলাদা বাজেট।
  * **Declarative Plan Gating:** ক্যাপ অতিক্রমে উইজেট অফ নয়; `<PlanGate />` + Billing API আপগ্রেড রিকোয়েস্ট।
  * **Zero Dead Code (YAGNI):** গুগল ও মেটার মতো হাই-কোয়ালিটি ক্লিন কোড স্ট্যান্ডার্ড নিশ্চিত করতে কোনো অপ্রয়োজনীয় বা কমেন্টেড কোড রাখা হবে না।

---
*ফাইলটি সফলভাবে তৈরি ও সংরক্ষিত হয়েছে:* `MASTER_ARCHITECTURE_AND_ROADMAP.md`
