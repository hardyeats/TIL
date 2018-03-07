PS C:\WINDOWS\system32> Import-module acmesharp
Import-module : 이 시스템에서 스크립트를 실행할 수 없으므로 C:\Program Files\WindowsPowerShell\Modules\acmesharp\0.9.1.326\ACMESharp-Extensions\ACMESharp-Extensions.psm1 파일을 로드할 수 없습니다. 자세한 내용
은 about_Execution_Policies(https://go.microsoft.com/fwlink/?LinkID=135170)를 참조하십시오.
위치 줄:1 문자:1

Import-module acmesharp

CategoryInfo          : 보안 오류: (:) [Import-Module], PSSecurityException
FullyQualifiedErrorId : UnauthorizedAccess,Microsoft.PowerShell.Commands.ImportModuleCommand

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
```

