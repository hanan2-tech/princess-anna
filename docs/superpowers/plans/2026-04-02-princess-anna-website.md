# Princess Anna Store — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a complete bilingual (Hebrew default/English toggle) single-file dropshipping website for Princess Anna jewelry & accessories store with Lottie animations.

**Architecture:** Single `index.html` with all CSS and JS inlined. Lottie animations via `@lottiefiles/lottie-player` CDN. Formspree for order submissions. Bilingual text via `data-en`/`data-he` attributes swapped by JS.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, keyframes), Vanilla JS, Google Fonts CDN (Playfair Display + Lato + Heebo), `@lottiefiles/lottie-player@2.0.4` CDN, Formspree POST

**Reference spec:** `docs/superpowers/specs/2026-04-02-princess-anna-website-design.md`

---

## File Map

| File | Action | Responsibility |
|---|---|---|
| `index.html` | Create | Complete site: HTML + CSS + JS |
| `README.md` | Create | Deployment guide (EN + HE) |

---

## Task 1: Scaffold — `index.html` head, CSS variables, reset

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create `index.html` with this exact content**

```html
<!--
  ╔══════════════════════════════════════════════════════╗
  ║          PRINCESS ANNA — ADMIN GUIDE                ║
  ║               (עברית / English)                      ║
  ╚══════════════════════════════════════════════════════╝

  TO ADD A NEW PRODUCT / להוסיף מוצר חדש:
  Search for: <!-- PRODUCT CARD -->
  Copy one card block and change emoji, name_en/he, price, description_en/he, badge

  TO CHANGE PRICE / לשנות מחיר:
  Search for the product name, change the ₪ number inside class="product-price"

  TO ADD WHATSAPP NUMBER / להוסיף מספר וואטסאפ:
  Search for: REPLACE_WITH_PHONE_NUMBER
  Replace with: 972XXXXXXXXX (without + or spaces)

  TO CONNECT FORMSPREE / לחבר טופס:
  Search for: REPLACE_WITH_YOUR_FORMSPREE_ID
  Replace with your Formspree form ID

  TO CLOSE STORE TEMPORARILY / לסגור חנות זמנית:
  Search for: STORE_OPEN = true
  Change to: STORE_OPEN = false

  TO ADD INSTAGRAM/TIKTOK LINKS:
  Search for: REPLACE_INSTAGRAM / REPLACE_TIKTOK
  Replace with your profile URLs
-->
<!DOCTYPE html>
<html lang="he" dir="rtl" id="html-root">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Princess Anna | פרינסס אנה — תכשיטים ואקססוריז</title>
  <meta name="description" content="Princess Anna's magical jewelry and accessories store. Unique sparkly pieces delivered to your door. / חנות התכשיטים והאקססוריז של פרינסס אנה">
  <meta name="keywords" content="princess anna, תכשיטים, אקססוריז, תכשיטי ילדות, dropshipping jewelry">
  <meta property="og:title" content="Princess Anna Store 👑">
  <meta property="og:description" content="Magical jewelry & accessories ✨">
  <meta name="theme-color" content="#FF69B4">
  <!-- ANALYTICS: Replace GA_MEASUREMENT_ID with your Google Analytics ID -->
  <!-- <script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
  <script>window.dataLayer=window.dataLayer||[];function gtag(){dataLayer.push(arguments);}gtag('js',new Date());gtag('config','GA_MEASUREMENT_ID');</script> -->
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400&family=Lato:wght@300;400;700&family=Heebo:wght@300;400;600;700&display=swap" rel="stylesheet">
  <!-- Lottie Player -->
  <script src="https://unpkg.com/@lottiefiles/lottie-player@2.0.4/dist/lottie-player.js"></script>
  <style>
    /* ============================================================
       CSS CUSTOM PROPERTIES
    ============================================================ */
    :root {
      --pink-deep: #E91E8C;
      --pink-main: #FF69B4;
      --pink-light: #FFB6C1;
      --pink-pale: #FFF0F5;
      --white: #FFFFFF;
      --gold: #FFD700;
      --text-dark: #2D2D2D;
      --text-soft: #888888;
      --shadow-pink: 0 4px 24px rgba(233,30,140,0.15);
      --shadow-soft: 0 2px 16px rgba(0,0,0,0.08);
      --shadow-card: 0 8px 32px rgba(233,30,140,0.12);
      --radius-sm: 12px;
      --radius-md: 16px;
      --radius-lg: 24px;
      --transition: 0.3s ease;
      --header-h: 70px;
    }

    /* ============================================================
       RESET & BASE
    ============================================================ */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      font-family: 'Heebo', sans-serif;
      color: var(--text-dark);
      background: var(--white);
      line-height: 1.6;
      overflow-x: hidden;
    }
    [lang="en"] body { font-family: 'Lato', sans-serif; }
    [lang="en"] h1,
    [lang="en"] h2,
    [lang="en"] h3,
    [lang="en"] .serif { font-family: 'Playfair Display', serif; }
    a { text-decoration: none; color: inherit; }
    img { max-width: 100%; display: block; }
    button { cursor: pointer; border: none; background: none; font: inherit; }
    ul { list-style: none; }
  </style>
</head>
<body>
  <!-- content added in subsequent tasks -->
</body>
</html>
```

- [ ] **Step 2: Open `index.html` in browser — verify blank white page loads with no errors in console**

- [ ] **Step 3: Commit**
```bash
cd "C:\Users\hanan\Documents\GitHub\princess-anna"
git init
git add index.html
git commit -m "feat: scaffold index.html with head, CSS variables, reset"
```

---

## Task 2: CSS — layout utilities, header, hero

**Files:**
- Modify: `index.html` — append inside the `<style>` block (before `</style>`)

- [ ] **Step 1: Append the following CSS inside `<style>`, after the reset block**

