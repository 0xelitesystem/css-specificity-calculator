# CSS Specificity Calculator

Type any CSS selector and get its specificity as (a, b, c), with a plain-English breakdown of exactly what contributed. Switch to compare mode and it tells you which of two selectors wins a conflict and why. Runs entirely in your browser, no server, no tracking, no external dependencies.

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

## Privacy

Everything runs client-side in your browser. The selectors you type never leave your machine. There are no network requests, no analytics, and no external dependencies. Open the page source or your browser network tab to confirm.

## License

MIT. Copyright 0xelitesystem 2026.
