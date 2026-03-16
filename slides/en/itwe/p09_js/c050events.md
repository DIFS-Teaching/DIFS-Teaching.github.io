<!-- .slide: class="section" -->
 
<header>
  <h1>Events</h1>
  <p>types, listeners, propagation</p>
</header>

---

# Events

- [Event](https://developer.mozilla.org/en-US/docs/Web/API/Event) -- a signal that something happened in the browser
- triggered by *user actions* or *system changes*

<br>

<div style="font-size: 1.8rem">

| Category        | Events                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 🖱️ **Mouse**   | [click](https://developer.mozilla.org/en-US/docs/Web/API/Element/click_event), [dblclick](https://developer.mozilla.org/en-US/docs/Web/API/Element/dblclick_event), [mousedown](https://developer.mozilla.org/en-US/docs/Web/API/Element/mousedown_event), [mouseup](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseup_event), [mousemove](https://developer.mozilla.org/en-US/docs/Web/API/Element/mousemove_event), [mouseenter](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseenter_event), [mouseleave](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseleave_event), [mouseover](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseover_event), [mouseout](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseout_event), [contextmenu](https://developer.mozilla.org/en-US/docs/Web/API/Element/contextmenu_event), [wheel](https://developer.mozilla.org/en-US/docs/Web/API/Element/wheel_event) |
| ⌨️ **Keyboard** | [keydown](https://developer.mozilla.org/en-US/docs/Web/API/Element/keydown_event), [keyup](https://developer.mozilla.org/en-US/docs/Web/API/Element/keyup_event), [keypress](https://developer.mozilla.org/en-US/docs/Web/API/Element/keypress_event)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| 📱 **Touch**    | [touchstart](https://developer.mozilla.org/en-US/docs/Web/API/Element/touchstart_event), [touchmove](https://developer.mozilla.org/en-US/docs/Web/API/Element/touchmove_event), [touchend](https://developer.mozilla.org/en-US/docs/Web/API/Element/touchend_event), [touchcancel](https://developer.mozilla.org/en-US/docs/Web/API/Element/touchcancel_event)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| 🖊️ **Pointer** | [pointerdown](https://developer.mozilla.org/en-US/docs/Web/API/Element/pointerdown_event), [pointerup](https://developer.mozilla.org/en-US/docs/Web/API/Element/pointerup_event), [pointermove](https://developer.mozilla.org/en-US/docs/Web/API/Element/pointermove_event), [pointerenter](https://developer.mozilla.org/en-US/docs/Web/API/Element/pointerenter_event), [pointerleave](https://developer.mozilla.org/en-US/docs/Web/API/Element/pointerleave_event), [pointerover](https://developer.mozilla.org/en-US/docs/Web/API/Element/pointerover_event), [pointerout](https://developer.mozilla.org/en-US/docs/Web/API/Element/pointerout_event), [pointercancel](https://developer.mozilla.org/en-US/docs/Web/API/Element/pointercancel_event)                                                                                                                                                                                                                    |
| 📝 **Form**     | [input](https://developer.mozilla.org/en-US/docs/Web/API/Element/input_event), [change](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/change_event), [submit](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/submit_event), [reset](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/reset_event), [focus](https://developer.mozilla.org/en-US/docs/Web/API/Element/focus_event), [blur](https://developer.mozilla.org/en-US/docs/Web/API/Element/blur_event), [focusin](https://developer.mozilla.org/en-US/docs/Web/API/Element/focusin_event), [focusout](https://developer.mozilla.org/en-US/docs/Web/API/Element/focusout_event), [select](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/select_event), [invalid](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/invalid_event)                                                                                                |
| 🎬 **Media**    | [play](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/play_event), [pause](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/pause_event), [ended](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/ended_event), [timeupdate](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/timeupdate_event), [volumechange](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/volumechange_event), [loadeddata](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/loadeddata_event)                                                                                                                                                                                                                                                                                                                                                                                              |
| 🪟 **Window**   | [load](https://developer.mozilla.org/en-US/docs/Web/API/Window/load_event), [DOMContentLoaded](https://developer.mozilla.org/en-US/docs/Web/API/Document/DOMContentLoaded_event), [resize](https://developer.mozilla.org/en-US/docs/Web/API/Window/resize_event), [scroll](https://developer.mozilla.org/en-US/docs/Web/API/Document/scroll_event), [beforeunload](https://developer.mozilla.org/en-US/docs/Web/API/Window/beforeunload_event), [unload](https://developer.mozilla.org/en-US/docs/Web/API/Window/unload_event), [hashchange](https://developer.mozilla.org/en-US/docs/Web/API/Window/hashchange_event), [popstate](https://developer.mozilla.org/en-US/docs/Web/API/Window/popstate_event), [error](https://developer.mozilla.org/en-US/docs/Web/API/Window/error_event)                                                                                                                                                                                    |

</div>

<br>

- **pointer** -- modern unified input

---

# Event Listeners

- **inline HTML**

```html
<button onclick="doSomething()">Click</button>
```

- **DOM Element property**

```js
button.onclick = doSomething; // only one event handler
```

- **[addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)** (recommended)

```js
addEventListener("click", doSomething);

addEventListener("click", (e) => {
  // another listener
});
```

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/js/events.html"></div>

<div class="note"><a href="assets/examples/js/events.html">source</a></div>

---

# Event Propagation

- when an event occurs on an element, it *travels through the DOM*

<br>

1. **capturing phase** (trickling down) -- event travels from the root down to the target element
2. **target phase** -- event reaches the element that triggered it
3. **bubbling phase** (bubbling up) -- event travels back up from target to root

<br>

- `event.`[`stopPropagation()`](https://developer.mozilla.org/en-US/docs/Web/API/Event/stopPropagation) -- it stops propagation
- `event.`[`preventDefault()`](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault) -- it prevents default action

<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/Event_bubbling">Event Bubbling</a></span>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/js/propagation.html"></div>

<div class="note"><a href="assets/examples/js/propagation.html">source</a></div>

---

# DOM Ready

- *`DOMContentLoaded`* event -- fired when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading

```html
<script>
  document.addEventListener("DOMContentLoaded", () => {
    // code to run when the DOM is ready
    const par = document.querySelector(".par");
    par.textContent = "The night is dark and full of terrors.";
  });
</script>

<!-- elements are located after the script -->
<p class="par">Winter is coming...</p>
```



