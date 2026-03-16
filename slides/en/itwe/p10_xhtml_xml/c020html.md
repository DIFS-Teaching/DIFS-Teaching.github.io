# Multimedia `<audio>`

  - The `controls` attribute displays the controls (play, stop, pause)
  - JavaScript API for controlling the playback

```html
<audio controls>
   <source src="sound.ogg" type="audio/ogg">
   <source src="sound.mp3" type="audio/mpeg">
   Audio is not supported.
</audio>
``` 

<audio controls>
   <source src="https://www.fit.vut.cz/study/course/ITW/public/assets/sample-5.ogg" type="audio/ogg">
   Audio is not supported.
</audio>


  - Different supported formats and codecs (MP3, WAW, OGG, ...)
  - Browser-dependent 

---

# Multimedia `<video>`

```html
<video controls height="240" width="320">
   <source src="file.mp4" type="video/mp4">
   <source src="file.ogg" type="video/ogg">
   Video is not supported.
 </video>
``` 

<video controls height="480" width="640" style="position: absolute; right: 5em; bottom: 3em;">
   <source src="https://www.fit.vut.cz/study/course/ITW/public/assets/sample-5.mp4" type="video/mp4">
   Video is not supported.
 </video>

  - Different supported formats and codecs (MP4, WebM, OGG, ...)
  - Browser-dependent 

---

# Vector Graphics `<svg>`

  - SVG a MathML may be included directly in the document
    - with `xmlns` *namespace definition* optional in HTML
    - note the XML syntax discussed later

<pre class="code-render" default-style="" resizable="false" style="width: 400px; height: 270px; float: right; z-index: 1; margin: 2rem">
 <svg height="120"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="50" fill="red" />
  <rect x="80" y="20" height="60" width="60"
        style="stroke:none; fill:#00ff00;
        fill-opacity: 0.5;" />
</svg> 
</pre>

```xml
<svg height="120" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="50" fill="red" />
  <rect x="80" y="20" height="60" width="60"
        style="stroke:none; fill:#00ff00;
        fill-opacity: 0.5;" />
</svg> 
```

  - Or use the SVG files as any other image

```html
<img width="200" height="120" src="figure.svg">
```

<span class="note">See details on <a href="https://developer.mozilla.org/en-US/docs/Web/SVG">MDN</a></span>

---

# Inline frame

<iframe width="800" height="400" src="assets/examples/iframedoc.html" sandbox="allow-scripts allow-same-origin allow-popups allow-forms">
Inline frames are not supported.
</iframe>

<div class="">

```html
<iframe width="400" height="400" src="iframedoc.html">
Inline frames are not supported.
</iframe>
```

- Document is displayed in a separate context; it should not be able to access or influence the parent document.

</div>

---

# Microdata

  - A possible way of adding semantics to the elements
  - For futher automated processing
  - Attributes: 
    - **itemscope** – item set container
    - **itemprop** – a property
    - **itemtype** – element type denoted as URL
    - **itemid** – a global identifier (e.g. ISBN for books)
    - **itemref** – global identifier reference

---

# Microdata (II)

  - Example
  
```html
<div itemscope="" itemtype="http://example.org/person">
 <p>My name is <span itemprop="name">John</span>.</p>
 <p>My surname is <span itemprop="surname">Smith</span>.</p>
 <p>I was born in <span itemprop="born-city">Brně</span>.</p>
</div>
```
