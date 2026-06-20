# Universal Component Prompts — Full Library

**Brackets:** `[FILL]` = replace every time · `[FILL = default]` = replace or keep the default · `[clause ?]` = keep or delete · `[A | B | C]` = pick one · `[× N]` = repeat N times. **Everything not in brackets is a fixed engine value — keep it exactly.**

---
### FOUNDATION
---

## 1 · Tech Stack — CDN Single-File (no build)

```text
Build a single-page site as ONE self-contained HTML file with no bundler. In <head>, pin exactly these CDNs:
Tailwind via <script src="https://cdn.tailwindcss.com"></script>; React 18 UMD (react@18.3.1 + react-dom@18.3.1
development builds); Babel Standalone @7 so JSX can be written inline; and Framer Motion 11
(framer-motion@11/dist/framer-motion.js) followed by <script>window.Motion = window.FramerMotion;</script>.
Set <body> background to [BG_BASE = #000000]. Mount a React app on #root. Write every component inside its own
<script type="text/babel"> block and expose it via window.ComponentName = ComponentName. Extend the inline
Tailwind config so font-heading maps to '[FONT_DISPLAY = Instrument Serif]', font-body maps to
'[FONT_BODY = Inter]', and the default borderRadius DEFAULT is "[RADIUS = 9999px]" (so a bare `rounded` class
renders a pill). Load fonts with a Google Fonts <link>. Output the complete file, ready to open in a browser.
```

## 2 · Tech Stack — Vite + React + TypeScript

```text
Scaffold a Vite + React 18 + TypeScript project with Tailwind CSS 3.4. Use lucide-react for all icons and
[framer-motion | gsap | framer-motion + gsap] for animation. [Add shadcn/ui ?]. Do not add any other UI library.
In index.css set html, body, #root to height:100%, margin:0, background:[BG_BASE = #000000], color:[INK = #FFFFFF],
font-family:'[FONT_BODY = Inter]', sans-serif, with -webkit-font-smoothing:antialiased. The outermost wrapper is
`relative` with `overflow-x: clip`. Build these sections in order, each as its own component file:
[HeroSection, MarqueeSection, AboutSection, ServicesSection, ProjectsSection, Footer]. Make the whole page fully
responsive (mobile → tablet → desktop) using Tailwind sm/md/lg/xl prefixes on every padding, font size and span.
```

## 3 · Font Loader (any source)

```text
Load fonts before first paint (before any @tailwind directives). Use whichever source matches:
• Google Fonts — @import url('https://fonts.googleapis.com/css2?family=[FONT_DISPLAY+:ital@0;1]&family=[FONT_BODY]:wght@[300;400;500;600]&display=swap');
• Self-hosted (onlinewebfonts / CDN) — add <link href="[FONT_CDN_URL]" rel="stylesheet"> in index.html.
• Local file — @font-face { font-family:'[FONT_NAME]'; src:url('[WOFF_URL]') format('woff'); font-weight:normal;
  font-style:normal; font-display:swap; }
Expose as CSS variables: --font-display:'[FONT_DISPLAY]', serif; --font-body:'[FONT_BODY]', sans-serif. All
headings use var(--font-display) [in italic ?]; all body text uses var(--font-body).
```

## 4 · Global Tokens + Reset

```text
Add a global reset: *{ box-sizing:border-box; margin:0; padding:0 }. Define these :root CSS variables and use
them everywhere instead of hard-coded colors:
--bg:[BG_BASE = #000000]; --ink:[INK = #FFFFFF]; --muted:[MUTED = rgba(255,255,255,0.6)];
--accent:[ACCENT = #7342E2]; --surface:[#101010]; --stroke:[rgba(255,255,255,0.1)].
Apply --bg to html, body, #root and the outermost wrapper. [Optional gradient-text helper ?]: add a
.gradient-text class → background:linear-gradient(180deg,[STOP_A] 0%,[STOP_B] 100%); -webkit-background-clip:text;
background-clip:text; -webkit-text-fill-color:transparent; color:transparent.
```

---
### SURFACES & TEXTURE
---

## 5 · Liquid Glass — Subtle Frosted Surface

```text
Add this exact `.liquid-glass` utility in a <style> block. Do not simplify the ::before mask trick — it is what
renders the gradient hairline border that catches light. Apply it to [nav pill / chips / cards / secondary buttons],
always paired with a rounded radius.

.liquid-glass{
  background:rgba(255,255,255,0.01);
  background-blend-mode:luminosity;
  backdrop-filter:blur(4px); -webkit-backdrop-filter:blur(4px);
  border:none;
  box-shadow:inset 0 1px 1px rgba(255,255,255,0.1);
  position:relative; overflow:hidden;
}
.liquid-glass::before{
  content:""; position:absolute; inset:0; border-radius:inherit; padding:1.4px;
  background:linear-gradient(180deg,
    rgba(255,255,255,0.45) 0%, rgba(255,255,255,0.15) 20%,
    rgba(255,255,255,0) 40%, rgba(255,255,255,0) 60%,
    rgba(255,255,255,0.15) 80%, rgba(255,255,255,0.45) 100%);
  -webkit-mask:linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite:xor; mask-composite:exclude;
  pointer-events:none;
}
```

## 6 · Liquid Glass — Strong (primary action)

```text
Add a `.liquid-glass-strong` variant for the single primary action / the one element that should feel solid. It is
identical to `.liquid-glass` (include that base too) but overrides the blur and shadow, and uses heavier border-gradient
stops. Apply it to the primary CTA only.

.liquid-glass-strong{
  backdrop-filter:blur(50px); -webkit-backdrop-filter:blur(50px);
  box-shadow:4px 4px 4px rgba(0,0,0,0.05), inset 0 1px 1px rgba(255,255,255,0.15);
}
.liquid-glass-strong::before{
  /* same mask trick as .liquid-glass::before, but gradient stops:
     rgba(255,255,255,0.5) 0%, 0.2 20%, 0 40%, 0 60%, 0.2 80%, 0.5 100% */
}
```

## 7 · Fluted / Ribbed Glass Panel

```text
Add a `.fluted-glass` panel — a translucent surface with vertical reeded-glass grooves. Use it behind [the nav /
feature cards]. Tune groove width and tint via the bracketed values.

.fluted-glass{
  background:repeating-linear-gradient(90deg,
    rgba(255,255,255,[0.06]) 0px,
    rgba(255,255,255,[0.02]) [3px],
    rgba(255,255,255,[0.06]) [6px]);
  backdrop-filter:blur([12px]); -webkit-backdrop-filter:blur([12px]);
  border:1px solid rgba(255,255,255,0.08);
  border-radius:[RADIUS = 1.5rem];
  position:relative; overflow:hidden;
}
Add a faint inset highlight on the top edge via an inset box-shadow.
```

## 8 · Noise / Grain Overlay

```text
Add a film-grain overlay over [the background video / the whole page] to kill banding and add cinematic texture. It
must be pointer-events:none and sit above the media but below the content. Use one of:
• SVG filter (sharper): <svg style="position:absolute;width:0;height:0"><filter id="grain"><feTurbulence
  type="fractalNoise" baseFrequency="0.9" numOctaves="2"/></filter></svg>, then a fixed/absolute div with filter:url(#grain).
• PNG tile: a div with background-image:url([NOISE_PNG]); background-size:[180px].
Set opacity:[0.7] and mix-blend-mode:[overlay | multiply | soft-light].
```

## 9 · Gradient / Shiny Text

