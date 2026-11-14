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
- Press feedback: scale 0.97 + opacity 0.85, 140ms — no color flash.

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
- RemoteViews allow-list: TextView/LinearLayout/FrameLayout/ImageView only.
- Data encodings identical between app and widget; skin switch re-renders via
  a pushed themeStyle field, defaulting to classic on garbage.

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
