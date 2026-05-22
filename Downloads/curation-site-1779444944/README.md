# Curation Media — Website

The marketing website for [Curation Media](https://curationmedia.net) — a supply-side platform specializing in curating premium, high-performing ad inventory.

Built as a static HTML/CSS site with no build step. Designed for deployment to GitHub Pages, Netlify, Vercel, or any static host.

---

## Pages

| Page | File | URL path |
|------|------|----------|
| Homepage | `index.html` | `/` |
| For Advertisers | `advertisers.html` | `/advertisers/` |
| For Publishers (Refresh Detect™) | `publishers.html` | `/publishers/` or `/refresh-detect/` |
| About | `about.html` | `/about/` |
| Patent Information | `patent.html` | `/patent-information/` |
| Contact | `contact.html` | `/contact/` |
| Privacy Policy | `privacy-policy.html` | `/privacy-policy/` |
| Terms of Service | `terms.html` | `/terms/` |

The shared stylesheet `shared.css` is loaded by all pages except `index.html` (which has its own inline styles).

---

## Design system

- **Typography:** Fraunces (display serif), Inter Tight (body sans), JetBrains Mono (technical metadata) — all loaded from Google Fonts
- **Palette:** Warm paper (`#F4F0E8`) over deep ink (`#0E1410`), with brand green (`#2DBE6C`) and rust accent (`#C7491F`)
- **Layout:** Editorial grids, asymmetric compositions, custom SVG data visualizations
- **No frameworks:** Vanilla HTML/CSS with minimal JavaScript only where interaction is required

---

## Contact form

The contact form on `/contact/` posts to Formspree:

```
https://formspree.io/f/xredkgpa
```

Submissions are handled via AJAX (fetch with `Accept: application/json`) for a no-redirect UX with inline success/error states. A `_gotcha` honeypot field is included for spam protection.

To change the form endpoint, edit the `action` attribute on `<form id="contactForm">` in `contact.html`.

---

## Deployment

### GitHub Pages

1. Push to the `main` branch
2. In repo Settings → Pages, set source to `main` / `(root)`
3. Add a `CNAME` file with `curationmedia.net` (already in repo)
4. Point DNS at GitHub Pages:
   - `A` records for apex domain pointing to GitHub Pages IPs (185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153)
   - or `CNAME` record for `www` subdomain pointing to `curationmedia1.github.io`

### Other static hosts

The site is fully static. Drop all `.html` and `.css` files into the deploy target — no build step required. Works on Netlify, Vercel, Cloudflare Pages, S3, etc.

---

## Local development

No build tools needed. Just open `index.html` in a browser, or run a simple local server:

```bash
# Python 3
python3 -m http.server 8000

# Node
npx serve .
```

Then open `http://localhost:8000`.

---

## File structure

```
.
├── index.html              # Homepage
├── advertisers.html        # For Advertisers
├── publishers.html         # For Publishers / Refresh Detect™
├── about.html              # About / company history
├── patent.html             # Patent information
├── contact.html            # Contact form (Formspree)
├── privacy-policy.html     # Privacy Policy
├── terms.html              # Terms of Service
├── shared.css              # Shared design system stylesheet
├── CNAME                   # Custom domain for GitHub Pages
├── .gitignore
└── README.md
```

---

## Editing content

All pages are hand-written HTML — content lives directly inside each `.html` file. To update copy:

1. Open the page file in any editor
2. Find the relevant `<h1>`, `<p>`, `<li>`, etc.
3. Edit the text
4. Commit and push

For repeated elements (nav, footer), update each file individually — there is no template engine. If you'd prefer a build step with partials, see "Future considerations" below.

---

## Future considerations

- **Sitemap:** A `sitemap.xml` and `robots.txt` should be added for SEO before launch
- **Analytics:** Drop in Google Analytics, Plausible, or Fathom tag in the `<head>` of each page (or factor into a shared snippet)
- **Open Graph images:** Each page currently uses the default OG image referenced in metadata; consider custom OG cards per page
- **Build step (optional):** If maintaining the nav/footer across 8 files becomes painful, consider migrating to Eleventy, Astro, or a simple Jekyll setup
- **Form analytics:** Formspree dashboard provides submission tracking; consider also piping to a CRM via Formspree's webhook integrations

---

## License

Copyright © 2025 Curation Media SSP. All rights reserved.
