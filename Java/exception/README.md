# Exceptions in Java

## 예외(exception)란 무엇인가?
프로그램 실행 중(=런타임) 프로그램 명령의 정상적인 흐름을 방해하는 원하지 않거나 예상치 못한 이벤트다.

## 오류(error) vs 예외(exception)
오류 : 타당햔 애플리케이션이라면 잡지 말아야 할(should not try to catch) 심각한 문제
예외 : 타당한 애플리케이션이라면 잡으려고 시도할 수 있는(might try to catch) 조건

## 예외 계층 구조
모든 예외 및 오류 타입은 `Throwable` 클래스의 하위 클래스다. `Exception`은 사용자 프로그램이 잡아야 하는 예외적인 조건에 사용된다. `NullPointerException`은 이런 예외 중 하나다. `Error`는 자바 런타임 시스템(JVM)이 런타임 환경(JRE)과 관련된 오류를 나타내기 위해 사용한다. `StackOverflowError`는 이런 오류 중 하나다.
![](http://cdncontribute.geeksforgeeks.org/wp-content/uploads/Exception-in-java1.png)

## JVM이 예외를 처리하는 방법
기본적인 예외 처리: 메소드 안에서 예외가 발생할 때마다, 그 메소드는 `Exception` 객체를 생성해 JVM에게 전달한다. 이 객체는 예외의 이름과 설명, 그리고 예외가 발생한 프로그램의 현재 상태를 가지고 있다. 예외 객체를 만들고 런타임 시스템에 맡기는 일을 예외 던지기(throwing an Exception)라고 부른다. 여기엔 예외가 발생한 메소드에 이르기 위해 호출된 메소드들의 목록이 있을 수 있다. 이 목록을 **콜 스택(Call Stack)**이라고 부른다.
- 런타임 시스템이 콜 스택에서 발생한 예외를 처리하는 코드 블록을 가지고 있는 메소드가 있는지 살펴본다. 이러한 코드 블록을 **예외 핸들러(Exception handler)**라고 부른다.
- 런타임 시스템은 예외가 발생한 메소드부터 시작해 콜 스택을 따라 역순으로 메소드들을 살펴보며 예외 핸들러를 찾는다.
- 런타임 시스템이 적합한 핸들러를 찾았다면 예외를 그 핸들러에게 전달한다.
- 런타임 시스템이 콜 스택에 있는 메소드 전체를 살펴봤는데도 적합한 핸들러를 찾지 못했다면, 예외 객체를 런타임 시스템의 일부인 **기본 예외 핸들러(default exception handler)**에게 넘긴다. 이 핸들러는 예외 정보를 다음과 같은 형식으로 출력하고 **비정상적으로** 프로그램을 종료한다.
```
Exception in thread "xxx" Name of Exception : Description
... ...... ..  // Call Stack
```

아래 도표를 보면서 콜 스택의 흐름을 파악해보자.
![](https://www.geeksforgeeks.org/wp-content/uploads/call-stack.png)

```java
// 예외가 던져졌을 때
// 적합한 예외 핸들러를 찾기 위해
// JVM이 콜스택을 어떻게 탐색하는지 보여주는 JAVA 프로그램
class ExceptionThrown {
    // 예외(ArithmeticException)를 던짐.
    // 이 메소드 안에선 적합한 예외 핸들러를 찾을 수 없음.
    static int divideByZero(int a, int b) {

        // this statement will cause ArithmeticException(/ by zero)
        int i = a/b;

        return i;
    }

    // The runTime System searches the appropriate Exception handler
    // in this method also but couldn't have found. So looking forward
    // on the call stack.
    static int computeDivision(int a, int b) {

        int res =0;

        try {
          res = divideByZero(a,b);
        }
        // doesn't matches with ArithmeticException
        catch(NumberFormatException ex) {
           System.out.println("NumberFormatException is occured");
        }
        return res;
    }

    // 이 메소드에서 적합한 예외 핸들러(즉, 일치하는 catch 블록)를 찾을 수 있음.
    public static void main(String args[]){

        int a = 1;
        int b = 0;

        try {
            int i = computeDivision(a,b);
        }
        // matching ArithmeticException
        catch(ArithmeticException ex) {
            // getMessage will print description of exception(here / by zero)
            System.out.println(ex.getMessage());
        }
    }
}
```
결과:
```
/ by zero.
```

## 프로그래머는 예외를 어떻게 처리해야 하는가?
사용자 정의된 예외 처리: 자바의 예외 처리는 5가지 키워드로 관리된다. `try`, `catch`, `throw`, `throws`, `finally`. 예외를 일으킬 것이라 예상되는 프로그램 구문은 `try` 블록 안에 들어갈 수 있다. `try` 블록 안에서 예외가 발생하면, 그 예외는 던져진다(thrown). 당신의 코드는 이 예외를 잡을(catch) 수 있고(`catch` 블록 사용), 합리적인 방법으로 처리할 수 있다. 시스템에서 생성된 예외는 자바 런타임 시스템에 의해 자동으로 던져진다. 수동으로 예외를 던지려면 `throw` 키워드를 쓰면 된다. 한 메소드 바깥으로 던져질 예외는 `throws` 절에서 지정돼야 한다. `try` 블록이 완료된 이후 `finally` 블록 안의 코드는 반드시 실행해야 한다.


## try-catch 구문의 필요성 (사용자 정의된 예외 처리)
```java
// java program to demonstrate
// need of try-catch clause

class GFG {
    public static void main (String[] args) {

        // array of size 4.
        int[] arr = new int[4];

        // this statement causes an exception
        int i = arr[4];

        // the following statement will never execute
        System.out.println("Hi, I want to execute");
    }
}
```
결과:
```
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 4
    at GFG.main(GFG.java:9)
```
이 경우, JVM은 프로그램을 **비정상적으로** 종료한다. `System.out.println("Hi, I want to execute");`은 결코 실행되지 않는다. 이게 실행되려면, 예외를 try-catch를 이용해 처리해야 한다.

## try-catch 구문 사용법
```java
try {
// block of code to monitor for errors
// the code you think can raise an exception
}
catch (ExceptionType1 exOb) {
// exception handler for ExceptionType1
}
catch (ExceptionType2 exOb) {
// exception handler for ExceptionType2
}
// optional
finally {
// block of code to be executed after try block ends
}
```
기억할 점:
- 한 메소드 안에 예외를 던질 수 있는 구문이 하나 이상이라면 이 구문들을 각각 `try` 블록에 담고 저마다의 `catch` 블록을 통해 서로 다른 예외 핸들러를 제공하라.
- `try` 블록 내에서 발생한 예외는 관련된 예외 핸들러에 의해 처리된다. 예외 핸들러를 연관시키려면 `catch` 블록을 뒤에 두어야 한다. 각 `catch` 블록은 인자 타입의 예외를 처리한다. 인자 타입은 `Throwable` 클래스의 하위 클래스여야 한다.
- `finally` 블록은 선택 사항이다. `try` 블록에서 예외가 발생하든 아니든 반드시 실행된다. 예외가 발생한다면 `try` 블록, `catch` 블록 이후 실행된다. 예외가 발생하지 않았다면 `try` 블록 이후 실행된다. 자바에서 `finally` 블록은 파일을 닫거나 연결을 닫는 클린 업 코드에 주로 쓰인다.


**요약**
![](http://cdncontribute.geeksforgeeks.org/wp-content/uploads/Exception.png)


# References
[Exceptions in Java](https://www.geeksforgeeks.org/exceptions-in-java/)