# KAYAK - Welcome / Onboarding Email

> Recreated for portfolio purposes only. Original email by KAYAK. Not affiliated with or endorsed by KAYAK Software Corporation. Assets sourced from KAYAK's public image CDN.

---

## Overview

Recreation of KAYAK's welcome onboarding email, sent to new users after account creation. The email introduces three core product features - Price Alerts, Trips, and Wishlist - through a clean card-based layout, followed by a secondary CTA promoting the KAYAK Navigator tool and app download section.

The build prioritizes **fluid responsive behavior**, **cross-client compatibility**, and **structural clarity** through semantic commenting and modular section blocks.

---

## Technical Highlights

### Fluid Layout (No Media Queries Required)
The email uses percentage-based widths and `max-width` constraints on key containers rather than relying on media queries for core layout behavior. This ensures compatibility with Gmail mobile's limited `<head>` CSS support while maintaining readability across screen sizes.

### Bulletproof Rounded Buttons
CTA buttons use `v:roundrect` (not `v:rect`) for Outlook rendering - correctly producing rounded corners in all Outlook versions where CSS `border-radius` is ignored.

### Preheader with Invisible Characters
The preheader uses zero-width non-joiner characters (`͏‌`) to pad the preview text to the desired length, preventing email clients from pulling in body copy as preview text - a standard production technique.

### Dark Mode Support
Implements dual dark mode strategy:
- `color-scheme: light dark` declared in `:root` for client-level awareness
- `u+.body .txt_white { mix-blend-mode: screen }` for Gmail dark mode text handling
- `u+.body .txt_white2 { mix-blend-mode: difference }` for secondary text elements

### Outlook Dividers
Section dividers use `bgcolor` on `<td>` elements with explicit height spacers rather than CSS borders - ensuring consistent rendering across all Outlook versions.

### CAN-SPAM Compliance
Footer includes physical mailing address, unsubscribe link, email preferences, and feedback links - meeting full CAN-SPAM requirements.

---

## Structure

```
├── Preheader (hidden)
├── Header
│   ├── KAYAK logo
│   └── Navigation icons - Flights, Hotels, Cars, Packages
├── Hero
│   ├── Illustration
│   ├── Headline + body copy
│   └── Primary CTA - "Get started" (orange, rounded, bulletproof)
├── Content - "Account perks, unpacked"
│   ├── Perk 1 - Price Alerts (icon + text card)
│   ├── Perk 2 - Trips (icon + text card)
│   └── Perk 3 - Wishlist (icon + text card)
├── Secondary CTA - KAYAK Navigator
│   ├── Headline + body copy
│   ├── Secondary CTA - "Check it out" (outlined button)
│   └── Navigator illustration
├── App Download Section
│   ├── Headline + copy
│   ├── App Store + Google Play badges
│   └── Mobile app illustration
├── Social Icons - TikTok, Facebook, Twitter, Instagram
└── Footer
    ├── Tagline
    ├── Legal links
    └── Physical address + copyright
```

---

## Key Decisions

**Fluid over responsive:** Given Gmail mobile's CSS limitations in the `<head>`, the layout was built to be inherently fluid rather than breakpoint-dependent. The two-column perk cards maintain readability down to ~360px without requiring stacking.

**`v:roundrect` for buttons:** Unlike the more common `v:rect` pattern, `v:roundrect` with `arcsize` was used to match the original's rounded button corners in Outlook.

**Invisible preheader padding:** The zero-width character technique was chosen over a single long text string to allow natural language in the preheader while preventing body copy bleed across all clients.

---

## QA Testing

| Client | Result |
|---|---|
| Gmail Web (Chrome) | ✓ Pass |
| Gmail Mobile (Android) | ✓ Pass |
| Outlook Web (outlook.com) | ✓ Pass |
| Dark Mode (DevTools emulation) | ✓ Pass - partial Gmail Android |

### Known Limitations
- Two-column perk layout below 360px may feel tight - full stack behavior requires media queries not implemented in this fluid build
- Gmail Android dark mode applies partial color inversion on light background sections - inherent Gmail limitation, not fixable via CSS alone
- Social icon spacing uses `&nbsp;` inline approach - a table-based implementation would be more Outlook-consistent

---

## Assets

All images sourced from KAYAK's public image CDN (`kayak.com/eimg/`). No assets were downloaded, modified, or redistributed. All URLs point to their original public locations.

---

*Built by Nicolás Quinchía - [Portfolio](https://nicolasquinchia.github.io/email-portfolio/) · [GitHub](https://github.com/nicolasquinchia) · [LinkedIn](https://linkedin.com/in/nicolasquinchia)*
