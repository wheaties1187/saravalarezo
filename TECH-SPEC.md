# Technical Specification — saravalarezo.com

Technical reference for the Sara Valarezo makeup artist website. For project context see [`README.md`](README.md).

---

## Stack

| Layer | Choice | Notes |
|---|---|---|
| Runtime | Node.js | LTS — no specific version pinned |
| Framework | Express 4.x | Static file serving only — no API routes |
| Frontend | Vanilla HTML/CSS/JS | Single `index.html` — no build step |
| Fonts | Google Fonts CDN | Cormorant Garamond + DM Sans (substitutes) |
| Hosting | Railway | Auto-deploy from GitHub main |
| Domain | saravalarezo.com | Registered via Namecheap |
| SSL | Let's Encrypt | Auto-provisioned by Railway |
| Version control | GitHub | github.com/wheaties1187/saravalarezo |

---

## Repository Structure

```
saravalarezo/
├── server.js               # Express app — serves /public as static files
├── package.json            # start script: node server.js
├── .gitignore              # node_modules/, .env, .DS_Store, zips/, creative/
├── README.md               # Project overview
├── TECH-SPEC.md            # This file — technical reference
├── public/
│   ├── index.html          # Entire site — HTML, CSS, and JS in one file
│   ├── assets/
│   │   ├── logo-wordmark.png         # Full wordmark (white bg — used in footer)
│   │   ├── logo-wordmark-glow.png    # Transparent/glow version — used in hero
│   │   ├── logo-monogram.png         # SV monogram dark — nav when scrolled + favicon
│   │   └── logo-monogram-white.png   # SV monogram white — nav over hero
│   └── images/
│       ├── gallery-1.jpg through gallery-6.jpg
│       ├── saravalarezo-about.jpg
│       └── saravalarezo-hero-bg.jpg  # Blush-colorized hero background
├── docs/
│   └── ...                 # Brand assets, PDFs
├── creative/               # PSD/design files — gitignored, local only
└── zips/                   # Build artifacts — gitignored
```

---

## Infrastructure

### Railway

- Project: `saravalarezo` — separate project from `2weeks.app`, same Railway account
- Service connects directly to GitHub repo — deploys on every push to `main`
- Port: Railway injects `PORT` env var at runtime — app uses `process.env.PORT || 3000`
- Custom domain configured under: Settings → Networking → Custom Domain
- SSL auto-provisioned via Let's Encrypt once DNS propagates

### DNS (Namecheap — Advanced DNS)

| Type | Host | Value | TTL |
|---|---|---|---|
| CNAME | @ | jg0ofqkw.up.railway.app | 1 min |
| TXT | _railway-verify | railway-verify=fdc7594b7ead... | 1 min |

> Two legacy Namecheap default records (parking page CNAME and URL redirect) were deleted. Only the two Railway records above should be present.

---

## Deployment Workflow

```bash
# 1. Edit files locally
# 2. Test locally
node server.js          # visit http://localhost:3000

# 3. Commit and push
git add .
git commit -m "description of change"
git push                # Railway auto-deploys (~30–60 seconds)
```

Monitor deployment in Railway dashboard — the service card shows build status. Verify live at saravalarezo.com after deploy completes.

---

## Frontend Architecture

### CSS Design Tokens

```css
--color-white:       #ffffff
--color-blush-light: #faf2ee   /* hero and alternate section backgrounds */
--color-blush:       #f3e0d4   /* borders, gallery placeholders, accents */
--color-nude:        #d9b89c
--color-black:       #1a1a18   /* primary text, nav, footer */
--color-taupe:       #a68b6e   /* labels, muted text, accent */
--color-rose:        #c47a8a
--color-slate:       #4e7080
--color-navy:        #2b3a47

--font-display: 'Cormorant Garamond'  /* TODO: swap to 'PF Marlet Display' */
--font-body:    'DM Sans'             /* TODO: swap to 'Neue Haas Grotesk Display Pro' */
```

### Typography

- **Display:** Cormorant Garamond via Google Fonts CDN (substitute for licensed PF Marlet Display)
- **Body:** DM Sans via Google Fonts CDN (substitute for licensed Neue Haas Grotesk Display Pro)
- To swap: add `@font-face` blocks in CSS using files in `public/fonts/`, then update `--font-display` and `--font-body` variables — no other changes needed

### Nav Layout

- 3-column CSS grid: `1fr auto 1fr`
- Logo left (`justify-self: start`), links center (`justify-self: center`), CTA right (`justify-self: end`)
- **Transparent by default** — background `rgba(255,255,255,0)`, links and button white
- **On scroll (>20px):** `.scrolled` class applied — background `rgba(255,255,255,0.87)`, blur(8px), links and button switch to dark
- **Logo swap:** `logo-monogram-white.png` over hero → `logo-monogram.png` when scrolled (via JS src swap)
- Smooth `0.3s` transition on background, backdrop-filter, border, and box-shadow

### JavaScript

- **Nav scroll behavior** — at 20px scroll depth: toggles `.scrolled` on `<nav>`, swaps logo src between white and dark monogram, transitions all nav colors
- **Mobile nav toggle** — hamburger button opens/closes `#nav-links` on small screens
- **FAQ accordion** — single-open pattern, smooth `max-height` transition
- No frameworks, no build step — plain vanilla JS

---

## Known Issues Resolved

| Issue | Fix |
|---|---|
| Footer `<nav>` inheriting fixed positioning from main nav CSS | Changed footer nav to `<div class="footer-links">` |
| Nav links white-on-white (invisible against white nav background) | Nav now starts transparent with white links over hero; transitions to dark on scroll |
| Nav links spreading full page width | Switched nav from `flex / space-between` to 3-column CSS grid |
| Duplicate "Book" link + two "Book Now" buttons in nav | Removed inline Book link and button — kept only top-right CTA |
| PSD file in `creative/` folder bloating git pushes (3.71MB, HTTP 400 errors) | Purged from git history with `git filter-branch`, added `creative/` to `.gitignore` |

---

## Pending Technical Tasks

- [ ] Install licensed fonts: add files to `public/fonts/`, add `@font-face` to CSS, update `--font-display` and `--font-body` variables
- [ ] Optimize gallery images for web — compress to <500KB each (consider `sharp` or `imagemin`)
- [ ] Add `og:image` and social meta tags to `<head>` for link preview sharing
- [ ] Set up analytics — Google Analytics or [Plausible](https://plausible.io)
- [ ] Contact form — [Formspree](https://formspree.io) is a clean no-backend option
- [ ] Convert favicon to transparent PNG or `.ico` for cleaner browser tab appearance
