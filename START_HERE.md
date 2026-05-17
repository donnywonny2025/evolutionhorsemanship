# Evolution Horsemanship — Project Status & Handoff

> **Last updated:** May 17, 2026 — Antigravity session  
> **Next agent:** Gemini (same workspace)

---

## Quick Start

```bash
cd "/Volumes/WORK 2TB/WORK 2026/evolutionhorsemanship"
npm run dev    # → http://localhost:5173
```

Source repo: `https://github.com/donnywonny2025/evolutionhorsemanship.git` (main)  
Deploy repo: `https://github.com/donnywonny2025/leftdisplay.git` (main → Netlify auto-deploy)

---

## Current State: Production-Ready Landing Page

The site is a single-page landing built with Vite (vanilla HTML/CSS/JS). No frameworks.

### Key Files
| File | What it does |
|------|-------------|
| `src/index.html` | All page structure, scroll restoration script, IntersectionObserver for reveals |
| `src/style.css` | Complete design system — variables, layout, responsive, animations |
| `src/images/` | All presenter photos, ranch imagery, logos |
| `src/media/coming_soon.mp4` | Promo video (945KB, HEVC — may need H.264 fallback) |

### Page Sections (scroll order)
1. **Hero** — Full-bleed horse photo, "The Horseman Symposium" title, animated chevron scroll cue
2. **Symposium** — Dark section: date/venue meta, video showcase, 6-presenter grid, venue line
3. **Equine Services** — Section intro + 2 service rows (True Horsemanship, Boarding)
4. **People Focused Services** — Section intro + 2 service rows (Lifemanship, Business Blast)
5. **Founder** — Donna Blem quote + portrait (dark bg)
6. **Sponsors** — Quality Horseman feature + sponsor strip
7. **Contact** — Two-column: "Visit the Ranch" info (left) + mailing list form (right)
8. **Footer** — Navigation, connect links, copyright

### Design System Variables (defined at top of style.css)
- Colors: `--forest-deep`, `--forest`, `--moss`, `--cream`, `--cream-warm`, `--gold`, `--gold-light`
- Fonts: `--font-display` (Playfair Display), `--font-heading` (Lora), `--font-body` (Raleway)
- Spacing: `--space-xs` through `--space-2xl` (clamp-based)

---

## What Was Done Tonight

1. ✅ Scroll-to-top fix (scrollRestoration = 'manual' in `<head>`)
2. ✅ Header locked (transitions restricted to background/box-shadow only)
3. ✅ "Discover" line replaced with animated chevron scroll cue
4. ✅ Section-intro centering (flexbox + auto margins)
5. ✅ Linda Parelli portrait sourced and added
6. ✅ Video controls: native browser controls appear on play (play/pause, scrubber, volume, fullscreen)
7. ✅ Section separation: alternating service row backgrounds, gold divider borders, bigger section intro padding
8. ✅ Contact section rebuilt: two-column layout with email/Facebook/location (no phone numbers) + mailing form
9. ✅ Footer updated: "Privacy Policy" → "Email Donna"

---

## What's Next: Animations

**See `directives/ANIMATION_SPEC.md` for the full spec** — ready-to-implement CSS with exact timing, selectors, and keyframes.

Summary:
- **Nav light sweep**: Gold shimmer cascades across each nav link sequentially (20s cycle, 1.5s stagger)
- **Hero breathing**: Date, gold rule, tagline, and CTA all have subtle polyrhythmic opacity/glow pulses
- **Section intro reveals**: Gold divider lines grow from center on scroll

Design direction from Jeff: **"Elegant, slick, modern, soft, clean, precise, timed."** This is equestrian luxury — think dressage, not rodeo.

---

## Deployment Pipeline

When ready to show the client:

1. Copy `src/` contents → `/Volumes/WORK 2TB/WORK 2026/leftdisplay/`
2. Ensure `netlify.toml` publish dir is correct
3. `git add -A && git commit -m "Evolution Horsemanship preview" && git push`
4. Netlify auto-deploys from leftdisplay repo
5. Share the live URL with Donna and Mike

### Video Note
`coming_soon.mp4` is HEVC encoded. Consider adding an H.264 fallback `<source>` for broader browser support before deploying.

---

## Git Status

All changes pushed to `main` on GitHub. Clean working tree.

```
https://github.com/donnywonny2025/evolutionhorsemanship.git
```

---

## File Organization

```
src/
├── index.html              # Landing page (single file, ~390 lines)
├── style.css               # Design system + all styles (~1420 lines)
├── images/
│   ├── presenters/         # Linda Parelli, Luis Lucio, Ryan Rose, etc.
│   ├── donna_about.jpg     # Founder portrait
│   ├── ranch_horses.jpg    # Service row imagery
│   ├── horsemanship_*.jpg  # Service imagery
│   ├── business_blast.jpg  # Business Blast section
│   └── quality_horseman_logo.jpg
├── media/
│   └── coming_soon.mp4     # Promo video
directives/
├── ANIMATION_SPEC.md       # ← START HERE for next task
└── DEPLOY_TO_LEFTDISPLAY.md
```
