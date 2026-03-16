# Style Definition Process

  * Basic style of elements (headings, paragraphs, tables, ...) 
    * Built-in user agent style
    * Author style sheet based on the graphical design
  * Specification of details and specific cases 
    * Layout of particular elements (header, footer, ...)
    * Special cases (of tables, headings, ...)
  * We use the CSS mechanisms 
    * Cascade of rules
    * Inheritance

---

# Rule Application

  * Multiple selectors usually apply to a single element

```html
<p class="intro">Following text is
    <span class="imp">important</span></p>
``` 

```css
p.intro span { color: red; }
p span { color: blue; font-weight: bold; }
``` 

  * What color will be used to display the word ``important''?

**Side note:** The `!important` directive (**very specific use**)

```css
p.intro span { color: red; }
p span { color: blue !important; font-weight: bold; }
```
