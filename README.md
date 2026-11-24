# PoStag-ujep

[![Target](https://img.shields.io/badge/target-portal.ujep.cz-5b9bf8?style=flat-square)](https://portal.ujep.cz/)
[![Palette](https://img.shields.io/badge/palette-Graphite_%2B_Cobalt_v2-19191c?style=flat-square)](#barevná-paleta)
[![WCAG](https://img.shields.io/badge/a11y-WCAG_2.1_AA-4cc38a?style=flat-square)](#přehled-úprav)
[![Stylus](https://img.shields.io/badge/extension-Stylus-a1a1aa?style=flat-square)](https://add0n.com/stylus.html)

Klidný tmavý userstyle (Graphite + Cobalt, WCAG 2.1 AA) a modernizace rozhraní pro portál **IS/STAG na UJEP** (`portal.ujep.cz`).

---

## Přehled úprav

| Oblast | Změny |
| :--- | :--- |
| **Vzhled (Unslop v2)** | Neutrální grafitová škála bez fialového zákalu a barevných přechodů, klidný chrom, jeden kobaltový akcent a off-white primární akce. |
| **Přístupnost (WCAG 2.1 AA)** | Kontrasty textu ≥ 4.5 : 1, kontrast hranic vstupů ≥ 3 : 1, podtržené odkazy v textu, globální `:focus-visible`, `forced-colors` a `prefers-reduced-motion`. |
| **Layout** | Převod tabulkového rozložení na **Flexbox / CSS Grid**, sticky boční panel (240 px) a 4px rozměrová mřížka. |
| **Rozvrh** | Opravený výpočet šířek sloupců v režimu *Combined*, klidné karty s 3px levým proužkem a textovým prefixem typu výuky (`P·`/`C·`/`S·`/`Z·`), `tabular-nums` časy. |
| **Předzápis & Tabulky** | 16barevná paleta akcí, zebra řádkování, stavy plateb, výsledků studia, žádostí (`S048`) a konzultací (`S110`). |
| **Responzivita** | Přizpůsobení pro menší monitory (`< 1200px`) a transformace tabulek na karty pro mobily (`< 768px`). |

---

## Barevná paleta

Styl využívá nativní CSS proměnné definované v `:root`:

| Proměnná | Hex | Použití |
| :--- | :--- | :--- |
| `--s-crust` | `#0f0f11` | Hlavička, záhlaví tabulek a portletů, vstupy |
| `--s-mantle` | `#141416` | Hlavní pozadí stránky a kontejnerů |
| `--s-base` | `#19191c` | Pozadí portletů, karet a modálních oken |
| `--s-s0` / `--s-s1` | `#2a2a2e` / `#52525b` | Zvýšené povrchy, jemné linky a 3:1 okraje vstupů |
| `--s-txt` / `--s-sub1` / `--s-ov` | `#ededef` / `#a1a1aa` / `#94949e` | Tři úrovně textu (primární, sekundární, meta) |
| `--s-blue` | `#5b9bf8` | Akcent chromu, odkazy, aktivní indikátory a `:focus-visible` |
| `--s-green` / `--s-yellow` / `--s-red` | `#4cc38a` / `#f0c451` / `#f26469` | Tlumené sémantické barvy pro stavy, notifikace a platby |

---

## Instalace

1. Nainstaluj rozšíření **Stylus** pro [Firefox](https://addons.mozilla.org/cs/firefox/addon/styl-us/) nebo [Chromium](https://chromewebstore.google.com/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne).
2. Otevři [`stylus.user.css`](https://raw.githubusercontent.com/Richieee-0006/PoStag-ujep/main/stylus.user.css) (Stylus rovnou nabídne přímou instalaci a automatické aktualizace), případně zkopíruj obsah souboru do nového stylu pro URL začínající na `https://portal.ujep.cz/`.

---

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
