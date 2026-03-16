
# Zanoření a vztahy



1. člen je jedinou prostou strukturou = vnoření hierarchie struktur

…
 vlastnostk: Člen

…



Vlastník

 vnitřní struktura





…

 vlastnostk:
 Člen

…





Vlastník

 objekt







3. člen je jediným objektem = vytváření vztahu typu 1:1

4. členové jsou v kolekci objektů = vytváření vztahu typu 1:N

…

 vlastnostk:

 Členové

…



Vlastník

 objekt





 objekt





 objekt





 objekt













2. členové jsou v kolekci prostých struktur = vytváření hierarchie struktur s vnořenými kolekcemi

…
 vlastnostk: Členové





Vlastník

 vnitřní struktura





 vnitřní struktura





 vnitřní struktura





 vnitřní struktura





---

# Vztahy kontra strukturalizace

---

>


	private String url;



	…

}

---

# Mapped Superclass – výsledek 
- Třída _Publication_ není entitou
	- Nemá tabulku v databázi
	- **Nelze specifikovat vztah publikace – autor** 
- Vhodné pro efektivní definici sdílených vlastností

![Obrázek 6](image4.png)

---

# Tabulka pro každou třídu

_@Entity_

_@Inheritance(strategy =_    	_InheritanceType.TABLE_PER_CLASS__)_

public abstract class Publication {



	_@Id_

	protected Long id;



	protected String title;



	_@__ManyToMany_

	_@__JoinTable__(…)_

	private Set<Author> authors;



	…

}

_@Entity_

public class Book extends Publication {



	private int pages;



	…

}

_@Entity_

public class BlogPost extends Publication {



	private String url;



	…

}

---

# Tabulka pro každou třídu – výsledek 
- Oddělené tabulky pro jednotlivé třídy
- Třída Publication je entita
	- Lze definovat vztah Publication – Author 
- Dotazy nad třídou Publication nejsou efektivní
	- Vede na JOIN nad konkrétními tabulkami
	- Např. for (Publication p : author.getPublications()) { … }

![Obrázek 6](image5.png)

---

# Jediná tabulka

_@Entity_

_@Inheritance(strategy =_    	_InheritanceType__.__SINGLE___TABLE)_

_@__DiscriminatorColumn__(name =_ 	_“__Publication_Type__”)_

public abstract class Publication {



	_@Id_

	protected Long id;



	protected String title;



	_@__ManyToMany_

	_@__JoinTable__(…)_

	private Set<Author> authors;



	…

}

_@Entity_

_@__DiscriminatorValue__(“Book”)_

public class Book extends Publication {



	private int pages;



	…

}

_@Entity_

_@__DiscriminatorValue__(“Blog”)_

public class BlogPost extends Publication {



	private String url;



	…

}

---

# Jediná tabulka – výsledek 
- Jedna tabulka pro všechny odvozené třídy
	- Jeden sloupec slouží jako diskriminátor
- Efektivní dotazování
	- Filtrování podle hodnoty diskriminátoru
	- Snadná reprezentace vztahu Publication – Author 
- Hodnoty nevyužitých vlastností jsou nulové
	- Nelze specifikovat _not_ _null_ nad vlastnostmi podtříd – omezuje kontrolu integrity dat
	- 

![Obrázek 6](image6.png)

---

# Joined

_@Entity_

_@Inheritance(strategy =_    	_InheritanceType__.__JOINED__)_

public abstract class Publication {



	_@Id_

	protected Long id;



	protected String title;



	_@__ManyToMany_

	_@__JoinTable__(…)_

	private Set<Author> authors;



	…

}

_@Entity_

public class Book extends Publication {



	private int pages;



	…

}

_@Entity_

public class BlogPost extends Publication {



	private String url;



	…

}

---

# Joined – výsledek 
- Tabulka pro každou třídu včetně Publication
- Snadná reprezentace vztahů, možnost integritních omezení
- Neefektivní dotazování
	- Vždy vede na JOIN více tabulek

![Obrázek 6](image7.png)

---

# Otázky?



---
