# Nothing OS design — full token reference

Labels: **[official]** = from Nothing's own materials; **[impl]** = working
implementation value (dashbord `src/theme/variables.css` unless noted).
Claim-by-claim audit: `fact-check.md`. Verified 2026-11.

## Brand palette [official]

| Role | Name | Hex | Notes |
|---|---|---|---|
| Foundation | Pure Black | #000000 | layout/text base |
| Foundation | Pure White | #FFFFFF | |
| Foundation | Window Grey | #B1B3B3 | secondary text, dividers |
| Foundation | N-Grey | #DCD7D2 | |
| Foundation | — | #F4F4F4 | light section backgrounds |
| Primary | N-Red | #C8102E print / **#D71920** on-screen (refs also cite #D71921) | THE signal accent |
| Primary | N-Blue | #002F6C | data encoding only |
| Primary | N-Yellow | #FFC700 | data encoding only |

## App tokens — classic style

### Dark (default, `:root`) [impl]

| Token | Value |
|---|---|
| `--nt-bg` | #000000 (true OLED black) |
| `--nt-surface` | #1A1A1A |
| `--nt-surface-2` | #242424 (elevated/pressed) |
| `--nt-tile` | rgba(ink, 0.055) inset panel |
| `--nt-border` | rgba(ink, 0.08); strong: 0.12 |
| `--nt-text` | #FFFFFF; dim: rgba(ink, 0.5); glow: rgba(ink, 0.18) |
| `--nt-ink` | 255,255,255 (raw RGB triplet → any alpha) |
| `--nt-accent` | #D71A21 (impl; canonical official: #D71920) — press: #B21319; on-accent text: #FFFFFF |
| `--nt-data-positive` | rgb(34,197,94); light mode: rgb(21,128,61) |
| `--nt-data-goal` | #FFD700; light mode: #B8860B |
| Fonts | body/head: Space Grotesk; display numerics: Doto; mono: Space Mono |
| Tracking | label 0.12em, kicker 0.18em |
| Radii | 8 / 16 / 24 / pill 999 |
| Spacing | 4 / 8 / 12 / 16 / 24 / 32 |
| Motion | 140/280/400ms; decel cubic-bezier(0.2,0,0,1); std cubic-bezier(0.4,0,0.2,1); press-scale 0.97 |

### Light (`html.theme-light`) [impl]

| Token | Value |
|---|---|
| `--nt-bg` | #EBEBEB |
| `--nt-surface` | #FFFFFF; surface-2 #E2E2E2 |
| `--nt-border` | rgba(0,0,0,0.08); strong 0.14 |
| `--nt-text` | #0A0A0A; dim rgba(0,0,0,0.5) |
| `--nt-ink` | 10,10,10 |

## App tokens — OS 5 deltas (`html.theme-os5`, re-points only) [impl]

| Token | OS 5 dark | OS 5 light |
|---|---|---|
| `--nt-font-body`/`head` | Geist [official face] | Geist |
| `--nt-font-display` (numerics) | Geist Mono [official face] | Geist Mono |
| `--nt-font-accent-display` | Doto — HERO ONLY | Doto — hero only |
| `--nt-font-mono` | Geist Mono | Geist Mono |
| `--nt-tracking-label` / `kicker` | 0.10em / 0.16em | same |
| `--nt-radius-sm/md/lg` | 12 / 20 / 28 | 12 / 20 / 28 |
| `--nt-surface` | rgba(20,20,20,0.66) + frost | rgba(255,255,255,0.72) + frost |
| `--nt-surface-2` | rgba(44,44,44,0.72) | rgba(255,255,255,0.9) |
| `--nt-surface-fallback` (solid, overlays) | #141414 | #FFFFFF |
| `--nt-frost` | blur(24px) saturate(1.4) | same |
| `--nt-border` | rgba(255,255,255,0.10); strong 0.16 | black 8%; strong 14% |
| `--nt-text-dim` | rgba(255,255,255,0.55) | rgba(0,0,0,0.5) |
| Dot-grid substrate | rgba(255,255,255,0.045) | rgba(0,0,0,0.05) |
| Widget panel (native) | #D9141414, 28dp radius, #1FFFFFFF hairline | — |