```css
    /* ============================================================
       LAYOUT UTILITIES
    ============================================================ */
    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 20px;
    }
    section { padding: 80px 0; }
    .section-title {
      font-size: clamp(1.8rem, 4vw, 2.6rem);
      font-weight: 700;
      text-align: center;
      margin-bottom: 12px;
      color: var(--text-dark);
    }
    [lang="en"] .section-title { font-family: 'Playfair Display', serif; }
    .section-subtitle {
      text-align: center;
      color: var(--text-soft);
      margin-bottom: 48px;
      font-size: 1rem;
    }
    .gold-line {
      width: 60px;
      height: 3px;
      background: linear-gradient(90deg, var(--gold), var(--pink-main));
      margin: 12px auto 40px;
      border-radius: 2px;
    }

    /* ============================================================
       STORE CLOSED BANNER
    ============================================================ */
    #store-closed-banner {
      background: linear-gradient(135deg, var(--pink-deep), #c2185b);
      color: var(--white);
      text-align: center;
      padding: 14px 20px;
      font-size: 1.1rem;
      font-weight: 600;
      position: sticky;
      top: 0;
      z-index: 9999;
    }

    /* ============================================================
       STICKY HEADER
    ============================================================ */
    header {
      position: sticky;
      top: 0;
      z-index: 1000;
      background: rgba(255,255,255,0.92);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border-bottom: 1px solid rgba(255,105,180,0.15);
      height: var(--header-h);
      display: flex;
      align-items: center;
    }
    .header-inner {
      display: flex;
      align-items: center;
      justify-content: space-between;
      width: 100%;
    }
    /* Logo */
    .logo-wrap {
      display: flex;
      align-items: center;
      gap: 10px;
      flex-shrink: 0;
    }
    .logo-text-wrap { display: flex; flex-direction: column; line-height: 1.2; }
    .logo-name {
      font-family: 'Playfair Display', serif;
      font-size: 1.3rem;
      font-weight: 700;
      color: var(--pink-deep);
      letter-spacing: 0.5px;
    }
    .logo-tagline {
      font-size: 0.62rem;
      color: var(--gold);
      letter-spacing: 1.5px;
      text-transform: uppercase;
    }
    /* Nav */
    .nav-menu {
      display: flex;
      gap: 32px;
      align-items: center;
    }
    .nav-menu a {
      font-size: 0.9rem;
      font-weight: 600;
      color: var(--text-dark);
      transition: color var(--transition);
      position: relative;
    }
    .nav-menu a::after {
      content: '';
      position: absolute;
      bottom: -3px;
      inset-inline-start: 0;
      width: 0;
      height: 2px;
      background: var(--pink-deep);
      transition: width var(--transition);
    }
    .nav-menu a:hover { color: var(--pink-deep); }
    .nav-menu a:hover::after { width: 100%; }
    /* Language toggle */
    .lang-toggle {
      display: flex;
      align-items: center;
      gap: 4px;
      background: var(--pink-pale);
      border-radius: 20px;
      padding: 4px 6px;
      flex-shrink: 0;
    }
    .lang-btn {
      padding: 4px 10px;
      border-radius: 16px;
      font-size: 0.78rem;
      font-weight: 700;
      transition: all var(--transition);
      color: var(--text-soft);
    }
    .lang-btn.active {
      background: var(--pink-deep);
      color: var(--white);
    }
    /* Hamburger (mobile) */
    .hamburger { display: none; flex-direction: column; gap: 5px; cursor: pointer; padding: 4px; }
    .hamburger span { display: block; width: 24px; height: 2px; background: var(--text-dark); border-radius: 2px; transition: all var(--transition); }
    #menu-toggle { display: none; }

    /* ============================================================
       HERO
    ============================================================ */
    #home {
      position: relative;
      min-height: calc(100vh - var(--header-h));
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      background: linear-gradient(160deg, var(--pink-pale) 0%, #fff5fb 50%, var(--white) 100%);
      overflow: hidden;
      padding: 80px 20px;
    }
    .hero-lottie-bg {
      position: absolute;
      inset: 0;
      pointer-events: none;
      opacity: 0.55;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    /* CSS sparkle fallback (shown when Lottie not loaded) */
    .sparkle-particle {
      position: absolute;
      color: var(--gold);
      font-size: 1.2rem;
      opacity: 0;
      animation: floatUp var(--dur, 4s) var(--delay, 0s) ease-in-out infinite;
    }
    .hero-content { position: relative; z-index: 1; max-width: 700px; }
    .hero-badge {
      display: inline-block;
      background: linear-gradient(135deg, var(--pink-light), var(--pink-pale));
      border: 1px solid var(--pink-light);
      border-radius: 20px;
      padding: 6px 18px;
      font-size: 0.82rem;
      font-weight: 600;
      color: var(--pink-deep);
      margin-bottom: 20px;
    }
    .hero-title {
      font-family: 'Playfair Display', serif;
      font-size: clamp(2rem, 6vw, 3.6rem);
      font-weight: 700;
      line-height: 1.2;
      color: var(--text-dark);
      margin-bottom: 16px;
    }
    [lang="en"] .hero-title { font-family: 'Playfair Display', serif; }
    [lang="he"] .hero-title { font-family: 'Heebo', sans-serif; font-weight: 700; }
    .hero-sub {
      font-size: 1.1rem;
      color: var(--text-soft);
      margin-bottom: 36px;
      max-width: 500px;
      margin-inline: auto;
    }
    .btn-primary {
      display: inline-block;
      background: linear-gradient(135deg, var(--pink-deep), var(--pink-main));
      color: var(--white);
      padding: 16px 44px;
      border-radius: 50px;
      font-size: 1.05rem;
      font-weight: 700;
      box-shadow: var(--shadow-pink);
      transition: transform var(--transition), box-shadow var(--transition);
      position: relative;
      overflow: hidden;
    }
    .btn-primary::after {
      content: '';
      position: absolute;
      top: 0; inset-inline-start: -100%;
      width: 100%; height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,0.25), transparent);
      animation: shimmer 2.5s infinite;
    }
    .btn-primary:hover { transform: translateY(-3px); box-shadow: 0 8px 32px rgba(233,30,140,0.35); }
    .hero-shipping {
      margin-top: 20px;
      font-size: 0.85rem;
      color: var(--text-soft);
    }
```

- [ ] **Step 2: Verify `index.html` is still valid HTML (no syntax errors) by opening in browser**

- [ ] **Step 3: Commit**
```bash
git add index.html
git commit -m "feat: add layout utilities, header, hero CSS"
```

---

## Task 3: CSS — shop cards, how-it-works, form, about, footer, WhatsApp

**Files:**
- Modify: `index.html` — append inside `<style>`, after hero CSS

- [ ] **Step 1: Append the following CSS**

