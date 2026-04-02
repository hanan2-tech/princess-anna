# Princess Anna Store — Dropshipping Strategy Design
**Date:** 2026-04-02
**Status:** Approved by user

---

## 1. Business Context

Anna (age 8) sells girls jewelry & accessories at **hanan2-tech.github.io/princess-anna**.
The goal is a fully automated dropshipping operation:
- Customer orders on the site
- Anna gets notified, collects payment via Bit/Paybox
- Supplier ships directly to customer — no inventory held

**Target market:** Israel-first (Hebrew, ₪), worldwide secondary
**Budget:** Free tools only
**Payment:** Bit / Paybox (manual, after order confirmation)
**Products:** 20–50 curated girls jewelry/accessories items

---

## 2. Supplier Selection

### Primary: CJdropshipping (FREE)
- Free account, no monthly fee
- Ships to Israel in 7–15 business days
- Full public REST API (product search, order creation, tracking)
- 1M+ product catalog including girls jewelry
- Direct integration without Shopify required
- API docs: https://developers.cjdropshipping.com/

### Backup: HyperSKU (FREE)
- Free account
- Ships to Israel
- REST API available
- Jewelry-focused catalog
- Use if CJdropshipping doesn't have a specific item

### Manual fallback: AliExpress
- No API, but can be ordered manually for one-off items
- Photos can be imported manually

### NOT using (reasons):
- Zendrop: Shopify-only integration
- Spocket: Paid plans only, Shopify-focused
- AutoDS: Paid ($7.90/month minimum)
- Zendrop: Shopify-only

---

## 3. Architecture Overview

```
┌─────────────────────────────────────────────────────────┐
│  FRONTEND (GitHub Pages — free static hosting)          │
│  index.html + products.json                             │
│  - Loads products dynamically from products.json         │
│  - Customer browses, selects, fills order form          │
│  - Submits to Vercel API endpoint                       │
└────────────────────┬────────────────────────────────────┘
                     │ POST /api/order
┌────────────────────▼────────────────────────────────────┐
│  BACKEND (Vercel Serverless — free tier)                │
│  Node.js API routes                                     │
│  /api/order        — receive & validate order           │
│  /api/products     — proxy CJdropshipping product search│
│  /api/track        — get order tracking status          │
│  /api/admin        — password-protected admin view      │
└──────┬─────────────────────────┬───────────────────────┘
       │                         │
┌──────▼──────┐         ┌────────▼──────────────┐
│  Supabase   │         │  CJdropshipping API   │
│  (free DB)  │         │  (free, no Shopify)   │
│  - orders   │         │  - product catalog    │
│  - products │         │  - order placement    │
│  - tracking │         │  - tracking updates   │
└─────────────┘         └───────────────────────┘
       │
┌──────▼──────────────────────────────────────────────────┐
│  NOTIFICATIONS                                          │
│  - Email to Anna: Gmail via Nodemailer (free)           │
│  - WhatsApp to customer: wa.me link (manual)            │
│  - Future: WhatsApp Business API (free tier)            │
└─────────────────────────────────────────────────────────┘
```

---

## 4. Phase Plan

### Phase 1 — Real Product Catalog (Week 1)
**Goal:** Replace emoji placeholders with real product photos and data from CJdropshipping.

**Deliverables:**
1. `products.json` — 20–30 curated girls jewelry/accessories products with:
   - Real CJdropshipping product IDs
   - Real product photos (CDN URLs from CJdropshipping)
   - Accurate descriptions (EN + HE)
   - Prices in ₪ (with ~3x markup from USD cost)
   - Product categories: necklaces, bracelets, earrings, hair accessories, bags, sets

2. Updated `index.html`:
   - Products loaded dynamically from `products.json` via `fetch()`
   - Image `<img>` tags replacing emoji placeholders
   - Product cards show real photos with fallback emoji if image fails
   - Product dropdown in order form auto-populated from JSON
   - Category filter buttons: All / נקלסים / צמידים / עגילים / שיער / תיקים

3. CJdropshipping account registered at cjdropshipping.com

**Tools needed:** CJdropshipping free account (browse + copy product data)

---

### Phase 2 — Vercel Backend (Week 2)
**Goal:** Replace Formspree with a proper backend. Orders saved to DB, Anna notified by email.

