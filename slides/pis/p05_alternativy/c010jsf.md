<!-- .slide: class="section" -->

<header>
	<h1>Java Server Faces (JSF)</h1>
	<p>Serverová prezentační vrstva</p>
</header>

---

# Prezentační vrstva
- Webové API + JS tlustý klient
	- Prezentační logika na klientovi
	- Business operace přístupné pomocí API (REST, SOAP, …)
	- Klientská aplikace může využívat klientský framework
		- Angular, React.js, Vue.js, …
- Serverový framework
	- Prezentační logika na serveru
	- Server generuje HTML (CSS, JavaScriptový) kód
	- Komponentově orientované frameworky

---

# Prezentační vrstva na serveru
- Funkčnost zajišťuje webový kontejner
- Pro Jakarta EE standardně 2 vrstvy
	- Facelets
	- Java Server Faces

- Existují další webové frameworky (Struts, Spring, Vaadin, …)

---

# Java Servlet
- Třída implementující chování serveru
- Obecný `jakarta.servlet.GenericServlet`
	- Metody `init()`, `destroy()`, `service()`
- HTTP `jakarta.servlet.http.HttpServlet`
	- Metody `doGet()`, `doPost()`, …
- Vytváření instancí řídí server
- Jedna instance může obsluhovat více požadavků

---

# Java Server Pages
- Dynamické webové stránky
	- HTML (XHTML, XML, …) kód
	- Vložený kód v Javě (_scriptlet_)
	- Definované značky
	- Výrazy – unified expression language (EL)
- Umožňuje definovat **knihovny značek** (tag libraries)
	- Chování každé značky implementováno jako třída
	- XML deskriptor knihovny

---

# Příklad JSP

```jsp
<%@ page language="java" contentType="text/html; charset=utf-8" 
	pageEncoding="utf-8"%>

<!DOCTYPE html>
<html>
<head>
	<title>My JSP Page</title>
</head>
<body>
	<h1>Hello World!</h1>
	<p>
	<%
		out.println("Current time: " + new java.util.Date());
	%>
	</p>
</body>
</html>
```

---

# Zpracování JSP stránky
- Stránka se překládá na servlet (třídu)
- Překlad zajišťuje kontejner
	- Skripty – vloženy do stránky
	- Tagy – volání metod příslušných tříd
	- Výrazy – volání evaluátoru

---

# Facelets
- Překlad XHTML stránek na interní objektovou reprezentaci – **Facelet**
	- Zpracování šablon
	- Související soubory (resources)
- Možnost definice knihoven značek
	- Vystačíme s existujícími
- Zpracování výrazů jazyka EL
	- Přístup k objektům, jejich vlastnostem a metodám

---

# XML namespaces

```xml
<html xmlns="http://www.w3.org/1999/xhtml"
	xmlns:ui="http://java.sun.com/jsf/facelets">
```

```xml
<ui:composition template="template.xhtml">
	<ui:define name="content">
	    <h2>Welcome</h2>
	    <p><a href="person_list.xhtml">Simple forms demo</a></p>
	</ui:define>
</ui:composition>
```

---

# Java – Namespaces
- Facelets tags
	
`xmlns:ui="http://xmlns.jcp.org/jsf/facelets"`
	

- JSF Core – obecné definice
	
`xmlns:f="http://xmlns.jcp.org/jsf/html"`
	

- JSF HTML – obsah stránky
	
`xmlns:h="http://xmlns.jcp.org/jsf/core"`

---

# Java Server Faces
- Komponentový MVC framework nad Facelets
- Značky pro generování základních prvků uživatelského rozhraní
	- Rozšiřitelné knihovny komponent
- Řídicí servlet implementující chování

---

# Nadstavbové knihovny
- [PrimeFaces](https://www.primefaces.org/)
- Apache MyFaces
- OmniFaces
- RichFaces (JBoss, není dále vyvíjen)
- …

---

# Experssion language
- `#{objekt}` – vyhledá objekt daného jména v kontextu stránky, požadavku, session a aplikace
- Metody: `#{customer.sayHello}`
- Vlastnosti: mapují se na set / get
	- `#{customer.name}`
	
---

# Logika uživatelského rozhraní
- EJB/CDI služby – model 
- _Managed beans_
	- Spravované objekty přístupné přes EL
	- Implementují chování UI
	- Vlastnosti a metody vázané na prvky GUI
- _Validators_
	- Kontrola vstupních dat
- _Converters_
	- Převod dat na řetězec a zpět

---

# Definice chování
- Každá stránka produkuje výsledek ve formě řetězce (outcome)
	- Statický (zadaný konstantou)
	- Dynamický (generovaný metodou)
		- Často po provedení nějaké akce
- Přechody mezi stránkami externě v XML souboru `faces-config.xml`

Demo: [Web frontend](https://github.com/DIFS-Teaching/jakartaee-basic/tree/main/web-frontend)
