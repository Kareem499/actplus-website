# ACT Plus Digital Solutions — Project Documentation

## Project Overview

**Live URL:** https://actplusds.com  
**Repository:** https://github.com/Kareem499/actplus-website  
**Branch:** `main` → auto-deploys via GitHub Pages  
**Local dev server:** `python3 -m http.server 8888` from the project root  
**Local URL:** http://localhost:8888  

### Tech Stack
- Pure static HTML/CSS/JS — no build tools, no framework
- Hosted on GitHub Pages
- DNS and CDN via Cloudflare (DNS only mode — no proxying)
- Forms via Formspree
- Fonts via Google Fonts (Montserrat + Open Sans)
- Analytics via Google Tag Manager (`G-CXV0Z0S9R3`)

### Folder Structure
```
/
├── index.html          # Homepage
├── contact.html        # Contact + Book a Conversation
├── services.html       # Services
├── partners.html       # Partners & Ecosystem
├── about.html          # About
├── thanks.html         # Form success page
├── CNAME               # actplusds.com — DO NOT DELETE
├── main.css            # Shared styles (not currently used — styles are inline per page)
├── main.js             # Shared JS
├── lang.js             # Language toggle (stub)
├── sitemap.xml
├── robots.txt
└── assets/
    ├── act-logo.svg           # White logo (for dark backgrounds)
    ├── act-logo-dark.svg      # Dark logo (for nav/light backgrounds)
    ├── act-plus-logo.png      # OG/meta image
    ├── mark-navy.png          # Favicon
    └── clients/               # Client logo files (see section below)
```

---

## Access & Credentials

| Service | Access Holder | Email |
|---|---|---|
| GitHub repo | Kareem AlWazir | kareamelwazir@gmail.com |
| Cloudflare | Kareem AlWazir | kareem@ramlatech.com |
| GoDaddy (domain registrar) | Bassem AlWazir | bwazir@actplusds.com |
| Google Analytics | — | G-CXV0Z0S9R3 |
| Formspree (contact form) | — | endpoint: `xrerzepn` |
| Formspree (RFP form) | — | endpoint: `mjgjbgwk` |
| Booking calendar | — | https://calendar.app.google/iimx72oQiLnDs8EJ9 |

---

## DNS & Domain Configuration

### Registrar
Domain `actplusds.com` is registered at **GoDaddy** (Bassem AlWazir).  
Nameservers have been pointed to Cloudflare — GoDaddy is now registration-only.

### Cloudflare Setup
Nameservers are set to Cloudflare. DNS management happens in Cloudflare, not GoDaddy.

**Correct DNS records:**

| Type | Name | Value | Proxy |
|---|---|---|---|
| A | actplusds.com | 185.199.108.153 | DNS only (gray) |
| A | actplusds.com | 185.199.109.153 | DNS only (gray) |
| A | actplusds.com | 185.199.110.153 | DNS only (gray) |
| A | actplusds.com | 185.199.111.153 | DNS only (gray) |
| CNAME | www | kareem499.github.io | DNS only (gray) |
| TXT | _dmarc | "v=DMARC1; p=quarantine; ..." | DNS only |

**Records to delete if they reappear (GoDaddy leftovers):**
- A `15.197.148.33`
- A `3.33.130.190`
- CNAME `_domainconnect` → `_domainconnect.gd.domaincontrol.com`

**Critical:** All GitHub Pages A records and the `www` CNAME must be **DNS only (gray cloud)**. If proxied (orange), GitHub Pages cannot issue an SSL certificate and the site will show a blank page or SSL error.

### DNSSEC
DNSSEC is disabled on GoDaddy — correct, leave it disabled. Cloudflare DNSSEC can be enabled separately from Cloudflare dashboard → DNS → DNSSEC tab once fully propagated.

### GitHub Pages HTTPS Setup
If "Enforce HTTPS" is greyed out:
1. Confirm all A records are DNS only in Cloudflare
2. In GitHub repo → Settings → Pages → remove custom domain → Save
3. Wait 2 minutes
4. Re-add `actplusds.com` → Save
5. Wait 10–30 minutes for Let's Encrypt to issue the certificate
6. "Enforce HTTPS" checkbox will become available

---

## Design System

### CSS Variables
Defined inline in each page's `<style>` block:

```css
--deep-sea:    #003A55;   /* Primary brand — dark navy */
--deep-sea-2:  #00587d;   /* Secondary navy */
--majestic:    #177cac;
--trust:       #0097c0;
--innovate:    #6fd0f6;   /* Accent — light blue */
--midnight:    #0A1420;   /* Darkest — footer bg */

--ink:    #0A1420;        /* Body text */
--ink-2:  #2A3342;
--ink-3:  #6B7588;        /* Muted text */
--ink-4:  #A0A8B5;        /* Very muted */
--line:   #E8ECF1;        /* Borders */
--line-2: #D2D8E0;
--bg:     #FFFFFF;
--bg-2:   #F7F9FB;        /* Light grey sections */

--font-sans:    'Open Sans', system-ui, sans-serif;
--font-display: 'Montserrat', sans-serif;
--max-w:  1360px;
--gutter: 56px;           /* 24px on mobile */
```

