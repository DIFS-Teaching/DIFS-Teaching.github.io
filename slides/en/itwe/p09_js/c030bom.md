<!-- .slide: class="section" -->
 
<header>
  <h1>BOM -- Browser Object Model</h1>
  <p>window, navigator, location, history, screen, dialogs</p>
</header>

---

# Browser Object Model -- window

  - provides JavaScript access to browser-specific objects, outside the DOM
  - enables interaction with the browser environment

- **[window](https://developer.mozilla.org/en-US/docs/Web/API/Window)** -- the global object representing the browser window
  - [document](https://developer.mozilla.org/en-US/docs/Web/API/Document) -- document content (DOM)
  - [navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator) -- information about the browser
  - [location](https://developer.mozilla.org/en-US/docs/Web/API/Location) -- URL info and navigation
  - [history](https://developer.mozilla.org/en-US/docs/Web/API/History) -- browser history manipulation
  - [screen](https://developer.mozilla.org/en-US/docs/Web/API/Screen) -- screen resolution and display info
  - [alert()](https://developer.mozilla.org/en-US/docs/Web/API/Window/alert), [confirm()](https://developer.mozilla.org/en-US/docs/Web/API/Window/confirm), [prompt()](https://developer.mozilla.org/en-US/docs/Web/API/Window/prompt), [setTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/Window/setTimeout) -- simple dialog boxes
  - ...

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window)</span>

---

# Hello World

```js
  /* Write "Hello, World!" to the console */
  window.console.log("Hello, World!");

  /* Write "Hello, World!" to the document */
  window.document.write("Hello, World!");
```

- `window` is the global object, so we can omit it:

```js
  console.log("Hello, World!");
  document.write("Hello, World!");
```

- vypíše se "Hello, World!" do konzole a do dokumentu (na stránku)

<pre class="code-render" default-style="

" resizable="true" style="height: 200px;">

<script>
  console.log("Hello, World!");
  document.write("Hello, World!");
</script>

</pre>

---

# Navigator

- provides information about the browser and environment

```js
document.write(navigator.appName);    // "Netscape" in modern browsers (legacy value)
document.write(navigator.appVersion); // detailed version info, e.g. "5.0 (Windows)"
document.write(navigator.userAgent);  // detailed user agent string
document.write(navigator.platform);   // platform info, e.g. "Win32", "MacIntel", "Linux x86_64"
document.write(navigator.language);   // browser language, e.g. "en-US"
document.write(navigator.onLine);     // boolean indicating if the browser is online
```

<pre class="code-render" default-style="" resizable="true" style="height: 470px;">

<script>
  document.write(`<p>${navigator.appName}</p>`);
  document.write(`<p>${navigator.appVersion}</p>`);
  document.write(`<p>${navigator.userAgent}</p>`);
  document.write(`<p>${navigator.platform}</p>`);
  document.write(`<p>${navigator.language}</p>`);
  document.write(`<p>${navigator.onLine}</p>`);
</script>

</pre>

<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/API/Navigator">MDN</span>

---

# Location

- represents the current URL of the window

```js
document.write(window.location.href);     // full URL
document.write(window.location.protocol); // "http:" or "https:"
document.write(window.location.host);     // "example.com:8000"
document.write(window.location.pathname); // "/page.html"
document.write(window.location.hash);     // "#section1"
```

<pre class="code-render" default-style="

" resizable="true" style="height: 450px;">

<script>
  document.write(`<p>${window.location.href}</p>`);     // full URL
  document.write(`<p>${window.location.protocol}</p>`); // "http:" or "https:"
  document.write(`<p>${window.location.host}</p>`);     // "example.com:8000"
  document.write(`<p>${window.location.pathname}</p>`); // "/page.html"
  document.write(`<p>${window.location.hash}</p>`);     // "#section1"
</script>

</pre>

<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/API/Location">MDN</span>

---

# Location: redirection

- change the URL and navigate to a different page

```js
window.location.href = "https://www.example.com";
```

<pre class="code-render" default-style="
button {
  padding: 10px 20px;
  font-size: 32px;
  cursor: pointer;
}
" resizable="true" style="height: 450px;">

<script>
  function redirect() {
    window.location.href = "https://www.example.com";
  }
</script>

<button onclick="redirect()">Redirect to example.com</button>

</pre>

---

# History

- allows manipulation of the browser history stack

```js
window.history.back();    // go back one page
window.history.forward(); // go forward one page
window.history.go(-2);   // go back two pages
window.history.go(1);    // go forward one page
```

<pre class="code-render" default-style="

button {
  padding: 10px 20px;
  font-size: 32px;
  cursor: pointer;
}

" resizable="true" style="height: 200px;">


<button
  onclick="window.location.href=window.location.origin +
          '/assets/examples/js/back.html'">Redirect to back.html
</button>
<button onclick="window.history.forward()">forward()</button>

</pre>

- example: [back.html](assets/examples/js/back.html) and [forward.html](assets/examples/js/forward.html)

<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/API/History">MDN</span>

---

# Screen

- provides information about the user's screen and display capabilities

```js
document.write(screen.width);        // total screen width
document.write(screen.height);       // total screen height
document.write(screen.availWidth);   // available width (excluding taskbar, etc.)
document.write(screen.availHeight);  // available height
document.write(screen.colorDepth);   // color depth in bits
document.write(screen.pixelDepth);   // pixel depth in bits
```

<pre class="code-render" default-style="" resizable="true" style="height: 500px;">
<script>
  document.write(`<p>Width: ${screen.width}</p>`);        // total screen width
  document.write(`<p>Height: ${screen.height}</p>`);       // total screen height
  document.write(`<p>Available Width: ${screen.availWidth}</p>`);   // available width (excluding taskbar, etc.)
  document.write(`<p>Available Height: ${screen.availHeight}</p>`);  // available height
  document.write(`<p>Color Depth: ${screen.colorDepth}</p>`);   // color depth in bits
  document.write(`<p>Pixel Depth: ${screen.pixelDepth}</p>`);   // pixel depth in bits
</script>
</pre>

<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/API/Screen">MDN</span>

---

# Dialogs

```js
alert("Winter is coming!");

let ready = confirm("Are you ready to enter Westeros?");
if (ready) {
  let name = prompt("What is your name?");
  alert(`Welcome, ${name}!`);
} else {
  alert("Come back later!");
}
```

- dialogs are blocked in `iframe` -- [run example](assets/examples/js/dialogs.html)

<br>

- blocking and inflexible -- freeze the page, cannot be styled or customized
- legacy and unreliable -- often restricted or blocked (iframes, sandbox, modern browsers)

<br>

- alternative: custom modals or the modern *`<dialog>`* element -- non-blocking, fully stylable, and more reliable

<span class="note">
  <a href="https://developer.mozilla.org/en-US/docs/Web/API/Window/alert">MDN Dialogs</a>
</span>
