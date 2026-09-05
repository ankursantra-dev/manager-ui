# HYPER-DETAILED BUILD PROMPT — "Minifolio" Dark/Lime Template Style

Copy-paste this entire prompt into an AI code generator (Claude, v0, Cursor, etc.) or use it as a dev spec. Every value is explicit — no guessing required.

---

## 1. DESIGN TOKENS (exact values)

### Colors
```css
--color-bg-page:        #0E0E0E;   /* outer page background */
--color-bg-card:        #161616;   /* card / section background */
--color-bg-card-alt:    #1E1E1E;   /* nested chip / stat block bg */
--color-border:         #2A2A2A;   /* 1px hairline borders on cards */
--color-accent:         #D4FA3D;   /* neon lime — primary accent */
--color-accent-hover:   #E4FF6B;   /* lighter lime on hover */
--color-accent-active:  #B8DE1F;   /* darker lime on click/press */
--color-text-primary:   #FFFFFF;   /* headings */
--color-text-secondary: #A6A6A6;   /* body copy */
--color-text-muted:     #6E6E6E;   /* captions, timestamps */
--color-text-on-accent: #0A0A0A;   /* text sitting on lime bg */
--color-success:        #4ADE80;
--color-star:           #D4FA3D;   /* rating stars */
--shadow-card:          0 20px 40px -12px rgba(0,0,0,0.55);
--shadow-card-hover:    0 28px 55px -10px rgba(0,0,0,0.65);
--radius-card:          16px;
--radius-chip:          10px;
--radius-pill:          999px;
```

### Typography
- **Font family:** `"Inter", "Satoshi", -apple-system, sans-serif` (load Inter from Google Fonts, weights 400/500/600/700/800)
- **H1 (hero headline):** 44px desktop / 30px tablet / 24px mobile, weight 800, line-height 1.1, letter-spacing -0.02em
- **H2 (section headline):** 32px / 26px / 22px, weight 700, line-height 1.15, letter-spacing -0.01em
- **H3 (card title):** 18px, weight 600
- **Body:** 15px / 14px mobile, weight 400, line-height 1.65, color var(--color-text-secondary)
- **Eyebrow label (pill above headings):** 12px, weight 600, uppercase OFF (sentence case), letter-spacing 0.01em
- **Stat number:** 28px, weight 800, color white
- **Stat caption:** 12px, weight 400, color muted
- **Button label:** 14px, weight 600
- **Highlighted word rule:** exactly ONE word per headline rendered in `var(--color-accent)`, rest in white — never bold-different, only color changes.

### Spacing scale (use only these values — 4px base grid)
```
4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 120
```
- Card internal padding: 24px mobile → 32px desktop
- Section vertical padding: 64px mobile → 120px desktop
- Gap between grid items: 16px mobile → 24px desktop
- Max content width: 1280px, centered, 24px side gutters on mobile / 80px on desktop

---

## 2. LAYOUT STRUCTURE (exact sections, top to bottom)

1. **Top band** — full-width solid lime (`--color-accent`) bar, 96px tall desktop / 64px mobile. Contains: logo (left, black wordmark + geometric icon mark), nav pill links (center, dark rounded pill container), CTA button "Let's Talk" (right, black bg + lime text pill button).
2. **Hero section** — dark background. Two-column desktop (60/40 split): left = eyebrow badge + H1 with one lime word + paragraph + two buttons (primary lime pill + secondary ghost outline pill) + 3-stat row. Right = portrait/mockup image with lime blurred circle shape behind it (decorative, blur 80px, opacity 0.4).
3. **Logo strip** — horizontal row of 5-6 grayscale client logos, opacity 0.5, hover → opacity 1 + grayscale(0) transition.
4. **Feature/service cards row** — 3-column grid, dark cards, circular icon badge top-left (lime stroke, dark fill), title, 1-line description, "Learn more →" text link with lime arrow.
5. **Stats/proof strip** — dark card, 3-4 column grid, giant number + label, separated by 1px vertical hairline dividers (hidden on mobile, stack instead).
6. **Process/timeline section** — numbered rows (01, 02, 03) each with title + description, left-aligned number in lime, connected by a thin vertical line on desktop.
7. **Portfolio/work grid** — 2-3 column masonry-style cards, image thumbnail top, category tag pill overlay (top-left, lime bg, black text), title + short desc below, whole card lifts on hover.
8. **Testimonial carousel** — dark card, avatar circle, 5 lime stars, quote text, name + role, dot-pagination below.
9. **CTA banner** — full-width lime section (mirrors top band), bold black H2, black pill button with lime text (inverse of primary button).
10. **Footer** — dark, 4-column link layout, logo + tagline left, social icon circles (dark bg, lime icon, lime bg on hover), bottom copyright bar with 1px top border.

