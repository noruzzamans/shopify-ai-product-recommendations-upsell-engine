# 🚀 Shopify AI Product Recommendations & Upsell Engine
**প্রজেক্ট স্ট্র্যাটেজি, ডেটা অ্যানালাইসিস এবং এক্সিকিউশন গাইড**  
**নোট:** অ্যাপের অফিশিয়াল নাম বোর্ড মিটিংয়ে চূড়ান্ত হবে।  
**লাইভ কম্পিটিটর স্ন্যাপশট:** [COMPARISON.md](COMPARISON.md) (সেপ্টেম্বর ২০২৬) — এই ফাইলের সাথে কনফ্লিক্ট হলে COMPARISON জিতবে।

---

## 👥 টিম লিডারশিপ ও রোলস (Leadership & Roles Definition)

প্রজেক্টের সুনির্দিষ্ট কর্মবন্টন এবং টিম গভর্নেন্স মডেল:

| টিম মেম্বার | অফিশিয়াল রোল (Role) | মূল দায়িত্ব ও কাজের পরিধি (Core Responsibilities) |
| :--- | :--- | :--- |
| **এনামুল ভাই** | **Team Lead & Strategic Director** | • **কোর ভিশন ও ডিরেকশন:** ইনিশিয়াল প্রজেক্ট স্ট্র্যাটেজি গাইডলাইন প্রদান এবং সামগ্রিক প্রোডাক্ট ভিশন পরিচালনা।<br>• **স্কোপ ও প্রায়োরিটি নির্ধারণ:** কোন মার্কেট সেগমেন্টে ফোকাস করা হবে ও কোন কোন ফিচার আগে আসবে তা চূড়ান্ত অনুমোদন।<br>• **স্ট্র্যাটেজিক রিভিউ ও মেন্টরশিপ:** রিসার্চ ও ইঞ্জিনিয়ারিং মাইলস্টোন নিয়মিত যাচাই, রিভিউ এবং কৌশলগত দিকনির্দেশনা প্রদান।<br>• **বিজনেস ও জিটিএম (GTM):** প্রোডাক্টের প্রাইসিং স্ট্র্যাটেজি, মার্কেট-ফিট এবং বিজনেস অ্যালাইনমেন্ট নিশ্চিতকরণ। |
| **নুরুজ্জামান রুবেল** | **Lead Engineer & Product Manager (PM)** | • **প্রোডাক্ট ও কম্পিটিটর রিসার্চ:** এনামুল ভাইয়ের স্ট্র্যাটেজিক গাইডের ওপর ভিত্তি করে শীর্ষ ৪ প্রতিদ্বন্দীর (LimeSpot, Wiser, **CBB Frequently Bought Together**, Nosto) মেকানিক্স ও দুর্বলতার বিস্তারিত রিভার্স-ইঞ্জিনিয়ারিং ও সুযোগ চিহ্নিতকরণ।<br>• **সিস্টেম আর্কিটেকচার ডিজাইন:** শপিফাই নেটিভ এক্সটেনশন স্যুট, ক্লাউডফ্লেয়ার এজ আর্কিটেকচার (Cloudflare Workers + D1) এবং ৪-টিয়ার ওয়াটারফল রিকমেন্ডেশন ইঞ্জিনের টেকনিক্যাল ব্লুপ্রিন্ট প্রণয়ন।<br>• **হ্যান্ডস-অন ফুল-স্ট্যাক ডেভেলপমেন্ট:** React Router v7, Shopify Polaris, Native Vanilla JS Custom Elements (< ৫KB), Cloudflare Edge Workers ও শপিফাই ওয়েবহুকের সম্পূর্ণ হ্যান্ডস-অন কোডিং ও অ্যাপ্লিকেশন ডেভেলপমেন্ট।<br>• **ইঞ্জিনিয়ারিং স্ট্যান্ডার্ডস ও কোয়ালিটি:** [ENGINEERING_STANDARDS_AND_PATTERNS.md](ENGINEERING_STANDARDS_AND_PATTERNS.md) অনুযায়ী বিশ্বমানের ক্লিন কোড, পারফরম্যান্স (< ৫KB সাইজ), ১০০/১০০ লাইটহাউস স্কোর এবং "Built for Shopify" কমপ্লায়েন্স নিশ্চিতকরণ। |

