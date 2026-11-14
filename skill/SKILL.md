---
name: nothing-os-design
version: 1.1.0
author: Hermes Agent
license: MIT
description: "Use when styling Nothing OS-style apps: tokens, accents."
metadata:
  hermes:
    tags: [design-system, nothing-os, theme, typography, accent]
    related_skills: [dashbord-app]
---

# Nothing OS design language — base truth

A standalone, shareable spec for building Nothing-styled apps and themes.
Every load-bearing number is labeled **[official]** (from Nothing's own
materials) or **[impl]** (a working implementation choice — sensible, but not
an official Nothing spec). Nothing publishes no formal design-token spec, so
most exact values are [impl]; the [official] layer is the palette, the type
philosophy, and the OS 5 direction. Full claim-by-claim audit with sources:
`references/fact-check.md`.

## When to use

- Bootstrapping a NEW app or theme that should wear the Nothing look.
- Styling, reviewing, or extending pages/components/widgets in a themed app.
- Accent-color picker / theme-switcher / dark-light work.
- Judging "does this look Nothing?" — check it against the guardrails below.

## Authority & sources

- **Tier 1 — official:** nothing.tech Nothing OS 5.0 page; Nothing's OS 5.0
  announcement (community forum, 2026-08-25; Android 17; open beta Aug 26 on
  Phone (3), stable from 2026-10-12); nothing.wiki Nothing brand reference
  (palette + typography specs).
- **Tier 2 — verified assets:** Geist + Geist Mono (Vercel & Basement Studio,
  SIL OFL 1.1); Doto (Óliver Lalan, SIL OFL 1.1, variable axes wght 100–900 /
  ROND 0–100, 6×10 dot matrix); Space Grotesk (Florian Karsten 2018, OFL 1.1,
  a proportional variant of Space Mono, Colophon Foundry 2016, OFL).
- **Tier 3 — reference implementation:** the dashbord app
  (`~/projects/dashbord/docs/DESIGN.md`, `src/theme/variables.css`) carries
  battle-tested [impl] values; community spec `github.com/wangbh030722/
vibe-nothing-ui-design` (SPEC/DESIGN) for dot-icon and accent-scarcity rules.
- Nothing's own faces (NDot 55/57, NType 82, Lettera Mono LL) and icon artwork
  are **proprietary brand assets — never ship them**. Use the OFL stand-ins.

## Core vision (all styles)

A hyper-minimalist, technical interface: raw data, structural honesty, built
from typography and geometry — no photographic or decorative assets. It should
feel like it runs directly on the hardware (dot-matrix numerals, LED-like
readouts, exposed engineering).

- **Typography does the heavy lifting.** Hierarchy comes from size jumps,
  uppercase kickers with wide tracking, and weight — not from color or icons.
- **Structure comes from hairlines and whitespace.** No drop shadows, no
  gradients. (A frosted `backdrop-filter` is material, not shadow — allowed.)
- **Motion is mechanical, never springy.** No bounce, no parallax.

