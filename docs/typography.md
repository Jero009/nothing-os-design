# Typography — full spec

All faces verified OFL 1.1 (fact-check.md has the sources). Nothing's own
faces are proprietary — the OFL faces below are the legal stand-ins.

## Font roles & stacks

| Role | Classic | Nothing OS 5 |
|---|---|---|
| Body / headings | Space Grotesk (≈NType82 role) | Geist |
| Numerics (tiles, timers, readouts) | Doto (dot matrix ≈NDot role) | Geist Mono |
| Hero display numeral | Doto | Doto — kept as character accent ONLY |
| Mono / fine print | Space Mono (≈Lettera role) | Geist Mono |

Rules:
- Numerals NEVER render in the body face.
- Doto is never body text; in OS 5 it is additionally never a metric tile or
  readout — hero display only.
- In dot-matrix contexts, keep the unit intact: `78%` renders whole in the dot
  face; letter units (GB, K, bpm) stay small sans.
- **Doto weight rule:** large dot-matrix type ≈400–500 weight so adjacent dots
  stay separate and round. Heavy weights (700/900) smear dots together and
  pinch curve tops (the "0" grows a pointed head). Roundness axis (ROND) up =
  rounder dots; the Nothing feel is round dots, not square pixels.
- Uppercase kicker labels with wide tracking (+0.16–0.18em) are the signature
  typographic move.

## Face reference (verified)

| Face | Designer / origin | License | Notes |
|---|---|---|---|
| Geist Sans | Vercel & Basement Studio | SIL OFL 1.1 | 9 weights, geometric Swiss-style |
| Geist Mono | Vercel | SIL OFL 1.1 | 9 weights, tabular/code |
| Doto | Óliver Lalan | SIL OFL 1.1 | variable: wght 100–900, ROND 0–100; 6×10 matrix |
| Space Grotesk | Florian Karsten (2018; variant of Space Mono, Colophon Foundry 2016) | SIL OFL 1.1 | 4 styles + variable |
| Space Mono | Colophon Foundry (2016, Google Fonts) | SIL OFL 1.1 | fixed-width |
| NDot 55 / NType 82 / Lettera Mono LL | Nothing (proprietary) | NOT licensed | never ship; extracted-firmware copies online are unofficial |
| NDot日本語 ("NDot JP", incl. the `Ndot-77_JP_Extended` build) | community extension of NDot | SIL OFL 1.1 | the one openly-licensed NDot derivative (x.com/NdotJP_Font); covers JP glyphs; used by MissingCore/Music. Legitimate NDot-style alternative to Doto; this spec keeps Doto as default (variable, maintained). |

Shipped-app observation (2026-11-25): MissingCore/Music bundles Geist +
Geist Mono (credited OFL) and NDot JP (credited OFL) — and also ships
`NType82-*.otf` files **without any license attribution** (nothing in its
`THIRD_PARTY.md`/`licenses.json`). NType82 is Nothing-proprietary; treat that
as the cautionary example, not a pattern to copy. This spec's rule stands:
**never ship NType82/NDot/Lettera.**

## Nothing brand typography specs [official] (for composing brand-style display type)

| Face | Job | Constraints |
|---|---|---|
| NType82 Headline | headlines only | 40pt+, leading 80% of size, tracking −20, one/two words, sentence case |
| NType82 Regular | body / preamble / quotes | leading 125% (7.5–15pt), 115% (15–60pt), 100% (60pt+); tracking +1% (≤30pt) / −1% (>30pt) |
| NType82 Mono | mechanical body blocks | 7.5–15pt max, left-aligned, never mix sizes in one block, tracking untouched |
| NDot 55 | logotype & product names ONLY | leading 90%, tracking 0, never combined with other fonts in one layout |
| Lettera Mono LL | small informative/legal text | 5–10pt only, font width 90%, leading 110%, never at display size |

## Nothing OS 5 system UI type scale [device-measured 2026-11-28]

