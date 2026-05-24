# Guía para asistentes IA · V2C Email Templates

Esta guía está dirigida a **asistentes de IA** (Claude, GPT, Cursor, Copilot…) que ayudan a adaptar las plantillas de email V2C para una comunicación concreta.

Si eres un desarrollador o partner adaptando una plantilla a mano, también te servirá como referencia técnica.

---

## Tu misión

Dado un briefing en lenguaje natural (lo que el usuario quiere comunicar), producir un archivo `output/campaign.json` con:

- El HTML adaptado de una de las tres plantillas maestras (`masters/editorial.html`, `data.html`, `bold.html`)
- Asunto en cada idioma solicitado
- Versiones traducidas si el briefing menciona varios idiomas
- Notas explicativas para que el usuario sepa qué decisiones tomaste

El JSON resultante se puede subir a una plataforma de envío compatible (formato detallado más abajo).

---

## Flujo

1. Lee el briefing del usuario.
2. Elige la maestra que mejor encaja (o usa la que el usuario te indique).
3. Adapta el HTML rellenando los placeholders de contenido (sección "Variables").
4. Si hay varios idiomas, traduce el resultado.
5. Genera asuntos atractivos por idioma (máx 60 caracteres, sin spam triggers).
6. Escribe `output/campaign.json` con el schema indicado.
7. Explica al usuario qué decisiones tomaste y qué debería revisar antes de enviar.

---

## Reglas innegociables

### 1. NO toques las regiones LOCKED

Cualquier bloque entre `<!-- LOCKED -->` y `<!-- /LOCKED -->` se copia **literal**. Contiene el footer legal obligatorio por RGPD/LSSI (CIF, dirección, política de privacidad, enlace de baja). Modificarlo es ilegal y rompe el mecanismo de bajas.

### 2. Variables Handlebars — no inventes nuevas

Estas variables se sustituyen al enviar, **una por destinatario**. No las cambies, no inventes otras nuevas.

| Variable | Origen típico | Ejemplo |
|---|---|---|
| `{{firstname}}` | Nombre del destinatario | "Pedro" |
| `{{lastname}}` | Apellido del destinatario | "García" |
| `{{fullname}}` | Nombre completo | "Pedro García" |
| `{{email}}` | Email del destinatario | "pedro@cliente.com" |
| `{{company}}` | Empresa | "Acme S.L." |
| `{{owner_firstname}}` | Nombre del responsable de cuenta | "Carlos" |
| `{{owner_lastname}}` | Apellido del responsable | "Vidal" |
| `{{owner_email}}` | Email del responsable | "carlos@v2charge.com" |
| `{{owner_initials}}` | Iniciales del responsable | "CV" |
| `{{unsubscribe_url}}` | URL de baja (solo dentro de LOCKED) | — |

Si una variable no tiene valor para un destinatario concreto, se sustituye por cadena vacía — el HTML no se rompe, pero "Hola , esto..." queda raro. Asume `firstname` siempre presente o usa "Hola {{firstname}}," con coma.

### 3. Placeholders de contenido (estos SÍ los rellenas)

Cada maestra tiene placeholders entre llaves para el contenido editable. Los listo por maestra al final.

### 4. Compatibilidad de clientes de email

Outlook (Windows) renderiza con un motor MSHTML antiguo. **NO uses:**

- ❌ Flexbox (`display: flex`)
- ❌ Grid (`display: grid`)
- ❌ `gap` en tablas
- ❌ CSS variables (`var(--x)`)
- ❌ `position: absolute/relative`
- ❌ `aspect-ratio` (usa width/height fijos)
- ❌ `text-wrap: balance`
- ❌ `@import` de Google Fonts (Gmail los elimina)
- ❌ `<style>` con reglas complejas (solo media queries básicas)
- ❌ `filter: brightness(0) invert(1)`
- ❌ SVG inline (usa PNG)

**Usa siempre:**

- ✅ Layout con `<table role="presentation">` + `<tr>` + `<td>`
- ✅ CSS inline (`style="..."`)
- ✅ Anchos fijos en `<td width="...">` y `<table width="...">`
- ✅ `<table>` para columnas (no flex)
- ✅ Logos PNG: negro `https://v2charge.com/wp-content/uploads/2022/01/logotipo-v2c-black.png` · blanco `https://newsletter.v2charge.com/v2c-logo-white.png`
- ✅ Ancho del contenedor: **600px** máximo
- ✅ Media query `@media screen and (max-width: 600px)` para móvil (esto sí va dentro de `<style>`)
- ✅ Pre-header oculto después del `<body>`

### 5. Identidad de marca V2C

