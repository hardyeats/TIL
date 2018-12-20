# [Data Types](https://www.tutorialspoint.com/csharp/csharp_data_types.htm)
## Value Type
밸류 타입 변수는 값을 곧바로 할당 받을 수 있다. `System.ValueType` 클래스로부터 파생 됐다.
밸류 타입은 데이터를 직접 가진다. 당신이 `int` 타입을 선언하면 시스템은 값을 저장할 메모리를 할당한다.
현 플랫폼에서 타입의 정확한 크기를 알고 싶으면 `sizeof` 메소드를 쓰면 된다. 저장 공간의 크기를 바이트 단위로 출력한다.
```cs
Console.WriteLine($"Size of int: {sizeof(int)} byte(s)");
```
## Reference Type
레퍼런스 타입 변수엔 실제 데이터를 담겨 있지 않다. 대신 변수들에 대한 레퍼런스를 가지고 있다.
다시 말하면, 메모리 주소를 참조하고 있다.
### Ojbect Type
오브젝트 타입은 C# Common Type System(CTS)에서 모든 데이터 타입의 가장 기본이 되는 클래스다. 오브젝트 타입에는 그 어떤 타입의 값도 할당할 수 있지만, 그 전에 형 변환(type conversion)을 해야 한다.
밸류 타입이 오브젝트 타입으로 변환되는 것을 박싱(boxing)이라고 하고, 오브젝트 타입이 밸류 타입으로 변환되는 것을 언박싱(unboxing)이라고 한다.
```cs
object obj;
obj = 100; // 박싱이 이루어짐.
```
### Dynamic Type
```cs
dynamic d = 20;
```
다이나믹 타입과 오브젝트 타입은 비슷하지만, 타입 검사가 이루어지는 시점이 다르다. 다이나믹 타입 변수의 타입 검사는 런 타임에 이뤄지며, 오브젝트 타입의 변수의 타입 검사는 컴파일 타임에 이뤄진다.
### String Type
오브젝트 타입으로부터 파생됐다.
### user-defined reference type
`class`, `interface`, `delegate`
## Pointer Type
포인터 타입 변수에는 다른 타입의 메모리 주소를 저장한다. 포인터 타입에 대해서는 **안전하지 않는 코드(Unsafe Code)**에서 다룬다.
# [형 변환(Type Conversion)](https://www.tutorialspoint.com/csharp/csharp_type_conversion.htm)
C#에선 두 가지 형태의 타입 캐스팅이 있다.
- 암시적 형 변환(implicit type conversion)
- 명시적 형 변환(explicit type conversion) - 유저가 미리 정의된 함수를 사용해 명시적으로 일어남.

# 변수(Variables)
변수란 우리의 프로그램이 사용할 수 있는 저장 공간에 붙여진 이름일 뿐이다. C#에서 각 변수는 특정한 타입을 가지며, 타입은 변수의 크기와 값의 범위와 적용될 수 있는 연산을 결정한다.

|Type|Example|
|----|-------|
|Integral types|sbyte, byte, short, ushort, int, uint, long, ulong, char|
|Floating point types|float, double|
|Decimal types|decimal|
|Boolean types|true or false values, as assigned|
|Nullable types|Nullable data types|
또 다른 밸류 타입으로는 `enum`이 었고, 레퍼런스 타입으로는 `class`가 있다.
## 변수 정의하기
```cs
int i, j, k;
char c, ch;
float f, salary;
double d;
```
변수 정의와 동시에 초기화하려면 -
```cs
int i = 100;
```
## 변수 초기화하기
변수는 등호 뒤에 상수 표현식을 붙여 초기화(값 할당)된다.
```cs
int d = 3, f = 5;    /* initializing d and f. */
byte z = 22;         /* initializes z. */
double pi = 3.14159; /* declares an approximation of pi. */
char x = 'x';        /* the variable x has the value 'x'. */
```
# 캡슐화(Encapsulation)
캡슐화란 물리적 혹은 논리적 패키지 안에 하나 이상의 항목을 넣는 과정이다. 객체지향 프로그래밍 방법론에서 캡슐화란 **구현 세부내용에 대한 접근을 막는 것**이다.
캡슐화는 **접근 제한자(acess specifier)**로 구현할 수 있다. 접근 제한자로 클래스 멤버가 보이는 범위를 정한다. C#이 지원하는 접근 제한자들은 다음과 같다.
- Public
- Private
- Protected
- Internal
- Protected internal

## Public Access Specifier
퍼블릭 접근 제한자는 클래스의 멤버 변수와 함수를 다른 함수나 객체에 노출시킨다. 퍼블릭 멤버는 클래스 바깥에서도 접근할 수 있다.
