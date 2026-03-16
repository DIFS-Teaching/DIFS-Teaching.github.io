<!-- .slide: class="section" -->

<header>
  <h1>Selected Inline-Block Elements</h1>
  <p>multimedia, forms</p>
</header>

---

# Image `<img>`

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

- **required attributes**
  - ***`src`*** -- image address (URL or file path)
  - ***`alt`*** -- alternative text shown if the image fails to load, also used by screen readers
- **optional attributes**
  - ***`width`***, ***`height`*** -- dimensions in px (better page rendering if browser knows size in advance)
  - [`loading`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/loading) -- `eager` = loads immediately, `lazy` = loads when reaches to viewport
  - [`srcset`, `sizes`](https://developer.mozilla.org/en-US/docs/Web/HTML/Guides/Responsive_images) -- responsive images
  - [`usemap`](https://www.w3schools.com/tags/tryit.asp?filename=tryhtml_areamap) -- reference to image map (`<map>`)
  - [...](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/img)

---

# Image: Supported Formats

| Format   | Description    | Support                       |
|----------|-------------------------------------------------------------|-------------|
| **JPEG / JPG** | compressed, lossy format for photos              | all |
| **PNG**        | lossless format, supports transparency                 | all |
| **GIF**        | animation, 256 colors, transparency                           | all  |
| **WebP**       | modern format, lossy/lossless, transparency & animation | modern |
| **AVIF**       | new format, high compression, transparency & HDR        | modern |
| **SVG**        | vector format, scalable without quality loss         | modern |
| **APNG**       | animated PNG                                             | modern |

---

# Vector Graphics `<svg>`

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

- ***`width`***, ***`height`*** -- drawing area dimensions
- ***`viewBox`*** -- coordinate system (minX minY width height)
- ***`xmlns`*** -- XML namespace (SVG is an XML language -- **[W3C specification](https://www.w3.org/TR/SVG2/)**)


<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/SVG">MDN</a>,</span>
<span class="note">More in the course PIS -- Advanced Information Systems</span>

=--

<!-- .slide: class="editor" -->

# SVG -- Example

<div data-iframe="assets/examples/robot/svg.html"></div>

<div class="note"><a href="assets/examples/robot/svg.html">source</a></div>

---

# Raster Graphics `<canvas>`

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

- ***`width`***, ***`height`*** -- drawing area dimensions
- rendering is done via JavaScript context (***`getContext("<context>")`***):
  - **[2d](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D)** or **[webgl](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext)**
- graphical elements, unlike SVG, ***are not represented in the DOM***

<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API">MDN</a>,</span>
<span class="note">More in the course PIS -- Advanced Information Systems</span>


=--

<!-- .slide: class="editor" -->

# SVG -- Example

<div data-iframe="assets/examples/robot/canvas.html"></div>

<div class="note"><a href="assets/examples/robot/canvas.html">source</a></div>

---

# SVG vs. Canvas

<span class="note">More in the course PIS -- Advanced Information Systems</span>

<div style="font-size: 2rem;">

| Criteria | **SVG** | **Canvas** |
|-----------|---------|------------|
| **Type of graphics** | 🟢 Vector | 🟢 Raster |
| **Zoom quality** | 🟢 Lossless | 🔴 Pixelates |
| **Interactivity** | 🟢 Easy -- DOM events (onclick)  | 🔴 More complex -- coordinate calculations |
| **Animation** | 🟢 CSS, JS libs (GSAP, Anime.js) | ⚪ JS code (`requestAnimationFrame`) |
| **Performance** | 🔴 Weaker with thousands of objects | 🟢 Fast for large scenes |
| **Accessibility & SEO** | 🟢 Visible in DOM | 🔴 Only bitmap |
| **Styling** | 🟢 CSS support (selectors, filters) | ⚪ Style only via JS API (`fillStyle`, `strokeStyle`) |
| **Image usage** | ⚪ Bitmaps possible (`<image>`) | ⚪ Bitmaps + pixel manipulation (`drawImage`, `getImageData`) |
| **Typical use** | 🟢 Icons, charts, maps | 🟢 Games, animations, effects |
| **Browser support** | 🟢 All modern | 🟢 All modern |

</div>

---

# Multiple Image Sources: `<picture>`

```html
<picture>
  <!-- WebP version for modern browsers -->
  <source srcset="image.webp" type="image/webp">
  
  <!-- JPG version for smaller screens -->
  <source srcset="image-small.jpg" media="(max-width: 600px)">
  
  <!-- Default image (fallback) -->
  <img src="image.jpg" alt="Beautiful landscape" width="600">
</picture>
```

- ***`<source>`*** -- elements specify different versions by:
  - ***`type`*** -- image format (e.g. image/webp).
  - ***`media`*** -- conditions via CSS media queries.
- ***`<img>`*** -- required fallback at the end if no <source> matches.

---

# Audio and Video

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

- contains one or more ***`<source>`*** elements with different formats
  - **audio:** MP3, OGG, WAV, **video:** MP4, WebM, OGV
- ***`width / height`*** – player dimensions, ***`controls`*** -- shows control panel,<br> ***`loop`*** -- plays in a loop, ***`muted`*** -- starts muted, ***`poster`*** -- image shown before playback,<br> ***`autoplay`*** -- plays after loading (video often requires *`muted`* due to browsers),<br> ***`preload`*** -- how much data to load before user starts playback

<span class="note">[MDN audio](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/audio),</span>
<span class="note">[MDN video](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/video)</span>

=--

<!-- .slide: class="editor" -->

# Video -- Custom Player

<div data-iframe="assets/examples/video/video.html"></div>

<div class="note"><a href="asset/examples/video/video.html">source</a></div>

---

# Form Elements: `<input>`

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

- **[`type`](https://www.w3schools.com/html/html_form_input_types.asp)** -- input type
- *`name`* -- field name, key for data submission, *`value`* -- default field value, *`placeholder`* -- helper text inside field, *`readonly`* -- read-only, *`autocomplete`* -- enable/disable autofill
- **[validation](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Form_validation)**: `required`, `disabled`, `min`, `max`, `step`, `checked`, `maxlength`, `pattern`

<span class="note">More in the [IIS](https://www.fit.vut.cz/study/course/IIS/.en) course -- Information Systems</span>

---

# Form Elements: `<label>`, `<select>`, `<textarea>`, `<button>`

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

- ***`label`*** -- uses *`for`* attribute referencing the *`id`* of the form element it labels
- ***`select`*** -- *`multiple`* -- allows selecting multiple options, *`size`* -- number of visible options without scrolling
- ***`textarea`*** -- *`rows`* -- number of visible text lines, *`cols`* -- number of visible characters per line
- ***`button`*** -- *`type`*: `submit` -- default, submits form; `reset` -- clears form; `button` – no action, programmable

<span class="note">More in the [IIS](https://www.fit.vut.cz/study/course/IIS/.en) course -- Information Systems</span>

=--

<!-- .slide: class="editor" -->

# Form Example

<div data-iframe="assets/examples/form/form.html"></div>

<div class="note"><a href="assets/examples/form/form.html">source</a></div>

---

# Status Elements: `<meter>`, `<progress>`

```html
Battery level: <meter value="0.7">70%</meter>
Disk C usage: <meter id="disk_c" value="2" min="0" max="10">2 out of 10</meter>
Disk D usage: <meter id="disk_d" value="0.6">60%</meter>
<br><br>
Downloading: <progress value="30" max="100">30%</progress>
```

<pre class="code-render" default-style="
* {
  font-size: .7rem;
}
" resizable="true" style="height: 150px;">
Battery level: <meter value="0.7">70%</meter>
Disk C usage: <meter id="disk_c" value="2" min="0" max="10">2 out of 10</meter>
Disk D usage: <meter id="disk_d" value="0.6">60%</meter>
<br><br>
Downloading: <progress value="30" max="100">30%</progress>
</pre>

- ***`<meter>`***
  - displays a known value in a known range
  - useful for measuring levels: temperature, capacity, score, rating

- ***`<progress>`***
  - shows progress of a process
  - useful for downloads, uploads, data loading