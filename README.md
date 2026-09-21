# 💎 Shopify AI Product Recommendations & Upsell Engine

> Research pack. Frozen competitor snapshot: [COMPARISON.md](COMPARISON.md). Latency / bundle-size lines below are **targets**, not measured competitor-beating data.

---

## 👥 Leadership & Governance

| মেম্বার | রোল | মূল দায়িত্ব |
|:---|:---|:---|
| **এনামুল ভাই** | **Team Lead & Strategic Director** | কোর ভিশন, মার্কেট স্কোপিং, স্ট্র্যাটেজিক মেন্টরশিপ, বিজনেস ও জিটিএম (GTM) অ্যালাইনমেন্ট। |
| **নুরুজ্জামান রুবেল** | **Lead Engineer & Product Manager** | কম্পিটিটর রিভার্স-ইঞ্জিনিয়ারিং, সিস্টেম আর্কিটেকচার, ফুল-স্ট্যাক এজ ডেভেলপমেন্ট ও "Built for Shopify" কমপ্লায়েন্স। |

---

## 📑 Documentation Sitemap & Workspace Index

এই রিপোজিটরিতে সম্পূর্ণ প্রজেক্টের গবেষণা, কম্পিটিটর রিভার্স-ইঞ্জিনিয়ারিং, টেকনিক্যাল আর্কিটেকচার এবং কোডিং স্ট্যান্ডার্ড সুসংগঠিতভাবে সাজানো রয়েছে:

### 1. কোর স্ট্র্যাটেজি ও আর্কিটেকচার
* 📌 [COMPARISON.md](COMPARISON.md) — **Frozen** competitor prices, ratings, Shopify surfaces (Sept 2026). Conflicts → this file wins.
* [ALGORITHM_AND_LLM_COST.md](ALGORITHM_AND_LLM_COST.md) — ওয়াটারফল কীভাবে চলে, LLM কোথায় বসবে, খরচ (Sept 2026 prices).
* [MASTER_ARCHITECTURE_AND_ROADMAP.md](MASTER_ARCHITECTURE_AND_ROADMAP.md)  
  টেকনিক্যাল ব্লুপ্রিন্ট (Workers + D1, waterfall, extensions). ইমপ্লিমেন্টেশন হাইপোথিসিস।
* [PROJECT_STRATEGY_AND_DATA_ANALYSIS.md](PROJECT_STRATEGY_AND_DATA_ANALYSIS.md)  
  পজিশনিং ও লাইভ-ভেরিফায়েড গ্যাপ (unsourced TAM/ARR কাটা)।
* [ENGINEERING_STANDARDS_AND_PATTERNS.md](ENGINEERING_STANDARDS_AND_PATTERNS.md)  
  কোডিং প্যাটার্ন; `<5KB` / `<15ms` টার্গেট, মাপা নয়।
* [ENAMUL_SUGGEST_SHOPIFY_PRODUCT_RECOMMENDATIONS_COMPETITIVE_STRATEGY.md](ENAMUL_SUGGEST_SHOPIFY_PRODUCT_RECOMMENDATIONS_COMPETITIVE_STRATEGY.md)  
  অরিজিনাল প্রোডাক্ট-লিড মেমো। COMPARISON-এর সাথে কনফ্লিক্ট হলে COMPARISON জিতবে।

### 2. কম্পিটিটর রিভার্স-ইঞ্জিনিয়ারিং (`competitors/`)
* [competitors/LIMESPOT.md](competitors/LIMESPOT.md) — লাইভ অ্যাডমিন + ডিজাইনার।
* [competitors/CBB_FREQUENTLY_BOUGHT_TOGETHER.md](competitors/CBB_FREQUENTLY_BOUGHT_TOGETHER.md) — Code Black Belt FBT (আগে ভুল নাম `JULIUS.md`)।
* [competitors/NOSTO.md](competitors/NOSTO.md) — এন্টারপ্রাইজ CXP।
* [competitors/WISER.md](competitors/WISER.md) — লিস্টিং + ডেমো স্টোরফ্রন্ট (অ্যাডমিন ওয়াটারফল নয়)।

---

