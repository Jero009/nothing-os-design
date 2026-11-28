# Web screenshot sources — second measurement source (2026-11-28)

The primary type-scale measurements came from a sanitized 720×1600 screenshot
set (`docs/screenshots/`). This directory adds an independent second source:
full-resolution Nothing OS 5 device screenshots from other devices, collected
from the web, plus official renders for visual reference only.

Rules observed here (mirror of the repo's source discipline):

- **Device screenshots** (community/press) are measurement sources. Every file
  carries its origin below. Density is only asserted where a shot proves it
  (see typography.md "Cross-device validation").
- **Official renders** (`official-*`) are `[official]` visual reference ONLY —
  marketing renders are never measured (scaled/graded, not device output).
- **Press imagery** (`press-*`) is qualitative reference; press screenshots are
  re-encoded by publications, so ink measurements from them are indicative.
- Screenshots are provided as design reference for the measured values;
  Nothing OS UI depicted remains © Nothing Technology Ltd. Community
  screenshots remain the property of their posters (post links below).

## Device screenshots (nothing.community, OS 5.0 announcement thread d/61730)

| File | Device | Resolution | Source |
|---|---|---|---|
| community-phone3-devcheck-display.png | Phone (3) | 1260×2800 | [post 305820](https://nothing.community/d/61730/305820) — [CDN](https://cdn.nothing.community/2026-08-30/1788079409-807011-screenshot-20260830-141214.png) |
| community-phone3-beta-dialog-dark.png | Phone (3) | 1260×2800 | [post 303996](https://nothing.community/d/61730/303996) — [CDN](https://cdn.nothing.community/2026-08-26/1787735930-802734-screenshot-20260826-122022.png) |
| community-phone3-apps-unverified-dark.png | Phone (3) | 1260×2671 | [post 304564](https://nothing.community/d/61730/304564) — [CDN](https://cdn.nothing.community/2026-08-26/1787756634-597164-screenshot-20260826-203145.png) |
| community-phone3a-quickshare.png | Phone (3a) | 1080×2392 | [post 303998](https://nothing.community/d/61730/303998) — [CDN](https://cdn.nothing.community/2026-08-26/1787735933-793314-screenshot-20260826-111445.png) |
| community-phone3a-system-services.png | Phone (3a) | 1080×2392 | [post 305014](https://nothing.community/d/61730/305014) — [CDN](https://cdn.nothing.community/2026-08-27/1787830620-626168-screenshot-20260827-133641.png) |
| community-phone3a-app-info.png | Phone (3a) | 1080×2392 | [post 305041](https://nothing.community/d/61730/305041) — [CDN](https://cdn.nothing.community/2026-08-27/1787833672-351825-screenshot-20260827-142706.png) |
| community-phone3a-qs-light.png | Phone (3a) | 1080×2392 | [post 306556](https://nothing.community/d/61730/306556) — [CDN](https://cdn.nothing.community/2026-09-02/1788334318-439966-screenshot-20260902-124829-1.png) |
| community-phone3a-qs-bt-popup.png | Phone (3a) | 1080×2392 | [post 306556](https://nothing.community/d/61730/306556) — [CDN](https://cdn.nothing.community/2026-09-02/1788334373-202339-screenshot-20260902-124843.png) |
| community-phone3a-notifshade-light.png | Phone (3a) | 1080×2392 | [post 306556](https://nothing.community/d/61730/306556) — [CDN](https://cdn.nothing.community/2026-09-02/1788334645-511246-screenshot-20260902-125817.png) |
| community-phone3a-lockscreen-dark.png | Phone (3a) | 1080×2392 | [post 304993](https://nothing.community/d/61730/304993) — [CDN](https://cdn.nothing.community/2026-08-27/1787824761-840510-screenshot-20260827-115852.png) |
| community-phone2a-beta-ota-dark.png | Phone (2a) | 1084×2412 | [post 310876](https://nothing.community/d/61730/310876) — [CDN](https://cdn.nothing.community/2026-09-23/1790132844-548342-screenshot-20260923-083706.png) |

Device identifications: Phone (3) — About/DevCheck pages in the same poster's
set show "Nothing Phone (3)" and DevCheck reports 1260×2800 @ 458 dpi
("978dp x 440dp"); Phone (3a) — About phone page reads "Nothing Phone (3a)";
Phone (2a) — OTA page build string "PacmanPro" (Phone (2a) codename) at
1084×2412. Nothing's OS 5.0 rollout table (post 1) matches these devices
receiving OS 5 in Aug–Sep 2026.

Density evidence per device — the input for px→sp conversion:

- **Phone (3): 458 dpi (density 2.8625) — read directly from the DevCheck
  screenshot.** Only device in the set with an in-shot density readout.
- Phone (3a), Phone (2a): no density readout captured; sp values are derived
  against the Phone (3)-anchored comparison in typography.md and carry the
  uncertainty stated there. Screenshots are retained so the measurements can
  be re-derived when a density readout becomes available.

## Nothing X on an emulator (own capture)

| File | What | Source |
|---|---|---|
| nothing-x-scanning-emulator.png | Nothing X 2.1.1 scanning page, headless Android emulator (Pixel 6 profile, API 35, 1080×2400, density verified 420 dpi via `wm density`) | own capture; APK from [APKMirror, Nothing X 2.1.1 universal](https://www.apkmirror.com/apk/nothing-technology-limited/ear-1/ear-1-2-1-1-release/nothing-x-2-1-1-android-apk-download/) |

Used to validate the ink-height method against authentic Nothing app UI at a
known density (app text should land on clean sp steps).

## Official renders ([official] — visual reference only, never measured)

| File | Source |
|---|---|
| official-os5-announcement-1..6 | Nothing's own OS 5.0 announcement images, post [302895](https://nothing.community/d/61730/302895): [1](https://cdn.nothing.community/2026-08-25/1787655201-288972-image1-1.jpg), [2](https://cdn.nothing.community/2026-08-25/1787655228-340444-image2-1.png), [3](https://cdn.nothing.community/2026-08-25/1787655274-909675-imag3-1.png), [4](https://cdn.nothing.community/2026-08-25/1787655305-797573-image-4-1.png), [5](https://cdn.nothing.community/2026-08-25/1787655333-429526-image5-1.png), [6](https://cdn.nothing.community/2026-08-25/1787655375-51046-image6-1.png) |
| official-us-nothing-tech-hero.webp | [us.nothing.tech/pages/nothing-os](https://us.nothing.tech/pages/nothing-os) (Sanity CDN, retrieved 2026-11-28) |
| official-us-nothing-tech-bt-connect-popup.webp | us.nothing.tech/pages/nothing-os (Sanity CDN) |
| official-us-nothing-tech-font-chooser-roboto-vs-geist.webp | us.nothing.tech/pages/nothing-os (Sanity CDN) |
| official-us-nothing-tech-lock-micrographics.webp | us.nothing.tech/pages/nothing-os (Sanity CDN) |
| official-us-nothing-tech-lockscreen-notification.webp | us.nothing.tech/pages/nothing-os (Sanity CDN) |
| official-us-nothing-tech-qs-separate-vs-classic.webp | us.nothing.tech/pages/nothing-os (Sanity CDN) |
| official-us-nothing-tech-quickshare-qr.webp | us.nothing.tech/pages/nothing-os (Sanity CDN) |
| official-us-nothing-tech-statusbar-closeup.webp | us.nothing.tech/pages/nothing-os (Sanity CDN) |

## Press imagery (qualitative reference)

| File | Source |
|---|---|
| press-androidpolice-font.jpg | Android Police OS 5 hands-on (anpoimages CDN): [nothing-os-5-font.JPG](https://static0.anpoimages.com/wordpress/wp-content/uploads/wm/2026/08/nothing-os-5-font.JPG) |
| press-androidpolice-home.jpg | Android Police OS 5 hands-on: [nothing-os-5-home.JPG](https://static0.anpoimages.com/wordpress/wp-content/uploads/wm/2026/08/nothing-os-5-home.JPG) |
| press-androidpolice-lock.jpg | Android Police OS 5 hands-on: [nothing-os-5-lock.JPG](https://static0.anpoimages.com/wordpress/wp-content/uploads/wm/2026/08/nothing-os-5-lock.JPG) |
| press-9to5androidpolice-partner-quick-settings.jpg | Press quick-settings shot (Android Police / 9to5Google hands-on): [nothing-os-5-quick-settings.JPG](https://static0.anpoimages.com/wordpress/wp-content/uploads/wm/2026/08/nothing-os-5-quick-settings.JPG) |

Press files were re-encoded (metadata stripped, resized) before archiving, so
they are not byte-identical to the publication originals; URLs above point at
the original CDN assets.

## Reviewed and excluded from measurement

- Announcement-campaign renders (kept as `official-os5-announcement-*` for
  reference): scaled marketing renders — never a measurement source.
- Press review shots other than the four above (91mobiles hands-on, Beebom):
  resized in-page assets; qualitative reference only, not archived.
- Screenshots that show no readable system UI text at known scale (wallpapers,
  camera shots, Reddit memes, DevCheck pages of other apps).
