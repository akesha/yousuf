# Handoff: Yousuf Marvi Personal Site

## Overview
A single-page personal portfolio for an educator / leader. Five anchored sections — Home (intro + animated stats), Project (4-slide image carousel), Articles (writing list with hover preview), Awards (fellowships / credentials grid), and Contact (scroll-driven timeline + form).

## About the Design Files
The files in this bundle are **design references created in HTML** — a working prototype showing the intended look and behavior, not production code to copy directly. The task is to **recreate this design in the target codebase's existing environment** (React, Next.js, etc.) using its established patterns, components, and libraries. If no environment exists yet, choose an appropriate framework — Next.js + Tailwind is a natural fit for this static-leaning site.

## Fidelity
**High-fidelity.** Final colors, typography, spacing, animations, and interactions are all in place. Recreate pixel-perfectly.

## Screens / Sections

### 01 Home
- **Layout:** Two-column hero (text left, "Theme cards" right), then a 3-up animated stats row.
- **Theme cards:** 3 stacked cards. Click toggles an open state revealing a description popover anchored to the right of the card. Magnetic hover (subtle translate toward cursor on mousemove).
- **Stats:** Three counters that animate from 0 to target on viewport entry: 38k+ students, 1k+ teachers, 14y+ teaching.

### 02 Project (slideshow)
- **Layout:** 5fr / 7fr grid, 60px gap. Left = title + body + counter. Right = 4:3 photo frame with image-slot drop targets.
- **Slides:** 4 entries (Math Counts team / Robotics / Global Math Project / Newcomer note). Title is sans-serif 800-weight, ~64px. Body is dim-grey 16px.
- **Nav:** Yellow circular prev/next buttons inset on the frame's edges (-32px), keyboard ←/→, and yellow pill dot pagination centered along bottom of frame.
- **Transitions:** Slide image cross-fades + scale (0.55s ease). Copy fades and translates on each change (0.5s).
- **Counter:** `01/04` style, current number white, total dim.

### 03 Articles
- **Layout:** Vertical list of horizontal cards (thumbnail · meta + title + body · arrow).
- **Hover:** A floating preview card follows the cursor, showing title / kicker / excerpt with a yellow left border and pointer-arrow at bottom-center. Cursor-following uses requestAnimationFrame + lerp at 0.18.

### 04 Awards
- **Layout:** 4-column grid (Fellowships, Credentials, Teacher Training, Curriculum Dev). Each is a vertical list of organization names.

### 05 Contact (scroll-driven timeline)
- **Layout:** Centered vertical spine with a yellow glowing traveler dot that follows scroll progress. Three checkpoints alternate left/right of the spine, each lighting their dot when the traveler reaches them. Ends with a closing headline + 4-field contact form.
- **Form fields:** Name, Email, Subject, Message. Yellow accent border on focus.

## Global UI Elements

### Side menu (right rail, fixed)
- Vertical list of 5 anchor links: `01 02 03 04 05`. Active section's number turns yellow (#DFF314), tick line extends to 48px and glows, small dot pops to the left. Hover reveals the section label.
- Auto-hides under 880px.

### Custom cursor (hover:hover devices only)
- 6px yellow dot + 34px ring. Ring grows to 64px on hover targets, becomes a vertical text-caret on inputs. `mix-blend-mode` not used; ring is semi-transparent yellow.

### Atmosphere
- Fixed yellow corner glows: 60vmax radial blooms top-left and bottom-right at 22% opacity, 40px blur. Behind everything, follows scroll naturally because they're position:fixed.
- SVG noise grain layer overlaid on the page.

### Word-reveal animation
- Display headlines split per-word; each word fades up 28% with an 8px → 0 blur transition (1.1s, ease).

### Scroll snap
- `scroll-snap-type: y proximity` on `<html>`. Each major section is `min-height: 100vh` and `scroll-snap-align: start`. Contact section is exempt (long timeline scrolls freely).

## Design Tokens

### Colors
```
--bg:        #181818   (page background)
--panel:    #1f1f1d   (card surfaces)
--ink:        #f4f1ea   (primary text)
--ink-dim: #9b988e   (secondary text)
--line:       #2a2a28   (borders)
--accent: #DFF314   (yellow brand highlight)
```

### Typography
- **Sans (body / UI):** `DM Sans`, system-ui fallback. Weights 400/500/600/700/800.
- **Serif (display / accents):** `Piazzolla`, georgia fallback. Weight 500 for headlines.
- **Display headline scale:** `clamp(44px, 6vw, 80px)`, line-height 1.04, letter-spacing -0.02em.
- **Slideshow title scale:** `clamp(36px, 4.4vw, 64px)`, sans 800.

### Spacing & Radius
- Section padding: 140px top / 120px bottom / 32px sides
- Card radius: 12-28px
- Pill radius: 999px

### Shadows
- Card lift: `0 30px 60px -20px rgba(0,0,0,.5)`
- Yellow accent halo: `0 0 12px rgba(223,243,20,.5)`

## Interactions Summary
- Smooth scroll, proximity snap on root sections
- Magnetic hover on theme cards + article rows
- Article hover-card follows cursor with lerp
- Slideshow: arrows, dots, keyboard, copy fade-out → swap → fade-in
- Stats: counter animation on intersection observer
- Contact timeline: scroll progress drives traveler position; checkpoints light up sequentially

## Assets
- All photos are user-supplied via `<image-slot>` drop targets. The component is in `image-slot.js`.
- No third-party images bundled. Logos / faces shown in screenshots are placeholders.

## Files
- `index.html` — single-page site, all sections
- `image-slot.js` — drag-and-drop image placeholder web component (used in the slideshow)

## Deploying as a live site (GitHub Pages)
This is a static site — `index.html` + `image-slot.js` only.
1. Create a new GitHub repo.
2. Drop both files at the root.
3. Settings → Pages → Build from `main` branch, root folder.
4. Live URL appears in 30–60 seconds.