```css
    /* ============================================================
       SHOP SECTION
    ============================================================ */
    #shop { background: var(--white); }
    .products-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 28px;
    }
    /* PRODUCT CARD */
    .product-card {
      background: rgba(255,255,255,0.85);
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
      border-radius: var(--radius-lg);
      box-shadow: var(--shadow-card);
      border: 1px solid rgba(255,182,193,0.3);
      overflow: hidden;
      transition: transform var(--transition), box-shadow var(--transition);
      position: relative;
    }
    .product-card:hover {
      transform: translateY(-8px);
      box-shadow: 0 16px 48px rgba(233,30,140,0.22);
    }
    .card-image-area {
      background: linear-gradient(135deg, var(--pink-pale), #ffe4f0);
      height: 180px;
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
    }
    .product-emoji { font-size: 80px; line-height: 1; user-select: none; }
    .card-badge {
      position: absolute;
      top: 12px;
      inset-inline-start: 12px;
      padding: 4px 12px;
      border-radius: 20px;
      font-size: 0.7rem;
      font-weight: 700;
      letter-spacing: 0.5px;
      text-transform: uppercase;
    }
    .badge-gold { background: var(--gold); color: #333; }
    .badge-green { background: #4caf50; color: var(--white); }
    .badge-purple { background: #9c27b0; color: var(--white); }
    .badge-rose { background: #e91e63; color: var(--white); }
    .heart-btn {
      position: absolute;
      top: 12px;
      inset-inline-end: 12px;
      font-size: 1.4rem;
      color: var(--pink-light);
      transition: color var(--transition), transform var(--transition);
      padding: 4px;
      line-height: 1;
    }
    .heart-btn:hover { color: var(--pink-deep); transform: scale(1.2); }
    .card-body { padding: 20px; }
    .product-name {
      font-size: 1.05rem;
      font-weight: 700;
      margin-bottom: 6px;
      color: var(--text-dark);
    }
    [lang="en"] .product-name { font-family: 'Playfair Display', serif; font-size: 1rem; }
    .product-desc {
      font-size: 0.85rem;
      color: var(--text-soft);
      margin-bottom: 16px;
      line-height: 1.5;
    }
    .product-footer {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
    }
    .product-price {
      font-size: 1.4rem;
      font-weight: 700;
      color: var(--pink-deep);
    }
    .btn-order {
      display: inline-block;
      background: linear-gradient(135deg, var(--pink-deep), var(--pink-main));
      color: var(--white);
      padding: 10px 20px;
      border-radius: 50px;
      font-size: 0.88rem;
      font-weight: 700;
      transition: transform var(--transition), box-shadow var(--transition);
      white-space: nowrap;
    }
    .btn-order:hover { transform: translateY(-2px); box-shadow: var(--shadow-pink); }

    /* ============================================================
       HOW IT WORKS
    ============================================================ */
    #how-it-works {
      background: linear-gradient(160deg, #fff5fb, var(--pink-pale));
    }
    .steps-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 36px;
      text-align: center;
    }
    .step-card {
      padding: 36px 24px;
      background: rgba(255,255,255,0.75);
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
      border-radius: var(--radius-lg);
      box-shadow: var(--shadow-soft);
      border: 1px solid rgba(255,182,193,0.25);
      position: relative;
    }
    .step-number {
      position: absolute;
      top: -14px;
      inset-inline-start: 50%;
      transform: translateX(-50%);
      width: 28px;
      height: 28px;
      background: linear-gradient(135deg, var(--pink-deep), var(--pink-main));
      color: var(--white);
      border-radius: 50%;
      font-size: 0.8rem;
      font-weight: 700;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    [dir="rtl"] .step-number { transform: translateX(50%); }
    .step-icon {
      width: 100px;
      height: 100px;
      margin: 0 auto 16px;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .step-icon-fallback { font-size: 56px; }
    .step-title {
      font-size: 1rem;
      font-weight: 700;
      margin-bottom: 8px;
      color: var(--text-dark);
    }
    .step-desc { font-size: 0.88rem; color: var(--text-soft); }

    /* ============================================================
       ORDER FORM
    ============================================================ */
    #order {
      background: var(--white);
    }
    .form-wrapper {
      max-width: 640px;
      margin: 0 auto;
      background: rgba(255,255,255,0.9);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border-radius: var(--radius-lg);
      padding: 48px 40px;
      box-shadow: var(--shadow-card);
      border: 1px solid rgba(255,182,193,0.3);
    }
    .form-row { margin-bottom: 20px; }
    .form-row label {
      display: block;
      font-size: 0.88rem;
      font-weight: 600;
      color: var(--text-dark);
      margin-bottom: 7px;
    }
    .form-row input,
    .form-row select,
    .form-row textarea {
      width: 100%;
      padding: 12px 16px;
      border: 1.5px solid var(--pink-light);
      border-radius: var(--radius-sm);
      font-size: 0.95rem;
      font-family: inherit;
      color: var(--text-dark);
      background: var(--white);
      transition: border-color var(--transition), box-shadow var(--transition);
      outline: none;
    }
    .form-row input:focus,
    .form-row select:focus,
    .form-row textarea:focus {
      border-color: var(--pink-deep);
      box-shadow: 0 0 0 3px rgba(233,30,140,0.1);
    }
    .form-row textarea { resize: vertical; min-height: 90px; }
    .payment-box {
      background: linear-gradient(135deg, var(--pink-pale), #ffe4f2);
      border: 1px solid var(--pink-light);
      border-radius: var(--radius-md);
      padding: 16px 20px;
      margin-bottom: 24px;
      font-size: 0.9rem;
      color: var(--pink-deep);
      font-weight: 600;
    }
    .btn-submit {
      width: 100%;
      padding: 16px;
      background: linear-gradient(135deg, var(--pink-deep), var(--pink-main));
      color: var(--white);
      border-radius: 50px;
      font-size: 1.05rem;
      font-weight: 700;
      box-shadow: var(--shadow-pink);
      transition: transform var(--transition), box-shadow var(--transition);
      position: relative;
      overflow: hidden;
    }
    .btn-submit::after {
      content: '';
      position: absolute;
      top: 0; inset-inline-start: -100%;
      width: 100%; height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,0.25), transparent);
      animation: shimmer 2s infinite;
    }
    .btn-submit:hover { transform: translateY(-2px); box-shadow: 0 8px 32px rgba(233,30,140,0.35); }
    /* Thank you message */
    #thank-you {
      display: none;
      text-align: center;
      padding: 40px 24px;
      background: linear-gradient(135deg, var(--pink-pale), #ffe4f2);
      border-radius: var(--radius-lg);
      border: 1px solid var(--pink-light);
      animation: fadeIn 0.5s ease;
    }
    #thank-you.show { display: block; }
    .thankyou-text {
      font-size: 1rem;
      color: var(--text-dark);
      line-height: 1.7;
      margin-top: 16px;
    }

    /* ============================================================
       ABOUT
    ============================================================ */
    #about {
      background: linear-gradient(160deg, var(--pink-pale), #fff5fb);
    }
    .about-card {
      max-width: 700px;
      margin: 0 auto;
      text-align: center;
      background: rgba(255,255,255,0.8);
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
      border-radius: var(--radius-lg);
      padding: 48px 40px;
      box-shadow: var(--shadow-card);
      border: 1px solid rgba(255,182,193,0.25);
    }
    .about-crown { font-size: 56px; margin-bottom: 20px; }
    .about-text {
      font-size: 1rem;
      color: var(--text-dark);
      line-height: 1.8;
    }

    /* ============================================================
       FOOTER
    ============================================================ */
    footer {
      background: linear-gradient(135deg, #1a0010, #2d0020);
      color: rgba(255,255,255,0.8);
      padding: 48px 0 28px;
      text-align: center;
    }
    .footer-logo-name {
      font-family: 'Playfair Display', serif;
      font-size: 1.2rem;
      color: var(--pink-main);
      margin-bottom: 4px;
    }
    .footer-tagline { font-size: 0.7rem; color: var(--gold); letter-spacing: 1.5px; margin-bottom: 24px; }
    .social-links { display: flex; justify-content: center; gap: 16px; margin-bottom: 20px; }
    .social-btn {
      width: 42px; height: 42px;
      background: rgba(255,255,255,0.1);
      border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      font-size: 1.1rem;
      transition: background var(--transition), transform var(--transition);
    }
    .social-btn:hover { background: var(--pink-deep); transform: translateY(-3px); }
    .footer-info {
      font-size: 0.82rem;
      color: rgba(255,255,255,0.6);
      margin-bottom: 8px;
    }
    .footer-policy { font-size: 0.75rem; color: rgba(255,255,255,0.4); margin-bottom: 20px; }
    .footer-copy { font-size: 0.75rem; color: rgba(255,255,255,0.35); }

    /* ============================================================
       WHATSAPP FLOATING BUTTON
    ============================================================ */
    #whatsapp-btn {
      position: fixed;
      bottom: 28px;
      inset-inline-end: 28px;
      width: 58px; height: 58px;
      background: #25d366;
      border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      box-shadow: 0 4px 20px rgba(37,211,102,0.45);
      z-index: 999;
      transition: transform var(--transition);
      animation: waPulse 2.5s ease-in-out infinite;
    }
    #whatsapp-btn:hover { transform: scale(1.1); animation: none; }
    #whatsapp-btn svg { width: 30px; height: 30px; fill: var(--white); }
    .wa-tooltip {
      position: absolute;
      inset-inline-end: 68px;
      bottom: 50%;
      transform: translateY(50%);
      background: var(--text-dark);
      color: var(--white);
      font-size: 0.78rem;
      font-weight: 600;
      padding: 6px 12px;
      border-radius: var(--radius-sm);
      white-space: nowrap;
      opacity: 0;
      pointer-events: none;
      transition: opacity var(--transition);
    }
    .wa-tooltip::after {
      content: '';
      position: absolute;
      inset-inline-start: 100%;
      top: 50%;
      transform: translateY(-50%);
      border: 5px solid transparent;
      border-inline-start-color: var(--text-dark);
    }
    #whatsapp-btn:hover .wa-tooltip { opacity: 1; }
```

- [ ] **Step 2: Verify in browser — still no errors**

- [ ] **Step 3: Commit**
```bash
git add index.html
git commit -m "feat: add shop, how-it-works, form, about, footer, WhatsApp CSS"
```

---

## Task 4: CSS — @keyframes animations + mobile responsive

**Files:**
- Modify: `index.html` — append inside `<style>`, before `</style>`

- [ ] **Step 1: Append animations and responsive CSS**

