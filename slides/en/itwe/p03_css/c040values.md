<!-- .slide: class="section" -->

<header>
  <h1>Property Values</h1>
  <p>specific, numbers, lengths, sizes, measures, functions, colors</p>
</header>

---

# Property Value

- a specific setting that defines ***how a property should behave*** and what effect it has on rendering an element in the browser
  - e.g. `red`, `10px`, `flex`, ...

<br>

- each property has a defined set of allowed values (type) according to the **[W3C CSS specification](https://www.w3.org/Style/CSS/current-work)**

```css
color: blue;
font-size: 12pt;
```

- values can be combinations of several basic types

```css
margin: 10px 20px;
font: italic small-caps bold 16px/1.5 Arial;
```

---

# Value Types

- ***specific property values***
  - predefined textual values directly in the specification for particular properties
  - `display: block | inline | inline-block | flex | grid | ...`

- ***numbers***
  - integers and decimals
  - `line-height: 1.5`, `z-index: 10;`, ...

- ***lengths, sizes***
  - *absolute*: `px`, `cm`, `mm`, `in`, `pt`, `pc`
  - `1in` = `96px`, `1in` = `72pc`, `1pc` = `12pt`
  - *relative*: `em`, `rem`, `%`, `ex`, `ch`, `vw`, `vh`, `vmin`, `vmax`
  - `margin`: `10px`, `font-size`: `1.2em`, ...

  - examples below...

=--

# Value Types: em, rem

<pre class="code-render" default-style="
html {
  font-size: 20px;
}

.em2 {
  font-size: 2em;
}

.rem2 {
  font-size: 2rem;
}

body > div {
  border: 2px solid blue;
  margin: 2rem;
}

div > div {
  border: 2px solid green;
  margin: 2rem;
}
" resizable="true" style="width: 50%; height: 840px; float: right; z-index: 1" tags="true">

Default font size: 1rem

<div class="rem2">
  Font size: 2rem
  <div class="rem2">Font size: 2rem</div>
  <div class="em2">Font size: 2em</div>
</div>

<div class="em2">
  Font size: 2em
  <div class="rem2">Font size: 2rem</div>
  <div class="em2">Font size: 2em</div>
</div>

</pre>

```css
html {
  font-size: 20px;
}

.em2 {
  font-size: 2em; /* 2x parent */
}

.rem2 {
  font-size: 2rem; /* 2x root */
}

body > div {
  border: 2px solid blue;
  margin: 2rem;
}

div > div {
  border: 2px solid green;
  margin: 2rem;
}
```

=--

# Value Types: vw, %

<pre class="code-render" default-style="
html { border: 2px solid red }
body { border: 2px solid black }

.pct75 {
  /* 75% of parent width */	
  width: 75%;
}

.vw75 {
  /* 75% of viewport width */
  width: 75vw;
}

div {
  border: 2px solid blue;
  margin: 2rem;
}

div > div {
  border: 2px solid green;
}
" resizable="true" style="width: 50%; height: 750px; float: right; z-index: 1" tags="true">

<div class="pct75">
75%
<div class="pct75">75%</div>
<div class="vw75">75vw</div>
</div>

<div class="vw75">
75vw
</div>
</pre>

```css
html { border: 2px solid red }
body { border: 2px solid black }

.pct75 {
  /* 75% of parent width */	
  width: 75%;
}

.vw75 {
  /* 75% of viewport width */
  width: 75vw;
}

div {
  border: 2px solid blue;
  margin: 2rem;
}

div > div {
  border: 2px solid green;
}
```

=--

# Value Types: vmax

<pre class="code-render" default-style="
html {
  border: 2px solid red;
  height: 99vh;
}

.vmax50 {
  width: 50vmax;
}

div {
  border: 2px solid blue;
  margin: 2rem;
}
" resizable="true" style="width: 30%; height: 700px; float: right; z-index: 1" tags="true">
  <div class="vmax50">
  50vmax
  </div>
</pre>

```css
html {
  border: 2px solid red;
  height: 99vh;
}

.vmax50 {
  /* 50% of the larger viewport dimension */
  width: 50vmax;
}

div {
  border: 2px solid blue;
  margin: 2rem;
}
```

---

# Value Types

- ***functional values***
  - special syntax with parameters
  - `calc(), var(), min(), max(), clamp(), attr()`
  - `width: calc(100% - 40px);`

- ***URL and references***
  - link to a file or resource.
  - `background-image: url("bg.png"); cursor: url("cursor.cur"), auto;`

- ***colors***
  - keywords (`red`, `blue`, `transparent`)
  - hex notation (`#ff0000`, `#f00`)
  - functions: `rgb()`, `rgba()`, `hsl()`, `hsla()`, `lab()`, `color()`

---

# Value Types: named colors

<pre class="code-render" default-style="
.colors {
  display: flex;
  flex-wrap: wrap;
}

.colors > div {
  font-size: .7rem;
  /*border: 2px solid black;*/
  width: 250px;
  padding: .2rem;
}
" resizable="true" style="height: 800px;">

<!--<h4>Basic set</h4>
<div class="colors"></div>

<h4>Extended set</h4>-->
<div class="colors"></div>

<script>
  let renderColors = function(rootElement, colors) {
  colors.forEach(color => {
    let colorElement = document.createElement("div");
    colorElement.style["background-color"] = color;
    colorElement.innerHTML = color;
    rootElement.append(colorElement);
    
    // text color based on brightness
    const s = getComputedStyle(colorElement);
    if(s && s["background-color"]) {
      const [r, g, b] = s["background-color"].match(/\d+/g).map(Number);
      if(r & g & b) {
        const brightness = (r * 299 + g * 587 + b * 114) / 1000;
        colorElement.style.color = brightness < 128 ? "white" : "black";
      }
    }
  });
  }

  //let colors = [ "black", "silver", "gray", "white", "maroon", "red", "purple", "fuchsia", "green", "lime", "olive", "yellow", "navy", "blue", "teal", "aqua" ];
  let colorsExtra = [
  "aliceblue", "antiquewhite", "aqua", "aquamarine", "azure", "beige", "bisque", "black", "blanchedalmond", "blue", "blueviolet", "brown", "burlywood", "cadetblue", "chartreuse", "chocolate", "coral", "cornflowerblue", "cornsilk", "crimson", "cyan", "darkblue", "darkcyan", "darkgoldenrod", "darkgray", "darkgreen", "darkgrey", "darkkhaki", "darkmagenta", "darkolivegreen", "darkorange", "darkorchid", "darkred", "darksalmon", "darkseagreen", "darkslateblue", "darkslategray", "darkslategrey", "darkturquoise", "darkviolet", "deeppink", "deepskyblue", "dimgray", "dimgrey", "dodgerblue", "firebrick", "floralwhite", "forestgreen", "fuchsia", "gainsboro", "ghostwhite", "gold", "goldenrod", "gray", "green", "greenyellow", "grey", "honeydew", "hotpink", "indianred", "indigo", "ivory", "khaki", "lavender", "lavenderblush", "lawngreen", "lemonchiffon", "lightblue", "lightcoral", "lightcyan", "lightgoldenrodyellow", "lightgray", "lightgreen", "lightgrey", "lightpink", "lightsalmon", "lightseagreen", "lightskyblue", "lightslategray", "lightslategrey", "lightsteelblue", "lightyellow", "lime", "limegreen", "linen", "magenta", "maroon", "mediumaquamarine", "mediumblue", "mediumorchid", "mediumpurple", "mediumseagreen", "mediumslateblue", "mediumspringgreen", "mediumturquoise", "mediumvioletred", "midnightblue", "mintcream", "mistyrose", "moccasin", "navajowhite", "navy", "oldlace", "olive", "olivedrab", "orange", "orangered", "orchid", "palegoldenrod", "palegreen", "paleturquoise", "palevioletred", "papayawhip", "peachpuff", "peru", "pink", "plum", "powderblue", "purple", "red", "rosybrown", "royalblue", "saddlebrown", "salmon", "sandybrown", "seagreen", "seashell", "sienna", "silver", "skyblue", "slateblue", "slategray", "slategrey", "snow", "springgreen", "steelblue", "tan", "teal", "thistle", "tomato", "turquoise", "violet", "wheat", "white", "whitesmoke", "yellow", "yellowgreen"
  ]

  //renderColors(document.getElementsByClassName("colors")[0], colors);
  renderColors(document.getElementsByClassName("colors")[0], colorsExtra);
</script>

</pre>

<span class="note">[W3C](https://www.w3.org/TR/css-color-3/#svg-color)</span>

---

# Value Types: colors

<pre class="code-render" default-style="
  body { font-family: Arial, sans-serif; margin: 20px; }

  .colors {
    display: flex;
    gap: 4rem;
  }

  label { display: block; margin-bottom: 10px; }

  .box {
    width: 400px; height: 200px;
    margin: 20px 0;
    border-radius: 8px;
    border: 4px solid #333;
    display: flex;
    align-items: center;
    justify-content: center;
    background: repeating-conic-gradient(#eee 0% 25%, #fff 0% 50%) 50% / 20px 20px; /* checkerboard for alpha */
  }

  .fill {
    width: 100%; height: 100%;
    display: flex; align-items: center; justify-content: center;
    font-weight: bold; color: #000;
  }

  ul { list-style: none; padding: 0; }

  li { margin: 3px 0; font-family: monospace; margin: .5rem 0 }
" resizable="true" style="height: 800px;">

<div class="colors">
  <div class="color-group">
  <label>
    <b>Color:</b>
    <input type="color" id="colorPicker" value="#3584e4">
  </label>
  <div class="box">
    <div class="fill" id="preview">Preview</div>
  </div>
  <ul>
    <li id="hexOut">HEX:</li>
    <li id="rgbOut">RGB:</li>
    <li id="hslOut">HSL:</li>
  </ul>
  </div>
  <div class="color-group opacity">
  <label>
    <b>Transparency:</b> 
    <input type="range" id="alphaPicker" min="0" max="1" step="0.01" value="1">
  </label>
  <div class="box">
    <div class="fill" id="preview-alpha">Preview</div>
  </div>
  <ul>
    <li id="hexaOut">HEXA:</li>
    <li id="rgbaOut">RGBA:</li>
    <li id="hslaOut">HSLA:</li>
  </ul>
  </div>
</div>

<script>
function hexToRgb(hex) {
  hex = hex.replace("#", "");
  const r = parseInt(hex.substr(0,2), 16);
  const g = parseInt(hex.substr(2,2), 16);
  const b = parseInt(hex.substr(4,2), 16);
  return [r, g, b];
}

function rgbToHsl(r, g, b) {
  r /= 255; g /= 255; b /= 255;
  const max = Math.max(r, g, b), min = Math.min(r, g, b);
  let h, s, l = (max + min) / 2;
  if (max === min) { h = s = 0; }
  else {
    const d = max - min;
    s = l > 0.5 ? d / (2 - max - min) : d / (max + min);
    switch(max){
      case r: h = (g - b) / d + (g < b ? 6 : 0); break;
      case g: h = (b - r) / d + 2; break;
      case b: h = (r - g) / d + 4; break;
    }
    h /= 6;
  }
  return [Math.round(h*360), Math.round(s*100), Math.round(l*100)];
}

function updateColors() {
  const hex = document.getElementById("colorPicker").value;
  const alpha = parseFloat(document.getElementById("alphaPicker").value);
  const [r,g,b] = hexToRgb(hex);
  const [h,s,l] = rgbToHsl(r,g,b);

  // HEX
  document.getElementById("hexOut").textContent = `HEX: ${hex}`;

  // HEXA
  const hexa = hex + Math.round(alpha*255).toString(16).padStart(2,"0");
  document.getElementById("hexaOut").textContent = `HEXA: ${hexa}`;

  // RGB
  document.getElementById("rgbOut").textContent = `RGB: rgb(${r}, ${g}, ${b})`;

  // RGBA
  document.getElementById("rgbaOut").textContent = `RGBA: rgba(${r}, ${g}, ${b}, ${alpha})`;

  // HSL
  document.getElementById("hslOut").textContent = `HSL: hsl(${h}, ${s}%, ${l}%)`;

  // HSLA
  document.getElementById("hslaOut").textContent = `HSLA: hsla(${h}, ${s}%, ${l}%, ${alpha})`;

  // Preview box
  document.getElementById("preview").style.backgroundColor = `rgb(${r},${g},${b})`;
  document.getElementById("preview-alpha").style.backgroundColor = `rgba(${r},${g},${b},${alpha})`;
}

document.getElementById("colorPicker").addEventListener("input", updateColors);
document.getElementById("alphaPicker").addEventListener("input", updateColors);
updateColors();
</script>

</pre>

---

# Other Value Types (less used)...

- ***time units***
  - s (seconds), ms (milliseconds)
  - animations and transitions: `transition-duration: 200ms;`

- ***angle units***
  - used for transforms and gradients
  - `deg, grad, rad, turn`

- ***frequency, resolution, etc.***
  - `Hz`, `kHz` (frequency -- rarely used)
  - `dpi, dpcm, dppx` (resolution)

---

# Variables

- user-defined properties that start with two dashes (*--*).
- store a value (e.g. color, size, number) and can be ***reused*** within a style rule
- the value is retrieved using the *`var(--name)`* function

```css
:root {
  --main-color: #3498db;
  --padding: 1rem;
}

button {
  background-color: var(--main-color);
  padding: var(--padding);
}

button.danger {
  --main-color: #e74c3c; /* local override */
}
```

