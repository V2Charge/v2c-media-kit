# V2C Media Kit · Email

Sistema de diseño de email oficial V2C. Plantillas, identidad y guías para uso por **V2C Official Installers**, distribuidores autorizados, partners de comunicación, agencias y medios.

Este repositorio complementa el [material gráfico oficial V2C](https://v2charge.com/material-grafico) (logos, vídeos, manual de identidad) con el componente específico de email.

---

## ¿Qué contiene?

Tres plantillas de email HTML listas para producción, basadas en la identidad visual V2C:

| Plantilla | Uso recomendado | Estilo |
|---|---|---|
| **Editorial** | Newsletters, comunicados periódicos | Magazine refinado, fondo claro, mucho aire |
| **Data** | Anuncios de producto, actualizaciones técnicas | Stats + features + firma del responsable |
| **Bold** | Eventos, lanzamientos, invitaciones | Dark, dramático, foco en una sola idea |

Todas las plantillas siguen los estándares de email marketing profesional: layout en `<table>`, CSS inline, ancho 600 px, compatibilidad con Outlook, Gmail, Apple Mail y clientes móviles, footer legal RGPD/LSSI y soporte para personalización por destinatario.

---

## ¿A quién va dirigido?

- 🔧 **V2C Official Installers** que quieren comunicar a su cartera de clientes manteniendo coherencia con la marca V2C.
- 📦 **Distribuidores** autorizados que envían comunicaciones sobre producto V2C.
- 🎨 **Agencias y partners** de comunicación que diseñan campañas para V2C.
- 📰 **Prensa y medios** que necesitan materiales de referencia visual.

---

## Empezar

### Opción A — Descarga directa

Clica el botón verde **"Code"** arriba a la derecha → **"Download ZIP"**. Te llevas las plantillas, las personalizas en tu editor HTML favorito, y las usas en tu plataforma de envío habitual (Mailchimp, HubSpot, Brevo, Resend, etc.).

### Opción B — Git (recomendado si lo vas a usar varias veces)

```bash
git clone https://github.com/V2Charge/v2c-media-kit.git
cd v2c-media-kit
```

### Opción C — Asistido por IA (más rápido)

Si trabajas habitualmente con un asistente de IA (Claude, ChatGPT, Cursor, Copilot…), abre la carpeta en tu editor con plugin de IA y pídele en lenguaje natural:

> *"Adapta la maestra Editorial para anunciar una formación presencial sobre Trydan Pro el 15 de junio en Madrid, CTA a registrarse. Idiomas español y francés."*

El archivo [`CLAUDE.md`](./CLAUDE.md) le enseña a la IA cómo respetar la identidad V2C, mantener el footer legal intacto y producir HTML email-compatible. Es una guía pensada para LLMs pero también es una buena referencia técnica si lo haces a mano.

---

## Estructura

```
masters/
  editorial.html     ← Plantilla A
  data.html          ← Plantilla B
  bold.html          ← Plantilla C
examples/
  campaign.example.json
output/              ← Donde dejas tu trabajo personalizado (vacío por defecto)
CLAUDE.md            ← Guía técnica para asistentes IA y desarrolladores
README.md
```

---

## Personalización

Cada plantilla usa **variables Handlebars** (`{{firstname}}`, `{{cta_url}}`, etc.) que puedes:

- **Sustituir manualmente** antes de enviar el correo (busca y reemplaza)
- **Dejarlas tal cual** si tu plataforma de envío soporta merge tags Handlebars (Resend, HubSpot Marketing Email, Mailchimp con conversión, etc.)
- **Generar un JSON estructurado** con tu asistente de IA listo para subir a una plataforma compatible

Variables comunes:

| Variable | Significado |
|---|---|
| `{{firstname}}` | Nombre del destinatario |
| `{{lastname}}` | Apellido del destinatario |
| `{{company}}` | Empresa del destinatario |
| `{{owner_firstname}}` | Tu nombre (o el del responsable de cuenta) |
| `{{owner_email}}` | Tu email de contacto |
| `{{cta_url}}` | URL del botón principal |
| `{{unsubscribe_url}}` | URL de baja de la lista (obligatorio por RGPD) |

Lista completa con todos los placeholders de contenido en [`CLAUDE.md`](./CLAUDE.md).

---

## Identidad visual

Estas plantillas siguen el [manual de identidad corporativa V2C](https://v2charge.com/material-grafico). Resumen rápido:

- **Tipografía:** Montserrat (con fallback Arial para email)
- **Paleta:** Negro `#0E0E0E`, blanco `#ffffff`, grises `#F4F4F2` / `#ECECEA` / `#7A7A78`
- **Logos:** [versión negra](https://v2charge.com/wp-content/uploads/2022/01/logotipo-v2c-black.png) · [versión blanca](https://newsletter.v2charge.com/v2c-logo-white.png) · [SVG vectorial](https://v2charge.com/material-grafico)
- **Tono:** B&W minimalista, editorial, mayúsculas con letter-spacing en eyebrows

---

## Footer legal

Todas las plantillas incluyen un **bloque de footer legal** marcado con comentarios `<!-- LOCKED -->...<!-- /LOCKED -->`. Contiene:

- CIF B98496706
- Domicilio: Camí Nou 268, 46950 Xirivella, Valencia
- Enlace a la [política de privacidad](https://v2charge.com/privacy-policy/)
- Variable de baja (`{{unsubscribe_url}}`)
- Iconos de redes sociales V2C

**No modifiques este bloque** — es obligatorio por RGPD/LSSI y la baja debe funcionar técnicamente. Si necesitas adaptarlo (cambiar la dirección si eres un distribuidor en otro país, por ejemplo), contacta primero con el equipo de comunicaciones V2C.

---

## Licencia y uso

Estas plantillas son **propiedad de V2C** y se ofrecen libremente para uso por:

- V2C Official Installers en sus comunicaciones a clientes finales
- Distribuidores autorizados V2C
- Agencias y partners contratados por V2C
- Prensa y medios para referencia

No se permite el uso por terceros no autorizados ni la modificación del logo, footer legal o identidad de marca. Para usos comerciales fuera de los anteriores, contacta con el equipo de comunicaciones V2C.

---

## Contacto

Para añadir nuevas plantillas, corregir algo, o cualquier consulta sobre identidad de marca:

📧 **comunicacion@v2charge.com** — equipo de Comunicación y Marketing V2C
🌐 **[v2charge.com/material-grafico](https://v2charge.com/material-grafico)** — todo el material gráfico oficial

---

<details>
<summary><sub>Información para el equipo V2C</sub></summary>

<br>

Si formas parte del equipo V2C (Official Installer, distribuidor, comunicación interna), tienes acceso a la plataforma de envío interna donde puedes subir el `output/campaign.json` directamente, elegir tu segmento de contactos en HubSpot, y enviar — sin tocar HTML.

Pídele acceso a tu responsable o consulta el portal interno.

</details>

---

<sub>V2C · CIF B98496706 · Camí Nou 268, 46950 Xirivella, Valencia, España</sub>
