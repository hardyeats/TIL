## OAuth2가 뭔데?

[OAuth2](https://oauth.net/2/)란 OAuth 프로토콜(혹은 프레임워크)의 2번째 버전이다.



## 기초 지식

### 역할(Roles)

OAuth2에는 다음의 4가지 역할(role)이 등장한다.

- **Resource Owner** : 일반적으로 당신.
- **Resource Server** : 보호 받아야 할 데이터를 호스팅하고 있는 서버.
- **클라이언트(Client)** : resource server에의 접근을 요청하고 있는 앱.
- **인증 서버(Authorization Server)** : 클라이언트에게 액세스 토큰을 발급해 주는 서버. 클라이언트는 Resource Server에 뭔가를 요청할 때 이 토큰을 사용한다.


### 토큰(Tokens)

토큰이란 클라이언트의 요청을 받았을 때 인증 서버가 생성하는 랜덤 문자열이다.

토큰에는 2가지 종류가 있다.

- **액세스 토큰(Access Token)** 
- **리프레시 토큰(Refresh Token)** : 액세스 토큰과 함께 발급되지만, 엑세스 토큰과는 달리, 클라이언트가 자원 서버에 요청할 때마다 매번 사용하지는 않는다. 액세스 토큰이 만료됐을 때 이를 갱신하기 위해 인증 서버에 보내는 토큰이다.


### Access token scope

스코프(scope)란 액세스 토큰의 권한이다. 스코프가 좁을수록, resource owner가 액세스를 허락할 가능성이 높다.

### HTTPS

OAuth2는 인증 서버와 클라이언트 간 통신에 HTTPS를 사용하기를 요구한다. 둘 간에 민감한 데이터가 오고 가기 때문이다.


## 참고

[Understanding OAuth2](http://www.bubblecode.net/en/2016/01/22/understanding-oauth2/)