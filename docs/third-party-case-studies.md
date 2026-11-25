# Third-party case study — MissingCore/Music (2026-11-25)

A source-checked study of a real, shipping third-party app built in the
Nothing visual language. It complements the dashbord reference
implementation: dashbord is a **dashboard app**, MissingCore/Music is a
**media player** — a second independent translation of the same design
language into a non-Nothing app. Where both implementations agree, this spec
treats the value as cross-confirmed; where they diverge, both ranges are
legitimate impl choices.

**The app:** [MissingCore/Music](https://github.com/MissingCore/Music) —
open-source (AGPL-3.0) offline local music player for Android 7+
(React Native/Expo), on Google Play and GitHub releases. Its README:
"A Nothing inspired local music player." It integrates with Nothing devices
through the **standard media session only**: the Nothing Media Player widget
and Glyph Music Visualization work with it without any proprietary API
(`docs/nothing-interactions.md` in that repo) — the sanctioned integration
surface for third-party apps. **No code was copied into this spec; only
measured/observed values are documented, with file references.** This spec
remains MIT.

## Palette cross-check (source: `mobile/src/constants/Styles.ts`,
theme defaults: `src/modules/customization/theme/core/constants.ts`)

| MissingCore value | Role there | This spec's canonical | Verdict |
|---|---|---|---|
| `#D71921` (primary, dark+light) | signal/interactive accent | on-screen red `#D71921` (measured EXACT on device) | ✅ exact second source |
| `#FFC700` (secondary) | secondary/data encoding | N-Yellow `#FFC700` [official] | ✅ exact |
| `#000000` (surface, dark) | page background | true-black OLED rule (measured) | ✅ exact |
| `#1C1C1C` (surfaceContainerLowest) | lowest dark container | measured circle icon buttons `#1C1C1C` | ✅ exact |
| `#D1D1D1` (neutral83) | light container high | measured light QS off-tiles `#D1D1D1` | ✅ exact |
| `#F2F2F2` (light surface) | light page bg | measured light pages `#F1F1F1` | ✅ 1 bit off |
| `#121212` (surfaceBright) | elevated dark surface | dashbord solid fallback `#141414` | ⚠️ same near-black family |
| `#ADADAD` (onSurfaceVariant, dark) | dim text | Window Grey `#B1B3B3` [official] | ⚠️ dimmer variant of the same family |

**Full ink ramps [impl — MissingCore]:** dark surfaces climb
`#000000 → #121212 → #1C1C1C → #212121 → #292929 → #323232 → #3B3B3B` (7
surface steps) with text down `#FFFFFF → #ADADAD → #606060`; light runs
`#FAFAFA → #F2F2F2 → #EBEBEB → #D9D9D9 → #D1D1D1` (containers) on text
`#FFFFFF → #ADADAD`. This is a finer ramp than this spec's 4-value impl set
(`#1A1A1A/#242424/#141414/#EBEBEB`); both fit the measured system values
(`#1B1B1B` surfaces, `#303030` selected pill sits inside MissingCore's
`#292929–#323232` container band).

**Accent ramps [impl — MissingCore]:** red `#AE141B / #C5171F / #D71921`
(nRed40/45/50), yellow `#E5B300 / #F0BB00 / #FFC700`. The dark-theme "dim"
variant of the primary is `#AE141B` — i.e. **press/dim DARKENS the accent**,
matching dashbord's press token (`#D71A21 → #B21319`). Two independent
implementations darken on press by ~10–15%; this spec promotes that to the
recommended pattern: derive pressed/dim states with a darker mix of the same
hue, never a lighter one.

**Two-red system [impl — MissingCore]:** signal/interactive red `#D71921`
separate from the semantic **error** red `#C8102E` (the print brand red,
dim ramp `#AF0E28/#B80F2A`). This spec documents `#C8102E` as print-only for
*Nothing system* usage; MissingCore shows an app may legitimately adopt it as
its error hue while keeping `#D71921` as the signal accent. If you use two
reds, keep the roles fixed app-wide and never swap them.

