<!-- .slide: class="section" -->
 
<header>
  <h1>Dynamic Data Fetch</h1>
  <p>fetch</p>
</header>

---

# Fetch API

- API for HTTP requests, replaces older [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) (XHR)
- Based on [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- Works with JSON, text, files, APIs

```js
fetch(url, options)
  .then(response => {
    // handle HTTP response
    return response.json();
  })
  .then(data => {
    // work with data
    console.log(data);
  })
  .catch(error => {
    // handle network errors
    console.error(error);
  });

```

<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API">MDN</a><span>

---

# Fetch Request

- interface of the Fetch API which represents a resource request
- used to ask for data or send data (GET = retrieve, POST/PUT = send/update, DELETE)

```js
fetch("/api/users", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "Authorization": "Bearer token123"
    },
    body: JSON.stringify({
      name: "Jon Snow",
      role: "Knights Watch"
    }),
    credentials: "include"
});
```

<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/API/Request">MDN</a></span>

---

# Fetch Response

- interface of the Fetch API represents the response to a request

<br>

- `response.`*`ok`* -- true if status 200–299
- `response.`*`status`* -- HTTP status code (200, 404, 500 …)
- `response.`*`statusText`* -- status message ("OK", "Not Found")
- `response.`*`type`* -- basic / cors / opaque

<br>

- `response.`*`json()`* -- parses JSON data
- `response.`*`text()`* -- gets response as text
- `response.`*`blob()`* -- gets binary data (images, files)
- `response.`*`formData()`* -- gets form submissions
- `response.`*`arrayBuffer()`* -- gets low-level binary data

<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/API/Response">MDN</a></span>

---

# Async + await

- cleaner syntax for working with Promises
- try/catch for error handling

```js
async function query() {
  try {
    const response = await fetch(url, options);
    
    if (!response.ok) {
      throw new Error("HTTP error");
    }
    
    const data = await response.json();
    console.log(data);
  
  } catch (error) {
    console.error(error);
  }
}

query().then(() => { ... });
```

<span class="note"><a href="https://restcountries.com/v3.1/all?fields=name&fields=cca3">restcountries.com API</a></span>

---

# Example: then()

```js
fetch("https://restcountries.com/v3.1/all?fields=name&fields=cca3")
  .then(response => {
    if (!response.ok) {
      throw new Error("HTTP error");
    }
    return response.json();
  })
  .then(countries => {
    console.log(countries);
  })
  .catch(error => {
    console.error(error);
  });
```

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/js/fetch_then.html"></div>

<div class="note"><a href="assets/examples/js/fetch_then.html">source</a></div>

---

# Example: async + await

```js
async function fetchCountries() {
  try {
    const response = await fetch("https://restcountries.com/v3.1/all?fields=name&fields=cca3");
    
    if (!response.ok) {
      throw new Error("HTTP error");
    }
    
    const countries = await response.json();
    console.log(countries);
  
  } catch (error) {
    console.error(error);
  }
}

fetchCountries();
```

<span class="note"><a href="https://restcountries.com/v3.1/all?fields=name&fields=cca3">restcountries.com API</a></span>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/js/fetch_await.html"></div>

<div class="note"><a href="assets/examples/js/fetch_await.html">source</a></div>

---

# Example: Endless Page

<!-- .slide: class="editor" -->

<div data-iframe="assets/examples/js/endless.html"></div>

<div class="note"><a href="assets/examples/js/endless.html">source</a></div>
