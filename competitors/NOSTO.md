# 🔍 Nosto (AI Search & Discovery) — Enterprise Deep Dive
**ফোল্ডার:** `competitors/`  
**উৎস:** শপিফাই অ্যাপ স্টোর লাইভ লিস্টিং ও অফিশিয়াল প্রোফাইল  
**স্ট্যাটাস:** এন্টারপ্রাইজ কমার্স এক্সপেরিয়েন্স প্ল্যাটফর্ম (Shopify Plus Focus)  
**সর্বশেষ আপডেট:** সেপ্টেম্বর ২০২৬  

---

## ১. অ্যাপ পরিচিতি ও লাইভ প্রোফাইল (App Store Overview)

| তথ্য ক্ষেত্র | লাইভ ডেটা (স্ক্রিনশট অনুযায়ী) |
| :--- | :--- |
| **অফিশিয়াল অ্যাপের নাম** | **Nosto \| AI Search & Discovery** |
| **ডেভেলপার** | **Nosto Solutions Ltd** |
| **শপিফাই অ্যাপ স্টোর লিংক** | [apps.shopify.com/nosto-personalization-for-shopify](https://apps.shopify.com/nosto-personalization-for-shopify) |
| **রেটিং ও রিভিউ সংখ্যা** | **4.7 ★** (মাত্র **৬১টি** রিভিউ) ⚠️ |
| **প্রাইসিং মডেল** | **"Free to install" (হিডেন এন্টারপ্রাইজ বিলিং ট্র্যাপ)** |
| **বিলিং নোটিস** | *"A Nosto account is required and is not free of charge. External charges may be billed separately. Contact Nosto for details."* |
| **সাপোর্টেড ভাষা (৩টি)** | English, French, German |

### অফিশিয়াল হেডলাইন ও ভ্যালু প্রপোজিশন:
> *"Intelligent Commerce Experience Platform helping brands increase online engagement and revenue."*  
> *"We help online brands transform the commerce experience by enriching and connecting customer, product, and content data so they can deliver personalized experiences at scale."*

---

## ২. কোর ফিচার ও ৫টি প্ল্যাটফর্ম পিলার (Core Capabilities)

Nosto নিজেকে শুধু একটি সাধারণ রিকমেন্ডেশন অ্যাপ হিসেবে উপস্থাপন করে না; তারা একটি পূর্ণাঙ্গ **Commerce Experience Platform (CXP)**:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                 Nosto AI Commerce Experience Platform (CXP)                 │
│                                                                             │
│  [1. AI Site Search]          [2. 1-to-1 Personalization]                   │
│  • Personalized Search        • Customer Affinity Profiling                 │
│  • Semantic Autocomplete      • Real-time Intent & Sizing                   │
│                                                                             │
│  [3. Visual Merchandising]    [4. UGC & Dynamic Content]                    │
│  • Drag-and-drop Ranking      • Authentic Social Proof                      │
│  • Margin / Stock Rules       • Personalized Banners                        │
│                                                                             │
│                   [5. Business Intelligence (BI)]                           │
│                   • Shopper Segment Deep-Dives                              │
│                   • Attribution & Discovery Metrics                         │
└─────────────────────────────────────────────────────────────────────────────┘
```

1. **১-টু-১ কাস্টমার অ্যাফিনিটি প্রোফাইলিং (Individual Affinity Graph):**  
   * লাইভ ভিডিওতে দেখানো অনুযায়ী—প্রতিটি গ্রাহকের জন্য আলাদা প্রোফাইল তৈরি হয় (যেমন: গ্রাহক *Hannah Laurent*-এর প্রিয় ক্যাটাগরি: *T-Shirts, Hoodies*; প্রিয় রঙ: *Yellow*; সাইজ: *Medium*)।
   * এর ফলে একই পেজে দুই ভিন্ন গ্রাহক সম্পূর্ণ ভিন্ন ও পারসোনালাইজড প্রোডাক্ট দেখে।
2. **AI Site Search (সার্চ ও ডিসকভারি):**  
   * গ্রাহকের আগের সার্চ ও ক্রয়ের ওপর ভিত্তি করে সার্চ রেজাল্ট পারসোনালাইজ করে।
3. **ভিজুয়াল মার্চেন্ডাইজিং (Merchandising Rules):**  
   * মার্চেন্ট হাই-মার্জিন বা বেশি স্টক থাকা পণ্যগুলোকে রিকমেন্ডেশনের শীর্ষে পিন করে রাখতে পারে।
4. **ইউজিসি ও ডায়নামিক কনটেন্ট (UGC & Content Personalization):**  
   * ইনস্টাগ্রাম ও টিকটক থেকে ইউজিসি (User Generated Content) এনে রিকমেন্ডেশন উইজেটের সাথে দেখায়।
5. **বিজনেস ইন্টেলিজেন্স (BI Analytics):**  
   * গ্রাহকদের কেনাকাটার আচরণ ও ট্রেন্ডের ওপর গভীর ডেটা ইনসাইটস।

---

## ২. লাইভ ড্যাশবোর্ড ও ক্লাউড আর্কিটেকচার (Live Dashboard & SaaS Architecture)

`noruzzaman-dev-store`-এ Nosto ইনস্টল করার পর সরাসরি তাদের লাইভ এন্টারপ্রাইজ ড্যাশবোর্ড (`my.nosto.com/admin/shopify-[id]/dashboard`) উন্মোচিত হয়েছে:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          my.nosto.com Cloud Admin                           │
│                                                                             │
│  [Top Navigation Architecture]                                              │
│  ├── Dashboard (Central Health & Analytics)                                 │
│  ├── Experience.AI ▾ (Autonomous ML & Segmentation Engine)                 │
│  ├── Product Experience Cloud ▾ (PXC: Search, Merchandising & Recs)         │
│  ├── Content Experience Cloud ▾ (CXP: UGC, Dynamic Banners & Copy)          │
│  └── ✨ Ask Huginn [Beta] (Generative AI Merchandising Copilot)              │
│                                                                             │
│  [Core Functional Modules]                                                  │
│  ├── 1. AI Segments Opportunities: প্রোঅ্যাকটিভ অটোনোমাস সেগমেন্ট সাজেশন     │
│  ├── 2. Behavioral Profiles: রিয়েল-টাইম কাস্টমার ট্র্যাকিং ও Live Feed       │
│  ├── 3. UGC Monitoring: সোশ্যাল মিডিয়া (Instagram/TikTok) কনটেন্ট মাইনিং    │
│  ├── 4. Scheduling: টাইম-বেসড ক্যাম্পেইন অটোমেশন                            │
│  └── 5. Integrations & APIs: Klaviyo, Meta Pixel, Google Analytics, Dotdigital│
└─────────────────────────────────────────────────────────────────────────────┘
```

### ১. এক্সটার্নাল এন্টারপ্রাইজ সাশ (Dedicated Cloud Infrastructure)
* লাইমস্পটের মতো Nosto শপিফাই অ্যাডমিনের ভেতর চলে না; তারা তাদের হাই-পারফরম্যান্স ডেডিকেটেড ক্লাউড পোর্টাল **`my.nosto.com`**-এ চলে।
* এটি অত্যন্ত দ্রুত এবং মিলি-সেকেন্ড রেসপন্স টাইমে বড় বড় স্টোরের লাখ লাখ ট্রাফিক হ্যান্ডেল করতে সক্ষম।

---

### ২. ৩টি কোর ক্লাউড পিলার (The Three Cloud Pillars)
Nosto-এর পুরো প্রোডাক্ট লাইন ৩টি প্রধান এন্টারপ্রাইজ পিলারে বিভক্ত:
1. **Experience.AI:**  
   * অটোনোমাস মেশিন লার্নিং ইঞ্জিন, যা স্বয়ংক্রিয়ভাবে গ্রাহকদের ডেটা বিশ্লেষণ করে ক্লাস্টার ও সেগমেন্ট তৈরি করে।
2. **Product Experience Cloud (PXC):**  
   * সাইট সার্চ, ক্যাটাগরি মার্চেন্ডাইজিং এবং প্রোডাক্ট পেজ / কার্ট রিকমেন্ডেশন উইজেট নিয়ন্ত্রণ করে।
3. **Content Experience Cloud (CXP):**  
   * ডায়নামিক ব্যানার, পারসোনালাইজড টেক্সট এবং সোশ্যাল ইউজিসি (UGC) রিকমেন্ডেশনের সাথে ইন্টিগ্রেট করে।

---

### ৩. জেনারেটিভ এআই কোপাইলট — `✨ Ask Huginn [Beta]`
* নর্ডিক মিথলজির ওডিনের কাক "Huginn"-এর নামানুসারে Nosto তাদের নিজস্ব **Generative AI Copilot** তৈরি করেছে।
* মার্চেন্ট সাধারণ ভাষায় চ্যাট করে (`"Show me low-performing bundles"` বা `"Create a VIP discount campaign"`) তাৎক্ষণিকভাবে ক্যাম্পেইন সাজাতে পারে।

---

### ৪. বিহেভিওরাল প্রোফাইল ও লাইভ ফিড (Behavioral Profiles & Live Feed)
* Nosto-এর মূল চালিকাশক্তি হলো **"Behavioral Profiles"**।
* প্রতিটি ভিজিটর সাইটে ঢুকলে তার জন্য একটি ডাইনামিক প্রোফাইল তৈরি হয়, যা তার ক্লিক, ব্রাউজিং ক্যাটাগরি, সাইজ প্রেফারেন্স ও কার্ট ভ্যালু রিয়েল-টাইমে ট্র্যাক করে।
* **Live Feed:** মার্চেন্ট একটি লাইভ ফিড দেখতে পারে যেখানে স্টোরে এই মুহূর্তে কোন গ্রাহক কী ব্রাউজ করছে তা লাইভ দেখা যায়!

---

### ৫. গভীর ইকোসিস্টেম ইন্টিগ্রেশন (Klaviyo, Meta, GA4)
* **Klaviyo Integration:** ব্রাউজিং বিহেভিয়ার সরাসরি Klaviyo-তে পুশ করে পারসোনালাইজড ব্যাক-ইন-স্টক বা ব্রাউজ অ্যাবান্ডনমেন্ট ইমেইল পাঠাতে পারে।
* **Meta & Google Analytics:** ক্রস-চ্যানেল রিটার্গেটিংয়ের জন্য সরাসরি অডিয়েন্স সিঙ্ক।

---

## ৩. `Experience.AI` কোর ইঞ্জিন ও ৭টি এন্টারপ্রাইজ পিলার (The 7 Pillars of Experience.AI)

লাইভ ড্যাশবোর্ডের `Experience.AI` ড্রপডাউন থেকে উন্মোচিত হয়েছে তাদের এন্টারপ্রাইজ পারসোনালাইজেশন ফ্রেমওয়ার্ক:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       Experience.AI Navigation Suite                        │
│                                                                             │
│  [1. Business Analytics]             [2. Audience Insights & Builder]       │
│  • রেভিনিউ অ্যাট্রিবিউশন              • ডায়নামিক বিহেভিওরাল সেগমেন্টেশন      │
│  • ডিসকভারি পাথ ট্র্যাকিং              • আরএফএম (RFM) ও লাইফটাইম ভ্যালু ক্লাস্টার│
│                                                                             │
│  [3. Product Intelligence]           [4. UGC Monitoring]                    │
│  • ক্যাটালগ অ্যাট্রিবিউট এনরিচমেন্ট    • ইনস্টাগ্রাম/টিকটক সোশ্যাল প্রুফ      │
│  • ভিজুয়াল সিমিলারিটি ও ইনভেন্টরি পেসিং• ইউজিসি ট্যাগিং ও মডারেশন            │
│                                                                             │
│  [5. Global Merchandising]           [6. Campaign Testing]                  │
│  • স্টোর-ওয়াইড র‍্যাঙ্কিং রুলস        • ইন-অ্যাপ নেটিভ A/B ও মাল্টিভেরিয়েট  │
│  • মার্জিন বুস্টিং ও স্টক সুরক্ষা      • স্ট্যাটিস্টিক্যাল সিগনিফিকেন্স ইঞ্জিন  │
│                                                                             │
│                        [7. Placements Architecture]                         │
│                        • ডিকাপল্ড হেডলেস প্লেসমেন্ট স্লট                      │
│                        • যেকোনো পেজে কনটেন্ট ও উইজেট ম্যাপিং                  │
└─────────────────────────────────────────────────────────────────────────────┘
```

| এন্টারপ্রাইজ মডিউল | কাজের প্রক্রিয়া ও আর্কিটেকচারাল গুরুত্ব |
| :--- | :--- |
| **১. Business Analytics** | কোন কোন রিকমেন্ডেশন বা সার্চ কোয়েরি থেকে কত ডলার সেলস এসেছে তার এন্ড-টু-এন্ড অ্যাট্রিবিউশন। |
| **২. Audience Insights & Builder** | ক্রেতাদের আচরণের ওপর ভিত্তি করে ডাইনামিক অডিয়েন্স তৈরি (যেমন: *"গত ৭ দিনে ৩ বার উইন্টার জ্যাকেট দেখেছে এমন ক্রেতা"* বা *"ডিসকাউন্ট খুঁজছে এমন প্রাইস-সেনসিটিভ ভিজিটর"* )। |
| **৩. Product Intelligence** | স্বয়ংক্রিয়ভাবে প্রোডাক্টের বৈশিষ্ট্য (কালার, স্টাইল, মার্জিন, স্টক ডেপথ) বিশ্লেষণ করে স্মার্ট অ্যাসোসিয়েশন তৈরি করে। |
| **৪. UGC Monitoring** | সোশ্যাল মিডিয়া থেকে কাস্টমারদের ছবি ও ভিডিও এনে সরাসরি রিকমেন্ডেশন উইজেটে যুক্ত করে কনভার্সন রেট বাড়ানো। |
| **৫. Global Merchandising** | মার্চেন্ট চাইলে উচ্চ মুনাফার (High Margin) পণ্যগুলোকে রিকমেন্ডেশনের প্রথমে বুস্ট করতে পারে এবং কম স্টক থাকা পণ্য নিচে নামাতে পারে। |
| **৬. Campaign Testing (Native A/B Testing)** | **প্রতিযোগীদের বড় ফাঁক পূরণ:** LimeSpot বা CBB-তে কোনো নেটিভ A/B টেস্টিং ছিল না। Nosto-তে রয়েছে পূর্ণাঙ্গ স্ট্যাটিস্টিক্যাল A/B টেস্টিং ইঞ্জিন, যা স্বয়ংক্রিয়ভাবে বিজয়ী অ্যালগরিদম নির্বাচন করে। |
| **৭. Placements** | থিমের পেজগুলোতে নির্দিষ্ট "প্লেসমেন্ট স্লট" তৈরি করে রাখা হয়, যাতে মার্চেন্ট কোডিং ছাড়াই যেকোনো স্লটে যেকোনো এআই ক্যাম্পেইন রান করতে পারে। |

> ⚡ **রিয়েল-টাইম ট্র্যাকিং সক্রিয়:**  
> ড্যাশবোর্ডে দেখা যাচ্ছে **`Live behavioral profiles: 12`**! অর্থাৎ Nosto-এর ক্লাউড ট্র্যাকার ইনস্টল হওয়ার সাথে সাথেই স্টোরের ১২ জন ভিজিটরকে রিয়েল-টাইমে ট্র্যাক করে বিহেভিওরাল প্রোফাইল বিল্ড করা শুরু করেছে।

---

## ৪. `Product Experience Cloud` (PXC) আর্কিটেকচার (The 5 Monetization Pillars)

লাইভ ড্যাশবোর্ডের `Product Experience Cloud ▾` ড্রপডাউন থেকে Nosto-এর ৫টি কোর প্রোডাক্ট মনেটাইজেশন মডিউল উন্মোচিত হয়েছে:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       Product Experience Cloud (PXC)                        │
│                                                                             │
│  [1. Recommendations]                [2. Post-Purchase Upsell]              │
│  • অন-সাইট এআই উইজেট (PDP, Cart)     • শপিফাই নেটিভ ১-ক্লিক পোস্ট-পারচেজ    │
│  • মাল্টি-লেয়ার রুলস ও ফিল্টারিং     • চেকআউটের ঠিক পরে তাৎক্ষণিক অফার      │
│                                                                             │
│  [3. Search]                         [4. Personalized Emails]               │
│  • পারসোনালাইজড সাইট সার্চ ও অটোকমপ্লিট• ইমেইল টেমপ্লেটে ডায়নামিক রিকমেন্ডেশন │
│  • টাইপো টলারেন্স ও সিনোনিম মাইনিং   • Klaviyo/Omnisend-এর জন্য এপিআই ব্লক  │
│                                                                             │
│                        [5. Triggered Emails]                                │
│                        • ব্রাউজ অ্যাবান্ডনমেন্ট ও কার্ট রিকভারি             │
│                        • প্রাইস ড্রপ ও ব্যাক-ইন-স্টক স্বয়ংক্রিয় ইমেইল       │
└─────────────────────────────────────────────────────────────────────────────┘
```

| পিএক্সসি (PXC) মডিউল | কাজের প্রক্রিয়া ও আর্কিটেকচারাল গুরুত্ব |
| :--- | :--- |
| **১. Recommendations** | পুরো স্টোরের বিভিন্ন পেজে (Home, Collection, PDP, Cart) মেশিন লার্নিং ভিত্তিক প্রোডাক্ট রিকমেন্ডেশন উইজেট বসানো। |
| **২. Post-Purchase Upsell** | **শপিফাই নেটিভ পোস্ট-পারচেজ ইঞ্জিন:** চেকআউট সম্পন্ন হওয়ার পর কিন্তু থ্যাঙ্কইউ পেজে যাওয়ার আগে গ্রাহককে ১-ক্লিক আপসেল অফার প্রদর্শন করা (যেখানে পেমেন্ট তথ্য পুনরায় টাইপ করতে হয় না)। |
| **৩. Search** | সাধারণ সার্চ বারকে এআই সার্চ ইঞ্জিনে রূপান্তর করা, যাতে গ্রাহকের আগের ক্রয়ের ইতিহাস অনুযায়ী সার্চ রেজাল্ট রিয়েল-টাইমে পারসোনালাইজড হয়। |
| **৪. Personalized Emails** | Klaviyo বা অন্যান্য ইমেইল মার্কেটিং অ্যাপের ভেতরে ডাইনামিক রিকমেন্ডেশন ব্লক এম্বেড করার সুবিধা। |
| **৫. Triggered Emails** | সাইট ছেড়ে চলে যাওয়া ভিজিটরদের কাছে স্বয়ংক্রিয়ভাবে কার্ট রিকভারি, ব্রাউজ অ্যাবান্ডনমেন্ট বা প্রাইস ড্রপ ইমেইল পাঠানো। |

---

## ৫. `Content Experience Cloud` (CXP) আর্কিটেকচার (Content Personalization & Pop-ups)

লাইভ ড্যাশবোর্ডের `Content Experience Cloud ▾` ড্রপডাউন থেকে তাদের কনটেন্ট পারসোনালাইজেশন ও লিড জেনারেশন মডিউল উন্মোচিত হয়েছে:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       Content Experience Cloud (CXP)                        │
│                                                                             │
│  [1. Content Personalization]                [2. Pop-ups Engine]            │
│  • ডায়নামিক হিরো ব্যানার ও হেডলাইন           • এক্সিট-ইনটেন্ট (Exit-Intent)  │
│  • সেগমেন্ট-ভিত্তিক কাস্টম প্রমোশন           • কার্ট অ্যাবান্ডনমেন্ট অফার   │
│  • গ্রাহকের অ্যাফিনিটি অনুযায়ী টেক্সট পরিবর্তন • ইমেইল সাবস্ক্রিপশন ক্যাপচার   │
└─────────────────────────────────────────────────────────────────────────────┘
```

1. **Content Personalization (ডায়নামিক ব্যানার ও কনটেন্ট):**  
   * স্টোরের ব্যানার ও টেক্সট স্বয়ংক্রিয়ভাবে ভিজিটরের পছন্দের সাথে পরিবর্তিত হয় (যেমন: পুরুষ গ্রাহক ঢুকলে হোমপেজের ব্যানারে মেনস কালেকশন দেখাবে, আর মহিলা গ্রাহক ঢুকলে উইমেন্স কালেকশন দেখাবে)।
2. **Pop-ups Engine (বিহেভিওরাল পপ-আপ):**  
   * গ্রাহক যখন ব্রাউজার ট্যাব বন্ধ করতে যায় (Exit Intent) অথবা কার্ট রেখে চলে যেতে চায়, তখন রিয়েল-টাইমে ডিসকাউন্ট অফার বা ইমেইল ক্যাপচার পপ-আপ প্রদর্শন করা।

---

## ৬. ৭-পেজ রিকমেন্ডেশন ক্যাম্পেইন ম্যাট্রিক্স (The 7-Page Recommendation Matrix)

`my.nosto.com/campaigns/list` পেজ থেকে Nosto-এর পূর্ণাঙ্গ অন-সাইট রিকমেন্ডেশন আর্কিটেকচার উন্মোচিত হয়েছে:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                 Nosto 7-Page Recommendation Hierarchy (18 Slots)            │
│                                                                             │
│  [1. Front Page (Home)]         ──► 4 Active Slots (Trending, Bestsellers)  │
│  [2. Category Page (Collection)]──► 2 Active Slots (Category Top, Clearance)│
│  [3. Product Page (PDP)]        ──► 3 Active Slots (FBT, Cross-Sell, Alt)   │
│  [4. Shopping Cart]             ──► 3 Active Slots (Cart Upsell, Threshold) │
│  [5. Search Results]            ──► 2 Active Slots (Zero-Result Fallback)   │
│  [6. 404 Error Page]            ──► 2 Active Slots (Loss Recovery)          │
│  [7. Shopify Thank You Page]    ──► 1 Active Slot (Post-Checkout Cross-Sell)│
│                                                                             │
│  Total Pre-configured Campaigns: 17/18 Active Slots Across The Storefront   │
└─────────────────────────────────────────────────────────────────────────────┘
```

### ১. ৭টি পেজ টাইপ ও ১৮টি ডিফল্ট প্লেসমেন্ট স্লট
মার্চেন্টকে স্ক্র্যাচ থেকে কোনো উইজেট ডিজাইন করতে হয় না; ইনস্টল হওয়ার সাথে সাথে পুরো স্টোরের ৭টি স্ট্র্যাটেজিক পেজে **১৮টি রিকমেন্ডেশন স্লট** স্বয়ংক্রিয়ভাবে ম্যাপ হয়ে যায়:

| পেজের নাম | স্লট সংখ্যা | মূল উদ্দেশ্য ও অ্যালগরিদম |
| :--- | :---: | :--- |
| **১. Front Page (Home)** | **৪টি** | নতুন ও রিটার্নিং ক্রেতাদের জন্য ট্রেন্ডিং আইটেম, বেস্টসেলার এবং সম্প্রতি দেখা পণ্য। |
| **২. Category Page** | **২টি** | কালেকশনের সেরা মার্জিন পণ্য এবং ক্যাটাগরি-নির্দিষ্ট ডিসকাউন্ট আইটেম। |
| **৩. Product Page (PDP)** | **৩টি** | Frequently Bought Together বান্ডেল, বিকল্প পণ্য (Upsell) এবং পরিপূরক পণ্য (Cross-sell)। |
| **৪. Shopping Cart** | **৩টি** | কার্ট ভ্যালু বুস্টার, ফ্রি শিপিং থ্রেশহোল্ড আপসেল ও ইমপালস বাই। |
| **৫. Search Results** | **২টি** | কোনো কিছু সার্চ করার পর পারসোনালাইজড রেজাল্ট এবং সার্চ ব্যর্থ হলে ফলব্যাক পণ্য। |
| **৬. 404 Error Page** | **২টি** | ব্রোকেন লিংকে আসা হারিয়ে যাওয়া ট্রাফিককে ফিরিয়ে আনতে বেস্টসেলার রিকমেন্ডেশন। |
| **৭. Shopify Thank You Page** | **১টি** | অর্ডার সম্পন্ন হওয়ার পর কাস্টমারকে পরবর্তী ক্রয়ের জন্য এনগেজড রাখা। |

---

### ২. ডিকাপল্ড আর্কিটেকচার (Template vs Algorithm vs Segment)
Nosto-এর ইঞ্জিনিয়ারিংয়ের মূল শক্তি হলো এর ৩-স্তরীয় ডিকাপলিং:
1. **Algorithm / Type:** পণ্য নির্বাচনের নিয়ম (যেমন: *Frequently Bought Together*, *Personalized for You*, *Top Sellers*)।
2. **Template (Visual):** স্টাইলিং ও লেআউট (বাম পাশে `Templates` ও `Template Gallery` দিয়ে সম্পূর্ণ আলাদা কন্ট্রোল)।
3. **Audience Segment:** কোন ক্যাম্পেইনটি কোন ধরনের ক্রেতা দেখবে (যেমন: সব ভিজিটর বনাম কেবল হাই-ভ্যালু ভিআইপি ক্রেতা)।
4. **Performance Tracking:** প্রতি স্লটের জন্য আলাদা **Click-through rate (CTR)**, **Conversion rate (CVR)** এবং সরাসরি অ্যাট্রিবিউটেড **Total Sales ($)** ট্র্যাকিং।

---

## ৭. ৬-ধাপের এন্টারপ্রাইজ রিকমেন্ডেশন উইজার্ড (The 6-Step Creation Engine Deep Dive)

`my.nosto.com/campaigns/add` থেকে Nosto-এর ৬টি ধাপের প্রতিটি সেটিংস পুঙ্খানুপুঙ্খভাবে রিভার্স-ইঞ্জিনিয়ারিং করা হয়েছে:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                 Nosto 6-Step Creation Engine (Complete Flow)                │
│                                                                             │
│  [Step 1: Setup] ──► 11 Page Types + Shopify+ Checkout Trap + Slot Bounds  │
│  [Step 2: Rec Type] ──► 13 AI Algorithms (Personalized, VisualAI, Replenish)│
│  [Step 3: Customization] ──► IF/THEN Filters + 3 Fill Modes + Merchandising│
│  [Step 4: Visual Settings] ──► ✨ GenAI Title + UGC Photo Hover + Templates │
│  [Step 5: Fallbacks] ──► Multi-Tier Fallback: "Fill" vs "Replace" Strategy │
│  [Step 6: Summary & Launch] ──► Decoupled Placement & Segment Binding       │
└─────────────────────────────────────────────────────────────────────────────┘
```

### ধাপ ১: জেনারেল সেটআপ ও ১১টি পেজ টাইপ (Setup)
* **স্লট বাউন্ডস:** প্রতিটি উইজেটের জন্য সর্বনিম্ন (`Min: 1`) এবং সর্বোচ্চ (`Max: 10`) প্রোডাক্ট সীমা নির্ধারণ।
* **১১টি পেজ কাভারেজ:** Front, Category, PDP, Cart, Search, Landing Page, 404, Thank You, General Layout, Other, এবং **Headless API-Only Mode**।
* **শপিফাই প্লাস গেটকিপিং:** চেকআউট পেজের রিকমেন্ডেশন শুধুমাত্র **Shopify Plus** মার্চেন্টদের জন্য সীমাবদ্ধ (`Only available for Shopify+`)।

---

### ধাপ ২: রিকমেন্ডেশন টাইপ ও অ্যালগরিদম (Recommendation Type)
* ১৩টি বিশেষায়িত মেশিন লার্নিং অ্যালগরিদম (Personalized, VisualAI, Replenishment, Geo-targeted, Live Feed ইত্যাদি)।
* **ডি-ডুপ্লিকেশন রুলস:** কার্টে থাকা পণ্য এবং বর্তমানে দেখা পণ্য স্বয়ংক্রিয়ভাবে বাদ দেওয়া।

---

### ধাপ ৩: কাস্টমাইজেশন, ফিল্টারিং ও ফিল মোড (Customization)
বাম পাশের সাব-মেনু: `Filters` | `Fill Mode` | `Merchandising Rules` | `Variant Settings` | `Visual AI Settings`

১. **Filters (কন্ডিশনাল রুলস ইঞ্জিন):**
   * `No filter:` Use algorithm output with no filters or conditions (ডিফল্ট)।
   * `Basic filter:` Add filter to include and exclude products (কালেকশন, ট্যাগ, ভেন্ডর)।
   * `Advanced dynamic filter:` Add advanced conditional filters based on IF and THEN rules (যেমন: *IF কার্ট ভ্যালু > $৫০ THEN দেখাও $২০ এর নিচের এক্সেসরিজ*)।
২. **Fill Mode (স্লট ব্যাকফিলিং স্ট্র্যাটেজি):**
   * `Fill with similar products:` Fill available product positions with cross-sales (ডিফল্ট)।
   * `Fill with bestsellers:` Fill available product positions with bestsellers।
   * `Show only recommended products:` Strictly respect the applied recommendation rules (কোনো ব্যাকফিল করবে না)।
৩. **Merchandising Rules:**
   * ফিল্টারের পর অর্ডারিং ঠিক করা: *"Merchandising rules can affect the order of your product recommendations after they've been filtered."*
   * সরাসরি লিংক: `Edit Merchandising rule ↗` ও `Create rule` বাটন।

---

### ধাপ ৪: ভিজুয়াল সেটিংস, জেন-এআই ও ইউজিসি (Visual Settings)
বাম পাশের সাব-মেনু: `Recommendation title` | `UGC` | `Template Settings`

১. **জেনারেটিভ এআই টাইটেল (`✨ Generate title`):**  
   * Huginn GenAI বোতামে এক ক্লিকেই রিকমেন্ডেশনের হাই-কনভার্টিং টাইটেল (যেমন: *"Trending now"*, *"Frequently Paired With This"*) জেনারেট হয়ে যায়।
২. **ইউজিসি ও সোশ্যাল প্রুফ হোভার (`User-generated photography ⚠️`):**  
   * টগল: *"Turn on the toggle to use UGC instead of product images. Show the latest content that have been approved and published for a given product."*
   * **UGC Alternative (Hover) Image:** মাউস হোভার করলে সাধারণ পণ্যের ছবি ফ্লিপ হয়ে কাস্টমারের আসল সোশ্যাল মিডিয়া ফটো দেখা যায় (`Learn more ↗`)।
৩. **Template Settings:**  
   * ড্রপডাউন সিলেক্টর: `shopify-default`।
   * শর্টকাট লিংক: `Go to template ↗` এবং `Show template visual settings`।

---

### ধাপ ৫: ফলব্যাক ইঞ্জিন ("Fill" বনাম "Replace" স্ট্র্যাটেজি)
বাম পাশের সাব-মেনু: `Fallbacks` | `Fallback Behavior`

১. **Fallbacks রুল কার্ড:**  
   * *"Create a fallback recommendations for when the primary recommendation does not have required number of products to recommend."*  
   * প্রাইমারি সামারি কার্ডের নিচে `+ Add fallback` দিয়ে একাধিক চেইন ফলব্যাক যুক্ত করা যায়।
২. **Fallback Behavior (২টি সুস্পষ্ট আচরণ):**
   * **Option A — Fill with a fallback products:**  
     * *"If the primary recommendation does not have required amount of products, it will be filled with products from fallback recommendations showing the primary recommendation's title."* (একই টাইটেল রেখে বাকি স্লট ব্যাকফিল করে)।
   * **Option B — Replace with a fallback (ডিফল্ট):**  
     * *"If the primary recommendation does not have required amount of products, it will be replaced with the fallback that meets the criteria showing the fallback's title for the recommendation."* (সম্পূর্ণ উইজেটটি ফলব্যাক ক্যাম্পেইনে রূপান্তরিত হয় এবং টাইটেলও স্বয়ংক্রিয়ভাবে বদলে যায়)।

---

### ধাপ ৬: সামারি, ডিকাপল্ড প্লেসমেন্ট ও সেভ (Summary & Save)
বাম পাশের সাব-মেনু: `Summary`

* **অ্যাক্টিভ সামারি গ্রিড:**
  * **Title:** মার্চেন্টের দেওয়া নাম (যেমন: `dsbvd`)
  * **Slot ID:** স্বয়ংক্রিয় ইউনিক স্লট সিলেক্টর (যেমন: `frontpage-nosto-5`)
  * **Status:** `Enabled` (সবুজ ব্যাজ)
  * **Page type:** `Front` (হোমপেজ)
  * **Placements:** `Not set ⚠️` (লাল সতর্কবার্তা)
  * **Segments:** `Not set` (লাল সতর্কবার্তা)
  * **Schedule:** `Off`
  * **Recommendation type:** `Personalized recommendations`
  * **Template:** `shopify-default`
* **ক্যাম্পেইন অ্যাকশন কন্ট্রোল:**
  * `Preview campaign` বাটন দিয়ে লাইভ প্রিভিউ দেখা যায়।
  * নিচের অ্যাকশন বার: `Cancel` | `Save as draft` | `Previous` | `Save` (সবুজ প্রাইমারি বাটন)।
* **ডিকাপল্ড আর্কিটেকচার:** Nosto ক্যাম্পেইন ক্রিয়েশনকে প্লেসমেন্ট ও অডিয়েন্স সেগমেন্ট থেকে সম্পূর্ণ আলাদা (Decoupled) রাখে, ফলে একই রিকমেন্ডেশন লজিক বিভিন্ন পেজে ও বিভিন্ন ইউজারের জন্য পরে রিইউজ করা যায়।

---

## ৮. রিকমেন্ডেশন অ্যালগরিদম ক্যাটালগ (The Recommendation Algorithm Catalog)

`my.nosto.com/campaigns/add` পেজের স্টেপ ২ (`Recommendation type`) থেকে Nosto-এর অত্যাধুনিক মেশিন লার্নিং অ্যালগরিদমের সম্পূর্ণ তালিকা উন্মোচিত হয়েছে:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    Nosto AI Algorithm Taxonomy Grid                         │
│                                                                             │
│  [1. 1-to-1 Behavioral AI]                                                  │
│  ├── Personalized recommendations: ব্রাউজ ও কার্ট হিস্ট্রি ভিত্তিক          │
│  ├── Browsing history: পূর্বে দেখা পণ্যের রিমাইন্ডার                        │
│  └── Browsing history related: সাম্প্রতিক আচরণের সাথে সম্পর্কিত নতুন পণ্য     │
│                                                                             │
│  [2. Computer Vision / Visual AI] (Industry-First)                          │
│  ├── Visually similar to browsing history: ছবির রঙ, প্যাটার্ন ও শেপ ম্যাচিং │
│  └── Visually similar to order history: পূর্বের অর্ডারের মতো দেখতে পণ্য     │
│                                                                             │
│  [3. Contextual & Geo-Intelligence]                                         │
│  ├── Geo-targeted trending products: গ্রাহকের ভৌগোলিক এলাকার ট্রেন্ডিং আইটেম│
│  └── Landing page recommendations: বিজ্ঞাপনের ট্রাফিক সোর্স (UTM) অনুযায়ী    │
│                                                                             │
│  [4. Transactional, Replenishment & Social Proof]                           │
│  ├── Replenish recommendations: কনজিউমেবল পণ্যের রি-অর্ডার প্রেডিকশন এআই   │
│  ├── Live feed: রিয়েল-টাইম স্টোর অ্যাক্টিভিটি ও সোশ্যাল প্রুফ স্ট্রিম       │
│  ├── Cherry-picked recommendations: মার্চেন্টের হ্যান্ড-পিকড ম্যানুয়াল কালেকশন │
│  ├── Best sellers: সামগ্রিক স্টোরের শীর্ষ বিক্রিত পণ্য                      │
│  └── Order related recommendations: অতীত অর্ডারের সাথে সম্পর্কিত ক্রস-সেল    │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ৯. প্রাইসিং ট্র্যাপ ও বিজনেস মডেল বিশ্লেষণ (The Enterprise Barrier)

Nosto-এর রিভিউ সংখ্যা মাত্র **৬১টি** হওয়ার পেছনে রয়েছে তাদের বিতর্কিত প্রাইসিং স্ট্র্যাটেজি:

```
[Shopify App Store: "Free to Install"]
                 │
                 ▼
[Install Click ──► External Redirect to Nosto Sales Rep]
                 │
                 ▼
[Contract Negotiations: $500 to $2,500+/month OR 1.5% to 4% Gross Revenue]
                 │
                 ▼
[SMB Merchants Drop Out ──► Only High-End Shopify Plus Stores Remain]
```

* **"Contact Nosto for details":** তারা অ্যাপ স্টোরে কোনো স্পষ্ট প্রাইসিং দেয় না।
* **বাইরের ইনভয়েসিং (External Billing):** শপিফাইয়ের নিজস্ব বিলিং সিস্টেম এড়িয়ে আলাদা ক্রেডিট কার্ড বা এন্টারপ্রাইজ ইনভয়েস পাঠায়।
* **উচ্চ মূল্যের বাধা (High Barrier to Entry):** সাধারণ মার্চেন্টদের (SMBs) জন্য Nosto সম্পূর্ণ ধরাছোঁয়ার বাইরে। সাধারণত যাদের বার্ষিক সেলস $১ মিলিয়নের বেশি, কেবল তারাই Nosto ব্যবহার করতে পারে।

---

## ১০. চার প্রতিযোগীর সামগ্রিক আর্কিটেকচার তুলনা (Master 4-Competitor Matrix)

| ফিচার | LimeSpot Personalizer | Frequently Bought (CBB) | Nosto CXP | ClearRecs AI (আমাদের ডিজাইন) |
| :--- | :--- | :--- | :--- | :--- |
| **টার্গেট মার্কেট** | মিড-মার্কেট ($১৭-$১,৭০০/মাস) | SMB ফ্রেন্ডলি ($০-$৩৯.৯৯/মাস) | এন্টারপ্রাইজ ($৫০০-$২,৫০০+/মাস) ❌ | **SMB থেকে এন্টারপ্রাইজ ($০-$৪৯/মাস ফেয়ার ক্যাপড)** 💎 |
| **অনবোর্ডিং টাইম** | ১৫-২০ মিনিট (জটিল) ❌ | ৬০ সেকেন্ড (৩ ধাপ) ✅ | সপ্তাহব্যাপী সেলস কল ও সেটআপ ❌ | **৪৫ সেকেন্ড (থিম এম্বেড + ১-ক্লিক ভার্টিক্যাল টেমপ্লেট)** ⚡ |
| **রেকমেন্ডেশন অ্যালগরিদম** | ১৫টি বক্স ও ক্যাসকেডিং | ৪-টিয়ার ওয়াটারফল চেইন | ১৩টি এআই অ্যালগরিদম + VisualAI | **স্মার্ট ওয়াটারফল + VisualAI + Explainable AI** 🔥 |
| **Explainable AI ব্যাজ** | নেই ❌ | নেই ❌ | নেই ❌ | **আছে ("৮৭% ক্রেতা এটি সাথে নিয়েছেন")** 💎 |
| **ইন-উইজেট ভ্যারিয়েন্ট** | নেই ❌ | আছে (ইনলাইন ড্রপডাউন) ✅ | আংশিক টেমপ্লেট ডিপেন্ডেন্ট | **আছে (ইনলাইন কালার সোয়াচ ও ড্রপডাউন)** 💎 |
| **A/B টেস্টিং ইঞ্জিন** | নেই ❌ | নেই ❌ | আছে (স্ট্যাটিস্টিক্যাল ইঞ্জিন) ✅ | **নেটিভ ইন-উইজেট A/B টেস্টিং** 🧪 |
| **Slide Cart Drawer** | নেই ❌ | নেই ❌ | নেই ❌ | **আছে (মাল্টি-টিয়ার ফ্রি শিপিং ও গিফট বারসহ)** 🛒 |
| **Checkout UI Extension** | নেই (শুধু পোস্ট-পারচেজ) | নেই ❌ | শুধুমাত্র Shopify Plus-এর জন্য লকড ❌ | **সকল প্ল্যানের জন্য ১-ক্লিক নেটিভ চেকআউট এক্সটেনশন** 💳 |
| **Post-Purchase Upsell** | আছে (কাস্টম পেজ) | নেই ❌ | আছে (নেটিভ পোস্ট-পারচেজ) | **নেটিভ ১২০ সেকেন্ড কাউন্টডাউন টাইমারযুক্ত ১-ক্লিক আপসেল** ⏳ |
| **হেডলেস ও পাবলিক এপিআই** | এন্টারপ্রাইজ লকড | পাবলিক এপিআই আছে | পাবলিক এপিআই আছে | **আল্ট্রা-ফাস্ট এজ এপিআই (Sub-50ms GraphQL)** ⚡ |

---

## ১১. Nosto-এর মারাত্মক দুর্বলতা ও সীমাবদ্ধতা (Exploitable Weaknesses)

এনামুল ভাইয়ের (Product Lead) স্ট্র্যাটেজি অনুযায়ী Nosto-কে পরাস্ত করার মূল ফাঁকসমূহ:

1. **মারাত্মক সেলস ফ্রিকশন ও কোনো সেলফ-সার্ভ অনবোর্ডিং নেই ❌:**  
   * কোনো মার্চেন্ট অ্যাপটি ইনস্টল করে সরাসরি ড্যাশবোর্ডে গিয়ে কাজ শুরু করতে পারে না; তাদেরকে সেলস টিমের সাথে মিটিং বুক করতে বাধ্য করা হয়।
2. **অতিরিক্ত জটিল ও স্লো অনবোর্ডিং (Complexity Overhead) ❌:**  
   * একটি স্টোরে Nosto সেটআপ ও টিউন করতে কয়েক সপ্তাহ লেগে যায়। সাধারণ মার্চেন্টদের পক্ষে এত জটিল রুলস মেইনটেইন করা অসম্ভব।
3. **চেকআউট পেজ শুধুমাত্র শপিফাই প্লাসে সীমাবদ্ধ ❌:**  
   * তারা সাধারণ শপিফাই স্টোরগুলোতে চেকআউট পেজের রিকমেন্ডেশন সম্পূর্ণ লক করে রেখেছে।
4. **ছোট ও মাঝারি মার্চেন্টদের (SMB) অবহেলা ❌:**  
   * শপিফাইয়ের ৯০% মার্চেন্ট যারা মাসে $০ থেকে $৪৯ খরচ করতে চায়, Nosto তাদের কোনো সেবাই দেয় না।
5. **কোনো নেটিভ স্লাইড কার্ট ড্রয়ার (Slide Cart Drawer) নেই ❌:**  
   * তারা সার্চ ও মার্চেন্ডাইজিংয়ে বড় হলেও শপিফাইয়ের সবচেয়ে হাই-কনভার্টিং টাচপয়েন্ট—**Slide Cart Drawer** অফার করে না।
6. **ব্ল্যাক-বক্স এআই (No Explainable AI on Storefront) ❌:**  
   * স্টোরফ্রন্টে গ্রাহককে কোনো সামাজিক ব্যাখ্যা বা সোশ্যাল প্রুফ ("৮৭% ক্রেতা এটি সাথে নিয়েছেন") দেখানো হয় না।

---

## ১২. ClearRecs AI কীভাবে Nosto-কে টেক্কা দেবে (ClearRecs Strategic Supremacy)

| ফিচার | Nosto CXP | ClearRecs AI (আমাদের সল্যুশন) |
| :--- | :--- | :--- |
| **টার্গেট অডিয়েন্স** | শুধুমাত্র এন্টারপ্রাইজ ও প্লাস স্টোর | **সকল শপিফাই মার্চেন্ট (SMB থেকে এন্টারপ্রাইজ)** 🎯 |
| **অনবোর্ডিং ফ্লো** | সেলস কল, চুক্তি ও সপ্তাহব্যাপী অপেক্ষা ❌ | **৪৫ সেকেন্ডের ১-ক্লিক সেলফ-সার্ভ অনবোর্ডিং** ⚡ |
| **প্রাইসিং স্বচ্ছতা** | লুকানো (মাসে $৫০০-$২,৫০০+) ❌ | **স্বচ্ছ ও ফেয়ার ক্যাপড প্রাইসিং ($০ থেকে $৪৯/মাস)** 💰 |
| **১-টু-১ অ্যাফিনিটি প্রোফাইল** | আছে (রঙ, সাইজ, ক্যাটাগরি অ্যাফিনিটি) | **আছে (ClearRecs Smart Affinity Engine)** 🧠 |
| **Explainable AI ব্যাজ** | জটিল ব্ল্যাক-বক্স ❌ | **স্পষ্ট সামাজিক প্রমাণ ("৮৭% ক্রেতা এটি নিয়েছেন")** 🔥 |
| **ইন-উইজেট A/B টেস্টিং** | জটিল এন্টারপ্রাইজ মডিউল | **১-ক্লিক অটোমেটিক A/B টেস্টিং উইথ উইনার অটো-সিলেকশন** 🧪 |
| **Slide Cart Drawer** | নেই ❌ | **আছে (মাল্টি-টিয়ার ফ্রি শিপিং ও গিফট প্রগ্রেস বারসহ)** 🛒 |
| **Checkout UI Extension** | শুধুমাত্র Shopify Plus-এর জন্য লকড ❌ | **১-ক্লিক নেটিভ চেকআউট ইউআই এক্সটেনশন (সবার জন্য উন্মুক্ত)** 💳 |
| **Post-Purchase Upsell** | আলাদা মডিউল বা সীমিত | **নেটিভ ১২০ সেকেন্ড কাউন্টডাউন টাইমারযুক্ত ১-ক্লিক আপসেল** ⏳ |
| **রিপ্লেনিশমেন্ট প্রেডিকশন** | কনফিগার করা জটিল | **১-ক্লিক ভার্টিক্যাল টেমপ্লেট (বিউটি ও সাপ্লিমেন্টের জন্য রেডি)** 🔄 |

---
*ডকুমেন্টটি সংরক্ষিত:* `competitors/NOSTO.md`

