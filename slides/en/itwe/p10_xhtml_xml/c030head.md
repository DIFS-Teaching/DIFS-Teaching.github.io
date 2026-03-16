<!-- .slide: class="section" -->

# Document header: Metadata and relations

---

# Link relations

  - Adds _semantics_ to links -- the purpose of the link
  - Applicable to the `<link>` and `<a>` elements


  - A link to an external resource – adding related contents to a document

```html
<link rel="stylesheet"  href="style.css" type="text/css">
``` 
    
 - Hyperlink – navigation to another document 


```html
<a rel="next" href="slide010.html">next</a>
```

---

# Link relations (II)

  - Some interesting _rel_ values: 
    - **author**
    - **alternate** \-- alternative version (RSS, mobile, etc.)
    - **external** \-- external resources
    - **licence** \-- content license
    - **tag** \-- tag page (e.g. blogs)
    - **search** \-- search page
    - **first, last** \-- first, last document in a set
    - **prev, next** \-- previous, next document in a set
    - **up, down** \-- hierarchical navigation

<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/rel">Complete reference on MDN</a></span>

---

# Page icon

  - Displayed in the URL field, in bookmarks, ...
  - A file in ICO format stored on server
  - Specification in document header:
  
```html
<link rel="icon" href="favicon.ico" type="image/x-icon">
``` 

  - Most browsers automaticaly look for a **favicon.ico** file in the server root directory even without this specification
  - Other image formats may be supported (SVG, PNG, ...)
  - Multiple icons may be provided, the browsers chooses the last usable one.

---

# RSS and ATOM export

  - XML languages for content syndication
  - Allows to subscribe to new content via a client software
    - A [standalone application](https://play.google.com/store/apps/details?id=com.vanniktech.rssreader) or a [browser extension](https://chromewebstore.google.com/detail/rss-feed-reader/pnjaodmkngahhkoihejjehlcdlnohgmp)

```html
 <link rel="alternate"
      type="application/atom+xml"
      title="Feed of recent questions"
      href="/feeds">

<link rel="alternate"
      type="application/rss+xml"
      title="Top News"
      href="http://my-web.com/rss/index.php"> 
```

---

# Meta information

  - Meta information -- additional information about the document itself
  - Always in the document header
  - Two possible variants: 
    - User information
        ```html
        <meta name="..." content="...">
        ```

    - HTTP header equivalent
        ```html
        <meta http-equiv="..." content="...">
        ```

---

# User information

  - Document description 

```html
<meta name="description" content="Short description">
```
  - Keywords 
  
```html
<meta name="keywords" content="WWW, HTML, pages, design">
```

  - Document author 
  
```html
<meta name="author" content="John Smith, john@smith.org">
```

---

# User information (II)

  - Generator (software)
```html
<meta name="generator" content="Mozilla Composer">
```
  - Information for indexing robots
```html
<meta name="robots" content="index,follow">
<meta name="robots" content="noindex,nofollow"> 
```
  - Responsive design settings
```html
<meta name="viewport" content="width=device-width">
<meta name="viewport" content="user-scalable=no, initial-scale=1"> 
 ```

---

# Facebook meta tags

  - Tags for the Facebook Open Graph Protocol
  - Allows to specify metadata for page sharing 
  
```html
<meta property="og:title" content="Page Title">
<meta property="og:description" content="Page description">
<meta property="og:site_name" content="my-website.com">
<meta property="og:url" content="http://my-website.com/info/">
<meta property="og:image"
      content="http://my-website.com/thumbnail.jpg">
<meta property="og:type" content="article">
```

---

# HTTP equivalents

  - The same iformation as in HTTP headers
  - No access to the server configuration needed
  - Content type = MIME type + encoding 
```html
<meta http-equiv="content-type" content="text/html; charset=utf-8">
```
  - Content language
```html
<meta http-equiv="content-language" content="en">
```

---

# Redirect

  - After displaying a page, another document is automaticaly displayed after the specified time
  - E.g. redirect to IMDB.com after 6 seconds 

```html
<meta http-equiv="refresh" content="6;URL=https://www.imdb.com/">
```

---

# Cache control

  - Controls whether to store or not to store the document in cache
  - Influences just the browser cache

```html
<meta http-equiv="cache-control" content="cache">

<meta http-equiv="cache-control" content="no-cache">
```

  - Cache expiration

```html
<meta http-equiv="expires" content="Wed 19 Nov 2025 16:10:00">
```

  - After this date, the page should be removed from cache
