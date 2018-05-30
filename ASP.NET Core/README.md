

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