## Lambdaexception

`LambdaEntryPoint.cs`가 속한 코드의 `namespace`를 바꿨는지 확인하라. 만약 바꿨다면, AWS 콘솔에서 [함수 코드]-[핸들러] 안의 이름을 적당히 바꿔야 한다. `::` 사이로 왼쪽이 어셈블리 이름이고, 오른쪽부터 네임스페이스가 시작된다.



## Insufficient permissions 

```
Unable to access the artifact with Amazon S3 object key '****' located in the Amazon S3 artifact bucket '****'. The provided role does not have sufficient permissions.
```

`CodePipeline`에서 `CodeDeploy`를 통해 스테이징할 때 발생한 실패 메시지.

`CodeBuild`로부터 전달받은 artifact가 없을 때 발생한다. `buildspec.yml`파일을 수정해야 할지도 모름.



## BundleType must be either YAML or JSON 

`CodePipeline`에서 `CodeDeploy`를 통해 스테이징할 때 발생한 실패 메시지.

AppSpec 파일을 작성할 것.



## API GATEWAY에서 특정 버전의 LAMBDA 호출하기

Resouces -> Integration Request -> Lambda Function 이름 수정

`some-function` -> `some-function:Prod`