---

## 3. COMPONENT-LEVEL INTERACTION SPEC (no ambiguity)

### Buttons
**Primary pill button (lime):**
- Default: bg `--color-accent`, text `--color-text-on-accent`, padding 14px 28px, radius `--radius-pill`, font-weight 600
- Hover: bg → `--color-accent-hover`, transform `translateY(-2px)`, shadow `0 8px 20px rgba(212,250,61,0.35)`, transition `all 200ms cubic-bezier(0.4,0,0.2,1)`
- Active/click: bg → `--color-accent-active`, transform `translateY(0) scale(0.97)`, transition `100ms ease-out`
- Focus-visible: 2px solid white outline, 2px offset

**Secondary ghost pill button:**
- Default: transparent bg, 1.5px solid `--color-border`, text white
- Hover: border → `--color-accent`, text → `--color-accent`, background `rgba(212,250,61,0.06)`
- Active: scale(0.97)

**Icon-only circular buttons (nav arrows, social):**
- 40px diameter, dark bg, 1px border
- Hover: border → lime, icon color → lime, rotate 8deg (for arrow icons only), 250ms ease
- Click: scale(0.9) then spring back via `cubic-bezier(0.34,1.56,0.64,1)` 300ms

### Cards (service/portfolio/testimonial)
- Default: `--shadow-card`, border 1px `--color-border`, `transform: translateY(0) scale(1)`
- Hover: `transform: translateY(-6px) scale(1.01)`, shadow → `--shadow-card-hover`, border-color → `--color-accent` at 40% opacity, transition `all 350ms cubic-bezier(0.16,1,0.3,1)`
- Portfolio card image: `transform: scale(1)` default → `scale(1.08)` on card hover, transition `600ms cubic-bezier(0.16,1,0.3,1)`, overflow hidden on parent
- Category tag pill on portfolio card: fades/slides in from `translateY(8px) opacity:0` → `translateY(0) opacity:1` on card hover, 250ms delay 50ms

### Headline word highlight
- The lime-colored keyword in each H1/H2 has a subtle continuous animation: `text-shadow` pulse — animate `0 0 0px rgba(212,250,61,0)` → `0 0 16px rgba(212,250,61,0.5)` → back, 3s ease-in-out infinite, ONLY on the hero H1 (not repeated elsewhere, avoid visual noise)

