# [HTTP/1.x의 연결 관리](https://developer.mozilla.org/en-US/docs/Web/HTTP/Connection_management_in_HTTP_1.x)
연결 관리는 HTTP의 핵심 주제다. 연결을 열고 유지하는 일은 웹 사이트와 웹 어플리케이션의 성능에 크게 영향을 미칠 수 있다. HTTP/1.x에는 short-lived connetions, persistent connections, HTTP pipelining 같은 모델들이 있다.

---
HTTP는 클라이언트와 서버 간의 연결을 제공하기 위해 대부분 TCP에 의존한다. 초창기에는 연결 처리를 위해 사용한 모델이 하나였다. 이런 연결들은 수명이 짧았다(short-lived). 즉, 요청이 전송될 때마다 연결이 새로 만들어졌고, 응답이 수신될 떄마다 연결이 닫혔다.

이런 단순한 모델은 태생적으로 성능의 한계를 품고 있었다. TCP 연결을 여는 일은 자원을 소비하는 작업이다. 클라이언트와 서버는 여러 개의 메시지를 주고 받아야 한다. 요청 전송이 필요할 때마다 대역폭과 네트워크 레이턴시는 성능에 영향을 미친다. 모던 웹 페이지들은 필요한 정보를 제공하기 위해 많은 요청들을 요구하기 때문에, 초기 모델로 구현하기엔 비효율적이다.

HTTP/1.1에 이르러 2가지 새로운 모델이 추가 되었다. persistent-connection 모델은 연속적인 요청 사이에 연결을 열어두기 때문에 새로운 연결을 열 필요가 없다. HTTP 파이프라이닝 모델은 한 걸음 더 나아가, 응답을 기다리지 않고 연속 요청 여러 개를 보냄으로써 네트워크 레이턴시를 훨씬 줄인다.