- **Tipografía:** `'Montserrat', Arial, sans-serif`. Montserrat solo renderiza en clientes que la carguen; el fallback Arial es lo que ven Outlook y Gmail por defecto. Diseña tamaños asumiendo Arial.
- **Paleta:**
  - Negro: `#0E0E0E`
  - Blanco: `#ffffff`
  - Gris fondo claro: `#F4F4F2`
  - Gris fondo muy claro: `#F8F8F6`
  - Gris bordes: `#ECECEA`
  - Gris texto secundario: `#7A7A78`
  - Gris cuerpo: `#1F1F1F`
- **NO uses el rojo V2C** salvo que el briefing lo pida explícitamente. La línea visual de estas plantillas es B&W minimalista.
- Mayúsculas con `letter-spacing` en eyebrows/labels (estilo editorial).

### 6. Asunto (subject)

- Máximo **60 caracteres** (idealmente 40–50).
- En el idioma del email.
- Sin spam triggers: ❌ MAYÚSCULAS, ❌ `!!!`, ❌ "GRATIS"/"FREE", ❌ `$$$`, ❌ "urgente".
- Gancho claro y específico, sin clickbait.

Buenos ejemplos:
- "Nuevo Trydan Pro: formación presencial en Madrid"
- "Calendario de formaciones V2C - reserva tu plaza"
- "Installer Summit '26 - 22 junio en Valencia"

### 7. Pre-header oculto

Justo después del `<body>`:

```html
<span style="display:none;max-height:0;overflow:hidden;mso-hide:all;color:transparent;">
  [Texto 50-80 caracteres que aparece como preview en el inbox]
</span>
```

El inbox muestra asunto + pre-header. No los dupliques, complementan.

---

## Schema del `output/campaign.json`

```json
{
  "name": "Nombre interno (no se envía al destinatario)",
  "from_name": "V2C",
  "from_email": "tu@email.com",
  "reply_to": "tu@email.com",
  "notes": "Explicación opcional: qué decisiones tomaste, qué revisar.",
  "versions": {
    "es": {
      "subject": "Asunto en español",
      "html": "<!DOCTYPE html>... HTML completo en español ..."
    },
    "fr": {
      "subject": "Sujet en français",
      "html": "<!DOCTYPE html>... HTML complet ..."
    }
  }
}
```

**Reglas del JSON:**

- `versions` tiene una clave por idioma. Códigos ISO: `es`, `fr`, `it`, `pt`, `de`, `nl`, `en`.
- Al menos una versión obligatoria.
- `html` es el documento completo (`<!DOCTYPE html>...</html>`), no un fragmento.
- Las regiones LOCKED deben estar intactas con `{{unsubscribe_url}}` dentro.

---

## Placeholders por maestra

### Editorial (`masters/editorial.html`)

| Placeholder | Descripción | Ejemplo |
|---|---|---|
| `{{edition_label}}` | Etiqueta superior derecha | "EDICIÓN · MAYO 2026" |
| `{{kicker}}` | Eyebrow sobre el titular | "PROGRAMA OFFICIAL INSTALLER" |
| `{{headline}}` | Frase después de "Hola {{firstname}}, " | "esto cambia tu manera de instalar." |
| `{{hero_image_url}}` | URL absoluta del hero | `https://...png` |
| `{{hero_image_alt}}` | Alt text del hero | "Sesión de formación V2C" |
| `{{hero_caption}}` | Pie de foto pequeño | "Centros Saltoki e-solar..." |
| `{{body_label}}` | Etiqueta lateral del cuerpo | "LA NOTA" |
| `{{body_html}}` | Cuerpo del mensaje (HTML interno permitido: `<b>`, `<br>`) | "Lanzamos un calendario..." |
| `{{meta_1_label}}` / `{{meta_1_value}}` | Primera meta (clave / valor) | "DURACIÓN" / "4 horas" |
| `{{meta_2_label}}` / `{{meta_2_value}}` | Segunda meta | "FORMATO" / "Presencial" |
| `{{meta_3_label}}` / `{{meta_3_value}}` | Tercera meta | "COSTE" / "Gratuito" |
| `{{cta_url}}` | URL del botón principal | `https://v2charge.com/...` |
| `{{cta_text}}` | Texto del botón | "RESERVAR MI PLAZA →" |
| `{{cta_subtext}}` | Texto bajo el botón | "o responde a este correo" |

### Data (`masters/data.html`)

