# Sara Valarezo — Makeup Artist Website

Website for Sara Valarezo, a Miami-based luxury bridal and special occasion makeup artist.

**Live site:** [saravalarezo.com](https://saravalarezo.com)  
**Repo:** [github.com/wheaties1187/saravalarezo](https://github.com/wheaties1187/saravalarezo)

---

## Quick Start

```bash
npm install
node server.js
```

Then open [http://localhost:3000](http://localhost:3000).

**Deploy:** Push to `main` — Railway auto-deploys within ~60 seconds.

---

## Project Summary

| | |
|---|---|
| **Client** | Sara Valarezo |
| **Business** | Luxury bridal & special occasion makeup artist |
| **Location** | Miami, FL (destination bookings available) |
| **Domain** | saravalarezo.com (Namecheap) |
| **Hosting** | Railway (same account as 2weeks.app) |
| **Booking** | Square Appointments (embed live) |
| **Instagram** | [@saravalarezopromakeup](https://instagram.com/saravalarezopromakeup) |
| **TikTok** | @saravalarezopromakeup (unconfirmed — verify handle) |

---

## Site Sections

1. **Nav** — SV monogram, centered links (About, Services, Gallery, Pricing), Book Now CTA
2. **Hero** — Blush background, wordmark, tagline, consultation CTA
3. **About** — Portrait photo + bio copy
4. **Services** — Bridal, Bridal Party, Social & Events, Editorial
5. **Gallery** — 6-photo editorial grid
6. **Pricing** — Social ($120+), Bridal ($350+), Bridal Party ($280+/person), Editorial ($400+)
7. **Booking** — Square Appointments embed
8. **Testimonials** — 3 quotes (placeholder — needs real client reviews)
9. **FAQ** — Accordion, 6 questions
10. **Footer** — Social links, nav, Miami location

---

## Brand

- **Primary colors:** White `#ffffff`, Blush `#faf2ee`, Nude `#f3e0d4`, Black `#1a1a18`
- **Accent colors:** Taupe `#a68b6e`, Rose `#c47a8a`, Slate `#4e7080`, Navy `#2b3a47`
- **Display font:** PF Marlet Display *(pending license — currently Cormorant Garamond)*
- **Body font:** Neue Haas Grotesk Display Pro *(pending license — currently DM Sans)*
- **Logo files:** `public/assets/logo-wordmark.png`, `public/assets/logo-monogram.png`

---

## Current Status

| Area | Status | Notes |
|---|---|---|
| Infrastructure | ✅ Complete | Railway live, DNS configured, SSL active |
| GitHub / CI | ✅ Complete | Auto-deploys on push to main |
| Site design | ✅ Complete | Full single-page site live |
| Navigation | ✅ Complete | Transparent over hero, frosted on scroll, logo swaps white↔dark |
| Hero background | ✅ Complete | Blush-colorized photo, centered |
| Gallery photos | ✅ Complete | 6 photos in editorial grid |
| About photo | ✅ Complete | saravalarezo-about.jpg in place |
| Favicon | ✅ Complete | SV monogram PNG (blush bg) |
| Square booking | ✅ Complete | Embed code live |
| .gitignore | ✅ Complete | node_modules/, .env, .DS_Store, zips/, creative/ |
| Bio / copy | ⏳ Placeholder | Sara to write actual copy |
| Testimonials | ⏳ Placeholder | Replace with real client quotes |
| Pricing | ⏳ Placeholder | Social $150+ confirmed — rest TBD |
| Licensed fonts | 🔲 Pending | Awaiting PF Marlet + Neue Haas font files |

---

## Pending Items

- [ ] Sara to confirm actual pricing rates
- [ ] Sara to write About section bio
- [ ] Replace placeholder testimonials with real client quotes
- [ ] Verify TikTok handle
- [ ] Add licensed font files to `public/fonts/` and update CSS variables
- [ ] Add `og:image` meta tag for social sharing previews
- [ ] Set up analytics (Google Analytics or Plausible)
- [ ] Consider a contact form (Formspree — no backend needed)
- [ ] Optimize gallery images for web (<500KB each)
- [ ] Convert favicon to transparent PNG or `.ico`

---

## Related

- See [`TECH-SPEC.md`](TECH-SPEC.md) for full technical reference
