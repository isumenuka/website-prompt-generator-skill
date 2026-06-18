---
name: website-prompt-generator
description: Generate highly detailed, component-by-component prompts for building websites based on user ideas. Trigger this skill whenever the user asks for a prompt, a detailed specification, or a build guide for a new website, landing page, or web application, especially if they mention wanting something cinematic, modern, or using React/Tailwind/Framer Motion. ALSO trigger when the user uploads reference images, screenshots, mockups, or UI designs and wants a prompt or blueprint built from them — even if they don't say "website-prompt-generator" explicitly. If reference images are provided alongside any website/build request, always enter Image Blueprint Mode.
---

# Website Prompt Generator

This skill converts a user's idea — or a set of uploaded reference images — into a highly detailed, comprehensive build prompt that can be fed into an AI coding assistant (Cursor, Lovable, Bolt, v0, etc.) to build the site.

---

## ⚡ Mode Selection: Read First

Before doing anything, decide which mode applies:

| Situation | Mode |
|-----------|------|
| User describes an idea in words only | **[Text Mode]** — generate from description |
| User uploads 1+ images / screenshots / mockups | **[Image Blueprint Mode]** — analyze images first, then generate |
| User uploads images AND gives a description | **[Image Blueprint Mode]** — images take priority; use description as context |

If images are present but you can't view them, ask the user to re-upload or paste them before proceeding. Do not build a blueprint from imagination when images were provided.

---

## 📝 Text Mode

*Use this when no images are uploaded.*

### Approach

Act as an expert technical UI/UX designer and frontend architect. The resulting prompt must leave nothing to the imagination — specify the exact tech stack, colors, typography, layout, animations, and content structure.

**CRITICAL STEP**: This skill comes bundled with detailed prompt examples in `references/Motion Sites Ideas prompts.md`. Before generating, use `grep_search` or `view_file` to find 1–3 examples that closely match the user's requested style or domain. Use them as a direct template for tone, structure, and level of detail. Do not skip this step!

### Output Format (Text Mode)

Wrap your entire output in a single ` ```markdown ` block so it's easy to copy-paste:

```
Build Prompt: [Catchy Title of the Website]
Build a [type of site] with [key visual features].

Tech Stack
- React + Vite + TypeScript
- Tailwind CSS
- Framer Motion
- Lucide React

Fonts
- Specify exact Google Fonts (e.g., Instrument Serif + Barlow:300;400;500;600). Include weight usage.

Color System / Theme
- Define CSS variables or Tailwind tokens with precise HEX/HSL values for bg, fg, accent, muted.

Global Styles / CSS Utilities
- Any special CSS classes needed (e.g., .liquid-glass, noise texture, gradient text, custom scrollbar). Provide exact CSS.

Section 1: [Section Name]
- Layout: flex/grid structure, padding, alignment, z-index.
- Background: solid / gradient / image / video.
- Content: typography (clamp sizes, weight, tracking), text, buttons, icons.
- Animations: exact Framer Motion props (initial, whileInView, transition ease/duration/delay).

Section 2: [Section Name]
- (Repeat for all sections)

Reusable Components
- Buttons, cards, badges, tags, animation wrappers — defined once with variants.

