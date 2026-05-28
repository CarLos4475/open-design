# Brand Spec — Sistema de Cifrado Matricial (Apple-style light + glass)

## Source
User direction change — Apple-style light design with glassmorphism.

## Color tokens (OKLch)

```css
--bg:        oklch(97% 0.004 240);   /* near-white cool background */
--surface:   oklch(100% 0 0);        /* pure white panels */
--glass:     oklch(100% 0 0 / 0.72); /* translucent glass surface */
--glass-alt: oklch(96% 0.005 240 / 0.6);
--fg:        oklch(18% 0.012 250);   /* near-black text */
--fg-muted:  oklch(45% 0.015 250);   /* secondary text */
--muted:     oklch(68% 0.01 250);    /* muted grey */
--border:    oklch(90% 0.008 250);   /* subtle borders */
--border-glass: oklch(100% 0 0 / 0.3);
--accent:    oklch(58% 0.20 255);    /* electric blue (Apple-style) */
--accent2:   oklch(70% 0.18 145);    /* neon green for valid states */
--shadow-sm: 0 1px 3px oklch(0% 0 0 / 0.06);
--shadow-md: 0 4px 16px oklch(0% 0 0 / 0.08);
--shadow-lg: 0 12px 40px oklch(0% 0 0 / 0.12);
```

## Typography

- **Display / Titles:** `-apple-system`, `BlinkMacSystemFont`, `SF Pro Display`, `Inter`, system-ui, sans-serif
- **Body:** `-apple-system`, `BlinkMacSystemFont`, `SF Pro Text`, `Inter`, system-ui, sans-serif
- **Mono / Code / Matrices:** `SF Mono`, `JetBrains Mono`, `IBM Plex Mono`, ui-monospace, Menlo, monospace

## Layout posture

- Light, airy background with subtle gradient mesh or blurred orbs
- Glass panels: `backdrop-filter: blur(20px) saturate(180%)` with translucent white surfaces
- Thin, subtle borders on glass (`rgba(255,255,255,0.3)`)
- Rounded corners (12–16px) on all panels and inputs
- Soft, layered shadows for depth hierarchy
- Electric blue primary actions, neon green for success/valid
- Tight letter-spacing on display sizes (-0.02em)
- Tabular numerics for matrix values
- Smooth, eased transitions with Apple-style spring physics feel
