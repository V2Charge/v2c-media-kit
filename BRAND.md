# V2C Brand · Quick reference para email

Referencia rápida de la identidad V2C aplicada a estas plantillas. Para el manual completo, consulta [material gráfico oficial](https://v2charge.com/material-grafico).

## Paleta

| Uso | Hex | Notas |
|---|---|---|
| Negro principal | `#0E0E0E` | Texto, botones primarios, fondos dark |
| Blanco | `#ffffff` | Fondos light, texto sobre dark |
| Gris fondo claro | `#F4F4F2` | Body background en plantillas light |
| Gris fondo muy claro | `#F8F8F6` | Cards, secundarios sobre blanco |
| Gris bordes | `#ECECEA` | Separadores, borders |
| Gris texto secundario | `#7A7A78` | Captions, eyebrows, metadata |
| Gris texto cuerpo | `#1F1F1F` | Texto largo de body |

**Nota:** la línea visual de estas plantillas es B&W minimalista. El rojo histórico V2C (`#e30613`) no se usa por defecto. Si una campaña necesita un color de acento, consulta con el equipo de comunicación.

## Tipografía

- **Familia:** Montserrat (Google Fonts)
- **Fallback en email:** `'Montserrat', Arial, sans-serif`
- **Pesos usados:** 400 (regular), 600 (semibold), 700 (bold)

> En clientes de email que no cargan webfonts (Outlook, Gmail por defecto, Apple Mail con privacidad activa), el sistema usa Arial automáticamente. Diseña los tamaños asumiendo Arial — Montserrat es un nice-to-have.

### Tratamiento editorial

- **Eyebrows / labels** en mayúsculas, peso 600-700, con letter-spacing `0.14em` a `0.22em` según tamaño.
- **Titulares** en peso 700, letter-spacing negativo (`-0.025em` a `-0.045em` para los display grandes), line-height ajustado (`0.92` a `1.05`).
- **Cuerpo** en peso 400, line-height `1.6` a `1.7`.

## Logotipos

| Versión | URL | Uso |
|---|---|---|
| Negro | `https://v2charge.com/wp-content/uploads/2022/01/logotipo-v2c-black.png` | Plantillas light |
| Blanco | `https://newsletter.v2charge.com/v2c-logo-white.png` | Plantillas dark |
| SVG vectorial | [v2charge.com/material-grafico](https://v2charge.com/material-grafico) | Materiales fuera de email |

**Regla:** ancho típico en email = 56–64 px. No estires, no recolorees, no apliques `filter: brightness()` o `filter: invert()` (no funcionan en Gmail/Outlook).

## Iconos de redes sociales

URLs oficiales para usar en footers:

```
LinkedIn:  https://v2charge.com/wp-content/uploads/2023/06/v2c-linkedin.png
Instagram: https://v2charge.com/wp-content/uploads/2023/06/v2c-instagram.png
Facebook:  https://v2charge.com/wp-content/uploads/2023/06/v2c-facebook.png
X:         https://v2charge.com/wp-content/uploads/2026/05/twitter-x.png
YouTube:   https://v2charge.com/wp-content/uploads/2023/06/v2c-youtube.png
```

Tamaño recomendado en email: 14 × 14 px.

## Estándares de email

Estas plantillas siguen las mejores prácticas para máxima compatibilidad:

- Layout: `<table role="presentation">` (no flex, no grid)
- CSS inline obligatorio; solo se permiten `<style>` para media queries de móvil
- Ancho del contenedor: **600 px** (industry standard)
- Imágenes: URL absolutas, con `alt` text, formato PNG/JPG (no SVG inline)
- Fuentes web vía `<link>`: opcional (Outlook las ignora, Gmail también — siempre fallback a Arial)
- Pre-header oculto justo tras `<body>` para optimizar el preview del inbox
- Footer legal RGPD/LSSI con CIF, dirección y baja, marcado como región LOCKED

## Datos legales V2C

Pie obligatorio (no modificar):

```
V2C · CIF B98496706
Camí Nou 268, 46950 Xirivella, Valencia, España
https://v2charge.com/privacy-policy/
```
