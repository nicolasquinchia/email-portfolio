# Headspace - All Day, Everyday Support Email

> Recreated for portfolio purposes only. Original email by Headspace. Not affiliated with or endorsed by Headspace, Inc. Assets sourced from Really Good Emails (assets.mailcharts.com) and Headspace's public CDN.

---

## Overview

Recreation of a Headspace promotional/engagement email highlighting four core product offerings: guided meditations, the Ebb AI companion, weekly therapy sessions, and expert-led sleep programs. The email uses a distinctive two-column layout — a left column of stacked feature images alongside a vertical timeline graphic, and a right column of headline + body copy + CTA links — creating a structured, editorial feel unique among the three portfolio emails.

The build prioritizes **dual-column to single-column stacking**, **custom web font rendering with system fallbacks**, and **precise mobile reflow** through a comprehensive hide/show class strategy.

---

## Technical Highlights

### Dual-Column Hide/Show Architecture
The desktop layout uses a three-cell row: a left `<td>` with stacked feature images, a center `<td>` with a vertical timeline graphic, and a right `<td>` with article text. On mobile, the image column and desktop timeline are hidden via `.hide { display: none !important; }`, and individual images are re-injected inline within the text column using `.show_mob { display: block !important; }`. This approach avoids CSS stacking of multi-cell rows — a technique required because Gmail mobile strips `<head>` CSS that would otherwise handle column reordering.

### Two Timeline Graphics (Desktop vs Mobile)
The vertical timeline line is implemented as an `<img>` (not a CSS border or background), with two separate image assets at different heights — one sized for desktop spacing, one for mobile. The desktop version is hidden on mobile (`.hide`) and the mobile version is hidden on desktop (`display: none` inline, revealed via `.show_mob`). This ensures the timeline correctly spans all four articles at both viewport sizes without relying on dynamic height calculations.

### Custom Web Fonts via @font-face
The email loads Headspace's proprietary `Apercu-Regular` and `Apercu-Bold` typefaces via `@font-face` declarations pointing to Headspace's static CDN (`static.headspace.com/fonts/`). All font declarations include `Arial, Helvetica, sans-serif` fallbacks for clients that block external font loading (Outlook, older Gmail). MSO-specific styles force Arial across all Outlook versions.

### Bulletproof Rounded Buttons
CTA buttons use `v:roundrect` with `arcsize="49%"` for Outlook rendering — producing correctly rounded pill-shaped buttons in all Outlook versions where CSS `border-radius` is ignored by the rendering engine.

### Comprehensive Mobile Resizing
The media query block includes an extensive set of utility classes for mobile-specific adjustments:
- Font size + line height pairs: `fs37_lh42`, `fs20_lh24`, `fs16_lh26`, `fs16_lh24`, `fs12_lh17`, `fs10_lh14`, `fs10`
- Spacer height overrides: `h98`, `h56`, `h53`, `h50`, `h49`, `h45`, `h30`, `h24`, `h20`, `h18`, `h11`
- Horizontal padding classes: `px-37`, `px-28`, `px-27`, `px-10`, `px-0`, `pl-20`
- Vertical padding classes: `pt-31`, `pt-15`, `pt-5`

These classes override desktop spacer `<td>` heights and font sizes independently, allowing precise layout control without duplicating structural markup.

### Preheader with Invisible Characters
The preheader uses zero-width non-joiner characters (`͏‌`) to pad preview text length — preventing email clients from pulling visible body copy into the inbox preview snippet.

### Dark Mode Support
Implements dual dark mode handling:
- `color-scheme: light dark` declared in `:root` for client-level color scheme awareness
- `u+.body .txt_white { mix-blend-mode: screen }` for Gmail dark mode text rendering
- `u+.body .txt_white2 { mix-blend-mode: difference }` for secondary text elements

### Social Icons — Table-Based Spacing
Social icons (Facebook, Instagram, X, YouTube) use a dedicated `<table>` with fixed-width spacer `<td>` cells between each icon — a more Outlook-consistent approach than `&nbsp;` inline spacing, ensuring even gaps across all clients.

