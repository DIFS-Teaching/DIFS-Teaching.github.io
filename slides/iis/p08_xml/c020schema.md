<!-- .slide: class="section" -->

<header>
    <h1>XML Schémata</h1>
    <p>Typová kontrola serializovaných dat</p>
</header>

---
# Typová kontrola

- Pro konkrétní aplikaci je možno definovat konkrétní jména značek, atributů, atd.
- Zavedením možnosti **_typového určení a kontroly_** (text, čísla, enumerace apod.) obsahu značek umožňuje 
	- **_definovat_**
	- **_kontrolovat_**
	- **_přenášet_**
	obecné datové struktury.
- Tím se ze značkovacích jazyků stává **_obecný prostředek pro_** **_serializaci_** **_strukturovaných dat_**

---

# Definice typu dokumentu
- Definice typu dokumentu (DOCTYPE) definuje **schéma** pro danou aplikaci – **metadata** 
- Definice DTD (Document Type Definition)
	- Starší „historická“ syntaxe
	- Samotné definice nejsou v jazyce XML
- Definice XSD (XML Schema Definition)
	- Používá XML syntaxi
	- Více možností (např. pořadí prvků, datové typy, …)
- Další alternativy (např. RelaxNG)

---

# Příklad: XML dokument a DTD

```xml
<?xml version="1.0" encoding="UTF-8"?>
<person>
   <address>
      <city>New York</city>
      <postalCode>10021</postalCode>
      <state>NY</state>
   </address>
   <firstName>John</firstName>
   <lastName>Smith</lastName>
   <phoneNumbers>
      <item>212 555-1234</item>
      <item>646 555-4567</item>
   </phoneNumbers>
   <decription>Some text</description>
</person>
```
<!-- .element: class="col"  -->

```dtd
<!ELEMENT person (address,firstName,lastName,phoneNumbers,
description?)>
<!ELEMENT address (city,postalCode,state,streetAddress)>
<!ELEMENT firstName (#PCDATA)>
<!ELEMENT lastName (#PCDATA)>
<!ELEMENT phoneNumbers (item)+>
<!ELEMENT city (#PCDATA)>
<!ELEMENT postalCode (#PCDATA)>
<!ELEMENT state (#PCDATA)>
<!ELEMENT streetAddress (#PCDATA)>
<!ELEMENT description (#PCDATA)>
<!ELEMENT item (#PCDATA)>
```
<!-- .element: class="col"  -->

- (prvek „description“ je nepovinný)

---

# Příklad: Totéž s atributy

```xml
<?xml version="1.0" encoding="UTF-8"?>
<person>
   <address
      city="New York"
      postalCode="10021"
      state="NY"
      streetAddress="21 2. street"/>
   <firstName>John</firstName>
   <lastName>Smith</lastName>
   <phoneNumbers>
      <item>212 555-1234</item>
      <item>646 555-4567</item>
   </phoneNumbers>
</person>
```
<!-- .element: class="col"  -->

```dtd
<!ELEMENT person (address,firstName,lastName,phoneNumbers,
description?)>
<!ELEMENT address EMPTY>
<!ATTLIST address
  city CDATA #REQUIRED
  postalCode CDATA #REQUIRED
  state NMTOKEN #REQUIRED
  streetAddress CDATA #REQUIRED>
<!ELEMENT firstName (#PCDATA)>
<!ELEMENT lastName (#PCDATA)>
<!ELEMENT phoneNumbers (item)+>
<!ELEMENT description (#PCDATA)>
<!ELEMENT item (#PCDATA)>
```
<!-- .element: class="col"  -->

- (prvek „description“ je nepovinný)

---

# Typy deklarací

|  |  |
|-------------------|-------------------|
|`<!DOCTYPE ...>`	|	typ dokumentu 	|
|`<!-- …… -->`		|	komentář |
|`<![CDATA[ …]]>` |	sekce znakových dat |
|`<!ENTITY ……>`	|	deklarace entity |
|`<!ELEMENT ……>` |		deklarace elementu |
|`<!ATTLIST ……>`	|	deklarace atributu |

\+ některé další

---

