
## HTTP 

<details>
<summary><strong style="font-size:1.17em">HTTP 프로토콜이 뭐죠?</strong></summary>

```text
HTTP는 TCP/IP 기반 통신 프로토콜로 www에서 데이터를 전달하는데 사용됩니다.
HTTP 사양은 클라이언트 요청 데이터가 구성되고 서버로 전송되는 방법과 
서버가 이러한 요청에 응답하는 방법을 지정합니다.

기본기능은 stateless, connectionless, MIME 유형을 사용하여 모든 유형의 데이터를 전송,
HTTP 메소드, 캐싱 지원등을 합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">HTTP 헤더의 역할과 중요한 헤더들에 대해 설명해 주세요.</strong></summary>

```text
HTTP 헤더는 클라이언트와 서버 간에 전송되는 메타데이터를 포함합니다. 
예를 들어, Content-Type 헤더는 전송되는 데이터의 형식을 나타내고, 
Authorization 헤더는 인증 정보를 전달합니다. 
Cache-Control이나 Expires와 같은 헤더는 캐싱 전략에 대한 정보를 담고 있습니다
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">서버에서 지정하는 Cache-Control 값들</strong></summary>

```text
private: 브라우저만 캐싱 가능
public: 중간 서버(프록시 등)도 캐싱 가능
max-age=3600: 캐시 유효시간을 초 단위로 지정
must-revalidate: 캐시가 신선한 상태일때는 사용하지만 만료되면 서버에 확인 필수
no-cache: 캐시 사용 전 서버 확인 필수
no-store: 캐시 저장 안 함
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">HTTP 프로토콜에서 데이터 압축은 어떻게 이루어지나요?</strong></summary>

```text
 HTTP는 Content-Encoding 헤더를 통해 데이터를 압축할 수 있습니다. 
 지원 가능한 압축 방식으로는 gzip 등이 있습니다.
 
 클라이언트가 지원 가능한 압축 방식을 Accept-Encoding 헤더로 서버에 알리고, 
 서버는 해당 방식으로 응답을 압축해 전달합니다. 
 
 이를 통해 네트워크 대역폭을 절약하고 성능을 개선할 수 있습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">HTTP와 HTTPS 차이점</strong></summary>

```text
http는 암호화되지않은 프로토콜로, 클라이언트와 서버 간에 데이터를 평문으로 주고 받습니다. 주로 80번포트를 사용하며 보안에 취약합니다.

https는 SSL/TLS 암호화가 적용된 프로토콜 입니다.
클라이언트와 서버 간에 주고받는 데이터를 암호화하여 보호합니다. 암호화 덕분에 중간에서 데이터를 가로채더라도 해커가 내용을 알 수 없습니다.
주로 443번 포트를 사용합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Http 1.0 / 1.1 / 2 / 3에 대해 설명하세요</strong></summary>

```text 
HTTP 1.0은 Content-Type, 버전 정보, 상태코드라인이 생겼고, 1개의 커넥션을 맺고 하나의 요청과 응답만 가능하다는게 단점입니다.

HTTP/1.1은 파이프라이닝, 청크 전송 인코딩, 캐시 제어 헤더 기능을 제공합니다. 

HTTP/2는 바이너리 프레임 레이어가 추가되고, 멀티 플렉싱, 헤더 압축, 서버 푸시, 스트림 우선순위 지정 기능을 제공합니다.
하지만 HTTP2가 TCP 위에서 동작한다는 점에서, 헤드오브라인 블로킹 문제가 발생합니다.

HTTP/3 은 UDP 위에서 동작하는 QUIC이라는 새로운 전송계층 프로토콜을 사용합니다. 따라서 UDP 특성과 QUIC의 특성인 스트림 독립성, 빠른 연결이 가능합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Http 1.1의 파이프라이닝, 청크전송, 캐시제어 각각 설명해주세요</strong></summary>

```text
파이프라이닝을 통해 클라이언트는 하나의 TCP 연결에서 이전 요청의 응답을 기다리지 않고 여러 요청을 연속적으로 보낼 수 있습니다. 그러나 서버는 여전히 요청을 받은 순서대로 응답을 처리하고 전송해야 하기 때문에 HOL 블로킹 문제가 있습니다.

청크 전송 인코딩으로 전체 응답을 기다릴 필요 없이 작은 단위로 쪼개 응답을 보냅니다.

캐시 제어 헤더로 불필요한 데이터 전송을 줄이고, 조건부 요청을 사용하여 자원이 변경된 경우에만 서버에 요청하도록 할 수 있습니다. 이는 성능을 향상 시킵니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">HTTP 2의 멀티플렉싱, 서버 푸시, 헤더 압축, 스트림 우선순위에 대해 설명해주세요</strong></summary>

```text
멀티플렉싱은 단일 TCP 연결을 사용하여 동시에 여러 데이터 스트림을 처리할 수 있습니다. 
데이터 스트림에 데이터를 프레임이라는 작은 단위로 쪼개어 전송합니다. 이 프레임들은 각각의 스트림을 통해 주고 받으며, 스트림번호가 매겨져있어 다시 종합할 수 있습니다.

서버 푸시는 서버가 클라이언트의 요청을 기다리지 않고 미리 필요한 리소스를 전송하여 웹 페이지 로딩속도를 개선합니다.

헤더 압축은 HTTP 헤더 패킷에서 중복 정보를 제거하는 HPACK 압축을 사용합니다.

스트림 우선순위는 스트림에 가중치를 부여해 우선순위를 매겨 우선순위 높은 리소스에 대해 더 많은 프레임을 보내도록 합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">HTTP2에서 HOL문제가 왜 발생하죠?</strong></summary>

```text
여러개의 스트림이 같은 TCP 연결을 공유하고 있기 때문에 하나의 패킷 손실이 발생하면 TCP는 손실된 패킷이 재전송될 때까지 모든 스트림이 멈추는 현상이 발생합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">QUIC에 대해 더 자세히 알려주세요</strong></summary>

```text
UDP의 속도와 단순함을 이용하면서도, TCP가 제공하는 신뢰성을 보장하는 기능들을 QUIC이 자체적으로 구현한 것입니다.

- QUIC은 TCP처럼 패킷 손실을 감지하고, 손실된 패킷만 재전송합니다. 다만, TCP와 달리 다른 스트림의 데이터는 계속 전송됩니다.
- QUIC은 HTTP/2처럼 하나의 연결에서 여러 스트림을 동시에 처리할 수 있습니다. 하지만 TCP와 달리, 각 스트림이 독립적으로 처리되기 때문에 헤드 오브 라인 블로킹 문제가 발생하지 않습니다.
- QUIC은 TCP와 달리 처음부터 TLS를 내장하여, 연결 설정 시에 바로 암호화된 통신을 시작합니다. 이는 TCP에서 발생하는 핸드셰이크 과정을 단축시켜 연결 지연을 줄여줍니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">QUIC 핸드셰이크가 TCP보다 빠른 이유</strong></summary>

