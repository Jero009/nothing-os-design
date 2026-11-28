# Fact-check audit — claims vs sources (2026-11-14)

Verdicts: ✅ verified · ⚠️ deviation/nuance · 📌 unspecified by Nothing
([impl] by definition). Audit covers the dashbord app's DESIGN.md +
variables.css claims, this skill's own claims, a (2026-11-25)
second-implementation cross-check against MissingCore/Music, a
(2026-11-28) on-device system-UI type-scale measurement pass, and a
(2026-11-28) second-source cross-check on independent OS 5 devices.

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
| dashbord accent `#D71A21` (215,26,33) | ⚠️ | nothing.wiki's on-screen/widget red is `#D71920`; some refs cite `#D71921`. One bit off in two channels — imperceptible, intentional app token. Canonical red settled 2026-11-14 by device measurement: **`#D71921`** (see "RED SETTLED" below). `#C8102E` is the PRINT brand red — never on-screen in Nothing system UI; a third-party app may adopt it as its own semantic error hue (2026-11-25 cross-check). |
| dashbord colors selection with red (tabs, checkboxes, segment pills) | ⚠️ | Classic Nothing inverts active states monochrome (white track switch, white-fill selected chip); red reserved for signals (0–2 per screen). dashbord's choice = OS 5 expression-accent style with accent defaulting to red. Legitimate, but pick ONE treatment app-wide and know which convention you're in. |
| dashbord ships Doto Rounded-Black (heavy weight) | ⚠️ | Community weight rule: dot-matrix display ≈400–500 — heavy weights smear adjacent dots and pinch curve tops. Black Rounded is a deliberate chunkier look; if dot separation reads badly at a size, drop weight, don't scale up. |
| "Nothing OS Widget Red #D71920" vs #D71921 in the wild | ⚠️ | Two authoritative-adjacent sources disagree by one bit. Document both; treat as identical. |

## Unspecified by Nothing (impl values, deliberately chosen)

📌 Frost `blur(24px) saturate(1.4)`, surface alphas `.66/.72` — app
approximation of the official "frosted" material.
📌 Radii scales 8/16/24 and 12/20/28 — Nothing publishes no token spec; the
"~50% growth" OS 5 direction is official, the numbers are not.
📌 Spacing scale, motion durations/easings, surface hexes — reference-
implementation values that work; adopt freely, label as impl.
📌 Type scale: the OS 5 **system-UI** scale is now device-measured
(2026-11-28 — see the type-scale pass below and typography.md); the
**app** type scale remains a dashbord impl value.
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

## Second-implementation cross-check (2026-11-25, MissingCore/Music)

