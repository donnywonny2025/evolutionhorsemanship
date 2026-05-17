# Animation Spec — Evolution Horsemanship Landing Page

## Design Principles
- **Equestrian-elegant**: gold tones only, nothing flashy or techy
- **Soft & precise**: ease-in-out curves, never snapping or jarring
- **Low deltas**: opacity changes in the 15-25% range — "just kind of there"
- **Respect `prefers-reduced-motion`**: already wired in `style.css`

---

## 1. Nav Bar Light Sweep (Priority)

**What**: A soft gold shimmer passes horizontally across each nav link text, one at a time, cascading left to right.

**Technique**: CSS `background-clip: text` with a moving linear-gradient.

```css
/* Apply to each .main-nav a link */
.main-nav a {
  background: linear-gradient(
    90deg,
    currentColor 0%,
    currentColor 40%,
    var(--gold-light) 50%,
    currentColor 60%,
    currentColor 100%
  );
  background-size: 300% 100%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: navShimmer 20s ease-in-out infinite;
}

@keyframes navShimmer {
  0%    { background-position: 200% center; }  /* shimmer offscreen right */
  6%    { background-position: -100% center; }  /* sweeps left across the word */
  8%,100% { background-position: -100% center; }  /* holds quiet */
}
```

**Stagger timing** (each link gets an `animation-delay`):
| Link | Delay |
|------|-------|
| HOME | 0s |
| SYMPOSIUM | 1.5s |
| SERVICES | 3.0s |
| ABOUT | 4.5s |
| SPONSORS | 6.0s |
| CONTACT | 7.5s |

This means: HOME sweeps at 0s, SYMPOSIUM at 1.5s, SERVICES at 3s, etc. After CONTACT finishes (~8.5s), there's ~11.5s of quiet before the cycle repeats at 20s.

**Note on current nav CSS**: Nav links are `.main-nav a` (see ~line 165 in style.css). The `HOME` link with `.active` class has an underline — make sure the shimmer doesn't break the active underline styling. Test the `currentColor` approach first; if it conflicts with the underline `border-bottom`, you may need to keep the underline as a `::after` pseudo-element instead.

**Hover interaction**: On hover, the shimmer should pause and the link should just show a clean gold color (already the current `:hover` behavior). Add `animation-play-state: paused` on hover.

---

## 2. Hero Ambient Breathing

**Date line** (`.hero-meta` — "MARCH 28–29, 2026 — OCALA, FLORIDA"):
```css
.hero-meta {
  animation: softBreathe 6s ease-in-out infinite;
}

@keyframes softBreathe {
  0%, 100% { opacity: 0.75; }
  50%      { opacity: 1; }
}
```

**Gold rule** (`.hero-rule` — the thin gold line under the title):
```css
.hero-rule {
  animation: ruleGlow 8s ease-in-out infinite;
}

@keyframes ruleGlow {
  0%, 100% { width: 80px; opacity: 0.5; }
  50%      { width: 100px; opacity: 0.85; }
}
```

**Tagline** (`.hero-tagline` — the italic subheadline):
```css
.hero-tagline {
  animation: taglineBreathe 7s ease-in-out infinite;
}

@keyframes taglineBreathe {
  0%, 100% { opacity: 0.7; }
  50%      { opacity: 1; }
}
```

**Learn More CTA** (`.hero-cta`):
```css
.hero-cta {
  animation: ctaPulse 5s ease-in-out infinite;
}

@keyframes ctaPulse {
  0%, 100% { box-shadow: 0 0 0 0 rgba(181, 149, 90, 0); }
  50%      { box-shadow: 0 0 20px 2px rgba(181, 149, 90, 0.15); }
}
```

### Why different cycle lengths
Using 5s, 6s, 7s, 8s creates a polyrhythm — elements go in and out of sync naturally, so the hero never looks like everything is pulsing together. It feels organic, like breathing.

---

## 3. Section Intro Gold Line Animation (Optional Enhancement)

Each `.section-intro .label::before` (the thin gold divider line above section labels) could grow in from center:

```css
.section-intro .label::before {
  animation: lineGrow 1s ease-out forwards;
  transform: scaleX(0);
}

@keyframes lineGrow {
  to { transform: scaleX(1); }
}
```

Trigger this when the element gets `.visible` from the scroll reveal system (already in place via IntersectionObserver).

---

## 4. Timing Summary

| Element | Animation | Duration | Easing | Notes |
|---------|-----------|----------|--------|-------|
| Nav links | Gold shimmer sweep | 20s cycle | ease-in-out | Staggered 1.5s apart |
| Hero date | Opacity breathe | 6s | ease-in-out | 0.75 → 1 |
| Hero gold rule | Width + opacity pulse | 8s | ease-in-out | 80px → 100px |
| Hero tagline | Opacity breathe | 7s | ease-in-out | 0.7 → 1 |
| Hero CTA | Box-shadow glow | 5s | ease-in-out | Gold 0→15% opacity |
| Section divider lines | Scale from center | 1s once | ease-out | On scroll reveal |

---

## Key CSS Selectors Reference

| Element | Selector | File Location |
|---------|----------|---------------|
| Nav links | `.main-nav a` | style.css ~L165 |
| Active nav link | `.main-nav a.active` | style.css ~L178 |
| Hero date line | `.hero-meta` | style.css ~L288 |
| Hero title | `.hero-content h1` | style.css ~L300 |
| Hero gold rule | `.hero-rule` | style.css ~L315 |
| Hero tagline | `.hero-tagline` | style.css ~L320 |
| Hero CTA button | `.hero-cta` | style.css ~L327 |
| Section intro label | `.section-intro .label` | style.css ~L428 |
| Section intro gold line | `.section-intro .label::before` | style.css ~L410 |

---

## Implementation Notes

1. All animation CSS goes in `src/style.css` — no JS needed
2. The `@keyframes` can go near the existing animation block (search for `@keyframes gentleBounce` around line 1295)
3. The nav links need `animation-delay` applied via `:nth-child()` since they don't have individual classes:
   ```css
   .main-nav a:nth-child(1) { animation-delay: 0s; }
   .main-nav a:nth-child(2) { animation-delay: 1.5s; }
   .main-nav a:nth-child(3) { animation-delay: 3s; }
   .main-nav a:nth-child(4) { animation-delay: 4.5s; }
   .main-nav a:nth-child(5) { animation-delay: 6s; }
   .main-nav a:nth-child(6) { animation-delay: 7.5s; }
   ```
4. Test on Chrome first (browser-harness). Safari may need `-webkit-` prefixes for `background-clip: text`.
5. The shimmer gold color should be `var(--gold-light)` (#d4b66a) — matches the brand palette.
