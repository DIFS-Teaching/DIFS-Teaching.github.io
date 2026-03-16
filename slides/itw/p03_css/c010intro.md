# Vizuální styl v HTML

- **HTML 4**
  - obsahovalo prezentační značky (*`<font>`*, *`<center>`*, *`<big>`*, ...)
  - a atributy (*`bgcolor`*, *`align`*, *`border`*, ...)

<br>

- 🔴 ***nevýhody:***
  - nepřehledný a těžko udržovatelný kód
  - změna vzhledu znamená zasahovat do každého HTML souboru → pracné a náchylné k chybám
  - dokument nelze snadno přeformátovat pro jiné výstupy (mobilní verze, tisk, čtečky)
  - špatná přístupnost → například `<b>` neříká čtečce, proč je text zvýrazněn
  - **dynamicky generovaný obsah**
    - program musí generovat obsah i vzhled
    - při změně vzhledu nutná změna programu

=--

<!-- .slide: class="editor" -->

# Vizuální styl v HTML -- příklad

<div data-iframe="assets/examples/html4/html4.html"></div>

<div class="note"><a href="assets/examples/html4/html4.html">zdroj</a></div>

---

# Oddělený vzhled od obsahu

- **HTML 5**
  - popsat ***strukturu*** a ***význam*** obsahu
  - vzhled popsán odděleně ve ***stylovém předpisu*** (*Cascading Style Sheet*)

<br>

- 🟢 <span style="color: green;">**výhody:**</span>
  - **oddělení obsahu a prezentace** -- HTML se stará o strukturu a význam, CSS o vzhled.
  - **snadná údržba** -- změna jedné CSS třídy změní vzhled na všech stránkách webu.
  - **opakovaná použitelnost** -- stejné styly lze aplikovat na různé dokumenty.
  - **flexibilita** -- různé styly pro různá zařízení (mobil, tisk, dark mode).
  - **pokročilé možnosti** -- animace, responzivní design, proměnné, grid/flexbox – to HTML neumí.

=--

<!-- .slide: class="editor" -->

# Oddělený vzhled od obsahu -- příklad

<div data-iframe="assets/examples/html4/html5.html"></div>

<div class="note"><a href="assets/examples/html4/html5.html">zdroj</a></div>