```text
QUIC은 1-RTT(1 Round-Trip Time) 또는 0-RTT로 매우 빠르게 연결을 설정할 수 있습니다. TCP는 최소 **3-웨이 핸드셰이크(3-way handshake)**가 필요하며, 
TLS 핸드셰이크까지 포함하면 여러 번의 왕복(RTT)이 필요합니다. 
하지만, QUIC에서는 클라이언트가 서버에 요청을 보내는 동시에 TLS 암호화 설정과 데이터 전송이 함께 이루어질 수 있습니다. 이로 인해 연결 설정 시간이 훨씬 줄어듭니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">HTTP 응답코드에 대해 설명해 주세요.</strong></summary>

```text
HTTP 응답 상태 코드는 특정 HTTP 요청이 성공적으로 완료되었는지 여부를 나타냅니다. 
응답은 5가지 클래스로 분류됩니다.
100번대는 정보성 응답, 200번대는 성공 응답, 
300번대는 리다이렉션, 400번대는 클라이언트 오류, 500번대는 서버 오류를 나타냅니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">401 (Unauthorized) 와 403 (Forbidden)은 의미적으로 어떤 차이가 있나요?
</strong></summary>

```text
401은 인증이 안된 상태라, 로그인이 필요합니다.
403은 인가가 안된 상태라, 특정 요청페이지에 접근 권한이 없습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">200 (ok) 와 201 (created) 의 차이에 대해 설명해 주세요.
</strong></summary>

```text
200은 요청이 성공적으로 수행되었으므로 
주로 조회(GET), 수정(PUT/PATCH), 삭제(DELETE) 작업에서 사용됩니다.

요청이 성공적으로 수행되어 새로운 리소스가 생성되었음을 의미
주로 생성(POST) 작업에서 사용됩니다.
```

</details>

---

## REST

---

<details>
<summary><strong style="font-size:1.17em">SOAP과 REST 차이점</strong></summary>

```text
SOAP
- XML 기반의 메시지 프로토콜
- 엄격한 규칙과 표준이 있음
- HTTP, SMTP 등 다양한 프로토콜 사용 가능
- 기업 간 통신등 엄격한 보안과 ACID를 준수할 필요가 있을 때 사용합니다. 

REST
- HTTP 기반의 아키텍처 스타일
- 리소스 중심의 설계
- HTTP 메서드로 행위 정의 (GET/POST/PUT/DELETE)
- 주로 JSON 사용합니다.
```
</details>

---

<details>
<summary><strong style="font-size:1.17em">Restful을 지키는게 뭔가요?</strong></summary>

```text
1. URL은 리소스를 나타내도록 명사 위주로 설계
2. HTTP 메서드의 적절한 사용을 위해 GET, POST, PUT, DELETE를 목적에 맞게 사용하고요
3. Stateless한 방식으로 각 요청은 독립적으로 처리되도록 했어요. 세션 정보는 서버에 저장하지 않고 토큰을 사용했습니다.
4. API의 버전을 URL에 포함시켜 하위 호환성을 유지했습니다. 예를들면 /api/v1/users
5. Swagger 같은 도구로 API 문서를 자동 생성하고 유지하고요
6. HTTP 상태 코드를 상황에 맞게 반환하고요
7. HATEOAS(헤이티오스)로 응답에 관련 리소스의 링크를 포함시켜 API 탐색을 용이하게 합니다. 
```
</details>

---

<details>
<summary><strong style="font-size:1.17em">GET,POST 이런거 말고 또 아는 메소드 있나요?</strong></summary>

```text
Trace Method 는 Client - Server Side 간 Loop back Test 를 진행할 수 있게 도와줍니다.

HEAD: GET과 동일하지만 응답 본문을 포함하지 않습니다. 예를들어,
헬스체크나 버젼 확인 등의 용도로 사용됩니다.

OPTIONS: 서버가 지원하는 메서드를 확인하기 위해 사용합니다. CORS에서 사용됩니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">멱등성이 뭐죠? 그리고 어떤 메소드가 멱등한가요?</strong></summary>

```text
멱등하다는 것은 첫 번째 수행을 한 뒤 여러 차례 적용해도 결과를 변경시키지 않는 작업 입니다. 

GET, PUT처럼 리소스를 조회하거나 대체하는 메서드는 멱등해요.
DELETE 역시 여러 번 호출해도 삭제된 리소스에 대한 결과는 달라지지 않아요.

반면 서버 데이터를 변경하는 POST, PATCH는 호출할 때마다 응답이 달라지기 때문에 멱등한 메서드가 아니에요.
이렇게 멱등하지 않은 메서드에 멱등성을 제공하려면 서버에서 멱등성을 구현해야 합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">그럼 이렇게 POST, PATCH와 같이 멱등성이 보장되지 않는 메서드는 어떻게 해야하나요?</strong></summary>

```text
클라이언트는 서버에게 API 요청을 보낼 때 헤더에 멱등키를 넣습니다.
서버는 DB에 해당 멱등키가 저장되어있다면 똑같은 요청으로 판단하고, 실제 요청을 실행하지않고, 해당 멱등키에 대한 응답을 반환합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">GET과 POST의 차이는 무엇인가요?</strong></summary>

```text
GET은 정보를 검색, 요청할 때 사용합니다.
또한 캐시가 가능합니다.

POST는 데이터를 body에 담아 전송하고
POST 요청을 성공적으로 처리한 결과로 원본 서버에 하나 이상의 리소스가 생성된 경우 원본 서버
는 다음을 제공하는 Location 헤더 필드가 포함된 201(생성됨) 응답을 보내야 합니다.
캐시되지않으며 POST요청이라도 body내용에 민감한
데이터를 담는 경우 반드시 암호화해 전송해야합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">POST와 PUT, PATCH의 차이는 무엇인가요?</strong></summary>

```text
POST는 새로운 리소스를 생성할 때 사용합니다.
클라이언트는 리소스의 URI를 모르는 상태에서 리소스를 생성할 수 있습니다
POST는 멱등하지 않습니다.
서버에서 정의한 다양한 작업을 모두 처리할 수 있는 통합 메서드로 사용됩니다.

