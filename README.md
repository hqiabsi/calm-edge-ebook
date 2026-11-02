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

## 0a. Home page ab Apple-style hai

| Page | Kya hai | URL |
|---|---|---|
| `index.html` | **Naya home page** — Apple jaisa clean design: hero, highlights, chapters, carousel, collections, buy section | https://hqiabsi.github.io/calm-edge-ebook/ |
| `store.html` | Shop — cart, filters, search, preview | https://hqiabsi.github.io/calm-edge-ebook/store.html |
| `classic.html` | Purana 3D wala landing page (delete nahi kiya, safe rakha hai) | https://hqiabsi.github.io/calm-edge-ebook/classic.html |

**Naya home page ek hi file hai — koi external CSS, koi CDN, koi font link nahi.** Isliye ye kabhi
tootega nahi, offline bhi chalega. Font system ka hai: iPhone/iPad par asli SF Pro dikhta hai
(bilkul Apple jaisa), Windows/Android par Segoe UI / Roboto.

### Edit kaise kare

- **Colours / radius / font:** file ke sabse upar `:root` block (jaise `--blue`, `--ink`, `--grey`).
- **Text:** file mein bade comment markers hain — `<!-- ================= HERO ================= -->`,
  `<!-- ================= HIGHLIGHTS ================= -->` wagairah. Ctrl+F se seedha wahan jao.
- **Book covers:** sab CSS se bante hain, koi image nahi. Har book par teen values:
  `--bw` (width), `--c1`/`--c2` (gradient), `--acc` (accent colour). Bas wahi badlo.
- **Carousel ki books:** `<!-- ================= LATEST / STORE RAIL ================= -->` section.
- **Price:** `#buy` section mein `₹399` / `₹699` (do jagah hain — hero link aur buy band).

---

## 0b. Aapki site par ab DO pages hain

| Page | Kya hai | URL |
|---|---|---|
| `index.html` | Single-book landing page (3D book, sample chapter reader) | https://hqiabsi.github.io/calm-edge-ebook/ |
| `store.html` | **Poora eCommerce store** — 13 books, search, filters, cart, quick preview | https://hqiabsi.github.io/calm-edge-ebook/store.html |

Dono ek doosre se linked hain (landing page ke nav mein "Store", store ke logo se landing).

### Store page mein kya-kya chalta hai

- Header: search bar + category dropdown, login/signup, wishlist, cart badge
- Hero: "featured book of the month" + Festive Sale banner + Get 50% Off coupon
- Categories grid (8 categories, live counts)
- Product grid: cover, badge, title, author, rating, price + MRP + % off, Preview + Add to cart
- Filters: max price, language (Hindi/English), format (PDF/EPUB), rating, author
- Sort: popularity, price low↔high, rating, newest
- Cart drawer: quantity +/−, remove, coupon code (`FESTIVE` 50%, `READ70` 20%, `FIRST10` 10%), total
- Quick preview modal, wishlist (dil ka icon), dark/light toggle
- Trust strip, newsletter, footer
- Cart aur wishlist browser mein save rehte hain (localStorage)

### Store edit kaise kare

**Books badalne ke liye:** `store.html` kholo → Ctrl+F se search karo `const BOOKS` → har book ek block hai:

```js
{ id: 1, title: "The Calm Edge", author: "Devika Mehta", cat: "Self-Help",
  lang: "English", format: "PDF + EPUB", rating: 4.8, reviews: 1240,
  price: 399, mrp: 699, pages: 214, tags: ["Bestseller"],
  c1: "#1d2d3c", c2: "#0b131b", acc: "#e8c583", blurb: "..." }
```

- `price` / `mrp` — sirf number (₹ aur comma nahi)
- `cat` — Fiction, Non-Fiction, Self-Help, Sci-Fi, Competitive Exams, Business, Romance, Children
- `format` — "PDF", "EPUB" ya "PDF + EPUB"
- `tags` — `["Bestseller"]`, `["New"]`, `["Editor's pick"]` ya khali `[]`
- `c1`, `c2`, `acc` — cover ka gradient aur accent colour
- Naya book add karne ke liye koi ek block copy karke `id` badal do