---

## ১. নির্বাহী সিদ্ধান্ত (Executive Decision: কোন প্রোডাক্ট বানাবেন?)

সমস্ত মার্কেট ডেটা, কম্পিটিটর অ্যানালাইসিস এবং মার্চেন্ট সাইকোলজি বিবেচনা করে চূড়ান্ত সিদ্ধান্ত:

> **অফিশিয়াল অ্যাপের নাম:** *[বোর্ড মিটিংয়ে নির্ধারিত হবে / TBD]*  
> **কোর পজিশনিং:** *"Wiser-এর দামে ($০-$৪৯/মাস) LimeSpot ও Nosto-এর চেয়ে দ্রুত এবং স্মার্ট AI রিকমেন্ডেশন — ৫ মিনিটে নো-কোড সেটআপ ও ট্রান্সপারেন্ট লজিক।"*

---

## ২. কী কী ডেটার ওপর ভিত্তি করে এই সিদ্ধান্ত নেওয়া হয়েছে? (Data-Driven Justifications)

পূর্ণ সেল-বাই-সেল ম্যাট্রিক্স: [COMPARISON.md](COMPARISON.md)। নিচে শুধু সেই দাবিগুলো রাখা হয়েছে যেগুলো **লাইভ লিস্টিং / অ্যাডমিন টিয়ারডাউন** দিয়ে ধরা যায়।

### ডেটা পয়েন্ট ১: লাইভ প্রাইস গ্যাপ (verified September 2026)
SMB ব্যান্ড ইতিমধ্যে ভরা — খালি নয়:

| অ্যাপ | লাইভ প্রাইস | রেটিং | কী প্রমাণিত দুর্বলতা |
| :--- | :--- | :--- | :--- |
| **LimeSpot** | Turbo $0–~$400 (অর্ডার); Max $50–$1,700 (রেভিনিউ) | 4.6 ★ / 507 | এক্সটার্নাল `app.limespot.com`; CSS sibling inject; লাইভ প্রিভিউতে OOS প্রোডাক্ট; পোস্ট-পারচেজ কার্ড/Shop Pay-only |
| **Wiser** | $0 / $9 / $19 / $49 (অর্ডার ক্যাপ) | 4.9 ★ / 559 | স্লাইড কার্ট আছে (ডেমো)। অ্যাডমিন ওয়াটারফল টিয়ারডাউন হয়নি — “জেনেরিক AI” / ৫০% চার্ন **এই প্যাকে প্রমাণিত নয়** |
| **CBB FBT** (আগে ভুল নাম: Julius) | $0 (৩ ম্যানুয়াল বান্ডেল) / $14.99 / $19.99 / $39.99 আনলিমিটেড | 4.9 ★ / 1,200+ · Built for Shopify | শক্ত PDP FBT + ৪-টিয়ার ওয়াটারফল; **কার্ট ড্রয়ার / চেকআউট / পোস্ট-পারচেজ নেই** |
| **Nosto** | অ্যাপ স্টোরে SKU নেই; আউটসাইড বিল; টিয়ারডাউন রেঞ্জ $500–$2,500+ | 4.7 ★ / 61 | সেলস-লেড; চেকআউট রেকস Plus-গেটেড; VisualAI আছে |

আমাদের পজিশন এই টেবিলের ওপর: **Wiser-এর $0–$49 ব্যান্ডে** CBB-লেভেল FBT + LimeSpot-এর OOS/এমবেড গ্যাপ বন্ধ করা — LimeSpot Max বা Nosto এন্টারপ্রাইজ প্রাইস কাটার দাবি নয়।

