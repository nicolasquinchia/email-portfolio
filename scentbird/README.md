# Scentbird — "Be Bold: Trending Note" Promotional Email

> Recreated for portfolio purposes only. Original email by Scentbird. Not affiliated with or endorsed by Scentbird. Assets sourced from Scentbird's public marketing CDN and self-hosted via GitHub for rendering consistency.

---

## Overview

Recreation of Scentbird's "Be Bold — Trending Note" promotional campaign email, featuring six luxury fragrance products. The build replicates the original's modular architecture, where each fragrance section is an independent, reusable component sharing the same HTML structure with unique background images and product assets layered on top.

The email presents a visually rich experience through full-width background images, transparent product bottle overlays, and fragrance note icon grids — all built with production-grade email techniques ensuring consistent rendering across Gmail, Outlook, and Apple Mail.

---

## Technical Highlights

### Dual Background Image System
The email uses two levels of background images simultaneously:

- **Outer wrapper** — a subtle decorative pattern applied to the full email body via `background-image` on the outermost `<td>`, with VML fallback for Outlook
- **Per-section backgrounds** — each of the six product modules has its own unique full-width background image (fruits, botanical elements, script typography) applied via `background-image` + VML `v:rect` fallback

This dual-layer approach creates the rich visual depth of the original while maintaining full Outlook compatibility.

### Transparent PNG Product Images
Fragrance bottle images use PNG format with transparent backgrounds, self-hosted on GitHub to ensure consistent rendering across all email clients. This resolves Gmail's known inconsistency with WebP transparency, which caused black background artifacts in the original CDN-hosted WebP assets.

### VML Bulletproof Buttons
All Subscribe Now CTAs use the `v:rect` + `w:anchorlock` VML bulletproof button technique, ensuring solid background color and correct dimensions in all Outlook versions where CSS `background-color` on anchor tags is not supported.

### Inline-Block Mobile Stacking for Fragrance Notes
Fragrance note icon grids use `display: inline-block` on `<td>` elements directly — without relying on media query-driven `display: block` — allowing natural wrapping behavior in Gmail mobile where `<head>` CSS is stripped. Custom mobile classes (`pr8`, `pr10`, `pr12`, `pr24`, `pl44`, `pt16`) handle precise spacing on wrap, and `fs14-lh16` increases touch target legibility on smaller screens.

### Conditional Line Breaks for Mobile
Long note labels use `<br class="show" style="display: none;">` — a hidden line break that becomes visible on mobile via the `.show` class in the media query. This allows two-line labels on mobile without breaking the single-line layout on desktop.

### Dark Mode Support
Implements dual dark mode strategy:
- `color-scheme: light dark` in `:root` for client-level awareness
- `u+.body .txt_white { mix-blend-mode: screen }` for Gmail dark mode text handling
- `.bg-mobile` class applies `background-size: cover` and resets `background-position` to `top center` on mobile, preventing background cropping when the layout height changes

### Modular Architecture
The email is built as six independent product modules sharing identical HTML structure. Only the following change between modules:

- Background image URL (both CSS and VML)
- Product bottle image URL, alt text, and link
- Brand name and fragrance name
- Fragrance note icon images, labels, and links
- CTA destination URL
- VML height value (each section has a unique pixel height)

This makes the template fully scalable — new products can be added by duplicating one module block and updating its variables, with no structural changes required.

---

## Structure

```
├── Preheader (hidden)
├── Header
│   ├── Dark bar — Scentbird logo
│   └── Tan bar — Subscribe promotional banner
├── Email body (outer decorative background)
│   ├── Product 1 — Juliette Has a Gun · Miami Shake (5 notes)
│   ├── Product 2 — Commodity · Ice(d)+ Bold (3 notes)
│   ├── Product 3 — Ex Nihilo · Lust in Paradise XDP (4 notes)
│   ├── Product 4 — Room 1015 · Poppy Riot (4 notes)
│   ├── Product 5 — Portals · Fiery Passion (5 notes)
│   └── Product 6 — Maison d'Etto · Noisette (5 notes)
└── Footer (dark)
    ├── SMS opt-in banner
    ├── Scentbird logo
    ├── App Store + Google Play badges
    ├── Social icons — Instagram, Facebook, Twitter, Pinterest, TikTok
    ├── Copyright + legal links
    ├── Physical address
    └── Legal disclaimer
```

---

## Key Decisions

**PNG over WebP for product images:** The original email used WebP assets from Scentbird's CDN. Gmail's inconsistent WebP transparency rendering caused black background artifacts on product bottle images. Converting to PNG and self-hosting via GitHub resolved this permanently without any visual quality loss.

**`min-height` over fixed `height` on background sections:** Using `min-height` in CSS allows sections to expand naturally if content reflows on smaller screens, while the VML fallback retains a fixed `height` value since Outlook does not support `min-height` on VML elements.

**`inline-block` stacking without media queries:** Fragrance note grids use `display: inline-block` on `<td>` cells so wrapping occurs naturally based on available width — no media query required. This ensures correct stacking in Gmail mobile, which strips `<head>` CSS entirely.

**Self-hosted social icons:** Instagram and Facebook icons were re-hosted on GitHub to avoid broken image fallbacks from the original Milled CDN URLs, which are session-scoped and expire.

---

## QA Testing

| Client | Result |
|---|---|
| Gmail Web (Chrome) | ✓ Pass |
| Gmail Mobile (Android) | ✓ Pass |
| Outlook Web (outlook.com) | ✓ Pass |
| Dark Mode (DevTools — prefers-color-scheme: dark) | ✓ Partial |

### Known Limitations
- Gmail Android dark mode applies partial color inversion on light background sections — this is a Gmail-specific limitation not fully controllable via CSS
- Outer decorative background image (`background-repeat: repeat`) may tile differently across clients depending on email width rendering — visually acceptable in all tested clients
- VML background heights are fixed pixel values matching desktop content height — on very small screens content may slightly overflow the VML-rendered area in Outlook (does not affect non-Outlook clients)

---

## Assets

Product bottle images (PNG with transparency) are self-hosted at:
`https://raw.githubusercontent.com/nicolasquinchia/email-portfolio/main/scentbird/images/`

Background section images sourced from Scentbird's public marketing CDN:
`https://scentbird-marketing.b-cdn.net/emails/2026-05-06_SB/1/`

Header, footer, and decorative assets sourced from Milled's public image CDN at time of recreation. All URLs point to their original public locations.

---

*Built by Nicolás Quinchía — [Portfolio](https://nicolasquinchia.github.io/email-portfolio/) · [GitHub](https://github.com/nicolasquinchia) · [LinkedIn](https://linkedin.com/in/nicolasquinchia)*
