<div align="center">

# `</>` JS/TS Online Compiler

**A fast, zero-install JavaScript & TypeScript playground that runs entirely in your browser.**

[![License: MIT](https://img.shields.io/badge/License-MIT-7c3aed.svg)](LICENSE)
![Version](https://img.shields.io/badge/version-1.0.4-5b8cff)
![No build step](https://img.shields.io/badge/build-none-4cc27f)
![TypeScript](https://img.shields.io/badge/TypeScript-5.4.5-3178c6?logo=typescript&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3.3-7952b3?logo=bootstrap&logoColor=white)

[Live Demo](#live-demo) · [Features](#features) · [Quick Start](#quick-start) · [User Guide](docs/USER_GUIDE.md) · [Architecture](docs/ARCHITECTURE.md) · [Contributing](CONTRIBUTING.md)

</div>

---

## Overview

**JS/TS Online Compiler** is a single-file web application for writing, running and experimenting with JavaScript and TypeScript. There is no server, no bundler and no `npm install` — open `index.html` and start coding. Your code is executed in a sandboxed `<iframe>` and the output (including errors) streams into a built-in console panel.

> **Note:** Code runs in *your browser's* JavaScript engine, not in Node.js. Browser globals (`window`, `document`, `fetch`, …) are available; Node APIs (`fs`, `require`, `process`, …) are not.

## Live Demo

Once you deploy to GitHub Pages (see [Deployment](#deployment)), your demo will be available at:

```
https://hamzaqid7.github.io/js-ts-online-compiler/
```

Replace this section with the real link and add a screenshot or GIF, e.g. `![Screenshot](docs/screenshot.png)`.

## Features

### Editor
- **JavaScript & TypeScript** modes with one-click switching
- **Syntax highlighting**, line numbers, active-line highlight and live `Ln / Col` indicator
- **Smart editing** — auto-closing brackets/quotes, auto-indent, Tab / Shift+Tab indentation, comment toggling
- **Multiple files** — open several `.js`, `.ts` or `.mjs` files as tabs
- **Adjustable font size** (14–28 px), remembered between visits
- **Auto-save** — your scratch code is restored on your next visit
- **Undo-friendly** Clear button (`Ctrl/Cmd + Z` brings your code back)

### Execution & Output
- **Instant run** with `Ctrl/Cmd + Enter`
- **TypeScript transpilation** in-browser using the official TypeScript compiler (targets ES2020)
- **Top-level `await`** and ES module syntax supported
- **Console capture** for `log`, `info`, `warn`, `error`, `debug`, `table` and `clear`, with color-coded output
- **Uncaught errors & unhandled promise rejections** are reported in the output panel
- **`prompt()`, `alert()` and `confirm()`** are supported and echoed to the console
- **Stop** button to terminate a running script
- **Copy / Clear** controls for output

### Interface
- **Dark & light themes** (dark by default, choice is remembered)
- **Resizable split view** — drag the divider, use arrow keys, or double-click to reset
- **Built-in examples** for both languages
- **Responsive**, accessible (ARIA labels, keyboard-operable divider) and respects `prefers-reduced-motion`
- Animated loading screen and subtle "blueprint grid" background

## Quick Start

### Option 1 — Open the file
```bash
git clone https://github.com/Hamzaqid7/js-ts-online-compiler.git
cd js-ts-online-compiler
# then just open index.html in your browser
```

### Option 2 — Serve it locally (recommended)
Any static server works:

```bash
# Python
python -m http.server 8080

# Node.js
npx serve .

# VS Code: install the "Live Server" extension and click "Go Live"
```
Then visit <http://localhost:8080>.

### Requirements
- A modern browser (Chrome, Edge, Firefox, Safari — current versions)
- An **internet connection** on first load for the CDN-hosted dependencies (see [Tech Stack](#tech-stack)). JavaScript mode still works if the TypeScript compiler fails to load; TypeScript mode needs it.

## Usage

1. Choose **JavaScript** or **TypeScript** in the header.
2. Write code, or pick a snippet from **Examples**.
3. Press **▶ Run** (or `Ctrl/Cmd + Enter`).
4. Read the result in the **Output** panel.

```ts
// TypeScript example
interface User { id: number; name: string; email?: string }

const users: User[] = [{ id: 1, name: "Ada" }, { id: 2, name: "Linus", email: "l@x.org" }];
for (const u of users) console.log(u.id, u.name, u.email ?? "no email");
```

### Keyboard Shortcuts

| Shortcut | Action |
| --- | --- |
| `Ctrl/Cmd` + `Enter` | Run code |
| `Ctrl/Cmd` + `S` | Save current file to disk |
| `Ctrl/Cmd` + `/` | Toggle line comment |
| `Tab` / `Shift` + `Tab` | Indent / outdent (works on multi-line selections) |
| `Ctrl/Cmd` + `Z` | Undo (also restores a cleared editor) |
| `←` / `→` on the divider | Resize panels |

See the full [User Guide](docs/USER_GUIDE.md) for more.

## Tech Stack

| Purpose | Technology |
| --- | --- |
| App | Vanilla HTML, CSS and JavaScript (single file, no build) |
| TypeScript compilation | [TypeScript 5.4.5](https://www.typescriptlang.org/) via cdnjs |
| UI framework | [Bootstrap 5.3.3](https://getbootstrap.com/) (CSS) via jsDelivr |
| Font | [Montserrat](https://fonts.google.com/specimen/Montserrat) via Google Fonts |
| Code execution | Sandboxed `<iframe>` + `postMessage` |
| Background effect | HTML5 Canvas |

## Project Structure

```
js-ts-online-compiler/
├── index.html                 # The entire application
├── README.md
├── LICENSE
├── CHANGELOG.md
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── SECURITY.md
├── docs/
│   ├── USER_GUIDE.md          # End-user documentation
│   └── ARCHITECTURE.md        # How the app works internally
└── .github/
    ├── ISSUE_TEMPLATE/        # Bug report & feature request forms
    ├── workflows/pages.yml    # GitHub Pages deployment
    └── PULL_REQUEST_TEMPLATE.md
```

## Deployment

### GitHub Pages (included workflow)
1. Push this repository to GitHub.
2. Go to **Settings → Pages** and set **Source** to **GitHub Actions**.
3. Push to `main` — the workflow in `.github/workflows/pages.yml` publishes the site.

Because the app is a static file, it also deploys as-is to Netlify, Vercel, Cloudflare Pages or any static host.

## Limitations

- **TypeScript is transpiled, not type-checked.** Syntax errors are reported; type errors (e.g. assigning a `string` to a `number`) are not.
- **Not Node.js.** No `require`, `fs`, `process`, etc. Code runs as a browser ES module.
- **Files don't import each other.** Tabs are separate; **Run** executes the active tab only.
- **Infinite synchronous loops** (`while(true){}`) can freeze the browser tab, and **Stop** cannot interrupt them — reload the page.
- Only the primary (`main`) tab is auto-saved; additional tabs live in memory until you **Save** them.

See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md#known-issues--improvement-ideas) for known issues and ideas.

## Security

User code runs in an iframe with `sandbox="allow-scripts allow-modals"` (no `allow-same-origin`), so it cannot read the host page's `localStorage` or DOM. It can still make network requests like any web page. See [SECURITY.md](SECURITY.md).

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) and our [Code of Conduct](CODE_OF_CONDUCT.md) first.

## Changelog

See [CHANGELOG.md](CHANGELOG.md).

## License

Released under the [MIT License](LICENSE).

## Author

**Hamza Aijaz Qidwai** — WordPress & Web Developer, Karachi, Pakistan
[GitHub](https://github.com/Hamzaqid7) · [LinkedIn](https://www.linkedin.com/in/hamzaqidwai-wordpress-dev)

---

<div align="center">If you find this project useful, please consider giving it a ⭐</div>
