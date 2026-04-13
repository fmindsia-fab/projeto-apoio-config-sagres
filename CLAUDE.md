# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file SPA (`index.html`) — an internal support guide for the **Squalus Gestão** ERP system. Used by support teams to reference configuration fields with annotated screenshots. No build step, no dependencies, no server required. Open `index.html` directly in a browser.

## Architecture

Everything lives in `index.html` (~1550 lines), structured in three embedded blocks:

1. **`<style>`** — Full dark-theme CSS using CSS custom properties (`--bg-page`, `--azul-accent`, `--amarelo`, etc. defined in `:root`). Layout is sidebar (`#sidebar`, fixed 290px) + main content area.

2. **`<body>`** — Page sections as `<section class="page-section" id="...">`. Navigation is driven by `data-` attributes; sections are toggled visible/hidden by JS. Screenshots reference the `prints/` directory.

3. **`<script>`** (inline, end of body) — Handles:
   - **Navigation**: `showSection(id)` shows/hides `.page-section` elements; sidebar links and search use this.
   - **Screen modal**: `openScreenModal(imgSrc)` opens a full-screen image viewer (`#screen-modal`).
   - **Highlight overlay**: SVG-based overlay (`#modal-svg-overlay`) renders a semi-transparent mask with a cutout over a field area. Coordinates are percentage-based (`top,left,width,height` as % of image dimensions) stored in `data-coords` attributes on table rows.
   - **Calibration mode**: Two-click tool (`toggleCalibrate`) to pick new coordinates for a field highlight directly on the screenshot. Saves to `localStorage` keyed as `coords_<imgSrc>_<fieldName>`.

## Adding a New Configuration Section

1. Add a `<section class="page-section" id="cfg-XXXX" data-section-img="prints/XXXX.png">` block following the existing pattern (breadcrumb, `<h2>`, `screen-print` div, `note-box`, one or more `fields-card` divs with a `fields-table`).
2. Add the corresponding nav link in `#sidebar` inside the appropriate `.nav-section`.
3. Place the screenshot at `prints/XXXX.png`. The `onerror` handler on `<img>` shows a placeholder if the file is missing — so the section works without the image.
4. Field highlight coordinates go in `data-coords="top,left,width,height"` (all % values) on each `<tr>` that maps to a screen field.

## Field Type Tags

Use the existing tag classes consistently:
- `tag-sim` — S/N boolean fields
- `tag-nao` — explicitly disabled/not applicable
- `tag-opt` — selection/dropdown fields
- `tag-txt` — free-text fields
