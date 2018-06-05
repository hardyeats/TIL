

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

