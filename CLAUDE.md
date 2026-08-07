# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A HACS (Home Assistant Community Store) Lovelace custom card for monitoring and controlling a
Rinnai RU199iN tankless water heater via the [rinnaicontrolr-ha](https://github.com/explosivo22/rinnaicontrolr-ha)
integration. The entire dashboard — markup, styles, and logic — is a single static, dependency-free
HTML file: `rinnai-dashboard.html`. There is no build system, package manager, bundler, linter, or
test suite; there is nothing to install and nothing to compile.

## Development workflow

There are no build/lint/test commands — this repo has no `package.json` or CI config. The workflow is:

1. Edit `rinnai-dashboard.html` directly.
2. Open the file directly in a browser to iterate. Outside of Home Assistant it auto-detects it's
   not embedded (see "Demo mode" below) and runs on simulated, randomly-changing sensor data — no HA
   instance is required to see the UI and animations work.
3. To verify against real data, copy the file into a Home Assistant instance's `www/` folder and
   embed it in a dashboard as an iframe card (see README.md `Configuration` section), or use HA's
   iframe card pointed at the file over a local dev server.
4. Releases are distributed through HACS, which requires a tagged GitHub release (tag must start
   with `v`, e.g. `v1.1.0`) — HACS will not pick up changes without one. Follow semantic versioning
   (patch for fixes, minor for new features, major for breaking changes). `GITHUB-UPDATE-GUIDE.md`
   documents the full release checklist (update file, update README/version badge, tag, publish
   release) if you're walking a user through cutting a release.

## Architecture

Everything lives in `rinnai-dashboard.html`, organized top to bottom as:

- **`<style>`** — all CSS, including keyframe animations for the water-tank visualizer, flow
  arrows, heating glow, and status pulse.
- **Markup** — a `.dashboard` grid of `.card` elements (temperature, flow rate, pump status,
  burner/heating status, fan diagnostics) plus a "Controls" section (temperature +/- stepper,
  recirculation start/stop with a duration input).
- **`<script>`** — all behavior, structured around a few key pieces:
  - **`ENTITY_MAP`** — the single source of truth mapping internal keys (e.g. `outletTemp`,
    `pumpRunning`) to Home Assistant entity IDs (e.g. `sensor.rinnai_outlet_temperature`). This is
    the block users edit when their entity IDs differ from the defaults; it's called out in the
    file with a banner comment. Any new sensor/entity wired into the dashboard should be added here
    first.
  - **`updateDashboard(data)`** — the single render function. Every UI update (temperatures, flow
    progress bar, pump/heating status colors and card backgrounds, the animated water-tank
    visualizer, the overall status badge, metric counters, control button states) flows through
    this one function applied to a plain `data` object keyed the same as `ENTITY_MAP`. When adding
    a new displayed value, extend this function and the corresponding DOM element/id, not a
    separate ad hoc updater.
  - **HA integration vs. demo mode** — `isHomeAssistant()` checks for `window.hassConnection` /
    `window.parent.hassConnection` to detect whether the file is running embedded in Home Assistant
    (as an iframe card) or standalone:
    - **In HA:** subscribes to `state_changed` events for every entity in `ENTITY_MAP`, and on each
      change reads current entity states via `hass.states` and calls `updateDashboard(data)`.
    - **Standalone (demo mode):** seeds a local `demoData` object and mutates it on a
      `setInterval`, randomly toggling pump/heating and ramping temperature toward target, calling
      `updateDashboard(demoData)` each tick. This is what makes the file previewable without any
      Home Assistant backend.
  - **Interactive controls** — `adjustTemperature()`/`setTemperature()` and
    `toggleRecirculation()` call `hass.callService(...)` against real HA services
    (`water_heater.set_temperature`, `rinnai.start_recirculation`, `switch.turn_off`) when embedded
    in HA, and fall back to a simulated response (mutating `sensors`/`demoData` and calling
    `showStatus(..., 'info')`) in demo mode. Temperature is clamped to 100–140°F and recirculation
    duration to 5–60 minutes in the UI itself — there is no server-side validation, so keep any new
    control's bounds enforced client-side here too.

## Supporting files

- `hacs.json` — HACS manifest; `filename` must match the actual dashboard file, `content_in_root: false`.
- `README.md` — user-facing install/config/troubleshooting instructions (HACS vs. manual install
  paths, entity name verification, iframe card YAML, customization instructions).
- `info.md` — short description HACS renders in its store listing.
- `INTERACTIVE-FEATURES.md` — detailed reference for the temperature/recirculation controls (exact
  service calls and payloads, safety limits, demo-mode behavior).
- `INSTALLATION-PATHS.md` — reference for where HACS vs. manual installs place the file on disk
  (`/config/www/community/rinnai-dashboard/` vs `/config/www/`) and the corresponding iframe URLs.
- `example-configuration.yaml` — optional Home Assistant `template` sensors/`automation` snippets
  users can add to their own `configuration.yaml` for derived stats (temperature rise, pump
  efficiency) and alerts; not consumed by the dashboard itself.
- `GITHUB-UPLOAD-GUIDE.md` / `GITHUB-UPDATE-GUIDE.md` — step-by-step guides (web UI, git CLI, GitHub
  Desktop) for publishing this repo and cutting new HACS releases; consult these when asked to help
  with the release process rather than re-deriving release steps from scratch.

## Conventions

- Keep the dashboard a single self-contained file with zero external dependencies (no CDN scripts,
  no build step) — this is a stated project goal ("Zero Dependencies" in README.md), not an
  accident.
- Entity IDs referenced in code/docs follow the `sensor.rinnai_*` / `binary_sensor.rinnai_*` /
  `water_heater.rinnai_water_heater` naming from the rinnaicontrolr-ha integration; when adding a
  new entity, document it in both `ENTITY_MAP` and README's entity list so users can reconcile
  against their own HA instance.
- Any new sensor/metric should have a sensible hardcoded fallback value in `updateDashboard`
  (matching the existing pattern of `parseFloat(data.x) || <default>`) so demo mode and partially
  configured HA setups both render something reasonable instead of blank/`NaN`.