**Coupon badalne ke liye:** `const COUPONS = { FESTIVE: 0.5, ... }` — 0.5 matlab 50% off.

**⚠️ Zaroori:** styling `store.css` mein hai jo **Tailwind se compile** hoti hai. Sirf text, price
ya book data badalne ho to koi rebuild nahi chahiye. Lekin naye *design classes* add karo (naya
button style, naya layout) to CSS dobara build karni padti hai — phone se ye nahi hoga, mujhe bol
dena main rebuild karke push kar dunga.

**Checkout:** abhi demo hai (button toast dikhata hai). Razorpay/Gumroad ka payment link milne par
`#checkoutBtn` wale code mein `window.location.href = "aapka-link"` laga dena — ya mujhe bol dena.

---

Ek ready-to-publish ebook website. Landing page single file hai; store page Tailwind-compiled CSS
(`store.css`) use karta hai. Koi framework, koi server nahi chahiye.

---

## 1. Folder mein kya hai

| File | Kaam |
|---|---|
| `index.html` | Poori website — HTML + CSS + JavaScript sab ek hi file mein. Yahi asli website hai. |
| `README.md` | Yahi guide. |
| `robots.txt` | Search engines ko crawl karne ki permission (Google ke liye zaroori). |
| `sitemap.xml` | Google ko batata hai ki site par kaunse page hain — Search Console mein submit karna hai. |

`index.html` self-contained hai: koi image folder nahi, koi `style.css` nahi, koi `app.js` nahi.
Sirf do cheezein internet se aati hain — Google Fonts aur Three.js (3D library). Agar internet
na ho ya CDN block ho, website phir bhi chalegi: 3D book ki jagah ek CSS wala 3D book dikh jayega.

**Website mein kya-kya hai**

- Interactive 3D book (Three.js) — mouse se drag karke ghumao, **scroll wheel / trackpad se zoom**, mobile par two-finger pinch, aur +/− / reset buttons (double-click se bhi reset)
- Dark + light theme toggle (choice browser mein yaad rehti hai)
- Scroll progress bar, sticky nav, fade-in animations
- Hero, "what's inside", 12-chapter table of contents, author, reviews, 3 pricing plans, FAQ
- 3D book ke neeche **"More titles" mini shelf** — chhote covers par click karo, library khul jayegi aur wahi book search ho jayegi
- **Library section with live search + category filters** — 8 books, title/author/topic se search, chips se filter, "no results" state, `/` key se seedha search box par jump
- Sample chapter reader — modal mein khulta hai, text size A- / A+ aur reading progress ke saath
- Newsletter form, mobile responsive, SEO + Open Graph tags

---

## 2. Pehle apne laptop par dekho (1 minute)

`index.html` par double click karo. Browser mein khul jayegi. Bas.

> Note: 3D book ke liye internet chahiye (Three.js CDN se aata hai). Baaki sab offline chalega.

Agar aap VS Code use karte ho: extension **Live Server** install karo, file par right click →
"Open with Live Server". Isse har save par page khud refresh hota hai — editing bahut aasan.

---

## 3. Sabse fast public karna — Netlify Drop (30 second, free)

Ye beginner ke liye best hai. GitHub account ki bhi zaroorat nahi.

1. `https://app.netlify.com/drop` kholo
2. `ebook-site` folder ko browser mein **drag and drop** kar do (folder, sirf file nahi)
3. 20-30 second mein aapko live link mil jayega, jaise `https://calm-edge-xyz123.netlify.app`
4. Free plan mein 100 GB bandwidth — ek ebook site ke liye kaafi se zyada

Link ko update karna hai? Dobara drop kar do, ya free Netlify account bana lo — phir dashboard se
file replace kar sakte ho aur apna domain bhi laga sakte ho.

---

## 4. GitHub Pages — permanent, free, recommended

Faayde: free, unlimited bandwidth, version history (purana version wapas la sakte ho), aur
`username.github.io` wala professional link.