### Typography Scale
```css
h1: clamp(44px, 5.5vw, 80px) — weight 400
h2: clamp(36px, 4vw, 60px)   — weight 400
h3: clamp(22px, 2vw, 30px)   — weight 600
h4: 17px                      — weight 600
body: 16px / 1.65
```

### Key Components

**Eyebrow label** — small uppercase label with a leading line, used above all section headings:
```html
<div class="eyebrow">Section Label</div>
```

**Buttons:**
```html
<a href="#" class="btn">Primary (navy)</a>
<a href="#" class="btn btn-light">Light (transparent, white border)</a>
<a href="#" class="btn btn-ghost">Ghost (transparent, dark border)</a>
```

**Sections** — all use `padding: 140px var(--gutter)` with a `.container` inside:
```html
<section>
  <div class="container">...</div>
</section>
```

### Hexagonal Decorative Accent
All page heroes use a large clipped hexagon shape positioned off the right edge. Text sits at `z-index: 2` above it, creating the "text flowing over hex" visual. Do not remove the `position: relative; z-index: 2` from hero content containers.

---

## Client Logos Carousel (index.html)

### Location in HTML
Section with class `.proof`, around line 704 in `index.html`.

### File Naming Convention
All logos live in `assets/clients/`. PNG format is standard:
```
1. Paltel.png
2. Jawwal.png
3. Reach.png
...
17. Zain-logo.png
18. itisaluna.png
etc.
```

### Current Logo List (20 logos)
1. Paltel
2. Jawwal
3. Reach
4. State of Palestine
5. PCBS
6. MTIT (Ministry of Telecom & IT)
7. Palestine Monetary Authority
8. The World Bank
9. Bank of Palestine
10. AlQuds Pharmaceuticals Group
11. GIZ
12. Munib & Angels Masri Foundation
13. BK Plus Europe
14. Zain
15. Itisaluna
16. Newroz Telecom
17. Pharmacare PLC
18. Sidata
19. Tech Trendy

**Omitted intentionally:** Fine Hygienic Holding, NFPC, Upliftt.

### Adding a New Logo
1. Place PNG in `assets/clients/`
2. Add a slot in the first half of `.proof-track`:
```html
<div class="proof-slot"><img src="assets/clients/YourLogo.png" alt="Logo Name"></div>
```
3. Add the identical slot in the second half (aria-hidden duplicate for the loop):
```html
<div class="proof-slot" aria-hidden="true"><img src="assets/clients/YourLogo.png" alt=""></div>
```
4. Adjust animation duration: `(total logos / 20) × 50s`

### CSS: Slot Sizing
```css
.proof-slot { width: 220px; height: 160px; border-right: 1px solid var(--line); }
.proof-slot img { max-height: 100px; max-width: 160px; object-fit: contain;
                  filter: grayscale(1) opacity(0.72); transition: filter 350ms ease; }
.proof-slot:hover img { filter: grayscale(0) opacity(1); }
```

### Per-Logo Scale Overrides
Logos with excessive whitespace in their image file use `transform: scale()` inline to fill the slot:

| Logo | Scale |
|---|---|
| MTIT | 1.3 |
| Palestine Monetary Authority | 1.3 |
| AlQuds Pharmaceuticals | 1.15 |
| Munib & Masri Foundation | 1.2 |
| Itisaluna | 1.55 |
| Newroz Telecom | 1.2 |
| Pharmacare PLC | 1.74 |
| Sidata | 1.35 |

---

## Page-by-Page Reference

### index.html — Homepage

| Section | ID / Class | Notes |
|---|---|---|
| Nav | `.nav` | Fixed, scrolled class added via JS |
| Hero | `.hero` | Full viewport, deep-sea bg, hex accent |
| Client logos | `.proof` | Infinite scroll carousel |
| Intro / Who we are | `#intro` | Sticky eyebrow column |
| Mandate statement | `.mandate` | Dark navy, gradient text headline |
| Pillars | `#pillars` | 3-column hover cards |
| Capabilities table | `#caps` | Expandable rows |
| Outcomes / ROI | `.outcome` | |
| Industries | `#industries` | |
| SOC / Security | `#soc` | |
| Footprint | `#footprint` | Regional presence |
| Quote | `.quote` | Clientele principle |
| Tech Trendy CSR | `.tt-csr` | Before CTA — see below |
| CTA / Contact | `#contact` | |
| Footer | `.footer` | |

### contact.html — Contact & Booking

**Formspree endpoints:**
- Contact form: `https://formspree.io/f/xrerzepn`
- RFP form: `https://formspree.io/f/mjgjbgwk`

**Booking calendar:** `https://calendar.app.google/iimx72oQiLnDs8EJ9`

| Section | ID | Notes |
|---|---|---|
| Hero | `.page-hero` | "Clarity before commitment" |
| Logo carousel | `.proof` | Same PNG set as homepage |
| Executive Briefing | `#book` | Links to Google Calendar |
| Contact form | `#contact` | Formspree `xrerzepn` |
| RFP submission | `#rfp` | Formspree `mjgjbgwk` |
| FAQ accordion | — | JS-powered, 6 questions |
| Location strip | `.location-strip` | Dark midnight bg |