PUT 요청에서는 클라이언트가 리소스의 정확한 URI를 알아야 됩니다.
POST 요청과 달리 PUT 요청은 멱등합니다. 
그래서 PUT 메서드는 주로 리소스를 업데이트할 때 사용합니다.
그러나 PUT 메서드는 리소스 전체를 업데이트해야 된다는 특징이 있어요. 
즉, 리소스 일부만 수정하고 싶어도 전체 필드 데이터를 요청 본문에 포함해야 돼요.

PATCH 메서드도 PUT 메서드와 같이 특정 리소스 URI를 정확히 알고 있어야 합니다.
PATCH는 클라이언트의 요청에 따라 리소스를 수정하고 부분 업데이트를 합니다
멱등하지 않고 안전하지 않습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">HTTP 1.1 이후로, GET에도 Body에 데이터를 실을 수 있게 되었습니다. 그럼에도 불구하고 왜 아직도 이런 방식을 지양하는 것일까요?</strong></summary>

```text
GET의 의미는 읽기 작업을 하기 위함인데 요청 본문은 서버에서 처리할 데이터를 전달합니다. 
즉, GET으로 본문을 보내면 이러한 명확한 구분이 흐려집니다.

서버가 GET 요청의 본문을 무시하거나 요청을 완전히 거부할 수도 있습니다.
또 본문이 있는 GET 요청은 캐시되지 않을 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">URI URN URL 차이</strong></summary>

```text
URI
인터넷 상의 리소스를 식별하는 모든 방법을 포함하는 개념
URL과 URN을 모두 포함하는 상위 개념

URL
리소스의 "위치(어디 있는지)"를 나타냄
특정 프로토콜,도메인을 포함하여 접근방법 지정, 웹에서 흔히 사용되는 주소형식

URN
리소스의 "이름(무엇인지)"을 나타냄
특정위치가 아닌 고유하고 변하지 않는 식별자 역할
예: ISBN
```

</details>

---

## TCP

---

<details>
<summary><strong style="font-size:1.17em">Stateless와 Connectionless에 대해 설명해 주세요.</strong></summary>

```text
Stateless란, 서버가 이전 요청에서의 클라이언트의 상태를 보존하지 않는다는 의미입니다.

Connectionless란, 클라이언트와 서버가 요청-응답 후 연결을 끊는 특성입니다. HTTP 1.0의 기본적인 특성 입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">왜 HTTP는 Stateless 구조를 채택하고 있을까요?</strong></summary>

```text
- 상태 정보를 서버가 별도로 관리할 필요가 없어 확장성이 좋습니다.
- 요청 내용만으로도 응답을 캐싱할 수 있어 성능 향상에 도움이 됩니다.
- 클라이언트와 서버 간 상호작용이 독립적이므로 클라이언트 상태 변화에 영향을 받지 않습니다.
```
</details>

---

<details>
<summary><strong style="font-size:1.17em">Connectionless의 논리대로면 성능이 되게 좋지 않을 것으로 보이는데, 해결 방법이 있을까요?</strong></summary>

```text
HTTP Keep-Alive로, 요청과 응답 간에 TCP 연결을 유지하여 새 연결을 생성하는 오버헤드를 방지합니다.

또는 HTTP 1.1은 HTTP 파이프라이닝 기능으로 응답을 기다리지 않고 여러 개의 요청을 보낼 수 있습니다. 
단, HOL 블로킹 문제가 발생할 수 있습니다. 
```
</details>

---

<details>
<summary><strong style="font-size:1.17em">TCP의 keep-alive와 HTTP의 keep-alive의 차이는 무엇인가요?</strong></summary>

```text
HTTP Keep Alive는 클라이언트와 서버 사이에 동일한 TCP 커넥션을 이용해 여러 요청을 주고 받기 위해 사용됩니다.
즉, 3-way handshake를 한번 하고, 그 이후에는 더이상 하지않기 때문에 서버리소스부하가 줄어듭니다.
그리고나서 마지막 요청이후에 keep alive가 설정한 시간이 지나면 tcp 커넥션을 끊습니다.

TCP Keep Alive는 TCP 연결이 맺어진 이후에 해당 연결을 유지하는 것에 대해 작은 패킷을 보내며 체크하는 메커니즘을 말합니다.
ACK을 정상적으로 받지 못하면 OS에서 TCP 연결을 종료합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Keep-Alive와 Connection: Close의 차이점</strong></summary>

```text
Keep-Alive는
목적: 하나의 TCP 연결을 통해 여러 HTTP 요청/응답을 주고받을 수 있게 합니다.
동작 방식:
클라이언트가 "Connection: Keep-Alive" 헤더를 요청에 포함시킵니다.
서버가 이를 지원하면, 응답에도 "Connection: Keep-Alive"를 포함시킵니다.

장점은
새로운 TCP 연결 설정에 드는 오버헤드를 줄여 성능을 향상시킵니다.
특히 여러 리소스를 연속적으로 요청할 때 효과적입니다.

HTTP 버전: HTTP/1.1에서는 기본적으로 Keep-Alive가 활성화되어 있습니다. 
따라서 응답헤더에 명시적으로 하지않습니다.

Connection: Close은

목적: 각 HTTP 요청/응답 쌍마다 새로운 TCP 연결을 사용합니다.
동작 방식:
클라이언트나 서버가 "Connection: Close" 헤더를 포함시킵니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Keep-Alive 단점, 문제점?</strong></summary>

```text
클라이언트와 서버사이에 프록시가 놓여있다면 문제가 생깁니다.

Keep-Alive 연결로 여러 요청을 처리할 때, 앞선 요청이 지연되면 뒤의 요청들도 모두 지연됩니다. 
클라이언트-프록시, 프록시-서버 간 연결에서 각각 HOL 블로킹이 발생할 수 있기 때문입니다.

또한, Keep-Alive 연결이 유지되면 프록시의 로드 밸런싱 능력이 제한될 수 있습니다.
즉, 특정 서버에 트래픽이 집중될 수 있어, 전체적인 시스템 효율성이 떨어질 수 있습니다.

```

</details>

---

<details>
<summary><strong style="font-size:1.17em">TCP에서 연결 손실(커넥션 로스)을 감지하는 방법</strong></summary>

```text
- 수신 측 윈도우가 0인 상태가 지속되면 연결 상태를 확인합니다
- 중복 ACK 패킷을 3번 연속으로 받으면 패킷 손실이라 판단하고 재전송을 수행합니다.
- TCP Keep Alive 패킷을 주기적으로 전송하는데 응답을 받지못하면 TCP 연결이 끊어졌다고 판단합니다.
- ACK이 RTO 시간 내에 도착하지 않으면 연결 문제로 간주합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">TCP 3-way 핸드셰이크에 대해 설명하세요</strong></summary>

```text
3 way 핸드셰이크는 클라이언트와 서버가 서로 <연결 준비 상태>임을 확인하고, <신뢰성 있는 데이터 전송을 보장>하기 위해 수행되는 <3단계의 프로세스>입니다.