```css
    /* ============================================================
       ANIMATIONS (@keyframes)
    ============================================================ */
    @keyframes shimmer {
      0% { inset-inline-start: -100%; }
      100% { inset-inline-start: 100%; }
    }
    @keyframes floatUp {
      0%   { opacity: 0; transform: translateY(0) scale(0.8); }
      20%  { opacity: 0.8; }
      80%  { opacity: 0.6; }
      100% { opacity: 0; transform: translateY(-120px) scale(1.1); }
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(16px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    @keyframes waPulse {
      0%,100% { box-shadow: 0 4px 20px rgba(37,211,102,0.45); }
      50%      { box-shadow: 0 4px 32px rgba(37,211,102,0.75), 0 0 0 10px rgba(37,211,102,0.1); }
    }
    @keyframes crownGlow {
      0%,100% { filter: drop-shadow(0 0 4px rgba(255,215,0,0.4)); }
      50%     { filter: drop-shadow(0 0 12px rgba(255,215,0,0.9)); }
    }
    @keyframes confettiDrop {
      0%   { transform: translateY(-20px) rotate(0deg); opacity: 1; }
      100% { transform: translateY(80px) rotate(720deg); opacity: 0; }
    }
    /* CSS confetti fallback pieces */
    .confetti-piece {
      position: absolute;
      width: 8px; height: 8px;
      border-radius: 2px;
      animation: confettiDrop 1.2s ease-out forwards;
    }
    /* Sparkle burst on card hover */
    .product-card::before {
      content: '✦';
      position: absolute;
      top: 10px; inset-inline-end: 48px;
      font-size: 1.2rem;
      color: var(--gold);
      opacity: 0;
      transform: scale(0) rotate(-20deg);
      transition: opacity 0.3s, transform 0.3s;
      pointer-events: none;
    }
    .product-card:hover::before { opacity: 1; transform: scale(1) rotate(15deg); }
    /* Crown Lottie glow */
    .crown-lottie-wrap {
      animation: crownGlow 3s ease-in-out infinite;
    }

    /* ============================================================
       MOBILE RESPONSIVE
    ============================================================ */
    @media (max-width: 900px) {
      .steps-grid { grid-template-columns: 1fr; max-width: 480px; margin: 0 auto; }
    }
    @media (max-width: 768px) {
      :root { --header-h: 60px; }
      .nav-menu { display: none; }
      .hamburger { display: flex; }
      #menu-toggle:checked ~ .nav-menu { display: flex; flex-direction: column; }
      .nav-menu {
        position: fixed;
        top: 60px; inset-inline-start: 0;
        width: 100%;
        background: rgba(255,255,255,0.97);
        backdrop-filter: blur(12px);
        padding: 20px;
        gap: 16px;
        border-bottom: 1px solid var(--pink-light);
        z-index: 999;
      }
      .nav-menu a { font-size: 1rem; padding: 8px 0; }
      .form-wrapper { padding: 32px 20px; }
      .about-card { padding: 32px 20px; }
      section { padding: 56px 0; }
      .products-grid { grid-template-columns: 1fr; max-width: 400px; margin: 0 auto; }
      .hero-title { font-size: 2rem; }
    }
    @media (min-width: 480px) and (max-width: 768px) {
      .products-grid { grid-template-columns: repeat(2, 1fr); max-width: none; }
    }
```

- [ ] **Step 2: Commit**
```bash
git add index.html
git commit -m "feat: add keyframe animations and mobile responsive CSS"
```

---

## Task 5: HTML — header + hero body content

**Files:**
- Modify: `index.html` — replace `<!-- content added in subsequent tasks -->` with the following

- [ ] **Step 1: Replace the comment inside `<body>` with this full HTML (add before `</body>`)**

```html
  <!-- ======================================================
       STORE CLOSED BANNER (shown when STORE_OPEN = false)
  ====================================================== -->
  <div id="store-closed-banner" style="display:none">
    <span data-he="👑 אנה בהפסקה! חוזרת בקרוב 🌸" data-en="👑 Anna is on a break! Back soon. 🌸"></span>
  </div>

  <!-- ======================================================
       STICKY HEADER
  ====================================================== -->
  <header>
    <div class="container header-inner">
      <!-- Logo -->
      <a href="#home" class="logo-wrap">
        <div class="crown-lottie-wrap" id="crown-lottie-wrap">
          <!-- Lottie crown added in Task 8; SVG fallback below -->
          <svg id="crown-svg" width="44" height="36" viewBox="0 0 44 36" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
            <path d="M4 28 L4 32 L40 32 L40 28 L4 28Z" fill="#FFD700" stroke="#F0B800" stroke-width="0.5"/>
            <path d="M4 28 L10 10 L22 22 L34 6 L40 28 Z" fill="#FFD700" stroke="#F0B800" stroke-width="0.8"/>
            <circle cx="4"  cy="10" r="2.5" fill="#E91E8C"/>
            <circle cx="22" cy="22" r="2.5" fill="#E91E8C"/>
            <circle cx="40" cy="10" r="2.5" fill="#E91E8C"/>
            <circle cx="34" cy="6"  r="2"   fill="#9c27b0"/>
            <circle cx="10" cy="10" r="2"   fill="#9c27b0"/>
          </svg>
        </div>
        <div class="logo-text-wrap">
          <span class="logo-name">Princess Anna</span>
          <span class="logo-tagline">✦ Jewelry &amp; Accessories ✦</span>
        </div>
      </a>

      <!-- Nav (desktop) -->
      <input type="checkbox" id="menu-toggle" aria-hidden="true">
      <ul class="nav-menu" role="navigation" aria-label="Main navigation">
        <li><a href="#home"         data-en="Home"  data-he="בית"></a></li>
        <li><a href="#shop"         data-en="Shop"  data-he="חנות"></a></li>
        <li><a href="#about"        data-en="About" data-he="אודות"></a></li>
        <li><a href="#order"        data-en="Order" data-he="הזמנה"></a></li>
      </ul>

      <!-- Right side: lang toggle + hamburger -->
      <div style="display:flex;align-items:center;gap:12px;">
        <div class="lang-toggle" role="group" aria-label="Language switcher">
          <button class="lang-btn" id="lang-he-btn" onclick="setLanguage('he')" aria-label="עברית">🇮🇱 עב</button>
          <button class="lang-btn" id="lang-en-btn" onclick="setLanguage('en')" aria-label="English">🇬🇧 EN</button>
        </div>
        <label class="hamburger" for="menu-toggle" aria-label="Toggle menu">
          <span></span><span></span><span></span>
        </label>
      </div>
    </div>
  </header>

  <!-- ======================================================
       HERO
  ====================================================== -->
  <section id="home">
    <!-- Lottie sparkle background (added Task 8) -->
    <div class="hero-lottie-bg" id="hero-sparkle-wrap">
      <!-- CSS fallback particles -->
      <span class="sparkle-particle" style="top:15%;inset-inline-start:8%;--dur:5s;--delay:0s">✦</span>
      <span class="sparkle-particle" style="top:25%;inset-inline-start:18%;--dur:6s;--delay:1s">✧</span>
      <span class="sparkle-particle" style="top:60%;inset-inline-start:5%;--dur:4.5s;--delay:0.5s">★</span>
      <span class="sparkle-particle" style="top:70%;inset-inline-start:22%;--dur:7s;--delay:2s">✨</span>
      <span class="sparkle-particle" style="top:10%;inset-inline-end:10%;--dur:5.5s;--delay:1.5s">✦</span>
      <span class="sparkle-particle" style="top:30%;inset-inline-end:5%;--dur:4s;--delay:0.8s">✧</span>
      <span class="sparkle-particle" style="top:55%;inset-inline-end:15%;--dur:6.5s;--delay:3s">★</span>
      <span class="sparkle-particle" style="top:80%;inset-inline-end:8%;--dur:5s;--delay:0.3s">✦</span>
      <span class="sparkle-particle" style="top:45%;inset-inline-start:50%;--dur:7s;--delay:1s">✨</span>
      <span class="sparkle-particle" style="top:20%;inset-inline-start:40%;--dur:4.8s;--delay:2.5s">✧</span>
      <span class="sparkle-particle" style="top:75%;inset-inline-start:35%;--dur:6s;--delay:0.2s">★</span>
      <span class="sparkle-particle" style="top:5%;inset-inline-start:55%;--dur:5.2s;--delay:3.5s">✦</span>
      <span class="sparkle-particle" style="top:88%;inset-inline-start:60%;--dur:4.2s;--delay:1.8s">✧</span>
      <span class="sparkle-particle" style="top:38%;inset-inline-end:30%;--dur:7.5s;--delay:0.6s">★</span>
      <span class="sparkle-particle" style="top:65%;inset-inline-end:40%;--dur:5.8s;--delay:4s">✨</span>
    </div>
    <div class="hero-content">
      <div class="hero-badge" data-en="🌍 Worldwide Shipping" data-he="🌍 משלוח לכל הארץ"></div>
      <h1 class="hero-title" data-en="Welcome to Princess Anna's Store 👑" data-he="ברוכים הבאים לחנות של פרינסס אנה 👑"></h1>
      <p class="hero-sub" data-en="Unique jewelry &amp; accessories, delivered to your door" data-he="תכשיטים ואקססוריז מיוחדים, עד הבית שלך"></p>
      <a href="#shop" class="btn-primary" data-en="Shop Now ✨" data-he="לקנייה ✨"></a>
    </div>
  </section>
```

- [ ] **Step 2: Open in browser — verify header and hero render correctly (sticky header, pink hero bg, sparkle particles floating)**