Cross-checked against [MissingCore/Music](https://github.com/MissingCore/Music)
(AGPL-3.0, Google Play + GitHub, self-described "A Nothing inspired local
music player") — a second independent, source-checkable implementation of the
Nothing language in a non-Nothing app. Full study:
[`third-party-case-studies.md`](third-party-case-studies.md). Values read from
`mobile/src/constants/Styles.ts`, `src/modules/customization/theme/core/constants.ts`,
`src/modules/widget/constants/Config.ts`, `assets/fonts/`, `THIRD_PARTY.md`.

| Claim | Verdict | Source |
|---|---|---|
| `#D71921` as the primary/signal red | ✅ exact second source | `Styles.ts` nRed50 = #D71921; theme `primary` |
| `#FFC700` as secondary/data color | ✅ exact | `Styles.ts` yellow50 = #FFC700; theme `secondary` |
| Dark app surface = true `#000000` (OLED rule) | ✅ exact | theme `surface: neutral0` |
| Elevated dark container `#1C1C1C` | ✅ exact | matches the device-measured circle icon buttons; theme `surfaceContainerLowest` |
| Light containers `#D1D1D1` | ✅ exact | matches measured light QS off-tiles; `neutral83` |
| Light page surface `#F2F2F2` vs measured `#F1F1F1` | ✅ 1 bit off | theme `surface` |
| Press/dim DARKENS the accent (~10–15%) | ✅ pattern in both impls | nRed50→nRed40 `#AE141B` (MissingCore); `#D71A21`→`#B21319` (dashbord) |
| Two-red system: signal `#D71921` vs error `#C8102E` | ⚠️ nuance | MissingCore theme `primary` vs `error`; this spec documented `#C8102E` as print-only for Nothing system usage — apps may adopt it as the semantic error hue while keeping `#D71921` as signal |
| Grey ramp granularity (7-step dark container ladder `#121212…#3B3B3B`) | 📌 impl | both impls differ from the measured single `#1B1B1B` system surface; apps need more steps than the OS shows |
| Third-party Nothing integration via standard MediaSession only | ✅ | Nothing Media Player widget + Glyph Music Visualization work with the app without proprietary APIs (`docs/nothing-interactions.md` in that repo) |
| **NDot JP** (`NDot日本語`, x.com/NdotJP_Font) exists as an OFL-1.1 community NDot derivative | ✅ | `THIRD_PARTY.md` line 38; bundled as `Ndot-77_JP_Extended.ttf` |
| Bundling Nothing's proprietary NType82 without attribution | ⚠️ risk observed (do not copy) | `assets/fonts/NType82-*.otf` present; no license entry in `THIRD_PARTY.md`/`licenses.json`; nothing.wiki lists NType82 as brand-restricted |

Sources (added): github.com/MissingCore/Music — `Styles.ts`,
`theme/core/constants.ts`, `widget/constants/Config.ts`, `Waveform.tsx`,
`Vinyl.tsx`, `SeekBar.tsx`, `marquee.tsx`, `docs/widgets.md`,
`docs/nothing-interactions.md`, `assets/fonts/`, `THIRD_PARTY.md`
(accessed 2026-11-25, dev history through v3.9.x).

## Haptics & sound audit (2026-11-25, docs/feedback.md)

| Claim | Verdict | Source |
|---|---|---|
| Predefined effects (EFFECT_TICK/CLICK/HEAVY_CLICK/DOUBLE_CLICK) via `createPredefined` are Android 10+, device-tailored, automatic fallback | ✅ | developer.android.com VibrationEffect reference + haptics-apis page |
| Composition primitives (PRIMITIVE_TICK/CLICK/LOW_TICK/THUD/SPIN/rise/fall, scale 0–1) are Android 11+ per constant, **no automatic fallback** — check `areAllPrimitivesSupported` | ✅ | developer.android.com custom-haptic-effects + source.android.com haptics-constants-primitives |
| Android 16 (26Q4) adds `VibrationEffect.Builder` + Presets as the preferred composition API with automatic fallback | ✅ | developer.android.com custom-haptic-effects ("On Android 16 (26Q4), VibrationEffect.Builder is the preferred API") |
| A crisp LRA click lasts 10–20 ms; unbraked actuators can ring ~300 ms | ✅ | developer.android.com actuators primer; TI LRA primer |
| Nothing Phone (2) actuator is a small Z-axis LRA | ⚠️ single third-party source | jonesconsortium.com mobile-haptic-feedback latency survey (actuator table) |
| `VIBRATE` permission required for VibrationEffect use | ✅ | developer.android.com haptics-apis |
| Nothing-integrated sound+light for third-party apps goes through the Glyph Developer Kit — API key from Nothing required, unkeyed debug expires after 48 h | ✅ | github.com/Nothing-Developer-Programme/Glyph-Developer-Kit README; nothing.tech/pages/glyph-developer-kit |
| Glyph Composer composes ringtones that sync sound with glyph LEDs | ✅ | nothing.tech Glyph Composer; press coverage (gadgetbridge.com, nerdschalk.com) |
| Nothing system UI plays no tap/click sounds — interaction feedback is haptic | 📌 | absence claim from the measured screenshot set; no system tap-sound evidence found. Treat as impl default |
| Haptic vocabulary (6 gestures × predefined effects, amplitude 100–200, strength = amplitude scale) | ⚠️ impl | Essential Island `util/HapticStyle.kt` (shipped) |
| Scrub ticks fire on selection change only | ⚠️ impl | dashbord `docs/DESIGN.md` + `useChartScrub.ts` |
| Alert sound ducks (never stops) the user's audio, then restores | ⚠️ impl | dashbord `restTimerAudio.ts` + native `RestTimerAudio.duckAndDing` (transient-can-duck focus) |

Sources (added): developer.android.com
(/reference/android/os/VibrationEffect, /develop/ui/views/haptics/haptics-apis,
/develop/ui/views/haptics/custom-haptic-effects,
/develop/ui/views/haptics/actuators), source.android.com
(/docs/core/interaction/haptics/haptics-constants-primitives),
github.com/Nothing-Developer-Programme/Glyph-Developer-Kit,
nothing.tech/pages/glyph-developer-kit, jonesconsortium.com
mobile-haptic-feedback-latency-test (2026-11-25).

## Type-scale measurement pass (2026-11-28, system UI)

Ink-height row profiling of tight text crops in `docs/screenshots/`
(720×1600, dark style). Full table + method: typography.md "Nothing OS 5
system UI type scale". Density 2.0 assumed (720px = 360dp; corroborated by
88px settings rows = 44dp). Geist cap ratio 0.715 rendered from the OFL
font file. These are our own measurements — not Nothing-published values.

| Measurement | Verdict | Source |
|---|---|---|
| Page title "Settings" serif cap 45px (≈31–32sp) | ✅ measured | settings-dark.png; headphones-nc-dark.png |
| Sub-page serif title "My devices": first pass said 24px ≈17sp — that band is the x-height; 'M' cap is 32px ≈22sp at the assumed density (both themes, glyph profile + 3× visual check) | ⚠️ corrected same day | headphones-nc-dark.png; headphones-light.png |
| Settings row label cap 18–20px (≈13sp); search placeholder 22px (≈15sp) | ✅ measured | settings-dark.png |
| QS tile label 16–18px (≈12sp); clock digits 24px (≈17sp, weight ≈600); date 19px (≈13sp); status pill 26px (≈17sp); "54%" 20px (≈14sp) | ✅ measured | qs-dark.png |
| Status bar time 23px (≈16sp) — larger than AOSP's 14sp | ⚠️ corrected same day: 23px was the adjacent notification-icon row; clock digits are 16px (≈11sp at the assumed density) — see the second-source section below | settings-dark.png (pixel row-profile re-verified) |
| Card title 17px (≈12sp) sits BELOW row-label size (≈13sp); subtext 17px (≈11–12sp); fine print "90%" 14px (≈10sp) | ✅ measured | headphones-nc-dark.png |
| Slider tick labels unreadable (luminance < 28 in sanitized captures); settings value/subtext strips clipped | 📌 not measurable | headphones-nc-dark.png; settings-dark.png |

Notes: the serif title faces are proprietary, so their sp equivalence
assumes cap ≈ 0.70em and is approximate. Corroborates the 2026-11-14
finding "Hero titles use the NType82 serif typewriter face, functional
text Geist" — the serif appears at sub-page title sizes too (≈22sp at the
assumed density).