```text
Render [HEADLINE_TEXT] as gradient-filled text: background:linear-gradient([180deg | to right], [STOP_A] 0%,
[STOP_B] [50%], [STOP_C ?] 100%); -webkit-background-clip:text; background-clip:text; -webkit-text-fill-color:transparent;
color:transparent. [Optional animated sweep ?]: set background-size:200% on the text and add a `.animate-shiny` class →
animation: shiny [6s] linear infinite, with @keyframes shiny{ 0%{background-position:-200% center} 100%{background-position:200% center} }.
```

## 10 · Progressive Blur (bottom fade)

```text
Add a `ProgressiveBlur` band fixed to the bottom of the viewport (z-30, pointer-events:none). Height [150px]. It uses a
CSS mask gradient (transparent at top → opaque at bottom) combined with backdrop-filter:blur([4px]) so it only blurs a
strip and fades from transparent into [BG_BASE = #000000] at the bottom edge. This is the ONLY element allowed to darken
the bottom — it must NOT cover the full viewport. [Optional scroll-reactive ?]: ramp the blur 0→[55px] as scrollYProgress
goes 0→1 (subtle 0–5px in the first half, then 5–55px in the second half).
```

---
### BACKGROUND VIDEO ENGINES
---

## 11 · Simple Looping Background Video

```text
Add a full-bleed background <video autoPlay loop muted playsInline preload="auto"> with object-cover, positioned
absolute inset-0 w-full h-full at z-0. Source: [VIDEO_URL]. [Optional crop ?]: shift with translate-y-[17%] (or scale
the video to width/height 120% with object-top) so the focal point sits in the [lower / upper] portion of the frame.
[Optional overlay ?]: place bg-gradient-to-b from-black/30 via-transparent to-black/60 on top — OR add no overlay so the
video shows at full brightness. The outer container is min-h-screen bg-[BG_BASE = #000000] overflow-hidden.
```

## 12 · Crossfade Loop — `FadingVideo` (seamless, no visible cut)

```text
Build a `FadingVideo` component that wraps a <video autoPlay muted playsInline preload="auto"> starting at opacity:0,
and loops it with a manual JS crossfade so the seam never shows (no CSS transitions — they fight the rAF). Source:
[VIDEO_URL]. Implement this engine exactly:
• Constants: FADE_MS = 500; FADE_OUT_LEAD = 0.55 (seconds).
• fadeTo(target, duration): drive opacity with requestAnimationFrame, reading the CURRENT value from
  video.style.opacity each time so a new fade resumes from wherever the last one stopped. At the start of every call,
  cancelAnimationFrame the previous rAF id.
• on 'loadeddata': set opacity 0, call play(), then fadeTo(1).
• on 'timeupdate': if not already fading out AND (duration - currentTime) <= 0.55 AND > 0, set the fadingOut ref and fadeTo(0).
• on 'ended': set opacity 0; after setTimeout(100ms) set currentTime = 0, call play(), clear the fadingOut ref, fadeTo(1).
• The native `loop` attribute is OFF — looping is manual via 'ended'.
• Cleanup on unmount: cancel rAF and remove all listeners.
Place it absolute inset-0 object-cover z-0. [Optional: no dark overlay — full brightness ?].
```

## 13 · Scroll-Scrubbed Video (currentTime driven by scroll)

```text
Build a `LiquidVideoCanvas`: a fixed fullscreen <video muted playsInline preload="auto"> with object-cover that is NOT
autoplayed — its currentTime is driven by scroll progress through requestAnimationFrame with LERP smoothing (factor
[0.12]). Source: [VIDEO_URL]. Use this frame-seek guard exactly (it prevents black flashes and jank):
  if (!isSeeking && !video.seeking) { isSeeking = true; video.currentTime = clampedTime; }
  else { nextSeekTime = clampedTime; }   // queue, run after current seek finishes
Listen for 'seeking' and 'seeked'; on 'seeked', execute any queued nextSeekTime.
Entrance: start at scale 1.12 / opacity 0; when readyState >= 3, animate over 1.4s with cubic ease-out to scale 1 /
opacity 1, with a 3.5s safety-timeout fallback. Error handling: track consecutive errors, max 3 retries.
Apply these scroll-driven effects directly to the DOM via ref (NOT React state): progressive blur 0→[55px], scale
[1.03]→[1.11]. Z-index layering must be exactly: video fixed inset-0 z-[1] < content z-10 < progressive-blur z-30 <
header z-50. Never set a background color on any layer above the video — it must stay visible through the content.
```

## 14 · Boomerang Video (forward → reverse, seamless)

```text
Build a `BoomerangVideoBg` that loops a short clip by ping-ponging captured frames. On load, capture each video frame
into an offscreen canvas (cap width [960px], scale to fit) using requestVideoFrameCallback when available, else
requestAnimationFrame; skip duplicate currentTimes. On 'ended', stop capturing and store the frame array. Then render
to a visible <canvas> at [30]fps, advancing an index forward and reversing direction at the ends (index += direction;
flip at 0 and length-1). Hide the source <video> once frames are ready and show the canvas. Source: [VIDEO_URL]. Mount
absolute inset-0 w-full h-full, object-cover, crossOrigin="anonymous".
```

---
### NAVIGATION
---

## 15 · Glass Pill Navbar (logo · links · CTA)

```text
Build a fixed top-[4] navbar, px-8 lg:px-16, z-50, constrained to max-w-5xl mx-auto (not full width). Three zones:
• LEFT: [a 48×48 .liquid-glass circle holding an italic-serif lowercase "[a]" / a Globe icon + "[BRAND]" in white,
  font-semibold, text-lg].
• CENTER (hidden on mobile, md:flex): a `.liquid-glass` pill, px-1.5 py-1.5, holding the links
  [Home, Voyages, Worlds, Innovation, Plan Launch] — each px-3 py-2 text-sm font-medium text-white/90,
  hover:text-white transition-colors — followed by a white pill CTA "[Claim a Spot]" (bg-white text-black
  rounded-full px-5 py-2, whitespace-nowrap) with a trailing ArrowUpRight icon.
• RIGHT: a 48×48 invisible spacer to balance the logo (or move the CTA here instead).
[Optional entrance ?]: fade and slide down, opacity 0→1, y -10→0, 0.6s easeOut.
```

## 16 · Split Navbar (logo left · CTAs right)

```text
Build a navbar max-w-7xl mx-auto, px-5 sm:px-8 py-4 sm:py-5, flex items-center justify-between, z-10:
• LEFT: [an SVG logo 32×32 fill [INK]] + "[BRAND]" [with ® as a <sup class="text-xs"> ?].
• CENTER (hidden md:flex, gap-8, ml-8): links [Vault, Plans, Install, News, Help], text-sm font-medium,
  text-white/70 hover:text-white [with a staggered entrance, delay 0.1 + i*0.05 ?].
• RIGHT (desktop): a primary button "[Start For Free]" → bg-[ACCENT = #7342E2] text-white rounded-full px-5 py-2.5;
  and a secondary button "[Sign In]" → bg-[#F2F2EE] text-[INK] rounded-full px-5 py-2.5.
• MOBILE: a hamburger (lucide Menu/X icon) that opens the right-side slide-in sheet (see “Mobile Slide-In Sheet”).
```

## 17 · Mobile Slide-In Sheet

```text
When the hamburger is tapped, render this with AnimatePresence + Framer Motion:
• BACKDROP: fixed inset-0, background [rgba(25,40,55,0.35)] with backdrop-filter:blur(4px).
• SHEET: fixed right-0 top-0, width min([88vw], [360px]), height 100dvh, background [#CFC8C5], box-shadow
  -12px 0 48px rgba(0,0,0,0.18). Animate x from '100%' to 0, ease [0.22, 1, 0.36, 1], duration 0.45s.
• CONTENT: a header with the logo and a close (X) button, a 1px divider, the nav links staggered (delay 0.18 + i*0.07),
  and bottom CTA buttons matching the desktop pair.
```

