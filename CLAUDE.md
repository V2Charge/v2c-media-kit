# AI Assistant Guide · V2C Email Templates

This guide is for **AI assistants** (Claude, GPT, Cursor, Copilot…) helping adapt the V2C email templates for a specific communication.

If you're a developer or partner customizing a template by hand, it also serves as a solid technical reference.

---

## Your job

Given a briefing in natural language (what the user wants to communicate), produce an `output/campaign.json` file with:

- HTML adapted from one of the three master templates (`masters/editorial.html`, `data.html`, `bold.html`)
- A subject line for each requested language
- Translated versions when the briefing mentions multiple languages
- Explanatory notes so the user knows what decisions you made

The resulting JSON can be uploaded to a compatible email sending platform (schema below).

---

## Flow

1. Read the user's briefing.
2. Pick the master that fits best (or use the one the user indicates).
3. Adapt the HTML by filling in the content placeholders (see "Variables").
4. If multiple languages are requested, translate the result.
5. Generate compelling subject lines per language (max 60 chars, no spam triggers).
6. Write `output/campaign.json` following the schema.
7. Explain to the user what decisions you made and what they should review before sending.

---

## Non-negotiable rules

### 1. NEVER touch LOCKED regions

Any block between `<!-- LOCKED -->` and `<!-- /LOCKED -->` is copied **verbatim**. It contains the legally mandatory footer (VAT ID, registered address, privacy policy link, unsubscribe link) required by GDPR and Spanish LSSI. Modifying it is illegal and breaks the unsubscribe mechanism.

### 2. Handlebars variables — don't invent new ones

These variables are substituted at send time, **one per recipient**. Don't change them, don't invent new ones.

| Variable | Typical source | Example |
|---|---|---|
| `{{firstname}}` | Recipient's first name | "Peter" |
| `{{lastname}}` | Recipient's last name | "Smith" |
| `{{fullname}}` | Full name | "Peter Smith" |
| `{{email}}` | Recipient's email | "peter@customer.com" |
| `{{company}}` | Company | "Acme Ltd." |
| `{{owner_firstname}}` | Account manager's first name | "Charles" |
| `{{owner_lastname}}` | Account manager's last name | "Vidal" |
| `{{owner_email}}` | Account manager's email | "charles@v2charge.com" |
| `{{owner_initials}}` | Account manager's initials | "CV" |
| `{{unsubscribe_url}}` | Unsubscribe URL (only inside LOCKED) | — |

If a variable has no value for a specific recipient, it's substituted with an empty string — the HTML doesn't break, but "Hi , this..." looks odd. Either assume `firstname` is always present, or use "Hi {{firstname}}," with the comma.

### 3. Content placeholders (these you DO fill in)

Each master has placeholders in curly braces for editable content. They're listed per master at the end of this document.

### 4. Email client compatibility

Outlook (Windows) renders HTML with an old MSHTML engine. **DO NOT use:**

- ❌ Flexbox (`display: flex`)
- ❌ Grid (`display: grid`)
- ❌ `gap` on tables
- ❌ CSS variables (`var(--x)`)
- ❌ `position: absolute/relative`
- ❌ `aspect-ratio` (use fixed width/height)
- ❌ `text-wrap: balance`
- ❌ `@import` of Google Fonts (Gmail strips them)
- ❌ `<style>` blocks with complex rules (only basic media queries)
- ❌ `filter: brightness(0) invert(1)`
- ❌ Inline SVG (use PNG)

**Always use:**

- ✅ `<table role="presentation">` + `<tr>` + `<td>` for layout
- ✅ Inline CSS (`style="..."`)
- ✅ Fixed widths in `<td width="...">` and `<table width="...">`
- ✅ `<table>` for columns (not flex)
- ✅ PNG logos: black `https://v2charge.com/wp-content/uploads/2022/01/logotipo-v2c-black.png` · white `https://newsletter.v2charge.com/v2c-logo-white.png`
- ✅ Max container width: **600px**
- ✅ `@media screen and (max-width: 600px)` media query for mobile (this DOES go inside `<style>`)
- ✅ Hidden pre-header right after `<body>`

### 5. V2C brand identity

