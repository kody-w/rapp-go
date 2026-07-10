# rapp·go

[![rapp·go v2](https://img.shields.io/endpoint?url=https://kody-w.github.io/rapp-go/api/v1/badge.json)](https://kody-w.github.io/rapp-go/)

A quiet, no-backend field game where nearby weather becomes a living, content-verified creature.

- **Live app:** https://kody-w.github.io/rapp-go/
- **Deterministic demo:** https://kody-w.github.io/rapp-go/?demo=1&reset=1

## What was rebuilt

Version 2 is a from-scratch, standalone implementation. It keeps the original product idea—weather creatures, nearby places, timing-based catches, a local satchel, and an installable PWA—but removes every monorepo-relative dependency.

The new repository includes:

- a hand-rolled canvas slippy map with CARTO/OpenStreetMap tiles
- deterministic procedural 3D creatures derived from weather, time bucket, and coarse place cell
- real-time Three.js/WebGL geometry with perspective, flat-shaded meshes, dynamic lights, shadows, rotation, breathing, and articulated parts
- **151 original starting species** across twelve grounded body plans, each with a stable field-guide number and animation rig
- moment-derived individual traits—proportions, markings, finish, asymmetry, crest, tail, ears, gait, and a hallmark feature—so same-species catches are not clones
- a three-wobble catch model with vessel, offering, rarity, and flee modifiers
- public OpenStreetMap Overpass places with range checks, cooldowns, deterministic drops, and lures
- an IndexedDB field journal plus local-only satchel and preferences
- content-addressed creature links that are verified before import
- deterministic demo, fixed-coordinate, and live-geolocation modes
- service-worker offline shell caching and an installable web manifest
- unit and browser-level end-to-end coverage in CI

The deployed machine-readable field guide is available at `api/v1/species.json`.

## Privacy model

Exact GPS is used only in the browser for distance and map placement. Weather requests use the center of a precision-5 geohash; place requests use a precision-6 geohash cell. There is no app backend, account, telemetry, ad system, or server inventory. See [PRIVACY.md](PRIVACY.md).

## Run locally

Requires Node.js 20 or later.

```sh
npm install
npx playwright install chromium
npm run serve
```

Open http://127.0.0.1:4173/?demo=1&reset=1.

## Validate

```sh
npm test
npm run test:e2e
npm run build
```

`npm run check` runs all three stages. GitHub Actions repeats the same checks before deploying `dist/` to Pages.

## Test modes

| URL option | Behavior |
| --- | --- |
| `?demo=1` | Fixed weather, location, places, time, and guaranteed first demo catch |
| `?fix=LAT,LNG` | Use a desktop-friendly fixed coordinate after onboarding |
| `?t=EPOCH_MS` | Pin the 30-minute creature field bucket |
| `?reset=1` | Clear only rapp·go's local browser state before boot |

## Architecture

```text
src/
  app.js                  UI state machine and complete journey
  game/                   catch, economy, and spawn rules
  lib/                    geo, RNG, creature identity and sharing
  services/               local storage, weather, and place adapters
  ui/                     canvas map and procedural creature renderer
tests/
  unit/                   deterministic rule tests
  e2e/                    mobile and desktop browser journeys
```

Map tiles are © OpenStreetMap contributors and © CARTO. Public place data is © OpenStreetMap contributors. Code is available under the [MIT License](LICENSE).
