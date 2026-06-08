---
name: nanfu-skill
description: Frontend development skill for the NANFU Global corporate brand (nanfu.global) — battery manufacturer design system. Use when building corporate sites needing dark hero sections, GSAP scroll-triggered text animations, battery-canvas particle systems, glassmorphism cards, animated SVG rings, international language selector, and interactive product popups with purchase country selector.
---

# Nanfu Global Design System

## Design Philosophy

**Dark and light breathe together.** Every dark section MUST be followed by a light section (or vice versa). This alternating rhythm is the first law of this design system — violating it produces flat, suffocating, depthless pages. Think of it as visual inhale/exhale.

Emotional register: confident innovation. Industrial precision. Premium restraint.
Aesthetic: deep darks + saturated red (#e60008) + generous whitespace. Never busy.

## Tech Stack

| Concern | Choice |
|---------|--------|
| Framework | Vanilla JS (no React/Vue required) |
| Animation | GSAP 3.12+ + ScrollTrigger + Lenis smooth-scroll |
| CSS | rem-based Flexbox + Grid; `html{font-size:5.20833vw}` |
| Icons | Emoji for prototypes; custom iconfont (woff2) for production |
| Lazy loading | IntersectionObserver |
| Legacy | jQuery 3.6.3 (only if existing project requires it) |

## Colors

```
--primary:           #e60008    // accent red — buttons, links, highlights
--primary-hover:     #d9000b    // pressed state
--secondary:         #1c509c    // selection, secondary accents
--bg-dark:           #000000    // hero, footer, quote dividers
--bg-section:        #f7f7f7    // light alternating sections
--bg-section-dark:   #0a0a0a    // dark alternating sections
--bg-card:           #ffffff    // cards on light backgrounds
--bg-card-dark:      #111111    // cards on dark backgrounds
--text-primary:      #ffffff    // text on dark backgrounds
--text-dark:         #1a1a1a    // text on light backgrounds
--text-muted:        rgba(255,255,255,0.50)  // muted on dark
--text-muted-dark:   rgba(0,0,0,0.45)        // muted on light
--shadow-card:       rgba(92,84,78,0.30)     // universal card shadow
--accent-glow:       rgba(230,0,8,0.30)      // skill-item glow
--glass-bg:          rgba(255,255,255,0.04)  // glass on dark
--glass-bg-light:    rgba(0,0,0,0.03)        // glass on light
--glass-border:      rgba(255,255,255,0.08)  // border on dark
--glass-border-light:rgba(0,0,0,0.08)        // border on light
```

### Section Alternation Rule (MANDATORY)

```
Position  Section    Background            Text color
────────  ─────────  ────────────────────  ──────────
1         Hero       --bg-dark (#000)      white
2         About      --bg-section (#f7f7f7) dark
3         Quote      --bg-dark (#000)      white
4         Blog       --bg-section-dark     white
5         Timeline   --bg-section (#f7f7f7) dark
6         Skills     --bg-section-dark     white
7         Projects   --bg-section (#f7f7f7) dark
8         Quote      --bg-dark (#000)      white
9         Contact    --bg-section (#f7f7f7) dark
10        Footer     --bg-dark (#000)      white
```

**No two adjacent sections may share the same background color.** Use the `.section.light` class on light-background sections to auto-switch text colors.

Implementation pattern:
```html
<!-- Dark section (default) -->
<section class="section" id="skills" style="background:var(--bg-section-dark)">

<!-- Light section — add .light class -->
<section class="section light" id="about" style="background:var(--bg-section)">
```

```css
/* Default: dark-section text (white) */
.section-title h2 { color: #fff; }
.section-title p  { color: var(--text-muted); }

/* .light overrides: switch to dark text */
.section.light .section-title h2 { color: var(--text-dark); }
.section.light .section-title p  { color: var(--text-muted-dark); }
```

## Typography (rem-based; 5.20833vw base → 1rem ≈ 100px @1920px)

**This table is a floor, not a suggestion. Never shrink these values.**

| Role       | Tag / Class | rem   | ≈px  | Where |
|------------|-------------|-------|------|-------|
| Hero title | h1          | 0.96  | 96   | Hero only |
| Section h2 | h2          | 0.72  | 72   | Every section-title |
| Sub-head   | h3          | 0.40  | 40   | About intro, card titles |
| Body lead  | .f-24       | 0.24  | 24   | Quote blockquote |
| Body       | .f-20       | 0.20  | 20   | Hero description, section-title p |
| Body sm    | .f-16       | 0.16  | 16   | About text, blog card h3 |
| Caption    | .f-14       | 0.14  | 14   | Nav links, meta, contact text |
| Caption sm | .f-12       | 0.12  | 12   | Tags, labels, footer |

Utility classes: `.f-12 .f-14 .f-16 .f-18 .f-20 .f-22 .f-24 .f-28 .f-36 .f-40 .f-48 .f-72 .f-96`
Font stack: `Microsoft YaHei, PingFang SC, Source Han Sans CN, sans-serif`
Weights available: 100 / 400 / 600 / 700

## Spacing System

| Token | Value | ≈px |
|-------|-------|-----|
| Section vertical padding | 1.2rem | 120 |
| Section-title bottom margin | 0.8rem | 80 |
| Card grid gap | 0.24rem | 24 |
| Content block gap | 0.48rem | 48 |
| Container max-width | 12rem | 1200 |
| Container horizontal padding | 0.32rem | 32 |

## Motion

| Easing | Bezier | Use |
|--------|--------|-----|
| power1.out | (0.25, 0.46, 0.45, 0.94) | Micro-interactions, hover |
| power2.out | (0.22, 1, 0.36, 1) | Section entrances, cards |
| power2.inOut | (0.65, 0, 0.35, 1) | Text reveals |
| power4.inOut | (0.76, 0, 0.24, 1) | Dramatic slides |
| back.out(1.2) | — | Skill item entrances |

Durations: 0.3s / 0.5s / 0.7s / 1s / 1.2s — pick by element weight. Heavier elements get longer durations.

## Layout Architecture

Single-column scroll, full-bleed sections. Breakpoints: 768px (tablet), 1024px+ (desktop).

```
<div id="app">
  <header>           <!-- fixed, .scrolled on scroll -->
  <section.hero>     <!-- 100vh, canvas particles -->
  <section.section>  <!-- × N, alternating bg -->
  <section.quote>    <!-- dividers between content blocks -->
  <footer>           <!-- .top(3-col) + .mid + .btm -->
  <div.fixBox>       <!-- floating back-to-top -->
</div>
```

Utility classes: `.fxc` (center), `.fxs` (align), `.fxb` (space-between), `.r1 .r2 .r3` (full-width)
Grid patterns: 3-col blog, 4-col skills, 2-col about/projects/contact

## Components

### 1. Section Structure (CRITICAL — most bugs come from broken structure)

Every `.section` MUST follow this exact nesting:
```html
<section class="section [light]" id="<name>" style="background:var(--bg-section[-dark])">
  <div class="container">
    <div class="section-title" data-text>
      <span class="sub">Label</span>   <!-- ALWAYS red, ALWAYS uppercase -->
      <h2>Section Title</h2>
      <p>Short description</p>
    </div>
    <!-- content grid here -->
  </div>
</section>
```

**Before closing any section, verify:** `section-title` is closed → content grid is closed → `container` is closed → `section` is closed. Four levels. Count them.

### 2. Hero
- `height: 100vh`, canvas particle background (150 particles)
- Dark radial-gradient overlay for depth
- Red glow circle behind content
- `[data-split]` on greeting, `[data-text]` on h1
- Two `.layer-btn` in `.hero-cta` flex row (one `.fill`, one outline)
- Bouncing scroll indicator at bottom

### 3. Section Title
```html
<div class="section-title" data-text>
  <span class="sub">About</span>
  <h2>关于我</h2>
  <p>描述文字</p>
</div>
```
The `.sub` red label is non-negotiable — it's the visual anchor every section needs.

### 4. Layer Button
```html
<!-- Filled variant (red bg) -->
<button class="layer-btn fill">
  <span class="mask"></span>
  <span class="txt">探索文章</span>
</button>

<!-- Outline variant (transparent, fills on hover) -->
<button class="layer-btn">
  <span class="mask"></span>
  <span class="txt">联系我</span>
</button>
```
```css
.layer-btn {
  border: 1px solid rgba(255,255,255,0.25);  /* visible outline */
  /* NEVER use mix-blend-mode — it produces cyan text on red bg */
}
.layer-btn .mask {
  background: var(--primary);  /* slides in from left on hover */
  transform: scaleX(0); transform-origin: left;
}
.layer-btn:not(.fill):hover .mask { transform: scaleX(1); }
.layer-btn:not(.fill):hover { border-color: var(--primary); }
.layer-btn .txt { color: #fff; z-index: 1; }  /* plain white, no blend mode */
```

**Anti-pattern:** `mix-blend-mode: difference` on button text. The red mask (#e60008) inverts to cyan — it looks broken and unreadable. Use plain `color: #fff` instead.

### 5. About Section
- 2-col grid: `.about-image` (avatar photo) + `.about-text`
- Avatar: circular `<img>` with `object-fit: cover`, red-tinted border, box-shadow glow, rotating `.ring` decoration
- Stats row: 3 `.about-stat` cards with `[data-count]` counter animation
- **Always `.section.light`** — the avatar and stats need the white card contrast

### 6. Blog Cards
```html
<article class="blog-card" data-text>
  <div class="blog-card-img">
    <div class="img-placeholder" style="background:linear-gradient(135deg,#1a1a2e,#16213e);">
      🎨  <!-- large emoji, centered -->
    </div>
    <span class="tag">设计</span>
  </div>
  <div class="blog-card-body">
    <div class="meta"><span>date</span><span>· read time</span></div>
    <h3>Title</h3>
    <p>Excerpt</p>
    <span class="read-more">阅读全文 <span class="arrow">→</span></span>
  </div>
</article>
```
- Card background: `--bg-card-dark` (#111) on dark sections
- Image area: `aspect-ratio: 16/10`, simple gradient + emoji placeholder (NO complex inline SVGs — they look ugly when AI-generated)
- Tag: absolute-positioned red pill, top-left
- Hover: card lifts `-0.08rem`, border turns red, image scales 1.08×

### 7. Timeline
```html
<div class="timeline">
  <div class="timeline-item" data-text>
    <div class="dot"></div>
    <div class="date">2024 — 至今</div>
    <h3>Title</h3>
    <p>Description</p>
  </div>
  <!-- 3–5 items recommended -->
</div>
```
- Vertical line: 2px gradient (`--primary` → transparent) on the left
- Dot: 16px circle, `border: 3px solid var(--bg-section)` — **the border must match the section background**, not hardcoded `#000`
- Minimum 3 items; 4–5 is ideal for a complete career narrative
- **Always `.section.light`** — dots need the light background to blend their border

### 8. Skills Grid
```html
<div class="skills-grid">
  <div class="skill-item" data-text>
    <span class="icon">⚛️</span>
    <div class="name">React</div>
    <div class="level">精通</div>
  </div>
</div>
```
- 4-col grid (2-col on tablet, 1-col on mobile)
- Glass background, red glow + border on hover
- Entrance: `back.out(1.2)` easing, staggered 0.06s

### 9. Project Cards
```html
<div class="proj-card" data-text>
  <div class="bg-svg" style="background:linear-gradient(135deg,#302b63,#0f0c29);">🌌</div>
  <div class="overlay">
    <h3>Title</h3>
    <p>Description</p>
    <div class="tech"><span>Tech1</span><span>Tech2</span></div>
  </div>
</div>
```
- `aspect-ratio: 16/10`, dark card background
- **Overlay ALWAYS visible** (not opacity:0→1 on hover — this breaks when two ScrollTriggers fight over the same element). Use a semi-transparent gradient as default, deepen on hover
- Simple gradient + emoji placeholder (NO inline SVGs)
- Tech tags: subtle border pills

### 10. Quote Divider
```html
<section class="quote-section" style="background:var(--bg-dark)" data-text>
  <div class="mark">"</div>
  <blockquote>Quote text</blockquote>
  <cite>— Attribution</cite>
</section>
```
- Always `--bg-dark` background — quotes are visual palate cleansers
- Large faded red quote mark as background decoration

### 11. Contact
```html
<section class="section light" id="contact" style="background:var(--bg-section)">
  ...
  <div class="contact-grid">
    <div class="contact-info">
      <div class="contact-item"><span class="icon">✉️</span><span class="text">email</span></div>
    </div>
    <form class="contact-form" data-text onsubmit="...">
      <input placeholder="...">
      <textarea placeholder="..."></textarea>
      <button class="layer-btn fill" type="submit">...</button>
    </form>
  </div>
</section>
```
- 2-col grid, `.section.light`
- Contact items: white card bg (`--bg-card`), light border
- Form inputs: white bg, dark text, `--primary` border on focus
- **Placeholder color must be `--text-muted-dark`** — invisible otherwise

### 12. Floating Button
```html
<div class="fixBox" id="fixBox">
  <button class="layer-btn fill" onclick="window.scrollTo({top:0,behavior:'smooth'})">
    <span class="mask"></span>
    <span class="txt">↑</span>
  </button>
</div>
```
- `position: fixed`, bottom-right, initially hidden (opacity:0)
- Visibility toggled by ScrollTrigger on hero leave/enter
- Circular (`.layer-cir`), filled red

## Animation System

### Architecture Rule: ONE ScrollTrigger per element

**This is the #1 source of invisible-content bugs.** Every `[data-text]` element must be animated by exactly ONE ScrollTrigger. When the generic `[data-text]` sweep at the bottom of the script animates an element that also has a specific animation (blog-card, proj-card, skill-item, etc.), two `gsap.from({opacity:0})` calls fight over the same element and it stays invisible.

**The generic `[data-text]` handler MUST exclude every element handled by a specific animator:**

```js
document.querySelectorAll('[data-text]').forEach(el => {
  if(
    el.closest('.section-title') ||
    el.closest('.hero-content') ||
    el.hasAttribute('data-split') ||
    el.closest('.blog-card') ||
    el.closest('.skill-item') ||
    el.closest('.proj-card') ||
    el.closest('.timeline-item') ||
    el.closest('.contact-item') ||
    el.closest('.contact-form')
  ) return;  // ← skip elements with dedicated animations
  gsap.from(el, { y: 0.3, opacity: 0, duration: 0.7, ease: 'power2.out',
    scrollTrigger: { trigger: el, start: 'top 80%', once: true } });
});
```

### Text Split (`[data-split]`)
- Split text into per-character `<span>` elements
- Initial state: `opacity: 0; translateY(0.1rem); rotateX(15deg)`
- ScrollTrigger `onEnter` → stagger 0.02s, power2.out 0.6s
- Use for hero greeting and hero description only

### Section Entrances
| Element | From | Duration | Stagger | Easing |
|---------|------|----------|---------|--------|
| section-title | y:0.4, opacity:0 | 1s | — | power2.out |
| blog-card | y:0.4, opacity:0 | 0.6s | 0.1s | power2.out |
| skill-item | y:0.3, opacity:0, scale:0.9 | 0.5s | 0.06s | back.out(1.2) |
| timeline-item | x:-0.3, opacity:0 | 0.7s | 0.15s | power2.out |
| proj-card | y:0.4, opacity:0, scale:0.95 | 0.7s | 0.12s | power2.out |
| about-image, about-text | y:0.4, opacity:0 | 0.8s | — | power2.out |

### Hero Parallax
- `.hero-content` scrubs: translateY + scale + opacity as hero scrolls out
- Particle canvas responds to mouse position

### Counter Animation
- `gsap.fromTo(el, {textContent:0}, {textContent:target, duration:2, snap:{textContent:1}})`
- Triggered by ScrollTrigger entering `.about-stat`

## Anti-Patterns (BLOCKING — reject code review if present)

1. ❌ **Two adjacent sections with the same background** — must alternate light/dark
2. ❌ **White text on light background** — invisible; switch to `--text-dark` / `--text-muted-dark`
3. ❌ **Shrinking type scale** — 0.96/0.72/0.40 rem are minimums, never go smaller
4. ❌ **Missing `.sub` red label** on any section-title — every section needs its visual anchor
5. ❌ **Cards without hover feedback** — every interactive surface must respond
6. ❌ **Light-section cards on dark backgrounds** — use `--bg-card` (white) on light, `--bg-card-dark` (#111) on dark
7. ❌ **Broken section structure** — every `.section` needs `.container > .section-title + content`
8. ❌ **`mix-blend-mode: difference` on buttons** — produces cyan-on-red, unreadable
9. ❌ **Two ScrollTriggers animating the same element** — invisible content; use the exclusion list
10. ❌ **Inline SVG illustrations** in cards — inconsistent, ugly when AI-generated; use gradient + emoji placeholders
11. ❌ **`opacity:0 → 1` overlay on hover** for project cards — breaks with scroll animations; use always-visible overlay
12. ❌ **Hardcoded dot border color** in timeline — must match `var(--bg-section)`

## Quality Gate (run BEFORE declaring "done")

- [ ] Sections alternate background: dark → light → dark → light → ... (check with grep)
- [ ] Every light section has `class="section light"` and light-section CSS overrides
- [ ] Type scale: h1=0.96, h2=0.72, body=0.20 (grep `font-size` to verify)
- [ ] Every `.section-title` contains `<span class="sub">` with a red label
- [ ] Every card has a hover state (border-color, transform, or box-shadow change)
- [ ] Light-section cards use `--bg-card` (white); dark-section cards use `--bg-card-dark` (#111)
- [ ] All GSAP ScrollTriggers use `once: true`
- [ ] The `[data-text]` sweep excludes blog-card, skill-item, proj-card, timeline-item, contact-item, contact-form
- [ ] No `mix-blend-mode` anywhere in button styles
- [ ] No inline SVG in card images (emoji placeholders only)
- [ ] Timeline dot border uses `var(--bg-section)`, not hardcoded color
- [ ] Mobile: all grids collapse to 1–2 columns
- [ ] HTML passes tag-balance check (`<section>` opens = closes, `<div>` opens = closes)

## Code Rules

1. Wrap everything in `<div id="app">`; CSS in `<head>`, scripts before `</body>`
2. All production images: `img[data-src][class=lazy]` with IntersectionObserver
3. `[data-text]` = whole-element fade-up; `[data-split]` = per-character stagger
4. Footer structure: `.footer-grid`(3-col) + `.footer-bottom`(copyright + social), `bg:#000`
5. Mobile: single-column grids, `.appNav` visible, `header nav` hidden
6. Every ScrollTrigger: `once: true` — no re-triggering on scroll-back
7. Color discipline: dark bg → white text, light bg → dark text. No exceptions.
8. Easing discipline: power1.out for micro, power2.out for entrance, power2.inOut for text
9. No two adjacent sections share a background color. Period.
10. ONE animation per element. The generic `[data-text]` handler excludes all specifically-animated selectors.
