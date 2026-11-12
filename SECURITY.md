# Security Policy

## How user code is executed
Code you type is run in an `<iframe>` with `sandbox="allow-scripts allow-modals"`. The sandbox does **not** include `allow-same-origin`, so executed code cannot access the host page's DOM, cookies or `localStorage`. Console output is passed back with `postMessage` and only accepted from the sandbox's own window.

Executed code **can** make outbound network requests and show modal dialogs, like any web page. **Do not paste secrets** (API keys, tokens, passwords) into the editor — the main tab is saved in your browser's `localStorage`.

## Supported versions
| Version | Supported |
| --- | --- |
| 1.0.x | ✅ |

## Reporting a vulnerability
Please **do not** open a public issue for security problems.

Email **hamzaaijaz41@gmail.com** with:
- A description of the issue and its impact
- Steps or a proof of concept to reproduce
- Affected browser(s) and version

You'll receive an acknowledgement as soon as possible, and we'll work with you on a fix and coordinated disclosure.

## Third-party dependencies
The app loads Bootstrap (jsDelivr), the TypeScript compiler (cdnjs) and Google Fonts at runtime. Versions are pinned. If you self-host or add dependencies, consider adding [Subresource Integrity](https://developer.mozilla.org/docs/Web/Security/Subresource_Integrity) hashes.