- 먼저, 클라이언트가 서버에 연결 요청 메시지인 SYN 패킷을 보냅니다.
- 서버는 이 요청을 수락하고, 응답으로 SYN과 ACK 패킷을 클라이언트에게 보냅니다.
- 클라이언트는 서버의 응답을 확인한 후, 다시 ACK 패킷을 서버로 보냅니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">TCP 4-way 핸드셰이크가 뭐죠?</strong></summary>

```text
4-way handshake 는 연결을 끊을때, 즉 세션을 종료할때 수행되는 절차입니다.

1.클라아이언트가 서버에게 연결 종료를 요청합니다.

2.서버는 바로 종료시키는 것이 아니라, 단순히 ACK 만을 날립니다. 
서버는 종료시키기 전에 본인도 마저 할일이 있기 때문에 바로 FIN 을 날리지 않고, 단순히 ACK를 날리고 CLOSE_WAIT 상태로 넘어갑니다.

3.서버는 본인이 할일을 다 마쳤다면 그제서야 FIN 을 날리고 연결을 종료하고자 합니다.

4.클라이언트는 서버의 FIN 을 잘 받았다는 ACK 를 서버에게 보내게되고, 
서버는 ACK 를 전달받으면 소켓을 timewait 시간동안 기다린 후, timewait 이 끝나면 그때서야 종료시킵니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">왜 종료 후에 바로 끝나지 않고, TIME_WAIT 상태로 대기하는 것 일까요?</strong></summary>


```text
4-way handshake 에서 소켓이 바로 종료(제거)되지 않고, 일정시간동안 대기한 후 제거되어야 합니다. 
이때 이 일정 대기시간을 TimeWait 이라고 부릅니다.

 네트워크 상의 문제로 클라이언트가 ACK 를 보내주지 못하는 경우가 발생할 수 있습니다. 
 이런 경우를 대비해, 서버가 다시 FIN 을 보내서 클라이언트로부터 
 ACK 를 확실히 응답받을 때 까지 혹시모를 대기시간(timewait) 이 필요한것입니다. 
```

</details>

---

## 쿠키,세션,JWT

---

<details>
<summary><strong style="font-size:1.17em">쿠키와 세션 차이에 대해 설명해주세요</strong></summary>

```text
쿠키는 클라이언트(브라우저) 측에 저장되는 작은 데이터 조각입니다.
로그인 정보 유지 등에 사용하고, 만료 기간을 설정할 수 있어요
클라이언트에 저장되므로 보안에 취약할 수 있고, 크기가 4KB로 제한되어 있습니다.

세션은 서버 측에서 유지되는 정보 저장 방식입니다.
서버의 메모리나 데이터베이스에 저장되고요
사용자별 상태 정보를 유지해요. 로그인 상태 유지나 장바구니 기능 등에 많이 사용합니다 
서버는 세션 생성 시 고유한 세션 ID를 발급하고, 이를 클라이언트에 쿠키로 전송해요. 이후 요청 시 이 ID로 세션을 식별하죠.
서버에 저장되므로 쿠키보다 안전해요. 민감한 정보를 다룰 때 주로 사용했어요
하지만 많은 세션을 유지하면 서버에 부담이 될 수 있습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">세션 방식의 로그인 과정에 대해 설명해 주세요.
</strong></summary>

```text
1. 클라이언트가 서버에 로그인 요청을 보냅니다.
2. 서버는 요청을 받아 로그인 정보를 검증합니다.
3. 로그인 정보가 유효하다면, 서버는 세션 ID를 생성하고, 세션 ID와 사용자 정보를 서버에 저장합니다.
4. 세션 ID를 클라이언트에 쿠키로 전송합니다.
5. 클라이언트는 이후 요청 시 쿠키에 저장된 세션 ID를 서버에 전송합니다.
6. 서버는 세션 ID를 통해 사용자 정보를 확인하고, 요청을 처리합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">HttpSession.getAttritube("user") 사용자 A가 접속해도 "user"를 Key로 값을 가져오고, 사용자 B가 접속해도 "user"를 Key로 가져옵니다. 같은 Key를 쓰는데 어떻게 A와 B를 구분해서 값을 가져오나요?</strong></summary>

```text
각 브라우저/클라이언트는 첫 접속시 고유한 세션ID(JSESSIONID)를 받습니다
이 세션ID는 쿠키로 브라우저에 저장됩니다
이후 요청시마다 브라우저는 자신의 JSESSIONID를 서버에 전송합니다
서버는 JSESSIONID를 기반으로 해당 사용자의 세션을 찾습니다
같은 "user" key를 사용하더라도 다른 세션에 저장되어 있어 값이 섞이지 않습니다
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
HTTP의 특성인 Stateless에 대해 설명해 주세요.
</strong></summary>

```text
Stateless란 서버가 클라이언트의 상태를 보존하지 않는다는 의미입니다.
따라서 모든 HTTP 요청은 이전 요청과 완전히 독립적으로 처리됩니다
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Stateless의 의미를 살펴보면, 세션은 적절하지 않은 인증 방법 아닌가요?
</strong></summary>

```text
세션은 실제로 Stateful한 특성을 가지고 있어서, 
HTTP의 Stateless 원칙과는 어긋납니다.

하지만, 세션은 서버 측에서 상태 정보를 유지하므로,
보안에 더 강력하고, 민감한 정보를 다룰 때 사용하기 좋습니다.

아니면 stateless한 jwt를 사용할 수도 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
규모가 커져 서버가 여러 개가 된다면, 세션을 어떻게 관리할 수 있을까요?
</strong></summary>