**New files:**
```
princess-anna/
├── index.html              (updated — form POSTs to /api/order)
├── products.json           (from Phase 1)
├── api/
│   ├── order.js            (POST — save order, email Anna)
│   ├── products.js         (GET — search/filter products from CJ API)
│   └── track.js            (GET — order tracking status)
├── admin/
│   └── index.html          (password-protected order management)
├── vercel.json             (routing config)
└── package.json
```

**Order flow:**
1. Customer submits form → `POST /api/order`
2. Vercel saves order to Supabase (status: `pending_payment`)
3. Nodemailer sends email to Anna with order details + customer info
4. Customer sees: "Anna will contact you on WhatsApp within 24h for Bit/Paybox payment"
5. Anna reviews order → sends Bit/Paybox link to customer
6. Anna marks order as `paid` in admin panel
7. Admin panel shows "Place on CJdropshipping" button → links to pre-filled CJ order

**Services (all free):**
- Vercel: free hobby plan (unlimited serverless functions)
- Supabase: free tier (500MB DB, 2GB bandwidth)
- Nodemailer + Gmail: free (uses Gmail SMTP)

---

### Phase 3 — Full Automation (Week 3-4)
**Goal:** Auto-forward paid orders to CJdropshipping API, auto-track, WhatsApp updates.

**New capabilities:**
1. **Auto-order on CJdropshipping** — when Anna marks order as `paid` in admin:
   - Backend calls CJdropshipping `POST /api/shopping/order/createOrderV2`
   - CJ order ID saved to Supabase
   - Status updates to `fulfilling`

2. **Tracking webhook** — CJdropshipping sends tracking updates to `/api/track`
   - Supabase updated with tracking number + carrier
   - Anna sees live status in admin panel

3. **WhatsApp notification** — when tracking number available:
   - wa.me link auto-generated for Anna to send customer
   - Future: WhatsApp Business API for auto-send

4. **Product sync** — nightly Vercel cron:
   - Check CJdropshipping stock levels
   - Hide out-of-stock products from site
   - Update prices if CJ prices change

---

## 5. Product Categories (Phase 1 targets)

| Category | Hebrew | Target count | CJdropshipping search term |
|---|---|---|---|
| Necklaces | שרשראות | 5-6 | "girls crystal necklace pendant" |
| Bracelets | צמידים | 5-6 | "girls butterfly bracelet charm" |
| Earrings (clip-on) | עגילים | 4-5 | "girls clip on earrings no piercing" |
| Hair accessories | אביזרי שיער | 5-6 | "girls hair bow glitter ribbon" |
| Bags | תיקים | 3-4 | "girls mini handbag glitter sequin" |
| Jewelry sets | סטים | 3-4 | "girls jewelry set princess gift" |

---

## 6. Pricing Strategy

CJdropshipping products cost ~$2–8 USD (including shipping to Israel).
Markup formula: **Cost × 3.5 = selling price in ₪**

Example:
- CJ product cost: $3 USD + $4 shipping = $7 total
- $7 × 3.7 = $25.9 USD = ~₪96
- Round to ₪89 or ₪99

Competitive range for this market: ₪35–₪120 per item.

---

## 7. Technical Stack (all free)

| Service | Purpose | Free tier |
|---|---|---|
| GitHub Pages | Frontend hosting | Free |
| Vercel | Backend (serverless) | Free hobby plan |
| Supabase | Database | 500MB free |
| CJdropshipping | Supplier + API | Free (pay per order) |
| Gmail SMTP | Email notifications | Free |
| Formspree | Fallback form (current) | Free 50/month |
| WhatsApp | Customer communication | Free |

---

## 8. Environment Variables (Vercel)

```
CJ_EMAIL=hanantal212@gmail.com
CJ_PASSWORD=<cj password>
CJ_ACCESS_TOKEN=<auto-refreshed by backend>
SUPABASE_URL=https://xxx.supabase.co
SUPABASE_KEY=<anon key>
GMAIL_USER=hanantal212@gmail.com
GMAIL_PASS=<gmail app password>
ADMIN_PASSWORD=<anna admin password>
```

---

## 9. Open Questions Resolved

| Question | Answer |
|---|---|
| Shopify needed? | No — Vercel + CJdropshipping API directly |
| Payment processor? | No — manual Bit/Paybox |
| Inventory storage? | No — pure dropshipping |
| Backend language? | Node.js (Vercel native) |
| Database? | Supabase (PostgreSQL, free tier) |
| Hosting? | GitHub Pages (frontend) + Vercel (backend) |
