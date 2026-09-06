# Hydra Samsung SM-X400 Android development stack

This branch catalogs the FOSS Android components used by Project Hydra's Samsung SM-X400 development lane. It intentionally does **not** copy Hydra runtime code into the Android FOSS catalog.

## Project integration repos

- `eggie-admin/hydra-shell-android`
  - integration branch: `sm-x400-widget-shizuku`
  - owns the Termux:Widget supervisor integration and read-only Shizuku sanity tooling
- `eggie-admin/vue-headless-cms`
  - source branch: `samsung-sm-x400-build-candidate`
  - pinned source head: `215310cff47d65311d6e7ff60eb63d6f176a444b`

## FOSS dependency/source forks

- `eggie-admin/termux-app`
  - Android terminal/runtime source lane
- `eggie-admin/Shizuku`
  - privilege-broker source lane
  - Hydra integration branch: `hydra-sm-x400-integration`
  - upstream source license remains Apache-2.0
- `eggie-admin/termux-x11`
  - optional display/X11 research lane

## Device trust lanes

### Stock Samsung / Secure Folder development

Preferred:

1. stock Samsung firmware
2. Developer Options enabled
3. USB or Wireless debugging enabled only when needed
4. Shizuku started using ADB / wireless debugging
5. explicit app authorization
6. Termux + Termux:Widget for localhost service control

Root and Sui are excluded from this trusted lane.

### Rooted laboratory Samsung

Root / Sui is a separate experimental target. It must not claim Secure Folder or Knox trust.

## Architecture rules

- Shizuku is optional and external to the APK dependency graph.
- Missing optional tools must downgrade capability instead of breaking the ordinary build.
- Privileged actions must be typed and allow-listed.
- Never execute arbitrary model-authored shell commands.
- Keep localhost development services bound to loopback.
- Preserve upstream licenses and provenance in each dependency/source fork.

## Current portable surface

The Android-dev integration branch tracks:

- Termux:Widget supervisor contract
- Samsung SM-X400 runtime dependency manifest
- Shizuku privilege-broker manifest
- read-only ADB/Shizuku sanity probe
- Secure Folder vs rooted-lab trust separation

This catalog branch is documentation-only so future updates from the upstream Android FOSS project remain easy to rebase.
