# V2C Media Kit · Email

Official V2C email design system. Templates, brand identity and guidelines for use by **V2C Official Installers**, authorized distributors, communication partners, agencies and press.

This repository complements the [official V2C graphic material](https://v2charge.com/material-grafico) (logos, videos, identity manual) with the email-specific component.

---

## What's inside

Three production-ready HTML email templates based on the V2C visual identity:

| Template | Best for | Style |
|---|---|---|
| **Editorial** | Newsletters, periodic updates | Refined magazine, light background, generous whitespace |
| **Data** | Product announcements, technical updates | Stats + features + account manager signature |
| **Bold** | Events, launches, invitations | Dark, dramatic, single-focus message |

All templates follow professional email standards: `<table>`-based layout, inline CSS, 600px width, Outlook/Gmail/Apple Mail compatibility, mobile-responsive, RGPD/LSSI-compliant footer, and per-recipient personalization.

---

## Who is this for?

- 🔧 **V2C Official Installers** communicating with their end-customer base while keeping V2C brand consistency
- 📦 **Authorized distributors** sending product or service communications
- 🎨 **Agencies and partners** producing V2C campaigns
- 📰 **Press and media** needing visual reference materials

---

## Getting started

### Option A — Direct download

Click the green **"Code"** button above → **"Download ZIP"**. You'll get the templates, customize them in your favorite HTML editor, and use them in your usual sending platform (Mailchimp, HubSpot, Brevo, Resend, etc.).

### Option B — Git (recommended for repeated use)

```bash
git clone https://github.com/V2Charge/v2c-media-kit.git
cd v2c-media-kit
```

### Option C — AI-assisted (fastest)

If you usually work with an AI assistant (Claude, ChatGPT, Cursor, Copilot…), open the folder in your AI-enabled editor and ask in natural language:

> *"Adapt the Editorial template for a hands-on training session about Trydan Pro on June 15th in Madrid. CTA: register. Languages: English, Spanish, French."*

The [`CLAUDE.md`](./CLAUDE.md) file teaches the AI how to preserve V2C brand consistency, keep the legal footer intact, and produce email-compatible HTML. It's written for LLMs but also serves as a solid technical reference if you customize templates by hand.

---

## Structure

```
masters/
  editorial.html     ← Template A
  data.html          ← Template B
  bold.html          ← Template C
examples/
  campaign.example.json
output/              ← Where your customized work goes (empty by default)
CLAUDE.md            ← Technical guide for AI assistants and developers
BRAND.md             ← Quick visual identity reference
LICENSE
README.md
```

---

## Customization

Each template uses **Handlebars variables** (`{{firstname}}`, `{{cta_url}}`, etc.) that you can:

- **Replace manually** before sending (find-and-replace)
- **Leave as-is** if your sending platform supports Handlebars merge tags (Resend, HubSpot Marketing Email, Mailchimp with conversion, etc.)
- **Generate a structured JSON** with your AI assistant, ready to upload to a compatible platform

Common variables:

| Variable | Meaning |
|---|---|
| `{{firstname}}` | Recipient's first name |
| `{{lastname}}` | Recipient's last name |
| `{{company}}` | Recipient's company |
| `{{owner_firstname}}` | Your first name (or the account manager's) |
| `{{owner_email}}` | Your contact email |
| `{{cta_url}}` | Primary button URL |
| `{{unsubscribe_url}}` | Unsubscribe link (mandatory under GDPR) |

Complete list of all content placeholders in [`CLAUDE.md`](./CLAUDE.md).

---

## Visual identity

These templates follow the [V2C corporate identity manual](https://v2charge.com/material-grafico). Quick summary:

- **Typeface:** Montserrat (with Arial fallback for email)
- **Palette:** Black `#0E0E0E`, white `#ffffff`, greys `#F4F4F2` / `#ECECEA` / `#7A7A78`
- **Logos:** [black version](https://v2charge.com/wp-content/uploads/2022/01/logotipo-v2c-black.png) · [white version](https://newsletter.v2charge.com/v2c-logo-white.png) · [SVG vector](https://v2charge.com/material-grafico)
- **Tone:** B&W minimal, editorial, uppercase eyebrows with letter-spacing

---

## Legal footer

All templates include a **legal footer block** marked with `<!-- LOCKED -->...<!-- /LOCKED -->` comments. It contains:

- VAT ID B98496706
- Registered address: Camí Nou 268, 46950 Xirivella, Valencia, Spain
- Link to the [privacy policy](https://v2charge.com/privacy-policy/)
- Unsubscribe variable (`{{unsubscribe_url}}`)
- V2C social media icons

**Do not modify this block** — it's required under GDPR / Spanish LSSI law, and the unsubscribe mechanism must remain functional. If you need to adapt it (e.g. you're an authorized distributor in another country with your own legal entity), contact the V2C communications team first.

---

## License and usage

These templates are **V2C property** and are made freely available for use by:

- V2C Official Installers in communications to their end customers
- V2C authorized distributors
- Agencies and partners contracted by V2C
- Press and media for reference

Use by unauthorized third parties is not permitted, nor is modification of the logo, legal footer or brand identity. For commercial use outside the above, contact the V2C communications team.

---

## Contact

To request new templates, report issues, or for any brand identity inquiries:

📧 **comunicacion@v2charge.com** — V2C Communications and Marketing team
🌐 **[v2charge.com/material-grafico](https://v2charge.com/material-grafico)** — full official graphic material

---

<details>
<summary><sub>Information for the V2C team</sub></summary>

<br>

If you're part of the V2C team (Official Installer, distributor, internal communications), you have access to the internal sending platform where you can upload the `output/campaign.json` directly, choose your HubSpot contact segment, and send — without touching HTML.

Ask your manager for access or check the internal portal.

</details>

---

<sub>V2C · VAT ID B98496706 · Camí Nou 268, 46950 Xirivella, Valencia, Spain</sub>