### Stat numbers (count-up on scroll)
- On scroll-into-view (Intersection Observer, threshold 0.4): animate number from 0 → final value over 1200ms using `easeOutExpo`, using `requestAnimationFrame` or a library like `react-countup`
- Trigger once only (don't re-animate on scroll back up)

### Nav pill (top band)
- Active link: black pill background behind text, text stays black (already on lime band) — indicator is a small dark rounded-full chip sliding via `transform: translateX()` with `300ms cubic-bezier(0.65,0,0.35,1)` when switching links
- Inactive links: no background, opacity 0.75 → hover opacity 1

### Logo strip
- Each logo: `filter: grayscale(100%) opacity(0.5)` default
- Hover: `filter: grayscale(0%) opacity(1)`, `250ms ease`
- Optional: infinite horizontal auto-scroll marquee at 30s loop duration, `animation: scrollX linear infinite`, pause on hover (`animation-play-state: paused`)

### Testimonial carousel
- Autoplay: advance every 6000ms, pause on hover/focus
- Slide transition: horizontal slide `transform: translateX()`, `500ms cubic-bezier(0.65,0,0.35,1)`, plus fade opacity 0→1 on incoming slide
- Dot pagination: inactive dot 6px circle `--color-border`, active dot elongates to 24px pill `--color-accent`, transition `width 300ms ease`
- Swipeable on touch devices (drag threshold 50px)

### Section scroll-reveal (global)
- All sections: children fade+slide in `opacity:0, translateY(24px)` → `opacity:1, translateY(0)`, `600ms cubic-bezier(0.16,1,0.3,1)`, staggered 80ms between siblings, triggered once via Intersection Observer at 15% visibility
- Respect `prefers-reduced-motion: reduce` — disable all transform/opacity entrance animations, keep only color/instant state changes

### Cursor feedback
- All clickable elements: `cursor: pointer`
- Buttons/cards: on `:active` state everywhere use `scale(0.97)` micro-press feedback, 100ms out / 150ms back

### Page load
- Hero content: staggered fade-up entrance on initial mount only — eyebrow (0ms) → H1 (100ms) → paragraph (200ms) → buttons (300ms) → stats (400ms), each `400ms ease-out`, `translateY(16px)→0`
- Top lime band + hero image: fade in `600ms` simultaneously

---

## 4. RESPONSIVENESS (exact breakpoints, mobile-first)

```css
/* Base = mobile, 0–639px */
--container-padding: 20px;
--section-padding-y: 56px;
--grid-cols: 1; /* all grids stack to 1 column */
--h1-size: 26px;
--h2-size: 22px;

/* sm: 640px+ (large phone) */
@media (min-width: 640px) {
  --container-padding: 24px;
  --grid-cols: 2; /* portfolio/services become 2-col */
}

/* md: 768px+ (tablet) */
@media (min-width: 768px) {
  --section-padding-y: 80px;
  --h1-size: 32px;
  --h2-size: 26px;
  /* nav switches from hamburger to inline pill nav */
}

/* lg: 1024px+ (small desktop) */
@media (min-width: 1024px) {
  --grid-cols: 3;
  --h1-size: 40px;
  --h2-size: 30px;
  /* hero becomes 2-column (60/40) instead of stacked */
  --container-padding: 48px;
}

/* xl: 1280px+ (desktop) */
@media (min-width: 1280px) {
  --container-padding: 80px;
  --h1-size: 44px;
  --h2-size: 32px;
  --max-width: 1280px;
}

/* 2xl: 1536px+ (large desktop) */
@media (min-width: 1536px) {
  --max-width: 1400px;
}
```

**Specific responsive behaviors:**
- **Nav:** below 768px → collapses to hamburger icon (right side of top band) opening a full-screen dark overlay menu, links stacked, staggered fade-in 60ms each, close via X icon top-right or swipe-down
- **Hero image:** below 1024px, moves below text content (order-2), width 80% centered, lime blur circle scales down proportionally
- **Stat grid:** 3-4 columns desktop → 2 columns tablet → 2 columns mobile (never 1, keep numbers punchy in pairs)
- **Portfolio grid:** 3 columns desktop → 2 columns tablet → 1 column mobile, image aspect-ratio locked 4:3 at all sizes
- **Testimonial carousel:** shows 1 card at all breakpoints, but padding/font shrink at mobile
- **Buttons:** full-width (`width:100%`) below 480px when stacked in a group of 2; side-by-side with `flex-wrap` above that
- **Font scaling:** use `clamp()` for fluid type where possible, e.g. `font-size: clamp(26px, 4vw + 10px, 44px);` for H1
- **Touch targets:** minimum 44x44px tappable area on all interactive elements below 768px
- **Overlapping mockup collage (if replicating the showcase-style hero):** on mobile, collapse stacked/rotated cards into a single non-overlapping card, no rotation, since overlap breaks on narrow viewports

---

## 5. ACCESSIBILITY & STATES (explicit, not optional)

- Color contrast: white text on `#161616` = 15.8:1 (AAA). Lime-on-black button text = 15.1:1 (AAA). Never place lime text on white or light backgrounds.
- All interactive elements need visible `:focus-visible` states (2px white or lime outline, 2px offset, never `outline:none` without replacement)
- All images: descriptive `alt` text
- Carousel: `aria-live="polite"` on active slide, pause button for autoplay
- Reduced motion: wrap all animation CSS in `@media (prefers-reduced-motion: no-preference)`
- All icon-only buttons: `aria-label` required

---

## 6. TECH IMPLEMENTATION NOTES

- Use CSS custom properties (tokens above) — no hardcoded hex values in components
- Use `IntersectionObserver` for scroll-reveal and count-up triggers (not scroll event listeners, for performance)
- Prefer CSS transitions/animations over JS animation libraries where possible; use Framer Motion only for the carousel slide and staggered entrance if in React
- Image formats: WebP/AVIF with fallback, `loading="lazy"` on all below-the-fold images
- All rounded corners consistently: cards 16px, chips 10px, buttons/pills 999px — never mix

---

**End of spec. Every color, size, spacing value, animation timing/easing curve, breakpoint, and interaction state above is explicit — implement exactly as written, do not invent or approximate any value not listed.**
