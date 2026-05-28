# EcoRecicla — Brand Spec

## Color Tokens (OKLch approximations)

```css
:root {
  --bg:        oklch(97% 0.008 95);       /* #FAFAF8 — crudo blanco */
  --surface:   oklch(100% 0 0);            /* #FFFFFF */
  --fg:        oklch(22% 0.015 100);       /* #2C2C2A */
  --muted:     oklch(55% 0.012 100);       /* #888780 */
  --border:    oklch(85% 0.010 95);        /* #D3D1C7 */

  --green-400: oklch(58% 0.14 120);        /* #639922 — verde primario */
  --green-600: oklch(44% 0.12 120);        /* #3B6D11 — verde oscuro */
  --green-800: oklch(32% 0.10 120);        /* #27500A — verde muy oscuro */
  --green-50:  oklch(94% 0.03 120);        /* #EAF3DE */
  --green-100: oklch(86% 0.06 120);        /* #C0DD97 */

  --teal-400:  oklch(60% 0.12 170);        /* #1D9E75 */
  --teal-600:  oklch(44% 0.10 170);        /* #0F6E56 */
  --teal-50:   oklch(95% 0.025 170);       /* #E1F5EE */

  --amber-200: oklch(72% 0.14 70);         /* #EF9F27 */
  --amber-400: oklch(56% 0.12 70);         /* #BA7517 */
  --amber-50:  oklch(96% 0.025 70);        /* #FAEEDA */

  --accent:    oklch(58% 0.14 120);        /* --green-400 primary action */
  --accent-2:  oklch(60% 0.12 170);        /* --teal-400 secondary */
  --accent-3:  oklch(72% 0.14 70);         /* --amber-200 status/warm */

  --cream:     oklch(96% 0.008 95);        /* #F5F0E8 */
}
```

## Typography

- **Display / Headings:** `Playfair Display`, `Cormorant Garamond`, Georgia, serif — bold, editorial, large
- **Body:** `DM Sans`, `Inter`, -apple-system, sans-serif — weight 300–400, airy
- **Labels / Tags:** uppercase, letter-spacing 0.15em+, 10–12px, weight 700

## Layout Posture

- Magazine editorial: asymmetric grids (1/3 + 2/3 splits), varied card heights
- Sharp corners: `border-radius: 0` or max `4px`
- Fine horizontal rules (`1px solid`) as editorial separators
- Alternating backgrounds: white crudo → dark green → cream
- Large display typography on dark hero (magazine cover feel)
- Category tags styled as `[ PLÁSTICO ]`, `[ METAL ]`
- Numbered article markers: `01 / 02 / 03`
- Subtle scroll animations (fade + translateY)
- Card hover: slight image zoom + color overlay

## Product Context

- Recycling rewards platform for CDMX citizens
- EcoPuntos system: plastic 5pts/100g, glass 4pts, paper 3pts, metal 8pts, organic 2pts, electronics 20pts/piece
- Green Points (collection centers) across CDMX delegations
- Admin panel with CRUD for users, points, deliveries
- Hackathon CDMX 2026
