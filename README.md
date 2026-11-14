# Nothing OS Design — measured spec

A pixel-measured, source-checked design specification for building apps and
themes in the **Nothing OS / Nothing OS 5** visual language.

Nothing publishes no official design-token spec. Everything here was either
taken from Nothing's own materials (labeled **[official]**) or measured
pixel-by-pixel from a real Nothing OS 5 device and a working reference
implementation (labeled **[impl]**). Every claim is audited in
[`docs/fact-check.md`](docs/fact-check.md) with sources.

> **Not affiliated with Nothing Technology Ltd.** "Nothing OS" and related
> marks belong to their owner. No Nothing proprietary assets (NDot, NType,
> Lettera fonts, icon artwork) are included or shipped — only open-licensed
> stand-ins are recommended.

![Nothing OS element mockups — dark and light, built from the measured tokens](docs/mockup-elements.png)

*Element mockups built from the measured tokens — interactive version:
[`docs/mockup-elements.html`](docs/mockup-elements.html)*

## Highlights — the parts everyone gets wrong

1. **Active states invert, they don't colorize.** On a real device: switch ON =
   white track/black knob, selected segment = grey-on-grey, QS tiles that are
   on are solid **#FFFFFF with black icons**. Color is not how this OS says
   "active".
2. **The accent is a signal, not a style.** Nothing red **#D71921** (measured
   exactly on-device) appears ~0–2 times per screen: destructive, live,
   error, needs-attention. Never on primary buttons, tabs, or links.
3. **The OS 5 "Translucent" material never frosts app pages.** Measured with
   the Translucent style active system-wide: Settings/quick settings stay
   solid `#1B1B1B` on true `#000000`. Translucency exists only over the
   wallpaper (home screen).
4. **The OS 5 color engine reaches the icon layer.** On a blue wallpaper the
   same home icon that is `#D71921` red in Classic renders `#1294D2` — the
   personalization hue replaces signal-colored icons, while system UI stays
   monochrome.
5. **Geometry is mode- and style-invariant.** Measured identical radii/rows
   across dark/light × Classic/Translucent (settings cards 25px @720 ≈ 13dp,
   rows 88px, QS tile gaps ~40px). Mode = color swap only.

## Contents

| File | What's in it |
|---|---|
| [`docs/tokens.md`](docs/tokens.md) | Full token tables: brand palette, classic dark/light, OS 5 deltas, complete 2×2 style×mode matrix, accent decision table — all measured values |
| [`docs/typography.md`](docs/typography.md) | Font roles & stacks, per-element type scale (size/weight/tracking), Nothing's official leading/tracking specs |
| [`docs/components.md`](docs/components.md) | Buttons, switches, chips, lists, alerts, dot-matrix icon construction (9×9 / 25×25), motion, accessibility |
| [`docs/fact-check.md`](docs/fact-check.md) | Claim-by-claim audit with verdicts and sources — the credibility layer |
| [`docs/screenshots/`](docs/screenshots/) | Sanitized reference screenshots covering all four style×mode combinations |
| [`skill/SKILL.md`](skill/SKILL.md) | The same spec packaged as a [Hermes Agent](https://hermes-agent.nousresearch.com/docs) skill (drop-in for agent use) |

## Methodology

Measurements were taken from on-device screenshots (720×1600) by sampling
pixel colors at known element positions, fitting corner radii by scanning
edge insets and least-squares fitting a circle, and cross-checking dominant
colors per region. Device-under-test ran Nothing OS 5.0 (Android 17). Values
labeled [impl] come from a production app implementation
([dashbord](https://github.com/Jero009/dashbord), `src/theme/variables.css`)
that has shipped through multiple releases.

Primary sources: Nothing OS 5.0 announcement (nothing.community, 2026-08-25),
nothing.tech OS 5 page, nothing.wiki brand reference, Vercel Geist / Google
Fonts Doto / Florian Karsten Space Grotesk licensing pages.

## Fonts (legal note)

Nothing's own typefaces are proprietary brand assets — **do not ship them**.
The spec uses these open (SIL OFL 1.1) stand-ins:

| Role | Classic | OS 5 |
|---|---|---|
| Body / headings | Space Grotesk | Geist |
| Numerics | Doto | Geist Mono |

## Using it

- **Designing an app/theme**: start with `docs/tokens.md`, follow the accent
  decision table, check your result against the guardrails in the Highlights.
- **Agent use**: copy `skill/` into your Hermes skills directory.
- **Verifying a claim**: `docs/fact-check.md` lists the verdict and source for
  every load-bearing number.

## License

MIT — see [LICENSE](LICENSE). Screenshots are provided as design reference
for the measured values; Nothing OS UI depicted remains © Nothing Technology
Ltd.