```text
1. Sticky Session 방식은 세션을 최초에 생성한 서버로 요청을 고정하는 방식입니다. 
정합성 이슈를 해결할 수 있으나, 로드 밸런싱과 가용성면에서 문제가 있을 수 있습니다.

2. Session Clustering 은 세션을 생성될 때마다 복제하여 각 서버의 세션 정보를 일치시켜 정합성 이슈를 해결합니다. 
하지만, 매번 세션 객체를 복제하는데 오버헤드가 발생하므로 사용 시, 이를 고려해야 합니다.

3. 세션 스토리지 분리 방식은 별도의 세션 저장소를 사용하는 것으로, 
서버가 아무리 늘어난다고 할 지라도 세션 스토리지에 대한 정보만 각각의 서버에 입력해주면 세션을 공유할 수 있게 됩니다.
하지만 세션 저장소에 대한 부하가 발생할 수 있으므로, 이를 고려해야 합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">JWT가 뭐죠?</strong></summary>

```text
- JSON 웹토큰은 정보를 안전하게 통신할 때 사용하는 인터넷 표준 토큰입니다.
- 헤더, 페이로드, 서명 세 가지 주요 요소로 구성되고 각 구성은 . 마침표를 구분자로 사용합니다.
- 헤더는 토큰의 유형인 JWS 또는 JWE과 서명 알고리즘을 명시합니다. 그리고 JSON으로 표현된 헤더를 Base64로 인코딩합니다.
 
- 필요에 따라 새로운 클레임을 추가할 수 있고, JWS 방식에서는 페이로드도 Base64로 인코딩합니다. 
누구나 디코딩할 수 있기 때문에 JWS 페이로드에는 민감한 정보를 넣으면 안 돼요. 
JWE 방식에서는 페이로드를 안전한 알고리즘과 비밀 키로 암호화하기 때문에 민감한 정보를 포함할 수 있어요.

- 서명은 헤더와 페이로드를 결합한 후 지정된 알고리즘과 비밀 키 또는 공개 키로 서명한 값입니다. 
이 서명은 JWT의 무결성을 보장하며, 데이터가 변경되지 않았음을 확인할 수 있습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">JWT의 장점과 단점</strong></summary>

```text
먼저 JWT는 독립적(Stateless)입니다. 
필요한 정보를 모두 자체적으로 들고 있어서 서버 측에서 세션을 저장할 필요가 없어요. 
이런 특징 덕분에 JWT를 이용하면 서버 부하를 줄일 수 있고 확장성을 확보할 수 있어요.

다음으로 JWT를 사용하면 무결성이 보장됩니다. 
JWS는 서명을 통해 토큰이 변조되지 않았음을 확인할 수 있어요. 
JWE는 페이로드를 암호화하기 때문에 데이터의 기밀성까지 보장할 수 있고요.

마지막으로 JWT는 간결하고, 
URL에서 안전하게 사용할 수 있습니다. 
모바일 기기 및 웹 애플리케이션에서 클라이언트가 편리하게 파싱하고 이용할 수 있어요. 

 
- 하지만 토큰을 탈취당한다면 강제로 만료시키기가 어려운 단점이 있습니다. 
- 그리고 JWT 크기도 매우 커 오버헤드 문제가 있고,
- 로그아웃에도 문제가 있는데, 세션은 단지 세션값을 날리면 되지만 JWT는 무상태이기 때문에 불가능합니다 
따라서 생명주기를 짧게 갖거나 로그아웃하거나 보안 위협이 감지된 토큰의 ID를 Redis에 저장하고, 
매 요청마다 이 블랙리스트를 체크했죠. 이렇게 하면 즉시 토큰을 무효화할 수 있었습니다.  
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">신뢰성이라는 말이 어려운데 당신이 이해한 바론 뭔가요</strong></summary>

```text
데이터 전송이 순서대로, 손실 없이 완벽하게 도착하는 것을 말합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">브라우저에 URL을 쳤을 때 무슨 일이 일어나나요?</strong></summary>

```text
- 예를들어 브라우저에 https://www.naver.com 인 URL을 입력하고 Enter 키를 누릅니다.
- 브라우저는 해당 URL을 파싱합니다. (https는 통신 프로토콜로 TLS를 사용하여 서버에 연결하도록 지시합니다. / 도메인 / 경로 / 리소스)
- 브라우저는 도메인의 IP 주소를 알아내기 위해 먼저, 브라우저 캐시를 확인하고 없으면 hosts 파일과 OS 캐시를 확인합니다.
- 여기에도 없다면 DNS 서버에게 IP 주소를 질의합니다.

- 먼저 로컬 DNS 서버는 캐시를 확인하고 없으면 Root Name Server에게 com이 있는 TLD Name Server 주소를 받습니다.
- 그리고 TLD Name Server에서 sub domain Name Server 주소를 받고 sub domain Name Server에서 IP 주소를 받게 되고 최종적으로 브라우저에게 도착하게 됩니다.

- IP 주소를 받은 웹 브라우저가 서버와의 TCP 연결을 시작하기 위해 요청 패킷을 
TCP/IP 라는 전송제어 프로토콜을 사용하여 라우터 장비와 ISP를 통해 이동하는데 라우팅 테이블을 사용하여 최적의 경로를 찾아 목적지 IP 주소를 가진 웹 서버에 도달합니다.

- 브라우저는 서버와의 TCP 연결을 시작합니다. 이때 TCP는 3-way handshake 방식으로 연결합니다.
- HTTPS 프로토콜의 경우 추가적으로 TLS Handshake를 수행합니다.
- 웹 브라우저가 서버에 연결되면, 웹 브라우저가 페이지의 콘텐츠를 응답받기 위해 서버에 HTTP 요청을 전송하는 것으로 시작합니다.
- 서버는 받은 패킷안에 HTTP 메세지를 확인하고 올바른 요청일 경우 요청에 대한 응답을 생성하고 클라이언트에게 보냅니다.

- 만약, 동적인 컨텐츠를 요청할 때 웹 서버는 클라이언트의 요청을 웹 애플리케이션 서버에 전달합니다.
- WAS는 관련된 Servlet을 메모리에 올리고, 해당 Servlet에 대한 Thread를 생성합니다. 그리고 HttpServletRequest와 HttpServletResponse 객체를 생성하여 필터를 거쳐 디스패처서블릿에 전달합니다.
- 그후 디스패처서블릿의 일련의 과정을 거친 후 Response 객체를 Servlet Container에 의해 HTTP 응답으로 변환되어 클라이언트에게 전송됩니다
- Web Server는 결과를 클라이언트에게 전달합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">TLS HandShake 설명해주세요</strong></summary>

```text
1. 사전단계로, CA 인증기관에서 서버의 공개키와 정보를 인증기관의 개인키로 서명하여 인증서를 제작하고 서버에 전달합니다.

2. 클라이언트가 서버에 연결을 요청합니다 (ClientHello).

3. 서버는 자신의 인증서를 클라이언트에게 전송합니다 (ServerHello, Certificate).

4. 클라이언트는 자신이 신뢰하는 CA의 공개키로 인증서를 검증합니다.

5. 검증이 성공하면 클라이언트는 서버의 공개키를 획득합니다.