**The monochrome guardrail** (Nothing's own rule, never break it): the system
stays *predominantly* black/white/grey. Color exists only as signal (scarce
accent) or data encoding (semantic data colors). Even OS 5's wallpaper-driven
color engine tints icons/widgets/controls while "Nothing's predominantly
monochrome character stays underneath" [official].

## The accent framework (the part everyone gets wrong)

Two different jobs share the word "accent". Separate them:

1. **Signal accent — color as alarm.** One hue (Nothing red, `#D71920`
   [official]), tiny area, high intent: live/recording, needs-decision,
   over-limit, destructive, error. Budget: **0–2 accent elements per screen**
   — if two things glow, nothing is signaled. Never on primary buttons, tabs,
   links, sliders, or hover by default.
2. **Active-state treatment — color as response.** Classic Nothing does NOT
   colorize active controls: **active states invert black↔white** — switch ON
   = white track/black knob (dark mode), selected chip/tab/primary button =
   white fill + black text, reversed in light mode. The OS 5 color engine
   introduces tinting controls with the user's wallpaper hue — that is the
   **expression accent**: an opt-in personalization layer applied to control
   state (switch-on fill, slider fill, selected tab/chip, progress fill,
   focus ring). Monochrome inversion is the default; tinting is the OS 5-era
   option.

**What gets the signal accent (allowed):** live/recording dots, destructive
confirm buttons, error/warning thresholds, needs-attention badges, at most one
hero signal region per screenful.

**What never gets any accent:** navigation chrome, toolbars, backgrounds, body
text, titles, dividers, borders, whole cards, empty states, decoration.
Data-semantic colors (goal = gold, positive = green) are a separate channel —
they never paint chrome and are never repainted by an accent picker; danger
stays red even when the expression accent is another hue.

**Mechanics:** accent is a token, never a literal; alpha variants derive via
`color-mix(in srgb, var(--accent) N%, transparent)`; text on accent flips
white/black by contrast; don't signal with color alone — pair the accent dot
with a glyph or position.

## The two styles

Nothing OS 5.0 ships OS 5 as an *additional style alongside the classic
theme* [official], not a replacement. Apps mirror this with a two-axis theme:
`mode` (dark/light) × `style` (classic/os5), implemented as pure token swaps
so no page knows the active skin.

| | Classic (Nothing OS ≤4) | Nothing OS 5 |
|---|---|---|
| Body/headings | Space Grotesk (NType82 stand-in) | **Geist** [official] |
| Numerics | dot-matrix font (NDot/Doto) | **Geist Mono** [official] |
| Dot-matrix | the numeric workhorse | **hero display only** — "character rather than compromise readability" [official] |
| Card material | flat solid grey `#1A1A1A` [impl] | **frosted translucent** material [official concept; exact blur/alpha = impl] |
| Radii | 8 / 16 / 24 [impl] | **12 / 20 / 28** [impl] |
| Depth | dot-grid texture, flat fills | layering + translucency |
| Accent / data colors / motion | unchanged | unchanged |

## Color system

**Foundation (layout + text, never accents) [official]:** Pure Black `#000000`,
Pure White `#FFFFFF`, Window Grey `#B1B3B3` (secondary text/dividers),
N-Grey `#DCD7D2`, `#F4F4F4` (light section backgrounds). In-app dark theme:
bg `#000000` (true OLED black), surfaces `#1A1A1A` / `#242424`, ink hierarchy
via white alphas (100% / 50% / ~18% glow) [impl].

**Signal accent [official]:** Nothing red `#D71920` (nothing.wiki "Nothing OS
Widget Red"; some references cite `#D71921` — one bit apart; the print/brand
primary is `#C8102E`, print-only). Nothing also defines N-Blue `#002F6C` and
N-Yellow `#FFC700` — in apps these survive only as *data* encodings, never
chrome.

**Data colors (semantic, fixed across styles) [impl]:** gold = goal encoding
(`#FFD700`, dark-mode-safe), green = positive (`rgb(34,197,94)`; darkened in
light mode). They never paint navigation, cards, or decoration.

Full tables: `references/tokens.md`.

## Surfaces, spacing, motion (shared) [impl]

- Spacing scale 4 / 8 / 12 / 16 / 24 / 32 px; cards pad 16, page gutters 16
  (24 on ≥600px), section gaps 24–32; max content width 760px.
- Motion: 140 / 280 / 400 ms; entrances `cubic-bezier(0.2,0,0,1)`, standard
  `cubic-bezier(0.4,0,0.2,1)`; animate transform/opacity only; press feedback
  = scale 0.97; hover = opacity drop, never color change; global
  `prefers-reduced-motion` handling.
- OS 5 frost: `backdrop-filter: blur(24px) saturate(1.4)` over
  `rgba(20,20,20,.66)` (dark) / `rgba(255,255,255,.72)` (light) + one hairline
  border (white 10% / black 8%). Floating overlays use the SOLID fallback
  (`#141414` / `#FFFFFF`) — blur over a dimmed backdrop reads as mud. Solid
  fallback when backdrop-filter is unsupported. Native widgets can't frost
  (RemoteViews): translucency + hairline is the honest approximation
  (`#D9141414`, 28dp radius, `#1FFFFFFF` stroke).

## Typography (summary — full spec in `references/typography.md`)

- Classic: Space Grotesk body/head + Doto numerics + Space Mono. OS 5: Geist
  body/head + Geist Mono numerics + Doto as hero-display accent only. All OFL,
  self-hosted; never ship Nothing's proprietary faces.
- Doto weight rule: keep dot-matrix type ≈400–500 weight so dots stay separate
  and round; heavy weights smear dots together.
- Numerals (timers, tiles, readouts) always render in the mono/dot face of the
  active style — never the body face. Uppercase kickers with +0.16–0.18em
  tracking are the signature move.

## Components (summary — full spec in `references/components.md`)

Buttons invert (primary = white fill/black text; destructive = solid red;
cancel = ghost hairline), cards are borderless in classic / one hairline in
OS 5, dot icons are true 9×9 grids of complete circles (never mask-clipped),
line icons are 24dp outlined 1.5-stroke monochrome.

## Implementation pointers

- dashbord app specifics (token names, widget layout pairs, skin-agnostic
  rules) → the `dashbord-app` skill + `~/projects/dashbord/docs/DESIGN.md`.
- Mockups/wireframes comparing skins: `~/projects/dashbord/docs/design/`.
- Measuring from Nothing OS screenshots: extract bg/surface/hairline-alpha/
  radius/row-height/list-padding and express as tokens; never hard-code
  measured px into components.
- Claim disputes: check `references/fact-check.md` before "correcting" a
  value — the official/impl labels are deliberate.