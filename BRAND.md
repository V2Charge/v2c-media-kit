# V2C Brand · Quick reference for email

Quick reference for V2C visual identity applied to these templates. For the full corporate manual, see the [official graphic material](https://v2charge.com/material-grafico).

## Palette

| Use | Hex | Notes |
|---|---|---|
| Primary black | `#0E0E0E` | Text, primary buttons, dark backgrounds |
| White | `#ffffff` | Light backgrounds, text on dark |
| Light grey background | `#F4F4F2` | Body background in light templates |
| Very light grey background | `#F8F8F6` | Cards, secondary surfaces on white |
| Border grey | `#ECECEA` | Dividers, borders |
| Secondary text grey | `#7A7A78` | Captions, eyebrows, metadata |
| Body text grey | `#1F1F1F` | Long-form body text |

**Note:** the visual line of these templates is minimal B&W. The historical V2C red (`#e30613`) is not used by default. If a campaign needs an accent color, check with the communications team.

## Typography

- **Family:** Montserrat (Google Fonts)
- **Email fallback:** `'Montserrat', Arial, sans-serif`
- **Weights used:** 400 (regular), 600 (semibold), 700 (bold)

> In email clients that don't load web fonts (Outlook, Gmail by default, Apple Mail with privacy protection), the system automatically falls back to Arial. Design font sizes assuming Arial — Montserrat is a nice-to-have.

### Editorial treatment

- **Eyebrows / labels:** uppercase, weight 600–700, letter-spacing `0.14em` to `0.22em` depending on size.
- **Headlines:** weight 700, negative letter-spacing (`-0.025em` to `-0.045em` for large display), tight line-height (`0.92` to `1.05`).
- **Body:** weight 400, line-height `1.6` to `1.7`.

## Logos

| Version | URL | Use |
|---|---|---|
| Black | `https://v2charge.com/wp-content/uploads/2022/01/logotipo-v2c-black.png` | Light templates |
| White | `https://newsletter.v2charge.com/v2c-logo-white.png` | Dark templates |
| SVG vector | [v2charge.com/material-grafico](https://v2charge.com/material-grafico) | Materials outside email |

**Rule:** typical width in email = 56–64 px. Don't stretch, don't recolor, don't apply `filter: brightness()` or `filter: invert()` (they don't work in Gmail/Outlook).

## Social media icons

Official URLs for use in footers:

```
LinkedIn:  https://v2charge.com/wp-content/uploads/2023/06/v2c-linkedin.png
Instagram: https://v2charge.com/wp-content/uploads/2023/06/v2c-instagram.png
Facebook:  https://v2charge.com/wp-content/uploads/2023/06/v2c-facebook.png
X:         https://v2charge.com/wp-content/uploads/2026/05/twitter-x.png
YouTube:   https://v2charge.com/wp-content/uploads/2023/06/v2c-youtube.png
```

Recommended size in email: 14 × 14 px.

## Email standards

These templates follow best practices for maximum compatibility:

- Layout: `<table role="presentation">` (no flex, no grid)
- Inline CSS mandatory; `<style>` blocks only for mobile media queries
- Container width: **600 px** (industry standard)
- Images: absolute URLs, with `alt` text, PNG/JPG format (no inline SVG)
- Web fonts via `<link>`: optional (Outlook ignores them, so does Gmail — always rely on Arial fallback)
- Hidden pre-header right after `<body>` to optimize inbox preview
- GDPR/LSSI legal footer with VAT ID, address and unsubscribe, marked as LOCKED region

## V2C legal data

Mandatory footer (do not modify):

```
V2C · VAT ID B98496706
Camí Nou 268, 46950 Xirivella, Valencia, Spain
https://v2charge.com/privacy-policy/
```
