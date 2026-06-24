# Third-Party Licenses

This project bundles the following third-party components. Each is redistributed
under its own license; the project's own code is MIT (see `LICENSE`).

## three.js (r160)
- License: **MIT**
- Copyright © 2010-2023 three.js authors
- Bundled at: `assets/vendor/three/` (core build + the addon modules used)
- Full text: [`assets/vendor/three/LICENSE`](assets/vendor/three/LICENSE)
- Project: https://threejs.org

## Hanken Grotesk (webfont)
- License: **SIL Open Font License 1.1**
- Copyright 2021 The Hanken Grotesk Project Authors
- Bundled at: `assets/fonts/hanken-grotesk-*.woff2`
- Full text: [`assets/fonts/HankenGrotesk-OFL.txt`](assets/fonts/HankenGrotesk-OFL.txt)
- "Hanken Grotesk" is a Reserved Font Name under the OFL.

## DM Mono (webfont)
- License: **SIL Open Font License 1.1**
- Copyright 2020 The DM Mono Project Authors
- Bundled at: `assets/fonts/dm-mono-*.woff2`
- Full text: [`assets/fonts/DMMono-OFL.txt`](assets/fonts/DMMono-OFL.txt)
- "DM Mono" is a Reserved Font Name under the OFL.

## PBR textures
- License: **CC0 1.0 (public domain)** — no attribution required
- Source: [Poly Haven](https://polyhaven.com)
- Bundled at: `assets/textures/`

## Postal-code coordinates (DACH PLZ lookup)
- Data: **GeoNames** postal-code dumps for DE, AT, CH
- License: **Creative Commons Attribution 4.0 (CC BY 4.0)** — https://creativecommons.org/licenses/by/4.0/
- Source: https://www.geonames.org/ (https://download.geonames.org/export/zip/)
- Bundled at: `assets/data/plz-dach.json`
- Modifications: rows aggregated to one centroid (mean lat/lon) per postal code; coordinates rounded to 4 decimals.

## Lawn texture
- Generated procedurally at runtime in `index.html` — no bundled asset, no third-party license.
