---
name: website-prompt-generator
description: Generate highly detailed, component-by-component prompts and blueprints for building websites based on user ideas. Automatically integrates the UI/UX design intelligence of the ui-ux-pro-max database (67 styles, 96 palettes, 57 typography pairings, and 99 UX guidelines). Trigger this skill whenever the user asks for a website prompt, landing page specifications, or a frontend build guide (React, Tailwind, Framer Motion, HTML, Next.js, Svelte, Vue, shadcn/ui, Anime.js, GSAP, React Spring, React Three Fiber / R3F, Spline 3D, WebGL, Magic UI, React Bits, Scroll Reveal), or uploads reference images/UI mockups, or asks for complex animations, 3D elements, or lightweight 3D effects (timelines, stagger, scroll, drag and drop, SVG morphing, scroll-linked animations, pinning, scroll scrubbing, batching, scroller proxying, spring physics, canvas rendering).
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

## 🎨 Step 0: UI/UX Design Intelligence Retrieval & Application (REQUIRED)

Before writing any build prompt or blueprint, execute the bundled search script in this skill to retrieve layout, typography, and color recommendations. Relying on this curated database ensures that the generated design system is industry-tested, accessibility-compliant, and perfectly matched to the product's business domain, rather than relying on guessed or generic color choices.

### 1. Extract Key Attributes
From the user's description or reference images, identify:
- **Product Type / Industry**: (e.g., SaaS, fintech, beauty/spa, education, portfolio, medical, e-commerce)
- **Visual Keywords / Vibe**: (e.g., minimal, glassmorphism, dark mode, brutalism, soft UI, luxury)
- **Target Stack**: (e.g., `html-tailwind` (default), `react`, `nextjs`, `vue`, `svelte`, `swiftui`, `react-native`, `flutter`, `shadcn`, `jetpack-compose`, `astro`, `nuxt-ui`, `nuxtjs`)

### 2. Execute UI/UX Pro Max CLI Commands
Run the following terminal commands in the workspace using the `run_command` tool to fetch design system parameters and stack guidelines:

- **Generate Complete Design System**:
  ```bash
  py .agents/skills/website-prompt-generator-skill-main/scripts/search.py "<product_type> <industry> <visual keywords>" --design-system -p "Project Name"
  ```
  *Tip*: If this is a multi-page web app or requires persistence, append `--persist` to save the design system globally to `design-system/MASTER.md` (Global Source of Truth) and page-specific overrides to `design-system/pages/[page-slug].md`. In the generated build prompt, explicitly instruct the developer tool to check and follow these markdown files.

- **Fetch Stack Guidelines** (run this if a specific tech stack is requested or chosen):
  ```bash
  py .agents/skills/website-prompt-generator-skill-main/scripts/search.py "<layout/component/responsive keywords>" --stack <stack_name>
  ```

- **Fetch Domain Guidelines** (if you need specific guidelines on `ux`, `accessibility`, `animation`, `landing`, or `chart`):
  ```bash
  py .agents/skills/website-prompt-generator-skill-main/scripts/search.py "<topic keywords>" --domain <domain_name>
  ```

### 3. Parse and Blend Results
Parse the console output of these scripts and apply them as follows:
- **Palette**: Map the exact primary, secondary, background, text, and CTA HEX/HSL colors from the script output directly into the CSS variable template.
- **Typography**: Apply the recommended Google Fonts pairings (including specific weights and CSS import links) to the heading and body fonts.
- **Key Effects**: Implement specific effects returned by the database (e.g. "frosted glass", "subtle depth shadows", "clear 3px focus rings").
- **Constraints / Anti-patterns**: Extract the "AVOID" warnings (e.g. "no neon colors", "no confusing booking flows", "no scale transforms that cause layout shift") and list them under a **Constraints** section.

