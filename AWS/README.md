## Lambdaexception

`LambdaEntryPoint.cs`가 속한 코드의 `namespace`를 바꿨는지 확인하라. 만약 바꿨다면, AWS 콘솔에서 [함수 코드]-[핸들러] 안의 이름을 적당히 바꿔야 한다. `::` 사이로 왼쪽이 어셈블리 이름이고, 오른쪽부터 네임스페이스가 시작된다.