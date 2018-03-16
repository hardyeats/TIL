## 관심사의 분리(Separation of Concerns)

관심사의 분리는 개발을 할 때 길잡이가 되어주는 원칙이다. 이 원칙에 의하면, 소프트웨어는 수행하는 작업의 종류에 따라 확실히 분리되어야 한다. 예를 들어, 사용자에게 꼭 알려줘야 하는 아이템이 무엇인지 식별한 후, 그걸 눈에 띄는 서식으로 변환하는 로직을 가진 애플리케이션을 떠올려 보자. 이때 아이템을 고르는 동작과 서식을 변환하는 동작은 분리 되어야 한다. 왜냐하면 이들은 각기 다른 관심사이기 때문이다. 다만 우연히 서로 연관이 닿았을 뿐이다.

구조적으로 애플리케이션을 만들 때, 핵심 비즈니스 동작을 인프라나 유저 인터페이스 로직과 분리함으로써 이 원칙을 따를 수 있다. 이상적으로는, 비즈니스 규칙 및 로직은 별도의 프로젝트로 분리해야 하며, 이 프로젝트는 다른 프로젝트에 의존해선 안 된다. This helps ensure that the business model is easy to test and can evolve without being tightly coupled to low-level implementation details. 관심사의 분리는, 애플리케이션 설계에 있어서 레이어 도입을 고려하게 만드는 핵심적인 원칙이다.

## 캡슐화(Encapsulation)





## References

Architecting Modern Web Apps with ASP.NET Core 2 and Azure