### 4a. Bina terminal (browser se)

1. `https://github.com` par account banao (free).
2. Top-right **+** → **New repository**.
   - Repository name: `ebook-site`
   - Visibility: **Public** (Pages free plan par public repo chahiye)
   - **Create repository**
3. Repo page par **"uploading an existing file"** link par click karo.
4. `index.html` aur `README.md` dono drag karo → **Commit changes**.
5. **Settings** → left sidebar mein **Pages**.
6. "Build and deployment" ke andar:
   - Source: **Deploy from a branch**
   - Branch: **main**, folder: **/ (root)**
   - **Save**
7. 1-2 minute ruko, page refresh karo. Upar green box mein link aa jayega:
   `https://YOUR-USERNAME.github.io/ebook-site/`

Bas, aapki website live hai. Ye link kisi ko bhi bhej sakte ho.

### 4b. Terminal se (agar git aata hai)

```bash
cd ebook-site
git init
git add .
git commit -m "first version"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/ebook-site.git
git push -u origin main
```

Uske baad Settings → Pages wahi steps.

### 4c. Update kaise kare

- Browser se: repo mein `index.html` kholo → pencil (edit) icon → change karo → **Commit changes**.
- Terminal se: file edit karo, phir

```bash
git add .
git commit -m "price update"
git push
```

1 minute mein live site update ho jayegi. (Purana version chahiye to repo ke **Commits** tab se
wapas ja sakte ho.)

> No-terminal option: **GitHub Desktop** app install karo (`https://desktop.github.com`). Isme
> file edit karke "Commit to main" → "Push origin" dabana hota hai. Bilkul simple.

---

## 5. Vercel ya Cloudflare Pages (optional)

Dono free hain aur GitHub repo se seedha connect ho jaate hain — push karte hi auto-deploy:

- Vercel: `https://vercel.com/new` → Import Git Repository → Framework: **Other** → Deploy
- Cloudflare Pages: `https://pages.cloudflare.com` → Connect to Git → build command khali chhodo,
  output directory `/` rakho

---

## 5b. Google ke apne platform par host karna (Firebase Hosting)

Agar aap website Google ke platform par rakhna chahte ho, to **Firebase Hosting** sahi jagah hai
(free, Google account se, HTTPS built-in, fast). Google Sites is file ke liye kaam nahi karega —
Google Sites mein poora custom HTML upload nahi hota, sirf embed kar sakte ho, aur `index.html`
aisa ka taisa nahi chalega.

**Ek baar ka setup:**

1. `https://console.firebase.google.com` → **Create a project** → naam do → Analytics skip kar
   sakte ho → project ban jayega.
2. Apne laptop par **Node.js** install karo: `https://nodejs.org` (LTS version).
3. Terminal / Command Prompt kholo aur ye chalao:

```bash
npm install -g firebase-tools
firebase login          # browser khulega, apna Google account se login karo
cd path/to/ebook-site   # jahan index.html hai
firebase init hosting
```

`firebase init` ke sawaalon ke jawab:

| Sawaal | Jawab |
|---|---|
| Use an existing project? | Haan, apna project chuno |
| What do you want to use as your public directory? | `.` (sirf ek dot — kyunki index.html isi folder mein hai) |
| Configure as a single-page app (rewrite all urls to /index.html)? | **No** |
| Set up automatic builds with GitHub? | No |
| File index.html already exists. Overwrite? | **No** (haan kar diya to aapki site mit jayegi) |

4. Deploy:

```bash
firebase deploy
```

Aapko link milega: `https://aapka-project.web.app` — bas live hai.

**Update karna:** file edit karo, phir `firebase deploy` dobara. Apna domain: Firebase console →
Hosting → **Add custom domain** → jo record bataye wo DNS mein daal do.

Free (Spark) plan mein 10 GB storage aur 360 MB/day transfer milta hai — ek ebook landing page ke
liye kaafi se zyada.

---

## 5c. Google search mein laana (Search Console) — ye asli "Google par daalna" hai

