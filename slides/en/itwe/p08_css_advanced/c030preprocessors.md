<!-- .slide: class="section" -->
 
<header>
  <h1>CSS Preprocessors</h1>
  <p>Variables, Scopes, Mixins</p>
</header>

---

# Motivation

- scripting / meta languages that compile to CSS
- extends CSS with variables, nesting, mixins, functions, and more

<br>

- 🟢 **goals:**
  - variables for consistent values (colors, fonts, spacing)
  - nesting for clearer structure
  - mixins and functions for reusable code
  - logic and operations (loops, conditionals)
  - modular code via imports

<br>

- **[Sass](https://sass-lang.com/)** / SCSS – most widely used, mature, supports variables, nesting, mixins, functions
- **[LESS](https://lesscss.org/)** – similar to Sass, integrates well with JavaScript
- **[Stylus](https://stylus-lang.com/)** – highly flexible, minimal syntax, supports both indented and CSS-like style

---

# Variables

**[Sass variables](https://sass-lang.com/documentation/variables/)**

<div style="width: 50%; height: 500px; float: right; z-index: 1; position: relative">

```css
body {
  color: #333;
  font-family: Arial, sans-serif;
}

.button {
  background-color: #3498db;
  padding: 16px;
  border-radius: 4px;
}
```

</div>

```sass
$primary-color: #3498db;
$text-color: #333;
$spacing: 16px;

body {
  color: $text-color;
  font-family: Arial, sans-serif;
}

.button {
  background-color: $primary-color;
  padding: $spacing;
  border-radius: 4px;
}
```

- Sass variables are compile-time only, while CSS variables work at runtime and can change dynamically in the browser

---

# Nesting

- **[Sass nesting](https://sass-lang.com/documentation/style-rules/)**

<div style="width: 50%; height: 500px; float: right; z-index: 1; position: relative">

```css
.nav { background: #333; }
.nav a { color: white; }
.nav a:hover { color: yellow; }
```

</div>

```sass
.nav {
  background: #333;

  a {
    color: white;

    &:hover {
      color: yellow;
    }
  }
}
```

- Sass nesting is compiled and more permissive, while CSS nesting is native but has stricter syntax rules.
  - **[CSS Nesting Level 1](https://drafts.csswg.org/css-nesting-1/)** (Editor’s Draft) -- [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Nesting)

---

# Mixins

- **[Sass mixins](https://sass-lang.com/documentation/at-rules/mixin/)**

<div style="width: 50%; height: 500px; float: right; z-index: 1; position: relative">

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 200px;
  background-color: #3498db;
}
```

</div>

```sass
@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  @include flex-center;
  height: 200px;
  background-color: #3498db;
}
```

- mixins exist in preprocessors like Sass, but CSS has no native mixins