- **Typeface:** `'Montserrat', Arial, sans-serif`. Montserrat only renders in clients that load it; Arial is the fallback Outlook and Gmail use by default. Design font sizes assuming Arial.
- **Palette:**
  - Black: `#0E0E0E`
  - White: `#ffffff`
  - Light grey background: `#F4F4F2`
  - Very light grey background: `#F8F8F6`
  - Border grey: `#ECECEA`
  - Secondary text grey: `#7A7A78`
  - Body text grey: `#1F1F1F`
- **DO NOT use the V2C red** unless the briefing explicitly asks for it. The visual line of these templates is minimal B&W.
- Uppercase with `letter-spacing` on eyebrows and labels (editorial style).

### 6. Subject line

- Max **60 characters** (ideally 40–50).
- In the email's language.
- No spam triggers: ❌ ALL CAPS, ❌ `!!!`, ❌ "FREE", ❌ `$$$`, ❌ "urgent".
- Clear, specific hook — no clickbait.

Good examples:
- "Trydan Pro: in-person training in Madrid"
- "V2C training calendar — book your spot"
- "Installer Summit '26 — June 22nd in Valencia"

### 7. Hidden pre-header

Right after `<body>`:

```html
<span style="display:none;max-height:0;overflow:hidden;mso-hide:all;color:transparent;">
  [50-80 character text that appears as inbox preview]
</span>
```

The inbox shows subject + pre-header. Don't duplicate them — they complement each other.

---

## `output/campaign.json` schema

```json
{
  "name": "Internal name (not sent to recipients)",
  "from_name": "V2C",
  "from_email": "your@email.com",
  "reply_to": "your@email.com",
  "notes": "Optional explanation: decisions you made, what to review.",
  "versions": {
    "en": {
      "subject": "English subject line",
      "html": "<!DOCTYPE html>... full HTML in English ..."
    },
    "es": {
      "subject": "Spanish subject line",
      "html": "<!DOCTYPE html>... full HTML in Spanish ..."
    }
  }
}
```

**JSON rules:**

- `versions` has one key per language. ISO codes: `en`, `es`, `fr`, `it`, `pt`, `de`, `nl`.
- At least one version required.
- `html` is the complete document (`<!DOCTYPE html>...</html>`), not a fragment.
- LOCKED regions must remain intact with `{{unsubscribe_url}}` inside.

---

## Placeholders per master

### Editorial (`masters/editorial.html`)

| Placeholder | Description | Example |
|---|---|---|
| `{{lang}}` | Language code for `<html lang="...">` | "en" |
| `{{preheader}}` | Hidden pre-header text | "What's new in V2C training this month." |
| `{{edition_label}}` | Top-right label | "EDITION · MAY 2026" |
| `{{kicker}}` | Eyebrow above headline | "OFFICIAL INSTALLER PROGRAM" |
| `{{greeting}}` | Greeting word (incl. comma) | "Hi" or "Hola" |
| `{{headline}}` | Phrase after "{{greeting}} {{firstname}}, " | "this changes the way you install." |
| `{{hero_image_url}}` | Absolute hero image URL | `https://...png` |
| `{{hero_image_alt}}` | Hero image alt text | "V2C training session" |
| `{{hero_caption}}` | Small caption under hero | "Saltoki e-solar centers..." |
| `{{body_label}}` | Sidebar body label | "THE NOTE" |
| `{{body_html}}` | Body content (basic HTML allowed: `<b>`, `<br>`) | "We're launching..." |
| `{{meta_1_label}}` / `{{meta_1_value}}` | First meta (key / value) | "DURATION" / "4 hours" |
| `{{meta_2_label}}` / `{{meta_2_value}}` | Second meta | "FORMAT" / "In-person" |
| `{{meta_3_label}}` / `{{meta_3_value}}` | Third meta | "COST" / "Free" |
| `{{cta_url}}` | Primary button URL | `https://v2charge.com/...` |
| `{{cta_text}}` | Button text | "BOOK MY SPOT →" |
| `{{cta_subtext}}` | Text below button | "or reply to this email" |

### Data (`masters/data.html`)