Site live hone ka matlab ye nahi ki wo Google par dikhegi. Google ko batana padta hai. Iska
official tool hai **Google Search Console** — free.

### Step 1 — Property add karo

1. `https://search.google.com/search-console` kholo, apne Google account se login karo.
2. **Add property** → do options aayenge:
   - **Domain** (`thecalmedge.in`) — poore domain ke liye, http/https/www sab cover. Verify karne
     ka sirf ek tarika hai: **DNS TXT record** (domain provider ke panel mein).
   - **URL-prefix** (`https://thecalmedge.in/`) — sirf wahi URL. Verify karne ke 4 tarike:
     HTML tag, HTML file upload, Google Analytics, Google Tag Manager.
3. Agar aapke paas domain hai to **Domain** chuno (best). Agar abhi `username.github.io/ebook-site`
   ya `xyz.netlify.app` par ho to **URL-prefix** chuno — usme DNS ki zaroorat nahi.

### Step 2 — Verify karo (sabse aasan tarika: HTML tag)

1. HTML tag method chuno. Google ek line dega:
   `<meta name="google-site-verification" content="AbCdEf123..." />`
2. `index.html` kholo — head section mein maine iske liye jagah banayi hui hai. Search karo:
   `GOOGLE SEARCH CONSOLE VERIFICATION`
3. Us comment ke neeche Google ka tag paste kar do, save karo, aur site par upload/push kar do.
4. Search Console mein wapas jaake **Verify** dabao. Ho gaya.

DNS method mein: domain provider (GoDaddy/Hostinger/Cloudflare) ke DNS panel mein **TXT** record
banao — name `@`, value jo Google ne diya (`google-site-verification=...`). 10 minute se 48 ghante
tak lag sakte hain.

### Step 3 — Sitemap submit karo

1. `sitemap.xml` file project mein already hai. Usme `https://yourdomain.com/` ko apne asli URL se
   replace karo. (`robots.txt` mein bhi `Sitemap:` wali line ko uncomment karo.)
2. Search Console → left menu **Indexing → Sitemaps** → `sitemap.xml` likho → **Submit**.
3. Status "Success" dikhna chahiye. Yahi Google ko batata hai ki site par kaunse page hain.

### Step 4 — Indexing request karo (fastest nudge)

1. Search Console ke top search bar (**URL Inspection**) mein apna poora URL daalo.
2. Live test chalne do → **Request Indexing** dabao.
3. Ye ek queue hai — turant nahi hota. Din ya hafte lag sakte hain, aur request karne se
   guarantee nahi milti.

### Step 5 — Check karo

Google par search karo: `site:yourdomain.com` — agar aapka page dikh gaya, matlab index ho gaya.
Search Console ke **Performance** tab mein 2-3 din baad data aana shuru hota hai.

### Kitna time lagta hai (honestly)

Naya site: **3 din se 3 hafte** typical hai. Bohot naye ya kam content wale page kabhi-kabhi
mahina bhi le lete hain. Google khud kehta hai ki baar-baar request karne se jaldi nahi hota.

### "Discovered / Crawled — currently not indexed" ka matlab

- **Discovered, not indexed** — Google ko URL pata hai, crawl queue mein hai. Intezaar karo.
- **Crawled, not indexed** — Google ne page padha par index karne layak nahi samjha. Aam taur par
  isliye hota hai ki content patla (thin) hai ya kisi doosre page se duplicate hai. Is case mein
  asli content, asli chapters, asli reviews add karna hi asli fix hai.

### Rank karne ke liye 5 practical cheezein

1. **Title aur description** — `index.html` ke head mein `<title>` aur `<meta name="description">`
   apne asli book ke hisaab se badlo. Google yahi dikhata hai.
2. **Asli content** — placeholder reviews hata do, apne chapters, sample, author bio likho. Google
   thin/duplicate pages ko index nahi karta.
3. **Backlinks** — link ko Instagram bio, LinkedIn, WhatsApp status, Medium, Quora, Reddit par
   share karo. Doosri sites se aane wale links ranking mein sabse zyada farak daalte hain.
