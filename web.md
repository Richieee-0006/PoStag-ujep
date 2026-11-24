# PoStag-ujep

Dark UserCSS theme with a built-in **Stylus Theme Picker** (6 dark palettes + independent UI accent & link color selectors), WCAG 2.1 AA accessibility, and Modern Web Guidance architecture for the UJEP IS/STAG university portal (`portal.ujep.cz`).

## Key Features
- **Built-in Stylus Theme Picker (`@preprocessor uso`):** Switch live between 6 curated palettes (`Graphite Mono`, `Warm Obsidian`, `Graphite Sage`, `Nord Slate`, `Catppuccin Mocha v2`, `Tokyo Night`) plus independent UI accent and link color overrides directly inside Stylus (`⚙️`).
- **De-cluttered Chrome & Tables:** Flattened single-card portlets (no nested triple borders) and clean data tables with underlines scoped only to inline prose links (WCAG 1.4.1).
- **WCAG 2.1 AA & Modern Web Guidance:** Verified 4.5:1+ text contrast across all 6 palettes, 3.2:1+ input boundaries, `rem` typography, `min-block-size`, unified `appearance: none` radios/checkboxes, global `:focus-visible`, `forced-colors`, and `prefers-reduced-motion`.
- **Flexbox, Grid & Vector Icons:** Sticky 240px sidebar, 4px spacing scale, and 13 vector Lucide browse icons replacing empty legacy raster squares.
- **Schedule & Enrollment Overhaul:** Fixes Combined-mode column collapse, pins teacher footers to a consistent bottom baseline, adds non-color type prefixes (`P·`/`C·`/`S·`/`Z·`), `tabular-nums`, and 16-color enrollment palettes.
- **Responsive Tables:** Converts dense data tables into card layouts on screens under `768px`.

## Tech Stack
- **Styling:** CSS3, UserCSS (`stylus.user.css`, `@preprocessor uso`)
- **Extension:** Stylus (Firefox / LibreWolf / Chromium)
