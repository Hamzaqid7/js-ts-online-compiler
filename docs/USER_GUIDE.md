# User Guide

A complete walkthrough of the JS/TS Online Compiler interface.

## Contents
1. [Getting started](#getting-started)
2. [The header toolbar](#the-header-toolbar)
3. [Writing code](#writing-code)
4. [Running code](#running-code)
5. [Working with files and tabs](#working-with-files-and-tabs)
6. [Output panel](#output-panel)
7. [Customisation](#customisation)
8. [Keyboard shortcuts](#keyboard-shortcuts)
9. [Supported console methods](#supported-console-methods)
10. [Data stored in your browser](#data-stored-in-your-browser)
11. [Troubleshooting & FAQ](#troubleshooting--faq)

---

## Getting started

Open the app, wait for the short loading screen, and you'll see two panels: the **editor** on the left and the **output** on the right. The editor starts in JavaScript mode with a "Hello World" snippet (or your previously saved code). Press **▶ Run** to execute it.

## The header toolbar

| Control | What it does |
| --- | --- |
| **JavaScript / TypeScript** | Switches the language of the main tab (`main.js` / `main.ts`). Each language keeps its own saved code. |
| **A− / A+** | Decreases / increases the editor font size (14–28 px, steps of 2). |
| **Examples** | Opens a prompt listing built-in snippets for the current language. Enter the number to load one. |
| **Open** | Opens one or more `.js`, `.ts` or `.mjs` files from your computer as tabs. |
| **Save** | Downloads the active tab as a file (`Ctrl/Cmd + S`). |
| **Theme (sun/moon)** | Toggles dark and light mode. |
| **▶ Run** | Runs the active tab (`Ctrl/Cmd + Enter`). |
| **■ Stop** | Appears while a script is running; ends execution. |

## Writing code

The editor supports:

- **Syntax highlighting** for keywords, strings, numbers, comments and more
- **Line numbers** and a highlighted current line
- **Cursor position** (`Ln, Col`, plus the number of selected characters) in the tab bar
- **Auto-closing** of `()`, `[]`, `{}`, `""`, `''` and `` ` ``
- **Auto-indent** on Enter, with an extra level after `{`, `(` or `[`
- **Tab handling** — `Tab` inserts two spaces; with a multi-line selection it indents every line; `Shift + Tab` outdents
- **Comment toggling** — `Ctrl/Cmd + /` comments or uncomments the selected lines
- **Copy** and **Clear** buttons above the editor. Clear uses the browser's undo stack, so `Ctrl/Cmd + Z` restores your code.

## Running code

When you press **Run**:

1. **JavaScript** is executed as-is.
2. **TypeScript** is first transpiled to ES2020 with the TypeScript compiler. If there are *syntax* errors they are listed in the output as `file(line,col): message` and the code is not run.
3. The code is placed in a fresh, sandboxed `<iframe>` and executed as an **ES module**.

Because the code is a module:

- **Top-level `await` works** — no need to wrap in an `async` function.
- Code runs in **strict mode**.
- Variables are module-scoped, not global.

A timer in the output bar shows how long the sandbox took to load. For long-running or asynchronous code, output continues to appear until the script finishes or you press **Stop**.

### Reading input

`prompt()` shows the browser's native prompt dialog and then prints the question and your answer to the output panel. `alert()` prints its message to the output; `confirm()` prints its message and always returns `true`.

```js
const name = prompt("What's your name?");
console.log(`Hello, ${name}!`);
```

### Importing libraries

Since code runs as a browser module, you may be able to import ES modules from a CDN that supports it, for example:

```js
import confetti from "https://cdn.jsdelivr.net/npm/canvas-confetti/+esm";
```

Availability depends on the CDN's CORS headers and your network. Node-style imports (`import fs from "fs"`) will not work.

## Working with files and tabs

- Click **Open** and choose one or more files. Each opens in a new tab; re-opening a file with the same name replaces that tab's content.
- The tab's language is chosen by extension: `.ts` → TypeScript, everything else → JavaScript.
- Click a tab to switch; use its close button to remove it. The first tab (`main`) can't be closed.
- **Run executes only the active tab.** Tabs don't import from one another.
- Use **Save** to download the active tab. Extra tabs aren't auto-saved, so download anything you want to keep.

## Output panel

- Messages are color-coded by type: normal logs, info, warnings and errors look different.
- **Copy** copies all output as plain text; **Clear** empties the panel (and stops a running script).
- Objects, arrays, functions, `BigInt` and `Symbol` values are formatted into readable text. Circular references are handled safely.

## Customisation

| Setting | How to change | Remembered? |
| --- | --- | --- |
| Theme | Sun/moon button | Yes |
| Font size | A− / A+ | Yes |
| Panel width | Drag the divider, press `←`/`→` while it's focused, or double-click to reset | No |
| Language | JavaScript / TypeScript buttons | Code per language is remembered |

## Keyboard shortcuts

| Shortcut | Action |
| --- | --- |
| `Ctrl/Cmd + Enter` | Run |
| `Ctrl/Cmd + S` | Save active tab |
| `Ctrl/Cmd + /` | Toggle comment |
| `Tab` / `Shift + Tab` | Indent / outdent |
| `Ctrl/Cmd + Z` | Undo |
| `←` / `→` (divider focused) | Resize panels |

## Supported console methods

| Method | Behaviour |
| --- | --- |
| `console.log`, `console.debug` | Standard output |
| `console.info` | Info output |
| `console.warn` | Warning output |
| `console.error` | Error output |
| `console.table` | Printed as formatted data (not a drawn table) |
| `console.clear` | Clears the output panel |

Uncaught exceptions and unhandled promise rejections are also reported as errors.

## Data stored in your browser

The app uses `localStorage` for small preferences only. Nothing is sent to a server.

| Key | Contents |
| --- | --- |
| `theme` | `"dark"` or `"light"` |
| `fs` | Editor font size |
| `c_js` | Saved code for the JavaScript main tab |
| `c_ts` | Saved code for the TypeScript main tab |

Clear your site data in the browser settings to reset everything.

## Troubleshooting & FAQ

**"TypeScript compiler failed to load (check your connection)."**
The TypeScript compiler is loaded from a CDN. Check your internet connection or any ad/script blockers, then reload.

**My TypeScript has a type error but still runs.**
The app *transpiles* TypeScript; it doesn't perform full type-checking. Use your editor or `tsc` for strict type checks.

**The page froze after I ran a loop.**
A synchronous infinite loop blocks the browser thread, and **Stop** can't interrupt it. Reload the page. Your last saved code is restored on the main tab.

**`require` / `process` / `fs` is not defined.**
This is a browser environment, not Node.js.

**My code disappeared after switching language.**
Each language keeps its own saved main tab. Switch back to see it again.

**The page is stuck on the loading screen.**
The loader dismisses itself after a few seconds even if a CDN is slow. If it persists, check your network and reload.

**Does my code leave my computer?**
No. Compilation and execution happen locally in your browser. (Your own code can of course make network requests if you write it to.)