4. **Speed + mobile** — ye site already fast aur mobile-ready hai (ek hi file, koi bhaari library
   nahi). Bas images bhaari na daalo.
5. **Har hafte ek chhota update** — naya chapter page, blog post ya FAQ add karte raho. Google
   active sites ko zyada crawl karta hai.

### Ye galtiyan mat karna

- `<meta name="robots" content="noindex">` galti se mat chhod dena — isse page kabhi index nahi hoga.
- `robots.txt` mein `Disallow: /` mat chhod dena (staging se copy hone par aam galti hai).
- Ek hi site ko teen URL par live mat rakho (`www` aur non-`www`, `http` aur `https`) — ek chuno,
  baaki redirect karo.
- Sitemap mein galat/404 URL mat daalo.

### Google ke aur free tools

- **Google Analytics 4** — kitne log aaye, kahan se. Code `index.html` ke head mein comment
  ke roop mein rakha hai, bas `G-XXXXXXXXXX` badal ke uncomment kar do.
- **PageSpeed Insights** (`https://pagespeed.web.dev`) — speed score.
- **Rich Results Test** — structured data check.
- **Google Business Profile** — ebook business ke liye zaroori nahi, sirf local shop/house business
  ke liye useful hai.

---

## 6. Apna domain lagana (jaise `thecalmedge.in`)

1. Domain kharido — GoDaddy, Namecheap, Hostinger, ya Cloudflare Registrar (~₹700-1200/saal `.in`).
2. **GitHub Pages** ke liye:
   - Repo → Settings → Pages → **Custom domain** mein `www.yourdomain.com` likho → Save
   - Domain provider ke DNS panel mein:
     - **CNAME** record: name `www` → value `YOUR-USERNAME.github.io`
     - **A** records (root/apex ke liye, 4 add karo): `185.199.108.153`, `185.199.109.153`,
       `185.199.110.153`, `185.199.111.153`
   - DNS propagate hone mein 10 minute se 24 ghante lag sakte hain.
   - Uske baad Pages settings mein **Enforce HTTPS** tick kar do (free SSL).
3. **Netlify** ke liye: Site settings → Domain management → Add domain → wahi CNAME ya nameservers
   jo Netlify batayega.

---

## 7. Editing guide — kya kahan badalna hai

`index.html` ko kisi bhi text editor (VS Code, Notepad++, ya even Notepad) mein kholo.
File mein bade comment markers hain — jaise `<!-- ================= HERO ================= -->`.
Ctrl+F se in markers ko search karke seedha us section par pahunch jao.

