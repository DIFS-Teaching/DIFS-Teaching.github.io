# Mechanical Soup

- ``Browser'' automation for [BeautifulSoup](#/beautifulsoup)
	- [Project pages](https://github.com/MechanicalSoup/MechanicalSoup)
- Classes and methods that simulate basic HTTP operations
	- ``Clicking on links'' -- getting the target and generating a GET request
	- ``Form filling'' -- getting the `action` and `method`, filling in the field values and sending the corresponding HTTP request.
- JavaScript is not supported

---

# Puppeteer
- A Chrome browser remotely controlled from node.js\
  https://github.com/puppeteer/puppeteer
- We can control the browser navigation
	- Entering URLs, clicking on links, filling out forms
	- [API documentation](https://github.com/puppeteer/puppeteer/blob/v5.3.1/docs/api.md)
- Execution of JS code in the browser context (`page.evaluate()`)
	- E.g. for extracting data from DOM

---

# Puppeteer Pros & Cons
- \+ Browser navigation <!-- .element: class="plus" -->
- \+ Convenient data extraction <!-- .element: class="plus" -->
	- DOM, CSS Selectors, [**XPath**](#/xpath), any JavaScript code
- \- Time and space demanding solution <!-- .element: class="minus" -->
	- The entire Chrome is started
- \- Challenging handling of external conditions <!-- .element: class="minus" -->
	- E.g. race conditions, regional variants of the pages, ...
- \- Difficult debugging <!-- .element: class="minus" -->
	- A part of the JS code runs in node.js, another part in the browser (different contexts)
