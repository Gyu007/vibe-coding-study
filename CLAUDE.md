# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

This is a static, framework-free multi-page HTML/CSS site built for a "vibe coding" study group (바이브 코딩 스터디). There is no build system, package manager, or test suite — the site runs directly in a browser.

## Language

All conversation and commit messages must be written in Korean.

## Running the site

Open any HTML file directly in a browser. No install or build step is required.

```bash
# Windows
start index.html
```

## Structure

- `index.html`, `about.html`, `contact.html` — the three pages. Each repeats the same `<header>`/`nav`/`footer` markup independently (no templating), so navigation or layout changes must be applied to all three files by hand.
- `css/style.css` — single shared stylesheet for all pages, using CSS custom properties (`--color-*`, `--max-width`) defined in `:root` for theming.
- `contact.html` has a `<form class="contact-form">` with no submit handler — it is a static mockup only.

## Known issue

`README.md` currently contains unresolved Git merge-conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) despite a prior commit claiming to fix this. If asked to touch `README.md`, resolve the conflict rather than editing around it.