- [ ] **Step 3: Commit**
```bash
git add index.html
git commit -m "feat: add header and hero HTML"
```

---

## Task 6: HTML — shop section (5 product cards)

**Files:**
- Modify: `index.html` — append after `</section>` (hero), before `</body>`

- [ ] **Step 1: Append shop section HTML**

```html
  <!-- ======================================================
       SHOP SECTION
  ====================================================== -->
  <section id="shop">
    <div class="container">
      <h2 class="section-title" data-en="Our Collection ✨" data-he="הקולקציה שלנו ✨"></h2>
      <div class="gold-line"></div>
      <div class="products-grid">

        <!-- PRODUCT CARD 1 -->
        <div class="product-card">
          <div class="card-image-area">
            <span class="product-emoji">⭐</span>
            <span class="card-badge badge-gold" data-en="BESTSELLER" data-he="הנמכר ביותר"></span>
            <button class="heart-btn" aria-label="Add to wishlist">♡</button>
          </div>
          <div class="card-body">
            <h3 class="product-name" data-en="Crystal Star Necklace" data-he="שרשרת כוכב קריסטל"></h3>
            <p class="product-desc" data-en="Delicate chain with sparkling crystal star pendant" data-he="שרשרת עדינה עם תליון כוכב קריסטל מנצנץ"></p>
            <div class="product-footer">
              <span class="product-price">₪55</span>
              <a href="#order" class="btn-order" data-en="Order Now" data-he="להזמנה"></a>
            </div>
          </div>
        </div>

        <!-- PRODUCT CARD 2 -->
        <div class="product-card">
          <div class="card-image-area">
            <span class="product-emoji">🦋</span>
            <span class="card-badge badge-green" data-en="NEW" data-he="חדש"></span>
            <button class="heart-btn" aria-label="Add to wishlist">♡</button>
          </div>
          <div class="card-body">
            <h3 class="product-name" data-en="Pink Butterfly Bracelet" data-he="צמיד פרפר ורוד"></h3>
            <p class="product-desc" data-en="Adjustable bracelet with butterfly charm and pink gems" data-he="צמיד מתכוונן עם פרפר ואבני ורוד"></p>
            <div class="product-footer">
              <span class="product-price">₪45</span>
              <a href="#order" class="btn-order" data-en="Order Now" data-he="להזמנה"></a>
            </div>
          </div>
        </div>

        <!-- PRODUCT CARD 3 -->
        <div class="product-card">
          <div class="card-image-area">
            <span class="product-emoji">🎀</span>
            <button class="heart-btn" aria-label="Add to wishlist">♡</button>
          </div>
          <div class="card-body">
            <h3 class="product-name" data-en="Sparkle Hair Bow" data-he="קשת שיער מנצנצת"></h3>
            <p class="product-desc" data-en="Large satin bow with glitter details" data-he="קשת סאטן גדולה עם פרטי גליטר"></p>
            <div class="product-footer">
              <span class="product-price">₪38</span>
              <a href="#order" class="btn-order" data-en="Order Now" data-he="להזמנה"></a>
            </div>
          </div>
        </div>

        <!-- PRODUCT CARD 4 -->
        <div class="product-card">
          <div class="card-image-area">
            <span class="product-emoji">✨</span>
            <span class="card-badge badge-purple" data-en="NO PIERCING" data-he="ללא ניקוב"></span>
            <button class="heart-btn" aria-label="Add to wishlist">♡</button>
          </div>
          <div class="card-body">
            <h3 class="product-name" data-en="Clip-On Star Earrings" data-he="עגילי כוכב קליפס"></h3>
            <p class="product-desc" data-en="Comfortable clip-on earrings with crystal stars — no piercing needed" data-he="עגילי קליפס עם כוכבי קריסטל — ללא ניקוב"></p>
            <div class="product-footer">
              <span class="product-price">₪42</span>
              <a href="#order" class="btn-order" data-en="Order Now" data-he="להזמנה"></a>
            </div>
          </div>
        </div>

        <!-- PRODUCT CARD 5 -->
        <div class="product-card">
          <div class="card-image-area">
            <span class="product-emoji">👜</span>
            <span class="card-badge badge-rose" data-en="LIMITED" data-he="מוגבל"></span>
            <button class="heart-btn" aria-label="Add to wishlist">♡</button>
          </div>
          <div class="card-body">
            <h3 class="product-name" data-en="Mini Glitter Handbag" data-he="תיק מיני גליטר"></h3>
            <p class="product-desc" data-en="Tiny sparkle shoulder bag, perfect for special occasions" data-he="תיק כתף קטן ומנצנץ, מושלם לאירועים"></p>
            <div class="product-footer">
              <span class="product-price">₪89</span>
              <a href="#order" class="btn-order" data-en="Order Now" data-he="להזמנה"></a>
            </div>
          </div>
        </div>

      </div><!-- /products-grid -->
    </div><!-- /container -->
  </section>
```

- [ ] **Step 2: Verify in browser — 5 cards in responsive grid, hover lifts card, badges display**

- [ ] **Step 3: Commit**
```bash
git add index.html
git commit -m "feat: add shop section with 5 product cards"
```

---

## Task 7: HTML — how-it-works + order form + about + footer + WhatsApp

**Files:**
- Modify: `index.html` — append after shop `</section>`, before `</body>`

- [ ] **Step 1: Append remaining sections**

