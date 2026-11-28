# Haptics & sound — feedback spec

How a Nothing-styled app should feel and sound. Labels follow the repo
convention: **[official]** = Nothing's own materials (or the Android platform
docs for platform APIs); **[impl]** = working implementation values.
Haptic/sound vocabulary sources: the Essential Island overlay app
([`util/HapticStyle.kt`](https://github.com/Jero009/essential-island), GPL-3.0)
and the dashbord app (`src/shared/utils/haptics.ts`,
`src/shared/utils/restTimerAudio.ts`, `docs/DESIGN.md`). Claim audit rows in
`fact-check.md` (2026-11-25).

## The one rule

**Interaction feedback is haptic, never audible; sound is alarm-only.**
Nothing's system UI plays no tap/click sounds — the click you "hear" on a
Nothing phone is the haptic. Apps follow: every touch gets its haptic from a
small fixed vocabulary, and sound is reserved for things that must interrupt
(timers, alarms). Decorative UI sounds (whooshes, pops, tap ticks) are never
Nothing.

## Haptics

### Platform building blocks [official — Android]

| API | Since | What | Fallback |
|---|---|---|---|
| `VibrationEffect.createPredefined(EFFECT_TICK / EFFECT_CLICK / EFFECT_HEAVY_CLICK / EFFECT_DOUBLE_CLICK)` | Android 10 (API 29) | device-tailored effects — the OEM tunes them per hardware | automatic (generic waveform); `areEffectsSupported` only tells you if it's the optimized version |
| `VibrationEffect.Composition` primitives (`PRIMITIVE_TICK`, `PRIMITIVE_CLICK`, `PRIMITIVE_LOW_TICK`, `PRIMITIVE_THUD`, `PRIMITIVE_SPIN`, `PRIMITIVE_QUICK_RISE/SLOW_RISE/QUICK_FALL`, scale 0–1) | Android 11+ (per constant) | composable short effects + chirps | **none** — check `areAllPrimitivesSupported` first or the whole effect silently fails |
| `VibrationEffect.Builder` + `Preset` (+ PWLE envelopes) | Android 16 (26Q4) | preferred composition API; presets supersede the short primitives | automatic per-element |
| `HapticFeedbackConstants` (view-level ticks) | 1.5+ | cheap view feedback (keyboard, clock tick) | n/a |

`VIBRATE` permission required for everything below the view-constant layer.
Physical note [official — Android actuators primer]: a crisp LRA click lasts
10–20 ms; unbraked actuators ring for up to ~300 ms — so short predefined
effects beat long custom waveforms on every device.

### Semantic vocabulary [impl — Essential Island]

One fixed vocabulary, mapped to the platform's predefined effects, amplitude
1–255. The vocabulary mirrors the visual grammar — enter is heavier than
exit, hold is heaviest, and a "lock" is deliberately duller than a "collapse"
so same-hand gestures feel different:

| Gesture/event | Effect | Duration | Amplitude | Feel |
|---|---|---|---|---|
| Expand (card opens) | CLICK | 22 ms | 150 | confirm |
| Collapse (card closes) | TICK | 14 ms | 110 | light release |
| Swipe action fires | TICK | 12 ms | 130 | crisp |
| Long-press / hold arm | HEAVY_CLICK | 60 ms | 200 | heavy |
| Merge (two cards join) | TICK | 10 ms | 90 | softest |
| Lock (state sealed) | CLICK | 28 ms | 100 | dull, longer — distinct from collapse |

Strength is a user setting that **scales amplitude** (off / light ×0.55 /
normal ×1.0 / strong ×1.5, clamped 1–255) — it never changes the effect
choice, and `off` vibrates never. On Android 10+ the system's own
device-tuned effect is used instead of the raw buzz; the amplitude numbers
are only the pre-29 fallback.

### Usage rules

- **Tick only when a scrubbed selection CHANGES** (dashbord chart-scrub rule;
  matches the platform pattern — Android's own controls tick on discrete
  value changes, never per frame [official — Android, observable platform
  behavior]) — never per frame, never per intermediate value.
- One haptic per completed gesture; fire on commit, not on touch-down.
- Never haptic decorative motion (entrances, marquee, pulses).
- Respect the system: if haptic feedback is disabled system-wide, do nothing.
- Sound never substitutes for a haptic and vice versa (see below).

### Nothing devices

- Nothing phones use small **Z-axis LRA** actuators (Phone (2) measured as a
  small Z-LRA in a third-party latency survey; single source, ⚠️). The
  character is short crisp clicks, not buzzes — long waveforms ring.
- The **Glyph Developer Kit** (nothing.tech/pages/glyph-developer-kit,
  github.com/Nothing-Developer-Programme/Glyph-Developer-Kit) exposes the
  rear-light `GlyphInterface` to third-party apps: requires an **API key
  provided by Nothing** in the manifest; unkeyed debug mode auto-disables
  after 48 h. If an app wants the Nothing "event becomes light" identity
  (timer, delivery, call), this is the sanctioned path — don't fake it with
  screen flashes or sounds.

## Sound

### Roles

| Sound | When | Behavior |
|---|---|---|
| Alert (timer done, rest over, alarm) | user-scheduled moment | **duck, don't stop**: transient audio focus (`AUDIOFOCUS_LOSS_TRANSIENT_CAN_DUCK` [official — Android platform API]) lowers the user's music, play the cue, restore volume |
| Error | destructive failure | haptic first (error pattern); sound only if the alert also fires |
| UI taps, transitions, toggles | never | haptic carries it; Nothing system UI has no tap sounds |

### Implementation pattern [impl — dashbord]

`restTimerAudio.duckAndDing()`: request transient-can-duck focus → play one
short cue on the alarm channel → restore the user's volume. On platforms
where the native bridge is unavailable, fall back to a Web Audio beep rather
than skipping the alert. Alarm cues ride the alarm volume, so Do-Not-Disturb
and ringer state keep working as the user expects.

### Sound design character

- Short, mechanical, single-layer cues — a "recording-light" of sound.
  No musical stings, no layered UI foley.
- If targeting Nothing hardware and wanting the brand's sound-plus-light
  ringtone identity: that is exactly what **Glyph Composer** (stock app)
  composes — user-created patterns sync sound with the glyph LEDs — and what
  the Glyph Developer Kit exposes programmatically. Ship a Glyph-compatible
  alert; don't sample Nothing's sounds.
- Silence is a feature: most Nothing-style screens should be audible-silent
  and haptic-alive.

## Checklist

- [ ] Every interactive element has a haptic from the fixed vocabulary
- [ ] Scrub ticks fire on selection change only
- [ ] Strength = amplitude scale with an `off`; effect choice never varies
- [ ] No UI tap/transitional sounds anywhere
- [ ] Alerts duck the user's audio and restore it
- [ ] `VIBRATE` permission present; primitive compositions check support
- [ ] (Optional, Nothing hardware) Glyph alerts via the Developer Kit