### ডেটা পয়েন্ট ২: মার্চেন্ট সাইকোলজি (ক্যাটাগরি লজিক, লিফট নম্বর নয়)
রিকমেন্ডেশন অ্যাপ মার্চেন্ট ড্যাশবোর্ডে অ্যাট্রিবিউটেড ডলার দেখায় বলে চ্যাটবট/ইমেজ-জেনারেটরের চেয়ে **রেভিনিউ সেন্টার** হিসেবে বিক্রি হয়। CBB-এর ৫-স্টেজ ফানেল (`Rendered → Converted`) এই মডেলের লাইভ প্রমাণ।  
**২x–৫x কনভার্সন / ২৫০–৪০০% ROI** এই রিপোতে মাপা হয়নি — ভেন্ডর মার্কেটিং; [COMPARISON.md](COMPARISON.md) অ্যাপেন্ডিক্স দেখুন।

### ডেটা পয়েন্ট ৩: প্রমাণিত ফিচার গ্যাপ (teardown থেকে)
* **Storefront explainer নেই** চারজনের কাছেই (CBB Bundle explorer শুধু অ্যাডমিন)।
* **LimeSpot OOS বাগ** লাইভ প্রিভিউতে ধরা (“The Out of Stock Snowboard”)। CBB-তে outbound exclusion আছে; ওয়েবহুক-ইনস্ট্যান্ট হাইড আলাদা কথা।
* **LimeSpot/Nosto অ্যাডমিন শপিফাইয়ের বাইরে**; CBB এমবেডেড।
* **A/B ইউনিক নয়:** LimeSpot Max-এ A/B/n, Nosto-তে স্ট্যাটিস্টিক্যাল A/B আছে। CBB-তে নেই।
* **ভার্টিক্যাল প্রিসেট:** LimeSpot অনবোর্ডিংয়ে ১২টি ইন্ডাস্ট্রি আছে — “কারো নেই” বলা যাবে না। আমাদের গ্যাপ হলো ৫-মিনিট টেমপ্লেটের সরলতা, ইন্ডাস্ট্রি ক্যাটাগরির অস্তিত্ব নয়।

### ডেটা পয়েন্ট ৪: Shopify ট্যাক্সোনমি (ecosystem)
* স্ট্যান্ডার্ড প্রোডাক্ট ট্যাক্সোনমি (ভার্টিক্যাল / ক্যাটাগরি / অ্যাট্রিবিউট) ক্যাটাগরি-ম্যাচ ফলব্যাকের জন্য প্রাসঙ্গিক।
* “AI সার্চ থেকে অর্ডার ১৫ গুণ” — এই প্যাকে সোর্স নেই; সাইট না হওয়া পর্যন্ত এক্সিকিউটিভ জাস্টিফিকেশনে ব্যবহার করবেন না।

---

## ৩. অ্যাপের মূল ৩টি ইউনিক ফিচার (Killer Differentiators)

প্রতিযোগীদের পেছনে ফেলতে তিনটি বেট — **“কারো নেই” নয়**, টিয়ারডাউন অনুযায়ী গ্যাপ:

1. **Feature 1: Recommendation Explainer (স্টোরফ্রন্ট)**
   * চারজনই জেনেরিক লেবেল দেয় (*You May Like*)। CBB-এর Bundle explorer অ্যাডমিন-অনলি।
   * আমাদের বেট: উইজেটে *"৭৩% কাস্টমার এই শার্টের সাথে এটি কিনেছেন"*। CTR লিফট এখনো মাপা হয়নি।

2. **Feature 2: 5-Minute Vertical Templates**
   * LimeSpot-এ ১২টি ইন্ডাস্ট্রি অনবোর্ডিং আছে; CBB-তে ৩-ধাপ উইজার্ড ~৬০ সেকেন্ড।
   * আমাদের বেট: ফ্যাশন / বিউটি / ইলেকট্রনিক্স প্রিসেট আরও কম কনফিগে — “৪৫ দিন vs ৫ মিনিট” LimeSpot Turbo-এর লাইভ ইনস্টলের সাথে মেলে না।