## ⚡ Architecture At A Glance

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                 Shopify AI Recommendations Tech Stack                       │
├─────────────────────────────────────────────────────────────────────────────┤
│  [Merchant Admin]     React Router v7 + Shopify Polaris + App Bridge v4     │
│  [Edge Engine]        Cloudflare Workers (Sub-15ms Latency, Zero Cold Start)│
│  [Edge Relational DB] Cloudflare D1 (SQLite Engine, 9 Domain Schemas)       │
│  [Storefront Widgets] Liquid + Native Custom Elements (< 5KB, 0 Dependencies)│
│  [Checkout & Upsell]  @shopify/ui-extensions (Purchase Bump & 120s Post-Buy)│
│  [Web Pixel]          Web Pixels API (Zero-Lag Sandbox Ingestion)           │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 🎯 The 4-Tier Waterfall Engine

মার্চেন্ট স্টোরে কখনোই যেন ফাঁকা উইজেট ডিসপ্লে না হয়, সেজন্য এজ-লেভেলে ৪-স্তরের ক্যাশড ফলব্যাক চেইন কাজ করে:

1. **Tier 1: Merchant Curated Rules** (`RecommendationRules` — অগ্রাধিকার ভিত্তিতে মার্চেন্ট কর্তৃক নির্দিষ্ট করা বান্ডেল)
2. **Tier 2: Co-Purchase Matrix AI** (`CoPurchaseMatrix` — রিয়েল অর্ডার হিস্ট্রি ও বাস্কেট অ্যানালাইসিস সিগন্যাল)
3. **Tier 3: Complement map** (`ComplementMap` — same-leaf category নয়; কেস → প্রোটেক্টর/চার্জার)
4. **Tier 4: Global Bestseller Fallback** (ইনভেন্টরি-শিল্ডেড বেস্টসেলার; উইজেট টাইটেল: Popular)

---

## 💰 Fair Capped Pricing Matrix

| প্ল্যান | মাসিক ফি | ক্যাপ ও ফিচারসমূহ |
|:---|:---|:---|
| **Free Tier** | **$০ / মাস** | প্রতি মাসে $৫০০ অ্যাপ সেলস পর্যন্ত সম্পূর্ণ ফ্রি • FBT উইজেট • ৪-টিয়ার ওয়াটারফল |
| **Starter** | **$১৯ / মাস** | $২,০০০ সেলস ক্যাপ • FBT বান্ডেল • স্মার্ট কার্ট ড্রয়ার ও প্রগ্রেস বার |
| **Growth (Sweet Spot)** | **$৪৯ / মাস** | $৭,৫০০ সেলস ক্যাপ • চেকআউট এক্সটেনশন • ১২০s পোস্ট-পারচেজ • সোশ্যাল প্রুফ ব্যাজ |
| **Pro / Scale** | **$৯৯ / মাস** | আনলিমিটেড সেলস • ইন-উইজেট A/B টেস্টিং • VisualAI • প্রায়োরিটি সাপোর্ট |

---

## 🚀 The 12 Agile Micro-Phases

- [x] **Phase 0:** Market Research, Competitor Reverse-Engineering & Architecture Blueprint
- [ ] **Phase 1:** Project Setup & Cloudflare Edge Shell (React Router v7 + Cloudflare Workers)
- [ ] **Phase 2:** Cloudflare D1 Schema & Fast-ACK Webhook Pipeline (< 25ms)
- [ ] **Phase 3:** Theme App Extension & Core Custom Elements (< 5KB)
- [ ] **Phase 4:** PDP Frequently Bought Together (FBT) Block with Inline Swatches
- [ ] **Phase 5:** 4-Tier Sub-15ms Edge Waterfall Algorithm
- [ ] **Phase 6:** 1-Click Multi-Add to Cart & Shopify Automatic Bundle Discounts
- [ ] **Phase 7:** Explainable AI Badges & Zero-Stock Inventory Shield
- [ ] **Phase 8:** Smart Slide Cart Drawer & Tiered Progress Bar
- [ ] **Phase 9:** Omnichannel Carousels & 5-Minute Vertical Rule Templates
- [ ] **Phase 10:** Checkout UI Extension Bump & 120-Second Post-Purchase Upsell
- [ ] **Phase 11:** Polaris Merchant Admin Dashboard & 5-Stage Funnel Analytics
- [ ] **Phase 12:** "Built for Shopify" 💎 Audit, Lighthouse 100/100 Tuning & App Store Launch

---
*Maintained by the Core Engineering Team.*
