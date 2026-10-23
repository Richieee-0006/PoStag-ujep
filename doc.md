# Technická dokumentace (`stylus.css`)

Detailní rozbor architektury, CSS proměnných, selektorů a oprav pro portál IS/STAG na UJEP (`https://portal.ujep.cz/`). Styl je rozdělen do 10 samostatných bloků `@-moz-document url-prefix("https://portal.ujep.cz/")`.

---

## Obsah

1. [Proměnné, reset, typografie a globální přepisy](#1-proměnné-reset-typografie-a-globální-přepisy)
2. [Hlavička, vyhledávání a navigace](#2-hlavička-vyhledávání-a-navigace)
3. [Kontejnery, rozložení a portlety](#3-kontejnery-rozložení-a-portlety)
4. [Karta studenta, info lišta a notifikace](#4-karta-studenta-info-lišta-a-notifikace)
5. [Rozvrh hodin](#5-rozvrh-hodin)
6. [Tabulky, platby, výsledky studia a subportlety](#6-tabulky-platby-výsledky-studia-a-subportlety)
7. [Grafický předzápis, vizualizace studia a studijní plán](#7-grafický-předzápis-vizualizace-studia-a-studijní-plán)
8. [Formuláře, vstupy, tlačítka, záložky a stránkování](#8-formuláře-vstupy-tlačítka-záložky-a-stránkování)
9. [Hlášky, modální okna, patička a opravy](#9-hlášky-modální-okna-patička-a-opravy)
10. [Responzivita (Media Queries)](#10-responzivita-media-queries)

---

## 1. Proměnné, reset, typografie a globální přepisy

První sekce definuje kompletní design systém v `:root`, sjednocuje vykreslování písma a řeší nativní inline styly, které IS/STAG generuje přímo do HTML atributů `style="..."`.

### Design tokeny (`:root`)

| Kategorie | Proměnné | Hodnoty / Popis |
| :--- | :--- | :--- |
| **Pozadí (Catppuccin)** | `--s-crust`, `--s-mantle`, `--s-base`, `--s-alt`, `--s-dis` | Od nejtmavší `#11111b` (hlavičky, vstupy) přes `#181825` (pozadí) po `#1e1e2e` (karty) a `#14141f` (neaktivní prvky). |
| **Povrchy a hrany** | `--s-s0`, `--s-s1`, `--s-sub`, `--s-alt2` | Odstíny `#313244` až `#45475a` pro rámečky, oddělovače a hover stavy. |
| **Text** | `--s-txt`, `--s-sub1`, `--s-sub0`, `--s-ov` | Hlavní text `#f0f4ff`, sekundární `#dce2f7`, tlumený `#a6adc8` a neaktivní `#7f849c`. |
| **Akcenty** | `--s-blue`, `--s-lav`, `--s-mauve`, `--s-red`, `--s-green`, `--s-yellow`, `--s-peach`, `--s-teal` | Sémantické barvy pro odkazy, stavy, bloky předmětů a notifikace. |
| **Přechody rozvrhu** | `--s-gl`, `--s-glb`, `--s-gs`, `--s-ge` | Lineární gradienty (`145deg`) pro přednášky, cvičení, semináře a zkoušky. |
| **Rozměry a zaoblení** | `--s-r-xs` až `--s-r-xl`, `--s-sw`, `--s-gap`, `--s-mw` | Zaoblení `3px`–`10px`, šířka sidebaru `230px`, mezera `20px`, max. šířka `1850px`. |
| **Bootstrap 5 přepisy** | `--bs-body-bg`, `--bs-body-color`, `--bs-card-bg`, `--bs-border-color`, `--bs-link-color` | Přímé napojení proměnných z nové šablony STAGu (Zebra / BS5) na lokální paletu. |

### De-tabulkování hlavních obalů
STAG obaluje stránku i portlety do vnořených tabulek (`table.app_portlet_frame_out`, `table.render_container`, `tbody.column`). Tyto prvky jsou převedeny na `display: block !important; width: 100% !important;`, čímž se odstraní fixní šířky a umožní responsivní chování.

### Přepisy inline stylů (Case-insensitive atributové selektory)
Starší moduly STAGu vkládají barvy natvrdo přes atribut `style`. Styl využívá selektory s příznakem `i` (case-insensitive) v obou variantách (s mezerou i bez mezery za dvojtečkou):
* **Bílá a světlá pozadí:** `*[style*="background-color: white" i]`, `#fff`, `rgb(255, 255, 255)`, `#F4F2F2`, `#E4E4C9` $\rightarrow$ přepsáno na `--s-base`.
* **Šedá pozadí (neaktivní buňky):** `rgb(180, 180, 180)`, `#b4b4b4`, `darkgray` $\rightarrow$ přepsáno na `--s-dis`.
* **Sémantické barvy textu:** Inline `red`, `green`, `#FFa500` a `#D975BC` jsou namapovány na odpovídající proměnné (`--s-red`, `--s-green`, `--s-peach`).

### Inverze log a oprava dvojitých ikon
* **Loga v hlavičce** (`.logo-cs`, `.z-logo_velke_cs` atd.) využívají `filter: invert(1) hue-rotate(180deg)` v kombinaci s `mix-blend-mode: lighten !important;`, díky čemuž zmizí původní bílý podklad loga bez nutnosti nahrávat externí obrázky.
* **Oprava `.has-text.xg_ro_31` a `.xg_ro_21`:** STAG u těchto odkazů vykresloval ikonu na pozadí `<a>` a zároveň uvnitř vnořeného `<span>`. Na `<a>` je proto aplikováno `background-image: none !important` a celý prvek je stylován jako moderní inline-flex tlačítko.

---

## 2. Hlavička, vyhledávání a navigace

Řeší horní lištu, vyhledávací pole, horizontální menu a levý boční panel napříč starou i novou (Bootstrap 5) šablonou.

* **Horní lišta (`.app_header_wrapper`, `#portal-header-wrapper`):** Přebarvena na `--s-crust` se spodním rámečkem `--s-s0`. Odkazy v pravé horní části (`.app_header_right .upper a`) jsou převedeny na samostatné štítky (pills).
* **Skrytí prázdných lišt:** Selektor `div.portal-nav-level-1:empty, div.portal-nav-level-2:empty { display: none !important; }` odstraňuje prázdné vymezovací pruhy v BS5 šabloně.
* **Horizontální navigace (`ul.app_menubar`, `nav.portal-top-nav`):** Převedena z `float: left` na Flexbox (`display: flex; flex-wrap: wrap; gap: 4px;`). Aktivní položka (`.selected`, `.active`) má modrý spodní indikátor pomocí `box-shadow: inset 0 -2px 0 var(--s-blue)`.
* **Hlavní layout (`.app_page_multi`):** Místo obtékání (`float`) používá `display: flex; flex-direction: row; align-items: flex-start; gap: 20px;`.
* **Sticky boční navigace (`.app_page_menu`, `aside.side-nav`, `.prohlizeni_nav_wrapper`):**
  * Pevná šířka `flex: 0 0 230px` (u prohlížení `190px`).
  * Při rolování zůstává připnutá (`position: sticky; top: 15px;`).
  * Aktivní položka má zvýrazněný levý okraj (`border-left: 4px solid var(--s-blue)`).

---

## 3. Kontejnery, rozložení a portlety

Definuje vzhled jednotlivých oken (portletů) a opravuje přetékání širokých tabulek.

* **Hlavní obsah (`.app_page_content`, `.portlet-container`):** Nastaveno `flex: 1 1 0%; min-width: 0;`. Vlastnost `min-width: 0` je klíčová pro Flexbox – zabraňuje tomu, aby široká tabulka uvnitř portletu roztáhla kontejner mimo obrazovku.
* **Karty portletů (`.app_portlet_frame_in`, `section.portlet`):** Zaoblené rohy (`--s-r-xl`), pozadí `--s-base` a hlavička (`.app_portlet_head_title`, `.portlet-header`) v barvě `--s-crust`.
* **Oprava portletu Praxe (`S088`):** Kontejnery `#seznamPraxiStudenta` a `.pxTabResizer` měly natvrdo nastavenou nízkou výšku s posuvníkem. Přepsáno na `height: auto !important; max-height: none !important;` a zastaralá uchopovací lišta `.resizeGrippie` je skryta.
* **Hlavička v Prohlížení (`.prohlizeniEntitaHead`):** Převedena z absolutního/float pozicování na `display: flex; justify-content: space-between; align-items: center;`.

---

## 4. Karta studenta, info lišta a notifikace

Upravuje osobní lištu přihlášeného uživatele (`#UserInfoG`, `.st-uc-info2`).

* **Flexbox řádek (`.st-uc-info2.fake-table-row`):** Původní simulovaná tabulka je převedena na `display: flex; flex-wrap: wrap; align-items: center; gap: 10px 16px;`.
* **Notifikace (`#notif_opener`):** Zvýrazněný červený odznak (`rgba(243, 139, 168, 0.16)`) s pevnou výškou `30px`. Duplicitní tlačítko „Přejít na další nepřečtené oznámení“ (`img[src*="notification-next"]`) je skryto pro čistší vzhled.
* **Studijní štítky (`.user-info-content span`):** Osobní číslo a role se vykreslují v neproporcionálním písmu (`--s-fm` / `JetBrains Mono`) jako zarovnané štítky o výšce `30px`.
* **Rozšířené info (`[id*="extended_info_div"]`):** Zarovnáno doprava (`margin-left: auto`) jako žlutý informační odznak (`--s-yellow`).

---

## 5. Rozvrh hodin

Kompletní přepis rozvrhové mřížky (`table.rozvrhMainTable`, `table.gpv_rozvrhMainTable`).

| Třída / Selektor | Typ akce / Prvek | Vzhled |
| :--- | :--- | :--- |
| `td.rozvrhRoakSkin_prednaska`, `.scss-pred` | Přednáška | Fialový gradient `--s-gl` + rámeček `--s-mauve` |
| `td.rozvrhRoakSkin_cviceni`, `.scss-cvic` | Cvičení | Modrý gradient `--s-glb` + rámeček `--s-blue` |
| `td.rozvrhRoakSkin_seminar`, `.scss-sem` | Seminář | Zelený gradient `--s-gs` + rámeček `--s-green` |
| `td.rozvrhRoakSkin_zkouska`, `_blokova` | Zkouška / Bloková výuka | Oranžový gradient `--s-ge` + rámeček `--s-peach` |
| `td.rozvrhLeftHeadingDenName[style*="fffbb5" i]` | Dnešní den | Žluté podsvícení s levým okrajem `3px solid var(--s-yellow)` |
| `div.rozvrhItemLineNekonaSe` | Výuka se nekoná | Výrazný štítek s pozadím `--s-red` a tmavým textem `--s-crust` |

* **Technický řádek `.rozvrhCasRadaCellspacer`:** STAG používá tento skrytý řádek k definici šířek sloupců (`width: 0.53%`). Styl zachovává šířku buněk, ale nuluje jejich výšku, padding a písmo (`height: 0; font-size: 0;`), aby nevznikaly prázdné mezery.
* **Čitelnost buněk:** Čas od–do (`.rozvrhRoakOdDoHSpacer`) má poloprůhledné tmavé pozadí `rgba(0, 0, 0, 0.38)`, místnost (`.rozvrhRoakMistnostSpacer a`) je vykreslena jako kontrastní tmavý štítek a rušivé mini-ikonky (`comment.png`, `ico_ra_small`, `ucitel`) jsou skryty.

---

## 6. Tabulky, platby, výsledky studia a subportlety

Sjednocuje datové tabulky (`table.xg_tab_c`, `table.ng_tab`, `table.podminky_abs`, `table.table`) a stavové řádky.

* **Zebra řádkování a hover:** Sudé řádky mají pozadí `--s-base`, liché `--s-mantle` a při najetí myší (`:hover`) se řádek zvýrazní barvou `--s-s0`.
* **Opakované / nesplněné předměty:** Řádky s inline barvou `#D975BC` nebo atributem `title*="failed"` dostávají tmavě vínové pozadí `--s-rep` (`#3d1c33`) a červený text `--s-red`.
* **Stavy plateb (`.platby_stav_*`):**
  * `stav_2` (Uhrazeno) $\rightarrow$ zelená (`--s-green`)
  * `stav_3` (Neuhrazeno / Po splatnosti) $\rightarrow$ červená (`--s-red`)
  * `stav_4`, `stav_7` (Čekající / Předpis) $\rightarrow$ žlutá (`--s-yellow`)
  * `stav_5` (Vráceno / Přeplatek) $\rightarrow$ modrá (`--s-blue`)
* **Studentské žádosti (`S048`) a Konzultace (`S110`):** Třídy `.predmet-ma-kladnou-odpoved`, `.predmet-nema-odpoved`, `.predmet-ma-zapornou-odpoved` a `.consultation-capacity-badge` jsou převedeny na jemné poloprůhledné barvy (`0.16` alpha) s odpovídajícím barevným textem.

---

## 7. Grafický předzápis, vizualizace studia a studijní plán

Nejkomplexnější sekce řešící modul `vsp` / `gpv` (Grafický předzápis a Vizualizace studia), který v původním STAGu silně spoléhá na absolutní pozicování a pevné pixelové rozměry.

### Opravy ovládacího panelu (`div.gpv-fu-b1`)
* **Odstranění grafického rámečku:** Dekorativní zaoblené hrany ze starých obrázků (`.gpv-fu-b0-left`, `-center`, `-right`) jsou skryty.
* **Oprava překryvu tlačítek:** Bloky `.gpv-form-block-2-1h:not(.gpv-form-block-2-1c)` a `.gpv-form-block-2-1c` mají přepočítané souřadnice `top` a `left`, aby se tlačítka *Help | Changes | Reset* nepřekrývala s přepínačem roků.
* **Zarovnání checkboxů (`.gpv-form-block-2-1d`):** Vstupy `input.gpv-fb3-input` (`12x12px`, `float: left; clear: left;`) a popisky `label.gpv-fb3-label` (`max-width: 136px; text-overflow: ellipsis;`) jsou přesně zarovnány do pravého sloupce bez rozpadání.

### Strom studijního plánu a bloky předmětů
* **Hlavičky segmentů (`.gpv-strom-planHead`, `.gpv-strom-segmentHead`):** Převedeny na Flexbox (`justify-content: space-between`), čímž se vyřešilo odskakování čítačů kreditů (`.gpv-strom-SegmentCounterHead`).
* **Kategorie předmětů:**
  * **Typ A (Povinné):** `.gpv-pred-typ-A` $\rightarrow$ červený akcent (`--s-red`)
  * **Typ B (Povinně volitelné):** `.gpv-pred-typ-B` $\rightarrow$ modrý akcent (`--s-blue`)
  * **Typ C (Volitelné):** `.gpv-pred-typ-C` $\rightarrow$ zelený akcent (`--s-green`)
* **Stavové proužky předmětu (`.gpv-predstav-*-brd-new`):** Levý okraj `6px solid` indikuje stav: splněno (`--s-green`), nesplněno (`--s-red`), aktuálně studováno (`--s-peach`), zapsáno (`--s-mauve`), vybráno (`--s-blue`).

### Spodní část předzápisu (`#spodekPredzapisu`) a 16 barevných sad
* Kontejnery `#spodekPredzapisu` a `.gpv-yellow-container` jsou převedeny z floatů na responsivní Flexbox, takže rozvrh (`.gpv-blue-container`, `.gpv-green-container`) plynule využívá dostupnou šířku.
* **16 barevných tříd (`.gpv-pred-II-0` až `.gpv-pred-II-15`):** Každému předmětu v grafickém předzápisu STAG přiřazuje jednu ze 16 barev pro spárování se spodním rozvrhem. Styl nahrazuje původní křiklavé světlé barvy 16 ručně vyladěnými tmavými odstíny s vysokým kontrastem textu.
* **Klasický předzápis (`#mainSirka`) a Zbývající povinnosti (`S073`):** Řádky v `#mainSirka` používají Flexbox místo pevných šířek a předměty ve Zbývajících povinnostech (`span.podminky_abs_predmet`) jsou vykresleny jako přehledné štítky s odděleným počtem kreditů.

---

## 8. Formuláře, vstupy, tlačítka, záložky a stránkování

Řeší formulářové prvky, našeptávače a přepínací záložky.

* **Ochrana checkboxů a radiobuttonů:** STAG přidává třídu `.text` nebo `.pv_input_as_chosen` i na checkboxy. Selektor pro textová pole proto explicitně vylučuje ostatní typy pomocí `:not([type="checkbox"]):not([type="radio"]):not([type="button"]):not([type="submit"]):not([type="reset"])`. Samotné checkboxy a radiobuttony mají pevný rozměr `16x16px` a `accent-color: var(--s-blue)`.
* **Knihovna Chosen.js (`.chosen-container`):** V původním CSS STAGu je použito agresivní pravidlo `table.ng_form_tab td .chosen-container { background: #ffe !important }`. Styl toto pravidlo přebíjí vyšší specificitou selektoru a nastavuje tmavé pozadí `--s-crust` pro výběrové pole a `--s-base` pro rozbalovací menu (`.chosen-drop`).
* **Hierarchie tlačítek:**
  1. **Sekundární tlačítka** (`button`, `.btn-default`, `.btn-secondary`) jsou definována jako první s pozadím `--s-s0` a textem `--s-txt`.
  2. **Primární tlačítka** (`input[type="submit"]`, `.btn-primary`, `button.submit`) následují po nich s modrým pozadím `--s-blue` a tmavým textem `--s-crust`.

---

## 9. Hlášky, modální okna, patička a opravy

Sjednocuje systémová oznámení, vyskakovací okna a patičku portálu.

* **Systémové hlášky:**
  * **Info (`.xg_msgFromServerInfo`, `.alert-info`):** Modrý levý okraj `--s-blue`.
  * **Varování (`.xg_msgFromServerWarning`, `.alert-warning`):** Žlutý levý okraj `--s-yellow`.
  * **Chyba (`.xg_msgFromServerError`, `.alert-danger`):** Červený levý okraj `--s-red`.
* **Skrytí prázdných validačních kontejnerů:** Selektory `.xgt_validationErrors:empty` a `.prohlizeniEntitaSearchedCoat:has(> .prohlizeniEntitaSearched:empty)` skrývají prázdné rámečky, které STAG vykresluje před odesláním vyhledávacího formuláře.
* **Modální okna a našeptávače:** Podpora pro `jQuery UI Dialog` (`.ui-dialog`), Bootstrap modály (`.modal-content`), detail předmětu (`.gpv-bublina-coat`), `qTip` (`.qtip-content`) a kalendář (`.calendar`).
* **Patička (`.app_footer_col_wrapper`):** Převedena na Flexbox s rovnoměrnými sloupci (`flex: 1 1 200px`) a skrytím prázdné dekorační lišty `.footer_header`.

---

## 10. Responzivita (Media Queries)

Zajišťuje použitelnost portálu na menších monitorech, tabletech a telefonech.

### Breakpoint `max-width: 1200px` (Menší notebooky a tablety)
* Hlavní kontejner `.app_page_multi` mění směr na sloupec (`flex-direction: column`).
* Boční panel (`.app_page_menu`, `aside.side-nav`) ruší `position: sticky`, roztahuje se na `100%` šířky a jeho položky se skládají vedle sebe jako horizontální tlačítka (`flex-direction: row; flex-wrap: wrap;`).

### Breakpoint `max-width: 768px` (Mobilní zařízení)
* Kompenzace výšky mobilní hlavičky (`margin-top: 56px` na `.app_content`).
* **Transformace tabulek (`table.table-reflow`):**
  * Hlavička `thead` je skryta (`display: none`).
  * Každý řádek `tbody tr` se mění na samostatnou kartu s mřížkou `display: grid; grid-template-columns: repeat(auto-fill, minmax(135px, 1fr));`.
  * Názvy sloupců se automaticky vypisují nad každou hodnotou pomocí pseudo-elementu `td::before { content: attr(data-header) !important; }`.