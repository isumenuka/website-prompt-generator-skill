# Design System Tokens — Complete Reference Library

Use this file to quickly define precise, consistent design systems from image references.
Every number here is a sensible default — pick what matches the mood of the uploaded images.

---

## Table of Contents
1. [Color Palette Templates](#1-color-palette-templates)
2. [Typography Scale](#2-typography-scale)
3. [Google Fonts Quick Picks](#3-google-fonts-quick-picks)
4. [Spacing & Layout Tokens](#4-spacing--layout-tokens)
5. [Border Radius Tokens](#5-border-radius-tokens)
6. [Shadow & Elevation Tokens](#6-shadow--elevation-tokens)
7. [Motion Tokens](#7-motion-tokens)
8. [CSS Variable Templates](#8-css-variable-templates)
9. [Tailwind Config Extensions](#9-tailwind-config-extensions)

---

## 1. Color Palette Templates

### Dark Premium (Agency / Portfolio)
```css
:root {
  --bg:          #0A0A0A;
  --bg-surface:  #111111;
  --bg-elevated: #1A1A1A;
  --fg:          #FFFFFF;
  --fg-muted:    rgba(255,255,255,0.65);
  --fg-subtle:   rgba(255,255,255,0.35);
  --accent:      #22C55E;
  --accent-glow: rgba(34,197,94,0.3);
  --border:      rgba(255,255,255,0.08);
  --border-strong: rgba(255,255,255,0.16);
}
```

### Warm Editorial (Luxury / Fashion / Film)
```css
:root {
  --bg:          #F4F0EB;
  --bg-surface:  #EDE8E1;
  --bg-dark:     #1A1510;
  --fg:          #1A1510;
  --fg-muted:    rgba(26,21,16,0.6);
  --fg-inverse:  #F4F0EB;
  --accent:      #C8A96E;
  --accent-alt:  #8B4513;
  --border:      rgba(26,21,16,0.1);
}
```

### Tech / SaaS Dark (Indigo / Purple)
```css
:root {
  --bg:          #060611;
  --bg-surface:  #0D0D1F;
  --bg-card:     #12122A;
  --fg:          #E8EAF6;
  --fg-muted:    rgba(232,234,246,0.6);
  --accent:      #6366F1;
  --accent-2:    #8B5CF6;
  --accent-glow: rgba(99,102,241,0.35);
  --border:      rgba(99,102,241,0.15);
  --border-glow: rgba(99,102,241,0.4);
}
```

### Neon Dark (Gaming / Web3 / Crypto)
```css
:root {
  --bg:          #080808;
  --bg-surface:  #0F0F0F;
  --fg:          #FFFFFF;
  --fg-muted:    rgba(255,255,255,0.5);
  --accent-lime: #A3E635;
  --accent-cyan: #22D3EE;
  --accent-pink: #EC4899;
  --glow-lime:   rgba(163,230,53,0.4);
  --glow-cyan:   rgba(34,211,238,0.4);
  --border:      rgba(255,255,255,0.05);
}
```

### Clean Light (SaaS / Startup / Tool)
```css
:root {
  --bg:          #FAFAF8;
  --bg-surface:  #F4F4F2;
  --bg-dark:     #18181B;
  --fg:          #18181B;
  --fg-muted:    #71717A;
  --fg-subtle:   #A1A1AA;
  --accent:      #6366F1;
  --accent-2:    #F59E0B;
  --border:      #E4E4E7;
  --border-strong: #D4D4D8;
}
```

### Cinematic Film (Creative Portfolio)
```css
:root {
  --bg:          #0C0C0C;
  --bg-surface:  #101010;
  --bg-light:    #FFFFFF;
  --fg:          #D7E2EA;
  --fg-muted:    rgba(215,226,234,0.6);
  --fg-dark:     #0C0C0C;
  --accent-grad: linear-gradient(123deg, #18011F 7%, #B600A8 37%, #7621B0 72%, #BE4C00 100%);
  --border:      rgba(215,226,234,0.1);
}
```

---

## 2. Typography Scale

### Fluid Scale (clamp-based)
```css
--text-display: clamp(4rem, 14vw, 12rem);   /* hero wordmarks */
--text-hero:    clamp(3rem, 8vw, 7rem);      /* primary section titles */
--text-h1:      clamp(2rem, 5vw, 4.5rem);    /* section headings */
--text-h2:      clamp(1.5rem, 3.5vw, 3rem);  /* subheadings */
--text-h3:      clamp(1.25rem, 2.5vw, 2rem); /* card titles */
--text-body-lg: clamp(1rem, 1.8vw, 1.35rem); /* intro paragraphs */
--text-body:    clamp(0.875rem, 1.4vw, 1rem);/* body copy */
--text-sm:      clamp(0.75rem, 1.2vw, 0.875rem);
--text-xs:      0.75rem;                     /* labels / badges */
```

### Tailwind Equivalents
| Use case | Tailwind class |
|---|---|
| Full-bleed wordmark | `text-[20vw]` or `text-[clamp(3rem,18vw,15rem)]` |
| Large editorial hero | `text-6xl md:text-8xl lg:text-[7rem]` |
| Section heading | `text-4xl md:text-5xl lg:text-6xl` |
| Card title | `text-2xl md:text-3xl` |
| Intro paragraph | `text-lg md:text-xl` |
| Body copy | `text-sm md:text-base` |
| UI label | `text-xs md:text-sm` |
| Badge | `text-[10px] md:text-xs` |

---

## 3. Google Fonts Quick Picks

### Premium Serif
```html
<link href="https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400;1,700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400;1,600&display=swap" rel="stylesheet">
```

### Modern Sans
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,700;1,300;1,400&display=swap" rel="stylesheet">
```

### Display / Bold
```html
<link href="https://fonts.googleapis.com/css2?family=Barlow:ital,wght@0,300;0,400;0,500;0,600;0,700;0,900;1,300;1,400&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Kanit:ital,wght@0,300;0,400;0,700;0,900;1,400&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Almarai:wght@300;400;700;800&display=swap" rel="stylesheet">
```

### Monospace
```html
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
```

### Pairing Recommendations
| Heading | Body | Vibe |
|---|---|---|
| Instrument Serif (italic) | Barlow (300–600) | Premium agency |
| Playfair Display | DM Sans | Luxury editorial |
| Space Grotesk | Inter | Tech startup |
| Kanit | Kanit (different weights) | Portfolio / 3D creative |
| Almarai | Almarai | Creative studio |
| DM Serif Display | Plus Jakarta Sans | SaaS premium |
| Cormorant Garamond | Inter Light | Ultra-luxury |

---

## 4. Spacing & Layout Tokens

### Container widths
```css
--container-sm:  640px;
--container-md:  768px;
--container-lg:  1024px;
--container-xl:  1280px;
--container-2xl: 1440px;
```

### Section vertical padding
```
Tight:           py-12 md:py-16
Normal:          py-16 md:py-24
Generous:        py-24 md:py-32
Cinematic:       py-32 md:py-48
Ultra-spacious:  py-48 md:py-64
```

### Horizontal padding
```
Mobile:   px-4 sm:px-6
Standard: px-6 md:px-10
Wide:     px-8 md:px-16 lg:px-20
```

### Stack gap patterns
```
Badge → Headline: gap-4
Headline → Subtext: gap-6
Subtext → CTA: gap-8 or gap-10
Card grid: gap-3 (tight) / gap-6 (normal) / gap-8 (airy)
```

---

## 5. Border Radius Tokens

| Token | Value | Use |
|---|---|---|
| `rounded-none` | 0px | Sharp industrial, editorial |
| `rounded-lg` | 8px | Cards on light bg |
| `rounded-xl` | 12px | Standard cards |
| `rounded-2xl` | 16px | Premium cards, modals |
| `rounded-3xl` | 24px | Hero containers |
| `rounded-[2rem]` | 32px | Inset hero sections |
| `rounded-[40px]` | 40px | Project stacking cards |
| `rounded-full` | 9999px | Buttons, pills, badges, avatars |

### Usage guide
- Dark premium: `rounded-2xl` cards + `rounded-full` buttons
- Editorial: `rounded-none` or `rounded-sm`
- Playful startup: `rounded-2xl`/`rounded-3xl` cards + `rounded-full` everything else
- SaaS dashboard: `rounded-lg` or `rounded-xl` throughout

---

## 6. Shadow & Elevation Tokens

### Light theme
```css
/* Elevation 1 */ box-shadow: 0 1px 3px rgba(0,0,0,0.06), 0 1px 2px rgba(0,0,0,0.04);
/* Elevation 2 */ box-shadow: 0 4px 16px rgba(0,0,0,0.08), 0 2px 4px rgba(0,0,0,0.04);
/* Elevation 3 */ box-shadow: 0 10px 40px rgba(0,0,0,0.12), 0 4px 12px rgba(0,0,0,0.06);
/* Elevation 4 */ box-shadow: 0 20px 60px rgba(0,0,0,0.16), 0 8px 24px rgba(0,0,0,0.08);
```

### Dark theme
```css
/* Subtle */ box-shadow: 0 4px 24px rgba(0,0,0,0.4);
/* Deep product */ box-shadow: 0 20px 60px rgba(0,0,0,0.6), 0 4px 12px rgba(0,0,0,0.3);
```

### Glow shadows
```css
/* Green */ box-shadow: 0 0 24px rgba(34,197,94,0.5), 0 0 60px rgba(34,197,94,0.2);
/* Indigo */ box-shadow: 0 0 24px rgba(99,102,241,0.5), 0 0 60px rgba(99,102,241,0.25);
/* Pink */ box-shadow: 0 0 24px rgba(236,72,153,0.5), 0 0 60px rgba(236,72,153,0.2);
```

---

## 7. Motion Tokens

### Easing curves
```js
const EASE_SNAP     = [0.22, 1, 0.36, 1];  // snappy — interactive elements
const EASE_SMOOTH   = [0.16, 1, 0.3, 1];   // smooth — text reveals
const EASE_OUT      = "easeOut";            // classic fallback
const EASE_CINEMATIC = [0.76, 0, 0.24, 1]; // slow cinematic
const SPRING        = { type: "spring", stiffness: 300, damping: 20 };
const SPRING_SOFT   = { type: "spring", stiffness: 180, damping: 24 };
```

### Durations
```
Micro:      0.15s – 0.2s
Standard:   0.3s – 0.5s
Normal:     0.5s – 0.7s
Expressive: 0.7s – 1.0s
Cinematic:  1.0s – 1.5s
```

### Common Framer Motion variants
```js
const fadeUp = {
  initial: { opacity: 0, y: 24 },
  animate: { opacity: 1, y: 0 },
  transition: { duration: 0.6, ease: [0.22, 1, 0.36, 1] }
};

const blurFade = {
  initial: { opacity: 0, y: 20, filter: "blur(10px)" },
  animate: { opacity: 1, y: 0, filter: "blur(0px)" },
  transition: { duration: 0.7, ease: "easeOut" }
};

const scaleIn = {
  initial: { opacity: 0, scale: 0.94 },
  animate: { opacity: 1, scale: 1 },
  transition: { duration: 0.5, ease: [0.22, 1, 0.36, 1] }
};

const clipReveal = {
  initial: { clipPath: "inset(100% 0 0 0)" },
  animate: { clipPath: "inset(0% 0 0 0)" },
  transition: { duration: 0.7, ease: [0.76, 0, 0.24, 1] }
};

const inViewFadeUp = {
  initial: { opacity: 0, y: 32 },
  whileInView: { opacity: 1, y: 0 },
  viewport: { once: true, margin: "-80px" },
  transition: { duration: 0.6, ease: [0.22, 1, 0.36, 1] }
};
```

### Stagger delays
```js
// Card grid (3–4 items): 0.08–0.12s
// Nav items (5–7 items): 0.04–0.06s
// Stat row (2–4 items):  0.10–0.15s
// Hero elements (4–6):   0.15–0.20s
```

---

## 8. CSS Variable Templates

```css
:root {
  --color-bg:          #0A0A0A;
  --color-surface:     #111111;
  --color-elevated:    #1A1A1A;
  --color-fg:          #FFFFFF;
  --color-fg-muted:    rgba(255,255,255,0.65);
  --color-fg-subtle:   rgba(255,255,255,0.35);
  --color-accent:      #6366F1;
  --color-accent-glow: rgba(99,102,241,0.35);
  --color-border:      rgba(255,255,255,0.08);

  --font-display: 'Instrument Serif', serif;
  --font-body:    'Inter', sans-serif;
  --font-mono:    'JetBrains Mono', monospace;

  --text-display: clamp(4rem, 12vw, 10rem);
  --text-hero:    clamp(2.5rem, 7vw, 6rem);
  --text-section: clamp(1.5rem, 4vw, 3.5rem);
  --text-body:    clamp(0.875rem, 1.5vw, 1.0625rem);

  --space-section: clamp(4rem, 8vw, 8rem);
  --space-card:    clamp(1.5rem, 3vw, 2.5rem);

  --radius-sm:   8px;
  --radius-md:   12px;
  --radius-lg:   16px;
  --radius-xl:   24px;
  --radius-full: 9999px;

  --ease-snap:   cubic-bezier(0.22, 1, 0.36, 1);
  --ease-smooth: cubic-bezier(0.16, 1, 0.3, 1);
  --duration-fast: 0.2s;
  --duration-base: 0.45s;
  --duration-slow: 0.7s;
}
```

---

## 9. Tailwind Config Extensions

```js
module.exports = {
  theme: {
    extend: {
      colors: {
        bg:       '#0A0A0A',
        surface:  '#111111',
        elevated: '#1A1A1A',
        accent:   '#6366F1',
        primary:  '#DEDBC8',
      },
      fontFamily: {
        heading: ['"Instrument Serif"', 'serif'],
        body:    ['Inter', 'sans-serif'],
        display: ['Kanit', 'sans-serif'],
        mono:    ['"JetBrains Mono"', 'monospace'],
      },
      animation: {
        'fade-rise':         'fade-rise 0.8s ease-out both',
        'fade-rise-delayed': 'fade-rise 0.8s ease-out 0.3s both',
        'spin-slow':         'spin 8s linear infinite',
        'pulse-glow':        'pulse-glow 2s ease-in-out infinite',
      },
      keyframes: {
        'fade-rise': {
          from: { opacity: '0', transform: 'translateY(24px)' },
          to:   { opacity: '1', transform: 'translateY(0)' },
        },
        'pulse-glow': {
          '0%, 100%': { boxShadow: '0 0 20px rgba(99,102,241,0.4)' },
          '50%':       { boxShadow: '0 0 60px rgba(99,102,241,0.7)' },
        },
      },
      backgroundImage: {
        'gradient-radial': 'radial-gradient(var(--tw-gradient-stops))',
      },
    },
  },
};
```
