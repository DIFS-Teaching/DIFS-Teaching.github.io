<!-- .slide: class="section" -->

# Selected CSS Solutions

---

# Using Icons

```html
<a href="#">Click me</a>
``` 

```css
a {
    background: #eeeeff url('newwin32.png') top right no-repeat;
    padding-right: 35px;
    padding-top: 35px;
}
``` 

<p style="padding: 1em;">
<a href="#" style="background: #eeeeff url('https://raw.githubusercontent.com/DIFS-Teaching/slides/refs/heads/main/en/itwe/p06_page_layout/assets/newwin32.png') top right no-repeat; padding-right: 35px; padding-top: 30px;">Click me</a>
</p>

---

# Horizontal list

```html
<ul>
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>
``` 

<pre class="code-render" class="col" default-style="
body {
   font-family: sans-serif;
}
" resizable="false" style="padding: 0; height: 5em">
<ul>
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>
</pre>

---

# Horizontal list

```css
ul.vertlist1 li { display: inline; }
```
```html
<ul class="vertlist">
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>
``` 

<pre class="code-render" class="col" default-style="
body {
   font-family: sans-serif;
}
ul.vertlist li { display: inline; }
" resizable="false" style="padding: 0; height: 5em">
<ul class="vertlist">
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>
</pre>

---

# Horizontal list

```css
ul.vertlist1 li { display: inline-block; }
```
```html
<ul class="vertlist">
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>
``` 

<pre class="code-render" class="col" default-style="
body {
   font-family: sans-serif;
}
ul.vertlist li { display: inline; }
" resizable="false" style="padding: 0; height: 5em">
<ul class="vertlist">
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>
</pre>

---

# Image sprites

- More images in one larger image
- The individual images are extracted using the background positioning
- More efficient and smooth user experience
- [Image sprite 1](assets/examples/imageSprite.png)
- [Image sprite 2](assets/examples/imageSprite2.png)

---

# Image sprites (II)

- [Example 1](assets/examples/sprite1.html)

```css
a.smile { background: url("imageSprite.png") -315px -28px; }
a.smile:hover { background: url("imageSprite.png") -341px -28px; }

a.del { background: url("imageSprite.png") -269px -52px; }
a.del:hover { background: url("imageSprite.png") -269px -68px; }
``` 

- [Example 2](assets/examples/sprite2.html)

