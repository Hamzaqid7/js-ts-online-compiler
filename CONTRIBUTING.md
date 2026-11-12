# Contributing

Thanks for your interest in improving JS/TS Online Compiler! This guide explains how to get set up and propose changes.

## Ground rules
- Be kind and follow the [Code of Conduct](CODE_OF_CONDUCT.md).
- Search [existing issues](../../issues) before opening a new one.
- Keep pull requests focused — one fix or feature per PR.

## Reporting bugs
Open an issue using the **Bug report** template and include:
- Browser and version, operating system
- Language mode (JS or TS)
- Steps to reproduce and a minimal code snippet
- Expected vs. actual behaviour, and any console errors

## Suggesting features
Use the **Feature request** template and describe the problem you're trying to solve, not just the solution.

## Development setup
The project has **no build step**. Everything is in `index.html`.

```bash
git clone https://github.com/Hamzaqid7/js-ts-online-compiler.git
cd js-ts-online-compiler
python -m http.server 8080      # or: npx serve .
```
Open <http://localhost:8080> and edit `index.html`; refresh to see changes.

Read [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) first — it explains the editor overlay, execution pipeline and sandbox.

## Pull request workflow
1. Fork the repo and create a branch: `git checkout -b feature/short-description`
2. Make your changes and test manually (see checklist below).
3. Update `README.md`, `docs/` and `CHANGELOG.md` (under **Unreleased**) if behaviour changes.
4. Commit using clear messages, e.g. `feat: add shareable links` / `fix: handle empty output copy`.
5. Push and open a PR using the template.

### Manual test checklist
- [ ] JavaScript and TypeScript both run the built-in examples
- [ ] A TypeScript syntax error shows a diagnostic and does not run
- [ ] `console.log/warn/error`, a thrown error and a rejected promise all appear in output
- [ ] Top-level `await` works
- [ ] Stop and Clear end a running timer-based script
- [ ] Open / Save work; tabs switch without losing cursor position
- [ ] Dark and light themes both look correct
- [ ] Divider drag, keyboard resize and double-click reset work
- [ ] Layout is usable on a narrow (mobile) viewport
- [ ] Reload restores code, theme and font size

## Code style
- Keep the app dependency-light and self-contained.
- Use 2-space indentation, semicolons and `const`/`let`.
- Use the existing CSS variables for any new colors so both themes work.
- Preserve accessibility: labels, `aria-*` attributes, keyboard operability, reduced-motion support.
- Any new CDN script must use a **pinned version**.

## License
By contributing you agree that your contributions are licensed under the [MIT License](LICENSE).
