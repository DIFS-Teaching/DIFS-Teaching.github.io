<!-- .slide: class="section" -->

<header>
	<h1>gRPC</h1>
	<p>Vysokovýkonné RPC od Googlu</p>
</header>

---

# gRPC
- Open-source RPC framework vyvinutý Googlem (2016)
- Přenos přes **HTTP/2** – multiplexing, binární přenos
- Serializace pomocí **Protocol Buffers** (protobuf)
	- Binární formát – kompaktnější a rychlejší než JSON/XML
- Silně typované rozhraní definované v `.proto` souboru
- Podpora streamování (server, klient, obousměrné)
- Vhodné zejména pro komunikaci mezi mikroslužbami

---

# Definice rozhraní (.proto)
- Rozhraní se popisuje v jazyce Protocol Buffers
- Z `.proto` souboru se **generuje kód** pro libovolný jazyk
	- Java, Python, Go, C++, PHP, ...

```protobuf
syntax = "proto3";

service MathService {
    rpc IsPrime (PrimeRequest) returns (PrimeResponse);
}

message PrimeRequest {
    int64 number = 1;
}

message PrimeResponse {
    bool result = 1;
}
```

---

# Volání služby (Python klient)

```python
import grpc
import math_pb2
import math_pb2_grpc

channel = grpc.insecure_channel('localhost:50051')
stub = math_pb2_grpc.MathServiceStub(channel)

request = math_pb2.PrimeRequest(number=1987)
response = stub.IsPrime(request)

print(response.result)  # True
```

---

# Implementace serveru (Python)

```python
import grpc
from concurrent import futures
import math_pb2_grpc, math_pb2

class MathServicer(math_pb2_grpc.MathServiceServicer):
    def IsPrime(self, request, context):
        n = request.number
        is_prime = n > 1 and all(
            n % i != 0 for i in range(2, int(n**0.5) + 1))
        return math_pb2.PrimeResponse(result=is_prime)

server = grpc.server(futures.ThreadPoolExecutor(max_workers=10))
math_pb2_grpc.add_MathServiceServicer_to_server(
    MathServicer(), server)
server.add_insecure_port('[::]:50051')
server.start()
```

---

# Implementace serveru (Java, Open Liberty)
- Open Liberty podporuje gRPC přes feature `grpc-1.0`
- Implementace rozšiřuje vygenerovanou třídu `ImplBase`
- CDI bean je automaticky zaregistrován jako gRPC service

```java
import io.grpc.stub.StreamObserver;
import jakarta.enterprise.context.ApplicationScoped;
import java.util.stream.LongStream;

@ApplicationScoped
public class MathServiceImpl extends MathServiceGrpc.MathServiceImplBase {

    @Override
    public void isPrime(PrimeRequest request,
                        StreamObserver<PrimeResponse> responseObserver) {
        long n = request.getNumber();
        boolean isPrime = n > 1 &&
            LongStream.rangeClosed(2, (long) Math.sqrt(n))
                      .noneMatch(i -> n % i == 0);
        responseObserver.onNext(
            PrimeResponse.newBuilder().setResult(isPrime).build());
        responseObserver.onCompleted();
    }
}
```

---

# Konfigurace Open Liberty (server.xml)

```xml
<featureManager>
    <feature>grpc-1.0</feature>
    <feature>grpcClient-1.0</feature>
    <feature>cdi-4.0</feature>
</featureManager>

<!-- gRPC sdílí port s HTTP/2, volitelná konfigurace pro všechny služby -->
<grpc target="*" maxInboundMessageSize="1048576"/>

<httpEndpoint id="defaultHttpEndpoint"
              httpPort="9080"
              httpsPort="9443"/>
```

- gRPC běží na stejném portu jako HTTP/2 – žádný samostatný port není potřeba
- Všechny CDI beany rozšiřující `ImplBase` jsou automaticky nalezeny

---

# Volání služby (Java klient)

```java
import io.grpc.ManagedChannel;
import io.grpc.ManagedChannelBuilder;

ManagedChannel channel = ManagedChannelBuilder
    .forAddress("localhost", 9444)
    .usePlaintext()
    .build();

MathServiceGrpc.MathServiceBlockingStub stub =
    MathServiceGrpc.newBlockingStub(channel);

PrimeRequest request = PrimeRequest.newBuilder()
    .setNumber(1987).build();
PrimeResponse response = stub.isPrime(request);

System.out.println(response.getResult());  // true
```

---

# Maven závislosti (gRPC Java)

```xml
<dependencies>
    <dependency>
        <groupId>io.grpc</groupId>
        <artifactId>grpc-stub</artifactId>
        <version>1.63.0</version>
    </dependency>
    <dependency>
        <groupId>io.grpc</groupId>
        <artifactId>grpc-protobuf</artifactId>
        <version>1.63.0</version>
    </dependency>
</dependencies>
```

- Kód se generuje z `.proto` souboru pluginem `protobuf-maven-plugin`
- Open Liberty poskytuje gRPC runtime – není třeba přidávat server závislosti

---

# Typy komunikace v gRPC
- **Unary RPC** – klasické volání: jeden požadavek, jedna odpověď
- **Server streaming** – jeden požadavek, proud odpovědí
- **Client streaming** – proud požadavků, jedna odpověď
- **Bidirectional streaming** – obousměrný proud zpráv

---


# Srovnání s REST a JSON-RPC
| | REST | JSON-RPC | gRPC | GraphQL | SOAP |
|---|---|---|---|---|---|
| Přenos | HTTP/1.1 | Libovolný (HTTP, WS…) | HTTP/2 | HTTP/1.1 | HTTP (nebo jiný) |
| Formát | JSON/XML | JSON | Protobuf (binární) | JSON | XML |
| Popis rozhraní | OpenAPI | – | `.proto` soubor | SDL schema | WSDL |
| Generování kódu | Volitelné | – | Ano | Volitelné | Ano |
| Streamování | Omezené | Ne | Ano | Subscriptions | Ne |
<!-- .element: class="small" -->
