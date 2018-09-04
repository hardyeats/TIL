https://stackoverflow.com/questions/30042791/entity-framework-savechanges-vs-savechangesasync-and-find-vs-findasync





## 관계 데이터(navigation property)를 불러오지 못할 때

https://stackoverflow.com/questions/42327515/ef-core-returns-null-relations-untill-direct-access





## PK 를 바꿔야 할 때 마이그레이션 코드 짜는 법

ID가 GUID 문자열인데,  이게 불편해서 타입을 `long`으로 바꾸려는 상황이다.

```c#
public class RefreshToken
{
    [Key]
    [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
    public string Id { get; set; }
    
    // ....
}
```

```c#
public long Id { get; set; }
```

이렇게 코드를 바꾼 후, 파워셸을 열어 해당 프로젝트 폴더로 이동한다.



```powershell
dotnet ef migrations add <당신이 원하는 >
```



그러면 마이그레이션 코드가 자동 생성됐을텐데,  여기서 그냥 업데이트를 하려고 하면, 다음 에러 메시지를 보게 된다.

```
System.InvalidOperationException: To change the IDENTITY property of a column, the column needs to be dropped and recreated.
```



마이그레이션 코드를 좀 손 봐야 한다.

`AlterKey` 메서드를 사용하는 메서드는 전부 먹통이라 보면 된다.

```c#
protected override void Up(MigrationBuilder migrationBuilder)
{
    migrationBuilder.DropPrimaryKey("PK_RefreshTokens","RefreshTokens");
    
    migrationBuilder.DropColumn("Id", "RefreshTokens");

    migrationBuilder.AddColumn<long>(
        "Id", "RefreshTokens")
        .Annotation("SqlServer:ValueGenerationStrategy", SqlServerValueGenerationStrategy.IdentityColumn);

    migrationBuilder.AddPrimaryKey(
        "PK_RefreshTokens", 
        "RefreshTokens", 
        "Id");
}
```



이제 다음 명령을 내리면 데이터베이스 업데이트가 가능하다.

```powershell
dotnet ef database update
```



**물론 이대로 진행하면, 기존에 저장되어 있던 `Id` 컬럼의 내용은 모두 지워지게 된다.**

아직 테스트 기간 중 로컬 DB에서 진행한 과정이기 때문에 문제가 없었던 것.



## The current CSharpHelper cannot scaffold literals of type 'Microsoft.EntityFrameworkCore.Metadata.Internal.DirectConstructorBinding'. Configure your services to use one that can.

ASP.NET Core의 버전과 Entity Framework Core의 버전이 불일치할 때 발생. 위 상황은 `Microsoft.AspNetCore.All`의 버전이 아직 2.0.5인데, `Npgsql.EntityFrameworkCore.PostgreSQL`의 버전을 2.0.2에서 2.1.0으로 올렸을 때 벌어진 일이다.



## Unable to create an object of type ‘SomeDbContext’. Add an implementation of ‘IDesignTimeDbContextFactory<>’ to the project, or see <https://go.microsoft.com/fwlink/?linkid=851728> for additional patterns supported at design time.

클래스 라이브러리 프로젝트에서 `dotnet ef migrations` 등의 명령을 이용해 마이그레이션을 추가하고 데이터베이스를 업데이트할 때 발생하는 에러다. 지시처럼 프로젝트에 `IDesignTimeDbContextFactory`의 구현체를 추가하면 해결된다. 다음 코드를 DB컨텍스트 코드가 있는 Data 폴더에 같이 넣어 두었다.

```csharp
public class DesignTimeDbContextFactory : IDesignTimeDbContextFactory<SomeDbContext>
{
    public SomeDbContext CreateDbContext(string[] args)
    {
            var builder = new DbContextOptionsBuilder<SomeDbContext>();
            string connectionString;
            switch (Util.GetHostingEnvironment())
            {
                case AspnetEnvironment.Development:
                    connectionString = Util.GetDbConnectionString("dev/Some/MySql");
                    break;
                case AspnetEnvironment.Staging:
                    connectionString = Util.GetDbConnectionString("stage/Some/MySql");
                    break;
                case AspnetEnvironment.Production:
                    connectionString = Util.GetDbConnectionString("prod/Some/MySql");
                    break;
                default:
                    throw new ArgumentException("Invalid hosting enviroment variable");
            }
            builder.UseMySql(connectionString);
            return new SomeDbContext(builder.Options);
    }
}
```

