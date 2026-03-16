# Motivace

- **Na webu je spousta dat** ||ukrytých ve webových stánkách||
- ??Potřebujeme dále zpracovat tato data v počítačových aplikacích
	- ??Propojení s vlastními daty
	- ??Agregace -- spojení výsledků z různých zdrojů
	- ??Analýza -- statistiky, získávání znalostí
	- ??... a mnohé další
- ??Potřebujeme **strukturovaná data**
	- Reprezentovatelná tabulkami relační databáze
	- Nebo alespoň XML, JSON, apod. *s pevnou strukturou*

---

# Data na webu
- Webové stránky nejsou silně strukturované
- Nejčastěji v HTML
	- Prvotním cílem je *vizuální prezentace*
	- Kód je druhotný, *podřízený prvnímu cíli*
	- Není určen k dalšímu zpracování
    - Často proměnlivé schéma
- **Slabě strukturované dokumenty**

---

# Vzhled a kód
![opice](assets/opice.png) <!-- .element: style="height:700px;float:left;margin-right:2em" -->

[Zdrojová stránka](https://www.u3opic.cz/)

<div class="fragment" style="position: absolute; font-size: 50%; top: 0; right: 0; width: 50em; max-height: 50%;">

```html
<section class="menu">
    <div class="container">
        <div class="row">
            <div class="col-md-12">
                <div class="page-header wow fadeInDown">
                    <h1>Dnešní polední menu</h1>
                </div>
            </div>
        </div>
        <div class="food-menu wow fadeInUp">
            <div class="row menu-items">
                <div class="menu-item col-sm-12 col-xs-12 starter"><div class="clearfix menu-wrapper"><h4>Hrachová polévka s opečenou houskou</h4></div></div><div class="menu-item col-sm-12 col-xs-12 starter"><div class="clearfix menu-wrapper"><h4>1. Indické butter chicken se smaženou cizrnou, rýže Basmati</h4><span class="price">149 Kč</span><div class="dotted-bg"></div></div></div><div class="menu-item col-sm-12 col-xs-12 starter"><div class="clearfix menu-wrapper"><h4>2. Smažený česnekový řízek z vepřové kotlety, bramborový salát s majonézou</h4><span class="price">159 Kč</span><div class="dotted-bg"></div></div></div><div class="menu-item col-sm-12 col-xs-12 starter"><div class="clearfix menu-wrapper"><h4>3. Barbecue Pulled Pork Hot Dog, smažené bramborové hranolky (máslová houska plněná trhaným vepřovým masem se sýrem čedar a křupavou cibulkou)</h4><span class="price">179 Kč</span><div class="dotted-bg"></div></div></div>
                </div>
            <div class="row">
                <div class="col-md-12">
                    <div class="menu-btn">
                        <a class="btn btn-default btn-lg" href="/denni-menu/" role="button">Zobrazit menu</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</section>
```

</div>

---

# Další zdroje

- Komerční
	- e-shopy||, realitní servery||||, letenky||||, sportovní výsledky||||, sledování konkurence||
- ?? Výsledky vyhledávání
	- Např. hlídání pozice
- ?? Veřejné rejstříky
	- jízdní řády
	- živnostenský rejstřík
	- statistický úřad
	- weby zastupitelstev
- ?? Kontrola reklamy
- ?? @@span class="large" style="line-height:0.5; vertical-align:top;" @@ &#8734; @@/span@@ dalších

---

# Dílčí problémy

- Získání zdrojových dat
	- Jak stáhnout potřebné dokumenty z WWW (aby obsahovaly to, co mají?)
	- Paralelizace
- **Nalezení a extrakce dat**
	- Identifikace požadovaných údajů ve stránce
- Uložení výsledků <!-- .element: class="grey" -->
	- Může jich být **opravdu mnoho** 

---

# Architektura

Základní architektura

![Architektura](assets/arch.svg) <!-- .element: width="100%" -->
