# Email Development Portfolio - Nicolás Quinchía

Production-grade HTML email projects covering promotional campaigns, lifecycle marketing, onboarding flows, and transactional emails. Each project is built with a focus on cross-client compatibility, responsive behavior, accessibility (ADA/WCAG), and real-world production techniques.

---

## About

I'm an Email Developer with 3+ years of professional experience building responsive, cross-client email campaigns for Fortune 500 clients - Johnson & Johnson, Pfizer, and USAA - through Publicis Group. My background combines hands-on email production with a full-stack engineering foundation from Holberton School, allowing me to bridge email development, CRM workflows, and frontend engineering.

This portfolio reflects the same standards I apply in production: clean, maintainable code, Outlook-safe VML fallbacks, fluid responsive layouts, and documented technical decisions.

🔗 [Portfolio Site](https://nicolasquinchia.github.io/email-portfolio/) · [LinkedIn](https://linkedin.com/in/nicolasquinchia) · [GitHub](https://github.com/nicolasquinchia)

---

## Projects

| Project | Type | Key Techniques |
|---|---|---|
| [Scentbird - Be Bold](./scentbird/) | Promotional | Dual background images, VML, inline-block stacking, PNG transparency |
| [KAYAK - Welcome Onboarding](./kayak/) | Onboarding | Fluid layout, v:roundrect buttons, preheader padding, dark mode |
| [Headspace - All Day Support](./headspace/) | Engagement | Hide/show dual-column, @font-face custom fonts, dual timeline assets, mobile spacer overrides |
| More coming soon... | | |

---

## Technical Stack

**Email fundamentals**
- XHTML 1.0 Transitional doctype
- Table-based layout with `role="presentation"`
- Inline CSS with MSO conditional comments
- HTML spacers for Outlook spacing control

**Outlook compatibility**
- VML background images (`v:rect` + `v:fill`)
- Bulletproof buttons (`v:rect` / `v:roundrect` + `w:anchorlock`)
- MSO conditional stylesheets

**Responsive & mobile**
- Fluid layouts with percentage widths and `max-width` constraints
- Media query-driven stacking (`display: block` / `display: inline-block`)
- Gmail mobile-safe stacking via `display: inline-block` on `<td>` (no `<head>` CSS dependency)
- Conditional line breaks for mobile label wrapping

**Dark mode**
- `color-scheme: light dark` in `:root`
- `u+.body { mix-blend-mode: screen }` for Gmail dark mode
- `@media (prefers-color-scheme: dark)` for Apple Mail and iOS

**Accessibility**
- Meaningful `alt` text on all non-decorative images
- Logical reading order for screen readers
- Sufficient color contrast ratios
- Descriptive CTA text

**Tooling & workflow**
- Git version control
- Litmus / Chrome DevTools for QA and rendering simulation
- Gmail, Outlook Web, and Android testing

---

## Repository Structure

```
email-portfolio/
│
├── scentbird/          ← Promotional - Be Bold campaign
│   ├── index.html
│   ├── images/
│   └── README.md
│
├── kayak/              ← Onboarding - Welcome email
│   ├── index.html
│   └── README.md
│
└── [more projects]/    ← In progress
```

---

## Disclaimer

Some projects in this repository are recreations of publicly available marketing emails originally distributed by their respective brands. These were developed strictly for portfolio and educational purposes.

I am not affiliated with, endorsed by, or connected to any featured brand. All trademarks, product names, logos, and images belong to their respective owners. No commercial use is intended.

---

*Nicolás Quinchía · Email Developer · Medellín, Colombia · Open to remote roles worldwide*