```html
  <!-- ======================================================
       HOW IT WORKS
  ====================================================== -->
  <section id="how-it-works">
    <div class="container">
      <h2 class="section-title" data-en="How It Works" data-he="איך זה עובד"></h2>
      <div class="gold-line"></div>
      <div class="steps-grid">

        <div class="step-card">
          <span class="step-number">1</span>
          <div class="step-icon" id="step-icon-1">
            <!-- Lottie added Task 8 -->
            <span class="step-icon-fallback" id="step-fallback-1">🛍️</span>
          </div>
          <h3 class="step-title" data-en="Choose your favorite item" data-he="בחרי את המוצר שאהבתם"></h3>
          <p class="step-desc" data-en="Browse our magical collection and pick what you love" data-he="עיינו בקולקציה הקסומה ובחרו מה שאוהבים"></p>
        </div>

        <div class="step-card">
          <span class="step-number">2</span>
          <div class="step-icon" id="step-icon-2">
            <span class="step-icon-fallback" id="step-fallback-2">📝</span>
          </div>
          <h3 class="step-title" data-en="Fill the order form" data-he="מלאי טופס הזמנה"></h3>
          <p class="step-desc" data-en="Fill in your details and we'll take care of the rest" data-he="מלאו את הפרטים ואנחנו נדאג לשאר"></p>
        </div>

        <div class="step-card">
          <span class="step-number">3</span>
          <div class="step-icon" id="step-icon-3">
            <span class="step-icon-fallback" id="step-fallback-3">📦</span>
          </div>
          <h3 class="step-title" data-en="Receive at home in 10–20 days" data-he="קבלי עד הבית תוך 10–20 יום"></h3>
          <p class="step-desc" data-en="Your magical item arrives at your door" data-he="הפריט הקסום שלך מגיע עד הבית"></p>
        </div>

      </div>
    </div>
  </section>

  <!-- ======================================================
       ORDER FORM
  ====================================================== -->
  <section id="order">
    <div class="container">
      <h2 class="section-title" data-en="Place Your Order 👑" data-he="הזמינו עכשיו 👑"></h2>
      <div class="gold-line"></div>
      <div class="form-wrapper">

        <!-- Thank you message (hidden until submit) -->
        <div id="thank-you">
          <div id="thankyou-lottie-wrap">
            <!-- Lottie confetti added Task 8; CSS confetti fallback injected by JS -->
          </div>
          <p class="thankyou-text" id="thankyou-text"
            data-en="👑 Thank you! Anna received your order and will contact you within 24 hours to confirm payment via Bit or Paybox. Get ready for something magical! ✨"
            data-he="👑 תודה רבה! אנה קיבלה את ההזמנה שלך ותיצור איתך קשר תוך 24 שעות לאישור תשלום דרך ביט או פייבוקס. תתכוננו למשהו קסום! ✨">
          </p>
        </div>

        <form id="order-form"
              action="https://formspree.io/f/REPLACE_WITH_YOUR_FORMSPREE_ID"
              method="POST">

          <div class="form-row">
            <label data-en="Full Name *" data-he="שם מלא *"></label>
            <input type="text" name="full_name" required
                   data-placeholder-en="Your full name" data-placeholder-he="השם המלא שלך">
          </div>

          <div class="form-row">
            <label data-en="Phone *" data-he="טלפון *"></label>
            <input type="tel" name="phone" required
                   data-placeholder-en="Your phone number" data-placeholder-he="מספר הטלפון שלך">
          </div>

          <div class="form-row">
            <label data-en="Email *" data-he="אימייל *"></label>
            <input type="email" name="email" required
                   data-placeholder-en="your@email.com" data-placeholder-he="your@email.com">
          </div>

          <div class="form-row">
            <label data-en="City *" data-he="עיר *"></label>
            <input type="text" name="city" required
                   data-placeholder-en="Your city" data-placeholder-he="העיר שלך">
          </div>

          <div class="form-row">
            <label data-en="Full Address *" data-he="כתובת מלאה *"></label>
            <input type="text" name="address" required
                   data-placeholder-en="Street, number, floor/apt" data-placeholder-he="רחוב, מספר, קומה/דירה">
          </div>

          <div class="form-row">
            <label data-en="Product *" data-he="מוצר *"></label>
            <select name="product" required id="product-select">
              <option value="" data-en="— Select a product —" data-he="— בחרי מוצר —"></option>
              <option value="crystal-star-necklace" data-en="Crystal Star Necklace — ₪55" data-he="שרשרת כוכב קריסטל — ₪55"></option>
              <option value="pink-butterfly-bracelet" data-en="Pink Butterfly Bracelet — ₪45" data-he="צמיד פרפר ורוד — ₪45"></option>
              <option value="sparkle-hair-bow" data-en="Sparkle Hair Bow — ₪38" data-he="קשת שיער מנצנצת — ₪38"></option>
              <option value="clip-on-star-earrings" data-en="Clip-On Star Earrings — ₪42" data-he="עגילי כוכב קליפס — ₪42"></option>
              <option value="mini-glitter-handbag" data-en="Mini Glitter Handbag — ₪89" data-he="תיק מיני גליטר — ₪89"></option>
            </select>
          </div>

          <div class="form-row">
            <label data-en="Quantity" data-he="כמות"></label>
            <input type="number" name="quantity" min="1" max="10" value="1">
          </div>

          <div class="form-row">
            <label data-en="Notes (optional)" data-he="הערות (אופציונלי)"></label>
            <textarea name="notes"
                      data-placeholder-en="Any special requests?" data-placeholder-he="בקשות מיוחדות?"></textarea>
          </div>

          <div class="form-row">
            <label data-en="How did you hear about us?" data-he="איך שמעתם עלינו?"></label>
            <select name="referral" id="referral-select">
              <option value="instagram" data-en="Instagram" data-he="אינסטגרם"></option>
              <option value="tiktok"    data-en="TikTok"    data-he="טיקטוק"></option>
              <option value="whatsapp"  data-en="WhatsApp"  data-he="וואטסאפ"></option>
              <option value="friend"    data-en="Friend"    data-he="חבר/ה"></option>
              <option value="other"     data-en="Other"     data-he="אחר"></option>
            </select>
          </div>

          <div class="payment-box">
            <span data-en="💳 Payment is made after order confirmation via Bit or Paybox"
                  data-he="💳 התשלום מתבצע לאחר אישור ההזמנה דרך ביט או פייבוקס"></span>
          </div>

          <button type="submit" class="btn-submit"
                  data-en="Send Order ✨" data-he="שליחת הזמנה ✨"></button>
        </form>

      </div><!-- /form-wrapper -->
    </div><!-- /container -->
  </section>

  <!-- ======================================================
       ABOUT
  ====================================================== -->
  <section id="about">
    <div class="container">
      <div class="about-card">
        <div class="about-crown">👑</div>
        <h2 class="section-title" style="margin-bottom:16px"
            data-en="About Princess Anna" data-he="על פרינסס אנה"></h2>
        <p class="about-text"
           data-en="Hi! I'm Anna, and I'm 8 years old. I love beautiful things — sparkly jewelry, colorful accessories, and everything that makes you feel like a princess. I carefully pick every item in my store so you get only the most magical pieces. Thank you for supporting my little shop! 👑"
           data-he="היי! אני אנה, ובת 8. אני אוהבת דברים יפים — תכשיטים מנצנצים, אקססוריז צבעוניים, וכל מה שגורם לך להרגיש כמו נסיכה. אני בוחרת בקפידה כל מוצר בחנות שלי כדי שתקבלי רק את הפריטים הכי קסומים. תודה שאתם תומכים בחנות הקטנה שלי! 👑">
        </p>
      </div>
    </div>
  </section>

  <!-- ======================================================
       FOOTER
  ====================================================== -->
  <footer>
    <div class="container">
      <div class="footer-logo-name">Princess Anna</div>
      <div class="footer-tagline">✦ Jewelry &amp; Accessories ✦</div>
      <div class="social-links">
        <a href="REPLACE_INSTAGRAM" class="social-btn" aria-label="Instagram" target="_blank" rel="noopener">
          <!-- Instagram SVG icon -->
          <svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor" aria-hidden="true"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/></svg>
        </a>
        <a href="REPLACE_TIKTOK" class="social-btn" aria-label="TikTok" target="_blank" rel="noopener">
          <!-- TikTok SVG icon -->
          <svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor" aria-hidden="true"><path d="M19.59 6.69a4.83 4.83 0 01-3.77-4.25V2h-3.45v13.67a2.89 2.89 0 01-2.88 2.5 2.89 2.89 0 01-2.89-2.89 2.89 2.89 0 012.89-2.89c.28 0 .54.04.79.1V9.01a6.33 6.33 0 00-.79-.05 6.34 6.34 0 00-6.34 6.34 6.34 6.34 0 006.34 6.34 6.34 6.34 0 006.33-6.34V8.69a8.18 8.18 0 004.78 1.52V6.76a4.85 4.85 0 01-1.01-.07z"/></svg>
        </a>
      </div>
      <p class="footer-info"
         data-en="🌍 Worldwide Shipping | 💳 Bit &amp; Paybox | 📦 10–20 Days Delivery"
         data-he="🌍 משלוח לכל העולם | 💳 תשלום בביט ופייבוקס | 📦 10–20 ימי עסקים"></p>
      <p class="footer-policy"
         data-en="Your information is used only to process your order and will never be shared."
         data-he="המידע שלך משמש רק לעיבוד ההזמנה ולא יועבר לאף גורם אחר."></p>
      <p class="footer-copy">© 2025 Princess Anna Store — All rights reserved</p>
    </div>
  </footer>

  <!-- ======================================================
       WHATSAPP FLOATING BUTTON
  ====================================================== -->
  <a id="whatsapp-btn" href="https://wa.me/REPLACE_WITH_PHONE_NUMBER" target="_blank" rel="noopener" aria-label="Chat on WhatsApp">
    <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
      <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/>
    </svg>
    <span class="wa-tooltip" data-en="Chat with Anna!" data-he="שלחו הודעה לאנה!"></span>
  </a>
```

- [ ] **Step 2: Open in browser — verify all sections render: how-it-works 3 steps, form fields visible, about card, dark footer, green WhatsApp button**

- [ ] **Step 3: Commit**
```bash
git add index.html
git commit -m "feat: add how-it-works, order form, about, footer, WhatsApp HTML"
```

---

## Task 8: Find Lottie animation URLs

**Files:**
- No file changes in this task — research only

- [ ] **Step 1: Search for hero sparkle/glitter Lottie animation**

Run WebSearch: `lottie animation glitter sparkle loop free JSON site:lottiefiles.com`  
Find a looping glitter/sparkle animation. Copy the CDN URL (format: `https://lottie.host/{uuid}/{name}.json`).  
Save as: `LOTTIE_SPARKLE_URL`

- [ ] **Step 2: Search for crown/princess Lottie animation**

Run WebSearch: `lottie animation crown princess gold loop free site:lottiefiles.com`  
Find a looping crown animation. Copy CDN URL.  
Save as: `LOTTIE_CROWN_URL`