## 18 · Hanging / Dropdown Center Nav

```text
Build an absolutely-positioned top-center navbar that hangs from the top edge of a video section:
[bg-black / .liquid-glass] rounded-b-2xl md:rounded-b-3xl px-4 py-2 md:px-8. It holds the links
[Our story, Collective, Workshops, Programs, Inquiries], text-[10px] sm:text-xs md:text-sm, gap-3 sm:gap-6 md:gap-12,
link color [rgba(225,224,204,0.8)] with hover [#E1E0CC] (inline styles). Hidden on mobile (hidden lg:block) [or compress
the gaps on mobile instead].
```

---
### HERO BLOCKS
---

## 19 · Centered Hero Stack

```text
Build the hero content block: relative z-10 flex-1 flex flex-col items-center justify-center text-center, pt-24 px-4
[translate-y-[-20%] to optically center it over a bottom-weighted video ?]. Animate every child in with Framer Motion,
initial {filter:'blur(10px)', opacity:0, y:20}, easeOut, staggered by delay:
• HEADLINE: "[HEADLINE_TEXT]" — font-display [italic ?], text-6xl md:text-7xl lg:text-[5.5rem], leading-[0.8],
  tracking-[-4px], max-w-2xl, color [INK = #FFFFFF]. [Use the BlurText component for word-by-word reveal ?].
• SUBHEAD (delay 0.8s): "[SUBHEAD_TEXT]" — mt-4 text-sm md:text-base font-body font-light leading-tight, max-w-2xl,
  color [INK].
• CTAs (delay 1.1s, flex items-center gap-6 mt-6): primary → .liquid-glass-strong rounded-full px-5 py-2.5 text-sm
  font-medium "[Start Your Voyage]" + ArrowUpRight; secondary → bare text link "[View Liftoff]" + a filled Play icon.
```

## 20 · Announcement Badge / Pill Chip

```text
Build a .liquid-glass rounded-full pill (Framer Motion entrance, delay 0.4s) that contains: a white pill chip "[New]"
(bg-white text-black px-3 py-1 text-xs font-semibold) followed by the message "[Maiden Crewed Voyage to Mars Arrives 2026]"
(text-sm text-white/90, pr-3). [Optional trailing ArrowRight icon ?]. Place it directly above the hero headline.
```

## 21 · Stat Cards Row

```text
Build a row (Framer Motion entrance, delay 1.3s, flex items-stretch gap-4 mt-8) of [2] `.liquid-glass` cards, each
p-5 w-[220px] rounded-[1.25rem]. Each card has, top to bottom: a 28×28 white outline SVG icon ([clock] / [globe]); a
big number in font-display italic, text-4xl tracking-[-1px] leading-none "[34.5 Min]" / "[2.8B+]"; and a label
text-xs font-body font-light mt-2 "[Average Watch Time]" / "[Users Worldwide]".
```

## 22 · Email-Capture Bar

```text
Build a max-w-xl w-full space-y-4 block:
• Input bar: .liquid-glass rounded-full pl-6 pr-2 py-2 flex items-center gap-3 — a transparent email input
  (placeholder "[Enter your email]", text-white placeholder:text-white/40, text-base) and a white circular submit button
  (bg-white rounded-full p-3 text-black) holding an ArrowRight icon (size 20).
• Sub copy below: text-white text-sm leading-relaxed px-4 "[Stay updated — subscribe and never miss a launch.]"
In a React artifact do NOT use a <form> tag — wire it with onClick / onChange handlers.
```

## 23 · Magnetic Portrait Hero

```text
Build an absolutely-centered portrait (left-1/2 -translate-x-1/2 z-10) wrapped in a `Magnet` component (mouse-following).
Magnet settings: padding [150], strength [3], activeTransition "transform 0.3s ease-out", inactiveTransition
"transform 0.6s ease-in-out". The image is [PORTRAIT_URL] at widths w-[280px] sm:w-[360px] md:w-[440px] lg:w-[520px]. On
mobile position it top-1/2 -translate-y-1/2; on sm+ pin it to bottom-0. Entrance via FadeIn, delay 0.6, y 30.
```

---
### TEXT ANIMATION PRIMITIVES
---

## 24 · `BlurText` — Word-by-Word Blur-In

```text
Build a `BlurText` component that animates a headline into focus word by word. An IntersectionObserver triggers it at
10% visibility. Split the text on spaces; render each word as a motion.span with initial {filter:'blur(10px)',
opacity:0, y:50}, keyframed in 3 steps to {filter:'blur(5px)', opacity:0.5, y:-5} then {filter:'blur(0px)', opacity:1,
y:0}; duration 0.7 (times [0, 0.5, 1]), ease easeOut. Stagger each word by delay = (i * 100)/1000 seconds. Each word is
display:inline-block with marginRight:0.28em (NOT a non-breaking space — tight letter-spacing eats it). The parent <p>
is display:flex; flex-wrap:wrap; justify-content:[center]; rowGap:0.1em. Usage:
<BlurText text="[Venture Past Our Sky]" className="[hero heading classes]" />.
```

## 25 · `WordsPullUp` — Words Slide Up

```text
Build a `WordsPullUp` component: split the text on spaces and render each word as a motion.span animating y:20→0,
opacity 0→1, staggered by delay [0.08]s per word, triggered by useInView({ once:true }). [Optional showAsterisk prop ?]
adds a superscript "*" after the final word’s last "a" (absolute top-[0.65em] -right-[0.3em] text-[0.31em]). Usage:
<WordsPullUp text="[Prisma]" className="[giant heading classes]" />.
```

## 26 · `WordsPullUpMultiStyle` — Mixed-Style Pull-Up

```text
Build a `WordsPullUpMultiStyle` component that takes an array of { text, className } segments, splits ALL of them into
individual words while preserving each segment’s className, then runs the same y:20→0 / opacity 0→1 pull-up (stagger
[0.08]s, useInView once). Wrap the words in an inline-flex flex-wrap justify-center container. Example segments:
[{ text:"I am [Marcus Chen],", className:"font-normal" },
 { text:"a [self-taught director].", className:"italic font-serif" },
 { text:"I have skills in [color grading and VFX].", className:"font-normal" }].
```

## 27 · `ScrambleIn` — Character Scramble-In (scroll-aware)

```text
Build a `ScrambleIn` component (props: text, scrollProgress, delay, trigger). Use this character set:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()_+~|}{[]:;?><
When triggered AND scrollProgress < 0.015: scramble in left→right over 900ms — each character has an index-based
threshold and transitions blank → random glyph → final character. When scrollProgress > 0.015: scramble OUT over 700ms
with opacity fading to 0. Initial state: non-breaking spaces matching the final text width (no layout shift). Use it for
headings like "[Brain]" / "[And Body]", each on its own line, font-light, leading-[0.95].
```

## 28 · `ScrambleText` — Hover Decode

```text
Build a `ScrambleText` component (props: text, isHovered, className). On hover, run a progressive left→right decode at
~40fps (25ms interval): each character index decodes at frame index*4, for a total of length*4 + 4 frames. On unhover,
instantly reset to the original text. Wrap any label: <ScrambleText text="[Download]" isHovered={hovered} />.
```

## 29 · Scroll Char-Opacity Reveal — `AnimatedLetter`

