<!-- .slide: class="section" -->

<header>
	<h1>Další architektury API</h1>
	<p>Alternativy k REST a GraphQL</p>
</header>
 
---

# Standardizace API
- Předchůdci REST
	- Snaha o maximální standardizaci volání serverových služeb přes HTTP
	- Vznik komplikovaných standardů webových služeb (SOAP atd.)
	- Obtížně použitelné bez podpůrných technologií – omezení na konkrétní implementační platformy
- REST – zjednodušení v reakci na komplikovanost WS
	- Flexibilita, ale žádný standard – mnoho ad hoc řešení
- GraphQL

---

# XML-RPC
- Předchůdce webových služeb
- Jednodušší – stále používané
- Definované XML zprávy pro předání parametrů i výsledku
- Podpora datových typů včetně polí, seznamů a struktur

---

# XML-RPC volání

```xml
<?xml version="1.0"?>
<methodCall>
	<methodName>trida.jePrvocislo</methodName>
	<params>
		<param>
			<value><int>1345</int></value>
		</param>
	</params>
</methodCall>
``` 

---

# XML-RPC výsledek

```xml
<?xml version="1.0"?>
<methodResponse>
	<params>
		<param>
			<value><boolean>0</boolean></value>
		</param>
	</params>
</methodResponse>
```

---

# Volání v PHP

```php
function xmlrpc($url, $method, $params, $types = array(), $encoding = 'utf-8') {
    foreach ($types as $key => $val) {
        xmlrpc_set_type($params[$key], $val);
    }

    $context = stream_context_create(array('http' => array(
        'method' => "POST",
        'header' => "Content-Type: text/xml",
        'content' => xmlrpc_encode_request($method, $params, 
			array('encoding' => $encoding))
    )));

    return xmlrpc_decode(file_get_contents($url, false, $context), $encoding);
}
```

---

# Webové služby (Web Services)
- Vzdáleně volané podprogramy umístěné na serveru
- Volání pomocí protokolu HTTP
	- Předání vstupních parametrů
	- Vrácení výsledku
- Předávají se XML data definovaná protokoly
	- WSDL – popis rozhraní služby
	- SOAP – volání služby

---

# Popis rozhraní služby: WSDL
- Web Services Description Language
- Platformově nezávislý popis rozhraní
	- XML dokument
	- Využíva XML Namespaces a XML Schema
- Definuje
	- Názvy funkcí
	- Jejich parametry
	- Způsob volání (vstupní URL)

---

# Příklad popisu služby

```xml
<message name="jePrvocisloRequest">
	<part name="cislo" type="xsd:long"/>
</message>
<message name="jePrvocisloResponse">
	<part name="return" type="xsd:boolean"/>
</message>
<portType name="Cisla">
	<operation name="jePrvocislo" parametrOrder="cislo">
	    <input message="m:jePrvocisloRequest" 
			name="jePrvocisloRequest"/>
 	    <output message="m:jePrvocisloResponse"
			name="jePrvocisloResponse"/>
	</operation>
</portType>
```

---

# Příklad popisu služby (II)

```xml
<binding name="cislaSoapBinding" type="m:Cisla">
 ... 
</binding>
<service name="CislaService">
	<port binding="m:cislaSoapBinding" name="cisla">
	   <wsdlsoap:address location="http://nekde.cz/cisla"/>
 	</port>
</service>
```

---

# Použití WSDL
- Na základě popisu lze automaticky generovat rozhraní v cílovém jazyce
	- „Stub“ - zástupnou metodu, která implementuje volání skutečné metody přes HTTP
- Rovněž lze generovat WSDL popis z rozhraní v cílovém jazyce
- Současné vývojové nástroje umožňuji vytvoření WS z funkce „jedním kliknutím“
	- Např. v Eclipse

---

# Volání služby: SOAP

```xml
<env:Envelope 
  xmlns:env="http://schemas.xmlsoap.org/soap/envelope/" 
  env:encodingStyle="  
            http://schemas.xmlsoap.org/soap/encoding/"
  xmlns:xs="http://www.w3.org/1999/XMLSchema"
  xmlns:xsi="http://www.w3.org/1999/XMLSchema-instance">
 <env:Header/> 
 <env:Body>
  <m:jePrvocislo xmlns:m="urn:mojeURI">
    <cislo xsi:type="xs:long">1987</cislo>
  </m:jePrvocislo>
 </env:Body>
</env:Envelope>
```

---

# Odpověď služby

```xml
<env:Envelope 
  xmlns:env="http://schemas.xmlsoap.org/soap/envelope/" 
  xmlns:xsi="http://www.w3.org/1999/XMLSchema-instance"
  xmlns:xsd="http://www.w3.org/1999/XMLSchema">
 <env:Body>
  <ns1:jePrvocisloResponse
    xmlns:ns1="urn:mojeURI"
    env:encodingStyle="	
            http://schemas.xmlsoap.org/soap/encoding/">
   <return xsi:type="xsd:boolean">true</return>
  </ns1:jePrvocisloResponse>
 </env:Body>
</env:Envelope>
```

---

# Komplexní příklady
- WSDL
http://www.w3.org/TR/wsdl20-primer/#basics-greath-scenario
- SOAP
http://www.w3.org/TR/soap12-part0/#L1165
- W3C Web Services Activity
http://www.w3.org/2002/ws/#documents


---

# Vyhledání webových služeb
- Idea centrálního registru
	- Protokol UDDI (Universal Description, Discovery and Integration)
	- Poskytovatelé ukládají WSDL popisy, klienti prohledávají
- Přehled služeb daného poskytovatele
	- WSIL (Web Services Inspection Language)
	- Seznam služeb v souboru `/inspection.wsil`

---

# Implementace WS
- Jakarta EE
	- JAX-WS API součástí standardu
	- Vytvoření webových služeb pomocí anotací
	- Běží na Jakarta EE aplikačním serveru
- PHP
	- Rozšíření SOAP
	- Třídy SoapServer, SoapClient, ...

---

# Jakarta EE
- Součástí Java EE je **Java API for XML Web Services (JAX-WS)**
- Server
	- Definice služeb pomocí anotací tříd a metod
	- Automaticky generuje WSDL popis
- Klient
	- Automatické generování proxy třídy z WSDL popisu

---

# Java EE Implementace

```java
package helloservice.endpoint;

import javax.jws.WebService;
import javax.jws.webMethod;

@WebService
public class Hello {

    public Hello() {    }

    @WebMethod
    public String sayHello(String name) {
        return "Hello, " + name + ".";
    }
}
```

---

# PHP
- Rozšíření SOAP
- Server
	- Třída `SoapServer`
	- Registruje třídy a metody implementující službu
- Klient
	- Třída `SoapClient`
	- Zpracuje WSDL a zpřístupní vzdálené metody

---

# PHP Soap Server

```php
<?php

function sayHello($name) {
    return "Hello, " . $name;
}

$server = new SoapServer(null,
       array('uri' => "urn://helloservice/endpoint"));
$server->addFunction('sayHello');
$server->handle();
```


---

# PHP SOAP Klient

```php
$client = new SoapClient(null,
	array('location' => "http://.../simple_server.php",
          'uri'      => "urn://my/namespace"));

$name = "Karel";
$result = $client->
             __soapCall("sayHello",array($name));

print $result;
```

---

# PHP s WSDL

```php
$soap = new SoapClient(
	'http://api.search.live.net/search.wsdl');

print_r($soap->__getFunctions());

$ret = $soap->Search(…);
```

