https://stackoverflow.com/questions/30042791/entity-framework-savechanges-vs-savechangesasync-and-find-vs-findasync





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