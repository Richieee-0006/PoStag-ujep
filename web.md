# PoStag-ujep

Graphite + Warm Amber dark UserCSS theme and accessibility overhaul (WCAG 2.1 AA, Modern Web Guidance) for the UJEP IS/STAG university portal (`portal.ujep.cz`).

## Key Features
- **Separated Accent & Link Palette:** Neutral Graphite ramp with Warm Amber (`#dfb464`) UI accent (active tabs, sidebar, checkboxes, focus ring) and calm Verdigris-Teal (`#75c2c0`, 8.5:1+ contrast) reserved exclusively for clickable links.
- **WCAG 2.1 AA & Modern Web Guidance:** Verified 4.5:1+ text contrast (9:1+ links), 3.2:1+ input boundaries, `rem` typography, `min-block-size`, unified `appearance: none` radios/checkboxes, global `:focus-visible`, `forced-colors`, and `prefers-reduced-motion`.
- **Flexbox, Grid & Vector Icons:** Sticky 240px sidebar, 4px spacing scale, and 13 vector Lucide browse icons replacing empty legacy raster squares.
- **Schedule & Enrollment Overhaul:** Fixes Combined-mode column collapse, adds non-color type prefixes (`P·`/`C·`/`S·`/`Z·`), `tabular-nums`, and 16-color enrollment palettes.
- **Responsive Tables:** Converts dense data tables into card layouts on screens under `768px`.

## Tech Stack
- **Styling:** CSS3, UserCSS (`stylus.user.css`)
- **Extension:** Stylus (Firefox / LibreWolf / Chromium)
