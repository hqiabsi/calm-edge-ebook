# The Calm Edge — Ebook Website

## 0. Aapki site LIVE hai

**Website:** https://hqiabsi.github.io/calm-edge-ebook/
**Code / editor:** https://github.com/hqiabsi/calm-edge-ebook

Ye site GitHub Pages par chal rahi hai — free, HTTPS ke saath, koi hosting bill nahi.
Neeche diye gaye steps sirf tab chahiye jab aap **dobara se** deploy karna chahein ya doosri jagah
host karna chahein. Aapki site ke liye wo pehle se ho chuka hai.

### Mobile se edit kaise kare (aapke paas phone hai)

**Tarika 1 — seedha GitHub app/browser se (2 minute):**
1. Phone par `github.com/hqiabsi/calm-edge-ebook` kholo (ya GitHub mobile app).
2. `index.html` par tap karo → pencil (✏️) icon → jo badalna hai badlo → **Commit changes**.
3. 1-2 minute mein site update ho jayegi. Browser mein hard refresh karo (ya incognito kholo).

**Tarika 2 — mujhse karwa lo (sabse aasan):**
Yahan chat mein bata do kya badalna hai ("price ₹499 kar do", "reviews hata do", "naya chapter
add karo") — main file edit karke seedha repo mein push kar dunga. Aapko kuch nahi karna.

**Tarika 3 — Netlify par backup copy:**
`https://app.netlify.com/drop` mobile browser par bhi chalta hai, par folder upload karna phone se
mushkil hota hai. Isliye GitHub hi behtar hai.

### Google search mein laane ke liye (ek kaam aapko karna hoga)

Google Search Console verification ke liye aapke Google account ka access chahiye, jo mere paas
nahi hai. Phone se aise karo:

1. Chrome mein `https://search.google.com/search-console` kholo → apne Gmail se login.
2. **Add property** → **URL prefix** chuno → `https://hqiabsi.github.io/calm-edge-ebook/` daalo.
3. Verification method mein **HTML file** chuno → Google ek file dega
   (`googlexxxxxxxx.html`) → **Download** kar lo.
4. Us file ko **yahin chat mein attach kar do** — main use repo mein daal dunga.
5. Wapas Search Console mein **Verify** dabao. Ho jayega.
6. Phir **Sitemaps** → `sitemap.xml` → **Submit**, aur URL Inspection → **Request Indexing**.

(`sitemap.xml` aur `robots.txt` mein aapka asli URL already set hai, kuch badalna nahi hai.)

---