```text
Wrap each character of [PARAGRAPH_TEXT] in an `AnimatedLetter` so the paragraph brightens as the reader scrolls past it.
Use useScroll with target offset ['start 0.8', 'end 0.2']. Each character’s opacity transitions 0.2 → 1 based on scroll
position, staggered via charProgress = index / totalChars over the range [charProgress - 0.1, charProgress + 0.05]. The
container is text-xs sm:text-sm md:text-base, color [#DEDBC8], leading-relaxed, max-w-[560px].
```

## 30 · `ShinyText` — Animated Gradient Sweep on Text

```text
Apply an animated gradient sweep to "[Revitalized]": fill the text with a gradient (see “Gradient / Shiny Text”), set
background-size:200%, and add animation: shiny [6s] linear infinite, with @keyframes shiny{ 0%{background-position:-200%
center} 100%{background-position:200% center} }. Use it as the accent line of a two-line headline.
```

## 31 · `FadeIn` — Generic Entrance Wrapper

```text
Build a reusable `FadeIn` wrapper with Framer Motion: initial {opacity:0, x:[0], y:[20]} animating to {opacity:1, x:0,
y:0}, transition {delay:[0], duration:[0.9], ease:[0.22, 1, 0.36, 1]}, viewport {once:true}. Apply across the hero with
these values: nav (delay 0, y -20), heading (delay 0.15, y 40), body text (delay 0.35, y 20), CTA (delay 0.5, y 20).
```

## 32 · `InViewAnimation` — Staggered Children Reveal

```text
Build an `InViewAnimation` wrapper for grids/lists: children animate from {scale:0.95, opacity:0} to {scale:1,
opacity:1}, triggered by useInView({ once:true, margin:"-100px" }), staggered by [0.15]s, ease [0.22, 1, 0.36, 1]. Wrap
each grid card and pass its index for the stagger delay.
```

---
### MOTION UTILITIES
---

## 33 · `Magnet` — Element Leans Toward Cursor

```text
Build a `Magnet` component that pulls its child toward the cursor. Track the mouse within a padding radius of [150]px
around the element; while inside, translate the child toward the cursor by (distance / [strength = 3]); while outside,
return it to 0. Use activeTransition "transform 0.3s ease-out" and inactiveTransition "transform 0.6s ease-in-out".
Usage: <Magnet padding={150} strength={3}>[child element]</Magnet>.
```

## 34 · Scroll-Reactive Marquee (two rows, opposite directions)

```text
Build two rows of tiles that translate horizontally based on page scroll position (not autoplay). Row 1 is the first
half of [IMAGE_LIST], tripled for a seamless wrap, moving RIGHT: translateX(offset - 200). Row 2 is the second half,
tripled, moving LEFT: translateX(-(offset - 200)). Compute offset = (scrollY - sectionTop + innerHeight) * [0.3]. Each
tile is [420×270]px, rounded-2xl, object-cover, lazy-loaded; use gap-3 between tiles and between rows. Set
willChange:'transform' and use a passive scroll listener.
```

## 35 · GSAP Infinite Loop Marquee (text ticker)

```text
Build an endless text ticker: a row repeating "[BUILDING THE FUTURE • ]" [×10], animated with GSAP — xPercent:-50,
duration [40], ease:"none", repeat:-1. Style it font-display [italic ?], uppercase, large. [Optional: pause on hover ?].
```

## 36 · Lenis Smooth Scroll (desktop only)

```text
Initialize Lenis for buttery site-wide scrolling, desktop only — disable it when the UA string is mobile or screen
width < 768. Config: duration [1.2], easing (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)), smoothWheel:true,
wheelMultiplier [1.0], touchMultiplier [1.5]. Drive it with requestAnimationFrame. Dependency: lenis ^1.3.x.
```

## 37 · Custom Cursor

```text
Build a custom cursor: a fixed [10px] dot plus a lagging [36px] ring, both pointer-events:none with mix-blend-mode
[difference]. The ring follows the dot with LERP smoothing. On hover over [data-cursor] targets, the ring scales to
[2.5] and the dot hides. Hide the native cursor. Disable the whole effect on touch devices.
```

## 38 · GSAP Pinned Parallax Gallery

```text
Build a min-h-[300vh] section for scroll-driven parallax:
• LAYER 1 (z-10): an h-screen block pinned with ScrollTrigger.create({ pin:contentRef, pinSpacing:false }) — containing
  an eyebrow "[Explorations]", a heading "[Visual *playground*]" (last word in font-display italic), subtext, and a
  "[Dribbble]" button.
• LAYER 2 (z-20, absolute): a grid grid-cols-2 gap-12 md:gap-40 inside max-w-[1400px], with [6] items split across the
  two columns, each driven up/down at a different parallax rate via GSAP. Cards are aspect-square max-w-[320px] with a
  slight rotation and a lightbox on click.
Dependency: gsap (ScrollTrigger).
```

---
### CONTENT SECTIONS
---

## 39 · Feature / Services Card Grid

```text
Build a 4-column feature grid (lg:h-[480px], gap-3 sm:gap-2 md:gap-1; 1 column on mobile → 2 on md → 4 on lg). Each card
enters with the InViewAnimation pattern (scale 0.95 + fade, stagger 0.15s):
• Card 1 (media): a full [video / image] background, object-cover, with bottom text "[Your creative canvas]".
• Cards 2–4 (bg-[#212121], rounded): a [10×10] rounded icon [ICON_URL] at top; a title with number "[01]"; a list of
  [3–4] checklist rows (lucide Check icon in [ACCENT], label text-gray-400); and a "[Learn more]" link with an ArrowRight
  rotated -45deg. Card titles: [Project Storyboard], [Smart Critiques], [Immersion Capsule].
```

## 40 · Bento Grid (asymmetric project tiles)

```text
Build a bento grid: grid grid-cols-1 md:grid-cols-12 gap-5 md:gap-6 with column spans alternating [7 / 5 / 5 / 7]. Use
[4] cards: [Automotive Motion], [Urban Architecture], [Human Perspective], [Brand Identity]. Each card is bg-[surface]
border border-[stroke] rounded-3xl, with an image (object-cover group-hover:scale-105), a halftone overlay
(radial-gradient(circle, #000 1px, transparent 1px) at 4×4px, opacity-20 mix-blend-multiply), and on hover a
bg-[bg]/70 layer fading opacity 0→1 with backdrop-blur-lg plus a reveal label — a pill with an animated gradient border,
white background, reading "View — *[Title]*" (title in font-display italic).
```

## 41 · Projects / Work Gallery (horizontal pills)

```text
Build a list of [4] project entries rendered as wide horizontal pills, rounded-[40px] sm:rounded-full: flex items-center
gap-6 p-4 bg-[surface]/30 hover:bg-[surface] border border-[stroke]. Each entry has a thumbnail image, a "[Title]", a
[read time], and a [date]. Stagger the entrances with FadeIn (delay i*0.1).
```

## 42 · Testimonials Grid (glass quotes)

```text
Build a testimonials section: max-w-6xl mx-auto px-6 py-20 md:py-28 border-t border-white/10, containing a 3-column grid
of `.liquid-glass rounded-2xl p-6` figures. Each figure has a blockquote (text-sm text-white/80 leading-[1.6], wrapped in
quotes) and a figcaption mt-6 pt-5 border-t border-white/10 with a name (text-sm font-semibold), role (text-xs
text-white/50), and company in UPPERCASE (text-xs text-white font-semibold tracking-wide). Provide [3] entries:
"[quote]" — [Name], [Role], [COMPANY].
```

## 43 · Testimonial Carousel (auto-scroll, infinite)

