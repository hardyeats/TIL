## 테스트 자동화 전략

### 유닛 테스트

유닛테스트는 시스템의 나머지 부분과 완전히 격리된 개별적인 **유닛(unit)**을 실행하는데 집중한다. 의존성들은 **모킹(mocking)**한 채, 특정한 입력을 하면 원하는 결과가 반환되는지 확인하는 작업이다.

일반적으로 하나의 클래스는 하나의 유닛으로 간주되며, 의존성들을 모킹하여 퍼블릭 메서드들을 테스트하게 된다. 이렇게 하면, 코드를 느슨하게 결합된 디자인으로 유도할 수 있다는 추가적인 이점이 있다. 그렇지 않으면 클래스를 의존성으로부터 분리할 수 없기 때문이다.

또한, 전체 애플리케이션을 시작하지 않고도, 코드를 작성하고 실행할 수 있다는 사실은 매우 중요하다.

- You will get the most benefits from them on methods rich in business logic, where you want to exercise different inputs, corner cases or error conditions.
- However, in areas of your code that concentrate on dealing with external dependencies and infrastructure (like databases, files, services, 3rd party libraries/frameworks), these tests add considerably less value. Most of what this code does is dealing with external dependencies that you will be mocking in your tests!
- Hence the importance of a testing strategy that combines different methods!

When it comes to running your unit tests, they are fast and require no special configuration on your Continuous Integration (CI) servers.

## Reference

[Unit Testing ASP.NET Core Applications](http://www.dotnetcurry.com/aspnet-core/1414/unit-testing-aspnet-core)