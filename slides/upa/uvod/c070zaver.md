# K čemu to celé je

<p class="cite" style="font-size: 100%; margin-top: 1em;">
``Máme tahle data a tenhle způsob přístupu k nim.<br>
Kam to uložíme a co s tím musíme udělat předtím?''
</p>

- ??Tuhle otázku dostanete na pohovoru na **každou datovou nebo backendovou pozici**
- ??Po UPA na ni umíte odpovědět &ndash; a umíte i **zdůvodnit, co tím ztrácíte**
- ??Když vám kdykoli během semestru nebude jasné, proč zrovna tohle, **zeptejte se**
	- Je to legitimní otázka a má odpověď

Note:
Tři propojení napříč semestrem &ndash; rezerva, když zbude čas nebo přijde dotaz
&bdquo;proč je tohle všechno v jednom předmětu&ldquo;:

1. **Projekt je první polovina.** Získání dat (1, 2), popisné charakteristiky (3),
   čištění a integrace (4), transformace (5). Doslova jedna ku jedné.
2. **Prokletí dimenzionality.** V přednášce 5 je důvod, proč redukujeme dimenze &ndash;
   ve vysoké dimenzi přestávají dávat smysl vzdálenosti. V přednášce 13 je důvod, proč
   selhávají indexy &ndash; ve vysoké dimenzi přestává dávat smysl dělení prostoru.
   Je to tentýž jev: jednou při přípravě dat, podruhé při jejich ukládání.
3. **Cesta ke grafům.** RDF a propojená data (2) &ndash; grafové databáze (9) &ndash;
   dotazovací jazyky nad grafy (10) &ndash; vektorové indexy a hledání podobnosti (13).
   Čtyři přednášky z různých částí semestru, jedna souvislá linka.
   Obrázek k tomu je v `assets/grafy.svg`.

---

# Volba technologií

<p class="cite" style="font-size: 100%; margin-top: 1em;">
``Nechápu obsesi na této fakultě s XML. Nadával jsem na to už v IIS, vyhodíte to dvěrmi, vleze to zase zpátky oknem. Nevím, co v praxi dělám špatně, ale na XML jsem zatím nenarazil ani omylem.''
</p>

- ??[data.gov.cz](https://data.gov.cz/datov%C3%A9-sady), katalog českých otevřených dat
   - ??XML: 11 tis. datových sad, CSV: 5 tis., JSON < 2 tis.
   - ??JSON-LD, Turtle, SPARQL endpoint
- ??[volby.cz](https://www.volby.cz/opendata/opendata.htm) (XML)
- ??[data.europa.eu](https://data.europa.eu/data)
   - ??CSV: 270 tis., JSON 87 tis., XML 82 tis.

---

# Volba technologií (II)

Chceme učit přenositelné principy, konkrétním technologiím se ale vyhnout nelze.

1. Pragmatická volba
   - Znalost určitých standardů (vč. XML) se od absolventa FIT očekává
   - Technologie (byť překonaná) je široce používána
2. Ideologická volba
   - Existující problém má **elegantní** a **v praxi ověřené** řešení, jen o něm ``řadoví ajťáci`` neví
   - Absolvent FIT má přicházet s lepšími řešeními.