| Kya badalna hai | Kahan | Kaise |
|---|---|---|
| Book ka naam, author ka naam | poore file mein `The Calm Edge`, `Devika Mehta` | Ctrl+H (find & replace) se sab jagah ek saath badlo |
| Colours | CSS ka `1. THEME TOKENS` block (file ke shuru mein) | `--gold`, `--bg`, `--text` ki values badlo — poori site follow karegi |
| Fonts | `<head>` ka Google Fonts `<link>` + `--font-display` / `--font-body` | fonts.google.com se naya font chuno, link replace karo |
| Hero headline | `<!-- HERO -->` section ka `<h1>` | `<span>` lines badlo |
| 3D book ka size / angle | script mein `const W = 2.62, H = 3.62, PAGES_D = 0.34` aur `group.rotation.set(...)` | numbers se experiment karo |
| 3D book ka cover art | script ka `makeCoverTexture()` function | usme title, subtitle, author ka text aur colours change karo |
| 3D book ka ghumne ki speed | `targetY += 0.0035;` (jitna bada, utna tez) | |
| 3D zoom ki limit | `const ZOOM_MIN = 0.68, ZOOM_MAX = 1.85;` | chhota number = zyada door, bada = zyada paas |
| 3D ka default angle | `resetView()` ke andar `targetY = -0.55, targetX = 0.06` | yahan se shuruaati angle set hota hai |
| Library ki books | `<!-- LIBRARY / OTHER BOOKS -->` section | neeche "Naya book add karna" dekho |
| Search ke categories (chips) | `<div class="chips">` | naya `<button class="chip" data-cat="poetry">Poetry</button>` add karo, aur us book ke card mein `data-cat="poetry"` daalo |
| Hero ke chhote covers | `<div class="mini-shelf">` | har `.mini-book` par `data-jump="Book ka poora naam"` — click par library mein wahi search chal jayegi |
| Chapters ke cards | `<!-- CHAPTERS -->` section | ek `<article class="chapter">` copy karke paste karo, naya chapter add ho jayega |
| Pricing / daam | `<!-- PRICING -->` section | `₹399` text aur `data-buy="..."` dono badlo |
| Reviews | `<!-- REVIEWS -->` section | naam, text, initials (`AK` wala span) badlo |
| FAQ | `<!-- FAQ -->` section | ek `<details class="qa">` copy karke naya sawaal add karo |
| Free sample chapter ka text | `<!-- READER MODAL -->` section, `id="readerText"` | paragraphs badlo |
| Author card | `<!-- AUTHOR -->` section | `DM` initials, naam, bio |
| Nav ke links | `<nav class="nav__links">` | |
| Browser tab ka title + Google result | `<head>` ka `<title>` aur `<meta name="description">` | |
| Share karne par dikhne wala preview | `<meta property="og:title">`, `og:description` | |
| Favicon (tab ka chhota icon) | `<head>` mein add karo: `<link rel="icon" href="favicon.png">` | 32×32 ya 180×180 PNG `favicon.png` naam se folder mein rakho |
| Photo lagana | koi bhi jagah `<div class="author__avatar">DM</div>` ko replace karo: `<img src="author.jpg" alt="Devika Mehta" style="width:118px;height:118px;border-radius:50%;object-fit:cover">` | image file folder mein rakho, naam match kare |

### Naya book library mein add karna

`<!-- LIBRARY / OTHER BOOKS -->` section mein koi bhi mojooda `<article class="book-card reveal" ...>` poora copy
karke uske neeche paste kar do, phir 6 cheezein badlo:

```html
<article class="book-card reveal" data-cat="money" data-search="book ka naam author ka naam money savings investing">
  <div class="book-card__stage">
    <div class="book-card__cover" style="--c1:#243a52;--c2:#0f1a26;--acc:#9dc0e0">
      <span class="book-card__edge"></span>
      <div class="book-card__art"><small>Ebook</small><strong>Cover<br>Title</strong><em>Author Name</em></div>
    </div>
  </div>
  <div class="book-card__info">
    <h3>Poora Book Title</h3>
    <p class="book-card__meta">Author Name &middot; Money</p>
    <div class="book-card__foot"><span class="book-card__price">&#8377;399</span><span class="book-card__rate"><b>&#9733;</b>4.7</span></div>
  </div>
</article>
```

1. `data-cat` — category (focus / career / money / writing / health, ya apni nayi)
2. `data-search` — **search yahi text padhta hai**, isliye title, author aur 4-5 keywords zaroor daalo
3. `--c1`, `--c2`, `--acc` — cover ka gradient aur accent colour
4. Cover ka `<strong>` — chhota title (2 lines mein todo `<br>` se)
5. `<h3>` aur `.book-card__meta` — poora naam aur author
6. `₹` price aur `★` rating

Aur `id="shelfCount"` wala text ("8 titles") automatically update hota hai — usse haath se badalne ki zaroorat nahi.

**Bade text changes ke liye tip:** kisi bhi section ka text badalne se pehle us section ko poora
select karke ek baar padh lo — HTML tags (`<p>`, `</p>`) ko chhedna nahi hai, sirf beech ka text.

---

## 8. Asli paisa kaise aayega (payments)

Abhi "Buy" buttons demo hain — click karne par toast message dikhta hai. Asli payment ke liye 3
options hain. **India ke liye Razorpay sabse aasan hai** (UPI, cards, netbanking, wallets).

