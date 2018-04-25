## 윈도우즈에서 redis 사용하기

- 아래 과정은 Windows10 / Windows Server 2008 R2에서 동시에 진행되었음.
- [레디스 윈도우 포팅 릴리즈 페이지](https://github.com/MicrosoftArchive/redis/releases)에서 최신 버전의 `.msi` 파일을 내려받아 실행한다.
- 인스톨 과정 중에 환경변수를 설정하고, 메모리 제한을 100MB로 지정한다.
- nuget에서 `StackExchange.Redis` 를 설치한다.
- 터미널에서 `redis-cli`를 입력해 로컬 서버에 접속한다.
- `ping`을 입력했을 때 `PONG`이 출력되는 것을 확인한다. 서버가 정상적으로 작동한다는 뜻이다.
- 암호설정


```powershell
127.0.0.1:6379> CONFIG get requirepass 
1) "requirepass" 
2) "" 
```

- 이렇듯 공백이 출력된다면 이 인스턴스에 대하여 암호가 설정되지 않았다는 뜻이다.

```powershell
127.0.0.1:6379> CONFIG set requirepass "newpassword" 
OK 
127.0.0.1:6379> auth "newpassword"
OK
127.0.0.1:6379> CONFIG get requirepass 
1) "requirepass" 
2) "newpassword" 
```

https://gigi.nullneuron.net/gigilabs/setting-up-a-connection-with-stackexchange-redis/

- 위의 포스팅을 참조해, 레디스 연결 객체를 싱글턴 패턴으로 생성한다.

```c#
public class FooController : Controller {
    
    private readonly IDatabase _redisDb;

    private static Lazy<ConnectionMultiplexer> conn = new Lazy<ConnectionMultiplexer>(
        () => ConnectionMultiplexer.Connect("localhost"));
    
    public FooController()
    {
        _redisDb = SafeConn.GetDatabase();
    }
}
```