6. 클라이언트는 임시 대칭키(세션 키)를 생성하고, 이를 서버의 공개키로 암호화하여 서버에 전송합니다.

7. 서버는 자신의 개인키로 암호화된 세션 키를 복호화하여 획득합니다.

8. 이제 클라이언트와 서버는 동일한 세션 키를 공유하게 되어, 이후의 통신에서 이 대칭키를 사용하여 데이터를 암호화하고 복호화합니다.
```

</details>

---

---

<details>
<summary><strong style="font-size:1.17em">공개키와 대칭키에 대해 설명해 주세요.</strong></summary>

```text
대칭키는 암호화와 복호화에 사용되는 키가 동일합니다.
공개키 암호화 방식에 비해 속도가 빠르지만, 키 배송 문제가 발생합니다.

공캐키 암호화 방식은 암호화와 복호화에 사용되는 키가 다릅니다.
공개키로 암호화한 암호문은 오직 개인키로만 복호화 할 수 있습니다.
대칭키 암호화 방식보다 속도가 느리지만, 대칭키 암호화 방식의 키 배송 문제를 해결 할 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">왜 HTTPS Handshake 과정에서는 인증서를 사용하는 것 일까요?
</strong></summary>

```text
HTTPS Handshake 과정에서 인증서를 사용하는 가장 핵심적인 이유는 
서버의 신원을 확인하고 안전한 키 교환을 보장하기 위해서입니다.

클라이언트가 접속하려는 서버가 실제로 정당한 서버가 맞는지 확인할 수 있습니다. 
이는 신뢰할 수 있는 인증기관(CA)이 발급한 인증서를 통해 검증됩니다

인증서 내부에는 서버의 공개키가 포함되어 있습니다. 
이 공개키는 CA의 개인키로 서명되어 있기 때문에 위조가 불가능하며, 
클라이언트는 이 공개키를 사용해 안전하게 대칭키를 교환할 수 있습니다
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">SSL과 TLS의 차이는 무엇인가요?</strong></summary>

```text
공개된 SSL 2.0에 취약점이 발견되어 아예 구조를 재설계해 SSL3.0이 나왔습니다.
그 이후 기존 버전과 구분하기위해 3.0 다음부터 등장한 SSL의 이름을
TLS로 변경했습니다.

주요 차이점은
인증할 때 SSL은 MAC을 사용하고, TLS는 HMAC을 사용합니다.

* MAC, HMAC은 메시지 무결성을 확인하기 위해 SHA 해시알고리즘을 사용
```

</details>

---

## OSI 7 Layer

<details>
<summary><strong style="font-size:1.17em">OSI 7 Layer란 뭔가요?</strong></summary>

```text
네트워크 프로토콜 디자인과 통신 과정을 7개의 계층으로 구분하여 만든 "표준 규격" 입니다.

- (물리 계층) 은 전송 매체(케이블, 광섬유 등)를 통해 데이터를 전기 신호 또는 광 신호로 변환하여 물리적으로 전달하는 역할을 합니다.
- (데이터 링크 계층)은 같은 네트워크 내에서 데이터의 오류 검출, 수정 및 흐름 제어를 담당합니다. MAC 주소를 사용해 물리적으로 인접한 장비 간 데이터를 전달합니다.
- (네트워크 계층) 은 서로 다른 네트워크 간의 데이터를 라우팅하고 전달 경로를 결정합니다. IP 주소를 사용하여 목적지까지 데이터를 전달합니다.
- 전송 계층은 프로세스 간의 데이터 전송을 담당하며, TCP와 UDP 프로토콜을 사용해 데이터 전송을 제어합니다.

- 세션 계층은 양 끝 단의 애플리케이션(클라이언트-서버) 간 통신을 관리하고 유지하는 역할을 합니다.
즉, 연결을 생성하고 유지하며, 필요하면 복구하는 기능을 담당

- (프레젠테이션 계층)은 데이터를 응용 계층에서 처리할 수 있는 형식으로 변환하고, 암호화나 압축을 처리합니다. 데이터 포맷 변환, 인코딩, 디코딩 등의 기능을 수행합니다. 예를들면 SSL , JPEC가 있습니다. 
- (응용 계층)은 사용자와 직접적으로 상호작용하는 애플리케이션 프로토콜을 제공합니다. 웹 브라우저, 이메일 등 다양한 네트워크 서비스가 이 계층에서 동작합니다. 예를들면  HTTP, FTP, SMTP가 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">OSI 모델과 TCP/IP 모델의 차이점은 무엇인가요?</strong></summary>

```text
OSI 모델은 7계층으로 구성되어 있고 이론적인 모델입니다. 
각 계층이 명확히 구분되어 있어 개념적으로 이해하기 쉽습니다.

TCP/IP 모델은 실무적으로 많이 사용되는 모델로, 4계층인 (네트워크 인터페이스, 인터넷, 전송, 응용)으로 구성됩니다. 실무에서의 구현과 더 가까운 모델입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">프로토콜 종류</strong></summary>

```text
응용계층에는 FTP, SMTP, Telnet, SSH 프로토콜이 있고,
표현계층에는 SSL, ASCII 프로토콜
전송계층에는 TCP, UDP
네트워크계층에는 IP, ICMP 
데이터링크계층에는 이더넷이 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">패리티 비트(Parity Bit)란 무엇인가</strong></summary>


```text
데이터의 무결성을 확인하는 방법으로, 전송되는 데이터에 대한 간단한 오류 검출을 위해 사용됩니다. 패리티 비트는 주로 1비트로 구성되며
짝수 패리티 또는 홀수 패리티가 있습니다
짝수패리티는 송신하는 데이터에서 1의 개수를 짝수로 맞추기 위해 패리비트를 추가합니다
홀수패리티는 1의 개수를 홀수로 맞추기 위해 패리티비트를 추가합니다

한계점은 1비트의 오류를 검출할 수 있지만 여러 비트가 동시에 잘못될 경우 오류를 감지하지못하고 또한 검출은 가능하지만 수정은 불가능합니다  
```

</details>

---

## 보안

<details>
<summary><strong style="font-size:1.17em">SOP 정책에 대해 설명해주세요</strong></summary>

```text
동일한 출처에서만 리소스를 공유할 수 있게 제한하는 브라우저정책입니다.
단, 이미지태그나 CSS파일등은 교차출처를 허용합니다.
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">CORS(Cross-Origin Resource Sharing)가 무엇이며, 어떻게 작동하나요?</strong></summary>

```text
CORS는 웹 브라우저에서 실행되는 스크립트가 다른 출처의 리소스에 접근할 수 있도록 허용하는 매커니즘입니다.