### Option A — Razorpay Payment Link (sabse simple, koi coding nahi)

1. `https://razorpay.com` par business account banao (KYC: PAN, bank details, ~1-2 din).
2. Dashboard → **Payment Links** → **Create Payment Link**
   - Amount: 399, Description: "The Calm Edge — Ebook"
   - Customer ko name/email/phone maango (tick karo)
   - **Success message** mein apna download link daal do (Google Drive ka PDF link, "anyone with
     the link" access) — ya email se bhejo
3. Link copy karo, jaise `https://rzp.io/l/calmedge399`
4. `index.html` mein Ctrl+F se search karo: `buy buttons (demo checkout)`
   Aur us block ko is se replace kar do:

```js
/* ---- buy buttons ---- */
$$('[data-buy]').forEach(btn => {
  btn.addEventListener('click', () => {
    const plan = btn.getAttribute('data-buy') || '';
    let url = 'https://rzp.io/l/calmedge399';          // Ebook only
    if (plan.includes('workbook')) url = 'https://rzp.io/l/calmedge699';
    if (plan.includes('Team'))     url = 'https://rzp.io/l/calmedge2499';
    window.location.href = url;
  });
});
```

Har plan ka apna Payment Link banao aur upar wale URLs replace kar do. Bas — paisa aana shuru.

### Option B — Instamojo / Cashfree / PayU

Wahi tarika: payment link banao, upar wale code mein URL badal do. Cashfree aur Instamojo India
mein popular hain, international ke liye **Gumroad** ya **Lemon Squeezy** behtar hai (wo file
delivery aur tax khud handle karte hain, aapko kuch nahi karna).

### Option C — Gumroad (sabse kam jhanjhat, global)

`https://gumroad.com` par product banao → PDF upload karo → price 399 → publish. Gumroad khud
payment, delivery aur receipts sambhal lega. Aapka kaam sirf link ko apne button se jodna hai.

> Delivery tip: bade PDF ke liye Google Drive link use karo (share → "Anyone with the link →
> Viewer"). Ya Gumroad/Instamojo se seedha file attach kar do — zyada safe.

---

## 9. Free chapter email se bhejna

Newsletter form abhi demo hai (thanks message dikhata hai, kahin save nahi karta). 3 easy options:

**A. Google Forms + Sheets (bilkul free, 5 minute)**
1. `https://forms.google.com` → naya form → ek "Email" field → Settings → Responses →
   "Collect email addresses" on
2. Form ka link le lo, aur `index.html` mein `<!-- CTA / NEWSLETTER -->` section mein
   `<form class="subscribe">` ko replace karo:
   `<a class="btn btn--gold" href="https://forms.gle/YOUR-FORM-LINK" target="_blank">Send it</a>`
3. Form ke "Confirmation message" mein free chapter ka Google Drive link daal do.

**B. Formspree** — `https://formspree.io` par form banao, aur `<form>` tag mein
`action="https://formspree.io/f/YOUR-ID" method="POST"` add kar do. Email par submissions aayengi.

**C. Mailchimp / Buttondown** — asli newsletter chahiye to inka embedded form code paste kar do.

---

## 10. Analytics aur SEO (optional, par worth it)

**Google Analytics 4:** `https://analytics.google.com` se Measurement ID (`G-XXXXXXX`) lo, aur
`</head>` se just pehle ye paste karo:

```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXX');
</script>
```

**Search mein aane ke liye:** `robots.txt` naam ki file banao jisme sirf ye likho:

```
User-agent: *
Allow: /
```

Aur `sitemap.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url><loc>https://yourdomain.com/</loc></url>
</urlset>
```

Phir Google Search Console (`https://search.google.com/search-console`) mein site add karke
sitemap submit kar do.

---

## 11. Common problems

| Problem | Solution |
|---|---|
| 404 page dikh raha hai | File ka naam exactly `index.html` hona chahiye (capital `I` nahi). GitHub Pages case-sensitive hai. |
| Push ke baad site update nahi hui | 1-2 min ruko, phir Ctrl+Shift+R (hard refresh). Repo ke **Actions** tab mein deploy status dekho. |
| 3D book nahi dikh raha | Internet check karo (Three.js CDN chahiye). Block ho to CSS fallback khud dikh jayega — ye design ka hissa hai, error nahi. |
| Fonts alag lag rahe hain | Google Fonts load nahi hue. Internet ya ad-blocker check karo. |
| Mobile par text chhota/bada lag raha hai | `<meta name="viewport">` line ko delete mat karna. |
| Custom domain kaam nahi kar raha | DNS ko 24 ghante tak time do; `www` ke liye CNAME, root ke liye 4 A records check karo. |
| Changes dikh nahi rahe | Browser cache. Ctrl+Shift+R, ya incognito mein kholo. |

---

## 12. Launch se pehle checklist

- [ ] Book ka naam, author ka naam, saare `₹` prices badle
- [ ] Sample chapter ka text apna hai (doosre ki copy nahi)
- [ ] Reviews asli hain ya hata diye (jhoothe reviews trust todte hain — aur India mein
      consumer law ke hisaab se risky bhi)
- [ ] Razorpay/Gumroad link jod diya, ek test payment kiya
- [ ] Download link test kiya — kisi doosre phone se bhi khol ke dekho
- [ ] Terms, Privacy, Refund links par asli page ya text hai
- [ ] `og:title` / `og:description` sahi hai (WhatsApp par link bhej ke preview dekho)
- [ ] Mobile par poora scroll karke dekha
- [ ] Favicon laga diya
- [ ] Apna email/contact hero ya footer mein visible hai

---

## 13. Seekhne ke resources (free)

**Official docs (sabse bharosemand)**
- GitHub Pages: `https://docs.github.com/en/pages`
- Netlify Drop: `https://app.netlify.com/drop`
- Three.js docs + examples: `https://threejs.org/docs` aur `https://threejs.org/examples`
- Web Dev (Google) — CSS aur performance ke free courses: `https://web.dev/learn`
- MDN HTML/CSS reference: `https://developer.mozilla.org`

**YouTube (naam search karo, channel ke playlists dekho)**
- Hindi mein: **CodeWithHarry**, **Hitesh Choudhary (Chai aur Code)** — HTML/CSS/JS basics + git
- English mein: **Kevin Powell** (CSS/layout ke best explanations), **Web Dev Simplified**,
  **Traversy Media**, **Fireship** (chhote quick concepts)
- Three.js ke liye search karo: *"three.js book 3d tutorial"* — **SimonDev** aur
  **Bruno Simon** ke videos sabse acche hain

**Inspiration aur design**
- `https://fonts.google.com` — free fonts (pairing ke liye)
- `https://coolors.co` — colour palettes
- `https://dribbble.com` — search "ebook landing page" / "book website"
- GitHub par search karo: `three.js book`, `ebook landing page` — ready-made repos milenge

**Git seekhne ke liye (agar naya hai)**
- `https://learngitbranching.js.org` — visual, interactive, free
- GitHub ka apna guide: `https://docs.github.com/en/get-started`

---

## 14. Aage kya add kar sakte ho

- **Multiple pages** — `about.html`, `blog.html` banao, `index.html` se copy karke nav same rakho
- **Real 3D page flip** — Three.js mein page-turn animation (three.js examples mein
  `webgl_animation_skinning` / "book" demos dekho)
- **Testimonials slider** — CSS scroll-snap se 20 line mein ban jata hai
- **Urdu/Hindi version** — `index-urdu.html` banao, `dir="rtl"` attribute lagao
- **Print-friendly chapter PDF** — browser ke "Print → Save as PDF" se seedha ban jata hai
- **WhatsApp order button** — `https://wa.me/91XXXXXXXXXX?text=Hi%2C%20mujhe%20ebook%20chahiye`

Kuch bhi atke to file ka wahi section bhej dena — usi ko fix kar denge.

---

*Ye template aapka hai. Ismein koi tracking, koi lock-in, koi subscription nahi.*
