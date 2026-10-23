# PoStag-ujep

[![Target](https://img.shields.io/badge/target-portal.ujep.cz-89b4fa?style=flat-square)](https://portal.ujep.cz/)
[![Palette](https://img.shields.io/badge/palette-Catppuccin_Mocha-cba6f7?style=flat-square)](https://github.com/catppuccin/catppuccin)
[![Stylus](https://img.shields.io/badge/extension-Stylus-a6e3a1?style=flat-square)](https://add0n.com/stylus.html)

Tmavý userstyle a modernizace rozhraní pro portál **IS/STAG na UJEP** (`portal.ujep.cz`).

---

## Přehled úprav

| Oblast | Změny |
| :--- | :--- |
| **Vzhled** | Kompletní přepis do palety **Catppuccin Mocha** včetně inline stylů, `Bootstrap 5`, `Chosen.js`, `jQuery UI` a `qTip`. |
| **Layout** | Převod tabulkového rozložení na **Flexbox / CSS Grid**, sticky boční panel a přepracovaná horní lišta. |
| **Rozvrh** | Barevné rozlišení výuky (přednášky, cvičení, semináře, zkoušky), zvýraznění aktuálního dne. |
| **Předzápis** | 16barevná paleta akcí, odlišení bloků `A` / `B` / `C`, oprava překrývajících se tlačítek a posuvníků. |
| **Tabulky** | Zebra řádkování, barevné stavy plateb, výsledků studia, žádostí (`S048`) a konzultací (`S110`). |
| **Responzivita** | Přizpůsobení pro menší monitory (`< 1200px`) a transformace tabulek na karty pro mobily (`< 768px`). |

---

## Barevná paleta

Styl využívá nativní CSS proměnné definované v `:root`:

| Proměnná | Hex | Použití |
| :--- | :--- | :--- |
| `--s-crust` | `#11111b` | Hlavička, záhlaví tabulek a portletů, vstupy |
| `--s-mantle` | `#181825` | Hlavní pozadí stránky a kontejnerů |
| `--s-base` | `#1e1e2e` | Pozadí portletů, karet a modálních oken |
| `--s-s0` / `--s-s1` | `#313244` / `#45475a` | Ohraničení, aktivní prvky, hover stavy |
| `--s-txt` | `#f0f4ff` | Primární text |
| `--s-blue` / `--s-mauve` | `#89b4fa` / `#cba6f7` | Odkazy, primární tlačítka, nadpisy sekcí |
| `--s-green` / `--s-yellow` / `--s-red` | `#a6e3a1` / `#f9e2af` / `#f38ba8` | Stavy, notifikace, bloky předmětů a platby |

---

## Instalace

1. Nainstaluj rozšíření **Stylus** pro [Firefox](https://addons.mozilla.org/cs/firefox/addon/styl-us/) nebo [Chromium](https://chromewebstore.google.com/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne).
2. Otevři [`stylus.css`](raw/main/stylus.css) v režimu **Raw** (Stylus nabídne přímou instalaci), případně zkopíruj obsah souboru do nového stylu pro URL začínající na `https://portal.ujep.cz/`.

---

## Konfigurace

Rozměry a typografii lze upravit na začátku souboru `stylus.css`:

```css
:root {
    --s-fs: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
    --s-fm: ui-monospace, "JetBrains Mono", monospace;
    --s-sw: 230px;   /* Šířka bočního panelu */
    --s-gap: 20px;   /* Mezera mezi panely */
    --s-mw: 1850px;  /* Maximální šířka obsahu */
}
```
