

프론트엔드에서 구글 계정 로그인을 통해 Id Token 스트링을 발급 받도록 유도한 후, 클라이언트가 보내주는 토큰을 구글 인증 서버에 보내 유효성을 검사하는 방식이다.

```c#
public interface IGoogleAccountsService
{
	[Get("/oauth2/v3/tokeninfo")]
	Task<GoogleIdTokenResponse> GetIdTokenClaims([AliasAs("id_token")] string idToken);
}
```
```c#
public class GoogleIdTokenResponse
{
    [JsonProperty("iss")] public string Issuer { get; set; }
    [JsonProperty("sub")] public string Subject { get; set; }
    [JsonProperty("azp")] public string Azp { get; set; }
    [JsonProperty("aud")] public string Audience { get; set; }
    [JsonProperty("iat")] public string IssuedAt { get; set; }
    [JsonProperty("exp")] public string ExpiredAt { get; set; }

    [JsonProperty("email")] public string Email { get; set; }
    [JsonProperty("email_verified")] public bool EmailVerified { get; set; }
    [JsonProperty("name")] public string Name { get; set; }
    [JsonProperty("picture")] public string PictureUrl { get; set; }
    [JsonProperty("given_name")] public string GivenName { get; set; }
    [JsonProperty("family_name")] public string FamilyName { get; set; }
    [JsonProperty("locale")] public string Locale { get; set; }
}
```

```c#
private readonly IGoogleAccountsService _googleAccountsService;

public AccountsController()
{
    _googleAccountsService = 
        RestService.For<IGoogleAccountsService("https://www.googleapis.com");
}
```



## 참조

[Sign In Using ID Tokens](https://developers.google.com/identity/one-tap/web/idtoken-auth)
```

```