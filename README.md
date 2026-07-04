# Pushti Naturals — Website

Wellness rooted in tradition. A static, responsive website for Pushti Naturals — unpolished millets, millet vermicelli and stone-milled flour.

**Live domain:** https://pushtinaturalsliving.com/
**GitHub repo:** https://github.com/pushtinaturaliving-source/pushtinaturalsliving

---

## Folder structure

```
pushtinaturalsliving/
├── index.html          Home page
├── about.html           About / brand story
├── products.html        Product catalogue (millets, vermicelli, flour)
├── benefits.html        Educational content on millets
├── contact.html         Contact form + business details
├── css/
│   └── style.css        All site styling (design tokens at the top)
├── js/
│   └── main.js           Nav toggle, scroll reveal, contact form handling
├── assets/
│   └── logo.jpg          Brand logo (swap product photos in here too)
├── robots.txt
├── sitemap.xml
└── README.md
```

No build step, no framework, no dependencies — just plain HTML, CSS and JavaScript, so it runs anywhere and deploys instantly.

---

## Running the site locally

You can open `index.html` directly in a browser, but running a local server avoids issues with relative paths and lets you test properly:

**Option A — Python (already on most machines):**
```bash
cd pushtinaturalsliving
python3 -m http.server 8000
```
Then visit `http://localhost:8000`.

**Option B — Node.js:**
```bash
cd pushtinaturalsliving
npx serve .
```

---

## Pushing to GitHub

If you're starting fresh in this folder:

```bash
cd pushtinaturalsliving
git init
git add .
git commit -m "Initial commit: Pushti Naturals website"
git branch -M main
git remote add origin https://github.com/pushtinaturaliving-source/pushtinaturalsliving.git
git push -u origin main
```

If the repository already has commits and you're adding this code to it:

```bash
git clone https://github.com/pushtinaturaliving-source/pushtinaturalsliving.git
# copy these files into the cloned folder, then:
cd pushtinaturalsliving
git add .
git commit -m "Add website files"
git push
```

**Making changes later:**
```bash
git add .
git commit -m "Describe what changed"
git push
```

---

## Deploying with GitHub Pages

1. Push the code to GitHub (see above).
2. In the repository, go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Set **Branch** to `main` and folder to `/ (root)`, then **Save**.
5. GitHub will publish the site at `https://pushtinaturaliving-source.github.io/pushtinaturalsliving/` within a few minutes.

**Using your own domain (pushtinaturalsliving.com):**
1. Still in **Settings → Pages**, add `pushtinaturalsliving.com` under **Custom domain** and save — this creates a `CNAME` file in your repo automatically.
2. At your DNS provider (Cloudflare, per your registration records), add:
   - An `A` record for the root domain pointing to GitHub Pages' IPs (`185.199.108.153`, `.109.153`, `.110.153`, `.111.153`), or a `CNAME` record for `www` pointing to `pushtinaturaliving-source.github.io`.
3. Enable **Enforce HTTPS** once the DNS check passes.

Any static host works the same way (Netlify, Vercel, Cloudflare Pages) — just point it at this folder.

---

## Connecting the contact form

The form in `contact.html` currently validates input and shows a confirmation message, but it doesn't send anywhere yet — this is a static site with no backend. To make it functional, pick one:

- **Formspree** (fastest): create a form at formspree.io, then change the `<form>` tag to `<form id="contact-form" class="form" action="https://formspree.io/f/yourFormId" method="POST">` and remove/adjust the `preventDefault()` logic in `js/main.js`.
- **Netlify Forms**: if hosting on Netlify, add `data-netlify="true"` to the `<form>` tag and a hidden `form-name` input — no JavaScript changes needed.
- **EmailJS**: add the EmailJS script and call `emailjs.send()` inside the submit handler in `js/main.js`.

---

## Designing visuals in Canva

The site currently ships with clean, hand-drawn SVG icons in place of product photography, so there's nothing to license and everything is easy to swap out.

**1. Create product mockups in Canva**
- Start from a blank design sized **1200 × 900 px** (matches the 4:3 product card frame) for individual product shots, or **1600 × 1200 px** for hero/banner imagery.
- Use Canva's "Product Photo" or "Packaging Mockup" templates, or place your own millet/flour photography inside a Canva frame for consistent cropping.
- Keep the brand palette in mind: warm oat cream (`#F4E9D6`), rust (`#A24E23`) and moss olive (`#707A3E`) — sample these in Canva's color picker so mockups feel consistent with the site.

**2. Export in web-optimized formats**
- Use Canva's **Share → Download** menu.
- Choose **PNG** (if you need transparency) or **JPG** (smaller file size, fine for photography).
- Under **Compress file (reduce quality)**, keep it checked to keep page load fast.
- Aim for exports under ~300 KB per image where possible.

**3. Swap placeholders into the site**
- Save your exported files into `assets/` — for example `assets/finger-millet.jpg`.
- In the relevant HTML file, find the `.product-card__art` block for that product and replace the inline `<svg>...</svg>` with:
  ```html
  <img src="assets/finger-millet.jpg" alt="Finger millet grains" loading="lazy" />
  ```
- The `.product-card__art` container already handles sizing and rounded corners, so images will slot in without further CSS changes.
- Do the same for the hero (`.grain-ring`) and logo (`assets/logo.jpg`) if you design a refreshed version in Canva.

---

## SEO notes

- Each page has a unique `<title>`, meta description, canonical URL and Open Graph tags — update these if page content changes.
- `sitemap.xml` and `robots.txt` are included; update the sitemap if you add pages.
- All images should keep descriptive `alt` text as you add real photography.
