# Scriptographer Web

A dependency-free browser reinterpretation of Scriptographer: generative vector scripting, interactive mouse tools, layers, inspector, console, local projects, SVG/PNG export and a compact Scriptographer-inspired API.

## Deploy

No build step is required. Upload the entire folder to any static host (Netlify, Vercel, GitHub Pages, Cloudflare Pages, S3, traditional hosting) and open `index.html`.

For local testing:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080`.

## Core scripting API

Global objects exposed to scripts:

- `Point`, `Size`, `Rectangle`
- `RGBColor`, `GrayColor`
- `Path`, `Group`, `Layer`, `PointText`, `Raster`
- `Tool`, `Palette`, `Dialog`
- `document`, `tool`, `print()`
- helpers: `random()`, `map()`, `clear()`

### Mouse tool example

```js
tool.minDistance = 4;
var path;

tool.onMouseDown = function(event) {
  path = new Path();
  path.strokeColor = '#111';
};

tool.onMouseDrag = function(event) {
  path.add(event.point);
  path.smooth();
};
```

Tool events include `point`, `lastPoint`, `delta`, `middlePoint`, `count`, `item`, and modifier keys.

## Keyboard

- Cmd/Ctrl + Enter — run script
- Cmd/Ctrl + S — save project in browser
- Cmd/Ctrl + Z — undo
- Cmd/Ctrl + Shift + Z — redo
- V — select
- H — hand
- T — script tool
- P — pen
- R — rectangle
- O — ellipse
- X — text
- Delete/Backspace — delete selection

## Export

- Click **Export** — SVG
- Shift-click **Export** — PNG

## Browser limitations vs. original Illustrator plug-in

This web version reproduces the creative scripting model in an SVG document rather than controlling Adobe Illustrator itself. Native Illustrator-only APIs such as live access to Illustrator documents, plug-in-only pathfinder internals, native tracing, Illustrator fonts/styles, placed symbols, and Illustrator-specific raster effects are represented by browser equivalents where practical, but cannot be identical in a standalone website.

The exported SVG is editable in Adobe Illustrator.