Measured from the sanitized device screenshots (`docs/screenshots/`,
720×1600, dark style) by ink-height row profiling of tight text crops.
Density 2.0 assumed (720px = 360dp — corroborated by 88px settings rows
= 44dp). sp estimates = cap height ÷ 2 ÷ 0.715 (Geist cap ratio, rendered
from the OFL font file) rounded to the nearest common Android step, ±1sp.
The serif title faces are proprietary, so their sp equivalence assumes
cap ≈ 0.70em and is approximate.

| Role | Measured text (shot) | Ink measured | px | Est. size |
|---|---|---|---|---|
| Page title, top level — serif typewriter | "Settings" (settings-dark) | 'S' cap, incl ~1px round overshoot | 45px | ≈31–32sp |
| Page title, sub-page — serif typewriter | "My devices" (headphones-nc-dark) | 'M' cap | 32px | ≈22sp (density-2.0 assumed) |
| Card title | "Noise Cancellation" (headphones-nc-dark) | 'N' cap | 17px | ≈12sp |
| List row label | "Lock screen" / "Notifications" / "Customisation" (settings-dark) | 'L' cap / asc–baseline | 18–20px | ≈13sp |
| Search placeholder (dim) | "Search" (settings-dark) | asc–baseline | 22px | ≈15sp |
| QS tile label | "Wi-Fi" / "Torch" / "Modes" (qs-dark) | cap | 16–18px | ≈12sp |
| QS clock | "16:05" (qs-dark) | digit height, weight ≈600 | 24px | ≈17sp |
| QS date (dim) | "Sat 14 Nov" (qs-dark) | asc–baseline | 19px | ≈13sp |
| Status bar time | "16:05" (settings-dark) | digit height | 16px | ≈11sp (density-2.0 assumed) |
| Battery % (QS header) | "54%" (qs-dark) | digit height | 20px | ≈14sp |
| QS status pill | "…evice is con…" (qs-dark) | asc–baseline, weight ≈500 | 26px | ≈17sp |
| Card subtext (dim) | "On · Adaptive" (headphones-nc-dark) | asc–baseline | 17px | ≈11–12sp |
| Fine print (dim) | "90%" (headphones-nc-dark) | digit height | 14px | ≈10sp |

