<!-- .slide: class="section" -->

<header>
	<h1>JSON-RPC</h1>
	<p>Vzdálené volání procedur přes JSON</p>
</header>

---

# JSON-RPC
- Jednoduchý protokol pro vzdálené volání procedur (RPC)
- Přenos dat pomocí **JSON** místo XML
- Transportně nezávislý – typicky HTTP nebo WebSocket
- Verze: 1.0 (2005), 2.0 (2010)
- Žádný popis rozhraní (na rozdíl od WSDL)
	- Dokumentace je věcí poskytovatele

---

# Základní charakteristika
- Požadavek obsahuje
	- `jsonrpc` – verze protokolu (`"2.0"`)
	- `method` – název voláné metody
	- `params` – parametry (pole nebo objekt)
	- `id` – identifikátor požadavku (chybí u notifikací)
- Odpověď obsahuje
	- `result` – výsledek při úspěchu
	- `error` – chybový objekt při neúspěchu
	- `id` – shodné s požadavkem

---

# Příklad volání

```json
POST /api HTTP/1.1
Content-Type: application/json

{
    "jsonrpc": "2.0",
    "method": "math.isPrime",
    "params": { "number": 1987 },
    "id": 1
}
```

---

# Příklad odpovědi

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
    "jsonrpc": "2.0",
    "result": true,
    "id": 1
}
```

---

# Chybová odpověď

```json
{
    "jsonrpc": "2.0",
    "error": {
        "code": -32602,
        "message": "Invalid params",
        "data": "Parameter 'number' must be a positive integer"
    },
    "id": 1
}
```

---

# Dávkové volání
- Více požadavků v jednom HTTP dotazu
- Pole JSON objektů

```json
[
    { "jsonrpc": "2.0", "method": "math.isPrime",
      "params": { "number": 7 }, "id": 1 },
    { "jsonrpc": "2.0", "method": "math.isPrime",
      "params": { "number": 10 }, "id": 2 }
]
```

