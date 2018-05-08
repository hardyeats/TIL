## [form 데이터를 주고 받기](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data)

웹이란 다음과 같은 아주 기초적인 클라이언트/서버 아키텍처로 요약될 수 있다: "한 클라이언트(보통은 웹 브라우저)가 HTTP 프로토콜을 사용해 어느 서버(대부분의 경우 서버는 Apache, Nginx, IIS, Tomcat일 것이다)에 요청을 보내는 것." 서버 역시 <u>같은 프로토콜</u>을 사용해 응답을 한다.

![A basic schema of the Web client/server architecture](https://developer.mozilla.org/files/4291/client-server.png) 

클라이언트 입장에서 HTML form이라는 건, 서버에게 보낼 HTTP 리퀘스트를 만들 때 사용자가 택할 수 있는 간편한 방법 중 하나다.