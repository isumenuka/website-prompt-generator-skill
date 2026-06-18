# UI Analysis System — How to Read Images Like a Designer

Read this file when analyzing uploaded reference images before generating a blueprint.
This system ensures you extract *every technically useful signal* from an image — not just mood words.

---

## Table of Contents
1. [Layout Decoding](#1-layout-decoding)
2. [Color Extraction](#2-color-extraction)
3. [Typography Reading](#3-typography-reading)
4. [Surface & Material Analysis](#4-surface--material-analysis)
5. [Spacing & Density Estimation](#5-spacing--density-estimation)
6. [Component Identification](#6-component-identification)
7. [Motion Inference](#7-motion-inference)
8. [Image Placement Spec](#8-image-placement-spec)
9. [Quick Analysis Checklist](#9-quick-analysis-checklist)

---

## 1. Layout Decoding

### Grid Detection
Look for these patterns and name them precisely:

| What you see | What to call it | Tailwind equivalent |
|---|---|---|
| Single centered column | Stack layout | `flex flex-col items-center` |
| Two columns side by side | 2-col split | `grid grid-cols-2` or `flex` |
| Three equal cards in a row | 3-col card grid | `grid grid-cols-3 gap-N` |
| Cards with one wide + two narrow | Asymmetric grid | `grid grid-cols-[2fr_1fr_1fr]` |
| Content pinned to left, visual right | Feature split | `flex justify-between` |
| Overlapping layered elements | Z-stack / hero stack | `relative` + `absolute` children |
| Content at bottom of full-height section | Bottom-anchored | `flex flex-col justify-end` |
| Nav bar running across the very top | Fixed header | `fixed top-0 w-full z-50` |

### Alignment Signals
- Text centered over a visual → `text-center` + `mx-auto`
- Text left-aligned with right-side image → `grid grid-cols-2`, text in col 1
- Elements all flush left → `items-start` or `text-left`
- Button aligned bottom-right of a card → `mt-auto ml-auto` or `absolute bottom-4 right-4`

### Focal Point
Identify where the eye goes first. That element gets:
- The biggest `font-size`
- Highest contrast
- Most padding/breathing room around it
- First animation (delay 0s or shortest delay)

---

## 2. Color Extraction

### Step-by-step color reading

**Background color** — Look at the dominant area with no content:
- Near-black (#0A0A0A → #1A1A1A) = "premium dark"
- Warm off-white (#F4F0EB, #FAFAF8) = "editorial light"
- Pure white (#FFFFFF) = "clean/SaaS"
- Navy/deep blue (#0B1929, #0D1B2A) = "tech/data"
- Saturated vivid (pure purple, electric blue) = "bold brand"

**Text color** — Check heading vs body:
- Pure white on dark = `#FFFFFF` or `text-white`
- Warm cream on dark = `#E8E0D5` or `#D7E2EA`
- Charcoal on light = `#1A1A1A`, `#111`, or `#0C0C0C`
- Muted body text = usually 60–80% opacity of heading color → `text-white/70` or `rgba(255,255,255,0.7)`

**Accent color** — The color that pops on everything else:
- Look for CTAs, active states, highlights, underlines, glow
- Name it with hex: `--accent: #22C55E` (green), `--accent: #6366F1` (indigo), etc.
- If there's a gradient CTA, capture the full `linear-gradient()` stops

**Glow / ambient color** — Soft colored light behind a hero element:
- Usually a radial-gradient with low opacity: `radial-gradient(ellipse at 50% 0%, rgba(99,102,241,0.3) 0%, transparent 70%)`
- Or a CSS `box-shadow: 0 0 80px rgba(accent, 0.4)` on an element

### Common palettes to recognize quickly

| Palette name | BG | FG | Accent | Vibe |
|---|---|---|---|---|
| Liquid Glass Dark | `#000` | `#fff` | white/translucent | Apple-tier premium |
| Warm Editorial | `#F4F0EB` | `#1A1A1A` | dusty rose / terracotta | Magazine / luxury |
| Tech Indigo | `#080B14` | `#E8EAF6` | `#6366F1` | SaaS / AI platform |
| Neon Dark | `#080808` | `#fff` | lime `#A3E635` or cyan `#22D3EE` | Gaming / crypto |
| Soft Neutral | `#FAFAF8` | `#111` | `#18181B` | Minimal / startup |
| Cinematic Film | `#0C0C0C` | `#D7E2EA` | gradient purple→pink | Portfolio / creative |

---

## 3. Typography Reading

### Font identification from an image

**Serif indicators** (pointed brackets, variable stroke width, serifs on letterforms):
- Heavy editorial serif → Playfair Display, Cormorant Garamond, Instrument Serif
- Elegant italic serif → Instrument Serif italic, EB Garamond
- Slab serif (chunky uniform serifs) → DM Serif Display, Libre Baskerville

**Sans-serif indicators** (no serifs, uniform strokes):
- Geometric/clean → Inter, DM Sans, Outfit, Plus Jakarta Sans
- Condensed/narrow → Barlow Condensed, Space Grotesk
- Wide tracking uppercase → Montserrat, Bebas Neue (display)
- Technical/monospace → JetBrains Mono, IBM Plex Mono, Space Mono

**Weight reading**:
- Hairline text (very thin) → `font-thin` (100) or `font-extralight` (200)
- Light body text → `font-light` (300)
- Default paragraph → `font-normal` (400)
- Medium UI labels → `font-medium` (500)
- Subheadings → `font-semibold` (600)
- Headings → `font-bold` (700)
- Hero display → `font-extrabold` (800) or `font-black` (900)

### Size estimation
If you can't measure exact px, use these reference anchors:
- Body copy (readable paragraph) ≈ 14–16px → `text-sm` or `text-base`
- UI labels, nav items ≈ 12–14px → `text-xs` or `text-sm`
- Section subheadings ≈ 20–28px → `text-xl` to `text-3xl`
- Section headings ≈ 36–64px → `text-4xl` to `text-6xl`
- Hero display (fills most of width) → `text-[clamp(3rem,12vw,9rem)]` or `text-[15vw]`
- Full-bleed wordmark touching edges → `text-[20vw]` to `text-[26vw]`

### Tracking and leading
- Letters packed very tightly → `tracking-tight` or `tracking-[-0.04em]`
- Normal → `tracking-normal`
- Spaced out (uppercase labels) → `tracking-wider` or `tracking-widest`
- Lines feel cramped (headlines) → `leading-none` (1.0) or `leading-tight` (1.1)
- Lines feel open (body) → `leading-relaxed` (1.6) or `leading-loose` (2.0)
- Specific: `leading-[0.85]` for very tight display stacks

### Text transformation
- ALL CAPS → `uppercase`
- Sentence case → `normal-case` (default)
- Mixed case label that looks like a badge → might be `capitalize`

---

## 4. Surface & Material Analysis

Match what you see to the correct CSS treatment:

### Frosted Glass / Glassmorphism
**Visual cue**: A panel that lets blurred background show through, with a subtle white rim.
```css
/* Standard glassmorphism */
background: rgba(255, 255, 255, 0.08);
backdrop-filter: blur(16px);
-webkit-backdrop-filter: blur(16px);
border: 1px solid rgba(255, 255, 255, 0.12);
border-radius: 16px;
```
**Tailwind shorthand**: `bg-white/10 backdrop-blur-xl border border-white/10 rounded-2xl`

### Liquid Glass (Apple-style, advanced)
**Visual cue**: Extremely minimal fill, glowing top/bottom border, deeper blur.
```css
.liquid-glass {
  background: rgba(255, 255, 255, 0.01);
  background-blend-mode: luminosity;
  backdrop-filter: blur(4px);
  border: none;
  box-shadow: inset 0 1px 1px rgba(255, 255, 255, 0.1);
  position: relative;
  overflow: hidden;
}
.liquid-glass::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1.4px;
  background: linear-gradient(180deg,
    rgba(255,255,255,0.45) 0%, rgba(255,255,255,0.15) 20%,
    rgba(255,255,255,0) 40%, rgba(255,255,255,0) 60%,
    rgba(255,255,255,0.15) 80%, rgba(255,255,255,0.45) 100%);
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
}
```

### Noise Texture Overlay
**Visual cue**: Subtle grain over a flat background, like film grain or paper texture.
```css
.noise-overlay::after {
  content: "";
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.08'/%3E%3C/svg%3E");
  opacity: 0.12;
  mix-blend-mode: overlay;
  pointer-events: none;
}
```

### Gradient Backgrounds
```css
/* Radial glow (often behind a hero element) */
background: radial-gradient(ellipse at 50% 0%, rgba(99,102,241,0.35) 0%, transparent 65%);

/* Directional gradient (hero section) */
background: linear-gradient(135deg, #0B0B1E 0%, #1a0533 50%, #0B0B1E 100%);

/* Edge fade (for section transitions) */
background: linear-gradient(to bottom, transparent 0%, #000 100%);
```

### Dotted / Grid Backgrounds
```css
/* Dot grid */
background-image: radial-gradient(circle, rgba(255,255,255,0.15) 1px, transparent 1px);
background-size: 24px 24px;

/* Line grid */
background-image: linear-gradient(rgba(255,255,255,0.05) 1px, transparent 1px),
                  linear-gradient(90deg, rgba(255,255,255,0.05) 1px, transparent 1px);
background-size: 32px 32px;
```

### Hard Shadow
```css
box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4), 0 4px 12px rgba(0, 0, 0, 0.2);
```

### Soft Glow (Neon/accent)
```css
box-shadow: 0 0 24px rgba(99, 102, 241, 0.6), 0 0 60px rgba(99, 102, 241, 0.3);
```

### Border Treatments
- Hairline white border on dark → `border border-white/10`
- Thick accent border → `border-2 border-[#6366F1]`
- Gradient border:
```css
background: linear-gradient(#0B0B1E, #0B0B1E) padding-box,
            linear-gradient(135deg, #6366F1, #EC4899) border-box;
border: 1px solid transparent;
```

---

## 5. Spacing & Density Estimation

### Padding inside elements
- Cramped (badge/chip) → `px-3 py-1` or `px-4 py-1.5`
- Compact (small button) → `px-4 py-2`
- Normal (standard button) → `px-6 py-3` or `px-8 py-3`
- Generous (hero CTA) → `px-10 py-4` or `px-12 py-4`
- Card internal padding (tight) → `p-4` or `p-5`
- Card internal padding (comfortable) → `p-6` to `p-8`
- Card internal padding (airy) → `p-10` to `p-12`

### Section spacing
- Tight/dense → `py-12` to `py-16`
- Normal → `py-20` to `py-24`
- Generous cinematic → `py-28` to `py-40`
- Ultra-spacious editorial → `py-48` to `py-64`

### Gap between elements
- Between grid cards → `gap-3` to `gap-6`
- Between stacked text blocks → `gap-4` to `gap-8`
- Between hero heading and subtext → `mt-4` to `mt-8`

### Density reading
- **Dense**: short `gap`, small `p-`, no empty space. Dashboards, pricing.
- **Airy**: large `py-`, wide `gap-`, `max-w-` constraint on text. Editorial, luxury.
- **Cinematic**: full-height sections, giant type, almost nothing else. Agencies.

---

## 6. Component Identification

### Navigation Bar
- **Full-width sticky bar**: `fixed top-0 w-full z-50 bg-[color]/90 backdrop-blur-md`
- **Floating pill nav**: `fixed top-4 left-1/2 -translate-x-1/2 rounded-full px-4 py-2 liquid-glass`
- **Minimal inset nav**: `absolute top-4 left-4 right-4 flex justify-between`
- Always check: hamburger on mobile (`md:hidden`), desktop links (`hidden md:flex`), logo position

### Hero Headlines
- **Full-bleed wordmark**: `text-[18vw] font-black leading-none tracking-tighter`
- **Centered editorial title**: `text-[clamp(3rem,8vw,7rem)] max-w-4xl mx-auto text-center`
- **Left-aligned feature title**: `text-[clamp(2.5rem,5vw,5rem)] text-left max-w-2xl`

### Card Components
- **Feature card** (icon + title + body): vertical `flex-col p-6 rounded-2xl bg-[surface]`
- **Project card** (image-heavy): `rounded-2xl overflow-hidden aspect-[4/3]`
- **Stat card** (number + label): `p-5 flex flex-col gap-2`, number is `text-4xl font-black`
- **Testimonial card**: `p-6 rounded-xl`, quote + avatar row at bottom

### Buttons
- **Pill CTA**: `rounded-full px-6 py-3 text-sm font-medium`
- **Ghost/outline**: `rounded-full px-6 py-3 border border-current`
- **Icon button**: `w-10 h-10 rounded-full flex items-center justify-center`
- **Tag/chip**: `rounded-full px-3 py-1 text-xs`

### Media elements
- **Full-bleed video**: `absolute inset-0 w-full h-full object-cover`
- **Contained hero image**: `w-full max-w-[640px] rounded-2xl shadow-2xl`
- **Fanned card cluster**: multiple `absolute` children at `rotate-[-8deg]`, `rotate-[0deg]`, `rotate-[8deg]`

---

## 7. Motion Inference

### Load / entrance animations
```js
// Standard fade-up
{ initial: { opacity: 0, y: 24 }, animate: { opacity: 1, y: 0 }, transition: { duration: 0.6, ease: [0.22, 1, 0.36, 1] } }

// Blur fade (Apple-style)
{ initial: { opacity: 0, y: 20, filter: "blur(10px)" }, animate: { opacity: 1, y: 0, filter: "blur(0px)" }, transition: { duration: 0.7, ease: "easeOut" } }

// Scale in (cards)
{ initial: { opacity: 0, scale: 0.95 }, animate: { opacity: 1, scale: 1 }, transition: { duration: 0.5, ease: [0.22, 1, 0.36, 1] } }

// Clip-path reveal (wordmarks)
{ initial: { clipPath: "inset(100% 0 0 0)" }, animate: { clipPath: "inset(0% 0 0 0)" }, transition: { duration: 0.7, ease: [0.76, 0, 0.24, 1] } }
```

### Stagger patterns
- Cards: `0.08s`–`0.12s` between each
- Nav links: `0.04s`–`0.06s` between each
- Stat numbers: `0.1s` between each

### Hover interactions
| Element | Effect | Code |
|---|---|---|
| Card | Lift + shadow | `whileHover: { y: -6, boxShadow: "0 20px 40px rgba(0,0,0,0.3)" }` |
| Button | Scale up | `whileHover: { scale: 1.04 }` |
| Image | Zoom | `whileHover: { scale: 1.06 }` + `overflow: hidden` on parent |
| Glow button | Glow intensifies | `whileHover: { boxShadow: "0 0 40px rgba(accent, 0.7)" }` |

### Easing reference
```
Snappy: ease: [0.22, 1, 0.36, 1]
Smooth: ease: [0.16, 1, 0.3, 1]
Cinematic: ease: [0.76, 0, 0.24, 1], duration: 1.0
Spring: type: "spring", stiffness: 300, damping: 20
```

---

## 8. Image Placement Spec

For every uploaded image, specify:

### Position template
```
- Placement: [absolute center | absolute right | inline-block left | background layer | overlapping]
- Size: [w-full | max-w-[640px] | w-[48%] | aspect-[4/3] with w-full]
- Z-index: [z-0 behind text | z-10 on top of bg | z-20 overlay]
- Crop / aspect ratio: [aspect-video | aspect-square | aspect-[3/4] | free]
```

### Surface treatment template
```
- Radius: [rounded-none | rounded-lg | rounded-2xl | rounded-3xl | rounded-full]
- Shadow: [none | shadow-lg | shadow-[0_20px_60px_rgba(0,0,0,0.4)]]
- Overlay: [none | gradient mask | frosted glass | vignette]
- Glow: [none | box-shadow: 0 0 40px rgba(accent,0.4)]
```

### Animation template
```
Load / in-view:
- initial: { opacity: 0, scale: 0.96, y: 20 }
- whileInView: { opacity: 1, scale: 1, y: 0 }
- transition: { duration: 0.7, ease: [0.22, 1, 0.36, 1] }
- viewport: { once: true, margin: "-80px" }

Scroll:
- Parallax: y = useTransform(scrollY, [start, end], [0, -60])

Hover:
- whileHover: { scale: 1.04 }  (cards with images)
- whileHover: { y: -8 }        (floating mockups)
```

---

## 9. Quick Analysis Checklist

Run for every image before writing a single line:

```
[ ] WHAT IS IT?
    → Full-screen hero | Section mockup | Card/component | Badge/pill | Nav | Chart | Poster

[ ] LAYOUT
    → Grid: single-col / 2-col / 3-col / asymmetric / stacked
    → Focal point: top-center / bottom / left / right
    → Density: dense / normal / airy / cinematic

[ ] PALETTE
    → BG color (hex estimate): ___
    → Text color (hex estimate): ___
    → Accent color (hex estimate): ___
    → Glow / gradient? ___

[ ] TYPOGRAPHY
    → Heading: serif / sans / mono | size | weight | tracking
    → Body: same analysis
    → Gradient text? Clip-text effect?

[ ] SURFACES
    → Background: flat / gradient / video / image / grid pattern
    → Cards: solid / glassmorphism / liquid-glass / noise / outlined
    → Shadows: none / soft / hard / glow

[ ] SPACING
    → Section padding: tight / normal / generous / cinematic
    → Card padding: tight / normal / airy
    → Gap between elements: close / standard / open

[ ] COMPONENTS IDENTIFIED
    → List each: nav type, hero type, card type, button type

[ ] MOTION INFERENCE
    → Load: what enters first? stagger?
    → Scroll: parallax / pin / scrub / none
    → Hover: lift / tilt / glow / zoom / magnetic / none

[ ] MOOD
    → Premium / Editorial / Playful / Technical / Cinematic / Minimal / Bold
```