3. **Feature 3: Real-Time Zero-Stock Shield**
   * LimeSpot লাইভ প্রিভিউতে OOS রেকমেন্ড করেছে। CBB-তে ম্যানুয়াল exclusion আছে।
   * আমাদের বেট: `inventory_levels/update` ওয়েবহুক দিয়ে উইজেট থেকে ইনস্ট্যান্ট হাইড।

---

## ৪. AI Engine-এ ব্যবহৃত ডেটা সিগন্যালসমূহ (Data Signals)

একটি স্বয়ংসম্পূর্ণ পার্সোনালাইজেশন চালাতে আপনার সিস্টেম ৪ স্তরের ডেটা ব্যবহার করবে:

```text
               ┌───────────────────────────────┐
               │     Shopify Customer Events   │
               │ (Browse, Cart, Wishlist, Time)│
               └───────────────┬───────────────┘
                                │
                                ▼
┌────────────────────────┐           ┌────────────────────────┐
│  Catalog Metadata &    │  ======>  │   Edge recs engine     │
│  Real-Time Inventory   │           │ (Workers + D1 waterfall)│
└────────────────────────┘           └───────────┬────────────┘
                                                 │
                                                 ▼
                                     ┌────────────────────────┐
                                     │  Explainable Widgets   │
                                     │  (PDP, Cart Drawer)    │
                                     └────────────────────────┘
```

1. **Behavioral Data (আচরণগত):** পেজভিউ, স্ক্রোল ডেপথ, কার্ট অ্যাড, উইশলিস্ট, ফিল্টার সিলেকশন।
2. **Catalog Metadata (পণ্যের তথ্য):** ট্যাগ, টাইটেল, ম্যাটেরিয়াল, সাইজ ভ্যারিয়েন্ট, প্রাইস মার্জিন।
3. **Association Data (ক্রাউড ডেটা):** মার্কেট বাস্কেট অ্যানালাইসিস (কোন দুটি আইটেম একই অর্ডারে বেশিবার বিক্রি হয়)।
4. **Vertical Logic (ইন্ডাস্ট্রি লজিক):** ফ্যাশন সাইজ ম্যাচিং বা ইলেকট্রনিক্স মডেল কমপ্যাটিবিলিটি।

---

## ৫. প্রস্তাবিত টেকনিক্যাল আর্কিটেকচার ও শপিফাই এক্সটেনশনস (World-Class Edge Architecture)

বিশ্বমানের শীর্ষস্থানীয় (World-Class Tier-1) শপিফাই অ্যাপগুলোতে যেভাবে আল্ট্রা-স্কেলেবল ও হাই-পারফরম্যান্স এজ কম্পিউটিং ব্যবহার করা হয়, আমাদের অ্যাপটি হুবহু সেই আন্তর্জাতিক আর্কিটেকচারাল স্ট্যান্ডার্ড অনুযায়ী ডিজাইন করা হয়েছে:

