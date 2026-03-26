
Radek Burget

burgetr@fit.vutbr.cz 

Technologie informačních systémů

Workflow systémy

---

# Vývoj architektur IS
- 60. léta – řada samostatných aplikací
	- vlastní uživatelské a datové rozhraní
	- vlastní metody ukládání dat
	- vlastní komunikace s uživatelem
- 70. léta – osamostatnění dat
	- databázové systémy
- 80. léta – osamostatnění uživatelského rozhraní
	- Windows API, X Window, ...
- 90. léta – osamostatnění řídicích procesů
	- workflow systémy
- 

---

# Podnikové (business) procesy
- Podnikový proces je koordinační mechanismus napříč organizačními jednotkami distribuovaný v čase a prostoru;
- integruje a koordinuje distribuované zdroje a poskytuje správnou informaci správnému jednotlivci ve správný čas k vykonání přiděleného úkolu.

CO – JAK – KDY – KDO
- Z hlediska technologie jde o
	- Popis procesů mimo vlastní implementaci IS
	- Infrastrukturu schopnou zajistit vykonání popsaných procesů
	- Doplňkové funkce: monitorování, analýza, …
	- 

---

# Příchozí faktura

![Picture 6](image3.png)

---

# Další příklady procesů
- Recenze příspěvků na konferenci
	- zaslání příspěvku, předání recenzentům, recenze příspěvků, zpráva autorovi, ...
- Zařízení služební cesty
	- objednávka letenek, ubytování, vypůjčení auta, zaplacení poplatků, schválení cesty, ...
- Vyřízení reklamace
	- obdržení požadavku, rozhodnutí o oprávněnosti, odpověď, ...
- Sledování pacientů v nemocnici
	- příjem, RTG, EKG, krev, diagnóza, léčení, ...
- 

---

# Příklady procesů (II)
- Vyřízení žádosti o půjčku
	- žádost o půjčku, analýza rizik, schválení, sledování splátek, uzavření případu, ...
- Vývoj programů
	- návrh, specifikace, implementace, ...
- Zápis studentů do dalšího ročníku
	- předběžný zápis, kontrola studia, zápis, změny, ...
- Výběrové řízení na zakázky
	- zadání, vyhodnocení nabídek, výběr dodavatele, řešení námitek, realizace, ...
- 

---

# Workflow
- Procedurální automatizace business procesu prostřednictvím správy sekvence pracovních aktivit a vyvolání příslušných lidských nebo IT zdrojů příslušejících k těmto aktivitám.
- Rozdíl mezi Business procesem a workflow je neurčitý, pojmy jsou často zaměňovány.
	- Workflow je konkrétní popis realizace procesu
	- BP lze chápat na obecnější úrovni

---

# Systémy pro řízení business procesů



---

# Zařazení workflow do infrastruktury
- Samostatný systém
	- Např. webové nebo jiné rozhraní
	- Sdílení podkladů a dokumentů
		- Např. naskenované faktury k vyřízení
	- Sledování stavu úkolů
		- Vývoj zpracování, zadávání doplňujících informací
- Integrace s existující infrastrukturou
	- E-mail (upozorňování na úkoly)
	- Účetní software, group managemet, …

---

# Standardizace
- Existuje množství SW nástrojů realizujících myšlenku workflow
- Potřeba integrace systémů – nutnost standardizace
- Workflow Management Coalition (WfMC)
	- založena 1993
	- nevýdělečná mezinárodní organizace prodejců, uživatelů, analytiků a univerzitních / výzkumných skupin (asi 130 členů)
	- tvorba standardů v oblasti
		- terminologie,
		- spolupráce a propojení wf systémů
	- tři komise a pracovní skupiny
	- 

---

# Hlavní standardy
- Workflow Reference Model
- Workflow Client Application Application Programming
- Glossary
- Interoperability Abstract Specification
- Audit Data Specification
- Process Definition Interchange
- Interoperability Internet e-mail MIME Binding
- Objektový model (IDL a OLE)
- Bezpečná spolupráce wf systémů
- 

---

# Referenční model workflow

![Picture 5](image4.png)

---

# Prvky workflow
- WES = workflow enactment service
_(workflow servery)_
	- Zajišťuje vykonání správné činnosti pomocí správného prostředku ve správný čas
	- Složen z jednoho nebo více _workflow engines_
- Workflow engine
	- Interpretace definice procesu
	- Vytváří instance procesů a řídí jejich vykonávání
	- Zajišťuje přechody mezi aktivitami a vytváření pracovních položek
	- Další funkce pro správu a dohled

---