### 4. Enforce Visual Quality Guidelines
Your output prompt/blueprint must explicitly instruct the developer tool to adhere to these core rules from the `ui-ux-pro-max` checklist, which are critical for achieving a premium visual design:
- **Icons & Visual Elements**: Use Lucide, Heroicons, or official brand SVGs from Simple Icons. Emojis must not be used as UI icons, as they look unpolished and unprofessional in a premium design.
- **Transitions & Hover**: Standardize transition speeds between 150ms and 300ms (e.g., `transition-colors duration-200`). Transitions outside this range feel either sluggish or too harsh. Ensure every hoverable or clickable element has `cursor-pointer` to signal interactivity to the user. Hover effects should avoid scaling transforms that shift other elements in the layout.
- **Light/Dark Contrast**: Ensure a minimum contrast ratio of 4.5:1 for normal body text to guarantee readability. For glass elements in light mode, use a high-opacity layer (`bg-white/80` or higher) and a visible light gray border (`border-gray-200`) to prevent the card from washing out against a light background.
- **Layout & Spacing**: Floating navbars should have offset margins (such as `top-4 left-4 right-4`) to prevent them from feeling cramped against window edges. Avoid overlapping elements unless intentionally layered with explicit z-index values. Maintain a consistent container width (e.g., `max-w-6xl` or `max-w-7xl`).
- **Accessibility**: Ensure keyboard focus rings are visible to help keyboard-only navigation. All form fields must have descriptive labels, all images must have alternative text, and transitions should respect the user's `prefers-reduced-motion` settings.
- **No Sci-Fi / Cyberpunk HUD Wireframes**: Do not use decorative node/constellation graphs, dashed polygon wireframe connection lines, or futuristic HUD-style diagrams. These elements look unpolished and dated. Use clean typographic hierarchies, structured charts, real UI mockups, or premium gradient/shimmer surfaces instead.

### 5. Interactive Selection & Preview (Interactive Sessions Only)
In active conversations, present a brief summary of the design tokens (retrieved primary/secondary/CTA colors, typography pairing, layout pattern, and a checklist) to the user for approval or adjustments **before** generating the final full build prompt/blueprint. This ensures user alignment.

---

## 📝 Text Mode

*Use this when no images are uploaded.*

### Approach

Act as an expert technical UI/UX designer and frontend architect. The resulting prompt must leave nothing to the imagination — specify the exact tech stack, colors, typography, layout, animations, and content structure. Incorporate all findings from **Step 0: UI/UX Design Intelligence Retrieval**.

**CRITICAL STEP**: This skill comes bundled with a universal component-prompt library in `references/core/animated-web-prompts.md`. Before generating, use `grep_search` or `view_file` to find 1–3 entries that match the user's requested style or domain. **Analyze** them — study their structure, level of technical specificity, the bracket/placeholder convention, and the animation techniques — then generate a **completely new** prompt with your own components and animations. Do NOT copy a sample verbatim or hand the library text back as the output: the samples set the quality bar and demonstrate the format, they are not the deliverable. Do not skip this step!
Additionally, if Anime.js is requested or is optimal for the animation requirements (like SVG morphing/drawing, complex stagger grids, or custom timelines), load `references/animations/animejs/animejs-api-reference.md` and `references/animations/animejs/animejs-examples.md` to ensure correct syntax, tree-shakeable imports, and clean React component structures (using `createScope` for component lifecycle cleanup).
Likewise, if GSAP ScrollTrigger is requested or is optimal for advanced scroll-driven actions (like pinning, complex scroll timelines, scroll scrubbing, or callback batching), load `references/animations/gsap/gsap-scrolltrigger-reference.md` to ensure correct plugin registration and proper cleanup using `@gsap/react` / `useGSAP()` hooks.

### Output Format (Text Mode)

Wrap your entire output in a single ` ```markdown ` block so it's easy to copy-paste:

```
Build Prompt: [Catchy Title of the Website]
Build a [type of site] with [key visual features].

## Global Design System Reference
- Note: If persisted, the developer tool must inspect `design-system/MASTER.md` and page overrides under `design-system/pages/` as the single source of truth for design tokens.

## UI/UX Design Rationale & Accessibility
- Explain the cognitive logic behind the selected color palette (e.g., "Deep blue communicates fintech security; WCAG contrast is 5.2:1").
- Detail why the typography pairing fits the product domain (e.g., "Instrument Serif adds luxury editorial feel, balanced by clean Barlow body text").
- Explain the spacing rhythm and interactive transitions choice (e.g., "200ms ease-out on cards to keep responses feeling snappy but smooth").

