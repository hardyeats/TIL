- 크롬에서, "~에 대한 연결이 더 이상 사용되지 않는 암호화 기술을 사용하여 암호화됩니다."  : 

https://en.wikipedia.org/wiki/Transport_Layer_Security#Data_integrity



https://blogs.msdn.microsoft.com/friis/2016/07/25/disabling-tls-1-0-on-your-windows-2008-r2-server-just-because-you-still-have-one/





https://support.microsoft.com/en-us/help/187498/how-to-disable-pct-1-0-ssl-2-0-ssl-3-0-or-tls-1-0-in-internet-informat



sql server가 문제가 될 수 있다.

https://support.microsoft.com/ko-kr/help/3135244/tls-1-2-support-for-microsoft-sql-server

---

- PUT, DELETE 메소드가 허용되지 않는다.

웹 서버에서 WebDAV를 비활성화 시켜보자.

---

```
[Information] Microsoft.AspNetCore.Authentication.JwtBearer.JwtBearerHandler: Bearer was not authenticated. Failure message: IDX10222: Lifetime validation failed. The token is not yet valid. ValidFrom: '**/**/2018 **:32:31', Current time: '**/**/2018 **:32:22'. 
```

JWT를 발행한 머신의 시간이 JWT를 검증하는 머신의 시간보다 8~9초 빨라서 발생한 일이다. [설정]-[날짜 및 시간]-[인터넷 시간]에서 동기화가 잘 되고 있는지 확인하고, [서비스]-[Windows Time]-[속성]-[일반]에서 시작 유형을 `자동`으로 바꾸고, [복구]에서 실패 시 컴퓨터의 응답을 모두 서비스 다시 시작으로 바꾸자.