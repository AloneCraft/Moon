# Moon

A streaming demo: the Moon's height and color data are fetched over HTTP Range requests and refined from the whole globe down to the ground (a scripted orbit of about 3 minutes, from 5,000 km to 2 m).

- Demo: <https://alonecraft.github.io/Moon/WebGPU/index.html> (WebGPU is required: recent desktop Chrome or Edge)
- Data: `MoonPacks/` (12 files, 31 MB: 6 cube faces of height, 6 of color)
- Player: `WebGPU/` (Unity 6000.6.6f1, WebGPU only, Brotli with the JavaScript decompression fallback; the data is requested from `../MoonPacks/`)
- Checksums and sizes: `manifest.json`. Credits: `NOTICE.md`.

## What to look for

- The HUD (top left) shows the data that has arrived: resident height tiles, color tiles on the GPU, downloaded MB, number of requests, requests merged into one Range, and cache hits.
- During a first run the whole orbit downloads about 12 MB in about 850 requests (all `206 Partial Content`). Reload the page and fly again: the browser's IndexedDB cache serves the data, so the requests drop to the pack headers only.
- The `Slow network` button is available only when the build is configured with a simulated connection; it is off in this build.

## URL options (for experiments)

- `?moon-packs=<url>`: load the packs from another folder (must send CORS headers and support Range).
- `?moon-lane=1`: add `?omni-lane=N` to the requests so that a browser does not serialize concurrent Range requests to the same URL.
- `?moon-pixels=<1..64>`: target pixel size of a cell (larger is coarser).

## Notes

- The player was built from a working tree of an unreleased project, so there is no source in this repository.
- This is a static site served by GitHub Pages from the `main` branch root.
