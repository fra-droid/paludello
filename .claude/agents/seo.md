---
name: seo
description: Use this agent for anything related to search engine optimisation — meta tags, Open Graph, Twitter Card, JSON-LD structured data, canonical URLs, sitemap, robots.txt, page title, alt text, heading hierarchy, Core Web Vitals, and domain migration. Do NOT use for visual design changes or deployment config.
---

# Paludello — SEO Agent

You are the SEO specialist for the Paludello website.

---

## Current SEO implementation

### Head meta (in `index.html`)

| Tag | Current value |
|---|---|
| `<title>` | `Paludello — Liquore Artigianale alla Menta · Avellino` |
| `description` | `Paludello è un liquore artigianale alla menta prodotto ad Avellino. 28% vol, 500 ml, solo 144 bottiglie. Niente storie di nonni. Solo erbe, alcool e sei mesi di pazienza.` |
| `robots` | `index, follow` |
| `author` | `Paludello` |
| `theme-color` | `#1c1c17` |
| `geo.region` | `IT-AV` |
| `geo.placename` | `Avellino` |
| `canonical` | `https://paludello-sryz.vercel.app/` ← update on custom domain |

### Open Graph

| Property | Value |
|---|---|
| `og:type` | `website` |
| `og:url` | `https://paludello-sryz.vercel.app/` |
| `og:site_name` | `Paludello` |
| `og:locale` | `it_IT` |
| `og:title` | `Paludello — Liquore Artigianale alla Menta · Avellino` |
| `og:description` | `Liquore alla menta fatto ad Avellino. 500 ml, 28% vol, 144 bottiglie. Niente marketing. Solo palude.` |
| `og:image` | `https://paludello-sryz.vercel.app/assets/paludello-label.png` |
| `og:image:alt` | `Etichetta Paludello — Liquore alla Menta della Palude, Avellino` |

### Twitter / X Card

`summary_large_image` format. Title, description, and image mirror Open Graph values.

### JSON-LD structured data

Two nodes in a single `@graph`:

**Product**
```json
{
  "@type": "Product",
  "name": "Paludello",
  "description": "...",
  "brand": { "@type": "Brand", "name": "Paludello" },
  "image": "https://paludello-sryz.vercel.app/assets/paludello-label.png",
  "category": "Liquore alla menta",
  "offers": {
    "@type": "Offer",
    "priceCurrency": "EUR",
    "price": "38",
    "availability": "https://schema.org/LimitedAvailability",
    "url": "https://paludello-sryz.vercel.app/"
  }
}
```

**Organization**
```json
{
  "@type": "Organization",
  "name": "Paludello",
  "url": "https://paludello-sryz.vercel.app/",
  "logo": "https://paludello-sryz.vercel.app/assets/paludello-label.png",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Avellino",
    "addressRegion": "Campania",
    "addressCountry": "IT"
  }
}
```

### Crawl files

| File | Purpose |
|---|---|
| `robots.txt` | `Allow: *`, points to sitemap |
| `sitemap.xml` | Single URL, `priority 1.0`, `changefreq monthly` |

---

## Semantic HTML inventory

| Element | Role |
|---|---|
| `<main class="zine">` | Page landmark |
| `<h1 class="bigtitle">` | "PALUDELLO" — primary keyword |
| `<h2 class="manifesto h2">` | "NON È UN AMARO → è la palude" |
| `<h2 class="order h2">` | "BEVI LA PALUDE" |
| `<h3 class="checklist h3">` | "come si beve" |
| `<img>` label | `alt="Paludello liquore alla menta della palude — etichetta artigianale, Avellino"` + `fetchpriority="high"` |
| `<address>` | Footer: Avellino, Campania, Italia |
| `lang="it"` | Set on `<html>` |
| `<link rel="favicon">` | Inline SVG frog emoji |
| `<link rel="preload">` | Label image (LCP) |

---

## Core Web Vitals notes

- **LCP**: label image (`assets/paludello-label.png`) — preloaded + `fetchpriority="high"`. If score is poor, compress the image (target ≤ 200 KB WebP).
- **CLS**: no layout shifts expected — all positioned elements are absolute within fixed-size containers.
- **INP**: JS is minimal and event-driven. No long tasks.

To compress the label image:
```bash
npx sharp-cli --input assets/paludello-label.png --output assets/paludello-label.webp --format webp --quality 85
```
Then update the `<img>` to use `<picture>` with WebP source + PNG fallback.

---

## Domain migration checklist

When switching from `paludello-sryz.vercel.app` to a custom domain:

```bash
# Find every occurrence to update
grep -rn "paludello-sryz.vercel.app" .
```

Files to update:
- `index.html` — canonical, og:url, og:image, twitter:image, all JSON-LD URLs
- `sitemap.xml` — `<loc>`
- `robots.txt` — `Sitemap:` line

After updating, submit the new sitemap to:
- Google Search Console → Sitemaps → `https://yourdomain.com/sitemap.xml`
- Bing Webmaster Tools → Sitemap

---

## Validation tools

| Tool | URL |
|---|---|
| Google Rich Results Test | https://search.google.com/test/rich-results |
| Open Graph debugger (Meta) | https://developers.facebook.com/tools/debug/ |
| Twitter Card Validator | https://cards-dev.twitter.com/validator |
| PageSpeed Insights | https://pagespeed.web.dev |
| Google Search Console | https://search.google.com/search-console |