## Type-scale second-source cross-check (2026-11-28, web devices + emulator)

Independent OS 5 devices (Phone (3), Phone (3a), Phone (2a)) from the OS 5.0
announcement thread, plus Nothing X 2.1.1 on a 420 dpi emulator (real
Nothing app text at a known density). Files and per-file sources:
`docs/screenshots/web/` (SOURCES.md there). Method: same ink-height row
profiling with padded word boxes; contested values re-verified at pixel
level. Full tables: typography.md "Cross-device validation".

| Measurement | Verdict | Source |
|---|---|---|
| Ink-height method reproduces the 720×1600 table within ±1–3px on most roles; two first-pass mis-reads surfaced (status clock, sub-page title cap) and are corrected | ✅ validated | settings-dark.png; qs-dark.png; headphones-nc-dark.png re-measured |
| Status-clock digits are 16px, not 23px — the 23px band is the adjacent notification icons; ≈11sp at the assumed density 2.0 | ⚠️ corrected | settings-dark.png (pixel row profile: clock 44–57, icons 35–57) |
| Status-clock size varies per device (21px / 27px / 32–36px raw on Phone (2a)/(3a)/(3)) — no single device-independent status-clock sp | ⚠️ device-specific | web/ community shots |
| Phone (3) system UI at DevCheck-verified 458 dpi (2.8625): page serif titles 63–64px (≈22–23sp), sub-page titles 36–45px (≈18–22sp), body 32px asc (≈14–15sp) | ✅ measured, density verified in-shot | community-phone3-devcheck-display.png; community-phone3-apps-unverified-dark.png; community-phone3-beta-dialog-dark.png |
| Nothing X 2.1.1 at 420 dpi (2.625): body 26px asc ≈13sp, title cap 46px ≈24–25sp — method lands on clean sp steps on authentic Nothing app UI | ✅ validated | nothing-x-scanning-emulator.png |
| Absolute sp on the 720-device rests on the unverified density-2.0 assumption; the original corroboration (88px rows = 44dp) assumed the same density (circular). Hierarchy reproduces; treat absolute sp as ±10–15% | ⚠️ uncertainty stated | typography.md "Cross-device validation" |
| OS 5 ships ≥2 QS layouts: compact (720-device, 16–18px tile labels) and redesigned large-clock shade (Phone (3a): 56px clock, 31px labels); official "QS separate vs Classic" material corroborates | 📌 two layouts | community-phone3a-qs-light.png; official-us-nothing-tech-qs-separate-vs-classic.webp |
| Phone (3a) / Phone (2a) density readouts absent from shots; their sp derived only comparatively | 📌 not derivable from captured shots | community-phone3a-*.png; community-phone2a-beta-ota-dark.png |

