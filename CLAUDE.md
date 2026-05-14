# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A collection of YouTube video companion pages — interactive, slide-deck-style HTML presentations authored by Yar Malik. Each subdirectory is one video's content:

- `claude-vs-gpt/` — "Anthropic Just Passed OpenAI" video (3 sections)
- `hermes-agent/` — "Hermes Agent + Owl Alpha" video (4 sections)

Deployed automatically to GitHub Pages on every push to `master` via `.github/workflows/static.yml`.

## Architecture pattern

Every video directory follows the same two-layer structure:

**Shell (`index.html`)** — the interactive presenter UI. Contains:
- A `screens[]` array with one entry per section: `{ title, file, url, beat, notes }`
- An iframe that loads each section file and CSS-scales it to fit the viewport (target: 1280×720)
- A sidebar with section list, a topbar with navigation buttons, and a statusbar
- A **Creator Panel** (hidden overlay, toggle with `C` key or bottom-right button) showing per-section talking points (`beat`) and bullet `notes` for use while recording

**Section files (`01_*.html`, `02_*.html`, …)** — full standalone HTML pages with all CSS inlined. They are loaded into the shell's iframe. No JavaScript in section files; all interaction is in `index.html`.

## Conventions

- **No build step.** Open any `index.html` directly in a browser; works without a local server. GitHub Pages serves the repo root.
- **No external dependencies** beyond Google Fonts (`JetBrains Mono`). All CSS and JS are inline.
- **Color themes** differ per video: `hermes-agent` uses green (`#10a37f`), `claude-vs-gpt` uses orange (`#f59e0b`). CSS custom properties (`--green`, `--orange`, etc.) control the theme.
- **Section numbering** is zero-based in JS (`go(0)` = section 1) but display uses 1-based (`01`, `02`, …).
- **Keyboard shortcuts** (defined at the bottom of each `index.html`): `←→` navigate, number keys jump to section, `C` toggle creator panel, `Escape` return to overview, `F` fullscreen iframe.

## Adding a new video

1. Create a new subdirectory.
2. Copy the `index.html` from an existing video and update the `screens[]` array, color theme variables, and branding text.
3. Add section files named `01_*.html`, `02_*.html`, … as standalone full-page HTML with inline CSS matching the theme.
4. Push to `master` — GitHub Pages deploys automatically.

## Adding a section to an existing video

1. Create the new `0N_*.html` section file.
2. Add a corresponding entry to the `screens[]` array in that video's `index.html`.
3. Update sidebar stats or any hardcoded section-count references (e.g., `'/04'` in `stSec` display strings).
