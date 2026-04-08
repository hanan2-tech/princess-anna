# Princess Anna Store 👑
# חנות פרינסס אנה 👑

A magical jewelry & accessories dropshipping store / חנות תכשיטים ואקססוריז קסומה

---

## Deploy to GitHub Pages / פריסה ל-GitHub Pages

**English:**
1. Create a GitHub account at github.com (email: `princessanna.shop@gmail.com`)
2. Click **New Repository** — name it: `princess-anna` — set to **Public**
3. Upload `index.html` to the repository (drag & drop or "Add file")
4. Go to **Settings → Pages → Source: Deploy from branch → main → / (root)**
5. Click Save — your site will be live at: `https://[username].github.io/princess-anna`

**עברית:**
1. צרי חשבון GitHub בכתובת github.com (עם דוא"ל: `princessanna.shop@gmail.com`)
2. לחצי **New Repository** — שם: `princess-anna` — Public
3. העלי את קובץ `index.html` (גרירה או "Add file")
4. Settings → Pages → Source: Deploy from branch → main → / (root)
5. לחצי Save — האתר יהיה חי בכתובת: `https://[username].github.io/princess-anna`

---

## Connect Formspree / לחיבור Formspree

**English:**
1. Sign up at [formspree.io](https://formspree.io) with the same Gmail
2. Click **New Form** — name: "Princess Anna Orders"
3. Copy the form ID (looks like: `xpwzbnkq`)
4. In `index.html`, search for `REPLACE_WITH_YOUR_FORMSPREE_ID` and replace it

**עברית:**
1. הירשמי ב-[formspree.io](https://formspree.io) עם אותו Gmail
2. לחצי **New Form** — שם: "Princess Anna Orders"
3. העתיקי את ה-ID (נראה כך: `xpwzbnkq`)
4. בקובץ `index.html`, חפשי `REPLACE_WITH_YOUR_FORMSPREE_ID` והחליפי

---

## Connect WhatsApp / לחיבור וואטסאפ

Search for `REPLACE_WITH_PHONE_NUMBER` in `index.html` and replace with your number in format `972XXXXXXXXX` (no `+`, no spaces, no dashes).

חפשי `REPLACE_WITH_PHONE_NUMBER` בקובץ `index.html` והחליפי במספר שלך בפורמט `972XXXXXXXXX` (ללא `+`, ללא רווחים).

---

## Add Social Links / להוסיף רשתות חברתיות

- Search for `REPLACE_INSTAGRAM` → replace with your Instagram profile URL
- Search for `REPLACE_TIKTOK` → replace with your TikTok profile URL

---

## Close Store Temporarily / לסגירת החנות זמנית

In `index.html`, find `var STORE_OPEN = true;` and change to `var STORE_OPEN = false;`

A banner will automatically appear at the top of the page.

---

## Add Google Analytics / Google Analytics

In `index.html`, find the commented `<!-- ANALYTICS: ... -->` block in `<head>`, uncomment it, and replace `GA_MEASUREMENT_ID` with your ID from [analytics.google.com](https://analytics.google.com).

---

## What needs to be replaced before going live:

| Placeholder | Location | Replace with |
|---|---|---|
| `REPLACE_WITH_YOUR_FORMSPREE_ID` | Form `action` attribute | Your Formspree form ID |
| `REPLACE_WITH_PHONE_NUMBER` | WhatsApp button href | `972XXXXXXXXX` |
| `REPLACE_INSTAGRAM` | Footer social link | Your Instagram URL |
| `REPLACE_TIKTOK` | Footer social link | Your TikTok URL |
| `GA_MEASUREMENT_ID` | Head comment block | Google Analytics ID (optional) |