## Accent decision table

See SKILL.md for the framework. Classic Nothing default = **monochrome
inversion** for active states; accent red = signal only. With an OS 5-style
expression accent, the "expression" column below tints with the user hue.

| Element | Signal red | Active-state treatment (classic → expression) |
|---|---|---|
| Switch/toggle ON | never | invert (white track) → accent fill |
| Slider/progress fill | never | invert/white → accent fill |
| Selected tab / chip / segment | never | invert (white fill) → accent |
| Checkbox/radio selected | never | invert → accent fill |
| Focus ring | never | hairline → accent ring |
| Destructive confirm | YES | always red |
| Live/recording/sync pulse | YES | red dot |
| Error/warning threshold | YES | red |
| Needs-decision badge | YES | red |
| Deload/sickness status glyph | YES (it is a signal) | red |
| Navigation chrome, toolbars | never | never |
| Body text, titles, dividers | never | never |
| Whole cards / empty states | never | never |
| Goal/positive data encodings | never (stay gold/green) | never |

Rules: 0–2 accent elements per screen; ≤1 hero signal region per screenful;
accent alpha via color-mix, never new hex; on-accent text flips white/black
by contrast; danger stays red even when the expression accent is another hue.

## MEASURED FROM DEVICE — Nothing OS 5.0 (real device, 2026-11-14)

Pixel-measured from OS 5 screenshots (720×1600 scale; ≈2 px/dp on a
1080-class panel — treat dp as ±15%). Source: on-device screenshots shared by
the user; PNG compression shifts colors ±1–2 bits.

**Theme context:** the device was running the OS 5 **"Translucent" style as
the active system theme for every screenshot** — including Settings, QS and
notifications. Those pages STILL render solid #1B1B1B on #000000. The
translucent material therefore only exists over the wallpaper (home screen /
lock screen); OS 5 does NOT apply transparency to app pages at all. Apps that
frost their cards are going beyond what the OS itself does — dashbord's OS5
frost is a deliberate extrapolation, not a copy of system behavior.

### Colors

| Element | Measured | Notes |
|---|---|---|
| Page background (Settings/QS/notifications) | **#000000** | true black everywhere [confirms OLED rule] |
| System surface (settings cards, QS tiles, notif cards, search bar, theme rows) | **#1B1B1B** | ONE grey for all system surfaces (dashbord uses #1A1A1A — same family) |
| QS music chip / elevated surfaces | #1F1F1F | slightly elevated |
| Circle icon buttons | #1C1C1C | |
| QS tile ON | **#FFFFFF** fill, black icon | strong inversion — never colored [confirms accent framework] |
| Switch ON | #F2F2F2 track + black knob | inversion, not color |
| Switch OFF | dark track, mid-grey #929292 knob | |
| Segment control | container #141414, selected pill #303030 | text #F2F2F2 selected / #929292 unselected — greyscale selection, never colored |
| Colour-engine swatches | #54AEEA / #93A4EB / #EA8BAA | the personalization hues live ONLY in swatches + home tinting |
| Dynamic color in Settings | #E9D2FD icon chip | Material-You remnant reduced to tiny icon chips |
| Headphones-app CTA red | **#EC232B** | companion-app primary CTA — the one place red drives a primary button (brand-app exception) |
| Widget battery ring | ~#CAB11A (gold family) | data encoding, not chrome |
| Dot-clock lit dots | ≈ white at 60–70% over panel | |

### Geometry (@720px; ≈2px = 1dp)

