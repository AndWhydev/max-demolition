# Max Demolitions — Google Ads Landing Page

Single-page, single-file landing page built for Google Ads traffic. Two primary conversions: **phone call** (`tel:0416355632`) and **quote form**.

Built by All Webbed Up. Same single-file pattern as the Show Limousines site — no build step, no frameworks, no dependencies to install.

---

## What this is

- `index.html` — the entire landing page (HTML + CSS in `<style>` + JS in `<script>`)
- `vercel.json` — security headers + cache control
- `.gitignore` — standard

Mobile-first. Designed for paid search traffic where Quality Score and Lighthouse matter.

### Design system

- **Aesthetic**: industrial trade — asphalt black, hi-vis safety yellow (`#FFD60A`), safety orange accent (`#FF6B1A`)
- **Type**: Archivo Black (display) + Inter (body) + JetBrains Mono (utility labels)
- **Motion**: GSAP + ScrollTrigger + Lenis smooth scroll + SplitType hero animation
- **Effects**: split-text hero reveal, scroll-reveal sections, animated stat counters, magnetic primary CTAs, custom cursor (desktop only), hazard-tape decorative strips, grain overlay
- **Restraint**: motion is dialled back relative to a luxury/agency build — this is a conversion page, not a portfolio. Industrial confidence over flash.

---

## Deploy to Vercel

### Option A — via GitHub (recommended)

```bash
# From this folder
git init
git add .
git commit -m "Initial: Max Demolitions Google Ads LP"
git branch -M main
git remote add origin git@github.com:<your-org>/max-demolitions-lp.git
git push -u origin main
```

Then on Vercel:
1. **New Project** → import the GitHub repo
2. Framework preset: **Other** (it's static HTML)
3. Root directory: `./`
4. Build command: *(leave blank)*
5. Output directory: `./`
6. Deploy

Custom domain: connect `maxdemolitions.com.au` or a sub-domain like `quote.maxdemolitions.com.au` in Vercel → Settings → Domains.

### Option B — via Vercel CLI

```bash
npm i -g vercel
vercel        # follow prompts (link to your team, deploy preview)
vercel --prod # ship to production
```

---

## TODOs requiring real client data

These are flagged in the HTML with `TODO:` markers. Replace before going live or the page will display placeholder text.

### Client confirmation needed
- [ ] **ABN** — currently `TODO` in footer + Schema.org
- [ ] **SafeWork NSW Asbestos Licence number** — currently `TODO` in licence panel
- [ ] **NSW Demolition Licence number** — currently `TODO` in licence panel
- [x] **Phone** confirmed: `0416 355 632` (client-provided 2026-06-14)
- [ ] **Confirm email** is `info@maxhaulage.com.au` (extracted from live site)
- [ ] **Confirm $20M public liability** figure — currently used in trust strip + hero (live site only says "comprehensive public liability"). Adjust if different.
- [ ] **Confirm "12+ years operating"** stat — live site says "since 2013", which gives 12 years in 2026
- [ ] **Confirm "800+ demos completed"** stat — currently a confident placeholder. Replace with real client number if available, or soften to "Hundreds of Sydney demos completed"
- [ ] **Physical office address** for Schema.org `PostalAddress` (currently just Sydney/NSW)
- [ ] **Service area suburbs list** — the list under the map is regional groupings. Replace with specific suburb names if client wants suburb-level SEO (Bondi, Randwick, Marrickville, Parramatta, Chatswood, etc.)

### Tracking — must be added before launching ads
- [ ] **GA4 measurement ID** — uncomment and replace `G-XXXXXXX` in the `<head>`
- [ ] **Google Ads conversion ID + labels** — replace `AW-XXXXXXX/abc123` (call conversion) and `AW-XXXXXXX/xyz456` (form conversion) in the JS `trackCallConversion()` and `trackFormConversion()` functions

### Form endpoint — Formspree (wired, needs form ID)
The quote form already POSTs to Formspree. Before launching ads:

1. Sign up at https://formspree.io with `info@maxhaulage.com.au` as the receiving address.
2. Create a new form, copy the form ID (looks like `xqkrgldz`).
3. In `index.html`, find `FORMSPREE_ENDPOINT` (one occurrence near the bottom of the `<script>` block) and replace `YOUR_FORM_ID` with the real ID.
4. Submit one test entry from the live URL to confirm the email lands in the inbox (and check spam once so Formspree mail isn't filtered).

Form payload also sends `_subject` (so emails arrive with a useful subject line like *"New quote request — house-demolition (Bondi)"*) and `_source` (so we can tell hero form vs final-CTA form apart).

### Imagery — wired in
- [x] **Hero background** — `assets/hero.webp` (excavator mid-takedown, dust)
- [x] **Why-us "crew on site" photo** — `assets/crew-why.webp` (4:5 vertical, dusk worksite)
- [x] **Equipment section** — `assets/equipment-02.webp` (excavator + tip truck)
- [x] **Project gallery** — 6 cards drawing from `project-*.webp` assets
- [x] **Logo** — `assets/logo.webp` in topbar (on warm-white plate) + footer
- [ ] Optional: add a real `og-image.jpg` (1200×630px) for OG/Twitter cards — currently referenced as `/og-image.jpg`, file doesn't exist. The hero shot makes a great OG.

---

## Brand details extracted from the live site

Pulled from `https://maxdemolitions.com.au/` on build day:

| Item | Value | Source |
|------|-------|--------|
| Business name | Max Demolitions / Max Demolitions & Excavations | homepage |
| Phone | 0416 355 632 | client-confirmed |
| Email | info@maxhaulage.com.au | every page |
| Established | 2013 | About Us page |
| Ownership | Family-owned | About Us page |
| Service area | All Sydney metropolitan | every page |
| Asbestos licence | Class A and Class B | Asbestos Removal page |
| Insurance | Public liability + WorkCover (no specific figures given) | Demolition page |
| Services | Demolition, Bulk Excavation, Asbestos Removal, Shoring, Site Remediation, Truck Hire | Services nav |
| Fleet (mentioned) | Bogies, 10-wheelers, super dogs, quad dogs, excavators | Truck Hire page |
| Tone signals | "Fixed Pricing, No Blowouts", "Fast Start Times", "Daily Progress Photos" | homepage USPs |
| Reviews (named) | David T., Lisa W., Sumaya B. | homepage testimonials |

### Brand details NOT extractable from live site (all marked TODO):
- ABN, asbestos licence number, demolition licence number, physical office address, specific public liability cover figure, founder/owner name, specific suburbs covered, project count.

---

## Lighthouse / perf notes

- All motion libraries (`gsap`, `ScrollTrigger`, `Lenis`, `split-type`) load with `defer` so they don't block render.
- Fonts use `display=swap`.
- Inline SVG favicon avoids an extra HTTP request.
- No images currently — page weight is well under 200KB.
- When client photos are added, run them through the image-pipeline skill (WebP, 800w + 1600w, responsive `<picture>`) before deploying.
- Reduced-motion media query disables all GSAP animations for users who prefer it.

Target on initial deploy: Lighthouse 95+ performance, 100 accessibility, 100 SEO, 100 best practices.

---

## File map

```
max-demolitions/
├── index.html      # Everything: HTML + CSS + JS
├── vercel.json     # Security headers, cache control
├── .gitignore      # Standard
└── README.md       # This file
```

Built by All Webbed Up — andy@allwebbedup.com.au
