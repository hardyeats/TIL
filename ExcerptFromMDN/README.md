## 

## 클라이언트/서버 아키텍처

웹이란 다음과 같은 아주 기초적인 클라이언트/서버 아키텍처로 요약될 수 있다: "한 클라이언트(보통은 웹 브라우저)가 HTTP 프로토콜을 사용해 어느 서버(대부분의 경우 서버는 Apache, Nginx, IIS, Tomcat일 것이다)에 요청을 보내는 것." 서버 역시 <u>같은 프로토콜</u>을 사용해 응답을 한다.

![A basic schema of the Web client/server architecture](https://developer.mozilla.org/files/4291/client-server.png) 

클라이언트 입장에서 HTML form이라는 건, 서버에게 보낼 HTTP 요청을 만들 때 사용자가 택할 수 있는 간편한 방법 중 하나다. 이를 통해 사용자는 HTTP 요청에 정보를 실어 보낼 수 있다.

## 클라이언트 사이드: 데이터 전송 방법 정의

`<form>` 요소는 데이터가 어떻게 보내질지에 대해 정의한다. `<form>` 요소의 모든 속성은 사용자가 전송(submit) 버튼을 누를 때 전달될 요청을 설정할 수 있도록 설계되어 있다. 2가지 중요한 속성은 `action`과 `method`다.

### `action` 속성

이 속성은 어디로 데이터가 전달될지를 정의한다. 값은 반드시 유효한 URL이어야 한다. 이 속성이 제공되지 않으면 데이터는 form을 지니고 있는 페이지의 URL로 전달된다.

아래 예제에서는, 데이터가 `http://foo.com`이라는 절대 URL로 전송된다.

```html
<form action="http://foo.com">
```

아래에서는 상대 URL을 사용한다. 데이터는 서버의 다른 URL로 전송된다.

```html
<form action="/somewhere_else">
```

아래와 같이 속성 없이 지정하면, `<form>` 데이터는 form이 있는 페이지와 동일한 페이지로 전송됩니다.

````html
<form>
````







# References

[Sending form data](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data)