- [ ] **Step 3: Search for shopping bag step icon**

Run WebSearch: `lottie animation shopping bag icon loop free site:lottiefiles.com`  
Find a shopping bag animation. Copy CDN URL.  
Save as: `LOTTIE_BAG_URL`

- [ ] **Step 4: Search for pencil/writing step icon**

Run WebSearch: `lottie animation pencil writing form icon loop free site:lottiefiles.com`  
Find a pencil or form-writing animation. Copy CDN URL.  
Save as: `LOTTIE_PENCIL_URL`

- [ ] **Step 5: Search for delivery/package step icon**

Run WebSearch: `lottie animation delivery package box icon loop free site:lottiefiles.com`  
Find a delivery box or package animation. Copy CDN URL.  
Save as: `LOTTIE_BOX_URL`

- [ ] **Step 6: Search for confetti/celebration animation**

Run WebSearch: `lottie animation confetti celebration burst free site:lottiefiles.com`  
Find a confetti burst animation (does NOT need to loop — `loop` attribute omitted).  
Save as: `LOTTIE_CONFETTI_URL`

- [ ] **Step 7: Verify each URL is accessible**

For each URL, run: `curl -I {URL}` — verify HTTP 200 response. If a URL is broken, search for an alternative.

---

## Task 9: Insert Lottie player elements into HTML

**Files:**
- Modify: `index.html` — insert `<lottie-player>` elements using URLs found in Task 8

- [ ] **Step 1: Replace crown SVG fallback container**

In `index.html`, find the element with `id="crown-lottie-wrap"` and replace its contents:

```html
        <div class="crown-lottie-wrap" id="crown-lottie-wrap">
          <lottie-player
            src="LOTTIE_CROWN_URL"
            background="transparent"
            speed="0.8"
            loop
            autoplay
            style="width:48px;height:40px;"
            aria-hidden="true">
          </lottie-player>
          <!-- SVG crown shown if Lottie fails to load -->
          <svg id="crown-svg" style="display:none" width="44" height="36" viewBox="0 0 44 36" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
            <path d="M4 28 L4 32 L40 32 L40 28 L4 28Z" fill="#FFD700" stroke="#F0B800" stroke-width="0.5"/>
            <path d="M4 28 L10 10 L22 22 L34 6 L40 28 Z" fill="#FFD700" stroke="#F0B800" stroke-width="0.8"/>
            <circle cx="4"  cy="10" r="2.5" fill="#E91E8C"/>
            <circle cx="22" cy="22" r="2.5" fill="#E91E8C"/>
            <circle cx="40" cy="10" r="2.5" fill="#E91E8C"/>
            <circle cx="34" cy="6"  r="2"   fill="#9c27b0"/>
            <circle cx="10" cy="10" r="2"   fill="#9c27b0"/>
          </svg>
        </div>
```

- [ ] **Step 2: Replace hero sparkle background**

Find `id="hero-sparkle-wrap"` and prepend a `<lottie-player>` before the CSS particle `<span>` elements:

```html
    <div class="hero-lottie-bg" id="hero-sparkle-wrap">
      <lottie-player
        src="LOTTIE_SPARKLE_URL"
        background="transparent"
        speed="1"
        loop
        autoplay
        style="width:min(700px,100vw);height:min(700px,100vh);position:absolute;inset:0;margin:auto;"
        aria-hidden="true">
      </lottie-player>
      <!-- CSS fallback particles remain below -->
      <span class="sparkle-particle" ...
```

- [ ] **Step 3: Replace step icons 1–3**

For each of the three step icon containers, replace the fallback span with a `<lottie-player>`:

**Step icon 1** — find `id="step-icon-1"`, replace inner content:
```html
          <div class="step-icon" id="step-icon-1">
            <lottie-player src="LOTTIE_BAG_URL" background="transparent" speed="1" loop autoplay style="width:100px;height:100px;" aria-hidden="true"></lottie-player>
          </div>
```

**Step icon 2** — find `id="step-icon-2"`, replace:
```html
          <div class="step-icon" id="step-icon-2">
            <lottie-player src="LOTTIE_PENCIL_URL" background="transparent" speed="1" loop autoplay style="width:100px;height:100px;" aria-hidden="true"></lottie-player>
          </div>
```

**Step icon 3** — find `id="step-icon-3"`, replace:
```html
          <div class="step-icon" id="step-icon-3">
            <lottie-player src="LOTTIE_BOX_URL" background="transparent" speed="1" loop autoplay style="width:100px;height:100px;" aria-hidden="true"></lottie-player>
          </div>
```

- [ ] **Step 4: Add confetti Lottie to thank-you section**

Find `id="thankyou-lottie-wrap"` and replace its content:
```html
          <div id="thankyou-lottie-wrap">
            <lottie-player
              id="confetti-lottie"
              src="LOTTIE_CONFETTI_URL"
              background="transparent"
              speed="1"
              style="width:200px;height:200px;margin:0 auto;"
              aria-hidden="true">
            </lottie-player>
          </div>
```
Note: no `loop` attribute on confetti — it plays once per order submission.

- [ ] **Step 5: Open in browser and verify all Lottie animations load (check Network tab for 200 responses on JSON files)**

- [ ] **Step 6: Commit**
```bash
git add index.html
git commit -m "feat: integrate Lottie animations (crown, sparkle, step icons, confetti)"
```

---

## Task 10: JavaScript — language switcher, form handler, store open/close

**Files:**
- Modify: `index.html` — append complete `<script>` block before `</body>`

- [ ] **Step 1: Append the following script block**

```html
  <script>
    // ============================================================
    // STORE CONFIGURATION
    // ============================================================
    const STORE_OPEN = true; // Change to false to show closed banner

    // ============================================================
    // LANGUAGE SWITCHER
    // ============================================================
    function setLanguage(lang) {
      const root = document.getElementById('html-root');
      root.lang = lang;
      root.dir = lang === 'he' ? 'rtl' : 'ltr';

      // Swap all text nodes that have data-en / data-he
      document.querySelectorAll('[data-en][data-he]').forEach(function(el) {
        el.textContent = el.dataset[lang];
      });

      // Swap placeholders
      document.querySelectorAll('[data-placeholder-en][data-placeholder-he]').forEach(function(el) {
        el.placeholder = lang === 'he' ? el.dataset.placeholderHe : el.dataset.placeholderEn;
      });

      // Swap <option> elements inside selects
      document.querySelectorAll('option[data-en][data-he]').forEach(function(el) {
        el.textContent = el.dataset[lang];
      });

      // Update active button state
      document.getElementById('lang-he-btn').classList.toggle('active', lang === 'he');
      document.getElementById('lang-en-btn').classList.toggle('active', lang === 'en');

      // Persist preference
      localStorage.setItem('princess-anna-lang', lang);
    }

    // ============================================================
    // FORM SUBMISSION — async POST to Formspree, no page reload
    // ============================================================
    var orderForm = document.getElementById('order-form');
    if (orderForm) {
      orderForm.addEventListener('submit', function(e) {
        e.preventDefault();

        var btn = orderForm.querySelector('.btn-submit');
        var lang = document.getElementById('html-root').lang || 'he';
        btn.disabled = true;
        btn.textContent = lang === 'he' ? 'שולחת...' : 'Sending...';

        fetch(orderForm.action, {
          method: 'POST',
          body: new FormData(orderForm),
          headers: { 'Accept': 'application/json' }
        })
        .then(function(response) {
          if (response.ok) {
            // Hide form, show thank-you
            orderForm.style.display = 'none';
            var ty = document.getElementById('thank-you');
            ty.classList.add('show');

            // Set correct thank-you text for current language
            var tyText = document.getElementById('thankyou-text');
            tyText.textContent = tyText.dataset[lang];

            // Play confetti Lottie
            var confettiLottie = document.getElementById('confetti-lottie');
            if (confettiLottie) {
              confettiLottie.play();
            } else {
              // CSS confetti fallback
              spawnCSSConfetti(document.getElementById('thankyou-lottie-wrap'));
            }
          } else {
            btn.disabled = false;
            btn.textContent = lang === 'he' ? 'שליחת הזמנה ✨' : 'Send Order ✨';
            alert(lang === 'he'
              ? 'שגיאה בשליחה. נסי שוב.'
              : 'Submission error. Please try again.');
          }
        })
        .catch(function() {
          btn.disabled = false;
          btn.textContent = lang === 'he' ? 'שליחת הזמנה ✨' : 'Send Order ✨';
          alert(lang === 'he'
            ? 'שגיאת רשת. בדקי חיבור לאינטרנט.'
            : 'Network error. Check your connection.');
        });
      });
    }

    // ============================================================
    // CSS CONFETTI FALLBACK (used if Lottie confetti unavailable)
    // ============================================================
    function spawnCSSConfetti(container) {
      var colors = ['#E91E8C','#FFD700','#FF69B4','#9c27b0','#4caf50','#FF6B6B'];
      for (var i = 0; i < 20; i++) {
        (function(i) {
          var piece = document.createElement('div');
          piece.className = 'confetti-piece';
          piece.style.cssText = [
            'position:absolute',
            'left:' + Math.random() * 100 + '%',
            'top:0',
            'background:' + colors[Math.floor(Math.random() * colors.length)],
            'width:' + (6 + Math.random() * 8) + 'px',
            'height:' + (6 + Math.random() * 8) + 'px',
            'border-radius:' + (Math.random() > 0.5 ? '50%' : '2px'),
            'animation-delay:' + (Math.random() * 0.8) + 's',
            'animation-duration:' + (0.8 + Math.random() * 0.8) + 's'
          ].join(';');
          container.style.position = 'relative';
          container.style.overflow = 'hidden';
          container.style.height = '80px';
          container.appendChild(piece);
        })(i);
      }
    }

    // ============================================================
    // STORE CLOSED BANNER
    // ============================================================
    if (!STORE_OPEN) {
      document.getElementById('store-closed-banner').style.display = 'block';
    }

    // ============================================================
    // INIT — run on page load
    // ============================================================
    (function init() {
      var savedLang = localStorage.getItem('princess-anna-lang') || 'he';
      setLanguage(savedLang);
    })();
  </script>
```