### CAN-SPAM Compliance + Mental Health Disclaimer
Footer includes physical mailing address, unsubscribe link, legal links, and copyright. Uniquely, this email also includes a prominent mental health crisis disclaimer above the footer (988 crisis line, 911 guidance) — standard practice for health and wellness brands operating in the US market.

---

## Structure

```
├── Preheader (hidden)
├── Hero
│   ├── Headspace logo
│   ├── Headline — "All day, everyday support"
│   ├── Body copy
│   ├── Primary CTA — "Get started today" (blue, pill-shaped, bulletproof)
│   └── Secondary CTA — "Check my coverage »"
├── Content — Four Feature Articles
│   ├── [Desktop] Left column — stacked feature images
│   ├── [Desktop/Mobile] Center column — vertical timeline graphic (dual asset)
│   └── Right column — article text (images injected inline on mobile via show_mob)
│       ├── Article 1 — Start your morning with mindfulness*
│       ├── Article 2 — Reflect on your day with Ebb*
│       ├── Article 3 — Attend your weekly therapy session
│       └── Article 4 — End your day with expert-led programs*
├── Repeat CTA
│   ├── Primary CTA — "Get started today"
│   ├── Secondary CTA — "Check my coverage »"
│   └── Subscription disclaimer footnote
├── Mental Health Crisis Disclaimer
├── Divider
├── Social Icons — Facebook, Instagram, X, YouTube
└── Footer
    ├── Navigation links — My Headspace, How it works, FAQs, T&Cs, Privacy Policy
    ├── Unsubscribe + registered user notice
    ├── Physical address
    └── Copyright
```

---

## Key Decisions

**Hide/show over CSS stacking:** The three-column desktop structure (images | timeline | text) cannot be reliably stacked using CSS alone in Gmail mobile. Instead, desktop image cells are hidden on mobile and equivalent images are re-injected within the text column via `show_mob`. This results in more markup but guarantees correct render order across all clients.

**Dual timeline image assets:** A single stretchy background line would be unreliable across clients. Two fixed-height `<img>` assets — one for desktop proportions, one for mobile — are toggled via hide/show, ensuring the timeline always aligns with its four anchor points.

**Spacer `<td>` height overrides instead of margin/padding:** All vertical spacing between sections uses explicit `height` spacer rows with corresponding mobile override classes. This is more reliable than `margin` or `padding-top` in table-based layouts, particularly in Outlook where CSS box model behavior is inconsistent.

**`v:roundrect` over `v:rect`:** Pill-shaped buttons (`border-radius: 32px`) require `v:roundrect` with `arcsize` in Outlook — `v:rect` produces square corners and would not match the original design.

---

## QA Testing

| Client | Result |
|---|---|
| Gmail Web (Chrome) | ✓ Pass |
| Gmail Mobile (Android) | ✓ Pass |
| Outlook Web (outlook.com) | ✓ Pass |
| Dark Mode (DevTools emulation) | ✓ Pass — partial Gmail Android |

### Known Limitations
- Custom `Apercu` fonts load only in clients that support `@font-face` and allow external font requests — Outlook and some Gmail configurations fall back to Arial
- Gmail Android dark mode applies partial color inversion on the light `#f9f4f2` background — inherent Gmail limitation, not fixable via CSS alone
- Timeline image assets are fixed-height — if article copy reflows to additional lines on very narrow viewports (<320px), the timeline graphic may not align perfectly with article anchors

---

## Assets

All images sourced from Really Good Emails (`assets.mailcharts.com`) and Headspace's public static CDN (`static.headspace.com`). No assets were downloaded, modified, or redistributed. All URLs point to their original public locations.

---

*Built by Nicolás Quinchía — [Portfolio](https://nicolasquinchia.github.io/email-portfolio/) · [GitHub](https://github.com/nicolasquinchia) · [LinkedIn](https://linkedin.com/in/nicolasquinchia)*