```text
Build an auto-scrolling testimonial carousel: it advances every [3s] and pauses on hover, with prev/next circular buttons
(w-12 h-12 rounded-full, border border-[#0D212C]/20, lucide ChevronLeft / ChevronRight). Triple the testimonials array
for an infinite-scroll effect; the transform uses transition 0.8s cubic-bezier(0.4, 0, 0.2, 1). Provide [5] testimonials,
each with an [avatar], [name], [role], and [quote].
```

## 44 · Pricing — 3-Tier with Billing Toggle + Watermark

```text
Build a pricing section, centered, overflow-x:hidden, with a giant two-line watermark headline behind the cards:
"[Your email.]" (white) over "[Revitalized]" (gradient text), font-size 9rem, font-weight 800, line-height 0.9,
letter-spacing -0.05em [filter:url(#noise) ?]. Hold a `yearly` boolean toggle in state. Lay out three plans in a 3-column
grid (gap 24px, max-w-1100px):
• [Free] — price "[Free]" — "[description]" — [feature list].
• [Standard] — monthly "[$9.99/m]" / yearly "[$99.99/y]" — "[description]" — [feature list].
• [Pro] (highlighted) — monthly "[$19.99/m]" / yearly "[$199.99/y]" — "[description]" — [feature list].
Each card (keep these exact values): background linear-gradient(135deg, rgba(0,0,0,0.7), rgba(0,0,0,0.4));
backdrop-filter blur(14px); border 1px solid rgba(255,255,255,1); border-radius 44px; padding 50px 24px; min-height
580px; transition all 0.6s cubic-bezier(.22,1,.36,1); hover translateY(-12px) scale(1.01) with border-color [ACCENT].
Inside each: a tier label (muted), a big price (font-size 2.8rem), a description, a checkmark list (28px circle + white
check), and a "[Choose Plan]" pill button (background #fff, color #000, border-radius 100px). The toggle is a 52×28 pill
whose knob translateX(24px) when active. On mobile (<1024px): watermark drops to 3.5rem (filter:none) and the grid
becomes a horizontal scroll-snap row (cards flex 0 0 320px, scroll-snap-align center, scrollbar hidden).
```

## 45 · Final CTA Panel

```text
Build a closing CTA section: max-w-6xl mx-auto px-6 py-20 md:py-32, holding a `.liquid-glass relative overflow-hidden
rounded-3xl px-8 py-16 md:py-24 text-center` panel with a radial glow overlay: radial-gradient(600px circle at 50% 0%,
rgba(255,255,255,0.15), transparent 70%) at opacity 0.3. Inside: an h2 (text-4xl md:text-6xl font-semibold tracking-tight
leading-[1.02]) reading "[Close the tabs.]" / "[Open your day.]"; a paragraph (mt-6 text-white/60 max-w-md mx-auto text-sm
leading-[1.6]) "[supporting line]"; and two buttons — a primary "[Download]" plus a secondary rounded-full border
border-white/15 px-5 py-3 hover:bg-white/5 "[Talk to sales]" with a trailing ChevronRight.
```

## 46 · Stats Strip

```text
Build a stats strip: py-16 md:py-24, a 3-column grid of big numbers with labels — "[20+]" [Years Experience], "[95+]"
[Projects Done], "[200%]" [Satisfied Clients]. Numbers in font-display, large; labels muted, uppercase, tracking-wide.
[Optional count-up on scroll-in ?].
```

---
### BUTTONS
---

## 47 · Solid Pill Button

```text
Build a solid pill button: bg-[ACCENT = #7342E2] text-white font-medium rounded-full px-5 py-2.5, text size
[clamp(0.9rem, 2vw, 1rem)] [with box-shadow 0 4px 24px [ACCENT]/28 ?]. Label "[Get It Free]" [with a trailing
ArrowRightCircle icon (20px) ?]. Hover: scale(1.04) + brightness(1.1); tap: scale(0.96).
```

## 48 · Glass CTA Button

```text
Build a glass CTA button for the primary action over video: .liquid-glass[-strong] rounded-full px-[14] py-[5]
text-base text-[INK] reading "[Begin Journey]". Hover: scale(1.03), cursor-pointer.
```

## 49 · Apple / Download Button

```text
Build an `AppleButton`: h-12 px-6 bg-white rounded-full, flex items-center gap-2, containing a Bootstrap-Icons apple
glyph and the text "[Download [BRAND]]" with the ScrambleText hover-decode effect on the label. whileHover scale 1.03
with background [#e2e2e6]; whileTap scale 0.97. No href.
```

## 50 · Arrow-Circle Button

```text
Build a `ContactButton`: a pill bg-[ACCENT] with [INK-on-accent] text, font-medium, plus a trailing circle
(w-9 h-9 sm:w-10 sm:h-10 rounded-full bg-black) holding an ArrowRight icon. On hover the gap widens (hover:gap-3) and the
circle scales up (group-hover:scale-110). Label "[Join the lab]".
```

---
### FOOTER
---

## 51 · Footer Columns

```text
Build a footer: bg-[surface = #fafafa] pt-20 pb-5, container max-w-[1100px] mx-auto px-5. Columns:
• Brand column: logo + a one-line "[mission statement]".
• "[Navigation]": links [Features, Benefits, Testimonials, Pricing] — each <a> text-[#888] text-[0.85rem]
  hover:text-[INK] transition-colors.
• "[Resources]" / "[Company]": [link list].
Each <h4> is font-semibold mb-5 text-[0.95rem]; each <li> is mb-3. [Optional giant wordmark watermark behind it ?].
[Optional flipped background video at bg-black/60 ?].
```

## 52 · Social Row + Availability Dot

```text
Build a bottom footer bar, flex justify-[center | between]: a row of social icon buttons [Twitter, LinkedIn, Dribbble,
GitHub] (each .liquid-glass rounded-full p-4 text-white/80 hover:text-white, with an aria-label), plus a green pulsing
dot and the text "[Available for projects]". [Optional © line ?].
```

---
### 3D & SPLINE SCENES
---

## 53 · Spline 3D Scene (lazy-loaded, with fallback)

```text
Add an interactive 3D model powered by Spline. Install @splinetool/runtime and @splinetool/react-spline. Build a
`SplineScene` component (mark the file 'use client') that lazy-loads the renderer so the heavy WebGL bundle never blocks
first paint: const Spline = lazy(() => import('@splinetool/react-spline')). Wrap
<Spline scene={[SCENE_URL]} className={className} /> in <Suspense> whose fallback is a w-full h-full flex items-center
justify-center holding a [spinner <span class="loader"> | "[Loading…]" text | pulsing skeleton]. Props: `scene` (the
prod.spline.design "[…/scene.splinecode]" URL) and an optional `className` for sizing. Render it at [w-full h-full] and
let the parent set dimensions. [Optional: gate interaction until in view — pointer-events-none until an IntersectionObserver
fires ?]. Keep the lazy() + Suspense pattern exactly — it is what stops the 3D payload from janking the initial load.
```

## 54 · Spotlight Beam Overlay (SVG)

```text
Add a `Spotlight` SVG that sweeps a soft cone of light across a dark section. Render an absolutely-positioned
pointer-events-none <svg>, z-[1], opacity-0, h-[169%] w-[138%] lg:w-[84%], with an `animate-spotlight` class and viewBox
"0 0 3787 2842". Inside a <g filter="url(#filter)"> place one <ellipse cx=1924.71 cy=273.501 rx=1924.71 ry=273.501>
transformed by matrix(-0.822377 -0.568943 -0.568943 0.822377 3631.88 2291.09), fill=[FILL = white], fill-opacity 0.21.
Define <filter id="filter"> as a feGaussianBlur stdDeviation 151 over a ~3785×2840 userSpaceOnUse region. Accept a
`className` prop for placement (e.g. "-top-40 left-0 md:left-60 md:-top-20") and a `fill` prop. Make it animate itself in
— add the keyframe:
@keyframes spotlight { 0% { opacity:0; transform:translate(-72%,-62%) scale(0.5) } 100% { opacity:1; transform:translate(-50%,-40%) scale(1) } }
.animate-spotlight { animation: spotlight 2s ease 0.75s 1 forwards }
Keep the ellipse geometry and the blur radius exactly — they are what make the beam read as light rather than a blob.
Use it only on near-black surfaces.
```

