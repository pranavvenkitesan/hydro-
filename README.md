# hydroflowdrink — static offline copy

A self-contained static copy of the hydroflowdrink.com site (a Next.js app).
No build step, no server-side code — just static files. All paths are
**relative**, so it runs both at a domain root and under a subpath.

## Run locally

Any static file server works. From this directory:

```bash
python3 -m http.server 8765
# open http://localhost:8765/
```

Other options: `npx serve`, `php -S localhost:8765`, VS Code Live Server, etc.

> Open via `http://` — not by double-clicking `index.html`. A `file://` origin
> blocks the app (Next.js treats `file:` as an opaque origin and WebGL/asset
> loading fails).

## Deploy

Paths are relative, so it works at root **or** a subpath:

- **GitHub Pages (project site)** — `https://<user>.github.io/<repo>/`. Enable
  Pages → Deploy from branch → `main` / root. The subpath just works.
- **Netlify / Vercel / Cloudflare Pages** — drag-and-drop or connect the repo.
  Served at root, no config.
- **Custom domain / root** — copy the files to the web root.

## Layout

```
index.html              entry page
_next/static/           Next.js JS chunks + CSS
images/                 photos, mockups, card art
imageSequence/          300 webp frames (scroll-driven can animation)
models/brandedcan.glb   3D can model (Draco-compressed)
draco/                  local Draco decoder (wasm + js)
videos/water4.mp4       background video
audio/sodaopening.mp3   can-open SFX (see audio/CREDITS.txt)
fonts/                  brand fonts (at.woff, mono.ttf) + google/ (localized)
6649e26.../             marquee crypto-logo SVGs
px/nx/py/ny/pz/nz.png   cubemap env faces (reflections)
favicon.ico
```

## Substitutions (not from the original site)

The live site is missing or hotlinks some assets; these were filled in so this
copy is fully self-contained and works offline:

- **audio/sodaopening.mp3** — original is 404 on the live site and not archived.
  Replaced with a CC BY-SA 3.0 can-open sound. See `audio/CREDITS.txt`.
- **px/nx/py/ny/pz/nz.png** — cubemap reflection faces. 404 on the live site
  too; generated soft studio-gradient faces so reflections render.
- **fonts/google/** — Inter / Montserrat / Poppins / Roboto (latin subset) were
  hotlinked from Google Fonts; downloaded and localized.
- **draco/** — the GLB decoder was loaded from `gstatic.com`; vendored locally.
- **6649e26.../*.svg** — marquee logos were hotlinked from a Webflow CDN;
  downloaded locally.

## Notes

- The 3D can renders with WebGL — needs a GPU-capable browser (any normal
  desktop/mobile browser). Headless/no-GPU environments show an error overlay.
- The can-open sound plays on user interaction (rotate/click), not on load —
  browsers block autoplay until a gesture. This matches the original.
