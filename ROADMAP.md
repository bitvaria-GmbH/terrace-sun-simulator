# Terrassen-Simulator 3D — Roadmap: Full Scene Configuration

## How to run
- Served over HTTP (required — textures are local, `file://` blocks them via CORS):
  ```
  cd terrace-sun-pro && python3 -m http.server 8000
  ```
  Open **http://localhost:8000/index.html** (normal Cmd+R reload works).
- Single file: `index.html`. All assets are vendored locally (zero external requests): textures `assets/textures/<mat>/{diff,nor,rough}.jpg` (CC0 Poly Haven, 1K), Three.js `assets/vendor/three/`, fonts `assets/fonts/`. The chair and lawn are generated procedurally.

## Current state (done)
- Sun model (NOAA) with **settable location** (presets + lat/lon/UTC/DST), settable terrace W×D.
- Real **self-hosted PBR** materials; **library**: wall (Weiß/Grau/Klinker/Holz/Anthrazit), surface (Fliesen/Holz/Beton/Naturstein/WPC).
- Products: Schirm, Segel, **Ampelschirm** (ex-Sombrano, rund/eckig), **Markise** (ex-Warema); anthracite fabric.
- **Granular furniture**: Tisch on/off + size, Stühle on/off, Sonnenliegen ±N, Pflanzkübel ±N.
- Shadows + all-day Schattenspur (fat lines); FPS (1.68 m eye) + Orbit; quality toggle.
- House width **fixed** (no longer grows with terrace).
- Engine-agnostic core (`Solar`, `sombranoGeom`, `wareamaPlane`, `canopyOutline`) — Unreal-portable seam.

## Full Scene Configuration — SHIPPED (2026-06-23)

### Phase 1 — Multi-step wizard panel ✓
- 6-step stepper (clickable dots + Zurück/Weiter + counter): **1 Standort → 2 Terrasse (Maße+Belag+Ausrichtung) → 3 Wände → 4 Sonnenschutz → 5 Ausstattung → 6 Sonne & Ansicht**.
- One step visible at a time (`.step[data-step]` + `showStep(n)`). Terrasse intentionally placed before Wände (size the slab, then place walls on its edges). Dots are clickable so time (step 6) stays one click away.

### Phase 2 — Per-wall configuration + placement ✓
- `S.walls = {left,right,front}`, each: **on, material (library), height (1.4–3 m), length, offset**. Cards generated in `buildWallControls()`; sliders collapse when the wall is off.
- Back wall = the house (fixed footprint, material via the Hauswand select). Does NOT scale with the terrace.
- `buildSideWalls()` clones material **and** textures per wall (`wallMatInstance`) so tiling is independent of the house; disposed on rebuild to avoid leaks.
- `clampPlayer` collides with enabled side walls.

### Phase 3 — Polish ✓
- **Save/load**: silent localStorage autosave on every panel change; "Link kopieren" writes the full config to the URL hash on demand; "Zurücksetzen" clears + reloads. Hash takes precedence over localStorage on load.
- **New objects**: Grill, Outdoor-Teppich, Beistelltisch (Extras group in Ausstattung).
- **"Terrasse beschattet" % readout**: Sutherland-Hodgman clip of the projected canopy polygon against the terrace rect + shoelace area (in the engine-agnostic core). Live with sun position.

### Deferred (not user-facing)
- Productionize assets: grass photo + SheenChair.glb still load from the jsdelivr CDN. For an offline/live-site embed, self-host them too (textures already self-hosted). SheenChair is a generic sample, not patio furniture — real product CAD needs an artist/paid asset.
- "Both products shadow compare" (compare two sun-protection options at once).

## Known constraints / honest notes
- Must be **served** (HTTP), not `file://` — local textures + glTF need it.
- Assets currently mix self-hosted (textures) + CDN (grass photo, SheenChair.glb). For the live site, self-host the grass + chair too.
- SheenChair is a generic sample model, not patio furniture; real product CAD would need an artist/paid asset.
- Headless `--use-angle=metal` renders ignore `file://` CORS — always verify over `http://localhost` to match the real browser.
