# Hydra Samsung SM-X400 Android development stack

This fork catalogs the FOSS Android components used by Project Hydra's Samsung SM-X400 development lane. It intentionally does **not** copy Hydra runtime code into the Android FOSS catalog.

## Canonical integration repos

- `eggie-admin/vue-headless-cms`
  - branch: `samsung-sm-x400-build-candidate`
  - owns the build-candidate, Vue/Godot frontend, widget packaging, full-stack manifest, and CI contract
- `eggie-admin/hydra-shell-android`
  - default branch: `main`
  - merged Samsung/Shizuku baseline: `4cad0eb56afe431446e54f880085a60576f6ffb8`
  - owns the Termux:Widget supervisor and localhost service control plane
- `eggie-admin/YagniLauncher`
  - default branch: `master`
  - Samsung kiosk merge: `f8bbb4c1bb67e2497e7ad9b0f0274754039b844a`
  - owns optional typed launcher actions for Cockpit, Termux, Shizuku, and Termux:X11

## FOSS dependency/source forks

- `eggie-admin/termux-app`
  - Android terminal/runtime source lane
  - Samsung integration is promoted only after native build, unit-test, and Gradle-wrapper checks are green
- `eggie-admin/Shizuku`
  - default branch: `master`
  - Hydra integration merge: `9a0b7df5fa757f295b07ba6e3c7a3dc3182a20a0`
  - privilege-broker source lane
  - upstream implementation remains under Apache-2.0
- `eggie-admin/termux-x11`
  - default branch: `master`
  - Samsung X11 merge: `2147bd8fea9f865e7106ef3a94ad92652289ade4`
  - optional display/X11 lane using display `:1`

## Device trust lanes

### Stock Samsung / Secure Folder development

Preferred:

1. stock Samsung firmware
2. Developer Options enabled
3. USB or Wireless debugging enabled only when needed
4. Shizuku started using ADB / Wireless debugging
5. explicit per-app Shizuku authorization
6. Termux + Termux:Widget own localhost service control
7. YagniLauncher may act as an optional front door but never as the privilege broker
8. Termux:X11 remains optional display transport

Root and Sui are excluded from this trusted lane.

### Rooted laboratory Samsung

Root / Sui is a separate experimental target. It must not claim Secure Folder or Knox trust.

## Canonical local control plane

- AXS: `127.0.0.1:8767`
- TigerVNC: `127.0.0.1:5901`
- WebSocket bridge: `127.0.0.1:6080`
- Hydra cockpit: `127.0.0.1:8787`
- Ollama: `127.0.0.1:11434`

## Architecture rules

- Shizuku is optional and external to the APK dependency graph.
- Termux:X11 and the kiosk launcher are optional capabilities.
- Missing optional tools downgrade capability instead of breaking the ordinary build.
- Privileged actions must be typed and allow-listed.
- Never execute arbitrary model-authored shell commands.
- Keep localhost development services bound to loopback.
- Stop only processes owned by the Hydra supervisor/wrapper.
- Preserve upstream licenses and provenance in every source fork.
- No secrets, signing keys, API keys, or model weights belong in these integration manifests.

## Full mutation surface

The Samsung constellation now tracks:

- Vue/Godot Android build candidate
- Termux:Widget supervisor
- Shizuku privilege-broker contract
- Termux Samsung runtime/bootstrap contract
- Termux:X11 PID-owned display controller
- YagniLauncher typed kiosk actions
- read-only ADB/Shizuku diagnostics
- Secure Folder vs rooted-laboratory trust separation
- repository and commit provenance through the central SM-X400 full-stack manifest

This catalog stays documentation-only so future upstream Android FOSS updates remain straightforward to rebase.