---

## Tech Trendy CSR Section

**Placement:** `index.html`, immediately before `<!-- CTA -->` section.  
**Class:** `.tt-csr`  
**Background:** `var(--deep-sea)` navy — visually distinct from surrounding sections.

### Key Content Facts
- Non-profit initiative founded by **Bassem Al-Wazir**, Chairman of ACT Plus Digital Solutions
- Founded 2020 during COVID-19 pandemic
- Based in Lebanon, active in Jordan, Syria, Palestine, UAE, Saudi Arabia
- Free membership model
- Website: https://techtrendy.org/
- Logo file: `assets/clients/22. Tech Trendy.png`

### To Update Content
Edit the `.tt-csr` section in `index.html`. Stats are in `.tt-stats` — 4 cells in a 2×2 grid. CTA button links to `https://techtrendy.org/`.

---

## Content & Tone Guidelines

### Enterprise Tone — Do
- Address CIOs, CTOs, transformation leads directly
- Use words like: *programme, engagement, mobilise, structured, accountable, principal*
- Quantify value: timelines, countries, engagement counts
- Position ACT Plus as a peer to enterprise clients, not a vendor

### Enterprise Tone — Do Not
- "No sales pressure, no obligation" — removes confidence, not enterprise language
- "Claim your free consultation" — transactional
- "Palestinian heritage" as a selling point or identity marker
- Reference Gaza in any context
- Use flag emojis in professional sections
- Placeholder names like "Ahmad" or "Hassan" in forms

### Office References
- Correct: *"Regional HQ: Ramallah — offices across the MENA region"*
- Correct: *"Ramallah · Amman · Baghdad · Erbil · Dubai · Riyadh · Toronto"*
- Avoid: *"From Ramallah, Palestine — to the world"*

---

## Git & Deployment Workflow

### Deploying Changes
```bash
git add [specific files]
git commit -m "type: description"
git push
```
GitHub Pages auto-deploys from `main` within ~2 minutes.

### Important: CNAME File
The file `CNAME` at the root contains `actplusds.com`. **Never delete this file.** It tells GitHub Pages to serve the site on the custom domain. If it disappears (e.g. after a reset), re-create it with just `actplusds.com` as its content.

### Commit Convention
```
feat:   new feature or section
fix:    bug fix
chore:  maintenance, file cleanup
seo:    meta, structured data, sitemap changes
style:  visual/CSS changes only
```

---

## Arabization Roadmap

### Approved Architecture
Separate `/ar/` folder with full Arabic HTML files — not JS-based content swapping. Ensures full SEO indexing of Arabic content.

```
/ar/
  index.html
  contact.html
  services.html
  partners.html
  about.html
```

### Implementation Plan

**Step 1 — RTL CSS**  
Add `dir="rtl" lang="ar"` to `<html>` on all Arabic pages.  
Create `assets/rtl.css` with layout overrides:
- Flex row directions reverse
- Margins/paddings mirror (use CSS logical properties where possible)
- Eyebrow line moves to right of text
- Hero hex accent moves to left side
- Nav logo right-aligned, links left-aligned

**Step 2 — Arabic Fonts**  
Add to Google Fonts import on Arabic pages:
```css
--font-sans:    'IBM Plex Arabic', sans-serif;
--font-display: 'Almarai', sans-serif;
```
Both are free, enterprise-appropriate, and support the full Arabic character set.

**Step 3 — Language Switcher**  
Add to nav on all pages:
```html
<a href="/ar/index.html" class="lang-toggle">ع</a>   <!-- on English pages -->
<a href="/index.html" class="lang-toggle">EN</a>      <!-- on Arabic pages -->
```

**Step 4 — hreflang SEO Tags**  
Add to `<head>` on every page pair:
```html
<!-- English pages -->
<link rel="alternate" hreflang="en" href="https://actplusds.com/index.html" />
<link rel="alternate" hreflang="ar" href="https://actplusds.com/ar/index.html" />

<!-- Arabic pages -->
<link rel="alternate" hreflang="ar" href="https://actplusds.com/ar/index.html" />
<link rel="alternate" hreflang="en" href="https://actplusds.com/index.html" />
```

**Step 5 — Content Translation**  
Priority order:
1. `index.html` (homepage)
2. `contact.html`
3. `services.html`
4. `partners.html`
5. `about.html`

### What Stays Shared
- All image assets and client logos
- Formspree endpoints (forms submit to same destination)
- Google Analytics tag
- Favicon and brand assets
- JavaScript (nav scroll, FAQ accordion, form success handling)

---

## Favicon & Search Appearance

The favicon (browser tab icon) is set via:
```html
<link rel="icon" type="image/png" href="assets/mark-navy.png" />
```
This also appears next to the URL in Google search results.  
File: `assets/mark-navy.png` — the navy ACT Plus mark.  
Ensure this tag is present in the `<head>` of every page.
