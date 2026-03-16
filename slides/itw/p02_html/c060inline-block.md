<!-- .slide: class="section" -->

<header>
	<h1>Vybrané řádkově-blokové elementy</h1>
	<p>multimédia, formuláře</p>
</header>

---

# Obrázek `<img>`

<pre class="code-render" default-style="" resizable="true" style="width: 30%; height: 410px; float: right; z-index: 1; margin: 2rem">
  <img src="https://www.fit.vut.cz/study/course/ITW/public/assets/homer.gif" alt="Homer"
    height="350">
</pre>

```html
<img
	src="homer.gif"
	alt="student when asked to answer a question"
	height="350">
```

- **povinné atributy**
  - ***`src`*** -- adresa obrázku (URL nebo cesta k souboru)
  - ***`alt`*** -- alternativní text, který se zobrazí, pokud se obrázek nenačte, a slouží pro čtečky obrazovky
- **volitelné atributy**
  - ***`width`***, ***`height`*** -- rozměry v px (lepší renderování stránky, pokud zná prohlížeč rozměry předem)
  - [`loading`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/loading) -- `eager` = načte se okamžitě, `lazy` = až když se blíží zobrazení na obrazovce
  - [`srcset`, `sizes`](https://developer.mozilla.org/en-US/docs/Web/HTML/Guides/Responsive_images) -- responzivní obrázky
  - [`usemap`](https://www.w3schools.com/tags/tryit.asp?filename=tryhtml_areamap) -- odkaz na mapu oblastí obrázku (`<map>`)
  - [...](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/img)

---

# Obrázek: podporované formáty

| Formát   | Popis    | Podpora                       |
|----------|-------------------------------------------------------------|-------------|
| **JPEG / JPG** | komprimovaný, ztrátový formát pro fotografie              | všechny |
| **PNG**        | bezztrátový formát, podporuje průhlednost                 | všechny |
| **GIF**        | animace, 256 barev, průhlednost                           | všechny  |
| **WebP**       | moderní formát, ztrátový i bezztrátový, průhlednost i animace | moderní |
| **AVIF**       | nový formát s vysokou kompresí, průhledností i HDR        | moderní |
| **SVG**        | vektorový formát, škálovatelný bez ztráty kvality         | moderní |
| **APNG**       | animovaný PNG                                             | moderní |

---

# Vektorová grafika `<svg>`

<pre class="code-render" default-style="" resizable="true" style="width: 18%; height: 270px; float: right; z-index: 1; margin: 2rem">
<svg width="200" height="200"
 	 xmlns="http://www.w3.org/2000/svg" viewBox="0 0 200 200">
  <!-- Face circle -->
  <circle cx="100" cy="100" r="90" fill="#FFEB3B"
	      stroke="black" stroke-width="4" />
    
  <!-- Eyes -->
  <rect x="58" y="73" width="14" height="14" fill="black" />
  <rect x="128" y="73" width="14" height="14" fill="black" />

  <!-- Smile -->
  <path d="M 60 130 Q 100 170 140 130" stroke="black" stroke-width="6"
	    fill="none" stroke-linecap="round" />
</pre>

```html
<svg width="200" height="200"
 	 xmlns="http://www.w3.org/2000/svg" viewBox="0 0 200 200">
  <!-- Face circle -->
  <circle cx="100" cy="100" r="90" fill="#FFEB3B"
	      stroke="black" stroke-width="4" />
    
  <!-- Eyes -->
  <rect x="58" y="73" width="14" height="14" fill="black" />
  <rect x="128" y="73" width="14" height="14" fill="black" />

  <!-- Smile -->
  <path d="M 60 130 Q 100 170 140 130" stroke="black" stroke-width="6"
	    fill="none" stroke-linecap="round" />
</svg>
```

- ***`width`***, ***`height`*** -- rozměry vykreslovací plochy
- ***`viewBox`*** -- souřadnicový systém (minX minY width height)
- ***`xmlns`*** -- XML jmenný prostor (jedná se o XML jazyk -- **[specifikace W3C](https://www.w3.org/TR/SVG2/)**)


<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/SVG">MDN</a>,</span>
<span class="note">Více v předmětu PIS -- Pokročilé informační systémy</span>

=--

<!-- .slide: class="editor" -->

# SVG -- příklad

<div data-iframe="assets/examples/robot/svg.html"></div>

<div class="note"><a href="assets/examples/robot/svg.html">zdroj</a></div>

---

# Rastrová grafika `<canvas>`

<pre class="code-render" default-style="" resizable="true" style="width: 18%; height: 270px; float: right; z-index: 1; margin: 2rem">
<canvas id="myCanvas" width="200" height="200"
        style="border:1px solid #ccc;">
</canvas>

<script>
  const canvas = document.getElementById("myCanvas");
  const ctx = canvas.getContext("2d");
  ctx.lineWidth = 4;

  // Head
  ctx.beginPath();
  ctx.arc(100, 100, 80, 0, Math.PI * 2);
  ctx.fillStyle = "#FFEB3B";
  ctx.fill();
  ctx.stroke();

  // Eyes (rectangle)
  ctx.fillStyle = "black";
  ctx.fillRect(60, 70, 10, 15);
  ctx.fillRect(120, 70, 10, 15);

  // Smile
  ctx.beginPath();
  ctx.arc(100, 110, 50, 0, Math.PI);
  ctx.stroke();
</script>
</pre>

<div class="code-container" style="height: 500px;">

```html
<canvas id="myCanvas" width="200" height="200"
        style="border:1px solid #ccc;">
</canvas>

<script>
  const canvas = document.getElementById("myCanvas");
  const ctx = canvas.getContext("2d");
  ctx.lineWidth = 4;

  // Head
  ctx.beginPath();
  ctx.arc(100, 100, 80, 0, Math.PI * 2);
  ctx.fillStyle = "#FFEB3B";
  ctx.fill();
  ctx.stroke();

  // Eyes (rectangle)
  ctx.fillStyle = "black";
  ctx.fillRect(60, 70, 10, 15);
  ctx.fillRect(120, 70, 10, 15);

  // Smile
  ctx.beginPath();
  ctx.arc(100, 110, 50, 0, Math.PI);
  ctx.stroke();
</script>
```

</div>

<br>

- ***`width`***, ***`height`*** -- rozměry vykreslovací plochy
- vykreslování probíhá pomocí JavaScriptového kontextu (***`getContext("<context>")`***:
  - **[2d](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D)** nebo **[webgl](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext)**
- grafické prvky na rozdíl od SVG ***nejsou reprezentovány v DOM***

<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API">MDN</a>,</span>
<span class="note">více v předmětu PIS -- Pokročilé informační systémy</span>


=--

<!-- .slide: class="editor" -->

# SVG -- příklad

<div data-iframe="assets/examples/robot/canvas.html"></div>

<div class="note"><a href="assets/examples/robot/canvas.html">zdroj</a></div>

---

# SVG vs. Canvas

<span class="note">více v předmětu PIS -- Pokročilé informační systémy</span>

<div style="font-size: 2rem;">

| Kritérium | **SVG** | **Canvas** |
|-----------|---------|------------|
| **Typ grafiky** | 🟢 Vektorová | 🟢 Rasterová |
| **Kvalita při zvětšení** | 🟢 Bezeztrátová | 🔴 Pixeluje se |
| **Interaktivita** | 🟢 Snadná -- DOM události (onclick)  | 🔴 Složitější -- výpočet souřadnic |
| **Animace** | 🟢 CSS, JS knihovny (GSAP, Anime.js) | ⚪ JS kód (`requestAnimationFrame`) |
| **Výkon** | 🔴 Slabší u tisíců objektů | 🟢 Rychlý pro velké scény |
| **Přístupnost a SEO** | 🟢 Viditelné v DOM | 🔴 Jen bitmapa |
| **Styling** | 🟢 CSS podpora (selektory, filtry) | ⚪ Styl jen přes JS API (`fillStyle`, `strokeStyle`) |
| **Použití obrázků** | ⚪ Bitmapy možné (`<image>`) | ⚪ Bitmapy + pixelová úprava (`drawImage`, `getImageData`) |
| **Typické použití** | 🟢 Ikony, grafy, mapy | 🟢 Hry, animace, efekty |
| **Podpora prohlížečů** | 🟢 Všechny moderní | 🟢 Všechny moderní |

</div>

---

# Více zdrojů obrázků: `<picture>`

```html
<picture>
  <!-- WebP verze pro moderní prohlížeče -->
  <source srcset="image.webp" type="image/webp">
  
  <!-- JPG verze pro menší obrazovky -->
  <source srcset="image-small.jpg" media="(max-width: 600px)">
  
  <!-- Výchozí obrázek (fallback) -->
  <img src="image.jpg" alt="Beautiful landscape" width="600">
</picture>
```

- ***`<source>`*** -- elementy určují různé verze podle:
  - ***`type`*** -- formát obrázku (např. image/webp).
  - ***`media`*** -- podmínky podle CSS media queries.
- ***`<img>`*** -- na konci je povinný fallback, pokud žádný <source> nevyhovuje.

---

# Audio a video

<pre class="code-render" default-style="" resizable="true" style="width: 30%; height: 410px; float: right; z-index: 1; margin: 2rem">
<audio width="480" controls style="width: 480px;">
  <source src="https://www.fit.vut.cz/study/course/ITW/public/assets/frank.ogg" type="audio/ogg">
  <source src="https://www.fit.vut.cz/study/course/ITW/public/assets/frank.mp3" type="audio/mp3">
  Your browser does not support the audio tag.
</audio>

<video width="480" height="270" controls>
  <source src="https://www.fit.vut.cz/study/course/ITW/public/assets/shoes.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
</pre>

```html
<audio style="width: 480px;" controls>
  <source src="frank.mp3" type="audio/mp3">
  <source src="frank.ogg" type="audio/ogg">
  Your browser does not support the audio tag.
</audio>

<video width="480" height="270" controls>
  <source src="shoes.mp4" type="video/mp4">
  <source src="shoes.webm" type="video/webm">
  Your browser does not support the video tag.
</video>
```

- obsahuje jeden nebo více elementů ***`<source>`*** s různými formáty
  - **audio:** MP3, OGG, WAV, **video:** MP4, WebM, OGV
- ***`width / height`*** – rozměry přehrávače, ***`controls`*** -- zobrazí ovládací panel,<br> ***`loop`*** -- přehrává dokola, ***`muted`*** -- startuje bez zvuku, ***`poster`*** -- obrázek zobrazený před spuštěním,<br> ***`autoplay`*** -- přehrává po načtení (video často vyžaduje *`muted`* kvůli prohlížečům),<br> ***`preload`*** -- kolik dat má načíst před tím, než uživatel spustí přehrávání

<span class="note">[MDN audio](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/audio),</span>
<span class="note">[MDN video](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/video)</span>

=--

<!-- .slide: class="editor" -->

# Video -- vlastní přehrávač

<div data-iframe="assets/examples/video/video.html"></div>

<div class="note"><a href="asset/examples/video/video.html">zdroj</a></div>

---

# Formulářové prvky: `<input>`

<pre class="code-render" default-style="
* {
  font-size: .7rem;
}
" resizable="true" style="width: 30%; height: 510px; float: right; z-index: 1; margin: 2rem">
<input type="text" placeholder="Text"><br>
<input type="password" placeholder="Password"><br>
<input type="email" placeholder="Email"><br>
<input type="number" min="0" max="10"><br>
<input type="url" placeholder="URL"><br>
<input type="tel" placeholder="Telephone"><br>
<input type="date"><br>
<input type="color"><br>
<input type="range" min="0" max="100"><br>
<input type="radio" name="gender" value="male"> Male
<input type="radio" name="gender" value="female"> Female<br>
<input type="checkbox"> Subscribe<br>
<input type="submit" value="Submit">
</pre>

```html
<input type="text" placeholder="Text"><br>
<input type="password" placeholder="Password"><br>
<input type="email" placeholder="Email"><br>
<input type="number" min="0" max="10"><br>
<input type="url" placeholder="URL"><br>
<input type="tel" placeholder="Telephone"><br>
<input type="date"><br>
<input type="color"><br>
<input type="range" min="0" max="100"><br>
<input type="radio" name="gender" value="male"> Male
<input type="radio" name="gender" value="female"> Female<br>
<input type="checkbox"> Subscribe<br>
<input type="submit" value="Submit">
```

- **[`type`](https://www.w3schools.com/html/html_form_input_types.asp)** -- typ vstupu
- *`name`* -- název pole, klíč pro odesílání dat, *`value`* -- výchozí hodnota pole, *`placeholder`* -- pomocný text uvnitř pole, *`readonly`* -- pro čtení, *`autocomplete`* -- povolení / zákaz doplňování
- **[validace](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Form_validation)**: `required`, `disabled`, `min`, `max`, `step`, `checked`, `maxlength`, `pattern`

<span class="note">Více v předmětu IIS -- Informační systémy</span>

---

# Formulářové prvky: `<label>`, `<select>`, `<textarea>`, `<button>`

<pre class="code-render" default-style="
* {
  font-size: .7rem;
}
" resizable="true" style="width: 30%; height: 250px; float: right; z-index: 1; margin: 2rem">
<label for="fruit">Choose a fruit:</label>
<select id="fruit" name="fruit">
  <option value="apple">Apple</option>
  <option value="banana">Banana</option>
  <option value="orange">Orange</option>
  <option value="strawberry">Strawberry</option>
</select><br>
<textarea name="message" rows="4" cols="30"></textarea><br>
<button type="submit" onclick="send(...)">Send</button>
</pre>

```html
<label for="fruit">Choose a fruit:</label>
<select id="fruit" name="fruit">
  <option value="apple">Apple</option>
  <option value="banana">Banana</option>
  <option value="orange">Orange</option>
  <option value="strawberry">Strawberry</option>
</select>
<textarea name="message" rows="4" cols="30"></textarea><br><br>
<button type="submit" onclick="send(...)">Send</button>
```

- ***`label`*** -- používá atribut *`for`* referující *`id`* formulářového prvku, se kterým je popisek propojen
- ***`select`*** -- *`multiple`* -- umožní vybrat více položek najednou, *`size`* --	počet viditelných položek bez nutnosti rolování
- ***`textarea`*** -- *`rows`* -- počet viditelných textových řádků, *`cols`* -- počet viditelných znaků na řádek
- ***`button`*** -- *`type`*: `submit` -- výchozí, odešle formulář; `reset` -- vymaže obsah formuláře; `button` – neprovádí akci, lze naprogramovat

<span class="note">Více v předmětu IIS -- Informační systémy</span>

=--

<!-- .slide: class="editor" -->

# Příklad formuláře

<div data-iframe="assets/examples/form/form.html"></div>

<div class="note"><a href="assets/examples/form/form.html">zdroj</a></div>

---

# Stavové prvky: `<meter>`, `<progress>`

```html
Úroveň baterie: <meter value="0.7">70%</meter>
Zaplnění disku C: <meter id="disk_c" value="2" min="0" max="10">2 out of 10</meter>
Zaplnění disku D: <meter id="disk_d" value="0.6">60%</meter>
<br><br>
Stahování: <progress value="30" max="100">30%</progress>
```

<pre class="code-render" default-style="
* {
  font-size: .7rem;
}
" resizable="true" style="height: 150px;">
Úroveň baterie: <meter value="0.7">70%</meter>
Zaplnění disku C: <meter id="disk_c" value="2" min="0" max="10">2 out of 10</meter>
Zaplnění disku D: <meter id="disk_d" value="0.6">60%</meter>
<br><br>
Stahování: <progress value="30" max="100">30%</progress>
</pre>

- ***`<meter>`***
  - slouží k zobrazení známé hodnoty v známém rozsahu
  - hodí se pro měření úrovně něčeho: teplota, kapacita, skóre, hodnocení

- ***`<progress>`***
  - zobrazuje postup nějakého procesu
  - hodí se pro stahování, nahrávání, načítání dat