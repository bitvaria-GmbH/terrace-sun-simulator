# Contributing

Thanks for your interest in the Terrassen-Simulator. Contributions of all
sizes are welcome — bug reports, fixes, and features.

## Reporting bugs / requesting features

Open an [issue](https://github.com/bitvaria-GmbH/terrace-sun-simulator/issues).
For bugs, please include:

- Browser + OS (and GPU, if it's a rendering/WebGL issue).
- What you did, what you expected, what happened instead.
- A screenshot or a shared scene URL (the **"Link kopieren"** button encodes the
  full scene into the URL) if relevant — it makes reproduction trivial.

## Running it locally

There is **no build step** and **no external network requests** — Three.js, the
fonts, and all textures are vendored. You only need a static file server, because
the local textures are blocked on `file://` by the browser's CORS policy:

```bash
git clone https://github.com/bitvaria-GmbH/terrace-sun-simulator.git
cd terrace-sun-simulator
python3 -m http.server 8000
# open http://localhost:8000/index.html
```

Any static server works (`npx serve`, etc.).

## Submitting changes

1. **Fork** the repo and create a branch off `main`.
2. Make your change. Keep the app self-contained — see *Architecture* below.
3. **Test by hand** in a browser: there is no automated test suite, so verify the
   scene renders, the wizard steps work, and the shadow/`% shaded` readout still
   behaves. Check both the orbit view and (on desktop) the first-person walk mode.
4. Open a **pull request** against `main` with a short description of what changed
   and why. Screenshots/GIFs for anything visual are very welcome.

## Architecture notes for contributors

The whole app is a single self-contained `index.html`. The solar math and shade
geometry are deliberately isolated as engine-agnostic **pure functions**
(`Solar`, `sombranoGeom`, `wareamaPlane`, `canopyOutline`, `clipPolyToRect`) so
the core could be ported off Three.js. When touching that logic, keep it pure —
no Three.js types or DOM access inside those functions.

Third-party code lives under `assets/vendor/` and `assets/fonts/` and is licensed
separately (see [`THIRD-PARTY-LICENSES.md`](THIRD-PARTY-LICENSES.md)) — please
don't modify vendored files; upgrade them wholesale instead.

## License

By contributing, you agree that your contributions are licensed under the
project's [MIT License](LICENSE).