# Prvky workflow
- Klientské aplikace workflow
	- Provádí jednotlivé úkoly
	- Interakce uživatelů s workflow
- Vyvolané aplikace
	- Spouštěné v souvislosti se započetím úkolu apod.

---

# Prvky workflow (II)
- Nástroje pro definici procesů
	- umožňují definici a rozplánování procesů na počítači
-  obvykle grafické nástroje
-  prvky modelu:
	- **zprávy** zaslané účastníkům procesu,
	- **události**, které mohou nastat,
	- **rozhodnutí**, která je třeba učinit;
-  základní prvky určují charakter modelu
- 

---

# Prvky workflow (III)
- Nástroje pro simulaci procesů
	- Co se stane, když ... ?
	- Ověření modelu, predikce
- Nástroje pro verifikaci procesů
	- Bude každá objednávka vyřízena?
	- Bude každá reklamace vyřízena do 14 dnů?
	- Matematické metody – Petriho sítě
- Nástroje pro administraci



---

# Rozhraní workflow systému
- Pro nástroje pro definici procesů
- Pro workflow klienty
- Pro volané aplikace
- Pro komunikaci s jinými WFM systémy
- Pro administraci a monitorování

---

![Picture 7](image5.png)

---

# Data ve workflow
- Model organizační struktury
	- Role, vztahy nadřízený – podřízený 
- Definice procesu
	- Činnosti, přidělení rolím, rozhodovací pravidla
- Seznam úkolů
	- Aktuální úkoly pro konkrétní uživatele
	- Uživateli buď skryt (postupné přidělování úkolů) nebo přístupný (uživatel si volí pořadí, možno i více úkolů současně)

---

# Data ve workflow
- Řídicí data workflow
	- Interní data WF systému nutná pro zajištění chodu příp. zotavení po havárii
	- Nedostupná externím aplikacím
- Věcná data workflow
	- Zpracování jádrem workflow systému
	- Používána pro rozhodování o dalším postupu
	- Dostupná i aplikacím
- Aplikační data workflow
	- Specifická data aplikací podporujících proces
	- Nejsou přístupná WF systému



---

# Reprezentace a provádění procesu
- Standardy WfMC definují základní pojmy používané pro reprezentaci workflow

---

![Picture 6](image6.png)

**Podprocesy**

---

![Picture 5](image7.png)

---

# 3D pohled na workflow
- **případ (case)**
	- konkrétní řešený problém (žádost o půjčku)
	- obvykle jej generuje externí zákazník
	- zpracovává se prováděním úloh v určitém pořadí
	- na základě definice workflow procesu
- **úloha (****task****)**
	- krok provádění procesu
	- charakterizuje se podmínkami platnými před _(__precondition__)_ a po _(__postcondition__)_ provedení
- 

---

# 3D pohled na workflow
- **zdroj (resource)**
	- zařízení (fax, tiskárna) nebo osoba (účastník, dělník, zaměstnanec)
	- vytvářejí **třídy zdrojů** na základě podobných  charakteristik
	- **role** je třída založená na schopnostech svých  prvků (např. programátoři)
	- **organizační jednotka** je třída založená na struktuře organizace (např. reklamační oddělení)
- 

---

# 3D pohled na workflow
- **pracovní položka, požadavek (work item)**
	- úkol řešený pro konkrétní případ, např. „vrátit panu Novákovi peníze za reklamované zboží“
- **činnost (activity)**
	- úkol řešený pro konkrétní případ a využívající konkrétní zdroj
	- vytváří frontu požadavků _(worklist)_

---

# Role
- práci vykonávají **kategorie pracovníků**
- jedna osoba může mít více rolí, mnoho osob má stejnou roli
- role jsou autorizovány provádět požadavky z front spojených s činnostmi
- požadavky na zpracování se přidělují staticky nebo dynamicky (load balancing)
- 

---

![Picture 7](image8.png)

---

# Struktura činnosti
- **Pracovní položka a fronta požadavků**
	- požadavky na provedení aplikace
	- strukturované zprávy obsahující parametry pro provedení činnosti
	- maximální doba provedení činnosti (připomenutí, předání jinam)
	- synchronizace paralelních instancí workflow
	- různé strategie: FIFO, LIFO, priority
- 

---

# Struktura činnosti
- **Příprava k provedení vybrané činnosti**
	- vyhodnocení vstupní podmínky na základě dat
	- závislých na řešeném případu
	- získání vstupních dat pro činnost
- **Akce jako jádro činnosti**
	- interaktivní: výběr položky uživatelem spustí provedení činnosti
	- automatické: příchod položky do fronty způsobí  provedení činnosti
- 

---

