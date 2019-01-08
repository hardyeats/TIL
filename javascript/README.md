# [비트 연산자(Bitwise Operator)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators)
**비트 연산자**는 피연산자들을 32비트(0과 1)의 나열로 취급한다. 예를 들어 십진수 9의 이진수 표기법은 1001이다. 비트 연산자는 이진수 표기법으로 연산을 수행하지만, 결과는 표준 자바스크립트 숫자값으로 반환한다.
```javascript
console.log(5 & 13); // 0101 & 1101 = 0101
// expected output: 5;

console.log(parseInt("0101",2) & parseInt("1101",2));
// expected output: 5;

console.log(5 & 13 & 3); // 0101 & 1101 & 0011 = 0001
// expected output: 1;

console.log(5 | 13); // 0101 | 1101 = 1101
// expected output: 13
```
## 부호가 있는 32비트 정수(Signed 32-bit integers)
모든 비트 연산자의 피연산자는 부호가 있는 32비트 정수(2의 보수 형식)로 변환됩니다. 2의 보수 형식(Two's complement format)이란 어떤 수의 음수가 (예> 5와 -5) 모든 수의 비트가 반전된 것(1의 보수)에서 1을 더한 것이다. 예를 들어 다음은 정수 `314`를 인코딩한 것이다:
```javascript
0000 0000 0000 0000 0000 0001 0011 1010
```
다음은 -`314`를 인코딩한 것이다. 다시 말해 `314`의 1의 보수다:
```javascript
1111 1111 1111 1111 1111 1110 1100 0101
```
다음은 `314`의 2의 보수다:
```javascript
1111 1111 1111 1111 1111 1110 1100 0110
```
2의 보수법은 가장 왼쪽의 비트(부호 비트)가 0이면 양수, 1이면 음수라는 것을 보장한다.
숫자 `0`은 오로지 0 비트로만 이루어진 정수다.
```javascript
0 (10진수) = 0000 0000 0000 0000 0000 0000 0000 0000 (2진수)
```
숫자 `-1`은 오로지 1 비트로만 이루어진 정수다.
```javascript
-1 (10진수) = 1111 1111 1111 1111 1111 1111 1111 1111 (2진수)
```
숫자 `-2147483648` (16진법 표기: -0x80000000)는 부호 비트를 제외하고 0 비트로만 이루어진 정수다.
```javascript
-2147483648 (10진수) = 1000 0000 0000 0000 0000 0000 0000 0000 (2진수)
```
숫자 `2147483647` (16진법 표기: 0x7fffffff)는 부호 비트를 제외하고 1 비트로만 이루어진 정수다.
```javascript
2147483647 (10진수) = 01111111111111111111111111111111 (2진수)
```
`-2147483648`과 `2147483647`은 부호가 있는 32비트로 표현할 수 있는 최솟값과 최댓값이다.