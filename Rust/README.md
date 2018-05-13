## 소유권(Ownership)이란 무엇인가?

### 스택(Stack)과 힙(Heap)

많은 프로그래밍 언어를 다룰 때, 스택과 힙에 대해 자주 생각해야할 일은 드물다. 하지만 러스트 같은 시스템 프로그래밍 언어를 다룰 땐, 어떤 값을 스택에 두느냐 힙에 두느냐에 따라 언어가 취하는 행동이 달라진다. 따라서 프로그래머는 분명하게 결정을 할 필요가 있다.

스택과 힙이란 런타임에 당신의 코드가 사용할 수 있는 메모리의 일부분이다. 하지만 서로 다른 방식으로 구성돼 있다. 스택은 받은 순서대로 값을 저장하며, 정반대의 순서로 값을 제거한다. 이를 후입선출(*last in, first out*)이라 부른다. 높이 쌓은 그릇 더미를 생각해보라. 그 더미에 그릇을 더 추가하고자 한다면, 맨 위에 얹게 될 것이다. 그릇을 꺼낼 때도 마찬가지다. 그릇을 밑이나 중간에 끼워 넣거나 빼는 건 결코 쉽지 않다! 데이터를 추가하는 걸 *pushing onto the stack*이라 부르고, 데이터를 제거하는 걸 *popping off the stack*이라 부른다.

데이터 처리 방식이 이렇게 때문에 스택은 빠르다. 데이터를 추가할 장소, 데이터를 조회할 장소를 찾을 필요가 없다. 그 장소는 항상 맨 위이기 때문이다. 그리고 스택에 있는 데이터는 항상 미리 알 수 있는 고정된 크기를 가지기 때문에 데이터 처리 속도가 빠르다.

컴파일 타임에 크기를 모르거나 크기가 바뀔 수 있는 데이터는 힙에 저장된다. 당신이 힙에 데이터를 저장하고자 한다면, 운영체제는 힙에 충분한 공간이 있는지 알아보기 시작한다. 그리고 그 공간에 "사용중"이라고 표시한 후, **포인터**(pointer)를 반환한다. 그 공간의 위치다. 이러한 과정을 *allocating on the heap*이라고 부르며, 종종 allocating이라고 줄여 말한다. 스택에 값을 푸시하는 것은 allocating이라 취급되지 않는다. 포인터는 크기가 얼만지 알고 바뀔 수 없으니까, 스택에 저장할 수 있다. 하지만 실제 데이터가 필요하다면 포인터를 따라가야 한다.

식당에 들어갔을 때를 떠올려 보자. 일단 일행이 몇 명인지를 알려주면, 종업원은 적당한 크기의 빈 테이블로 우리를 안내해 줄 것이다. 만약 일행 중 지각한 사람이 있다면, 종업원에게 우리가 어떤 테이블에 앉아있는지 물어볼 수 있을 것이다.

힙에 있는 데이터에 접근하는 것은 스택에 있는 데이터에 접근하는 것보다 느리다. 왜냐하면 포인터를 따라가야 하기 때문이다. 비유를 계속 이어나가 보자면,  서버가 수많은 테이블로부터 주문을 받아야 하는 식당이라고 생각해 보자. It’s most efficient to get all the orders at one table before moving on to the next table. Taking an order from table A, then an order from table B, then one from A again, and then one from B again would be a much slower process. By the same token, a processor can do its job better if it works on data that’s close to other data (as it is on the stack) rather than farther away (as it can be on the heap). Allocating a large amount of space on the heap can also take time.

당신의 코드가 어떤 함수를 호출할 때, 그 함수로 값들(거기엔 힙에 있는 데이터를 가리키는 포인터들이 포함될 수도 있을 것이다)이 전달되고, 함수의 지역 변수들이 스택으로 푸시된다. 그리고 함수가 끝났을 때 그 값들은 스택에서 팝된다.

코드의 어느 부분이 힙에 있는 어느 데이터를 쓰고 있는지 파악하는 것, 힙에서 데이터를 복제하는 걸 최소화하는 것, 힙에 있는 사용하지 않는 데이터를 지워서 공간을 아끼는 것은 모두 **소유권(ownership)**이란 개념이 다루는 문제다. 소유권을 이해하게 되면 스택과 힙에 대해 자주 고려하지 않아도 된다. 하지만 힙데이터를 잘 다루기 위해 소유권이 등장했다는 사실을 알면, 소유권이 어떻게 작동하고 무슨 일을 하는지 이해하는 데 도움이 된다.

### 소유권의 규칙

1. 러스트에서 값은 변수를 가지며, 그 변수는 그 값의 **소유자(owner)**라고 부른다.
2. 한 순간에 소유자는 한 명 뿐이다.
3. When the owner goes out of scope, the value will be dropped.

### 변수 스코프







## References

[What is Ownership?](https://doc.rust-lang.org/stable/book/second-edition/ch04-01-what-is-ownership.html)