### শপিফাই এক্সটেনশন স্যুট (Extensions Suite):
1. **Storefront FBT Block (`blocks/pdp-fbt.liquid`):** Liquid + Vanilla JS কাস্টম এলিমেন্ট (`<clearrecs-fbt>`) — সাইজ < ৫KB, কোনো থিম স্লোডাউন নেই।
2. **Smart Cart Drawer (`blocks/smart-cart.liquid`):** Liquid + Vanilla JS কাস্টম এলিমেন্ট (`<clearrecs-cart-drawer>`) — স্লাইড কার্ট ও মাল্টি-টিয়ার প্রগ্রেস বার।
3. **Omnichannel Carousel (`blocks/carousel.liquid`):** হোমপেজ ও কালেকশন পেজে রেকমেন্ডেশন স্লাইডার ব্লক।
4. **Checkout Upsell Bump (`purchase.checkout.block.render`):** `@shopify/ui-extensions` দিয়ে নির্মিত ১-ক্লিক অর্ডার বাম্প।
5. **Post-Purchase 1-click (`Checkout::PostPurchase::Render`):** পেমেন্টের পর, থ্যাংক-ইউয়ের আগে; সাইনড চেঞ্জসেট দিয়ে **একই অর্ডারে** লাইন যোগ। কার্ড/Shop Pay only; এক অ্যাপের স্লট। ১২০ সেকেন্ড টাইমার LimeSpot থেকে নেওয়া।
6. **Thank-you block (`purchase.thank-you.block.render`):** কনটেন্ট/রেকস — মূল অর্ডারে ১-ক্লিক অ্যাড নয়।
7. **Customer Account Reorder (`customer-account.order-status.block.render`):** Customer Account UI extension (চেকআউট প্যাকেজ নয়)।
8. **Web Pixel Tracker (`app-pixel`):** স্যান্ডবক্সড জিরো-ল্যাটেন্সি GDPR কমপ্লায়েন্ট ইভেন্ট ট্র্যাকার।

### মূল টেকনোলজি স্ট্যাক (Cloudflare Edge Architecture):
| স্তর | প্রযুক্তি | ভূমিকা |
| :--- | :--- | :--- |
| **Merchant Dashboard**| React Router v7 + Polaris + App Bridge v4 | নেটিভ শপিফাই অ্যাডমিন এক্সপেরিয়েন্স ও আধুনিক কন্ট্রোলার-ভিউ আর্কিটেকচার। |
| **Edge Server & Runtime**| Cloudflare Workers (`workers/app.js`) | Recs metafield / App Proxy p99 < 500ms। Workers Paid $0 নয়। |
| **Edge Database** | Cloudflare D1 (`migrations/*.sql`) | `CoPurchaseMatrix` + `ProductOrderStats` + `InventoryItemMap` + `AttributedLineItems`। |
| **Checkout Extensions** | `@shopify/ui-extensions` + Discount Function | Function = বান্ডেল ছাড়। চেকআউট অফার Plus-গেটেড। |
| **Storefront Widgets** | Liquid + Custom Elements | **Per-widget** gzip; FBT < 5KB। পাবলিক recs GET নয়। |
| **Webhook Engine** | Queue Fast-ACK, p99 < 500ms | Hygiene + GDPR Phase 2। `inventory_item_id` ম্যাপ। |
| **Styling & Design System**| Sass / SCSS (BEM & Tokens) | `_tokens.scss` ও `_base.scss` ভিত্তিক ক্লিন ও প্রিমিয়াম সিএসএস। |

---

## ৬. সংশোধিত ফেয়ার ক্যাপড প্রাইসিং মডেল (Fair Capped Pricing)

মার্কেট লিডারদের রেভিনিউ কাটার ট্র্যাপ এবং উচ্চ মূল্যের বাধা ভেঙে আমাদের স্বচ্ছ প্রাইসিং:

* **Free Tier ($0/মাস):** $৫০০ **অ্যাট্রিবিউটেড** সেলস (`_cr_src` লাইন)। ক্যাপ ছাড়ালে উইজেট বন্ধ নয়।
* **Starter ($১৯/মাস):** $২,০০০ অ্যাট্রিবিউটেড + FBT + Discount Function। কার্ট ড্রয়ার পরে।
* **Growth ($৪৯/মাস):** $৭,৫০০ অ্যাট্রিবিউটেড + explainer ব্যাজ। চেকআউট প্রোডাক্ট অফার Plus — SMB হেডলাইন নয়। পোস্ট-পারচেজ অপশনাল (এক স্লট)।
* **Scale ($৯৯/মাস):** **GMV ক্যাপ নেই।** A/B + VisualAI হাইপোথিসিস। “Fair capped unlimited” বলা যাবে না।

