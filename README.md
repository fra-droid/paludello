# PALUDELLO ░ menta della palude ░ AVELLINO

One-page website for **Paludello** — a mint liqueur made in Avellino. Punk DIY zine aesthetic. Not from Cilento.

## What it is

A single-page static site built in plain HTML/CSS/JS. No framework, no build step, no dependencies beyond Google Fonts.

**Sections:**
- Hero — giant stenciled title, torn label taped to the page, price tag, AVELLINO stamp
- Scrolling marquee strip
- Manifesto — scrawled text, dashed border, staples
- Polaroid photo placeholders (swap in real photos when ready)
- "Come si beve" checklist
- Frog terminal — click the frog, it talks back
- Order CTA
- Footer

**Interactive features:**
- 🐸 Ambient swamp audio — synthesized brown noise, crickets, distant frogs, water plops (toggle bottom-right)
- Cursor spore trails on mouse move
- Fireflies blinking in the background

## Files

```
paludello/
├── index.html               # the entire site
└── assets/
    └── paludello-label.png  # label artwork (drop in real product photos here)
```

## Running locally

No build step needed. Just serve the directory:

```bash
npx serve .
# → http://localhost:3000
```

Or open `index.html` directly in a browser.

## Deploying to Vercel

1. Push to GitHub
2. Go to [vercel.com](https://vercel.com) → **Add New Project** → import this repo
3. Settings: Framework = `Other`, Build Command = *(empty)*, Output Directory = *(empty)*
4. Deploy — done

Every push to `main` auto-redeploys.

## Customising

| What | Where in `index.html` |
|---|---|
| Price | `.price-tag .euro` — currently `€38` |
| Volume | `.vol-stamp` — currently `500 ML` |
| Order link | `<a class="order-cta" href="#">` — swap `#` for real URL |
| Frog lines | `const lines = [...]` in the `frog()` function |
| Photos | Replace the `.ph` placeholder divs with `<img>` tags |
| Contact email | Footer `<p>` — add email link when ready |

## Stack

- Plain HTML5 / CSS3 / vanilla JS
- Fonts via Google Fonts: Rubik Mono One, Special Elite, Permanent Marker, Caveat, Bungee Shade
- Audio: Web Audio API (synthesized, no audio files)
- Zero runtime dependencies