기본동작은
1. 클라이언트에서 HTTP 요청의 헤더에 Origin을 담아 전달합니다.
2. 서버는 응답헤더에 Access-Control-Allow-Origin을 담아 클라이언트로 전달합니다.
3. 클라이언트에서 Origin과 서버가 보내준 Access-Origin-Allow-Origin을 비교합니다.
4. 만약 유효하지 않다면 그 응답을 사용하지 않고 버리고 유효하면 가져옵니다

정확히는 크게 3가지로, Simple Request, Preflight Request, Credentialed Request 방식이 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Preflight에 대해 설명해 주세요.</strong></summary>

```text
1. 본 요청을 보내기 전에 OPTIONS 메서드로 예비 요청을 먼저 보내서 안전한지 확인합니다
2. 이때 요청의 Origin 헤더에 자신의 출처를 넣고, 실제 요청에 사용할 메서드와 헤더를 설정합니다.
3. 서버는 이 요청에 대한 응답으로 허용되는 Origin, 메서드,헤더 목록을 담고 preflight가 브라우저에 캐시될 수 있는 
시간을 설정해서 반환합니다
4. 브라우저는 보낸 요청과 서버가 응답해준 정책을 비교하여, 해당 요청이 안전한지 확인하고 본 요청을 보내게 됩니다.

```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Credentialed Request에 대해 설명해주세요.</strong></summary>

```text
인증이 필요한 요청, 즉 쿠키나 JWT 같은 인증 정보를 포함할 때 사용합니다.
credentials 옵션을 include로 설정해야 하고
서버에서도 Allow-Credentials 헤더를 true로 설정해야 합니다.
이때는 와일드카드(*)로 출처를 허용할 수 없고, 명시적인 출처를 설정해야 합니다
```
</details>

---

<details>
<summary><strong style="font-size:1.17em">왜 CORS가 필요한가요?</strong></summary>

```text
웹의 발전으로 브라우저에서 다른 출처의 API를 호출하는 일이 많아졌는데,
이때 악의적인 스크립트가 사용자의 데이터를 탈취하는 것을 방지하기 위해 필요합니다.
예를 들어 사용자가 로그인한 상태에서 악성 사이트가 은행 API를 호출하는 것을 막을 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">XSS에 대해서 설명해주세요</strong></summary>

```text
XSS는 웹사이트에 악성 스크립트를 삽입하여 사용자의 브라우저에서 실행되게 하는 공격입니다.
주요 유형은 3가지입니다.

저장형 XSS는 
특정사이트의 DB에 악성 스크립트를 저장하고 다른 사용자가 해당 게시글을 볼 때마다 스크립트가 실행됩니다.

반사형 XSS는
공격 스크립트가 URL 등 요청 파라미터에 포함되어 서버의 응답에 그대로 반영되어 돌아오는 방식입니다.

Dom 기반 XSS는
공격자가 조작 가능한 클라이언트 측 스크립트에서 발생하며, 서버로의 요청과 관계없이 브라우저에서 스크립트가 실행됩니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">CSRF랑 XSS는 어떤 차이가 있나요?</strong></summary>

```text
CSRF 공격은 피해자의 권한을 이용한 원치 않는 요청 전송입니다. 
방지하기 위해 CSRF 토큰이나 SameSite 쿠키 속성 설정, Referrer 검증 등이 있습니다. 

반면, XSS 공격은 공격자가 웹 페이지에 악의적인 스크립트를 삽입하여 사용자의 정보를 탈취하거나 조작하는 공격입니다.
방지하기 위해 
```
</details>

---

<details>
<summary><strong style="font-size:1.17em">SameSite가 뭐죠</strong></summary>

```text
SameSite는 브라우저가 Cross-Site 요청할 때 쿠키를 어떻게 보낼지 결정하는 쿠키의 속성입니다. 
세 가지 값을 설정할 수 있습니다:
Strict는 가장 엄격한 설정으로, 같은 도메인의 요청에만 쿠키를 전송합니다
Lax은 기본값으로, 다른 사이트에서 들어오는 GET 요청과 같은 '안전한' 요청에만 쿠키를 전송합니다.
None은 모든 Cross-Site 요청에 쿠키를 전송합니다. 이 경우 반드시 Secure 속성을 함께 사용해야 합니다.
```

</details>

---


<details>
<summary><strong style="font-size:1.17em">XSS는 프론트엔드에서만 막을 수 있나요?</strong></summary>

```text
백엔드단에서 
입력 값들을 유효성 검증하고, 특수문자들을 제외하기위해 정규식을 통해서 제거합니다.
```
</details>


---

<details>
<summary><strong style="font-size:1.17em">api.naver.com과 www.naver.com은 cors문제도 안생기고 same-site인가요?</strong></summary>

```text
SameSite 관점에서는 
Public Suffix 기준 com 이므로, 그 앞부분까지 같은 사이트로 보기 때문에
Same-site 맞습니다. 따라서 SameSite=Strict여도 쿠키는 전송됩니다.

CORS 판단은 
Origin 기준이므로 프로토콜,도메인,포트가 같아야하는데
도메인이 다르므로
CORS 설정이 필요합니다.
```

</details>

---

## TCP 와 UDP

---

<details>
<summary><strong style="font-size:1.17em">TCP와 UDP의 차이점은 무엇인가요?</strong></summary>


```text
TCP는 연결 지향적이며 데이터 전송의 신뢰성을 보장하는 프로토콜로, 흐름 제어, 오류 수정, 순서 보장을 제공합니다.
UDP는 연결 설정 없이 데이터를 바로 전송하고, 오버헤드가 적으며, 패킷 손실, 순서 보장, 재전송 같은 복잡한 절차가 없기 때문에 빠릅니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Checksum이 무엇인가요?</strong></summary>

```text
체크섬이란, 데이터 무결성을 보장하기 위한 값입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">TCP와 UDP 중 어느 프로토콜이 Checksum을 수행할까요?</strong></summary>

```text
둘 다 수행합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">그렇다면, Checksum을 통해 오류를 정정할 수 있나요?</strong></summary>

```text
Checksum은 오류를 감지할 수 있지만, 정정할 수는 없습니다.
오류가 감지되면, TCP는 해당 패킷을 폐기하고 재전송을 요청합니다.
UDP는 이런 메커니즘이 없어 오류 복구가 불가능합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">TCP가 신뢰성을 보장하는 방법에 대해 설명해 주세요.</strong></summary>

