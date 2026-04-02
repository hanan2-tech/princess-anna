# Princess Anna Store — Website Design Spec
**Date:** 2026-04-02  
**Project:** `C:\Users\hanan\Documents\GitHub\princess-anna`  
**Output:** `index.html` + `README.md` (single-page static site)

---

## 1. Overview

A single-file dropshipping storefront for Anna (age 8) selling jewelry & accessories. Bilingual (Hebrew / English). Deployed to GitHub Pages. No build process, no frameworks — only CDN links for Google Fonts and Lottie.

---

## 2. Tech Stack

| Concern | Solution |
|---|---|
| Structure | Single `index.html` |
| Styling | Vanilla CSS (inlined in `<style>`) |
| Logic | Vanilla JS (inlined in `<script>`) |
| Fonts | Google Fonts CDN (Playfair Display, Lato, Heebo) |
| Animations (CSS) | `@keyframes` for shimmer, float, pulse |
| Animations (Lottie) | `@lottiefiles/lottie-player` via unpkg CDN |
| Form backend | Formspree POST (placeholder ID) |
| Hosting | GitHub Pages (static) |

---

## 3. Design System

```
Colors:
  --pink-deep:  #E91E8C
  --pink-main:  #FF69B4
  --pink-light: #FFB6C1
  --pink-pale:  #FFF0F5
  --white:      #FFFFFF
  --gold:       #FFD700
  --text-dark:  #2D2D2D
  --text-soft:  #888888

Typography:
  Headings (EN): Playfair Display
  Body (EN):     Lato
  All (HE):      Heebo

Radius: 16–24px
Shadows: soft pink-tinted drop shadows
Cards: glassmorphism (backdrop-filter: blur(10px))
```

---

## 4. Language & RTL

- **Default language:** Hebrew (RTL) — set on first visit
- Toggle button top-right: `🇮🇱 עב | 🇬🇧 EN`
- On switch: set `document.documentElement.dir` + `lang`, swap all `[data-en]` / `[data-he]` text nodes
- Preference saved in `localStorage('lang')`

---

## 5. Lottie Animations

Library: `@lottiefiles/lottie-player` loaded from `unpkg.com` CDN.  
Each Lottie slot has a CSS fallback in case the CDN is unavailable.

| ID | Location | Animation type | Fallback |
|---|---|---|---|
| `lottie-hero-sparkle` | Hero background | Floating glitter/sparkle loop | CSS floating ✦ ✧ ★ particles |
| `lottie-crown` | Header logo area | Crown glow / gentle bounce loop | Static SVG crown with CSS glow pulse |
| `lottie-step-1` | How It Works — Step 1 | Shopping bag animation | 🛍️ emoji |
| `lottie-step-2` | How It Works — Step 2 | Pencil / form-writing animation | 📝 emoji |
| `lottie-step-3` | How It Works — Step 3 | Delivery box / truck animation | 📦 emoji |
| `lottie-thankyou` | Thank-you message | Confetti / celebration burst | CSS confetti shapes |

**Animation sources:** Free animations from LottieFiles public CDN  
(`https://lottie.host/{uuid}/{file}.json`). URLs resolved during implementation using WebSearch.

**Implementation pattern:**
```html
<lottie-player
  src="https://lottie.host/..."
  background="transparent"
  speed="1"
  loop
  autoplay
  style="width:120px;height:120px">
</lottie-player>
```

---

## 6. Page Sections

### 6.1 Header (sticky)
- Logo left: SVG crown + "Princess Anna" (Playfair Display, deep pink) + "✦ Jewelry & Accessories ✦" (gold, small)
- Lottie crown animation beside/above SVG crown
- Nav center: Home | Shop | About | Order
- Language toggle right
- Mobile: hamburger menu (CSS checkbox toggle, no JS required)

### 6.2 Hero
- Full-width gradient background (pink-pale → white)
- `lottie-hero-sparkle` as absolute-positioned background layer
- Headline + subtext (bilingual)
- CTA: "Shop Now ✨" → smooth scroll to #shop
- Badge: "🌍 Worldwide Shipping / משלוח לכל הארץ"

### 6.3 Shop — Product Grid
5 product cards in a responsive CSS Grid (1 col mobile → 2 col tablet → 3 col desktop):

| # | EN name | HE name | Price | Badge |
|---|---|---|---|---|
| 1 | Crystal Star Necklace | שרשרת כוכב קריסטל | ₪55 | BESTSELLER (gold) |
| 2 | Pink Butterfly Bracelet | צמיד פרפר ורוד | ₪45 | NEW (green) |
| 3 | Sparkle Hair Bow | קשת שיער מנצנצת | ₪38 | — |
| 4 | Clip-On Star Earrings | עגילי כוכב קליפס | ₪42 | NO PIERCING (purple) |
| 5 | Mini Glitter Handbag | תיק מיני גליטר | ₪89 | LIMITED (rose) |

Card anatomy: emoji (80px) on gradient bg → badge → name → description → price → "Order Now" button → heart icon (top-right, visual only).  
Hover: translateY(-6px) + shadow + CSS sparkle burst.

### 6.4 How It Works
3 steps, each with a Lottie icon above the text. Horizontal on desktop, vertical on mobile.

### 6.5 Order Form
- Fields: Full Name, Phone, Email, City, Address, Product (dropdown), Quantity (1–10), Notes, Referral source
- Payment info box (Bit / Paybox, styled info card, not a form field)
- Action: `https://formspree.io/f/REPLACE_WITH_YOUR_FORMSPREE_ID`
- On submit: JS `preventDefault()`, fetch POST to Formspree, hide form, show thank-you card with `lottie-thankyou`
- Thank-you text bilingual, animated pink card

### 6.6 About
Centered card, soft pink bg, large 👑, bilingual text about Anna.

### 6.7 Footer
- Small logo, copyright, social icon placeholders (Instagram, TikTok)
- Info line: shipping / payment / delivery days
- Privacy policy line

---

## 7. Floating Elements

- **WhatsApp button** — fixed bottom-right, green circle, pulse animation, tooltip bilingual, links to `https://wa.me/REPLACE_WITH_PHONE_NUMBER`

---

## 8. Admin / Operational Features

Comment block at top of HTML: ADMIN GUIDE in EN + HE explaining how to:
- Add products
- Change prices
- Set WhatsApp number
- Connect Formspree
- Open/close store (`STORE_OPEN = true/false`)
- Add Instagram/TikTok links

JS variable `const STORE_OPEN = true` — if false, show store-closed banner.

---

## 9. SEO & Meta

```html
<title>Princess Anna | פרינסס אנה — תכשיטים ואקססוריז</title>
<meta name="description" ...>
<meta name="keywords" ...>
<meta property="og:title" content="Princess Anna Store 👑">
<meta name="theme-color" content="#FF69B4">
<!-- ANALYTICS: Replace GA_MEASUREMENT_ID -->
```

---

## 10. Output Files

| File | Purpose |
|---|---|
| `index.html` | Complete site (all CSS + JS inlined) |
| `README.md` | Deployment guide in Hebrew + English |

---

## 11. Placeholders to Replace Before Go-Live

1. `REPLACE_WITH_YOUR_FORMSPREE_ID` — Formspree form ID
2. `REPLACE_WITH_PHONE_NUMBER` — WhatsApp number (format: `972XXXXXXXXX`)
3. `REPLACE_INSTAGRAM` — Instagram profile URL
4. `REPLACE_TIKTOK` — TikTok profile URL
5. `GA_MEASUREMENT_ID` — Google Analytics ID (optional)
