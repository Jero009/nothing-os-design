# Components — full spec [impl unless noted]

Measured from the dashbord reference implementation (`variables.css`). All
values are tokens in a real codebase — the numbers below are the token
VALUES, never literals in components.

## Surfaces & cards

- Dark: bg `#000000` (true OLED black — never near-black), card `#1A1A1A`,
  elevated/pressed `#242424`, inset tile `rgba(ink, 0.055)`.
- Light: bg `#EBEBEB`, card `#FFFFFF`, pressed `#E2E2E2`.
- Classic cards: borderless — separation from surface contrast alone.
- OS 5 cards: frosted translucent + exactly ONE hairline (white 10% / black
  8%). Never a second accent border. Overlays (alerts, action sheets,
  popovers) use the SOLID fallback — never frost over a dimmed backdrop.
- Dot-grid substrate: `radial-gradient` 1px dots on 12px grid; in OS 5 dimmed
  to 4–5% alpha (barely-there depth cue, dots live BEHIND cards).
- Headers: borderless and shadowless — kill any framework drop-shadow under
  the toolbar (reads as a grey band on true black).
- No box-shadows anywhere; the only glow is the white bloom (below).

## Radii

- Classic: sm 8 / md 16 / lg 24 / pill 999.
- OS 5: sm 12 / md 20 / lg 28 / pill 999.
- Cards and sheets = lg; popovers, inputs, list tiles = md–sm; buttons/chips
  = pill. OS 5 sheet: top corners lg, bottom square.

## Buttons (the inversion rule)

| Role | Fill | Text | Shape |
|---|---|---|---|
| Primary / confirm | solid white (dark) / black (light) — INVERTS | bg color | pill |
| Destructive | solid accent red | white | pill |
| Cancel / ghost | transparent + 1px hairline border | dim ink | pill |
| Tertiary/outline ("yellow" slot) | transparent + hairline | fg | pill |

- In classic Nothing, active/selected states INVERT monochrome — primary
  buttons and selected tabs/chips are white-on-black (dark mode), not colored.
  The accent red is signal-only (see SKILL.md framework).
- Alert button stack: full-width, stacked, min-height 46, column-reverse
  (confirm on top), gap 8.
- Press feedback: scale 0.97 + opacity 0.85, 140ms — no color flash on
  neutral/chrome elements. Accent-filled elements additionally darken their
  accent ~10–15% when pressed (cross-impl rule: dashbord press `#B21319`,
  MissingCore `#AE141B`) — darker, never lighter.

## Selection controls

- Switch ON: white track/black knob (dark), black track/white knob (light).
  With an OS 5-style expression accent: accent fill + on-accent knob.
- Checkbox/radio: 24px, hairline border; checked = accent fill (or inversion
  under the strict classic rule) + on-accent checkmark; selected radio label
  may pick up accent text.
- Selected item in an action sheet/select list: accent text + weight 600, or
  inverted fill — one treatment app-wide.
- Segment pills: container = tile bg, pill radius, padding 6; selected
  segment inverts (accent in the dashbord variant); min-height 34 (compact 30).

## Chips & status

- Chip: pill, 1px hairline, padding 4×10, 0.7rem/500 uppercase + label
  tracking, dim ink; optional 7px round dot INSIDE the chip — the dot is the
  one place the signal accent legitimately lives (live/degraded states).
- Loading pulse: 8px white dot, stepped opacity keyframes (1s, steps(4)) —
  mechanical LED feel, never a smooth breathing gradient.
- Glow (Glyph-style bloom): `0 0 24px rgba(ink, 0.18)` white — never colored
  neon.

## Lists & rows

- List background: surface/elevated; row min-heights: select 48, action-sheet
  row 52, list item 44–48. Row separators: 1px `rgba(ink, 0.04)` — or none;
  prefer whitespace + group cards. No zebra striping.
- Icon + label rows: leading icon 24dp outline (1.5dp stroke, currentColor,
  monochrome — never filled, never multicolored).
- **Icons are never unicode glyphs.** Symbol characters (⏮ ⏭ ✕ ◎ ❚❚) render
  as platform **emoji** — colored, filled, font-dependent. Icons are inline
  SVG (stroke ≈1.5–2.2, round caps, currentColor) or true dot-grids.

## Dot-matrix iconography