```text
흐름제어로 송신측과 수신측의 데이터 처리 속도 차이로 인한 데이터 손실을 방지합니다.
예를들면, Stop and Wait, Sliding Window 등이 있습니다.

혼잡제어는 네트워크 내의 패킷 수를 제어하여 네트워크 혼잡을 방지합니다.
이를 실현하기 위한 방법으로는 AIMD, Slow Start, Fast Recovery 등이 있습니다.

이외에 순서제어, 재전송 등이 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em"> AIMD, Slow Start, Fast Recovery 설명해주세요.</strong></summary>

```text
AIMD는
RTT(Round Trip Time)마다 혼잡 윈도우를 1씩 선형적으로 증가하다
패킷 손실이 발생하면 혼잡 윈도우를 절반으로 줄이는 방식입니다.

Slow Start는
처음에는 작은 혼잡 윈도우로 시작하고, 
ACK를 받을 때마다 윈도우 크기를 2배씩 증가시키는 방식입니다.

Fast Recovery는
패킷 손실이 발생했을 때 Slow Start로 돌아가지 않고 AIMD로 바로 진행하는 방식입니다.

```

</details>

---

<details>
<summary><strong style="font-size:1.17em">TCP의 혼잡 제어 처리 방법에 대해 설명해 주세요.</strong></summary>

```text
TCP의 혼잡 제어는

Slow Start


처음엔 혼잡 윈도우 크기를 1 로 시작
ACK 받을 때마다 윈도우 크기를 2배씩 증가(지수적 증가)
ssthresh에 도달하거나 패킷 손실이 발생할 때까지 계속


AIMD

ssthresh 도달 후 적용
RTT마다 윈도우 크기를 1씩 증가(선형적 증가)
패킷 손실 시 윈도우 크기를 절반으로 감소


Fast Recovery


중복 ACK 3번 받으면 패킷 손실로 간주
혼잡 윈도우 절반으로 줄이고
바로 AIMD로 진행 (Slow Start로 돌아가지 않음)
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">왜 HTTP는 TCP를 사용하나요?</strong></summary>

```text
HTTP는 신뢰성 있는 데이터 전송을 위해 TCP를 사용합니다.
TCP는 순서보장, 데이터 무결성, 흐름,혼잡 제어로 신뢰성을 보장하기 때문입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">그렇다면, 왜 HTTP/3 에서는 UDP를 사용하나요? 위에서 언급한 UDP의 문제가 해결되었나요?</strong></summary>

```text
HTTP 3는 QUIC 프로토콜을 사용하는데, QUIC은 UDP를 기반으로 하지만, TCP의 기능을 대부분 구현했습니다.
즉, UDP를 사용해 연결 설정 시간을 단축하고, 오버헤드를 줄이면서 TCP의 신뢰성을 유지할 수 있게 되었습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">그런데, 브라우저는 어떤 서버가 TCP를 쓰는지 UDP를 쓰는지 어떻게 알 수 있나요?</strong></summary>

```text
http 버전에 따라 판단합니다.
예를들면 1.1,2.0은 TCP를 사용하고 3.0은 UDP를 사용합니다.
```

</details>

---

## DHCP

---

<details>
<summary><strong style="font-size:1.17em">DHCP가 무엇인지 설명해 주세요</strong></summary>

```text
네트워크에서 컴퓨터 및 기타 네트워크 장치들에게 자동으로 IP주소와 관련 네트워크 설정을 할당하는 프로토콜
입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">DHCP는 몇 계층 프로토콜인가요?</strong></summary>

```text
DHCP는 7계층 응용 계층에 속합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">DHCP는 어떻게 동작하나요?</strong></summary>

```text
1. 클라이언트가 네트워크에 참여할 때 DHCP 서버를 찾기 위해 브로드캐스트 메시지를 보냅니다.
2. DHCP 서버가 할당 가능한 IP 주소를 클라이언트에게 제안
3. 클라이언트가 제안받은 IP 주소 사용을 요청
4. DHCP 서버가 IP 주소 사용을 최종 승인, 
임대 기간(Lease Time) 정보도 포함하여 클라이언트에게 전달
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">DHCP에서 UDP를 사용하는 이유가 무엇인가요?</strong></summary>

```text
1. UDP의 가벼운 특성과 최소한의 처리 오버헤드는 빠른 IP 주소 할당할 수 있습니다.
연결 설정 및 해제 절차가 없기 때문에 DHCP 메시지를 신속하게 전송할 수 있습니다.

2. UDP는 DHCP 작동에 필수적인 브로드캐스트와 멀티캐스트를 지원합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">DHCP에서, IP 주소 말고 추가로 제공해주는 정보가 있나요?</strong></summary>

```text
서브넷 마스크,기본 게이트웨이,DNS 서버 주소 등을 제공합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">DHCP의 유효기간은 얼마나 긴가요?</strong></summary>

```text
DHCP의 유효기간은 DHCP 서버관리자가 설정한 시간에 따라 다릅니다.
보편적으로 8시간에서 7일정도로 설정합니다.
```

</details>

---

## 웹 소켓

---

<details>
<summary><strong style="font-size:1.17em">웹소켓과 소켓 통신의 차이에 대해 설명해 주세요</strong></summary>

```text
웹소켓과 소켓은 모두 양방향 통신을 가능하게 하는 기술이지만,

소켓은 TCP/IP 프로토콜을 직접 이용하는 인터페이스입니다. 
운영체제 수준에서 제공되며, 프로세스 간의 양방향 통신을 위한 끝점(Endpoint) 역할을 합니다.

반면 웹소켓은 HTTP 프로토콜을 기반으로 하는 응용 계층 프로토콜입니다. 
초기 연결 시 HTTP를 통해 핸드셰이크를 수행하고, 
이후 웹소켓 프로토콜로 업그레이드되어 통신합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">소켓과 포트의 차이가 무엇인가요?</strong></summary>

```text
포트는 서비스를 구분하는 번호고,
소켓은 IP주소와 포트번호와 프로토콜로 구성된 실제 통신의 종단점입니다. 

한 포트에 여러 소켓 연결이 가능하고, 실제 데이터 통신은 이 소켓을 통해 이뤄집니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">사용자의 요청이 무수히 많아지면, 소켓도 무수히 생성되나요</strong></summary>

```text
넵 여러 소켓이 생성되지만, 이로 인해 메모리 사용량 증가하고 컨텍스트 스위칭 오버헤드가 발생합니다.

이를 해결하기 위해 미리 소켓을 생성해 놓고 재사용하는 커넥션 풀 방식이나
로드밸런싱으로 여러 서버에 부하를 분산하여 서버당 소켓 수를 제한합니다. 
```

</details>

---
