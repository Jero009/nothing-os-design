# Fact-check audit — claims vs sources (2026-11-14)

Verdicts: ✅ verified · ⚠️ deviation/nuance · 📌 unspecified by Nothing
([impl] by definition). Audit covers the dashbord app's DESIGN.md +
variables.css claims and this skill's own claims.

## Verified correct

| Claim | Verdict | Source |
|---|---|---|
| Geist is the OS 5 system typeface, replacing Roboto/Inter | ✅ | Nothing OS 5.0 announcement (community, 2026-08-25); gizdev firmware font extraction |
| OS 5 dot-matrix demoted to "character rather than compromise readability" | ✅ | Nothing OS 5.0 announcement (direct quote) |
| OS 5 = new frosted translucent software material | ✅ | Nothing OS 5.0 announcement |
| New color engine takes cues from wallpaper; monochrome character stays | ✅ | Nothing OS 5.0 announcement + nothing.tech |
| OS 5 ships alongside the Classic theme, not replacing it | ✅ | Nothing OS 5.0 announcement ("Alongside our Classic theme…") |
| OS 5.0 announced 2026-08-25; Android 17; beta Aug 26 (Phone 3); stable from 2026-10-12; Phone (1)/(2)/CMF Phone (1) excluded | ✅ | 9to5google 2026-08-25 + 2026-10-12; PhoneArena; nothing.tech rollout table |
| Geist + Geist Mono: SIL OFL 1.1, self-hostable (Vercel & Basement Studio) | ✅ | vercel.com/font; github vercel/geist-font; fontsource |
| Doto: SIL OFL 1.1 (Óliver Lalan), variable axes wght 100–900 + ROND 0–100, 6×10 matrix | ✅ | Google Fonts; github oliverlalan/Doto; fontsource |
| Space Grotesk OFL 1.1 (Florian Karsten 2018; variant of Space Mono, Colophon 2016); Space Mono OFL | ✅ | fonts.floriankarsten.com; Google Fonts OFL files |
| Brand palette: #000000, #FFFFFF, #B1B3B3, #DCD7D2, #C8102E, #002F6C, #FFC700 | ✅ | nothing.wiki brand reference |
| NDot/NType/Lettera proprietary — don't ship | ✅ | Nothing brand guidelines; nothing.wiki ("Never use NDot outside logo/product names") |
| Brand typography specs (NType82 80% leading etc.) | ✅ | nothing.wiki brand reference |
| Red used sparingly, "like a recording light" | ✅ | Nothing branding + community consensus |

## Deviations & nuances

| Claim | Verdict | Resolution |
|---|---|---|
| dashbord accent `#D71A21` (215,26,33) | ⚠️ | Official on-screen/widget red is `#D71920` (nothing.wiki); some refs cite `#D71921` (rainbrand). One bit off in two channels — imperceptible, intentional app token. Base truth records `#D71920/#D71921` as canonical. `#C8102E` is the PRINT brand red, never on-screen. |
| dashbord colors selection with red (tabs, checkboxes, segment pills) | ⚠️ | Classic Nothing inverts active states monochrome (white track switch, white-fill selected chip); red reserved for signals (0–2 per screen). dashbord's choice = OS 5 expression-accent style with accent defaulting to red. Legitimate, but pick ONE treatment app-wide and know which convention you're in. |
| dashbord ships Doto Rounded-Black (heavy weight) | ⚠️ | Community weight rule: dot-matrix display ≈400–500 — heavy weights smear adjacent dots and pinch curve tops. Black Rounded is a deliberate chunkier look; if dot separation reads badly at a size, drop weight, don't scale up. |
| "Nothing OS Widget Red #D71920" vs #D71921 in the wild | ⚠️ | Two authoritative-adjacent sources disagree by one bit. Document both; treat as identical. |

## Unspecified by Nothing (impl values, deliberately chosen)

📌 Frost `blur(24px) saturate(1.4)`, surface alphas `.66/.72` — app
approximation of the official "frosted" material.
📌 Radii scales 8/16/24 and 12/20/28 — Nothing publishes no token spec; the
"~50% growth" OS 5 direction is official, the numbers are not.
📌 Spacing scale, type scale, motion durations/easings, surface hexes —
reference-implementation values that work; adopt freely, label as impl.
📌 Exact greys `#1A1A1A/#242424/#141414/#EBEBEB` — not official; consistent
with the official monochrome direction.

