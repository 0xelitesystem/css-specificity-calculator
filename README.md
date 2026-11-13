# CSS Specificity Calculator

Type any CSS selector and get its specificity as (a, b, c), with a plain-English breakdown of exactly what contributed. Switch to compare mode and it tells you which of two selectors wins a conflict and why. Runs entirely in your browser, no server, no tracking, no external dependencies.

**Live demo:** https://0xelitesystem.github.io/css-specificity-calculator/

## Live demo

https://0xelitesystem.github.io/css-specificity-calculator/

## Features

- Scores any selector as the three-column tuple (a, b, c): IDs, then classes / attributes / pseudo-classes, then elements / pseudo-elements.
- Per-token breakdown showing which column each part of the selector fell into and why.
- Handles the tricky cases:
  - `:where()` always contributes zero.
  - `:is()`, `:not()`, and `:has()` take the specificity of their most specific argument.
  - `:nth-child(... of S)` adds the specificity of the `of` selector.
  - Pseudo-elements (`::before`, `:first-line`, and the single-colon legacy forms) count as elements.
  - The universal selector `*` and combinators (`>`, `+`, `~`, descendant space) contribute nothing.
  - Attribute selectors count in the class column.
- Notes that inline `style="..."` outranks any selector, and that `!important` overrides specificity entirely (it is not part of the score).
- Compare mode: enter two selectors and see which wins, with the exact column that broke the tie, or that source order decides an exact tie.
- Clickable example presets covering the common and the tricky cases.
- Selector lists (comma-separated) are scored per selector, since a list has no single specificity.
- Light and dark themes, keyboard usable, live updates as you type.

## How it works

The selector is walked character by character. IDs increment column a; classes, attribute selectors, and pseudo-classes increment column b; type (element) selectors and pseudo-elements increment column c. Balanced parentheses and brackets are tracked so functional pseudo-classes like `:is()` and `:not()` and attribute selectors parse correctly. For `:is()`, `:not()`, and `:has()`, the tool recursively scores each comma-separated argument and adds the single most specific one. For `:where()` it adds nothing. Comparison sorts the two tuples column by column (a first, then b, then c).

## Use

1. Type a CSS selector, or click one of the example presets.
2. Read its specificity as (a, b, c) and the per-token breakdown of which column each part landed in.
3. Switch to compare mode and enter two selectors to see which one wins and which column decided it.

## Why this exists

When a style refuses to apply, the cause is often specificity, and the rules for `:is()`, `:not()`, `:has()` and `:where()` are easy to get wrong by hand. This tool scores the selector and shows its working. It is a single HTML file with no tracking and no network calls, and it is MIT licensed.

## Privacy

Everything runs client-side in your browser. The selectors you type never leave your machine. There are no network requests, no analytics, and no external dependencies. Open the page source or your browser network tab to confirm.

The one thing the page saves is your light or dark theme choice, written to `localStorage` under the key `theme` when you press the theme toggle. Clearing site data removes it.

## Run locally

```
git clone https://github.com/0xelitesystem/css-specificity-calculator
cd css-specificity-calculator
```

Then open `index.html` in any modern browser, or serve the folder with `python -m http.server` and visit http://localhost:8000/.

## Build

No build step. The whole tool is one `index.html` file with inline CSS and JavaScript, and there is nothing to install or compile.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT. Copyright RBL Industries LLC 2026.
