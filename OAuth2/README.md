## OAuth2가 뭔데?

[OAuth2](https://oauth.net/2/)란 OAuth 프로토콜(혹은 프레임워크)의 2번째 버전이다.

이전 버전에 비해 프로토콜이 간소화 됐고, 여러 앱 간의 상호 운용성이 촉진될 것으로 기대된다.

## 기초 지식

### 역할(Roles)

OAuth2에는 다음의 4가지 역할(role)이 등장한다.

- **Resource Owner** : 일반적으로 당신.
- **자원 서버(Resource Server)** : 보호 받아야 할 데이터를 호스팅하고 있는 서버.
- **클라이언트(Client)** : 자원 서버에게 요청을 보내고 있는 앱.
- **인증 서버(Authorization Server)** : 클라이언트에게 토큰을 발급해 주는 서버.


### 토큰(Tokens)

토큰이란 인증 서버가 클라이언트의 요청에 따라 생성해 주는 랜덤 문자열이다.

토큰에는 2가지 종류가 있다.

- **액세스 토큰(Access Token)** : 서드 파티 앱이 사용자 데이터에 접근할 수 있도록 만들어 주는 토큰. 클라이언트가 자원 서버에게 요청을 보낼 때, 헤더나 파라미터로 담겨진다. 인증 서버가 정해주는 수명을 가지고 있다.
- **리프레시 토큰(Refresh Token)** : 액세스 토큰이 만료됐을 때 이를 갱신하기 위해 인증 서버에 보내는 토큰이다.


### Access token scope

스코프(scope)란 액세스 토큰의 권한이다. 스코프가 좁을수록, resource owner가 액세스를 허락할 가능성이 높다.

### HTTPS

OAuth2는 인증 서버와 클라이언트 간 통신에 HTTPS를 사용하기를 요구한다. 둘 간에 민감한 데이터가 오고 가기 때문이다.

## Register as a client

### Client registration

### Authorization server response

- Client Id : 유니크한 랜덤 문자열
- Client Secret : 절대 유출돼선 안 되는 비밀 키

> 더 알아보려면  [RFC 6749 — Client Registration](http://tools.ietf.org/html/rfc6749#section-2).

## Authorization grant types

OAuth2 defines 4 grant types depending on the location and the nature of the client involved in obtaining an access token.




## 참고

[Understanding OAuth2](http://www.bubblecode.net/en/2016/01/22/understanding-oauth2/)