| Placeholder | Descripción |
|---|---|
| `{{preheader}}` | Texto del pre-header oculto |
| `{{badge_text}}` | Badge superior derecho | "PRODUCT UPDATE" |
| `{{hero_kicker}}` | Eyebrow del hero dark | "NUEVO · TRYDAN V3" |
| `{{headline}}` | Titular grande blanco | "Más potencia,\nmisma instalación." |
| `{{hero_body}}` | Párrafo tras "{{firstname}}, " | "te adelantamos las novedades..." |
| `{{hero_image_url}}`, `{{hero_image_alt}}` | Hero image |
| `{{stat_N_value}}` / `{{stat_N_label}}` | 3 stats (N = 1, 2, 3) | "22 kW" / "POTENCIA MÁX." |
| `{{features_label}}` | Etiqueta de la sección | "LO QUE CAMBIA PARA TI" |
| `{{features_html}}` | Bloque HTML con las features. Estructura recomendada por feature: `<table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0" style="border-top:1px solid #ECECEA;"><tr><td style="padding:14px 0;"><table><tr><td style="width:22px;..."><div style="width:22px;height:22px;border-radius:11px;background:#0E0E0E;color:#fff;text-align:center;line-height:22px;font-size:12px;font-weight:700;">✓</div></td><td style="padding-left:14px;font-family:..."><div style="font-size:14px;font-weight:600;">Título</div><div style="font-size:13px;color:#5A5A58;margin-top:2px;">Descripción</div></td></tr></table></td></tr></table>` |
| `{{cta_primary_url}}` / `{{cta_primary_text}}` | Botón principal | "VER FICHA TÉCNICA" |
| `{{cta_secondary_url}}` / `{{cta_secondary_text}}` | Botón secundario | "PEDIR UNIDAD DEMO" |

### Bold (`masters/bold.html`)

| Placeholder | Descripción |
|---|---|
| `{{preheader}}` | Texto del pre-header oculto |
| `{{eyebrow}}` | Etiqueta superior derecha | "SAVE THE DATE" |
| `{{event_date_location}}` | Fecha + lugar | "22 · 06 · 2026 — VALENCIA" |
| `{{display_headline}}` | Titular display gigante (puede usar `<br>` para saltos) |
| `{{hero_image_url}}`, `{{hero_image_alt}}` | Hero image |
| `{{hero_caption_left}}` / `{{hero_caption_right}}` | Pies de foto a izq/der | "City of Arts & Sciences" / "09:00 — 18:00" |
| `{{message_html}}` | Mensaje después de "{{firstname}}, " |
| `{{schedule_html}}` | Bloque HTML del programa. Estructura por fila: `<table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0" style="border-top:1px solid rgba(255,255,255,.08);"><tr><td style="padding:16px 0;width:70px;font-family:'Montserrat',Arial,sans-serif;font-size:13px;font-weight:700;color:#fff;">HORA</td><td style="padding:16px 0;font-family:...;font-size:14px;color:rgba(255,255,255,.85);">Descripción</td><td style="padding:16px 0;width:18px;color:rgba(255,255,255,.3);text-align:right;">→</td></tr></table>` |
| `{{cta_url}}` / `{{cta_text}}` | Botón blanco grande | "CONFIRMAR ASISTENCIA →" |
| `{{cta_subtext}}` | Texto pequeño bajo el botón | "Plazas limitadas a..." |

---

## Checklist antes de entregar

Antes de escribir `output/campaign.json`, verifica:

- [ ] El HTML está basado en una maestra de `masters/`
- [ ] Las regiones `<!-- LOCKED -->...<!-- /LOCKED -->` están **idénticas** a la maestra original
- [ ] `{{unsubscribe_url}}` aparece dentro del LOCKED footer
- [ ] Variables Handlebars bien escritas (`{{firstname}}` no `{nombre}`, ni con espacios `{{ firstname }}`)
- [ ] Hay pre-header oculto
- [ ] Asunto < 60 caracteres, sin spam triggers, en el idioma correcto
- [ ] No hay `display: flex`, `grid`, `aspect-ratio`, `text-wrap: balance`
- [ ] Imágenes con URLs absolutas y `alt` text
- [ ] Si hay varias versiones, todas cumplen los puntos anteriores

---

## Después de generar

Al terminar, explica al usuario **en lenguaje natural**:

1. Qué maestra elegiste y por qué.
2. Qué cambios principales hiciste (asunto, hero, CTA, etc.).
3. Qué supuestos hiciste que el usuario debería confirmar (ej. *"Asumí CTA a `https://v2charge.com/formacion-madrid` — confirma que la URL es correcta"*).
4. Si hay traducciones, qué matices/diferencias tomaste por cada idioma.
5. **Indícale qué hacer con el JSON**: subirlo a su plataforma de email compatible, o exportar el HTML de cada idioma para usarlo en otra herramienta.
