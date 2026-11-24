# PoStag-ujep

Graphite + Cobalt dark UserCSS theme and accessibility overhaul (WCAG 2.1 AA) for the UJEP IS/STAG university portal (`portal.ujep.cz`).

## Key Features
- **Quiet Graphite + Cobalt Theme:** Replaces legacy light surfaces, inline styles, Bootstrap 5, Chosen.js, jQuery UI, and qTip with a neutral Graphite ramp and single Cobalt accent.
- **WCAG 2.1 AA Accessibility:** Verified 4.5:1+ text contrast, 3:1+ input boundaries, underlined prose links, global `:focus-visible`, `forced-colors`, and `prefers-reduced-motion`.
- **Flexbox & Grid Layout:** Converts legacy nested table layouts into Flexbox/CSS Grid with a sticky 240px sidebar and 4px spacing scale.
- **Schedule & Enrollment Overhaul:** Fixes Combined-mode column collapse, adds non-color type prefixes (`P·`/`C·`/`S·`/`Z·`), `tabular-nums`, and 16-color enrollment palettes.
- **Responsive Tables:** Converts dense data tables into card layouts on screens under `768px`.

## Tech Stack
- **Styling:** CSS3, UserCSS (`stylus.user.css`)
- **Extension:** Stylus (Firefox / LibreWolf / Chromium)
