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

## The OAuth flow

소비자(Consumer)란 OAuth 토큰을 요청하는 앱이다. 서비스 제공자(Service Provider)는 사용자에게 권한을 부여하고 토큰을 발급하는 앱이다.

In this blog post I will demonstrate how to configure authentication with GitHub, so for the sake of this blog post think of GitHub as the Service Provider.

Before anything can be done, you will need to register an application with the Service Provider. Typically you will need to specify a name for the application and a **redirect URI**. Once an application is registered, the Service Provider will provide a **client ID** and a **client secret** which is used during the authentication and token request process.

As for the actual OAuth 2 flow, it looks as follows:

![img](https://d33wubrfki0l68.cloudfront.net/f30d5ac10ca90445be13eea4338d2bbfb18c2ac5/0d726/assets/images/2015-04-14-introduction-to-aspnet5-generic-oauth-provider/oauth-flow.png) 

1. 소비자가, 어느 사용자에게 권한을 부여해달라고 서비스 제공자의 **인증 엔드포인트**에 요청함.
2. The Service Provider authenticates the user and prompts them whether to authorize the Consumer to access their information.
3. 사용자가 소비자를 승인하면, the Service Provider redirects back to the **redirect URI** on the Consumer’s website with a temporary access code.
4. The Consumer calls the **token endpoint** on the Service Provider website to exchange the code for a more permanent access token.
5. The Service Provider grants an access token which can be used to authenticate subsequent requests to protected resources.

## Register as a client

Since you want to retrieve data from a resource server using OAuth2, you have to register as a client of the authorization server.

Each provider is free to allow this by the method of his choice. The protocol only defines the parameters that must be specified by the client and those to be returned by the authorization server.

Here are the parameters (they may differ depending of the providers):

### Client registration

### Authorization server response

- Client Id : 유니크한 랜덤 문자열
- Client Secret : 절대 유출돼선 안 되는 비밀 키

> 더 알아보려면  [RFC 6749 — Client Registration](http://tools.ietf.org/html/rfc6749#section-2).

## Authorization grant types

OAuth2 defines 4 grant types depending on the location and the nature of the client involved in obtaining an access token.




## 참고

[Understanding OAuth2](http://www.bubblecode.net/en/2016/01/22/understanding-oauth2/)

[Authenticate with OAuth 2.0 in ASP.NET Core 2.0](https://www.jerriepelser.com/blog/authenticate-oauth-aspnet-core-2/)