# Struktura činnosti
- **Závěrečná analýza**
	- monitorování provádění aplikace: úspěch, chyba,  havárie
	- uložení výsledků aplikace – konverze a uložení  dat do společné paměti
- **Směrování**
	- přesun požadavků k dalším činnostem
	- na základě stavu (návratového kódu), výsledku



---

# Modelování business procesů



---

# Fáze vývoje workflow

![Picture 6](image9.png)

---

# Cíle BPM
- Formální popis procesů probíhajících v organizaci
- Možnost řízení takto popsaného procesu pomocí WFM systému
- Možnost analýzy, verifikace
	- Zvýšení efektivity

---

# Standardy pro modelování
- Business Process Modeling Notation (BPMN)
	- Grafická notace pro specifikaci procesů
	- Diagramy BPD (Business process diagram)
- Jazyky pro popis procesu
	- BPEL (BPEL4WS, WS-BPEL) – procedurální
	- XPDL – deskriptivní
	- BPMN XML serializace (definována od BPMN 2.0)
- Je definováno mapování
	- Ukládání BPMN grafů v XPDL
	- Mapování BPMN -> BPEL
	- 
	- 

---

# Elementy BPMN
- Objekty toku (flow objects)
	- Event (událost)
	- Activity (aktivita)
	- Gateway (brána)
- Spojovací objekty (connection objects)
	- Sequence flow (sekvenční tok)
	- Message flow (tok zpráv)
	- Association
- Plavecké dráhy (swimlanes)
- Artefakty (artifacts)

---

# Objekty toku
- Událost
	- Ovlivňuje tok procesu
	- Začátek nebo konec procesu
- Aktivita
	- Práce, činnost která se má vykonat
	- Atomická nebo podproces
- Brána
	- Rozhodování, paralelní zpracování







---

# Spojovací objekty
- Sekvenční tok
	- Navazující aktivity (pořadí)
- Tok zpráv
	- Zpráva mezi dvěma účastníky
procesu
- Asociace
	- Propojuje objekt s dodatečnou
informací







---

# Plavecké dráhy (swimlanes)
- Pool
	- Reprezentuje účastníky v procesech
	- Mezi pooly se komunikuje zprávami
	- 
	- 
- Swimlane
	- Kategorizují aktivity
	- 





Name





Name



---

# Příklad poolu

![Picture 5](image10.png)

---

# Směrování – řízení toku činnosti
- Rozdělení toku (split)
- Spojení (join)
- Různé druhy
	- XOR – vzájemné vyloučení
	- OR – nebo
	- AND – současně

---

# Workflow patterns
- Sekvence
	- Pracovní úkol je v procesu povolen, až je dokončeno provedení předcházejícího úkolu v procesu.

![Picture 4](image11.png)

http://www.workflowpatterns.com/ 

---

# Workflow patterns
- Parallel split (AND-split)
	- Rozděluje tok procesů (workflow) do dvou a více paralelních vláken.

![Picture 4](image12.png)

---

# Workflow patterns
- Synchronizace (AND-join)
	- Dalším úkolem se pokračuje, až po dokončení všech předchozích vláken.

![Picture 4](image13.png)

---

# Workflow patterns
- Výlučné rozhodnutí (XOR-split)
	- Rozděluje tok procesů na dvě nebo více větví, které jsou vzájemně výlučné. Podle podmínky v Gateway se vstupuje do jedné z větví.
	- 

![Picture 4](image14.png)

---

# Workflow patterns
- Jednoduché spojení (XOR-merge)
	- Spojení dvou nebo více nezávislých větví do jedné. Navazující aktivita začne okamžitě, jakmile jedno vlákno dosáhne svého konce.
	- 

![Picture 4](image15.png)

---

# Workflow patterns
- Multi-choice (OR-split)
	- Jedna nebo více variant

![Picture 4](image16.png)

---

# Workflow patterns
- Structured Synchronizing Merge (OR-join)
- Skončí všechno, co začalo (kontext)

![Picture 4](image17.png)

---

# Pravidla pro přechod mezi činnostmi
- Lhůta (deadline)
- Vstupní podmínka (pre-condition)
	- Musí být splněna pro spuštění činnosti
	- Vyhodnocována WF systémem
- Výstupní podmínka
	- Musí být splněna pro ukončení činnosti
	- Do té doby činnost trvá, příp. se opakuje
- Přechodová podmínka
	- Umožňuje určit pořadí zpracování činností
	- Např. mimořádné situace

---

# Flexibilita workflow
- Podmínky pro chod organizace se mění
	- Změna legislativy, restrukturalizace, …
