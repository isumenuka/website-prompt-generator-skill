# Section Patterns — Build-Ready Templates

A library of detailed, implementation-ready section specs covering every major pattern found in modern websites.
Pick the closest pattern to what you see in the reference image, then customize.

---

## Table of Contents
1. [Navigation Bars](#1-navigation-bars)
2. [Hero Sections](#2-hero-sections)
3. [Feature / Capabilities Sections](#3-feature--capabilities-sections)
4. [About / Story Sections](#4-about--story-sections)
5. [Cards & Grid Layouts](#5-cards--grid-layouts)
6. [Testimonials & Social Proof](#6-testimonials--social-proof)
7. [Pricing Sections](#7-pricing-sections)
8. [CTA / Conversion Sections](#8-cta--conversion-sections)
9. [Marquee / Scroll Strips](#9-marquee--scroll-strips)
10. [Footers](#10-footers)
11. [Reusable Animation Wrappers](#11-reusable-animation-wrappers)

---

## 1. Navigation Bars

### Pattern A: Floating Pill Nav (Liquid Glass)
**Use when**: Dark hero with video bg, Apple-style, premium aesthetic.
```
fixed top-4 left-1/2 -translate-x-1/2 z-50
Inner: liquid-glass rounded-full px-2 py-2 flex items-center gap-2

Left (logo): 44x44 liquid-glass rounded-full + italic serif letter or SVG
Center (links): hidden md:flex gap-1, each: px-3 py-2 text-sm text-white/80
Right (CTA): bg-white text-black rounded-full px-5 py-2 text-sm

Load: fade down from y:-20, delay:0, duration:0.5
```

### Pattern B: Full-Width Sticky Header
**Use when**: Light/neutral site, SaaS product, corporate.
```
sticky top-0 z-50 w-full border-b border-[--border]
bg-[--bg]/80 backdrop-blur-md
Inner: max-w-7xl mx-auto px-6 py-4 flex items-center justify-between

Logo: left (text or SVG, font-semibold)
Links: center (hidden md:flex gap-8, text-sm)
Actions: right (ghost + primary button)

Scroll: border appears + bg opacity increases
Load: elements slide from y:-20, 0.04s stagger
```

### Pattern C: Minimal Transparent Nav
**Use when**: Hero has inset rounded video/image bg.
```
absolute top-0 left-0 right-0 z-10
px-6 py-5 flex justify-between items-center

Logo: wordmark only
Links: hidden md:flex gap-8 text-sm
CTA: single liquid-glass or plain button
On scroll: becomes sticky + backdrop-blur
```

---

## 2. Hero Sections

### Pattern A: Cinematic Full-Screen (Video BG)
```
relative w-full min-h-screen overflow-hidden bg-black

Background (z-0):
  <video autoPlay muted loop playsInline>
  absolute inset-0 w-full h-full object-cover
  Optional: translate-y-[15%] to show lower frame
  Optional overlay: bg-gradient-to-b from-black/30 via-transparent to-black/60

Content (z-10):
  flex flex-col justify-center items-center text-center
  px-6 pt-32 pb-24 min-h-screen
  Headline: text-5xl md:text-7xl lg:text-8xl font-[display] text-white
  Subtext: max-w-xl text-base md:text-lg text-white/70 mt-6
  CTA: liquid-glass rounded-full px-10 py-4 text-white mt-10

Animations:
  Headline: blurFade delay:0
  Subtext: fadeUp delay:0.4s
  CTA: fadeUp delay:0.6s
```

### Pattern B: Split Layout (Text Left, Visual Right)
```
min-h-screen flex items-center px-6 md:px-12 lg:px-20 py-24
Inner: max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-2 gap-12 lg:gap-20 items-center

Text column:
  Badge: rounded-full px-3 py-1 bg-[accent]/10 text-[accent] text-xs uppercase
  Headline: text-4xl md:text-5xl lg:text-6xl font-bold leading-tight mt-4
  Subtext: text-lg text-[fg-muted] max-w-md mt-6
  CTAs: primary + ghost link mt-8

Visual column:
  Mockup: rounded-2xl shadow-2xl border border-white/10
  Optional glow behind: blur-3xl bg-accent/20 absolute rounded-full w-[400px] h-[400px] -z-10

Animations:
  Text: staggered fadeUp (0, 0.1, 0.2, 0.35s)
  Visual: scale 0.94→1 + fadeUp, delay 0.3s, spring
```

### Pattern C: Full-Bleed Wordmark Hero (Typographic)
```
min-h-screen flex flex-col overflow-hidden bg-[bg]

Massive heading (w-full overflow-hidden):
  text-[16vw] md:text-[18vw] font-black uppercase leading-none tracking-tight
  Animation: clip-path "inset(100% 0 0 0)" → "inset(0% 0 0 0)"

Bottom bar (flex justify-between items-end pb-10 px-6):
  Left: text-sm text-[fg-muted] max-w-[200px] uppercase tracking-wide
  Right: CTA button
```

### Pattern D: Centered Editorial with Card Fan
```
min-h-screen flex flex-col items-center justify-center text-center px-6 py-24

Card fan cluster (relative w-full max-w-[360px] h-[280px] mx-auto):
  Card 1: rotate-[-8deg] translate-y-[8px] z-10
  Card 2: rotate-[0deg] z-20 (front / largest)
  Card 3: rotate-[8deg] translate-y-[8px] z-10
  Each: rounded-2xl shadow-[0_20px_60px_rgba(0,0,0,0.3)]

Frosted panel (if present):
  absolute bottom-0 left-1/2 -translate-x-1/2 w-[90%]
  backdrop-blur-xl bg-white/40 rounded-2xl p-4

Wordmark: text-[clamp(2rem,10vw,7rem)] font-black uppercase tracking-tighter mt-8

Animations:
  Cards: deal from y:30 with rotate targets, 0.08s stagger, spring
  Panel: fadeUp delay 0.4s
  Wordmark: clip-path reveal delay 0.6s
  Hover: fan spreads wider, center card lifts -6px
```

---

## 3. Feature / Capabilities Sections

### Pattern A: 3-Column Feature Cards
```
py-24 md:py-32 px-6 md:px-12 bg-[bg]
max-w-7xl mx-auto

Header (mb-16):
  Kicker: text-sm font-medium text-[accent] uppercase tracking-widest
  Heading: text-4xl md:text-6xl font-bold leading-tight max-w-2xl

Card grid: grid grid-cols-1 md:grid-cols-3 gap-6

Each card:
  liquid-glass or bg-[surface] rounded-2xl p-6 min-h-[320px] flex flex-col
  Top row: Icon (44x44 nested rounded-xl) + Tags (flex flex-wrap justify-end)
  Spacer: flex-1
  Bottom: Title text-2xl + Body text-sm text-[fg-muted] max-w-[32ch]

Animations:
  Header: fadeUp on scroll
  Cards: staggered scaleIn 0.08s, whileInView
  Hover: y -6px, shadow deepens
```

### Pattern B: Vertical Feature List (Services)
```
py-24 px-6 md:px-12 bg-white or bg-[bg-light]
max-w-5xl mx-auto

List items (divide-y divide-[border]):
  Each: flex items-start gap-6 py-10 md:py-14
  Number: text-[clamp(3rem,8vw,7rem)] font-black text-[fg]/10 w-24 shrink-0
  Text block: Name (text-xl uppercase tracking-wider) + Body (text-base text-[fg-muted])

Animations: each row fadeUp with i*0.1s delay
```

### Pattern C: Asymmetric Bento Grid
```
grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 auto-rows-[240px] gap-4

Special cards:
  Featured wide: col-span-2 row-span-2 — large image or video
  Stats card: col-span-1 row-span-1 — big number + label
  Text card: heading + short body
  Visual card: image fill with gradient overlay text

Animations: staggered scaleIn 0.06s, whileInView
```

---

## 4. About / Story Sections

### Pattern A: Centered Text with Animated Characters
```
min-h-screen flex items-center justify-center px-6 py-24 text-center

Heading: text-[clamp(2rem,8vw,6rem)] font-black leading-none tracking-tight

Animated body paragraph:
  Each character wrapped in <motion.span>
  useScroll with offset ['start 0.8', 'end 0.2']
  Each char: opacity = useTransform(scrollYProgress,
    [charProgress - 0.1, charProgress + 0.05], [0.2, 1])
  max-w-[560px] mx-auto text-base md:text-lg leading-relaxed

Optional corner decorations:
  absolute positioned 3D objects (top-left, top-right, bottom-left, bottom-right)
  Each fades from x:-80 or x:80, duration 0.9, staggered
```

### Pattern B: Split Narrative (Text + Image)
```
py-24 md:py-32 px-6 md:px-12
grid grid-cols-1 lg:grid-cols-2 gap-16 items-center max-w-7xl mx-auto

Text side:
  Eyebrow: text-sm text-[accent] uppercase tracking-wider mb-4
  Heading: text-4xl md:text-5xl font-bold leading-tight
  Body: text-base text-[fg-muted] leading-relaxed mt-6 max-w-lg
  CTA: mt-10

Image side:
  Primary: w-full rounded-2xl shadow-2xl aspect-[4/5] object-cover
  Optional: floating stat badge (absolute -top-4 -right-4)
  Optional: second smaller image overlapping (absolute bottom-8 -left-8)
```

---

## 5. Cards & Grid Layouts

### Stacking / Sticky Cards (Scroll-Driven)
```
Container: relative (height = num_cards * 85vh)
Each card: sticky h-[85vh] rounded-[40px] border-2 border-[border] bg-[surface]

Scale-on-scroll:
const { scrollYProgress } = useScroll({ target: container });
const targetScale = 1 - (totalCards - 1 - i) * 0.03;
const scale = useTransform(scrollYProgress, [i / totalCards, 1], [1, targetScale]);
style={{ top: `${24 + i * 28}px` }}

Card layout:
  Top: number (text-[8vw] font-black) + category + name + "Live" button
  Bottom: asymmetric 2-col image grid
    Col A (40%): 2 stacked images
    Col B (60%): 1 tall image
    All images: same large border-radius as card
```

### Responsive Card Grid
```
Mobile:     grid-cols-1
Tablet:     md:grid-cols-2
Desktop:    lg:grid-cols-3
Ultra-wide: xl:grid-cols-4

gap-4 md:gap-6, items-stretch
Card min-height: min-h-[280px]
```

---

## 6. Testimonials & Social Proof

### Horizontal Scroll Testimonials
```
Outer: overflow-hidden
Inner: flex gap-4
Card: min-w-[340px] md:min-w-[400px] bg-[surface] rounded-2xl p-6 flex-shrink-0
  Quote: text-base leading-relaxed text-[fg-muted] mb-6
  Author: flex items-center gap-3
    Avatar: w-10 h-10 rounded-full object-cover
    Name: font-semibold | Title: text-sm text-[fg-muted]
  Stars (optional): flex gap-1 text-yellow-400 text-sm
```

### Logo / Partner Strip
```
Flex of partner logos
Each: grayscale opacity-40 hover:opacity-80 hover:grayscale-0 transition-all
Sizes: h-6 md:h-8
Gap: gap-8 md:gap-16
Text names variant: italic serif, text-2xl md:text-3xl tracking-tight
```

---

## 7. Pricing Sections

### 3-Tier Pricing
```
max-w-5xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-4

Tiers:
  Basic:      bg-[surface] border-[border]
  Pro:        bg-[accent] text-white border-transparent -mt-4 pb-12
  Enterprise: bg-[surface] border-[border]

Each card:
  Label: text-xs uppercase tracking-widest mb-2
  Price: text-5xl font-black + per-period suffix
  Features: mt-6 space-y-3 (Check icon + text-sm)
  CTA: mt-8 w-full rounded-full py-3
```

---

## 8. CTA / Conversion Sections

### Full-Width Banner CTA
```
py-24 px-6 bg-[accent] or dark, text-center
Heading: text-4xl md:text-5xl font-bold max-w-2xl mx-auto
Subtext: text-base text-[fg-muted] max-w-xl mx-auto mt-4
Buttons: flex gap-4 justify-center mt-8 flex-wrap
Animations: fadeUp whileInView, 0.1s stagger
```

### Email Capture (Newsletter)
```
py-20 flex flex-col items-center text-center
Heading: text-3xl md:text-4xl font-bold
Input bar: rounded-full px-5 pr-2 py-2 bg-white flex items-center gap-3 max-w-md mt-8
  input: flex-1 bg-transparent text-[bg] placeholder:text-[bg]/40
  Submit: bg-[accent] text-white rounded-full px-5 py-2 text-sm
Legal: text-xs text-[fg-muted] mt-4
```

---

## 9. Marquee / Scroll Strips

### Infinite Scroll Marquee (CSS)
```css
.marquee-track {
  display: flex;
  width: max-content;
  animation: marquee 20s linear infinite;
}
.marquee-track:hover { animation-play-state: paused; }
@keyframes marquee {
  from { transform: translateX(0); }
  to   { transform: translateX(-50%); }
}
```
```
Outer: overflow-hidden py-4 border-y border-[border]
Two duplicate .marquee-track for seamless loop
Items: text + bullet separator or logo images, px-6 gap-6
Reverse: animation-direction: reverse on second track
```

### Scroll-Parallax Image Row (Two Opposite Rows)
```
useScroll to track scrollY
offset = (scrollY - sectionTop + windowHeight) * 0.3

Row 1: translateX(offset - 200)    → moves right
Row 2: translateX(-(offset - 200)) → moves left

Tile: w-[420px] h-[270px] rounded-2xl object-cover flex-shrink-0
Row: flex gap-3, willChange: 'transform'
```

---

## 10. Footers

### Rich Multi-Column Footer
```
bg-[bg-dark] or bg-[surface] pt-20 pb-10 px-6 md:px-12
max-w-7xl mx-auto

Top: grid grid-cols-1 md:grid-cols-[2fr_1fr_1fr_1fr] gap-12
  Col 1: Logo + tagline + social icons (w-8 h-8 rounded-full border each)
  Col 2–4: Link groups with section heading + links

Bottom: flex justify-between items-center pt-8 border-t mt-12
  Legal: text-xs text-[fg-subtle]
  Back to top: arrow-up button

Animations: fadeUp whileInView
```

### Minimal Footer
```
py-8 px-6 border-t border-[border]
flex flex-col md:flex-row justify-between items-center gap-4
  Left: logo or brand name
  Center: copyright text-xs text-[fg-muted]
  Right: social icons or nav links
```

---

## 11. Reusable Animation Wrappers

### FadeIn (universal wrapper)
```tsx
const FadeIn = ({ delay = 0, duration = 0.6, x = 0, y = 24, children }) => (
  <motion.div
    initial={{ opacity: 0, x, y }}
    whileInView={{ opacity: 1, x: 0, y: 0 }}
    viewport={{ once: true, margin: "-50px" }}
    transition={{ delay, duration, ease: [0.22, 1, 0.36, 1] }}
  >
    {children}
  </motion.div>
);
```

### WordsPullUp
```tsx
// Splits text by space, staggers each word fadeUp on inView
const WordsPullUp = ({ text, className }) => {
  const words = text.split(' ');
  const isInView = useInView(ref, { once: true });
  return (
    <div ref={ref} className={`flex flex-wrap gap-x-[0.3em] ${className}`}>
      {words.map((word, i) => (
        <motion.span key={i} style={{ display: 'inline-block' }}
          initial={{ opacity: 0, y: 20 }}
          animate={isInView ? { opacity: 1, y: 0 } : {}}
          transition={{ delay: i * 0.08, duration: 0.6, ease: [0.22, 1, 0.36, 1] }}
        >{word}</motion.span>
      ))}
    </div>
  );
};
```

### AnimatedText (character scroll-opacity)
```tsx
// Each character's opacity tied to scroll progress
const AnimatedText = ({ text }) => {
  const ref = useRef(null);
  const { scrollYProgress } = useScroll({ target: ref, offset: ['start 0.8', 'end 0.2'] });
  return (
    <p ref={ref}>
      {text.split('').map((char, i) => {
        const charProgress = i / text.length;
        const opacity = useTransform(scrollYProgress,
          [charProgress - 0.1, charProgress + 0.05], [0.2, 1]);
        return <motion.span key={i} style={{ opacity }}>{char}</motion.span>;
      })}
    </p>
  );
};
```

### Magnet (cursor-following)
```tsx
const Magnet = ({ children, padding = 100, strength = 3 }) => {
  const ref = useRef(null);
  const [pos, setPos] = useState({ x: 0, y: 0 });
  const [isActive, setIsActive] = useState(false);
  // onMouseMove: offset from center / strength
  // onMouseLeave: reset to { x:0, y:0 }
  return (
    <div ref={ref}
      style={{
        transform: `translate3d(${pos.x}px, ${pos.y}px, 0)`,
        transition: isActive ? 'transform 0.3s ease-out' : 'transform 0.6s ease-in-out',
        willChange: 'transform'
      }}
    >{children}</div>
};
```

### Anime.js Animation Wrappers (React)

### AnimeFadeIn
```tsx
import { useRef, useEffect } from 'react';
import { animate, createScope } from 'animejs';

export const AnimeFadeIn = ({ children, delay = 0, duration = 600, y = 24 }) => {
  const containerRef = useRef(null);
  const scopeRef = useRef(null);

  useEffect(() => {
    scopeRef.current = createScope({ root: containerRef.current }).add(() => {
      animate(containerRef.current, {
        opacity: [0, 1],
        translateY: [y, 0],
        duration: duration,
        delay: delay,
        ease: 'outExpo'
      });
    });
    return () => scopeRef.current?.revert();
  }, [delay, duration, y]);

  return (
    <div ref={containerRef} style={{ opacity: 0 }}>
      {children}
    </div>
  );
};
```

### AnimeWordsPullUp
```tsx
import { useRef, useEffect } from 'react';
import { animate, stagger, createScope } from 'animejs';

export const AnimeWordsPullUp = ({ text, className, delay = 0 }) => {
  const containerRef = useRef(null);
  const scopeRef = useRef(null);
  const words = text.split(' ');

  useEffect(() => {
    scopeRef.current = createScope({ root: containerRef.current }).add(() => {
      animate('.word-span', {
        opacity: [0, 1],
        translateY: [20, 0],
        duration: 600,
        delay: stagger(80, { start: delay }),
        ease: 'outExpo'
      });
    });
    return () => scopeRef.current?.revert();
  }, [text, delay]);

  return (
    <div ref={containerRef} className={`flex flex-wrap gap-x-[0.3em] ${className}`}>
      {words.map((word, i) => (
        <span key={i} className="word-span inline-block" style={{ opacity: 0 }}>
          {word}
        </span>
      ))}
    </div>
  );
};
```

### AnimeScrollReveal (character scroll-opacity)
```tsx
import { useRef, useEffect } from 'react';
import { animate, onScroll, createScope } from 'animejs';

export const AnimeScrollReveal = ({ text, className }) => {
  const containerRef = useRef(null);
  const scopeRef = useRef(null);
  const chars = text.split('');

  useEffect(() => {
    scopeRef.current = createScope({ root: containerRef.current }).add(() => {
      animate('.char-span', {
        opacity: [0.2, 1],
        autoplay: onScroll({
          target: containerRef.current,
          sync: true,
          enter: 'top 80%',
          leave: 'bottom 20%'
        })
      });
    });
    return () => scopeRef.current?.revert();
  }, [text]);

  return (
    <p ref={containerRef} className={className}>
      {chars.map((char, i) => (
        <span key={i} className="char-span inline-block">
          {char === ' ' ? '\u00A0' : char}
        </span>
      ))}
    </p>
  );
};
```

### AnimeMagnet (cursor-following)
```tsx
import { useRef, useEffect } from 'react';
import { animate } from 'animejs';

export const AnimeMagnet = ({ children, padding = 100, strength = 3 }) => {
  const ref = useRef(null);

  useEffect(() => {
    const el = ref.current;
    if (!el) return;

    const handleMouseMove = (e) => {
      const rect = el.getBoundingClientRect();
      const elX = rect.left + rect.width / 2;
      const elY = rect.top + rect.height / 2;
      const dist = Math.hypot(e.clientX - elX, e.clientY - elY);

      if (dist < padding) {
        const x = (e.clientX - elX) / strength;
        const y = (e.clientY - elY) / strength;
        animate(el, {
          translateX: x,
          translateY: y,
          duration: 300,
          ease: 'outQuad',
          composition: 'replace'
        });
      } else {
        handleMouseLeave();
      }
    };

    const handleMouseLeave = () => {
      animate(el, {
        translateX: 0,
        translateY: 0,
        duration: 600,
        ease: 'outElastic(1, 0.6)',
        composition: 'replace'
      });
    };

    window.addEventListener('mousemove', handleMouseMove);
    el.addEventListener('mouseleave', handleMouseLeave);

    return () => {
      window.removeEventListener('mousemove', handleMouseMove);
      el.removeEventListener('mouseleave', handleMouseLeave);
    };
  }, [padding, strength]);

  return (
    <div ref={ref} className="inline-block will-change-transform">
      {children}
    </div>
  );
};
```

