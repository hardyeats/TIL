# HTTP 개관
HTTP란 HTML 문서와 같은 리소스를 가져올 수 있도록 하는 프로토콜(protocol)<a name="fn1ref"><sup>[1](#fn1)</sup></a>이다. HTTP는 웹 상의 모든 데이터 교환의 기반이다. 또한 일종의 클라이언트-서버 프로토콜인데, 이는 수신자(보통 웹 브라우저)가 요청(request) 시작한다는 의미다. HTML 문서는 텍스트, 레이아웃 설명, 이미지, 비디오, 스크립트 등과 같은 다양한 하위 문서가 덧붙여져 재구성된다.

![](https://mdn.mozillademos.org/files/13677/Fetching_a_page.png)

클라이언트와 서버는 (데이터 스트림이 아니라) 개별 메시지를 교환하여 통신한다. 클라이언트(보통 웹 브라우저)가 보낸 메시지를 **요청(request)**라고 하며, 서버가 보낸 메시지를 **응답(response)**이라고 한다.

![](https://mdn.mozillademos.org/files/13673/HTTP%20&%20layers.png)
HTTP는 1990년대 초에 설계되어 점차 진화해온 확장 가능한 프로토콜이다. TCP 또는 TLS 암호화 TCP 연결을 통해 전송되는 애플리케이션 계층 프로토콜이지만, 이론적으로는 별도의 신뢰할 수 있는 전송 프로토콜을 사용할 수도 있다. 이러한 확장성 덕분에, 단지 HTML 문서를 가져오는 데만 쓰는 게 아니라, 이미지나 비디오를 가져오는 데 쓸 수도 있고, 서버에 컨텐츠를 게시하는 데 쓸 수도 있다. 또한 HTTP는 웹 페이지를 업데이트하기 위해 문서의 일부를 가져올 수도 있다.
## HTTP 기반 시스템의 구성요소
HTTP는 클라이언트-서버 프로토콜이다. 즉, 요청들은 하나의 개체, 즉 유저 에이전트(user-agent)가 전송한다. 지금까지 유저 에이전트는 보통 웹 브라우저였지만, 검색 엔진 인덱스를 채우고 유지하는 크롤러 등 무엇이든 될 수 있다.

개별 요청이 서버로 전달되면, 서버는 이를 처리하고 **응답**이라고 불리는 답변을 제공한다. 이 요청과 응답 사이에는 수많은 개체들이 존재하며, 이들은 게이트웨이나 캐시의 역할을 하는 프록시(proxy)<a name="fn2ref"><sup>[2](#fn2)</sup></a>로 지정되어 서로 다른 작업을 수행한다.

![](https://mdn.mozillademos.org/files/13679/Client-server-chain.png)

실제로 브라우저와 서버 사이에는 많은 컴퓨터들(라우터, 모뎀 등)이 존재한다. 웹의 계층화된 설계 덕분에, 이런 컴퓨터들은 네트워크 계층과 전송 계층에 숨겨져 있다. HTTP는 애플리케이션 계층에 있다. 이런 계층들은 네트워크 문제를 진단하는 데 중요한 부분이지만, HTTP를 설명하는 일과는 관련이 없다.
### 클라이언트: 유저 에이전트
**유저 에이전트(user-agent)**란 사용자를 대신해 행동하는 모든 도구다. 주로 웹 브라우저를 말하며, 엔지니어나 웹 개발자가 사용하는 디버깅 프로그램들을 포함한다.

브라우저는 **항상** 요청을 시작하는 개체다. 서버는 요청을 시작할 수 없다(지난 몇 년 동안 서버 시작 메시지를 시뮬레이션하기 위해 일부 메커니즘이 추가됐지만).

웹 페이지를 표시하기 위해, 브라우저는 HTML 문서를 가져오기 위한 최초 요청을 페이지에 보낸다. 그 다음 이 파일을 파싱해 레이아웃 정보(CSS), 실행 스크립트, 페이지에 포함된 하위 리소스(주로 이미지, 비디오)에 해당하는 추가 요청들을 가져온다. 그런 다음 웹 브라우저는 이 자원들을 혼합해서 완전한 문서를 사용자에게 보여준다. 다음 단계에서 브라우저가 스크립트를 실행하면 더 많은 자원들을 가져올 수 있고, 브라우저는 이에 맞춰 웹 페이지를 업데이트한다.

웹 페이지는 하이퍼텍스트 문서다. 즉, 표시되는 텍스트 중엔 링크가 포함돼 있을 수 있다. 이를 활성화하면(보통 마우스 클릭) 브라우저에게 새로운 페이지를 가져오도록 지시해 웹을 탐색할 수 있다. 브라우저는 이런 지시들을 HTTP 요청으로 번역하고, HTTP 응답을 자세히 해석해 사용자에게 명확한 응답을 제공한다.
### 웹 서버
통신 채널의 반대편에는 클라이언트가 요청한 문서를 내려주는 서버가 있다. 하나의 서버는 오로지 하나의 가상 기계로만 제공된다. 하지만 실제로 그 서버는 여러 서버들로 이뤄졌을 수 있다. 여러 개의 서버들은 함께 부하를 나누고(로드 밸런싱), 다른 컴퓨터들(캐시, DB 서버, 이커머스 서버 등)에게 정보를 얻는 어느 복잡한 소프트웨어를 공유하며, 요청 받은 문서를 전체적으로든 부분적으로든 생성한다.

하나의 서버가 반드시 하나의 기계일 필요는 없다. 여러 개의 서버가 같은 기계에서 호스트될 수도 있다. HTTP/1.1과 `Host` 헤더를 사용하면 그 서버들이 같은 IP 주소를 공유할 수도 있다.
### 프록시
웹 브라우저와 서버 사이에, 수많은 컴퓨터와 기계들이 HTTP 메시지를 전달한다. 웹 스택의 계층화된 구조 때문에, 이들 대부분은 전송, 네트워크 또는 물리적 수준에서 작동한다. HTTP 계층에서는 투명하지만(transparent) 잠재적으로 성능에 상당한 영향을 미친다. 애플리케이션 계층에서 동작하는 기계와 컴퓨터들을 일반적으로 프록시라고 부른다. 이는 투명할 수도 있고 그렇지 않을 수도 있으며(요청이 프록시를 통화하면서 변경될 수도 있으며), 다음과 같은 다양한 기능을 수행할 수도 있다.
- 캐싱
- 필터링
- 로드 밸런싱
- 로깅

## HTTP의 기본적 특성
### HTTP는 간단하다
HTTP 메시지를 프레임 속에 캡슐화하는 HTTP/2 덕분에 복잡해지긴 했지만, HTTP는 일반적으로 간단하고 사람이 읽을 수 있도록 설계되었다. HTTP 메시지는 사람이 읽고 이해할 수 있으며, 초보자가 느낄 수 있는 복잡함이 크지 않다.
### HTTP는 확장가능하다
HTTP/1.0에서 도입된 HTTP 헤더 덕분에, HTTP는 확장하고 실험하기 쉬운 프로토콜이 됐다. 서버와 클라이언트가 간단히 합의하기만 해도 새로운 기능이 도입될 수 있다.
### HTTP is stateless, but not sessionless
HTTP is stateless: 동일한 연결 위에서 연속적으로 수행되는 두 요청 사이에는 어떠한 연관성도 없다. 이는 특정 페이지(예를 들어 이커머스 장바구니)와 일관성 있게 상호작용려는 사용자에게 곧바로 문제가 된다. HTTP의 핵심은 stateless이지만, HTTP Cookie를 통해 stateful session을 사용할 수 있다. 헤더 확장성을 사용하면 HTTP 쿠키가 워크플로에 추가되며, 각각의 HTTP 요청에서 동일한 컨텍스트 혹은 동일한 상태를 공유할 수 있는 세션 생성이 가능하다.
### HTTP와 연결(connections)
연결은 전송 계층에서 제어되며, 따라서 근본적으로는 HTTP의 범위에서 벗어난다. HTTP는 기저에 있는 전송 프로토콜이 연결 기반(connection-based)일 것을 요구하지 않지만, 메시지를 잃지 않을 것(reliable)을 요구한다. 인터넷에서 가장 널리 쓰이는 2가지 전송 프로토콜 중에 TCP는 신뢰할 수 있고(reliable), UDP는 그렇지 않다. HTTP는 연결 기반인 TCP 표준에 의존하지만, 연결을 반드시 요구하지 않는다.

HTTP/1.0은 요청/응답 교환을 할 때마다 TCP 연결을 열였기 때문에 2가지 중요한 결점(slow, cold)을 드러냈다. TCP 연결을 수립하려면 왕복 메시지가 여러 번 오고 가야 하므로 느리다. 그리고 여러 개의 메시지가 정기적으로 오고 가야한다면 차가운 연결(cold connection)보다 따뜻한 연결(warm connection)이 효율적이다.

이러한 결점들을 해결하기 위해 HTTP/1.1은 파이프라이닝(pipelining)과 지속적 연결(persistent connection)을 도입했다. `Connection` 헤더를 이용해 기저의 TCP 연결을 부분적으로 제어할 수 있다. HTTP/2는 한걸음 더 나아가, 단일 연결에서 메시지들을 멀티플렉싱하여 연결을 따뜻하고(warm) 효율적으로 유지한다.

HTTP에 더 적합하고 좋은 전송 프로토콜을 설계하기 위한 실험들이 진행 중이다. 예를 들어 구글은 UDP에 기반을 둔 [QUIC](https://en.wikipedia.org/wiki/QUIC)을 실험 중이다.
## HTTP로 제어할 수 있는 것들
This extensible nature of HTTP has, over time, allowed for more control and functionality of the Web. HTTP의 확장가능한 특성 덕분에, 시간이 지남에 따라 웹의 더 많은 부분을 제어할 수 있게 됐다. 캐시와 인증은 HTTP 역사의 초기부터 다뤄진 기능이다. 반면에 출처 제약(origin constraint)을 완화하는 기능은 2010년대에 추가됐다.
- 캐시
문서를 캐시하는 방법을 HTTP로 제어할 수 있다. The server can instruct proxies, and clients, what to cache and for how long. The client can instruct intermediate cache proxies to ignore the stored document.
- Relaxing the origin constraint
스누핑과 사행활 침해를 막기 위해, 웹 브라우저는 웹 사이트 간을 엄격히 분리한다. 동일한 출처(same origin)의 페이지만이 웹 페이지의 모든 정보에 접근할 수 있다. Though such constraint is a burden to the server, HTTP headers can relax this strict separation server-side, allowing a document to become a patchwork of information sourced from different domains (there could even be security-related reasons to do so).
- 인증(Authentication)
특정한 사용자만 접근할 수 있도록 보호해야 하는 페이지들이 있다. `WWW-Authenticate` 헤더 등을 사용해 HTTP가 제공하는 기본 인증(Basic authentication)을 구현할 수 있다. 혹은 HTTP 쿠키를 사용해 특정한 세션을 설정하는 방법도 있다.
- [Proxy and tunneling](https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling)
서버 및 클라이언트는 종종 인트라넷에 위치하며 다른 사람에게 그들의 실제 IP 주소를 숨긴다. HTTP 요청은 프록시를 통해 이 네트워크 장벽을 통과한다. 하지만 모든 프록시가 HTTP 프록시는 아니다. 예를 들어 SOCKS 프로토콜은 더 낮은 레벨에서 작동한다. Others, like ftp, can be handled by these proxies(lower level protocols).
- 세션
기본적인 HTTP가 stateless 프로토콜이긴 하지만, HTTP 쿠키를 사용하면 세션을 생성하고 요청과 서버 상태를 연결하는 게 가능하다. 이는 이커머스 장바구니 뿐만 아니라 사용자 설정을 허용하는 모든 사이트에 유용하다.

## HTTP flow
When the client wants to communicate with a server, either being the final server or an intermediate proxy, it performs the following steps:
1. TCP 연결을 연다: TCP 연결은 하나 혹은 여러 개의 요청을 보내는 데 사용될 것이고, 하나의 응답을 받기 위해 사용될 것이다. 클라이언트는 새로운 연결을 열거나, 기존 연결을 재사용하거나, 서버에 대한 여러 TCP 연결을 열 수 있다.
2. HTTP 메시지를 모낸다: (HTTP/2 이전의) HTTP 메시지는 사람이 읽을 수 있다. HTTP/2에선 이 메시지들이 프레임 속에 캡슐화되어 곧바로 읽을 수 없지만, 원칙은 그대로 유지된다.
```http
GET/ HTTP/1.1
Host: developer.mozilla.org
Accept-Language: fr
```
3. 서버가 보낸 응답을 읽는다:
```http
HTTP/1.1 200 OK
Date: Sat, 09 Oct 2010 14:28:02 GMT
Server: Apache
Last-Modified: Tue, 01 Dec 2009 20:18:22 GMT
ETag: "51142bc1-7449-479b075b2891b"
Accept-Ranges: bytes
Content-Length: 29769
Content-Type: text/html
<!DOCTYPE html... (here comes the 29769 bytes of the requested web page)
```
4. 연결을 닫거나 추가 요청을 위해 재사용한다.

HTTP 파이프라이닝이 활성화되면 첫번째 응답을 완전히 수신하기를 기다리지 않고 여러 요청을 보낼 수 있다. HTTP 파이프라이닝은 소프트웨어의 오래된 부분이 현대 버전과 공존하는 기존 네트워크에서 구현이 어렵다는 것이 입증되었다. HTTP 파이프라이닝은 HTTP/2에서 프레임 속의 멀티플렉싱 요청으로 대체되었다.
## HTTP 메시지
HTTP/1.1 및 이전 HTTP 메시지는 사람이 읽을 수 있다. HTTP/2에선 메시지가 프레임에 내장된다. 프레임은 헤더의 압축과 멀티플렉싱 같은 최적화를 가능케 하는 새로운 바이너리 구조다. Even if only part of the original HTTP message is sent in this version of HTTP, the semantics of each message is unchanged and the client reconstitutes (virtually) the original HTTP/1.1 request. It is therefore useful to comprehend HTTP/2 messages in the HTTP/1.1 format.
### 요청
![](https://mdn.mozillademos.org/files/13687/HTTP_Request.png)
### 응답
![](https://mdn.mozillademos.org/files/13691/HTTP_Response.png)
## HTTP 기반 API
가장 흔히 쓰이는 HTTP 기반 API는 `XMLHttpRequest`이며 유저 에이전트와 서버 간에 데이터를 교환할 때 사용한다. `Fetch API`도 같은 목적에 쓰이지만 더 강력하고 유연한 기능을 갖추고 있다.

또 다른 API인 서버 전송 이벤트(server-sent events)는 HTTP를 전송 메커니즘으로 사용하여 서버가 클라이언트로 이벤트를 전송할 수 있도록 하는 단방향 서비스다. 클라이언트는 `EventSource` 인터페이스를 사용하여 연결을 열고 이벤트 핸들러를 설정한다. 클라이언트 브라우저는 HTTP 스크림에 도착한 메시지를 적절한 `Event` 객체로 자동 변환하여, 해당 이벤트 `Type`을 처리하도록 등록된 이벤트 핸들러로 전달하거나, (그런 핸들러가 등록되지 않았으면) `onmessage` 이벤트 핸들러로 전달한다.
## 결론
HTTP는 확장가능하고 사용하기 쉬운 프로토콜이다. The client-server structure, combined with the ability to simply add headers, allows HTTP to advance along with the extended capabilities of the Web.

HTTP/2에선 성능을 향상시키기 위해 프레임에 HTTP 메시지를 삽입해서 약간 복잡해였지만, 메시지의 기본 구조는 HTTP/1.0 때와 같다. 세션 플로우도 단순하게 유지되어, 간단한 [HTTP 메시지 모니터](https://developer.mozilla.org/en-US/docs/Tools/Network_Monitor)로도 조사하고 디버깅할 수 있다.

---

<a name="fn1">1</a>: 서로 다른 컴퓨터 간에 데이터를 어떻게 교환할 것인지를 정해둔 규칙들. 디바이스 간에 교환할 데이터의 포맷이 무엇인지 동의가 이뤄진 후에야 디바이스 간 통신이 가능하다. 그런 포맷을 정하는 규칙들의 집합을 프로토콜이라 부른다.[↩](#fn1ref)

<a name="fn2">2</a>: 프록시 서버(proxy server)란 인터넷의 다른 네트워크를 탐색할 때 사용되는 중간 프로그램 혹은 컴퓨터다. 월드 와이드 웹의 컨텐츠에 접근하기 쉽게 만들어 준다. 프록시는 요청을 가로채서 응답을 되돌려준다. 프록시는 요청을 전달(forward)하거나, 전달하지 않거나(캐시), 수정할 수 있다. **리버스 프록시(reverse proxy)**는 인터넷에서 온 요청을 내부 네트워크의 서버로 전달한다.[↩](#fn2ref)