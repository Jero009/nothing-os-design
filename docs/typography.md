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

## Nothing brand typography specs [official] (for composing brand-style display type)

| Face | Job | Constraints |
|---|---|---|
| NType82 Headline | headlines only | 40pt+, leading 80% of size, tracking −20, one/two words, sentence case |
| NType82 Regular | body / preamble / quotes | leading 125% (7.5–15pt), 115% (15–60pt), 100% (60pt+); tracking +1% (≤30pt) / −1% (>30pt) |
| NType82 Mono | mechanical body blocks | 7.5–15pt max, left-aligned, never mix sizes in one block, tracking untouched |
| NDot 55 | logotype & product names ONLY | leading 90%, tracking 0, never combined with other fonts in one layout |
| Lettera Mono LL | small informative/legal text | 5–10pt only, font width 90%, leading 110%, never at display size |

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