## 55 · Interactive 3D Split Hero (copy · scene)

```text
Build an interactive 3D hero that pairs editorial copy with a live Spline model. Outer container: a `Card` (see “shadcn
Card”) w-full h-[500px] bg-black/[0.96] relative overflow-hidden. Drop a <Spotlight> (see “Spotlight Beam Overlay”) at
className "-top-40 left-0 md:left-60 md:-top-20" fill="white". Inside, a flex h-full two-up split:
• LEFT (flex-1 p-8 relative z-10, flex flex-col justify-center): an h1 text-4xl md:text-5xl font-bold rendered as
  gradient text (bg-clip-text text-transparent bg-gradient-to-b from-neutral-50 to-neutral-400) reading "[Interactive 3D]";
  below it a paragraph mt-4 text-neutral-300 max-w-lg "[Bring your UI to life with beautiful 3D scenes…]"; [Optional CTA
  row — see “Solid Pill Button” / “Glass CTA Button” ?].
• RIGHT (flex-1 relative): <SplineScene scene="[SCENE_URL]" className="w-full h-full" /> (see “Spline 3D Scene”).
[Optional: collapse to one column on mobile (flex-col) — scene on top, copy beneath ?]. The whole effect is the near-black
card + the spotlight beam + the model's own lighting, so keep the background near-black and add no competing overlay.
```

---
### LOADERS & PROGRESS
---

## 56 · Shimmer / Pulse Skeleton (theme-switched)

```text
Build a `Skeleton` placeholder primitive whose loading animation switches by theme — a horizontal SHIMMER sweep in light
mode, a soft PULSE in dark mode — driven by one CSS variable so no JS branching is needed. In :root set
--skeleton-animation: shimmer; in .dark override to --skeleton-animation: pulse. Define both keyframes exactly:
@keyframes skeleton-shimmer { 100% { transform: translateX(200%) } } and
@keyframes skeleton-pulse { 50% { opacity: 0.55 } }. Base block: rounded-lg bg-[#e9e9ec] dark:bg-white/10 relative
overflow-hidden. LIGHT — an ::after layer (absolute inset-0, background
linear-gradient(90deg, transparent, rgba(255,255,255,0.65), transparent), starting translateX(-100%)) runs
skeleton-shimmer [1.4s] ease-in-out infinite. DARK — the ::after is hidden and the block itself runs skeleton-pulse
[1.8s] ease-in-out infinite. Compose a demo card: a `.shadow-panel w-[250px] space-y-5 rounded-lg bg-transparent p-4`
wrapper holding one h-32 rounded-lg block over three text-line bars (h-3 rounded-lg, widths [w-3/5], [w-4/5], [w-2/5]).
Keep the two keyframes and the var-swap exactly — that single variable is what makes one component serve both themes.
```

## 57 · Progressive Flux Loader (3D phase labels + sheen)

```text
Build a `ProgressiveFluxLoader` — a glossy progress bar with a 3D "fly-in" phase label above it. Works controlled (pass
`value` 0–100) or uncontrolled (self-runs a sweep over [duration = 12]s, then loops after a 700ms pause). Drive the label
from a phases array of { at, label } where the label switches once each threshold is crossed; default phases
[{0,"starting up"},{25,"loading assets"},{55,"preparing magic"},{80,"almost there"},{100,"all done"}]. Dependency:
framer-motion.

TRACK: relative h-5 w-full overflow-hidden rounded-full bg-muted with inset shadow
[inset_0_2px_3px_rgba(0,0,0,0.09),inset_0_-1px_2px_rgba(255,255,255,0.7)] (darker inset variant in dark mode). Give it
role="progressbar", aria-valuenow, and aria-valuetext "`{pct}% – {label}`".

FILL: a motion.div whose width animates to `{pct}%` with transition { duration: 0.55, ease: [0.22, 1, 0.36, 1] }.
Background is the signature flux gradient, read from two CSS vars so it can be recolored per instance — --flux-from
(default #1d6ffb), --flux-to (default #74e1ff), mid = color-mix(in oklab, var(--flux-from), var(--flux-to)):
linear-gradient(90deg, from 0%, mid 35%, to 55%, mid 78%, from 100%). Box-shadow stacks a colored glow from the same
palette, a white top-edge highlight, and a deep-blue inset:
0 0 18px color-mix(from 55%,transparent), 0 0 32px color-mix(to 40%,transparent),
inset 0 1.5px 0 rgba(255,255,255,0.5), inset 0 -2px 3px rgba(0,40,120,0.35).

SHEEN: inside the fill, an absolute inset-y w-1/2 rounded-full span, background
linear-gradient(90deg, transparent, rgba(255,255,255,0.55) 50%, transparent), mixBlendMode:'screen', animating
x ['-110%','210%'], duration 1.6s linear infinite.

3D LABEL: a [h-16] container with perspective:1000px. On each label change use AnimatePresence mode="wait" on a
motion.div (transformStyle:'preserve-3d'), initial { opacity:0, z:-380, scale:0.65, filter:'blur(14px)' }, animate the
keyframes z:[-380,60,-8,0] / scale:[0.65,1.08,0.985,1] / filter blur 14→0, exit { opacity:0, z:220, scale:1.35,
blur(10px) }, transition { duration:0.9, ease:[0.22,1,0.36,1] }. Inside, split the label into chars; each char rises from
{ opacity:0, y:12, blur(8px) } to { opacity:1, y:0, blur(0) } with delay 0.18 + i*0.035, duration 0.45. Mark the label
aria-hidden (the progressbar carries the value). Under prefers-reduced-motion render the label as static text and animate
width instantly. Container: mx-auto w-full max-w-md flex flex-col items-center gap-8. Keep the z-fly-in keyframes, the
sheen sweep, and the gradient/shadow recipes exactly — they are the engine.
```

---
### PAGINATION & CONTROLS
---

## 58 · Pagination (prev · numbered · next)

```text
Build a `Pagination` control: hold `page` in state (1-based) against [totalPages = 3], laid out as a centered row
(flex justify-center items-center gap-1). Three parts:
• PREVIOUS — a pill (h-9 px-3 rounded-full inline-flex items-center gap-1.5 text-sm) holding a lucide ChevronLeft +
  "[Previous]"; disabled when page === 1 (opacity-40 pointer-events-none); onClick page → page−1.
• NUMBERED links — map 1…totalPages to square buttons (w-9 h-9 rounded-full grid place-items-center text-sm). The active
  page (p === page) is bg-[ACCENT = #7342E2] text-white; the rest text-[muted] hover:bg-black/5 dark:hover:bg-white/10;
  onClick sets page = p.
• NEXT — mirror of Previous: "[Next]" + a lucide ChevronRight; disabled when page === totalPages; onClick page → page+1.
Every button gets focus-visible:ring-2 ring-[ACCENT] and transition-colors. In a React artifact wire it with onClick — do
NOT use a <form>. [Optional: render the buttons as .liquid-glass pills (see "Liquid Glass") for an over-video placement ?].
```

