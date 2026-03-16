<!-- .slide: class="section" -->
 
<header>
  <h1>DOM -- Document Object Model</h1>
  <p>document, dynamic elements modification</p>
</header>

---

# Document Object Model -- document

- ***window.document*** -- the root object representing the web page
- each HTML element becomes a node in a tree structure
- allows JavaScript to read, change, add, or remove content dynamically

```
Node
 ├─ Document
 ├─ Element
 │   ├─ HTMLElement
 │   │   ├─ HTMLDivElement
 │   │   ├─ HTMLParagraphElement
 │   │   ├─ HTMLButtonElement
 │   │   └─ HTMLInputElement
 │   └─ SVGElement
 └─ Text
```

MDN: [Document](https://developer.mozilla.org/en-US/docs/Web/API/Document), [Element](https://developer.mozilla.org/en-US/docs/Web/API/Element), [HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement)

---

# Query Elements

```html
<h1 id="mainTitle">Game of Thrones</h1>
<ul>
  <li class="item">Tyrion</li>
  <li class="item">Arya</li>
  <li class="item">Sansa</li>
</ul>

<script>
  const header = document.getElementById("mainTitle");

  const itemsByClass = document.getElementsByClassName("item");

  const paragraphs = document.getElementsByTagName("p");

  const firstItem = document.querySelector(".item");

  const allItems = document.querySelectorAll(".item");

  console.log(header, itemsByClass, paragraphs, firstItem, allItems);
</script>
```

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/js/query.html"></div>

<div class="note"><a href="assets/examples/js/query.html">source</a></div>

---

# Node, Element, HTMLElement

- **[Node](https://developer.mozilla.org/en-US/docs/Web/API/Node)** -- basic unit of the DOM tree, can be an element, text, comment, etc.
  - `parentNode`, `childNodes`, `nextSibling`, `previousSibling`, etc.

<br>

- **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** -- represents an HTML or XML element, inherits from *Node*
  - `tagName`, `id`, `className`, `attributes`, etc.

<br>

- **[HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement)** -- specific to HTML elements, inherits from *Element*
  - `innerHTML`, `innerText`, `style`, etc.

<br>

- other specific element types ([HTMLDivElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLDivElement), [HTMLParagraphElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLParagraphElement), etc.) inherit from *HTMLElement* and have additional properties/methods

---

# Modifying Elements

```html
<div id="box" class="container">
  <p class="text">Winter is coming!</p>
</div>

<script>
  const box = document.getElementById("box");
  const para = box.querySelector(".text");
  const btn = document.getElementById("btn");

  para.textContent = "Brace yourselves!"; // Change text content
  box.innerHTML += "<p>The North remembers.</p>"; // Change HTML

  box.style.backgroundColor = "lightblue"; // Change style
  para.style.color = "darkred";

  box.classList.add("highlight"); // Change classes
  para.classList.remove("text");
</script>
```

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/js/change.html"></div>

<div class="note"><a href="assets/examples/js/change.html">source</a></div>

---

# Append and Remove Elements

```html
<div id="box" class="container">
  <p id="note">Winter is coming!</p>
</div>

<script>
  const box = document.getElementById("box");
  const note = document.getElementById("note");

  // create new elements
  const note2 = document.createElement("p");
  note2.textContent = "Brace yourselves!";
  const img = document.createElement("img");
  img.src = "winter_is_coming.jpg";
  img.width = 200;

  // add and remove elements
  box.appendChild(note2);
  box.appendChild(img);
  note.remove();
</script>
```

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/js/append.html"></div>

<div class="note"><a href="assets/examples/js/append.html">source</a></div>