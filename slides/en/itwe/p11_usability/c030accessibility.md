<!-- .slide: class="section" -->

<header>
    <h1>Web Accessibility</h1>
    <p></p>
</header>

---

# Accessible Web

- Content should be accessible without requiring specific hardware, software, knowledge or abilities
- Up to **30% of web users** are in some way limited
    - Suboptimal technical equipment
    - Limited display capabilities
    - Health conditions
    - Insufficient experience

---

# Minority User Groups — Technology

- Users of minority operating systems and browsers
    - Not everyone has Internet Explorer
    - Far fewer have Word or Excel!
- Users of alternative display devices
    - PDAs, smartphones
- Owners of outdated computers
    - Older software versions
    - Low screen resolution
    - Poor or no colour support

---

# Minority User Groups — Disabilities

- People with dyslexia
    - Do not read poorly structured or long texts
- Colour-blind users (even partially)
    - Struggle to perceive low contrasts
    - E.g. links distinguished only by a colour shade
- Visually impaired users
    - Require the ability to increase text size
- Users with physical disabilities
    - E.g. unable to use a mouse

---

# Rules for Accessible Web Creation

- International
    - [W3C](https://www.w3.org/) — [Web Content Accessibility Guidelines 2.1](https://www.w3.org/TR/WCAG21/) (WCAG)
- Czech legislation
    - [Act No. 99/2019 Coll.](https://www.zakonyprolidi.cz/cs/2019-99) on the accessibility of websites and mobile applications
        - Essentially an application of WCAG 2.1 rules
    - Follows on from Act No. 365/2000 Coll. on public administration information systems —
        [http://www.pravidla-pristupnosti.cz/](http://www.pravidla-pristupnosti.cz/)

---

# Mandatory Subjects (Czech Law)

The law defines mandatory subjects:

- Territorial self-governing unit
- Legal entity established by law
- Legal entity established or founded by the state or a territorial self-governing unit to satisfy needs in the general interest, financed predominantly from public funds
- A legal entity established by the above
- Voluntary union of municipalities
- University, school and school facility
- Qualified administrator of an electronic identification system

Most of these rules are also well applicable to other websites and will significantly improve their quality.

---

# WCAG Principles

- **Perceivable**
- **Operable**
- **Understandable**
- **Robust**

<span class="note">R. Pavlíček: <a href="https://poslepu.cz/web-content-accessibility-guidelines-wcag-seznamte-se-prosim/">WCAG introduction (in Czech)</a></span>

---

# Perceivable

- Provide **text alternatives** for non-text content.
- Provide **captions and alternatives** for audio and video content.
- Create **adaptable content** that can be processed by assistive technologies.
    - Responsive design is required
        - According to WCAG, a page must work at 320 px width (some users zoom in)
    - [ARIA attributes](https://jecas.cz/aria) (also in previous lecture)
- Ensure **sufficient contrast** between foreground and background so that things are easy to see and hear.

---

# Operable

- Ensure everything is **accessible from the keyboard**.
- Give users **enough time** to read and interact with page content.
- Do not use content that may cause **seizures**.
- Help users with **navigation and finding** content.
- **Make it easy for users to operate the site with various input devices** (not just the keyboard).

---

# Understandable

- Write text so that it is **readable and comprehensible**.
- Create content so that it **displays and behaves** as the user expects.
- Help users **avoid and correct mistakes**.

---

# Robust

- Ensure **maximum compatibility** with current and future technologies, including assistive technologies.

---

# Best Practice

1. Design the site as accessible from the very beginning
2. Build a skeleton (content structure and navigation) without defining the visual appearance
    - Clean (X)HTML with structural markup and attributes only
    - Maximum use of semantic elements (`header`, `footer`, `section`, ...)
3. Add helper links (e.g. skip navigation)
4. Test the usability of navigation without CSS (e.g. with `lynx`)
5. Define the appearance with CSS and hide helper links
    - If the HTML had to be changed, go back to step 4
6. Insert the actual content
7. Throughout the entire process, follow the rules described above

<span class="note"><a href="https://prirucky.ipk.nkp.cz/pristupnost/kontrolni_seznam_pro_overovani">Accessibility checklist</a></span>
<span class="note">Eva Cerniňáková: <a href="https://prirucky.ipk.nkp.cz/pristupnost/start">Accessible Web Pages (in Czech)</a></span>

---

# Auxiliary Content

For users with a screen reader:

- Helper links at the beginning of the page
    - Skip navigation, jump to main content (a reasonable number)
    - `<a href="#content" class="sr-only">Skip to main content</a>`
- Helper headings
    - Label sections that are otherwise distinguished only visually
    - E.g. *"Main menu"*

---

# Hiding Content

- **Completely hidden** (sections that should not currently be shown)
    - `display: none;`
    - `visibility: hidden;`
    - Content is not shown; screen readers will not read it

---

# Hiding Content from Screen Only

For helper links and similar elements that should still be read by assistive technologies:

- Absolute positioning outside the viewport
- Not shown on screen, but screen readers will read it

```html
<a href="#content" class="sr-only">Skip navigation</a>
```

```css
.sr-only {
    position: absolute;
    top: -500px;
    left: 0;
    width: 1px;
    height: 1px;
    overflow: hidden;
}
```

---

# References

- Web Content Accessibility Guidelines  
  [https://www.w3.org/TR/WCAG21/](https://www.w3.org/TR/WCAG21/)
- Accessible web pages — a guide for libraries  
  [https://prirucky.ipk.nkp.cz/pristupnost/start](https://prirucky.ipk.nkp.cz/pristupnost/start)
- Web Content Accessibility Guidelines (WCAG): an introduction  
  [https://poslepu.cz/web-content-accessibility-guidelines-wcag-seznamte-se-prosim/](https://poslepu.cz/web-content-accessibility-guidelines-wcag-seznamte-se-prosim/)
- WAVE Web Accessibility Evaluation Tool  
  [https://wave.webaim.org/](https://wave.webaim.org/)