---
### TEXT ANIMATION PRIMITIVES — Hover Reveal
---

## 59 · `CascadeText` — Per-Char Roll-Up on Hover

```text
Build a `CascadeText` component (props: text, [staggerDelay = 25]ms, [duration = 250]ms, [direction = up | down], color,
[hoverColor = #b2c73a], [fontSize = 3rem]) that rolls each character vertically on hover to reveal an identical copy
sliding in from below — a split-flap / odometer feel achieved with a text-shadow clone, no duplicated DOM. Mechanism,
keep exact:
• Split `text` into grapheme clusters with Intl.Segmenter("en",{granularity:"grapheme"}) (fallback [...text]) so emoji
  and accents stay intact.
• Outer wrapper: inline-block relative overflow-hidden font-extrabold uppercase tracking-tight cursor-pointer select-none,
  padding 0.15em 0.4em, line-height 1, color transition 0.35s ease (color → hoverColor on hover).
• Inner span: inline-flex overflow-hidden, height:1em.
• Each character span: inline-block will-change-transform, textShadow `0 {sign}em currentColor` (sign = +1 for direction
  up, −1 for down — the shadow IS the second copy), transition `transform {duration}ms {easing = ease-in-out}`,
  transitionDelay `{i * staggerDelay}ms`. On hover translateY({-sign}em); render a space as \u00A0.
Default tag is <a> (href "#", target/rel handled) but allow an `as` prop to swap it. Memoize the component. Usage:
<CascadeText text="[Hover me]" hoverColor="[#b2c73a]" />. Use it for nav links, oversized menu items, or footer links.
```

---
### CAROUSELS & INTERACTIVE GALLERIES
---

## 60 · Card Fan Carousel (GSAP fan + hover spread)

```text
Build a `CardFanCarousel` (GSAP) — a horizontal fan of portrait cards that deals in on load, spreads on hover, and
paginates with infinite wrap when there are more cards than fit. Dependency: gsap. Cap visible cards at 7 (HALF = 3).
Lock the fan geometry to these 7 slots (rot°, scale, x-rem, y-rem, zIndex), keep exact —
[-21,0.7756,-30,7.3,1] [-14,0.8498,-22,4.0,2] [-7,0.9346,-11,1.3,3] [0,1.0,0,0,10] [7,0.9346,11,1.3,3]
[14,0.8498,22,4.0,2] [21,0.7756,30,7.3,1]. With fewer than 7 cards, interpolate each slot from its signed distance d to
center: rot = d*21, scale = 1 − 0.2244*d², x = d*30, y = d²*7.3, zIndex = 10 − |offsetFromCenter|.

RESPONSIVE: multiply all x-offsets and entry distances by a width multiplier [<480:0.28, <640:0.38, <768:0.5,
<1024:0.75, else 1.0], and multiply all y-offsets by a height multiplier = min(1, (innerHeight*0.7) / idealHeightPx) so
the fan never overflows a short viewport.

LOAD: each card deals in from { x:0, y:12rem, rotation:0, scale:0.5, opacity:0 } to its slot with
ease "elastic.out(1.05,.78)", duration 1.2, delay 0.2 + slot*0.06.

HOVER: hovering a card lifts it (y −= 2.5rem, scale *= 1.08) and shoves its neighbors outward — pushStrength =
8 * (1 − |normalized|) * (1 + 0.2*max(0, 3 − distance)); left neighbors x −= push & rot −= 3/(dist+1), right neighbors
the mirror — all with ease "elastic.out(1,.75)", duration 0.5, stagger distance*0.02. Restore on container mouseleave
(50ms debounce).

PAGINATION (only when cards > 7): prev/next circular buttons [w-10 h-10 md:w-12 md:h-12 rounded-full border
border-black/10 dark:border-white/10 bg-black/5 dark:bg-white/5 backdrop-blur-[16px]] with a chevron SVG, plus a dot row
(active dot bg-black/70 dark:bg-white/80 scale-[1.3]). Cycling steps the center index with modulo wrap; entering cards fly
in from ±40rem / rotation ±30 / scale 0.5, exiting cards leave to ∓40rem / rotation ∓30 / opacity 0.

Each card: rounded portrait image, object-cover, lazy-loaded, optional linkUrl (target _blank for http). Pass a `cards`
array of { imgUrl, alt?, linkUrl? } — provide [7–10] entries. Keep the slot table and the two elastic eases exactly; they
are what make the fan feel physical.
```

## 61 · Scroll-Reel Testimonials (counter-rotating reel + char rise)

```text
Build a `ScrollReelTestimonials` — a quote panel beside a 3-column portrait "reel": the middle column is a real vertical
list of portraits, the two outer columns are blurred placeholder cells, and on each step the middle slides one pitch while
the outer columns counter-slide the opposite way. Lock the geometry: CELL = 121.33px, GAP = 8px, STEP = 3*(CELL+GAP) =
388px. Per step, middleY = (centerIndex − index) * STEP and sideY = −middleY; transition both with
`transform 800ms cubic-bezier(0.65,0,0.35,1)`, enabled only after first paint (so it starts at its offset, no slide-in).

REEL: a [w-[380px]] overflow-hidden box with a double mask that fades all four edges —
maskImage: linear-gradient(to right, transparent, black 14%, black 86%, transparent),
linear-gradient(to bottom, transparent, black 10%, black 90%, transparent) with maskComposite:intersect. Placeholder
Cell: 121.33² rounded-xl border bg-gradient-to-b from-secondary to-card blur-[1px]. Featured tile: 121.33² rounded-xl
overflow-hidden, image object-cover object-[center_30%], plus two overlays — a white mix-blend-saturation layer
(desaturate) and a diagonal sheen
linear-gradient(220.99deg, rgba(108,92,255,0) 32%, #6c5cff 41%, #adb1ff 47%, rgba(130,189,237,0.57) 54%, transparent 65%)
blur-[6px] mix-blend-overlay. Build the middle list as: 3 lead cells, then [featured + 2 cells] per testimonial, then 3
trailing cells.

TEXT — per-character rise: on each change, the OLD block first runs @keyframes scroll-reel-exit { from {opacity:1;
transform:translateY(0)} to {opacity:0; transform:translateY(-12px)} } over 240ms; THEN the new block mounts and each
character rises via @keyframes scroll-reel-char-rise { to { opacity:1; transform:translateY(0) } } with inline
animation-delay = charIndex * [charStaggerMs = 6]ms (split words into nowrap spans so wrapping is preserved). Keep an
invisible in-flow copy of the current quote+author to size the stage so wrapped text never clips. Mark it aria-live polite.

CONTROLS: a large decorative quote glyph, then prev/next circular buttons (h-6 w-6 rounded-full border
border-foreground/15, hover scale 1.08, disabled opacity-40) gated at the first/last index; also support ArrowLeft /
ArrowRight keys. Lock interactions during the 800ms slide. Pass a `testimonials` array of { quote, author, image, alt? } —
provide [3]. Container: max-w-[1060px] rounded-xl border bg-muted, flex-col on mobile → md:flex-row. Keep STEP, the two
keyframes, and the counter-rotation (sideY = −middleY) exactly.
```

---
### INTERACTIVE CANVAS EFFECTS
---

## 62 · Ink Reveal (canvas brush-erase overlay)

