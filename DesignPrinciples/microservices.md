### 분산 데이터 처리는 어렵다.

원자적 업데이트, 트랜잭션, 일관성/참조 무결성 및 내구성은 매우 중요하며, 포기해서는 안 된다. 불완전하거나 낡았거나 잘못된 데이터를 가지는 것은 무의미하다. ACID가 비즈니스 요구사항인데도 이를 기본적으로 제공하는 DB 기술(많은 NoSQL 데이터베이스, DB-per-마이크로서비스 아키텍처)을 사용하고 있다면, 애플리케이션 차원에서 이를 메워야 한다.

불가능한 일은 아니지만 매우 까다롭다. 특히 각 데이터베이스에 여러 개의 작성자가 있는 분산 설정에서는 데이터 유실, 데이터 일관성 문제 등을 포함한 버그가 발생할 가능성이 높다. For example, consider reading the [Jepsen analyses of well-known distributed database systems](https://jepsen.io/analyses), perhaps starting with the [analysis of Cassandra](https://aphyr.com/posts/294-call-me-maybe-cassandra). I don't understand half of that analysis, but the TL;DR is that distributed systems are so difficult that even industry-leading projects sometimes get them wrong, in ways that can seem obvious in hindsight.

또한 분산 시스템은 더 큰 개발 비용이 필요하다. 어느 정도는 개발 비용과 하드웨어 사이의 직접적인 트레이드 오프가 있다.

## References

[How to handle foreign key constraints when migrating from monolith to microservices?](https://softwareengineering.stackexchange.com/questions/378348/how-to-handle-foreign-key-constraints-when-migrating-from-monolith-to-microservi)