# Deklarace struktury a jejich prvků

Užívá se notace známá z **regulárních výrazů**

`()`	závorkové struktury

`?` 	volitelnost

`+`	jeden a více výskytů – je serializací **kolekce**

`*`	0 a více výskytů – je serializací **kolekce**

`,`	následnost – je serializací **struktury**

`|`	varianta - OR

`&`	jeden z možných - AND

---

# Typy atributů
- `CDATA`		řetězec znaků
- `NMTOKEN`		identifikátor (ale může začínat i číslicí)
- `NMTOKENS`	seznam NMTOKEN oddělených prázdnými znaky
- `ENTITY`		odkaz na entitu
- `ENTITIES`	seznam entit
- `ID`			unikátní identifikátor
- `IDREF`, `IDREFS` 		odkaz na identifikátor
- *výčet*		výčet hodnot `(hodnota|hodnota|…)`

---

# Standardní hodnota, resp. druh atributu
- není nezbytná
- `#REQUIRED`	povinný atribut
- *hodnota*		udává implicitní hodnotu atributu
- `#IMPLIED`	     (před hodnotou) nepovinný atribut
- `#FIXED`		     (před hodnotou) je to jediná možná hodnota

---

# Entity
- Možnost fyzicky izolovat a samostatně ukládat libovolnou **pojmenovanou** část dokumentu -- **entitu**
- Použití
	- Stejná informace se používá na několika místech
	- Informace může být nekompatibilními systémy reprezentována odlišně
	- Rozsáhlý dokument je vhodné z praktických důvodů členit
	- Informace je v jiném datovém formátu, nežli text XML (multimédia)

---

# Klasifikace entit 
- Interní a externí
- Textové a binární
- Dává nám 4 kombinace, přičemž interní binární není možná
- Interní textová, externí textová a externí binární je možná

---

# Deklarace entity
- Entita musí být v textu definována před prvním odkazem
- Při vícenásobné definici se bere první a ostatní se ignorují

`<!ENTITY jméno  entity … >`

`<!ENTITY myentity "obsah entity myentity">`

---

# Odkaz na entitu
- `&jméno entity;`
- Např.\
	`Stiskněte klávesu &lt;&lt;&lt;ENTER &gt;&gt;&gt;`\
	se zobrazí jako\
	`Stiskněte klávesu <<<ENTER>>>`

---

# Interní textové entity
- Zde je textový obsah uzavřen v uvozovkách (nebo apostrofech)

`<!ENTITY XML "eXtensible Markup Language">`

`Formát &XML; obsahuje entity`

se zobrazí jako

`Formát  eXtensible Markup Language obsahuje entity`

---

# Vestavěné entity
- není třeba deklarovat, nahrazují metaznaky jazyka XML
- `&lt;`		nahrazuje 	\<
- `&gt;`		nahrazuje 	\>
- `&amp;`		nahrazuje 	\&	
- `&apos;`		nahrazuje 	'
- `&quot;`		nahrazuje 	"


---

# Deklarace typu dokumentu
- `<!DOCTYPE jméno [ … ]>`
- musí se objevit před prvním elementem dokumentu
- Je možné použít pouze pro pojmenování a potom se část se závorkami vynechává

---

# XML Schema Definition

```xsd
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified">
  <xs:element name="person">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="address" type="xs:string"/>
        <xs:element name="firstName" type="xs:string"/>
        <xs:element name="lastName" type="xs:string"/>
        <xs:element ref="phoneNumbers"/>
        <xs:element minOccurs="0" name="description" type="xs:string"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
  <xs:element name="address">
    <xs:complexType>
      <xs:attribute name="city" use="required"/>
      <xs:attribute name="postalCode" use="required" type="xs:integer"/>
      <xs:attribute name="state" use="required" type="xs:string"/>
      <xs:attribute name="streetAddress" use="required"/>
    </xs:complexType>
  </xs:element>
  <xs:element name="phoneNumbers">
    <xs:complexType>
      <xs:sequence>
        <xs:element maxOccurs="unbounded" name="item" type="xs:string"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

- Modernější alternativa DTD, používá XML zápis.