## Sources (primary)

- Nothing OS 5.0 official page: us.nothing.tech/nothing-os/ (feature list,
  rollout table)
- Nothing OS 5.0 announcement thread: nothing.community/d/61774 (design
  language essay: material, Geist, color engine, monochrome guardrail)
- Brand reference: nothing.wiki/nothing/brand_reference (palette hexes,
  typography specs, NDot usage rules)
- 9to5google 2026-08-25 (announcement) & 2026-10-12 (stable rollout)
- PhoneArena (2026-08): OS 5.0 official, beta schedule
- vercel.com/font + github.com/vercel/geist-font (Geist, OFL 1.1)
- fonts.google.com/specimen/Doto + github.com/oliverlalan/Doto (Doto, OFL)
- fonts.floriankarsten.com/space-grotesk (Space Grotesk, OFL)
- Community spec: github.com/wangbh030722/vibe-nothing-ui-design (dot-icon
  construction, accent-scarcity budget, Doto weight rule)
- Reference implementation: dashbord repo `docs/DESIGN.md`,
  `src/theme/variables.css` (all impl values)

## Device-measurement verification (2026-11-14)

Pixel-measured from the user's actual Nothing OS 5 phone (11 screenshots;
full numbers in tokens.md "MEASURED FROM DEVICE"). Key confirmations:

- ✅ Page bg is TRUE #000000 (not near-black) — the OLED rule holds on device.
- ✅ Active states INVERT, never colorize: QS ON tiles are solid #FFFFFF with
  black icons; switch ON = white track/black knob; segment selection = grey
  #303030 pill, no hue. The accent framework's core claim is confirmed
  on-device.
- ✅ System surface is one grey ≈#1B1B1B (dashbord's #1A1A1A is the same
  family, 1 bit off).
- ✅ Translucency exists but is a home-screen material: with the Translucent
  style ACTIVE system-wide (confirmed by the user), Settings/QS/notification
  pages still render solid #1B1B1B on #000000; only wallpaper-backed surfaces
  (home widgets) get the ≈75% black scrim. OS 5 never frosts app pages.
- ⚠️ Companion-app exception found: the Headphones app uses a SOLID RED pill
  (#EC232B) as its primary CTA (Reconnect). System UI never does this; brand
  apps may. Note for app design: red primary CTA = consumer-brand voice, not
  the system convention.
- ⚠️ On-device radii (settings cards 25px, notif cards 26px, QS tiles ~40px @
  720-wide ≈ 12–13dp / 20dp) are SMALLER than the dashbord OS5 scale (28px).
  dashbord's 28px-lg is its own choice, not a measured OS value.
- ✅ RED SETTLED: #D71921 measured EXACTLY (2,860 pure px) on a classic-style
  home icon. The nothing.wiki "Nothing OS Widget Red #D71920/#D71921" value is
  confirmed; treat #D71920/#D71921/#D71A21 as one family, #D71921 canonical.
  The Headphones app CTA (#EC232B) is a different, brighter app-brand red —
  not the system red.
- ✅ FULL MATRIX MEASURED (2nd batch): geometry identical across all four
  style×mode combos (settings radius 25px in dark AND light); mode = color
  swap only, style = home panels + accent hue only. Classic panels are opaque
  exact-value (#1B1B1B / #F1F1F1); Translucent panels carry the wallpaper hue
  (dark: ×≈0.25 black scrim; light: +≈30–50% white).
- ⚠️ COLOR ENGINE SCOPE EXTENDED: in Translucent style the wallpaper hue
  replaces the RED ICON ACCENTS themselves (timer icon #D71921 → #1294D2 on a
  blue wallpaper), not just control fills. The expression accent reaches the
  home layer's signal-colored icons; system pages stay monochrome.
- ⚠️ Wallpaper color engine touches very little of system UI: dynamic color
  survives as tiny icon chips (#E9D2FD) + swatches; everything else stays
  monochrome.
- ✅ Hero titles use the NType82 serif typewriter face, functional text Geist.