![](https://mdn.mozillademos.org/files/13727/HTTP1_x_Connections.png)

> HTTP/2에서는 연결 관리 모델이 더 추가됐다.

## Short-lived connections
*short-lived connections*는 HTTP/1.0의 기본 모델이다. 각 HTTP 요청은 자신의 고유한 연결 위에서 완료된다.즉, 모든 HTTP 요청 이전에 TCP 핸드셰이크가 일어난단 뜻이다.

The TCP handshake itself is time-consuming, but a TCP connection adapts to its load, becoming more efficient with more sustained (or warm) connections. Short-lived connections do not make use of this efficiency feature of TCP, and performance degrades from optimum by persisting to transmit over a new, cold connection.

이 모델은 HTTP/1.0의 기본 모델이다(`Connection` 헤더가 없으면, 값이 `close`로 설정된다). HTTP/1.1에선 `Connection` 헤더의 값이 `close`일 때만 사용되는 모델이다.

## Persistent connections
short-lived connections는 2가지 큰 문제점이 있다. 새로운 연결을 여는 데 걸리는 시간이 상당하다는 점,그리고 기저에 있는 TCP 연결은 오랫동안 사용될 때(warm connection)만 성능이 좋아진다는 점이다. 이런 문제들을 완화하기 위해, 심지어 HTTP/1.1 이전부터, persistent connection 이란 개념이 고안되었다. *keep-alive conneciton*이라고도 불린다.

persistent connection은 일정 기간 동안 열려 있으면서 여러 요청을 처리하는데 사용된다. 이로써 새로운 TCP 핸드셰이크가 필요없고, TCP의 성능을 활용할 수 있다. 이 연결은 영원히 열려 있진 않다. 유휴 연결(idle connection)이 있다면 곧 닫힐 것이다(서버는 `Keep-Alive` 헤더를 사용해 연결이 열려있을 최소 시간을 정할 수 있다).

persistent connection도 단점이 있다. 유휴 상태인 연결들도 여전히 서버 자원을 소비하며, 과부하 상태에서 Dos 공격이 수행될 수 있다. 이런 경우, 차라리 유휴 상태면 즉시 연결을 닫는 non-persistent connection이 성능 향상을 가져올 수 있다.

HTTP/1.0 연결은 기본적으로 지속적이 않다. `Connection`을 `close` 외의 것으로 설정하면(흔히 `retry-after`) 연결이 지속된다.

HTTP/1.1 연결은 기본적으로 지속되며, 헤더 설정이 필요하지 않다(그러나 HTTP/1.0으로 폴백해야 하는 경우에 대한 방어 수단으로 종종 추가된다).

## HTTP 파이프라이닝
> HTTP 파이프라이닝은 모던 브라우저에서 기본적으로 작동하지 않는다.
> - 버그투성이 프록시가 여전히 흔해서 웹 개발자가 예측하고 진단할 수 없는 이상하고 불규칙한 행동을 야기한다.
> - Pipelining is complex to implement correctly: the size of the resource being transferred, the effective RTT that will be used, as well as the effective bandwidth, have a direct incidence on the improvement provided by the pipeline. Without knowing these, important messages may be delayed behind unimportant ones. The notion of important even evolves during page layout! HTTP pipelining therefore brings a marginal improvement in most cases only.
> - Pipelining is subject to the HOL problem.
> 이런 이유 때문에, HTTP/2에서 파이라이닝은 **멀티플렉싱**으로 대체되었다.

기본적으로 HTTP 요청은 순차적으로 실행된다. 다음 요청은 현재 요청에 대한 응답을 받은 후에만 실행된다. As they are affected by network latencies and bandwidth limitations, this can result in significant delay before the next request is seen by the server.

파이프라이닝은 동일한 지속적 연결을 사용해 응답을 기다리지 않고 연속적인 요청을 보내는 절차다. 이렇게 하면 연결 지연이 방지된다. Theoretically, performance could also be improved if two HTTP requests were to be packed into the same TCP message. The typical MSS (Maximum Segment Size), is big enough to contain several simple requests, although the demand in size of HTTP requests continues to grow.

Not all types of HTTP requests can be pipelined: only idempotent methods, that is `GET`, `HEAD`, `PUT` and `DELETE`, can be replayed safely: should a failure happen, the pipeline content can simply be repeated.

Today, every HTTP/1.1-compliant proxy and server should support pipelining, though many have limitations in practice: a significant reason no modern browser activates this feature by default.

## Domain sharding
> Unless you have a very specific immediate need, don't use this deprecated technique; switch to HTTP/2 instead. In HTTP/2, domain sharding is no longer useful: the HTTP/2 connection is able to handle parallel unprioritized requests very well. Domain sharding is even detrimental to performance. Most HTTP/2 implementations use a technique called connection coalescing to revert eventual domain sharding.

As an HTTP/1.x connection is serializing requests, even without any ordering, it can't be optimal without large enough available bandwidth. As a solution, browsers open several connections to each domain, sending parallel requests. Default was once 2 to 3 connections, but this has now increased to a more common use of 6 parallel connections. There is a risk of triggering DoS protection on the server side if attempting more than this number.

If  the server wishes a faster Web site or application response, it is possible for the server to force the opening of more connections. For example, Instead of having all resources on the same domain, say `www.example.com`, it could split over several domains, `www1.example.com`, `www2.example.com`, `www3.example.com`. Each of these domains resolve to the same server, and the Web browser will open 6 connections to each (in our example, boosting the connections to 18). This technique is called domain sharding.

![](https://mdn.mozillademos.org/files/13783/HTTPSharding.png)

## 결론
연결 관리를 개선하면 HTTP 성능이 대폭 향상된다. HTTP/1.1이나 HTTP/1.0에서 persistent connection을 사용하면 최고의 성능을 발휘한다(연결이 유휴 상태가 되기 전까진). 그러나 파이프라이닝의 실패는 더 우수한 연결 관리 모델 설계로 이어졌고, 이는 HTTP/2에 통합됐다.