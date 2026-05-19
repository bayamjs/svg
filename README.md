# SVG.js

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20282077.svg)](https://doi.org/10.5281/zenodo.20282077)
[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/bayamjs/svg)
[![Live Demo](https://img.shields.io/badge/demo-live%20preview-blueviolet.svg)](https://bayamjs.github.io/svg/)

A zero-dependency, JSON-driven SVG icon rendering engine for the web.

---

## Description

SVG.js maps icon keys to inline SVG paths through a flat JavaScript object. It injects icons directly into the DOM via a class-based pattern — no external font, no HTTP request, no build step required. Designed for low-bandwidth environments where external icon font dependencies are a liability.

---

## Key Features

- **Zero dependency** — pure vanilla JavaScript, no npm, no bundler, no build step
- **Single file** — all 60+ icon paths embedded in one `svg.js` file
- **Inline SVG injection** — icons rendered directly into the DOM via `svg.di()`
- **Class-based markup** — `<i class="di-{key}"></i>` convention, familiar to Bootstrap Icons users
- **CSS custom property theming** — colors via `--pColor`, `--sColor`, `--aColor`
- **Interactive gallery** — `index.html` with live search, 4 display modes, clipboard copy

---

## Prerequisites

No installation required. Just include two files in your HTML:

| File      | Role                                      |
|-----------|-------------------------------------------|
| `svg.js`  | Core engine — path dictionary + render API |
| `svg.css` | Base styles + CSS custom properties       |

**Browser support:** Any modern browser (Chrome, Firefox, Safari, Edge). No transpilation needed.

---

## Quick Start

### 1. Include the files

```html
<link rel="stylesheet" href="svg.css">
<script src="svg.js"></script>
```

### 2. Place an icon

```html
<i class="di-search"></i>
<i class="di-donat"></i>
<i class="di-github"></i>
```

### 3. Initialize

```html
<script>
  if (typeof svg !== 'undefined') svg.di();
</script>
```

That's it. Icons render inline as `<svg>` elements, fully styleable via CSS.

---

## Usage

### `svg.di()`

Scans the entire DOM for elements matching `.di-{key}` class names and injects the corresponding SVG path via `innerHTML`. Call once after DOM ready; call again after any dynamic content insertion.

```js
// inject all icons on page load
document.addEventListener('DOMContentLoaded', function () {
  svg.di();
});

// re-inject after dynamic content update
insertNewContent();
svg.di();
```

### `svg.icon(id)`

Returns a complete `<svg>` string for programmatic use.

```js
var markup = svg.icon('search');
// → '<svg class="svgicon" xmlns="..." viewBox="0 0 24 24"><path d="..."/></svg>'

document.getElementById('myTarget').innerHTML = svg.icon('search');
```

| Parameter | Type   | Default   | Description              |
|-----------|--------|-----------|--------------------------|
| `id`      | string | `'bayam'` | Any key from `svg.path`  |

### `svg.path`

Direct access to the icon path dictionary.

```js
console.log(svg.path.search);
// → "M20 11A1 1 0 002 11..."

// list all available icons
console.log(Object.keys(svg.path));
```

---

## Theming

Override CSS custom properties to match your brand:

```css
:root {
  --pColor: #00738e;   /* primary — icon stroke color   */
  --sColor: #00738e;   /* secondary — hover base         */
  --aColor: #DF8C43;   /* accent — interactive highlight */
}
```

Icons inherit `stroke` from `--pColor`. On hover, stroke transitions to `--aColor` with a dash animation.

---

## Available Icons

### UI & Navigation

| Key         | Description       | Key       | Description       |
|-------------|-------------------|-----------|-------------------|
| `menu`      | Hamburger menu    | `house`   | Home              |
| `search`    | Magnifier         | `person`  | User / profile    |
| `filter`    | Slider filter     | `eye`     | Visibility        |
| `threedots` | Vertical ellipsis | `geo`     | Location pin      |
| `scan`      | QR / barcode scan | `setting` | Settings gear     |
| `lock`      | Lock / security   | `bel`     | Notification bell |
| `calendar`  | Date picker       |           |                   |

### Actions

| Key        | Description    | Key      | Description |
|------------|----------------|----------|-------------|
| `upload`   | Upload         | `check`  | Checkmark   |
| `download` | Download       | `plus`   | Add / plus  |
| `save`     | Save           | `minus`  | Remove      |
| `pen`      | Edit           | `undo`   | Undo        |
| `trush`    | Delete / trash | `redo`   | Redo        |
| `printer`  | Print          | `camera` | Camera      |
| `link`     | Hyperlink      | `copy`   | Copy        |

### Content & Data

| Key        | Description       | Key        | Description      |
|------------|-------------------|------------|------------------|
| `file`     | Generic file      | `card`     | ID / credit card |
| `buku`     | Book              | `cart`     | Shopping cart    |
| `edu`      | Mortarboard       | `envelope` | Email            |
| `chart`    | Line chart        | `qrcode`   | QR code          |
| `code`     | Code / developer  | `web`      | Globe / website  |

### Social & Brand

| Key        | Key        | Key        | Key         |
|------------|------------|------------|-------------|
| `twitter`  | `x`        | `facebook` | `instagram` |
| `whatsapp` | `linkedin` | `youtube`  | `github`    |
| `discord`  | `arduino`  | `credly`   | `orcid`     |

### Ecosystem Identity

| Key       | Description                   |
|-----------|-------------------------------|
| `donat`   | DonatJS framework logo        |
| `bayam`   | BayamJS framework logo        |
| `ktupad`  | Ktupad platform logo          |
| `piawai`  | Piawai learning platform logo |
| `sismadi` | PT Sismadi Langit Solusi logo |
| `sls`     | SLS brand mark                |
| `ws`      | WS identifier                 |

---

## Adding Icons

Add a new entry to the `path` object in `svg.js`:

```js
var svg = {
  path: {
    // existing entries...
    myicon: `M12 2 L22 22 L2 22 Z`,
  }
};
```

All paths use a `24×24` viewBox coordinate space. The key becomes the CSS class: `di-myicon`.

---

## File Structure

```
svg/
├── svg.js        # Core engine — path dictionary + API
├── svg.css       # Base styles + CSS custom properties
├── index.html    # Interactive icon gallery
├── README.md     # This file
├── CITATION.cff  # Citation metadata (Zenodo / Google Scholar)
└── LICENSE       # MIT License
```

---

## How to Cite

If you use SVG.js in academic work, please cite it as:

```bibtex
@software{sismadi_svgjs_2024,
  author    = {Sismadi, Wawan},
  title     = {{SVG.js: A Lightweight JSON-Driven SVG Icon Rendering Engine}},
  year      = {2024},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.20282077},
  url       = {https://github.com/bayamjs/svg}
}
```

See [`CITATION.cff`](CITATION.cff) for full metadata including related works and references.

---

## License

MIT License © 2024 Wawan Sismadi / PT Sismadi Langit Solusi

---

## Author

**Wawan Sismadi**
NIDN: 0816087703 · SINTA ID: 6848496 · ORCID: [0009-0007-2685-5663](https://orcid.org/0009-0007-2685-5663)
Lecturer, Universitas IPWIJA · Doctoral Candidate, Universitas Ahmad Dahlan
Founder, PT Sismadi Langit Solusi · [sismadi.com](https://sismadi.com)