- Zajištění flexibility
	- Dopředné – uvažujeme všechny možné situace ve workflow
	- Zpětné – **změna workflow za běhu**

---

# Dynamická změna workflow
- Pomocí základních změn (evolution patterns)
	- Vždy je definováno, zda lze změnu provést a jak
- Převod existujících instancí
	- Concurrent to completion
	- Migrace na finální schéma
		- Jen za určitých podmínek
	- Migrace na ad-hoc schéma
- Verifikace výsledku
	- Bude WF stále dělat to, co má?

---

# Verifikace workflow
- Analýza cest
	- Dosažitelnost stavů
- Petriho sítě

---

# Technologie



---

# Jazyk XPDL
- XML Process Description Language
- Jazyk popisující BPMN graf
- Aplikace XML
- Prvky dokumentu
	- Package, application
	- Workflow process
	- Activity
	- Transition
	- Participant
	- DataField
	- DataType

---

# XML Serializace BPMN 2.0
- Obdobné použití, jako XPDL

![Picture 2](image18.png)

**<****process** **processType****="****Private****"** **isExecutable****="****true****" id="****com.sample.HelloWorld****„**
	**name****="Hello** **World****" >**



    **<!--** **nodes** **-->**

    **<****startEvent** **id="_1"** **name****="****StartProcess****" />**

    **<****scriptTask** **id="_2"** **name****="Hello" >**

      **<****script****>****System.out.println****("Hello** **World****");</****script****>**

    **</****scriptTask****>**

    **<****endEvent** **id="_3"** **name****="****EndProcess****" >**

        **<****terminateEventDefinition****/>**

    **</****endEvent****>**



    **<!--** **connections** **-->**

    **<****sequenceFlow** **id="_1-_2"** **sourceRef****="_1"** **targetRef****="_2" />**

    **<****sequenceFlow** **id="_2-_3"** **sourceRef****="_2"** **targetRef****="_3" />**



  **</****process****>**

---

# Jazyk BPEL
- Business Process Execution Language
- De-facto **průmyslový standard**
- Procedurální jazyk, opět XML
- Předpokládá implementaci úkolů pomocí webových služeb
	- Orchestrace volání webových služeb
- BPMN 2.0 obsahuje významnou podmnožinu ekvivalentních BPEL
	- Je možno použít BPMN 2.0 engine místo BPEL engine

---

# Webové služby
- Standard komunikace v distribuované aplikaci
	- Vzdálené volání funkcí
	- Výměna dokumentů
- Standardní jazyky
	- Popis rozhraní služby (WSDL)
	- Výměna zpráv (SOAP)
- Komunikace
	- Obvykle HTTP

---

# Vrstvy modelování procesů

![Picture 2](image19.jpeg)

---

# BPEL & BPMN engines
- Apache ODE
- MS BizTalk Server
- Oracle BPEL Process Manager
- IBM WebSphere Process Server
- jBoss jBPM
- …

---

# jBoss jBPM
- Framework implementující workflow, BPM a orchestraci procesů
- Běží na jBoss nebo jiném JEE serveru
- Snadná integrace Java EE aplikací
	- Web services, Java Messaging, JDBC, EJB
- Zajišťuje správu stavů a úloh
- Měří časy provádění kroků, logování
- Unifikuje správu workflow procesů

---

# jBPM Eclipse Plugin

![Zástupný symbol pro obsah 3](image20.png)

---

# Jazyky v jBPM
- Grafický editor BPMN
	- Eclipse
- BPMN 2.0 serializace
	- Workflow management
	- Správa úkolů prováděných lidmi
- BPEL
	- Web service orchestration v rámci JBoss BPEL serveru
	- Opuštěno v novějších verzích jBPM



---

# AgilPro
- Open source nástroje pro modelování procesů
- AgilPro LiMo
	- Grafický editor procesů
- AgliPro Simulator
	- Simulátor procesů
- Založeno na platformě Eclipse + JWT (Java Workflow Tooling)
	- Vlastní formát JWT
	- Export/import z XPDL, BPMN, atd.

---

# Bonita
- Open source projekt
	- Java EE a XPDL
	- API pro vytváření i provoz workflow
- Workflow prováděný virtuálním strojem

![Picture 4](image21.png)

---

![Picture 5](image22.png)

---

# Scarbo
- Grafický modeler + engine
- Založeno na Eclipse a Bonita

![Picture 4](image23.png)

---

# Literatura
- M. Beneš: Úvod do technologie workflow systémů (slidy)
- T. Novotný: Workflow – BPM Systémy
- P. Opletal: Procesy a workflow (slidy)
- V. Mates, T. Hruška: Workflow, studijní opora
- 

---

# Otázky?

---