Not measurable in the sanitized shots: slider tick labels ("Low/Mid/High/
Adaptive" — luminance below 28, dimmer than ~10% white) and the settings
row value/subtext lines (clipped/blur strips in the sanitized captures).

Findings:
- The QS clock is only ≈17sp but heavy (≈600) — the "chunky" look
  is weight, not size. (An earlier revision claimed status-bar time ≈16sp
  "larger than AOSP": that 23px band was the adjacent notification icons;
  the clock digits are 16px. Cross-device status clocks vary — see the
  validation section below.)
- Sub-page serif titles exist (≈22sp at the assumed density): the typewriter
  face is not only a top-level hero move.
- Card titles (≈12sp) sit BELOW list row labels (≈13sp) — hierarchy comes
  from weight + tracking, not size.
- Dim roles (date, subtext, placeholder, fine print) stay 50% white.

### Cross-device validation (2026-11-28 — second measurement source)

The single-device table above was re-measured against independent OS 5
devices from web sources (`docs/screenshots/web/`, per-file sources in
`docs/screenshots/web/SOURCES.md`) using the same ink-height row profiling
with padded word boxes, plus Nothing X 2.1.1 on a 420 dpi emulator as an
app-side check (real Nothing app text at a known density).

Density evidence — absolute sp requires it per device:

| Device | Evidence | Density |
|---|---|---|
| Phone (3) | DevCheck page in shot: "458 dpi (xhdpi)", "978dp x 440dp" | 2.8625 (verified) |
| Emulator (Pixel 6 profile, API 35) | `wm density` | 2.625 (verified) |
| Phone (3a) | no readout in shot | unknown |
| Phone (2a) | no readout in shot | unknown |
| 720×1600 source device (table above) | none; 2.0 assumed (720px = 360dp) | unverified |

Measured ink heights per role (px):

| Role | 720 dev (assumed 2.0) | Phone (3) @2.8625 | Phone (3a) @1080 | Phone (2a) @1084 | Nothing X @2.625 |
|---|---|---|---|---|---|
| Status-bar clock digits | 16 | 32–36 | 27 | 21 | 31 (stock Android 17) |
| Page/section serif title (asc–desc) | 57 ("Settings") | 63–64 | 78–84 | — | — |
| Page title (dot face, cap) | — | — | — | — | 46 ("SCANNING") |
| Sub-page title | 32 cap ("My devices" — first pass read the x-height, 24px) | 36–45 | — | — | — |
| Card/list title | 17 cap | — | 40–41 asc | — | — |
| Row label | 18–20 cap | — | 28–41 asc | 19–20 asc | — |
| Body text | — | 32 asc (≈14–15sp) | 34 asc | 19–29 | 26 asc (≈13sp) |
| QS tile label | 16–18 cap | — | 31–32 asc | — | — |
| QS shade clock | 24 digits | — | 56 digits | — | — |

Findings:

- The method validates: re-measuring the 720×1600 shots reproduces the table
  within ±1–3px on most roles (two first-pass mis-reads surfaced and are
  corrected: the status clock and the sub-page title cap), and Nothing X app
  text at the verified 420 dpi lands on clean sp steps (body ≈13sp, page
  title ≈24–25sp).
- Correction: the earlier "Status bar time 23px ≈16sp" measured the adjacent
  notification-icon row (icons are 23px tall), not the clock — the clock
  digits are 16px (≈11sp at the assumed density). Status-clock size is NOT
  uniform across OS 5 devices (21–36px raw across four devices); treat any
  single status-clock sp value as device-specific.
- Absolute sp on the 720-device rests on the unverified density-2.0
  assumption; its original corroboration (88px rows = 44dp) assumed the same
  density and is circular. Role hierarchy and relative sizes reproduce
  across all devices; treat the table's absolute sp as ±10–15% until a
  density readout for that device exists.
- OS 5 ships at least two quick-settings layouts: the 720-device's compact
  shade (16–18px tile labels) and a redesigned large-clock shade on
  Phone (3a) (56px clock, 31px tile labels) — matching the official
  "QS separate vs Classic" material. Tile-label sp differs between them;
  don't mix measurements across the two layouts.
- Serif sub-page titles are confirmed on a second device: Phone (3) shows
  the same tier at ≈18–22sp (36–45px @2.8625), consistent with the corrected
  ≈22sp above. (The first pass read the "My devices" x-height, 24px, as the
  cap; glyph-level profiling gives 'M' cap = 32px.)

The dashbord scale below is the reference app's own scale — prefer this
device-measured table when building Nothing-style UI.

## App type scale [impl — measured from the dashbord reference implementation]

Base font 16px. All label-class text is UPPERCASE + tracking.

| Element | Face | Size | Weight | Line | Tracking | Color |
|---|---|---|---|---|---|---|
| Page title (toolbar) | head | 1rem | 600 | — | 0.12em (label) | fg |
| Card title | head | 1.2rem | 600 | — | — | fg |
| Alert/sheet title | head | 0.95rem | 600 | — | 0.1em | fg |
| Alert message / body | body | 0.875rem | 400 | 1.5 | — | dim |
| Kicker (`.nt-kicker`) | head | 0.72rem | 400 | — | 0.18em | dim |
| Label (`.nt-label`) | head | 0.75rem | 500 | 1.2 | 0.12em | dim |
| Metric tile label | head | 0.75rem | 400 | — | 0.1em | dim |
| Metric tile value | display (mono/dot) | 0.95rem+ | 600 | 1 | — | fg |
| Chip (`.nt-chip`) | head | 0.7rem | 500 | 1 | 0.12em | dim |
| Empty state | body | 0.9rem | 400 | — | — | dim |
| Button (alert) | head | 0.78rem | 600 | — | 0.1em | per role |
| Action-sheet row | head | 0.9rem | 400 | — | 0.04em | fg |

- Ink hierarchy: fg 100% → dim 50% → glow 18% (dark); OS 5 softens dim to 55%.
- OS 5 tightens label tracking to 0.10em / kicker to 0.16em (Geist runs wider
  than Space Grotesk).
- Hierarchy comes from size jumps + weight + case, NOT from color — reserve
  non-grey colors for signal/data (see accent framework in SKILL.md).
