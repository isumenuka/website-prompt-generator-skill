---
name: website-prompt-generator
description: Generate highly detailed, component-by-component prompts for building websites based on user ideas. Trigger this skill whenever the user asks for a prompt, a detailed specification, or a build guide for a new website, landing page, or web application, especially if they mention wanting something cinematic, modern, or using React/Tailwind/Framer Motion.
---

# Website Prompt Generator

This skill converts a user's brief idea for a website into a highly detailed, comprehensive prompt that can be fed into an AI coding assistant to build the site.

## Approach

When generating the prompt, you must act as an expert technical UI/UX designer and frontend architect. The resulting prompt must leave nothing to the imagination. It must specify the exact tech stack, colors, typography, layout, animations, and content structure.

Your goal is to produce a prompt that matches the extremely high level of detail and structural precision found in professional cinematic web development specifications.

**CRITICAL STEP**: This skill comes bundled with over 60+ detailed prompt examples in the file `references/Motion Sites Ideas prompts.md`. Before generating your prompt, you MUST use your file reading tools (`grep_search` or `view_file`) to explore this reference file. Find 1-3 examples that closely match the user's requested style or domain, and use them as a direct template for your output's tone, structure, and level of detail. Do not skip this step!

## Output Format

Your output must follow this exact structure. Do not deviate from these sections:

```markdown
Build Prompt: [Catchy Title of the Website]
Build a [type of site] with [key visual features].

Tech stack
- React + Vite + TypeScript
- Tailwind CSS
- Framer Motion
- Lucide React

Fonts
- Specify exact Google Fonts to use for headings and body (e.g., family=Instrument+Serif:ital@0;1&family=Barlow:wght@300;400;500;600). Include specific weight usage.

Color System / Theme
- Define specific CSS variables or Tailwind colors (backgrounds, foregrounds, accents). Use precise HEX, RGB, or HSL values.

Global Styles / CSS Utilities
- Detail any specific CSS classes needed (e.g., `.liquid-glass`, noise textures, custom scrollbars, gradient text). Provide the exact CSS code for these utilities if necessary.

Section 1: [Section Name]
- **Layout**: Describe the flex/grid structure, positioning (absolute/relative), padding, and alignment.
- **Background**: Is it a solid color, gradient, or video? Provide placeholder URLs if needed.
- **Content**: Detail the typography (size using clamp/vw or tailwind classes, weight, leading, tracking), specific text, and UI elements (buttons, inputs, icons).
- **Animations**: Specify exact Framer Motion props (e.g., `initial: {opacity: 0, y: 20}`, `whileInView`, `delay`, `ease: [0.25, 0.1, 0.25, 1]`).

Section 2: [Section Name]
- (Repeat detailed breakdown for all sections...)

Reusable Components
- Define any buttons, cards, tags, or animation wrappers used across multiple sections.

Responsive Breakpoints
- Detail how the layout scales across mobile, tablet, and desktop using Tailwind prefixes.
```

## Guidelines for the Generated Prompt

1. **Markdown Format**: You MUST wrap your entire generated prompt inside a single ```markdown code block so that it is easy for the user to copy and paste.
2. **Be Hyper-Specific**: Do not just say "Add a button". Say "Add a rounded-full pill button with a gradient background (linear-gradient(123deg, #18011F 7%, #B600A8 37%, #7621B0 72%, #BE4C00 100%)), inner box-shadow, white text, uppercase, tracking-widest, px-8 py-3."
3. **Include Animations**: Specify Framer Motion variants, scroll-driven animations, useScroll, useTransform, or CSS keyframes for a dynamic feel.
4. **Aesthetic & Vibe**: Use terms like "liquid glass", "noise overlay", "glassmorphism", "large typography", "tight tracking", and "cinematic layouts". 
5. **Placeholders**: If the design needs images or videos, describe them exactly (e.g., "Full-screen muted autoplaying video covering the entire viewport").
6. **Exact Classes**: Use exact Tailwind classes (e.g., `text-[14vw]`, `md:-mt-5`, `tracking-tight`, `leading-none`).

## Example Output Snippet (For Tone and Specificity)

```markdown
Heading: "About me" using .hero-heading gradient text, font-black, uppercase, leading-none, tracking-tight, centered. Font size: clamp(3rem, 12vw, 160px). FadeIn: delay 0, y 40.

Animated paragraph: Uses a character-by-character scroll-driven opacity animation. Text: "With more than five years of experience..." -- color #D7E2EA, font-medium, centered, leading-relaxed, max-w-[560px], font size clamp(1rem, 2vw, 1.35rem). Each character animates from opacity 0.2 to 1 based on scroll progress, with scroll offset ['start 0.8', 'end 0.2'].
```
