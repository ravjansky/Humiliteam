# HumiliTeam Network

**Love God. Love People. Make Disciples.**

A youth community website for HumiliTeam Network, based in Olongapo City, Philippines. Built as a single-page static site with a focus on performance, cinematic motion design, and premium visual identity.

🌐 **Live:** [humiliteam.pages.dev](https://humiliteam.pages.dev)

---

## Overview

HumiliTeam Network is a youth-led faith community — 936 members strong, always open, everyone welcome. This site serves as the digital front door: a place for seekers, the curious, and the faithful to learn who we are and how to connect.

The design language is intentionally cinematic — dark charcoal backgrounds, gold accent typography, and a raymarched metaball hero that responds to cursor movement on desktop. Every motion on the page follows a strict easing system for brand coherence.

---

## Tech Stack

| Layer | Tech |
|-------|------|
| **Markup** | Semantic HTML5 |
| **Styling** | Vanilla CSS with custom properties, mobile-first, fluid typography via `clamp()` |
| **Animation** | GSAP 3.12 + ScrollTrigger |
| **Smooth Scroll** | Lenis 1.1 |
| **Hero Background** | Three.js raymarched metaball shader (WebGL) |
| **Hosting** | Cloudflare Pages |

No build step. No bundler. No framework. Just a single `index.html` that ships.

---

## Project Structure

```
humiliteam/
├── index.html              # the entire site — markup, styles, scripts
├── assets/
│   ├── favicons/
│   │   ├── favicon.ico     # primary favicon
│   │   ├── favicon.avif    # modern fallback
│   │   └── favicon.webp    # webp fallback
│   └── webclip.png         # apple-touch-icon + og:image
├── .gitignore
└── README.md
```

---

## Motion System

All animations enforce a strict three-token easing vocabulary. No library defaults, no named eases, no deviations.

```css
:root {
  --ease-signature: cubic-bezier(0.22, 1, 0.36, 1);  /* primary — hero, reveals, entrances */
  --ease-smooth:    cubic-bezier(0.4, 0.0, 0.2, 1);  /* subtle UI transitions */
  --ease-float:     cubic-bezier(0.25, 0.8, 0.25, 1); /* hover states, gentle motion */
}
```

This creates cinematic consistency across every interaction — scroll reveals, hover states, loader transitions, and the GSAP-driven page entrance.

---

## Performance

The hero shader is the heaviest element. Optimizations in place:

- **Reduced render resolution** — 50% on desktop, 35% on mobile. CSS upscales the canvas.
- **March steps capped** — 28 on desktop (down from 48), 12 on mobile.
- **Frame-throttled** — ~45fps desktop, ~30fps mobile. A slow-moving blob doesn't need 60fps.
- **Viewport-aware** — `IntersectionObserver` pauses the render loop entirely when the hero scrolls out of view.
- **Mouse interactivity disabled on mobile** — no cursor sphere computation, no attraction physics.
- **`prefers-reduced-motion`** — kills all animation durations and hides the loader entirely.
- **Debounced resize** — 150ms throttle on window resize events.

---

## Loader Sequence

1. **Cross fills from bottom** — a SVG cross of Jesus fills with gold, tracking real asset loading progress (fonts + shader compilation).
2. **Cross morphs into H** — the cross path transforms into a serif H letterform (for HumiliTeam).
3. **H zooms out as clip-path mask** — the H scales outward, revealing the full page beneath it.
4. **Hero entrance** — GSAP staggers in the headline, eyebrow, sub-copy, nav, and side elements.
5. **Safety timeout** — if assets take longer than 7 seconds, the loader force-completes.

---

## SEO

- Full Open Graph + Twitter Card meta tags
- JSON-LD structured data (Organization schema)
- Semantic heading hierarchy (single `<h1>`, proper `<h2>`/`<h3>` nesting)
- `<address>` element for contact info
- `aria-label` and `aria-labelledby` attributes throughout
- Canonical URL
- Descriptive alt text on all media

---

## Deployment

The site is deployed to **Cloudflare Pages** via Git integration. Any push to `main` triggers a new deployment automatically.

Since there's no build step, the Cloudflare Pages build command is empty and the output directory is `/` (root).

| Setting | Value |
|---------|-------|
| Build command | *(none)* |
| Build output directory | `/` |
| Root directory | `/` |

---

## Local Development

No dependencies to install. Just open the file:

```bash
# option 1: direct
open index.html

# option 2: local server (avoids CORS issues with ES modules)
npx serve .

# option 3: python
python3 -m http.server 8000
```

The Three.js import uses `esm.sh` CDN, so a local server is recommended for the shader to load properly.

---

## Credits

Designed and developed by **[RavDigitals](https://ravdigitals.com)**.

Built for the HumiliTeam Network community in Olongapo City, Philippines.

---

## License

This project is the property of HumiliTeam Network. All rights reserved.