Tech Stack
- React + Vite + TypeScript
- Tailwind CSS
- Framer Motion (for standard transitions), Anime.js (v4) (for complex timelines, staggers, and SVGs), GSAP + ScrollTrigger (for advanced scroll scrubbing, pinning, and batched viewport callbacks), React Spring (for physics-based spring transitions), or React Three Fiber / Spline (for interactive 3D WebGL scenes)
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
2. **All animations included**: Framer Motion variants, `useScroll`/`useTransform`, CSS keyframes — be explicit. **CRITICAL REQUIREMENT**: The generated prompt must utilize GSAP (ScrollTrigger) or Anime.js (v4) for at least one or more components/sections (e.g., GSAP scroll pinning, Anime.js staggered grids, custom timeline sequences, or SVG shape morphing). Provide explicit configuration options and code blocks for these animations rather than generic placeholders.
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

**Load `references/core/ui-analysis-system.md` now** — it gives you the per-image checklist, surface/material CSS recipes, typography reading guide, and motion inference patterns. Run the Quick Checklist from that file on every image before continuing.

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

### Step 3 — Load `design-system-tokens.md` and Blend with UI/UX Pro Max Design System

**Load `references/core/design-system-tokens.md` now** — match the palette template that most closely resembles the images, copy its CSS variables, and adjust hex values.

Then, blend these with the output of the **Step 0 UI/UX Pro Max** search results. Lock in the absolute design variables:
- **Palette**: Inferred CSS variables with exact HSL/HEX values from both visual findings and the Pro Max recommended design system.
- **Typography**: Families + weights + `clamp()` scale + tracking/leading (using the Google Fonts pairings returned by the Pro Max script).
- **Spacing / radius / elevation**: Section padding rhythm, container max-width, corner radii, shadow recipes (utilize the specific Pro Max guidelines on Spacing & Interaction).
- **Motion language**: Default easing and duration (e.g., `ease: [0.22, 1, 0.36, 1]`, `~0.6s`) plus specific hover/load guidelines.

### Step 4 — Load `section-patterns.md` then Write the Blueprint Prompt

**Load `references/core/section-patterns.md` now** — find the matching pattern for each section identified from the images. Pull its build spec directly into the relevant section block below. This is what makes the output build-ready rather than descriptive.

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
- Framer Motion, Anime.js (v4), GSAP + ScrollTrigger, React Spring, or React Three Fiber / Spline
- Lucide React
- (Add Lenis, Recharts, or specific library plugins only if the images or requirements imply them)

