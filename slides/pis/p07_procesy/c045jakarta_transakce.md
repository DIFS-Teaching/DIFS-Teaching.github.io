<!-- .slide: class="section" -->

<header>
	<h1>Transakce v Jakarta EE</h1>
	<p>JTA, @Transactional, @TransactionAttribute — propojení teorie s praxí</p>
</header>

---

# JTA — Java Transaction API
- Standardní Jakarta EE API pro správu transakcí (`jakarta.transaction`)
- Definuje rozhraní mezi aplikací, kontejnerem a TPS (XA protokol)
- Tři úrovně správy transakcí:
	- **CMT** (Container-Managed Transactions) — implicitní, zajišťuje kontejner pro EJB
	- **BMT** (Bean-Managed Transactions) — explicitní `UserTransaction`
	- **CDI interceptor** — anotace `@Transactional` od Jakarta Transactions 2.0
- Viz EJB s CMT v přednášce p04

---

# @Transactional — deklarativní správa

```java
@ApplicationScoped
public class ObjednavkaService {

    @Inject
    EntityManager em;

    @Transactional
    public void vytvorObjednavku(Objednavka o) {
        em.persist(o);
        // kontejner: begin před metodou, commit po návratu
        // RuntimeException → rollback automaticky
    }
}
```

- CDI bean (ne EJB) může mít transakci díky `@Transactional`
- `RuntimeException` → rollback; checked exception → commit (lze změnit: `rollbackOn`)

---

# @TransactionAttribute — řízení propagace

| Hodnota | Chování volané metody |
|---|---|
| `REQUIRED` | Připojí se k existující transakci; není-li, vytvoří novou |
| `REQUIRES_NEW` | Vždy vytvoří novou transakci; stávající pozastaví |
| `MANDATORY` | Musí existovat transakce; jinak výjimka |
| `SUPPORTS` | Připojí se k existující; bez transakce pracuje bez ní |
| `NOT_SUPPORTED` | Vždy mimo transakci; stávající pozastaví |
| `NEVER` | Nesmí být aktivní transakce; jinak výjimka |

---

# REQUIRES_NEW — nezávislá podtransakce

```java
@Transactional   // REQUIRED
public void zpracujObjednavku(long id) {
    ulozObjednavku(id);      // v téže transakci
    odesliPotvrzeni(id);     // nová nezávislá transakce
}

@Transactional(Transactional.TxType.REQUIRES_NEW)
private void odesliPotvrzeni(long id) {
    // commit/rollback tohoto volání neovlivní volající transakci
}
```

- Každé volání je samostatnou podtransakcí (viz dále)
- Neúspěch `odesliPotvrzeni()` nemusí zrušit celou objednávku
- Kontejner provede `chain()` automaticky namísto explicitního volání v aplikaci

---

# EJB a Container-Managed Transactions
- EJB (`@Stateless`, `@Stateful`, `@Singleton`) mají CMT jako výchozí chování
- Každá metoda je implicitně `REQUIRED` — kontejner spustí transakci automaticky
- `@TransactionAttribute` na metodě přebíjí výchozí nastavení

```java
@Stateless
public class SkladBean {
    // implicitně REQUIRED na každé metodě

    @TransactionAttribute(TransactionAttributeType.REQUIRES_NEW)
    public void zarezervujZbozi(long polozkaId) { ... }
}
```

- Zodpovědnost za **konzistenci** dat zůstává na programátorovi — viz ACID

---

# Shrnutí: transakce v Jakarta EE

| Teorie | Jakarta EE |
|---|---|
| Plochá transakce | `@Transactional` / CMT — kontejner zajistí begin/commit/rollback |
| `chain()` zřetězená transakce | `REQUIRES_NEW` — kontejner spustí nezávislou podtransakci |
| XA protokol (dále) | JTA koordinuje více zdrojů (DB + JMS broker) v jedné transakci |
| Konzistence = zodpovědnost programátora | Anotace nenahrazují správný návrh logiky |
