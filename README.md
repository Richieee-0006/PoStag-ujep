# PoStag-ujep

[![Target](https://img.shields.io/badge/target-portal.ujep.cz-dfb464?style=flat-square)](https://portal.ujep.cz/)
[![Palette](https://img.shields.io/badge/palette-Graphite_%2B_Warm_Amber_v2.1-19191c?style=flat-square)](#barevná-paleta)
[![WCAG](https://img.shields.io/badge/a11y-WCAG_2.1_AA-52c48c?style=flat-square)](#přehled-úprav)
[![Stylus](https://img.shields.io/badge/extension-Stylus-a8a8b2?style=flat-square)](https://add0n.com/stylus.html)

Klidný tmavý userstyle (Graphite + Warm Amber, WCAG 2.1 AA, Modern Web Guidance) a modernizace rozhraní pro portál **IS/STAG na UJEP** (`portal.ujep.cz`).

## Přehled úprav

| Oblast | Změny |
| :--- | :--- |
| **Vzhled (Unslop v2.1)** | Neutrální grafitová škála bez modrého/fialového oslnění, teplý jantarový akcent (`#dfb464`) vyhrazený primárně odkazům a off-white primární akce. |
| **Přístupnost & Modern Web** | Kontrasty textu ≥ 4.5 : 1 (odkazy > 9 : 1), okraje vstupů ≥ 3.2 : 1, `rem` typografie, `min-block-size`, sjednocené `appearance: none` radio/checkbox prvky, `:focus-visible`, `forced-colors` a `prefers-reduced-motion`. |
| **Layout & Prohlížení** | Flexbox / CSS Grid, sticky boční panel (240 px), 4px mřížka a sada 13 vektorových Lucide ikon v rozcestníku Prohlížení místo prázdných bílých dlaždic. |
| **Rozvrh** | Opravený výpočet šířek v režimu *Combined*, sjednocená 4řádková levá hierarchie štítků (`P·`/`C·`/`S·`/`Z·` časy, předmět, učebna, obsazenost + vyučující) a `tabular-nums`. |
| **Předzápis & Tabulky** | 16barevná paleta akcí, zebra řádkování, stavy plateb, výsledků studia, žádostí (`S048`) a konzultací (`S110`). |
| **Responzivita** | Přizpůsobení pro menší monitory (`< 1200px`) a transformace tabulek na karty pro mobily (`< 768px`). |

## Barevná paleta

Styl využívá nativní CSS proměnné definované v `:root`:

| Proměnná | Hex | Použití |
| :--- | :--- | :--- |
| `--s-crust` | `#0f0f11` | Hlavička, záhlaví tabulek a portletů, vstupy |
| `--s-mantle` | `#141416` | Hlavní pozadí stránky a kontejnerů |
| `--s-base` | `#19191c` | Pozadí portletů, karet a modálních oken |
| `--s-s0` / `--s-s1` | `#2a2a2e` / `#64646d` | Zvýšené povrchy, jemné linky a 3.2:1 okraje vstupů |
| `--s-txt` / `--s-sub1` / `--s-ov` | `#ededef` / `#a8a8b2` / `#90909a` | Tři úrovně textu (primární, sekundární, meta) |
| `--s-blue` | `#dfb464` | Teplý jantarový akcent odkazů, aktivních stavů a `:focus-visible` |
| `--s-green` / `--s-yellow` / `--s-red` | `#52c48c` / `#e5c158` / `#f0686c` | Tlumené sémantické barvy pro stavy, notifikace a platby |

## Instalace

1. Nainstaluj rozšíření **Stylus** pro [Firefox](https://addons.mozilla.org/cs/firefox/addon/styl-us/) nebo [Chromium](https://chromewebstore.google.com/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne).
2. Otevři [`stylus.user.css`](https://raw.githubusercontent.com/Richieee-0006/PoStag-ujep/main/stylus.user.css) (Stylus rovnou nabídne přímou instalaci a automatické aktualizace), případně zkopíruj obsah souboru do nového stylu pro URL začínající na `https://portal.ujep.cz/`.

## Konfigurace

Rozměry a typografii lze upravit na začátku souboru `stylus.user.css`:

```css
:root {
    --s-fs: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
    --s-fm: ui-monospace, "JetBrains Mono", monospace;
    --s-sw: 230px;   /* Šířka bočního panelu */
    --s-gap: 20px;   /* Mezera mezi panely */
    --s-mw: 1850px;  /* Maximální šířka obsahu */
}
```