## 3. Design System & UI/UX Rationale
### Global Design System Reference
- Note: If persisted, the developer tool must inspect `design-system/MASTER.md` and page overrides under `design-system/pages/` as the single source of truth for design tokens.
### Color & Typography Rationale
- Explain the visual and cognitive reasons for the selected palette and font pairings (e.g., "WCAG AA contrast compliant at 5.5:1, utilizing dark mode background to reduce eye strain for developers").
- CSS vars with precise hex: --bg, --fg, --muted, --accent, --glow
### Typography
- Headings: family, weights, clamp() scale, tracking, leading
- Body: family, weights, size scale
### Spacing / Radius / Elevation
- Section padding rhythm, max-w, radii, shadow recipes
### Motion Language & Accessibility
- Default easing + duration (e.g., ease: [0.22, 1, 0.36, 1], ~0.6s). One sentence describing the feel.
- Transition curves, focus rings, and prefers-reduced-motion accommodations.

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
- **GSAP / Anime.js Integration**: The generated blueprint/prompt must actively utilize GSAP (ScrollTrigger) or Anime.js (v4) for at least one or more components or sections. Define clear animation configs, timelines, or hooks for these components.

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
| `references/core/animated-web-prompts.md` | Text Mode (always) + Image Mode (for technique matching) | 50+ universal component prompts — analyze them for structure, specificity, and animation technique, then design something new. Never output them verbatim. `grep_search` by keyword. |
| `references/core/ui-analysis-system.md` | Image Blueprint Mode (always) | How to decode layouts, colors, type, surfaces, spacing, components, and motion from images. Includes the Quick Checklist. |
| `references/core/design-system-tokens.md` | Any time you need exact CSS values | Color palette templates (6 presets), typography scales, Google Fonts pairings, spacing tokens, shadow recipes, motion tokens, full CSS variable blocks. |
| `references/core/section-patterns.md` | When a matched section type is identified | 11 section categories with complete build specs: nav, hero, features, about, cards, testimonials, pricing, CTA, marquee, footer, animation wrappers. |
| `references/animations/animejs/animejs-api-reference.md` | When Anime.js is requested or chosen | Full API documentation for Anime.js v4, including timers, animations, timelines, stagger, scroll observers, draggable components, SVG morphing/drawing, and React integration rules. |
| `references/animations/animejs/animejs-examples.md` | When Anime.js is requested or chosen | Common Anime.js v4 animation recipes, timelines, scroll behaviors, SVG shape morphing, text splitting, UI toggle transitions, and React hooks. |
| `references/animations/gsap/gsap-scrolltrigger-reference.md` | When GSAP/ScrollTrigger is requested or chosen | Official reference manual for GSAP ScrollTrigger — covers scroll-linked animations, pinning, scrubbing, toggle actions, batching, scroller proxying, and React integration. |
| `references/animations/motion/core-concepts-deep-dive.md` | When advanced Framer Motion features are needed | Deep dive into variants orchestration, custom spring physics, layout animations, exit animations, and gestures. |
| `references/animations/motion/performance-optimization.md` | When optimizing bundle size or list performance | LazyMotion setup, useAnimate hooks, virtualization, and GPU acceleration. |
| `references/animations/motion/nextjs-integration.md` | When building Next.js applications | "use client" boundaries, SSR/hydration issues, and route transitions. |
| `references/animations/motion/accessibility-guide.md` | When implementing WCAG / reduced-motion | Handling prefers-reduced-motion, ARIA tags, and screen readers. |
| `references/animations/motion/common-patterns.md` | When copying common Framer Motion component code | Modal dialogues, accordions, carousels, tabs, and toast notifications. |
| `references/animations/motion/motion-vs-auto-animate.md` | When choosing between Framer Motion and AutoAnimate | Feature comparison and selection matrix. |
| `references/animations/[library-name]/` or `references/3d-webgl/[library-name]/` | When a specific 3D/animation library is requested | Check folders under `references/animations/` (such as `motion-framer`, `react-spring-physics`, `scroll-reveal-libraries`, `animated-component-libraries` (Magic UI, React Bits)) or `references/3d-webgl/` (such as `react-three-fiber`, `spline-interactive`, `threejs-webgl`, `substance-3d-texturing`, `web3d-integration-patterns`, `lightweight-3d-effects`) for their respective `SKILL.md` manuals and API guides. |

### Loading sequence for Image Blueprint Mode
1. Run Step 0 (UI/UX Pro Max search command for design system and optional stack).
2. Load `core/ui-analysis-system.md` → run the Quick Checklist on every image.
3. Load `core/design-system-tokens.md` → match the palette template, blend with the Pro Max output, and lock CSS variables.
4. Load `core/section-patterns.md` → match each image to a section pattern.
5. If using any animation or 3D library (Anime.js, GSAP, Framer Motion, R3F, Spline, React Spring, WebGL, Magic UI, Scroll Reveal), load its respective reference files or folder under `references/animations/` or `references/3d-webgl/` to read correct implementation instructions.
6. Grep `core/animated-web-prompts.md` for 1–2 entries matching the vibe → match their specificity level and technique, but write original components and animations (never copy the wording).

### Loading sequence for Text Mode
1. Run Step 0 (UI/UX Pro Max search command for design system and stack).
2. If using any animation or 3D library, load its respective reference manuals/folders under `references/animations/` or `references/3d-webgl/`.
3. Grep `core/animated-web-prompts.md` for 1–3 matching entries → use as a reference for format and quality bar, then generate something new.
4. Load `core/design-system-tokens.md` if you need to define additional CSS variables or font details.
5. Load `core/section-patterns.md` if a specific section type needs a detailed build spec.
