# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Academic project page for **Libra-VLA** (ACL 2026 paper: "Achieving Learning Equilibrium via Asynchronous Coarse-to-Fine Dual-System"). This is a static single-page site — one `index.html` file (~1200 lines) containing all HTML, CSS, and JavaScript inline.

## Architecture

The entire site lives in `index.html` with no build system, bundler, or dependencies beyond Google Fonts CDN (Inter, Noto Serif, JetBrains Mono).

### Structure within index.html

1. **CSS** (~250 lines) — CSS custom properties in `:root`, responsive layout via `container`/`container-wide` classes, table styling
2. **Header** — Title, author info, paper/arXiv buttons (currently placeholders)
3. **Animated Teaser Canvas** — JavaScript `<canvas>` drawing three paradigm comparison panels (discrete autoregressive, continuous diffusion, Libra-VLA hybrid). Uses `requestAnimationFrame` loop with Catmull-Rom interpolation. Auto-replays on a 9-second cycle (`CYCLE = 9000`)
4. **Interactive Balance SVG** — SVG balance beam with slider control. Demonstrates "Learning Equilibrium" concept — slider adjusts coarse bin granularity, tilts beam, updates weight blocks and status text
5. **Inverted-U SVG Chart** — Static SVG showing performance vs bin granularity
6. **Data Tables** — Ablation results (bin granularity, architectural components, asynchronous execution)
7. **Real-World Experiments** — Task images and SVG bar chart for success rates
8. **Method Section** — Architecture figure, paragraph descriptions
9. **Footer** — Citation placeholder

### Key interactive elements

- `#paradigm-canvas` — The animated teaser (panels a/b/c). Parameters: `W=900, H=310`, 6 coarse bins defined in `binBounds[]`, fine action curve in `curvePts[]`
- `#n-slider` — Balance beam slider (0-100, default 50). Drives tilt angle, weight block sizes, status labels, and explanation text
- `#beam-group` — SVG group that rotates for the balance visualization

### Static assets

All in `figs/` directory: `arch_v4.png`, `overall_v4.png`, `param_v3.png`, `realexp_v2.png`, `realtask.png`, `lbplus_tasks_v2.png`, `liberotasks.png`

## Development

Open `index.html` directly in a browser — no server required. For live reload during development, use any static file server (e.g., `python3 -m http.server`).

## Key Conventions

- All styling is inline `<style>` — no external CSS files
- All scripts are inline `<script>` IIFEs — no external JS files
- Color scheme uses CSS variables: `--accent: #5b21b6` (purple), with blue (`#60a5fa`) for Semantic Planner and purple (`#8b5cf6`) for Action Refiner throughout visualizations
- Tables use class `results` with `.best` for bold top values, `.second` for underlined, `.ours` for highlighted rows
- The paper is under review — author names are hidden, links are placeholder