**Widget defaults [impl — MissingCore] (`modules/widget/constants/Config.ts`):**
bg `#121212`, text `#FFFFFF`, muted `#ADADAD`, active `#D71921` on `#FFFFFF`,
inactive `#323232` on `#FFFFFF`. Same ink hierarchy as the app, red only as
the active/playing signal — consistent with the accent-scarcity budget.

## Typography (source: `assets/fonts/`, `src/modules/customization/font/core/constants.ts`,
`THIRD_PARTY.md`)

- Ships **Geist + Geist Mono** (OFL 1.1, credited) as the primary/mono faces —
  an independent second app choosing the same OS 5 stand-ins this spec
  recommends.
- Ships **NDot日本語 ("NDot JP")**, credited OFL-1.1
  (source: x.com/NdotJP_Font) — a community OFL extension of Nothing's
  proprietary NDot covering Japanese glyphs. This is the one known
  openly-licensed NDot derivative; it is a legitimate alternative to Doto
  where a literal NDot-style dot-matrix face is wanted. (This spec keeps Doto
  as the default recommendation — Doto is variable and maintained on Google
  Fonts.)
- ⚠️ Also bundles `NType82-Regular.otf` / `NType82-Headline.otf` with **no
  license entry** in `THIRD_PARTY.md` or `licenses.json`. NType82 is Nothing's
  proprietary brand face — this is exactly the risk this spec's legal note
  warns about. Recommendation unchanged: **never ship NType82/NDot**; use the
  OFL stand-ins (Space Grotesk / Geist, Doto / NDot JP).

## Component patterns (media player)

All values from source; file references in parentheses.

- **Waveform seekbar** (`navigation/screens/now-playing/components/Waveform.tsx`):
  2px bars on a 1.75px gap, minimum bar height 4px, rounded caps
  (`r = min(1, w/2, h/2)`), amplitudes normalized to the track max and cached
  per track. Progress renders as one path with a two-stop gradient whose stops
  share the same offset — a hard progress edge without two draw passes.
  Requires decoding the local audio file, so it only applies to apps that own
  the audio; remote-media surfaces (e.g. a media card showing another app's
  session) cannot compute it.
- **Vinyl artwork** (`modules/media/components/Vinyl.tsx`): 768-unit SVG —
  artwork circle at half the diameter, disc `#1C1C1C` with an SVG mask hole,
  three groove rings (stroke 3, white @ 7.5% opacity, radii 264/304/344),
  center hole r=12 (surface fill, `#C8C8C8` stroke 6), spin indicator 2×24px
  white when artwork is missing. The vinyl doubles as a seekbar at one
  rotation per 24s (or 1.8s "standard vinyl speed") — playful, but it ties
  scrubbing precision to rotation speed; fine for a full-screen player, not
  for compact surfaces.
- **Slider mechanics** (`components/Form/Slider.tsx`,
  `navigation/screens/now-playing/components/SeekBar.tsx`): track thickness
  12 (seekbar 40 with the waveform overlay), side hit-slop 8, rounded end
  stops, RTL-aware. While dragging, a `renderedPosition` holds the visual and
  the elapsed label at the thumb; the real seek commits **on release**
  (`onComplete`) — the same pattern dashbord ships. Second source confirmed:
  drag previews locally, commits once.
- **Marquee for overflowing titles** (`components/next/blocks/marquee.tsx`):
  linear speed = width/24 per second (24px/s), 3s pause at each end, loops
  back and forth. Use for titles only; never for body text.
- **Widgets carry no progress indicator** (`docs/widgets.md` in that repo):
  the author's stated reason is avoiding a widget update every second. Same
  battery logic behind this spec's "the visual is the hero, one word of text"
  widget rule — glanceable means no live tickers.
- **Theme export/import**: the app's custom themes are JSON files
  (name + scheme + the 26 color roles) importable/exportable in-app — a
  reminder that a token spec should stay exportable as data, not buried in
  stylesheets.