| Element | Measured | ≈dp |
|---|---|---|
| Page side margin (settings/cards) | 28px | 14 |
| Settings single-line row height | 88px | 44 |
| Settings card radius | **25px** (clean fit) | 12–13 |
| Grouped rows: internal gap / group gap | 2–3px / 26px | 1 / 13 |
| Search bar | stadium, 94px tall | 47 |
| Notification card radius | **26px** (clean fit) | 13 |
| Notification stack gap | 4–6px | 2–3 |
| QS tile radius | ≈40px | 20 |
| QS 2×1 tile | ≈283×120px; vertical gaps ≈40px | 141×60, gap 20 |
| QS tall pill (brightness) | 122×283px, stadium | 61×141 |
| Switch track | 68×48px, stadium | 34×24 |
| Theme&Style rows | radius ≈17px (tight fit) | 9 |
| Home long-press menu pills | 109px tall, stadium, gaps ≈6px | 54, gap 3 |
| Home widget panel radius | ≈22px | 11 |
| Home widget h-gap | ≈22px | 11 |

### Complete 2×2 matrix (measured 2026-11-14, second batch)

Same screens re-shot in every style×mode combination. **Geometry is
identical across all four** (settings card radius 25px, rows 88px, group gap
26px in dark AND light; search bar stadium both) — mode changes only color,
style changes only home panels + accent hue.

| Surface | Classic dark | Classic light | Translucent dark | Translucent light |
|---|---|---|---|---|
| App page bg | #000000 | #F1F1F1 (Headphones #F2F2F2) | #000000 | #F1F1F1 |
| App cards | #1B1B1B | #FCFCFC / #FFFFFF | #1B1B1B | #FCFCFC |
| QS shade bg | #000000 | **#E2E2E2** (darker than tiles!) | same as classic | same as classic |
| QS inactive tile | #1B1B1B (lighter than bg) | **#D1D1D1** (darker than bg) | — | — |
| QS ON / filled | #FFFFFF + black icon | #FFFFFF + black icon | — | — |
| App active fill | #FFFFFF or red | **#1C1C1C** + white icon (NC circle, segment) | — | — |
| Home widget panels | **opaque #1B1B1B** (exact, all widgets) | **opaque #F1F1F1** | wallpaper × ≈0.25 (≈70–75% black scrim) | wallpaper + ≈30–50% white (hue passes through) |
| Icon accent hue | **#D71921** (red, measured EXACT) | #D71921 | red | **wallpaper hue** — measured #1294D2 on a blue wallpaper |
| Settings dynamic icon chip | #E9D2FD | #FFFFFF | — | — |

Notes:
- **#D71921 confirmed EXACTLY on-device** (2,860 pure pixels of the classic
  timer icon, zero antialiasing) — this settles the brand-reference value as
  the canonical on-screen red. dashbord's #D71A21 is one bit off; Headphones'
  #EC232B CTA is a separate, brighter app-brand red.
- **The OS 5 color engine recolors the icon accents themselves**: the same
  timer icon slot that is #D71921 in Classic is #1294D2 in Translucent on a
  blue wallpaper. Expression accent reaches further than controls — it
  replaces red signal-icons on the home layer.
- Light-mode hierarchy inverts differently per surface: pages get DARKER
  cards (#FCFCFC on #F1F1F1), but the QS shade gets DARKER tiles (#D1D1D1 on
  #E2E2E2) — recessed off-tiles, white on-tiles.
- Translucent light scrim is lighter-but-tinted (≈30–50% white over
  wallpaper); translucent dark is darker-but-tinted (≈70–75% black). Both
  carry the wallpaper hue; Classic is always opaque exact-value.

### Typography observed on device

- Hero page titles ("Settings", "My devices") render in the **NType82 serif
typewriter face**; small app-bar titles + body text in **Geist**.
- Widget text ("D2", "L1", "10") uses the serif face; dot-matrix numerals
  (clock "1 6 0 5") only where the widget is itself a clock.
- Takeaway for apps: serif typewriter face = hero/editorial layer; Geist =
  everything functional.