| Placeholder | Description |
|---|---|
| `{{lang}}` | Language code for `<html lang="...">` |
| `{{preheader}}` | Hidden pre-header text |
| `{{badge_text}}` | Top-right badge — e.g. "PRODUCT UPDATE" |
| `{{hero_kicker}}` | Dark hero eyebrow — e.g. "NEW · TRYDAN V3" |
| `{{headline}}` | Big white headline — e.g. "More power,\nsame installation." |
| `{{greeting}}` | Greeting word — e.g. "Hi" |
| `{{hero_body}}` | Paragraph after "{{greeting}} {{firstname}}, " |
| `{{hero_image_url}}`, `{{hero_image_alt}}` | Hero image |
| `{{stat_N_value}}` / `{{stat_N_label}}` | 3 stats (N = 1, 2, 3) — e.g. "22 kW" / "MAX POWER" |
| `{{features_label}}` | Section label — e.g. "WHAT CHANGES FOR YOU" |
| `{{features_html}}` | HTML block with the features. Recommended structure per feature: `<table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0" style="border-top:1px solid #ECECEA;"><tr><td style="padding:14px 0;"><table><tr><td style="width:22px;"><div style="width:22px;height:22px;border-radius:11px;background:#0E0E0E;color:#fff;text-align:center;line-height:22px;font-size:12px;font-weight:700;">✓</div></td><td style="padding-left:14px;font-family:'Montserrat',Arial,sans-serif;"><div style="font-size:14px;font-weight:600;">Title</div><div style="font-size:13px;color:#5A5A58;margin-top:2px;">Description</div></td></tr></table></td></tr></table>` |
| `{{cta_primary_url}}` / `{{cta_primary_text}}` | Primary button — e.g. "VIEW DATASHEET" |
| `{{cta_secondary_url}}` / `{{cta_secondary_text}}` | Secondary button — e.g. "REQUEST DEMO UNIT" |

### Bold (`masters/bold.html`)

| Placeholder | Description |
|---|---|
| `{{lang}}` | Language code for `<html lang="...">` |
| `{{preheader}}` | Hidden pre-header text |
| `{{eyebrow}}` | Top-right label — e.g. "SAVE THE DATE" |
| `{{event_date_location}}` | Date + location — e.g. "22 · 06 · 2026 — VALENCIA" |
| `{{display_headline}}` | Giant display headline (can use `<br>` for line breaks) |
| `{{hero_image_url}}`, `{{hero_image_alt}}` | Hero image |
| `{{hero_caption_left}}` / `{{hero_caption_right}}` | Captions left/right — e.g. "City of Arts & Sciences" / "09:00 — 18:00" |
| `{{greeting}}` | Greeting word — e.g. "Hi" |
| `{{message_html}}` | Message after "{{greeting}} {{firstname}}, " |
| `{{schedule_html}}` | HTML block with the schedule. Structure per row: `<table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0" style="border-top:1px solid rgba(255,255,255,.08);"><tr><td style="padding:16px 0;width:70px;font-family:'Montserrat',Arial,sans-serif;font-size:13px;font-weight:700;color:#fff;">TIME</td><td style="padding:16px 0;font-family:'Montserrat',Arial,sans-serif;font-size:14px;color:rgba(255,255,255,.85);">Description</td><td style="padding:16px 0;width:18px;color:rgba(255,255,255,.3);text-align:right;">→</td></tr></table>` |
| `{{cta_url}}` / `{{cta_text}}` | Big white button — e.g. "CONFIRM ATTENDANCE →" |
| `{{cta_subtext}}` | Small text below button — e.g. "Limited spots for Official Installers" |

---

## Checklist before delivering

Before writing `output/campaign.json`, verify:

- [ ] The HTML is based on a master from `masters/`
- [ ] The `<!-- LOCKED -->...<!-- /LOCKED -->` regions are **identical** to the original master
- [ ] `{{unsubscribe_url}}` appears inside the LOCKED footer
- [ ] Handlebars variables are correctly written (`{{firstname}}` — not `{name}`, no spaces like `{{ firstname }}`)
- [ ] Hidden pre-header is present
- [ ] Subject < 60 characters, no spam triggers, correct language
- [ ] No `display: flex`, `grid`, `aspect-ratio`, `text-wrap: balance`
- [ ] Images have absolute URLs and `alt` text
- [ ] If multiple versions, all of them pass the checks above

---

## After generating

When done, explain to the user **in natural language**:

1. Which master you chose and why.
2. The main changes you made (subject, hero, CTA, etc.).
3. Any assumptions you made that the user should confirm (e.g. *"I assumed CTA points to `https://v2charge.com/training-madrid` — please confirm the URL is correct"*).
4. If translations were included, any nuances or differences you took per language.
5. **Tell them what to do with the JSON**: upload it to their compatible email platform, or export each language's HTML to use in another tool.
