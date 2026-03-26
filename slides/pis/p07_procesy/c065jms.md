<!-- .slide: class="section" -->

<header>
	<h1>Jakarta Messaging a reaktivní mikroslužby</h1>
	<p>JMS, @MessageDriven, MicroProfile Reactive Messaging</p>
</header>

---

# Jakarta Messaging (JMS)
- Standardní Jakarta EE API pro práci s **message brokery** (balíček `jakarta.jms`)
- Jednotné rozhraní pro různé brokery: ActiveMQ Artemis, IBM MQ, Oracle AQ, …
    - Adaptér pro RabbitMQ
- Dva komunikační modely:
	- **Point-to-Point (Queue)** — zpráva jde jednomu konzumentovi
		- = zotavitelná fronta
	- **Publish/Subscribe (Topic)** — zpráva jde všem přihlášeným konzumentům
- Realizuje "oddělený aplikační modul (message broker)"

---

# JMS XA transakce — řešení fyzické události
- Problém: atomické provedení **"ulož do DB"** + **"vlož do fronty"**
- Řešení: **JMS XA** — broker se chová jako XA resource, koordinovaný JTA (2PC)

| Výsledek transakce | Co se stane se zprávou |
|---|---|
| Rollback | Zpráva se **neodešle** — záznam odstraněn z fronty |
| Commit | Zpráva **jistě doručena** — přežije restart systému |

- Odpadá nutnost explicitního čítače pro detekci stavu fyzické události

---

# @MessageDriven — EJB konzument

```java
@MessageDriven(activationConfig = {
    @ActivationConfigProperty(
        propertyName  = "destination",
        propertyValue = "java:app/jms/ExpediceQueue")
})
public class ExpediceMDB implements MessageListener {

    @Override
    @Transactional
    public void onMessage(Message msg) {
        long objednavkaId = msg.getBody(Long.class);
        // zpracuj expedici — v nové transakci
        // RuntimeException → rollback → zpráva se vrátí do fronty
    }
}
```

- `@MessageDriven` bean (MDB) = EJB konzument zotavitelné fronty
- Kontejner volá `onMessage()` pro každou zprávu asynchronně
- Rollback → zpráva se **vrátí do fronty**

---

# MicroProfile Reactive Messaging — ukázka

```java
@ApplicationScoped
public class ObjednavkaProducer {

    @Inject
    @Channel("objednavky-out")
    Emitter<Long> emitter;

    public void vytvorObjednavku(Objednavka o) {
        em.persist(o);
        emitter.send(o.getId());   // async odeslání na kanál
    }
}

@ApplicationScoped
public class ExpediceConsumer {

    @Incoming("objednavky-in")
    public CompletionStage<Void> zpracuj(Long objednavkaId) {
        return expedujAsync(objednavkaId);   // non-blocking
    }
}
```

- Kanál je namapován na konkrétní broker (Kafka, RabbitMQ, …) v konfiguraci
- `@Outgoing` / `@Incoming` odpovídají rolím producenta/konzumenta fronty

---

# JMS vs. MicroProfile Reactive Messaging

| Aspekt | Jakarta Messaging (JMS) | MP Reactive Messaging |
|---|---|---|
| Threading | Blokující | Neblokující (Reactive Streams) |
| Typický kontext | Jakarta EE aplikace | Mikroslužby |
| Transakce | JTA (XA) | Závisí na brokeru a konfiguraci |
| Konzument | `@MessageDriven` | CDI bean s `@Incoming` |

- Obě řeší **stejný problém**: asynchronní zpracování zpráv přes broker
- MP Reactive Messaging: viz přednáška p05
