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
| Page title, sub-page — serif typewriter | "My devices" (headphones-nc-dark) | 'M' cap | 24px | ≈17sp |
| Card title | "Noise Cancellation" (headphones-nc-dark) | 'N' cap | 17px | ≈12sp |
| List row label | "Lock screen" / "Notifications" / "Customisation" (settings-dark) | 'L' cap / asc–baseline | 18–20px | ≈13sp |
| Search placeholder (dim) | "Search" (settings-dark) | asc–baseline | 22px | ≈15sp |
| QS tile label | "Wi-Fi" / "Torch" / "Modes" (qs-dark) | cap | 16–18px | ≈12sp |
| QS clock | "16:05" (qs-dark) | digit height, weight ≈600 | 24px | ≈17sp |
| QS date (dim) | "Sat 14 Nov" (qs-dark) | asc–baseline | 19px | ≈13sp |
| Status bar time | "16:05" (settings-dark) | digit height | 23px | ≈16sp |
| Battery % (QS header) | "54%" (qs-dark) | digit height | 20px | ≈14sp |
| QS status pill | "…evice is con…" (qs-dark) | asc–baseline, weight ≈500 | 26px | ≈17sp |
| Card subtext (dim) | "On · Adaptive" (headphones-nc-dark) | asc–baseline | 17px | ≈11–12sp |
| Fine print (dim) | "90%" (headphones-nc-dark) | digit height | 14px | ≈10sp |

Not measurable in the sanitized shots: slider tick labels ("Low/Mid/High/
Adaptive" — luminance below 28, dimmer than ~10% white) and the settings
row value/subtext lines (clipped/blur strips in the sanitized captures).

Findings:
- Status text runs larger than stock Android (status time ≈16sp vs AOSP
  14sp); the QS clock is only ≈17sp but heavy (≈600) — the "chunky" look
  is weight, not size.
- Sub-page serif titles exist (≈17sp): the typewriter face is not only a
  top-level hero move.
- Card titles (≈12sp) sit BELOW list row labels (≈13sp) — hierarchy comes
  from weight + tracking, not size.
- Dim roles (date, subtext, placeholder, fine print) stay 50% white.

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