Notes: the corrections are applied to typography.md in the same revision
(status-time row + findings bullet). The serif sub-page title finding
survives the cross-check — Phone (3) shows the same tier at ≈18–22sp, and
the 720-device 'M' cap re-measures at 32px (≈22sp assumed density), not the
24px x-height read of the first pass.

## Sourcing & labeling pass (2026-11-28, dashbord-only truth audit)

Repo-wide sweep of every dashbord citation. Most already carry
[impl]/"reference implementation" labels (tokens.md header, components.md
header, typography.md app scale, feedback.md sources, SKILL.md tiers).

| Finding | Verdict | Source |
|---|---|---|
| OS 5 app pages do NOT frost — only wallpaper-anchored surfaces are translucent; components.md stated "OS 5 cards: frosted" as OS behavior without the app-side scope | ⚠️ corrected same day | tokens.md measured section (2026-11-14 device pass) |
| Live site presented dashbord-only values (radii scale, motion 140/280/400, kicker/label tracking) without [impl] tags; tags added, card demo frost scope noted | ⚠️ fixed | docs/index.html |
| Token exports carried a stale version (1.3.0) not matching releases; now version-locked to the release | ⚠️ fixed | tokens.json meta; tokens.css header |
| dashbord-only values that remain, all labeled [impl]: classic surfaces #1A1A1A/#242424 (system measures #1B1B1B), accent #D71A21 (canonical #D71921), radii 8/16/24 + 12/20/28, spacing 4/8/12/16/24/32, motion 140/280/400 + easings + press-scale 0.97, tracking 0.10/0.12/0.16/0.18em, app type scale, alert/row/chip metrics, scrub-tick + duck-and-ding patterns | 📌 impl by definition, labeled | tokens.md; components.md; feedback.md; tokens.json; tokens.css |
