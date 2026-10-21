# FigCraft Web — Portable Package

FigCraft is a free, open-source **interface design tool** (similar to Figma) built by the
ArtCraft community in pure Rust. This package contains the **official prebuilt web version**
(v0.8.0) plus a small landing page, tuned to **work on phones** with touch gestures.

No build step, no server code — the whole thing is static files. Upload it anywhere.

---

## 1. Run it right now (30 seconds, no installs)

**Easiest — free hosting in your browser:**

1. Go to **https://app.netlify.com/drop**
2. Drag this whole folder onto the page
3. Done — you get a public `https://something.netlify.app` link you can open on your phone

**Other free options:**

| Host | How |
|---|---|
| Cloudflare Pages | dash.cloudflare.com → Workers & Pages → Create → Upload assets |
| GitHub Pages | Push the folder to a repo → Settings → Pages → deploy from branch |
| Any web server | Copy the folder's contents into your web root |

**Run on your own computer:**

```sh
cd figcraft-web-port
python3 -m http.server 8080
# open http://localhost:8080
```

> Note: opening `index.html` by double-click (file://) will **not** work — browsers block
> WebAssembly modules on local files. Use one of the methods above.

---

## 2. First steps in the editor (for Figma beginners)

When the editor opens you get a blank document ("Untitled"). The basics:

| What you want to do | How |
|---|---|
| Make a frame (an artboard/screen) | Press **F**, then drag on the canvas |
| Draw a rectangle / shape | Press **R** (or use the shape tools in the left rail) |
| Add text | Press **T**, click, then type |
| Move things around | Press **V** (move tool), click and drag |
| Change colors, corners, size | Select something → the right-hand design panel |
| Zoom | Mouse: **Ctrl/Cmd + scroll** · Touch: **pinch** |
| Pan the canvas | Mouse: hold **Space** and drag (or middle-button drag) · Touch: **two-finger drag** |
| Save your work | **Ctrl/Cmd + S** — your browser downloads a `.figcraft` file |
| Open a file | File → Open — your browser's file picker appears (accepts `.figcraft` and Figma `.fig`) |
| Export an image | Select a layer → Export in the right panel |

The layers panel (left) shows everything on the page, just like Figma. Auto layout,
components, styles and variables all live in the right-hand panel the same way Figma
arranges them — if you can use Figma, you already know FigCraft.

---

## 3. Using it on a phone

This port adds a **touch-gesture adapter** to the official web build:

- **One finger** — tap to select, drag to move (drag empty canvas to marquee-select)
- **Pinch with two fingers** — zoom in/out
- **Drag with two fingers** — pan the canvas
- Long-press may open the context menu (like right-click)

Tips:

- First launch downloads ~7 MB (the design engine) and caches it — later launches work
  **offline**.
- Typing text needs a keyboard; on phones the on-screen keyboard support is limited
  (upstream limitation) — a Bluetooth keyboard makes mobile editing comfortable.
- "Open standalone" opens the editor full-screen without the landing page.
- If rendering looks odd on an older phone, add `?webgl` to the editor URL to force the
  WebGL2 fallback.

---

## 4. What's in the folder

| Path | What it is |
|---|---|
| `index.html` | The landing page (mobile-first, no framework) |
| `figcraft/` | The editor: `index.html` (with the touch-gesture adapter), the WASM engine, wasm-bindgen glue, font licenses |
| `screenshots/` | Gallery images |
| `artcraft-mark.png`, `manifest.webmanifest` | Brand mark and PWA manifest |
| `nextjs-source/` | The Next.js 16 version of this site (`page.tsx`, `layout.tsx`, `editor-overlay.tsx`) if you prefer to run it as a Next.js app |

**Hosting requirements** (most hosts already do this): serve `.wasm` as
`application/wasm`, and enable gzip/brotli for `.wasm`/`.js`/`.html`.

---

## 5. Credits & license

- FigCraft engine: **storytold/figcraft** — https://github.com/storytold/figcraft · v0.8.0
  · dual-licensed MIT OR Apache-2.0 · a community project by ArtCraft (getartcraft.com)
- This port only wraps the official prebuilt web release, adds a touch-gesture adapter
  and a landing page. The WASM engine itself is unmodified.
