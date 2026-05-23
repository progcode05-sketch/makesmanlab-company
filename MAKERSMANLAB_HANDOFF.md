# Makersmanlab.com — Website Handoff

> Company website for **makersmanlab.com** — a single-page static site showcasing Noxlin and Linkora as products.

---

## Overview

| Item | Detail |
|---|---|
| Domain | `makersmanlab.com` + `www.makersmanlab.com` |
| Type | Static single-page website (pure HTML/CSS/JS — no framework, no build step) |
| File | `public/company.html` (single self-contained file) |
| Hosting | Vercel (free static hosting) |
| DNS | GoDaddy |

---

## File Structure

The entire website lives in **one file**:

```
company.html        ← entire website (HTML + CSS + JS, self-contained)
```

No dependencies. No npm. No build process. Open the file in a browser and it works.

---

## Design System

### Colors

| Token | Hex | Usage |
|---|---|---|
| `--blue` | `#0A66C2` | Primary accent, CTAs, links |
| `--blue-dark` | `#0856a8` | Button hover |
| `--blue-light` | `#e8f0fb` | Subtle backgrounds, icon fills |
| `--ink` | `#0a0a0b` | Primary text, headings |
| `--ink-2` | `#26262a` | Secondary text |
| `--ink-3` | `#5b5c63` | Body copy, descriptions |
| `--ink-4` | `#8e8f96` | Labels, meta text |
| `--surface` | `#ffffff` | Card backgrounds |
| `--bg` | `#f5f6f9` | Section backgrounds |
| `--line` | `#e4e6ec` | Borders, dividers |

### Typography

| Role | Font | Weight |
|---|---|---|
| Display / headings | Instrument Serif | 400 (regular + italic) |
| Body / UI | Inter | 400, 500, 600, 700 |

Loaded via Google Fonts — no local font files needed.

### Border Radius

| Token | Value | Usage |
|---|---|---|
| `--r` | `14px` | Cards, inputs |
| `--r-lg` | `20px` | Larger cards |
| `--r-xl` | `28px` | Hero cards, CTA sections |

---

## Page Sections

### 1. Navigation
- Sticky top nav with blur backdrop
- Logo: animated blue dot + "Makersmanlab"
- Links: Products, About, Contact (smooth scroll)
- CTA: "Explore products" → scrolls to #products

### 2. Hero
- Eyebrow badge: "2 products · 1 mission"
- H1: "Tools for people who take *LinkedIn seriously.*"
- Subtext: brand description
- Two CTAs: "See our products" + "Our story"

### 3. Stats Strip
- 4 stats: 2 products shipped / 1 founder / 0 VC funding / 100% LinkedIn focused

### 4. Products Section (`#products`)
- Two cards side by side (Noxlin + Linkora)
- Each card: number, icon, name, tagline, description, 3 feature bullets, CTA button
- Cards link to their subdomains in a new tab

### 5. About / Story (`#about`)
- Two-column layout: avatar card (left) + story text (right)
- Founder narrative: solo builder, indie hacker
- Pull quote in italics
- Tag pills: Bootstrapped, No VC, Built in public, etc.

### 6. Contact (`#contact`)
- Dark card with blue radial glow
- Email CTA → `progcode03@gmail.com`
- Quick links to both product sites

### 7. Footer
- Logo + product links + copyright

---

## Animations

- **Scroll reveal**: Elements fade up as they enter the viewport (IntersectionObserver)
- **Pulsing dot**: Blue dot in nav logo and hero eyebrow pulses gently
- **Button hover**: Subtle lift (`translateY(-1px)`) + shadow on all buttons

---

## Customisable Fields

Search for these strings in `company.html` to update them:

| What | Search for | Current value |
|---|---|---|
| Contact email | `progcode03@gmail.com` | Update to your email |
| Founder name / avatar | `about-avatar` | Shows "M" — replace with `<img>` for real photo |
| About story text | `about-body` | Edit the 2 paragraphs |
| Pull quote | `about-quote` | Update the quote text |
| Noxlin URL | `noxlin.makersmanlab.com` | Update if subdomain changes |
| Linkora URL | `linkora.makersmanlab.com` | Update if subdomain changes |
| Stats | `stat-n` | Update numbers as product grows |
| Copyright year | `© 2026` | Update annually |

---

## How to Add a Real Photo (About Section)

Find this in `company.html`:
```html
<div class="about-avatar">M</div>
```

Replace with:
```html
<img src="your-photo.jpg" class="about-avatar" style="object-fit:cover;" alt="Founder" />
```

Upload `your-photo.jpg` to the same folder as `company.html`.

---

## How to Add a New Product Card

Copy one of the existing product cards in the `products-grid` div and update:
- `product-num` → "Product 03"
- `product-icon` class → `blue` or `dark`
- `product-name` → new product name
- `product-tagline` → one-line description
- `product-desc` → 2–3 sentence description
- `product-features` → 3 bullet points
- `product-link` href → new product URL

---

## Deployment — Separate Vercel Project

### Step 1 — Create new GitHub repo

Create a new repo (e.g. `makersmanlab-website`) and add just one file:
```
index.html    ← rename company.html to index.html for this repo
```

### Step 2 — Deploy on Vercel

1. Go to **vercel.com/new**
2. Import the new GitHub repo
3. Framework preset: **Other** (it's static HTML, no framework)
4. Leave all build settings blank → click **Deploy**

### Step 3 — Add custom domain

1. Vercel → project → **Settings → Domains**
2. Add `makersmanlab.com` → Save
3. Add `www.makersmanlab.com` → Save
4. Vercel will give you DNS records

### Step 4 — GoDaddy DNS

Go to **GoDaddy → DNS** for `makersmanlab.com` and add:

| Type | Name | Value |
|---|---|---|
| `A` | `@` | *(Vercel's IP — shown in Vercel dashboard)* |
| `CNAME` | `www` | `cname.vercel-dns.com` |
| `TXT` | `_vercel` | *(verification value from Vercel)* |

Wait 10–30 minutes → both domains show ✅ Valid Configuration in Vercel.

---

## Blog Section (Future)

The navigation has no blog link yet. To add a simple blog:

**Option A — Notion as CMS (easiest)**
- Write posts in Notion → embed via `notion.so/page-id`
- Add a `/blog` page that iframes your Notion workspace

**Option B — Static HTML pages**
- Create `blog.html`, `post-1.html`, etc. in the same repo
- Add a "Blog" link to the nav pointing to `blog.html`
- No CMS needed — edit HTML files directly

**Option C — Hashnode or Ghost (most powerful)**
- Set up a blog at `blog.makersmanlab.com`
- Add a CNAME in GoDaddy: `blog` → your Hashnode/Ghost domain
- Add "Blog" to nav pointing to `https://blog.makersmanlab.com`

---

## Checklist Before Going Live

- [ ] Update contact email in company.html
- [ ] Replace "M" avatar with real photo (optional)
- [ ] Review About section text — personalise it
- [ ] Verify both product links open correctly
- [ ] Test on mobile (responsive at 860px and 560px breakpoints)
- [ ] Add `www` CNAME in GoDaddy to fix SSL on www subdomain
- [ ] Submit `makersmanlab.com` to Google Search Console

---

## Tech Stack Summary

```
HTML5 + CSS3 (custom properties) + vanilla JS
Fonts:   Google Fonts (Instrument Serif + Inter)
Icons:   Inline SVG (no icon library)
Animations: CSS transitions + IntersectionObserver
Build:   None — open in browser or deploy as-is
```

No React. No npm. No bundler. One file — done.
