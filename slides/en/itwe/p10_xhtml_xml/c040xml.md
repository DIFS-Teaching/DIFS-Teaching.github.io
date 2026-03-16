<!-- .slide: class="section" -->

# Alternatives to HTML: XML and XHTML

---

# XML and XHTML

  - **XML**
    - A general standard for data and document exchange
    - Syntactically similar to HTML, does not define the meaining of the tags (it depends on the particular application)
  - **XHTML**
    - The application of XML for web pages
    - Replace HTML with XML
    - Tag names and their meaning equal to HTML, syntax is XML

---

# Advantages of XML

  - Simple implementation 
    - The language is not so complex
    - Quite easy to process
  - It is possible to store, index and search in documents 
    - Native XML databases
  - Many tools for XML processing 
    - Document parsing (DOM, SAX parsers)
    - Transformations (XSLT)
    - ...
  - Many applications already use XML

---

# History

- XHTML 1.0 (2000)
  - Basic transformation of existing HTML 4 (last version 1999) to XML
  - Backward compatibility with HTML
- XHTML 1.1 (2001)
  - Modularization (modules for different applications)
  - Preparation for further extensions
  - Strict XML (no backward compatibility with HTML but the same tags)
- XHTML 2.0 (last working draft 2006)
  - Modern design but not compatible with predecessors
  - Slow developent, did not solve actual problems (e.g. multimedia), not well received
- HTML 5
  - Back to HTML, solve the important issues
  - Includes both the [HTML syntax](https://html.spec.whatwg.org/multipage/syntax.html#syntax) and the [XHTML syntax](https://html.spec.whatwg.org/multipage/xhtml.html)

---

# HTML and XHTML

  - Common features 
    - The same meaning of most the tags and attributes
    - Tags and attributes are written the same way
  - Differences 
    - Strict syntax
    - Formatting tags and attributes removed, replaced by CSS
    - It has to respect the XML rules
  - Currently, use of XHTML is not recommended, but it works

---

# HTML vs XHTML Differences

- Additional XML header (optional for UTF-8 encoding)

```xml
<?xml version="1.0" encoding="utf-8"?>
```

- The root element `<html>` should have the `xmlns` and `xml:lang` attributes
```xml
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
``` 

---

# Writing tags

  - All the tag names must be entered in **lowercase**
  - All non-empty tags must have an end tag
  - The tags empty **from definition** (`<br>`) must have an end tag too `<br></br>` or they can be written as `<br/>`
```xml
<img src="..." alt="..." />
<input type="..." name="..." />
```

  - Scripts that must be marked as CDATA:
```xml
<script type="text/javascript">
   <![CDATA[
     ... JavaScript code ...
     ]]> 
</script>
```

---

# XHTML and the Transfer Protocol

  - XHTML should be processed by a XML parser in the browser 
    - Which is different from the default HTML parser
  - This must be indicated by the MIME type during the HTTP transfer 
    - Type `text/html` for HTML documents
    - Type `application/xhtml+xml` or `application/xml` for XHTML documents
  - Practical issues 
    - A server side configuration necessary
    - Sometimes the `.xhtml` extension is properly recognized
  - [Examples](http://www.fit.vutbr.cz/~burgetr/itw/)

---

# General XML

  - The browsers allows general XML processing (which is not XHTML)
  - No built-in style is defined 
    - But it is possible to define the author style sheet
    - The `xml-stylesheet` directive
  - Style definition 
    - **CSS**
      - Style for the individual elements
    - **XSLT**
      - Internal transformation to an HTML document
      - May include JavaScript etc.
  - [Examples](http://www.fit.vutbr.cz/~burgetr/itw/)