Responsive Breakpoints
- How layout reflows on mobile/tablet/desktop using Tailwind prefixes.
```

### Text Mode Guidelines

1. **Hyper-specific**: Not "Add a button" — say "A `rounded-full` pill, `bg-gradient-to-r from-[#18011F] to-[#B600A8]`, `text-white uppercase tracking-widest px-8 py-3`, with an inner `box-shadow: inset 0 1px 0 rgba(255,255,255,0.15)`."
2. **All animations included**: Framer Motion variants, `useScroll`/`useTransform`, CSS keyframes — be explicit.
3. **Aesthetic vocabulary**: "liquid glass", "noise overlay", "glassmorphism", "large editorial typography", "cinematic layouts", "tight tracking".
4. **Placeholders**: If images/videos are needed, describe them precisely (e.g., "Full-screen muted autoplay video, `object-cover`, covering the entire viewport").
5. **Exact Tailwind**: Use real classes — `text-[14vw]`, `md:-mt-5`, `tracking-tight`, `leading-none`.

---

## 🖼️ Image Blueprint Mode

*Use this when the user uploads reference images, screenshots, mockups, or UI design files.*

### The Core Rules

- **1 image = 1 section** by default. A full-screen mockup becomes a section. A small UI fragment (pill, card, progress bar) may become a reusable component instead — use judgment.
- **4 images = 4 sections** (or components). Map every image to either a section or a named reusable component. No image is left orphaned.
- **You synthesize, you don't transcribe.** Turn the images into ONE coherent site. You are the art director, not a caption writer.
- **Be specific, not vague.** Infer hex colors, type scales, spacing, radii, and motion from what you see. State them confidently as design decisions.
- **Videos count too.** If the user uploads a video reference, analyze its motion language, color palette, and UI flow the same way you analyze images.

### Step 1 — Load `ui-analysis-system.md` and Analyze Every Image/Video

**Load `references/ui-analysis-system.md` now** — it gives you the per-image checklist, surface/material CSS recipes, typography reading guide, and motion inference patterns. Run the Quick Checklist from that file on every image before continuing.

For each uploaded file, capture all of the following before designing anything:

| Checklist item | What to note |
|---|---|
| **What it is** | Full screen, hero, card, pill/badge, nav, chart, poster, component state, video clip |
| **Layout** | Grid/stack/columns, alignment, density, focal point |
| **Palette** | Background, foreground/text, accent(s), any glow/gradient — estimate hex |
| **Typography** | Serif/sans/mono, weight, case (UPPER/sentence), tracking, size of biggest text |
| **Surface treatment** | Frosted glass, noise, hard shadows, gradients, dotted grid, radius (sharp vs rounded) |
| **Implied motion** | What obviously animates on load (stagger, clip reveal, count-up), scroll (parallax, pin), hover (lift, tilt, glow, zoom) |
| **Mood** | Playful / minimal / editorial / technical / premium / cinematic |

Run this checklist for all images before moving on.

### Step 2 — Build the Image → Section Map

Decide scroll order and role for each image:

| # | File / description | Section name | Role | One-line treatment |
|---|---|---|---|---|
| 1 | hero-mockup.png | Hero | Primary visual | Dark canvas, large wordmark, card fan enters with spring stagger |
| 2 | pricing-card.png | Pricing | Component (reused ×3) | Frosted glass card, green accent border on hover |
| … | … | … | … | … |

If multiple images repeat the same pattern, group them — don't force ten sections out of ten near-identical cards.

### Step 3 — Load `design-system-tokens.md` and Derive the Global Design System

**Load `references/design-system-tokens.md` now** — match the palette template (section 1) that most closely resembles the images, copy its CSS variables, and adjust hex values. Use section 7 (Motion Tokens) to define the site's motion language.

From the combined images, lock in:
- **Palette**: CSS vars (`--bg`, `--fg`, `--accent`, etc.) with exact hex values
- **Typography**: Families + weights + `clamp()` scale + tracking/leading
- **Spacing / radius / elevation**: Section padding rhythm, container max-width, corner radii, shadow recipes
- **Motion language**: One sentence describing the feel + the default easing and duration to reuse everywhere (e.g., `ease: [0.22, 1, 0.36, 1]`, `~0.6s`)

### Step 4 — Load `section-patterns.md` then Write the Blueprint Prompt

**Load `references/section-patterns.md` now** — find the matching pattern for each section identified from the images. Pull its build spec directly into the relevant section block below. This is what makes the output build-ready rather than descriptive.

Wrap your entire output in a single ` ```markdown ` block. Use this structure:

```
# [Project Name] — Website Blueprint
> Built from N uploaded reference image(s). Design system values are inferred decisions, not pixel measurements.

## 0. At a Glance
One-line concept · who it's for · overall vibe and motion language.

## 1. Image → Section Map
(The table from Step 2, finalized)

## 2. Tech Stack
- React + Vite + TypeScript
- Tailwind CSS
- Framer Motion
- Lucide React
- (Add GSAP + ScrollTrigger, Lenis, Three.js/R3F, Recharts only if the images imply them)

## 3. Design System
### Color
- CSS vars with precise hex: --bg, --fg, --muted, --accent, --glow
### Typography
- Headings: family, weights, clamp() scale, tracking, leading
- Body: family, weights, size scale
### Spacing / Radius / Elevation
- Section padding rhythm, max-w, radii, shadow recipes
### Motion Language
- Default easing + duration (e.g., ease: [0.22, 1, 0.36, 1], ~0.6s). One sentence describing the feel.

## 4. Global Styles / Utilities
- Only utilities the images imply: .glass, noise overlay, gradient text, custom scrollbar, dotted-grid bg.
- Include the actual CSS for each.

## 5. Header
- Structure: logo position, nav items, CTA — left/center/right.
- Behavior: fixed/sticky, shrink on scroll, backdrop-blur on scroll?
- Animations: Load (how it assembles) · Scroll (state change) · Hover (links, CTA).

## 6. Sections (in scroll order)

### Section 1 — [Name]  ← sourced from Image #N
- **Layout**: flex/grid, padding, alignment.
- **Background**: solid / gradient / image / video + placeholder.
- **Content & Typography**: exact text intent, clamp sizes, weights, tracking; buttons, inputs, icons.
- **Image Integration**:
  - Which uploaded image goes here, exact placement and sizing (w-, max-w-, aspect ratio).
  - Crop, layering, z-index, surface treatment (mask, shadow, glass overlay, border-radius).
  - How it sits relative to the text (behind, beside, overlapping).
- **Animations**:
  - *Load / in-view*: what enters, in what order, motion type, timing, Framer props.
    Example: `initial: { opacity: 0, y: 24 }, whileInView: { opacity: 1, y: 0 }, transition: { duration: 0.6, ease: [0.22, 1, 0.36, 1] }`
  - *Scroll*: parallax depth, pin, scrub, sticky (only if earned).
  - *Hover*: per interactive element — lift, tilt, glow, image zoom, cursor change.

(Repeat Section block for every section)

## 7. Footer
- Structure: columns, links, socials, legal, back-to-top.
- Animations: reveal on scroll-in; any hover / marquee.

## 8. Reusable Components
- Buttons, cards, badges/pills, tags, animation wrappers — defined once with exact styling and variants.

## 9. Responsive Breakpoints
- How layout reflows on mobile/tablet/desktop using Tailwind prefixes.
- What stacks, what hides, how type scales.

## 10. Build Order
- The recommended order to build in, and the 2–3 details that most define the site's feel.
```

### Image Mode — Quality Bar

- **Every image appears twice**: once in the Image → Section map, once in a section's "Image Integration" block.
- **Specific over vague**: colors with hex, type with a scale, motion with triggers and Framer props.
- **Three animation triggers always covered**: Load/in-view · Scroll · Hover — for every section that uses an image.
- **Cohesive**: disparate references resolve into one consistent system, not a patchwork.
- **Build-ready**: a developer or AI coding tool can build the site top-to-bottom without guessing.

---

## Worked Example — 1 Image → 1 Section

**Reference image**: A light, minimal "STORY MUSIC 2026" mockup — a fan of three album-art cards behind a frosted-glass panel listing tracks, with a circular dark play button and a heavy black wordmark below.

**Becomes:**

```markdown
### Section 1 — Hero ("Story Music")  ← Image #1
- **Layout**: Centered column on a near-white canvas (`#F4F4F5`). Stacked card cluster sits center, wordmark beneath, year pill below that. `py-24 md:py-32`, `max-w-[640px]` content.
- **Background**: Flat `#F4F4F5`. No texture — the cards carry the contrast.
- **Content & Typography**: Wordmark "STORY MUSIC" — `font-black UPPERCASE tracking-tight leading-none text-[clamp(2.5rem,11vw,7rem)] text-[#1A1A1A]`. Year pill "2026" — `bg-zinc-200 text-zinc-500 rounded-full px-4 py-1 text-sm`.
- **Image Integration**: Place the reference as the hero card cluster. Three album cards fanned at −8°, 0°, +8° — `rounded-2xl shadow-[0_20px_60px_rgba(0,0,0,0.12)]`, center card largest. Over the lower third: frosted track-list panel — `backdrop-blur-xl bg-white/40 rounded-2xl` listing track rows. A `w-14 h-14` circular play button `bg-[#1A1A1A]` with a white music-note icon, bottom-right of the panel.
- **Animations**:
  - *Load*: Cards deal in one-by-one from `y: 30, rotate: 0` into their fanned angles, `~0.08s` stagger, spring. Panel fades + slides up after (`initial: { opacity: 0, y: 24 }, transition: { delay: 0.4, duration: 0.6, ease: [0.22, 1, 0.36, 1] }`). Wordmark clip-path reveals upward.
  - *Scroll*: Card cluster drifts up ~12% slower than the page (light parallax via `useScroll + useTransform`).
  - *Hover*: Hovering the cluster spreads the fan wider and lifts the center card `~6px`; play button scales to `1.06` with a faint `ring-2 ring-black/20`.
```

---

---

## 📚 Reference Files — When to Load Each

Do NOT load all reference files at once. Load only what you need for the current task.

| File | Load when | What it gives you |
|---|---|---|
| `references/Motion Sites Ideas prompts.md` | Text Mode (always) + Image Mode (for tone matching) | 60+ real build prompts — use for tone, structure, and wording templates. `grep_search` by keyword. |
| `references/ui-analysis-system.md` | Image Blueprint Mode (always) | How to decode layouts, colors, type, surfaces, spacing, components, and motion from images. Includes the Quick Checklist. |
| `references/design-system-tokens.md` | Any time you need exact CSS values | Color palette templates (6 presets), typography scales, Google Fonts pairings, spacing tokens, shadow recipes, motion tokens, full CSS variable blocks. |
| `references/section-patterns.md` | When a matched section type is identified | 11 section categories with complete build specs: nav, hero, features, about, cards, testimonials, pricing, CTA, marquee, footer, animation wrappers. |

### Loading sequence for Image Blueprint Mode
1. Load `ui-analysis-system.md` → run the Quick Checklist on every image
2. Load `design-system-tokens.md` → match the palette template and lock CSS vars
3. Load `section-patterns.md` → match each image to a section pattern
4. Grep `Motion Sites Ideas prompts.md` for 1–2 prompts matching the vibe → steal their wording and specificity level

### Loading sequence for Text Mode
1. Grep `Motion Sites Ideas prompts.md` for 1–3 matching examples → use as template
2. Load `design-system-tokens.md` if you need to define a color system or font pairing
3. Load `section-patterns.md` if a specific section type needs a detailed spec