- Status/system glyphs: true 9×9 dot grids — CSS grid, every lit cell a
  COMPLETE circle (`border-radius: 50%`). Never `mask`/`clip-path`/dotted
  borders (they clip dots into partial circles). Size via one variable; gap
  scales with it.
- Hero/device-grade glyphs: 25×25 grid (the Glyph Matrix spec), circularly
  masked, generated from geometric functions — not hand-drawn bitmaps.
- Dot punctuation (· : …) renders from the same round-dot unit, slightly
  smaller than digit dots — not font glyphs.

## Widgets (native, glanceable)

- The visual element (bar/grid/ring) is the hero; at most ONE word of text +
  a date. The visual must FILL the frame (no letterboxing) and the widget must
  be shrinkable to 1 cell where the layout allows.
- Native widgets can't frost (RemoteViews): panel = `#D9141414`, 28dp radius,
  `#1FFFFFFF` hairline stroke. Fonts ship as TTFs in res/font.
  ⚠️ Those values are **Android ARGB** (alpha first). In CSS the same colors
  are `rgba(19,19,19,0.08)`-style — writing `#1FFFFFFF` in CSS parses as
  RRGGBBAA = an opaque cyan. Convert the format, never copy the literal.
- RemoteViews allow-list: TextView/LinearLayout/FrameLayout/ImageView only.
- Data encodings identical between app and widget; skin switch re-renders via
  a pushed themeStyle field, defaulting to classic on garbage.

## Media player patterns [impl — MissingCore/Music, source-checked 2026-11]

Second-source study: [`third-party-case-studies.md`](third-party-case-studies.md).
App-side patterns — the OS publishes no media-component spec.

- **Seek interaction**: the thumb and the elapsed label preview the dragged
  position while dragging; the real seek commits **on release**. Two
  independent implementations (dashbord, MissingCore) ship this — treat it as
  the Nothing-style default. Streams without a duration never preview (they
  cannot seek).
- **Waveform seekbar** (only when the app owns the audio file): 2px bars on a
  1.75px gap, min bar height 4px, rounded caps, amplitudes normalized to the
  track max, cached per track; progress = hard color edge along the same
  bars (two gradient stops at one offset). MissingCore colors played bars
  with `primary` (red by default) and remaining bars with
  `surfaceContainerHigh` — note the tension with the 0–2-element accent
  budget; a full-width red hairline is the aggressive reading. The
  conservative choice is ink for played / container-high for remaining.
  Not applicable to remote media sessions — no waveform can be computed from
  another app's stream.
- **Vinyl artwork treatment** (full-screen player): artwork at half diameter
  inside a `#1C1C1C` disc with three white groove rings (stroke ≈0.4% of
  diameter, 7.5% opacity, radii 34%/40%/45% of the disc), center hole
  (surface fill, light-grey stroke), 2×24px spin indicator when artwork is
  missing. Rotation-as-seekbar (1 rotation = 24s) is playful but imprecise —
  keep a normal drag seek for compact surfaces.
- **Marquee on overflowing titles**: linear 24px/s, 3s pause at each end,
  back-and-forth; titles only, never body text. Reduced-motion off-switch.
- **Home-screen widgets: no progress tickers.** A widget that updates every
  second for a playhead burns battery for zero glance value — show controls
  and state, not a moving playhead (MissingCore's documented rationale).

## Motion

- Durations: 140ms micro / 280ms standard / 400ms emphatic.
- Easing: entrances `cubic-bezier(0.2, 0, 0, 1)`; everything else
  `cubic-bezier(0.4, 0, 0.2, 1)`. No springs/bounce/overshoot.
- Animate transform + opacity ONLY. Entrance = fade + 6px rise. Hover =
  opacity drop (~0.8), never a color change.
- `prefers-reduced-motion` handled globally (durations ≈0, iterations 1).
- Haptics (if present): tick only when a scrubbed selection CHANGES.

## Accessibility

- Ink alphas on true black: 50% dim ≈ 5.3:1 (AA), 18% glow is decoration only
  — never carry text at glow alpha.
- Text on accent flips white/black by contrast ratio, not by taste.
- Never signal with color alone: pair the red dot with position/glyph/label.
- Charts keep ink in the mono/dot faces and fixed data colors — same encoding
  app-wide, readable in every skin.
