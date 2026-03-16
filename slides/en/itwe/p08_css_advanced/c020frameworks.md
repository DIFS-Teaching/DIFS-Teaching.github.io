<!-- .slide: class="section" -->
 
<header>
  <h1>CSS Frameworks</h1>
  <p>Component and Utility Based</p>
</header>

---

# Motivation

- **a pre-prepared set of CSS (and sometimes JavaScript) files that provides:**
  - predefined styles for layout, typography, and UI components
  - reusable design patterns to speed up development
  - responsive and cross-browser compatibility out of the box

<br>

- **goal:**
  - *speed up* development
  - ensure *consistent design* across pages and projects
  - promote *responsive* and *cross-browser* layouts
  - *reduce repetitive* CSS from scratch

---

# Type 1: Component-based Frameworks

  - provides ready-made UI components (buttons, forms, navigation, cards…)
  - **[Bootstrap](https://getbootstrap.com/)**, **[Foundation](https://get.foundation/)**, **[Bulma](https://bulma.io/)**, **[Materialize](https://materializecss.com/)**
  - 🟢 **advantages:**
    - quickly use pre-built elements
    - consistent look across the project
    - great for rapid prototyping
  - 🔴 **disadvantages:**
    - less flexibility -- customizing components for unique designs can be harder

=--

# Bootstrap

- [getbootstrap.com](https://getbootstrap.com/), MIT License
- popular front-end framework with CSS, JS components, and responsive grid
- 🟢 **advantages:**
  - fast development, responsive layouts, consistent design, large community
- 🔴 **disadvantages:**
  - can be bloated, sites may look similar, custom overrides can be tricky

<br>

- **[components](https://getbootstrap.com/docs/5.3/components/)**, **[layout](https://getbootstrap.com/docs/5.3/layout/grid/)**

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/frameworks/bootstrap.html"></div>

<div class="note"><a href="assets/examples/frameworks/bootstrap.html">source</a></div>

=--

# Foundation

- [get.foundation](https://get.foundation), MIT License
- responsive front-end framework with grid system, UI components, and accessibility features
- 🟢 **advantages:**
  - mobile-first, fully responsive layouts
  - strong focus on accessibility (A11y)
  - flexible grid and UI components
  - modular -- include only what you need
- 🔴 **disadvantages:**
  - smaller community than Bootstrap
  - slightly steeper learning curve
  - can be heavy if not customized

<br>

- **[Kitchen Sink](https://get.foundation/sites/docs/kitchen-sink.html)**

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/frameworks/foundation.html"></div>

<div class="note"><a href="assets/examples/frameworks/foundation.html">source</a></div>

=--

# Bulma

- [bulma.io](https://bulma.io), MIT License
- modern CSS-only framework based on Flexbox, providing responsive grid, UI components, and utilities
- 🟢 **advantages:**
  - lightweight and easy to use, no JavaScript required
  - modern Flexbox-based grid system
  - clean, minimalistic design
  - modular -- import only what you need
- 🔴 **disadvantages:**
  - lacks built-in JS components (requires custom JS for interactivity)
  - smaller community compared to Bootstrap
  - may require writing JS for interactive elements

<br>

- **[components](https://bulma.io/documentation/components/)**, **[comparison with Bootstrap](https://bulma.io/alternative-to-bootstrap/)**

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/frameworks/bulma.html"></div>

<div class="note"><a href="assets/examples/frameworks/bulma.html">source</a></div>

=--

# Materialize

- [materializecss.com](https://materializecss.com), MIT License
- front-end framework based on Google’s Material Design, providing CSS, JavaScript components, responsive grid, and UI elements
- 🟢 **advantages:**
  - built-in Material Design aesthetics
  - responsive grid system and prebuilt UI components
  - includes JavaScript components (modals, dropdowns, tooltips, sidenav, etc.)
  - easy to use for prototyping and consistent design
- 🔴 **disadvantages:**
  - can be heavier due to combined CSS + JS
  - design is opinionated -- may require overrides for custom look
  - smaller community than Bootstrap

<br>

- **[components](https://materializecss.com/badges.html)**

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/frameworks/materialize.html"></div>

<div class="note"><a href="assets/examples/frameworks/materialize.html">source</a></div>

---

# Type 2: Utility-based Frameworks

  - provides small, reusable classes that define a single property (e.g., `text-center`, `p-4`,<br> `bg-gray-200`)
  - **[Tailwind CSS](https://tailwindcss.com/)**
  - 🟢 **advantages:**
    - high flexibility – build custom UI without writing new CSS
    - minimizes the need to write custom styles
  - 🔴 **disadvantages:**
    - can lead to long class lists in HTML
    - requires careful planning of naming and structure

=--

# Tailwind CSS

- [tailwindcss.com](https://tailwindcss.com), MIT License
- utility-first CSS framework providing small, composable classes for styling directly in HTML; highly configurable and responsive
- 🟢 **advantages:**
  - high flexibility – build custom designs without writing custom CSS
  - utility classes promote consistency and reuse
  - responsive design and pseudo-class variants built-in (sm:, md:, hover:, etc.)
  - large community and rich ecosystem (plugins, components, templates)
- 🔴 **disadvantages:**
  - long class lists in HTML can reduce readability
  - steeper learning curve for beginners unfamiliar with utility-first approach
  - requires build tools (PostCSS, CLI, or CDN) for best performance

<br>

- **[styling with utility classes](https://tailwindcss.com/docs/styling-with-utility-classes)**

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/frameworks/tailwind.html"></div>

<div class="note"><a href="assets/examples/frameworks/tailwind.html">source</a></div>

---

# Drawbacks

- **bloat / Large size** -- many unused styles increase CSS size
- **learning curve** -- must learn framework classes and grid system
- **reduced flexibility** -- prebuilt components can limit custom design
- **uniform look** -- default components make sites look similar
- **dependency** -- tied to framework versions and updates
- **HTML clutter** -- long class lists reduce readability
- **performance** -- extra unused styles may slow down pages