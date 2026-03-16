<!-- .slide: class="section" -->

<header>
	<h1>Quick &amp; Dirty</h1>
	<p>Když potřebujeme rychle a jednorázově data z jednoduššího webu a nikdo se nás nebude ptát, jak jsme to udělali.</p>
</header>

---

# Shell je přítel

Motivace: [Evolution of a programmer](https://cgg.mff.cuni.cz/~semancik/cvika/programmer.html)

Co se hodí, než začneme programovat:
- `wget`, `curl`
- `cat`, `grep`, `sed`, `cut`
- `awk` (jen pro fajnšmekry :-)

```bash
wget https://www.fit.vut.cz/study/courses/ -O out.html
cat out.html | grep 'list-links__link' | sed 's/<[^<>]*>/;/g' | sed 's/;;*/;/g' >data.csv
cat data.csv | cut -f2 -d';'
```

```bash
wget https://www.fit.vut.cz/study/courses/ -O - | grep 'list-links__link' | sed 's/<[^<>]*>/;/g' | sed 's/\;;*/;/g' | cut -f2 -d';'
```

---

# Totéž v pythonu

```python
import urllib.request
import re

fid = urllib.request.urlopen('https://www.fit.vut.cz/study/courses/')
webpage = fid.read().decode('utf-8')
for line in webpage.split('\n'):
    if ('list-links__link') in line:
        line = re.sub(r"<[^<>]*>", ";", line);
        line = re.sub(r";;*", ";", line);
        print(line)
```

---

# Java

```java
import java.io.*;
import java.net.*;

public class Courses {
	
	public static void main(String[] args) {
		try {
			URI url = new URI("https://www.fit.vut.cz/study/courses/");
			HttpURLConnection con = (HttpURLConnection) url.toURL().openConnection();
			
			BufferedReader in = new BufferedReader(
					  new InputStreamReader(con.getInputStream()));
			
			String line;
			while ((line = in.readLine()) != null) {
			    if (line.contains("list-links__link")) {
			    	line = line.replaceAll("<[^<>]*>", ";");
			    	line = line.replaceAll(";;*", ";");
			    	System.out.println(line);
			    }
			}
			in.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

---

# Omezení jednoduchého přístupu

![opice](assets/imdb.png) <!-- .element: style="height:600px" -->

[Zdrojová stránka](https://www.imdb.com/title/tt6468322/fullcredits) -- regex?!

---

# Omezení jednoduchého přístupu

![UCI rankings](assets/uci.png) <!-- .element height="60%" width="60%" -->

[https://www.uci.org/mountain-bike/rankings](https://www.uci.org/mountain-bike/rankings) -- kde jsou data?

---

# Omezení jednoduchého přístupu

![UCI rankings](assets/uci_individual.png) <!-- .element height="60%" width="60%" -->

[https://www.uci.org/mountain-bike/rankings](https://www.uci.org/mountain-bike/rankings) -- stejné URL

---

# Omezení jednoduchého přístupu

![opice](assets/login.png) <!-- .element: style="display: block; margin: auto" -->

- Přihlašovací formulář s přesměrováním (a možným zabezpečením proti strojovému vyplnění)
- Zvládnutelné, ale komplikované
