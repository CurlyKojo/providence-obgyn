# Providence OBGYN — Website

Static site for Providence OBGYN, Dr. Symone's solo practice in Las Vegas.

## What's in here

```
site/
├── shared.css                          # Shared stylesheet for the whole site
└── articles/
    └── first-prenatal-visit.html       # "Your first prenatal visit" article
```

## Design system

- **Palette** — burgundy (`#561321`), warm ivory paper (`#f4efe6`), charcoal ink
- **Typography** — Fraunces (display), Cormorant Garamond (body/serif), Inter (UI), JetBrains Mono (eyebrows & meta)
- **Stylesheet** — `site/shared.css` defines all tokens as CSS variables on `:root`; every page pulls from one source of truth

## Running locally

No build step. Just serve the `site/` directory:

```bash
cd site
python3 -m http.server 8000
# then open http://localhost:8000/articles/first-prenatal-visit.html
```

## Implementation notes

- The article page uses a sticky in-page TOC (`.side-left`) wired to `id` anchors on each `<h2>`; `scroll-margin-top` keeps anchor targets clear of the sticky nav.
- Image placeholders (striped burgundy frames) mark spots where real photography/ultrasound imagery should be swapped in before launch.
- The "Print version →" share link points at `first-prenatal-visit-print.html` — that file exists in the original design bundle and can be added to this repo when ready.
- Fonts are loaded from Google Fonts; `preconnect` is in place to cut connection time.

## Credits

Design: Claude Design (claude.ai/design) · handoff bundle from `Symone's Medical Practice`.
