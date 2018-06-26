

https://stackoverflow.com/questions/46744561/how-to-do-simple-header-authorization-in-net-core-2-0

https://andrewlock.net/adding-default-security-headers-in-asp-net-core/

## CORS 허용에 대하여

```c#
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseCors(builder => {
        builder.AllowAnyOrigin();
        builder.AllowAnyMethod();
        builder.AllowAnyHeader();
        builder.AllowCredentials();
    });
    app.UseMvc();
}
```

`UseCors()`는 `UseMvc()`보다 **반드시** 앞서야 함.

## 우분투 16.04에서 실행

```bash
Failed to load ▒▒▒, error: libunwind.so.8: cannot open shared object file: No such file or dire              ctory
Failed to bind to CoreCLR at '/home/ubuntu/ServicesTester/libcoreclr.so'
```

```bash
$ sudo apt-get install -y libunwind-dev
```
## 우분투 16.04에서 실행2
```bash
An unhandled exception has occurred: The type initializer for 'System.Net.Http.CurlHandler' threw an exception.
System.TypeInitializationException: The type initializer for 'System.Net.Http.CurlHandler' threw an exception. 
---> System.TypeInitializationException: The type initializer for 'Http' threw an exception. 
---> System.TypeInitializationException: The type initializer for 'HttpInitializer' threw an exception. 
---> System.DllNotFoundException: Unable to load DLL 'System.Net.Http.Native': The specified module or one of its dependencies could not be found.
```

[리눅스 배포를 위한 의존성 목록](https://docs.microsoft.com/en-us/dotnet/core/linux-prerequisites?tabs=netcore2x#linux-distribution-dependencies)을 참조해 인스톨.

```bash
$ sudo apt-get install liblttng-ust0
```

## 우분투 16.04에서 실행3

```bash
/etc/systemd/system$ sudo nano myapp.service
```

myapp.service

```bash
[Unit]
Description=우분투에서 실행하는 닷넷코어 앱

[Service]
WorkingDirectory=/var/www/aspnetcore
ExecStart=/usr/bin/dotnet /var/www/aspnetcore/myapp.dll
Restart=always
RestartSec=10 # Restart service after 10 seconds if dotnet service crashes
SyslogIdentifier=myapp
User=www-data
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=api_key=XXXXXXXXXXXXX # 환경변수를 이곳에 지정

[Install]
WantedBy=multi-user.target
```

```bash
$ sudo service myapp start
```

## System.InvalidOperationException: The constraint entry 'version' - 'apiVersion' on the route 'v{version:apiVersion}/Contracts' could not be resolved by the constraint resolver of type 'DefaultInlineConstraintResolver'

의존하는 프로젝트에서 `Microsoft.AspNetCore.Mvc.Versioning` 모듈을 사용하고 있는데, 정작 자신은 이 모듈을 사용하고 있지 않을 때 발생.

우선 현 프로젝트에 `Microsoft.AspNetCore.Mvc.Versioning`를 설치한 후, `Startup.cs`에 다음 코드를 추가하자.

```c#
// This method gets called by the runtime. Use this method to add services to the container.
public void ConfigureServices(IServiceCollection services)
{
    // ...
    services.AddApiVersioning(opt => opt.AssumeDefaultVersionWhenUnspecified = true);
    services.AddMvc();
}
```

## JsonReaderException: Error reading JObject from JsonReader. Path '', line 0, position 0.

`.csproj`파일을 열어 `UserSecretsId` 요소를 제거 한다. 혹은 프로젝트를 우클릭 -> `Manage User Secrets` 클릭해 JSON 파일을 수정한다.