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
    padding-top: 30px;
}
``` 

<p style="padding: 1em;">
<a href="#" style="background: #eeeeff url('assets/newwin32.png') top right no-repeat; padding-right: 35px; padding-top: 30px;">Click me</a>
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
ul.hlist li { display: inline; }
```
```html
<ul class="hlist">
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>
``` 

<pre class="code-render" class="col" default-style="
body {
   font-family: sans-serif;
}
ul.hlist li { display: inline; }
" resizable="false" style="padding: 0; height: 5em">
<ul class="hlist">
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>
</pre>

---

# Horizontal list

```css
ul.hlist li { display: inline-block; }
```
```html
<ul class="hlist">
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>
``` 

<pre class="code-render" class="col" default-style="
body {
   font-family: sans-serif;
}
ul.hlist li { display: inline-block; }
" resizable="false" style="padding: 0; height: 5em">
<ul class="hlist">
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>
</pre>

---

# Image sprites

- Multiple images in one larger image
- The individual images are extracted using the background positioning
- Fewer HTTP requests (less relevant with HTTP/2)
- [Image sprite 1](https://difs-teaching.github.io/slides/en/itwe/p06_page_layout/assets/examples/imageSprite.png)
- [Image sprite 2](https://difs-teaching.github.io/slides/en/itwe/p06_page_layout/assets/examples/imageSprite2.png)

---

# Image sprites (II)

- [Example 1](https://difs-teaching.github.io/slides/en/itwe/p06_page_layout/assets/examples/sprite1.html)

```css
a.smile { background: url("imageSprite.png") -315px -28px; }
a.smile:hover { background: url("imageSprite.png") -341px -28px; }

a.del { background: url("imageSprite.png") -269px -52px; }
a.del:hover { background: url("imageSprite.png") -269px -68px; }
``` 

- [Example 2](https://difs-teaching.github.io/slides/en/itwe/p06_page_layout/assets/examples/sprite2.html)