- [ ] **Step 2: Open in browser and test:**
  - Page loads in Hebrew (RTL) by default
  - Click "🇬🇧 EN" — all text switches to English, layout mirrors to LTR
  - Click "🇮🇱 עב" — switches back to Hebrew
  - Reload page — language persists (localStorage)
  - Open DevTools Console — no JS errors

- [ ] **Step 3: Test form (temporarily):**
  - Fill out the form completely
  - Submit — verify loading state on button, then thank-you message appears
  - (Formspree will return error since ID is placeholder — verify the error handler shows the alert instead of crashing)

- [ ] **Step 4: Test store closed:**
  - In `<script>`, temporarily change `STORE_OPEN = false`
  - Reload — verify pink banner appears at top
  - Change back to `true`

- [ ] **Step 5: Commit**
```bash
git add index.html
git commit -m "feat: add JavaScript (language switcher, form handler, store toggle)"
```

---

## Task 11: README.md

**Files:**
- Create: `README.md`

- [ ] **Step 1: Create `README.md` with this content**

```markdown
# Princess Anna Store 👑
# חנות פרינסס אנה 👑

A magical jewelry & accessories dropshipping store / חנות תכשיטים ואקססוריז קסומה

---

## Deploy to GitHub Pages / פריסה ל-GitHub Pages

1. Create a GitHub account at github.com with the email `princessanna.shop@gmail.com`
2. Click **"New Repository"** — name it: `princess-anna`
3. Upload `index.html` to the repository
4. Go to **Settings → Pages → Source: main branch**
5. Your site will be live at: `https://[username].github.io/princess-anna`

---

1. צרי חשבון GitHub בכתובת github.com עם הדוא"ל `princessanna.shop@gmail.com`
2. לחצי **"New Repository"** — שם: `princess-anna`
3. העלי את קובץ `index.html` לריפוזיטורי
4. Settings → Pages → Source: main branch
5. האתר יהיה חי בכתובת: `https://[username].github.io/princess-anna`

---

## Connect Formspree / לחיבור Formspree

**EN:** Sign up at [formspree.io](https://formspree.io) with the same Gmail. Create a "New Form" named "Princess Anna Orders". Copy the form ID and replace `REPLACE_WITH_YOUR_FORMSPREE_ID` in `index.html`.

**HE:** הירשמי ב-[formspree.io](https://formspree.io) עם אותו Gmail. "New Form" — שם: Princess Anna Orders. העתיקי את ה-ID והחליפי את `REPLACE_WITH_YOUR_FORMSPREE_ID` בקובץ `index.html`.

---

## Connect WhatsApp / לחיבור וואטסאפ

**EN:** Search for `REPLACE_WITH_PHONE_NUMBER` in `index.html` and replace with your number in format `972XXXXXXXXX` (no `+`, no spaces).

**HE:** חפשי `REPLACE_WITH_PHONE_NUMBER` בקובץ `index.html` והחליפי במספר שלך בפורמט `972XXXXXXXXX` (ללא `+` וללא רווחים).

---

## Add Instagram & TikTok / להוסיף רשתות חברתיות

Search for `REPLACE_INSTAGRAM` and `REPLACE_TIKTOK` in `index.html` and replace with your profile URLs.

---

## Temporarily Close Store / לסגירת חנות זמנית

In `index.html`, search for `STORE_OPEN = true` and change to `STORE_OPEN = false`. A banner will appear automatically.

---

## Add Google Analytics / להוסיף Google Analytics

In `index.html`, find the commented Analytics block in `<head>` and replace `GA_MEASUREMENT_ID` with your ID from [analytics.google.com](https://analytics.google.com).
```

- [ ] **Step 2: Commit**
```bash
git add README.md
git commit -m "docs: add deployment guide README (EN + HE)"
```

---

## Task 12: Final verification

- [ ] **Step 1: Open `index.html` via double-click (file:// protocol) — verify everything works without a web server**

- [ ] **Step 2: Resize browser window — verify:**
  - Desktop (>900px): 3-column product grid, horizontal steps
  - Tablet (480–768px): 2-column product grid
  - Mobile (<480px): 1-column, hamburger menu appears, nav collapses

- [ ] **Step 3: Test language switch in both directions — verify ALL text flips including:**
  - Header nav links
  - Hero title, subtitle, CTA button
  - Product names, descriptions, badges, Order Now buttons
  - How It Works step titles and descriptions
  - Form labels and placeholders
  - Payment box text
  - Submit button
  - About text
  - Footer info and policy lines
  - WhatsApp tooltip

- [ ] **Step 4: Test smooth scroll — click each nav link, verify page scrolls to section**

- [ ] **Step 5: Test form submit flow — verify thank-you message appears (even if Formspree errors since ID is placeholder)**

- [ ] **Step 6: Verify product card hover — translateY up + shadow + sparkle ✦ appears**

- [ ] **Step 7: Verify WhatsApp button — pulse animation, tooltip on hover, correct href**

- [ ] **Step 8: Confirm remaining placeholders are clearly visible for Anna to replace:**
  - `REPLACE_WITH_YOUR_FORMSPREE_ID` in form action
  - `REPLACE_WITH_PHONE_NUMBER` in WhatsApp href
  - `REPLACE_INSTAGRAM` and `REPLACE_TIKTOK` in footer
  - `GA_MEASUREMENT_ID` in commented analytics block

- [ ] **Step 9: Final commit**
```bash
git add .
git commit -m "feat: Princess Anna Store — complete single-file website v1.0"
```

---

## Replacements Checklist (share with Anna / hand to user after build)

| Placeholder | Where | Replace with |
|---|---|---|
| `REPLACE_WITH_YOUR_FORMSPREE_ID` | Form `action` attribute | Formspree form ID (e.g. `xpwzbnkq`) |
| `REPLACE_WITH_PHONE_NUMBER` | WhatsApp `href` | `972XXXXXXXXX` |
| `REPLACE_INSTAGRAM` | Footer social link | Instagram profile URL |
| `REPLACE_TIKTOK` | Footer social link | TikTok profile URL |
| `GA_MEASUREMENT_ID` | `<head>` comment | Google Analytics measurement ID |