---

## ৭. ৪-ফেজের ডেভেলপমেন্ট ও রিলিজ টাইমলাইন (8-9 Weeks Sprint)

```text
[Phase 1: Core Engine & FBT MVP] ───► [Phase 2: Smart Cart & Multi-Page]
      (সপ্তাহ ১ - ৩ / ১৫-১৮ দিন)                   (সপ্তাহ ৪ - ৫ / ১০-১২ দিন)
      • React Router v7 & Edge Setup                    • Slide Cart Drawer + Progress Bar
      • App Embed & PDP FBT Widget                • Home/Collection/Cart Carousels
      • ৪-টিয়ার ওয়াটারফল ব্যাকএন্ড                • Explainable AI Badges
      • ইনলাইন ভ্যারিয়েন্ট সোয়াচ                 • Web Pixel Tracking
                      │                                           │
                      ▼                                           ▼
[Phase 3: Checkout & Advanced AI] ──► [Phase 4: Polish, A/B Test & Launch]
      (সপ্তাহ ৬ - ৭ / ১০-১২ দিন)                   (সপ্তাহ ৮ - ৯ / ১০-১২ দিন)
      • Checkout UI Extension                     • ইন-উইজেট A/B টেস্টিং
      • Post-Purchase 120s Upsell                 • "Built for Shopify" অডিট
      • VisualAI & Replenishment Rules            • ড্যাশবোর্ড অ্যানালিটিক্স
      • জিরো-স্টক রিয়েল-টাইম শিল্ড                • শপিফাই অ্যাপ স্টোর লাইভ
```

---

## ৮. মাস্টার আর্কিটেকচার ব্লুপ্রিন্ট ও কম্পিটিটর রিসার্চ ফাইলসমূহ (Master References)

সম্পূর্ণ বিস্তারিত টেকনিক্যাল স্পেসিফিকেশন, ডেটা ফ্লো এবং কোড আর্কিটেকচার আলাদা ডেডিকেটেড মাস্টার ফাইলে সংরক্ষিত রয়েছে:

* 📌 **Frozen comparison (this pack’s source of truth):** [COMPARISON.md](COMPARISON.md)
* 💎 **মাস্টার আর্কিটেকচার ও এক্সিকিউশন রোডম্যাপ:** [MASTER_ARCHITECTURE_AND_ROADMAP.md](MASTER_ARCHITECTURE_AND_ROADMAP.md)
* 📜 **ইঞ্জিনিয়ারিং স্ট্যান্ডার্ডস ও প্যাটার্নস:** [ENGINEERING_STANDARDS_AND_PATTERNS.md](ENGINEERING_STANDARDS_AND_PATTERNS.md)
* 🔍 **LimeSpot Personalizer ডিপ-ডাইভ:** [competitors/LIMESPOT.md](competitors/LIMESPOT.md)
* 🔍 **Wiser Recommendations ডিপ-ডাইভ:** [competitors/WISER.md](competitors/WISER.md)
* 🔍 **CBB Frequently Bought Together ডিপ-ডাইভ:** [competitors/CBB_FREQUENTLY_BOUGHT_TOGETHER.md](competitors/CBB_FREQUENTLY_BOUGHT_TOGETHER.md)
* 🔍 **Nosto Experience Cloud ডিপ-ডাইভ:** [competitors/NOSTO.md](competitors/NOSTO.md)
* 🚀 **এনামুল ভাইয়ের প্রোডাক্ট স্ট্র্যাটেজি গাইড (original memo):** [ENAMUL_SUGGEST_SHOPIFY_PRODUCT_RECOMMENDATIONS_COMPETITIVE_STRATEGY.md](ENAMUL_SUGGEST_SHOPIFY_PRODUCT_RECOMMENDATIONS_COMPETITIVE_STRATEGY.md)