```text
Build an `InkReveal` canvas overlay — an absolutely-positioned <canvas> (inset-0, z-1, cursor:none) that starts fully
painted in [maskColor = rgb(252,250,248)], hiding whatever sits beneath it; as the cursor moves, organic ink "stamps"
ERASE the paint (canvas destination-out) to reveal the layer below, and each stamp blooms then fades. Pure canvas, no
deps. Engine, keep exact:
• Each frame: refill the whole canvas with maskColor (globalCompositeOperation 'source-over'), then switch to
  'destination-out' and redraw every live stamp — so erased areas show through and re-heal as stamps die.
• A stamp is a wobble blob, not a clean circle: trace [segments = 36] points where radius *= 0.78 + 0.14*sin(3a+seed) +
  0.08*sin(5a+2.1·seed) + 0.05*sin(7a+0.7·seed), filled with a radial gradient (rgba(0,0,0,0.95·α) center → 0.88·α at 0.5
  → 0 at edge), inner-radius factor 0.2.
• Growth: radius eases rStart [10]px → rmax with 1−(1−t)³; alpha = 1−t²; lifetime [600]ms; rmax = [brushSize = 128] *
  (1 − [rVary = 0.45] + random·rVary).
• stampAlong: between the last and current pointer position, drop a stamp every [stampStep = 10]px (ceil(dist/step)
  steps) so fast strokes stay continuous. Cap live stamps at [maxStamps = 200] (shift the oldest).
• Sizing: devicePixelRatio capped at 2; re-fill maskColor on resize.
Drive it from onMouseEnter / onMouseMove (compute pos relative to the canvas rect) and start a requestAnimationFrame loop
that stops itself once no stamps remain. Place it over any image/section to make it "wipe on" under the cursor. Keep the
wobble formula, the destination-out refill, and the ease/alpha curves exactly — they are what make it read as ink, not an
eraser.
```

## 63 · Pixel Canvas Background (animated pixel ripple)

```text
Build a `PixelCanvas` animated background — a <canvas> (absolute inset-0, block w-full h-full) that fills its box with a
grid of tiny squares spaced every [gap = 6]px; each square grows in then shimmers, and the grid blooms OUTWARD from the
center like a ripple. Pure canvas, no deps. Engine, keep exact:
• Build one pixel per grid cell. Per pixel: speed = rand(0.08,0.4) * baseSpeed, sizeStep = rand(0.12,0.28), maxSize =
  rand(0.5,2), and a `delay` = distance from canvas center (√(dx²+dy²)) * 0.65 — the delay is what staggers the ripple
  from the middle out. baseSpeed (effectiveSpeed) = min([speed = 30],100) * 0.001.
• appear(): while a per-pixel counter ≤ delay, increment it and draw nothing; after the delay, grow size by sizeStep
  until it reaches maxSize, then flip to shimmer().
• shimmer(): bounce size between minSize 0.5 and maxSize at ±speed (reverse at the ends) so the field gently twinkles
  forever.
• disappear(): shrink size by 0.1 until 0, then mark the pixel idle (used to fade the field out).
• Each pixel picks a random color from a `colors` array; draw with fillRect at the cell origin plus a small centering
  offset.
Throttle the loop to ~60fps (skip frames under 1000/60ms), re-init on a ResizeObserver, and under prefers-reduced-motion
set all delays to 0. Pass `colors` (e.g. derive 4 muted tones + 1 accent from your theme tokens), `gap`, `speed`. Layer a
radial mask over it — radial-gradient(circle at center, transparent 0%, var(--bg) 100%) at ~0.8 opacity — so the field
fades into the page edges. Keep the center-distance delay and the grow→shimmer state machine exactly; they are the ripple.
```

---
### HERO BLOCKS — Continued
---

## 64 · Pixel-Perfect Hero (pixel canvas · glass text · logo marquee)

```text
Build a `PixelHero` — a full-height hero (relative w-full min-h-[100dvh] bg-background overflow-hidden) layered over the
animated `PixelCanvas` (see "Pixel Canvas Background"), feeding it colors derived from theme tokens
[muted, muted, muted, muted, [ACCENT/primary]] and gap 6. Stack, back to front:
• BACKGROUND: <PixelCanvas /> at z-0 pointer-events-none, with a radial mask
  radial-gradient(circle at center, transparent 0%, var(--background) 100%) at opacity-80 so it fades into the edges.
• HEADLINE: an h1 of two words on a "[liquid/tahoe] glass text" treatment — word1 "[Silent]" in font-serif italic, word2
  "[Precision.]" in font-sans font-extrabold tracking-tighter, sizes text-[2.8rem] → md:text-8xl lg:text-9xl leading-none.
  The glass fill, keep exact: color transparent; background linear-gradient(135deg, rgba(255,255,255,1) 0%, .4 25%, .1 45%,
  .9 55%, .2 75%, 1 100%); background-size 200% auto; -webkit-background-clip text; -webkit-text-stroke 1.5px
  rgba(255,255,255,0.3); filter drop-shadow(0 15px 35px rgba(0,0,0,0.4)) drop-shadow(0 5px 10px rgba(0,0,0,0.2)); plus
  @keyframes shimmer { 0%{background-position:200% center} 100%{background-position:0% center} } running 8s linear infinite.
• SUBHEAD: a font-light text-foreground/85 paragraph "[Minimalist interfaces driven by refined motion…]", max-w-xl.
• LOGO MARQUEE: an eyebrow "[Trusted by industry leaders]" over a row of [4–6] brand logos (inline SVGs, opacity-60
  hover:opacity-100), duplicated back-to-back and animated with @keyframes marquee { 0%{translateX(0)}
  100%{translateX(-50%)} } 25s linear infinite, inside a
  [mask-image:linear-gradient(to_right,transparent,white_15%,white_85%,transparent)] track. Show it in the center block on
  mobile and absolutely pinned bottom-8 on desktop.
• CTAs: a primary pill "[Explore Design]" — bg-gradient-to-b from-primary/90 to-primary text-primary-foreground rounded-xl
  with an inset highlight + lucide ArrowRight; and a secondary "[View GitHub]" — bg-gradient-to-b from-card/80 to-card
  ring-1 ring-border backdrop-blur-md with a lucide Github icon. Both hover:scale-[1.02] active:scale-[0.98].
Reveal the CTA row + desktop marquee with an isLoaded fade-up (opacity-0 translate-y-8 → opacity-100 translate-y-0,
duration-1000, staggered transitionDelay 450ms / 600ms). Props: word1, word2, description, primaryCta, secondaryCta,
githubUrl. Dependency: lucide-react. Keep the glass-text recipe and the marquee keyframe exactly.
```

---
### MARQUEE — Continued
---

## 65 · Infinite Ribbon (rotating marquee banner)

```text
Build an `InfiniteRibbon` — a full-width marquee banner that scrolls a phrase sideways forever and can be tilted. Props:
[repeat = 5], [duration = 10]s, [reverse = false], [rotation = 0]°, children. Outer bar: w-full overflow-hidden
bg-[#facc15] py-1 text-black text-lg (dark:bg-yellow-500), rotated via transform rotate({rotation}deg). Track: a flex
w-max whitespace-nowrap row containing the child repeated repeat*2 times (each mr-8 inline-block select-none), animated
linear infinite over {duration}s with — keep exact —
@keyframes iconiq-infinite-ribbon { from { transform: translateX(0) } to { transform: translateX(-50%) } } (and a
…-reverse variant from -50% → 0). The duplicate-and-translate-(-50%) pair is what makes the loop seamless; switching
`reverse` swaps the keyframe. Add an sr-only copy of the children for screen readers and mark the visible track
aria-hidden. Under prefers-reduced-motion force animation-duration 1ms / iteration 1. Stack two of them at rotation +5 and
−5 with `reverse` flipped for a crossing-ribbons hero accent. Use it as a section divider, a hero accent, or a
"now shipping" banner.
```
