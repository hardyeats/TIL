# [자바는 어떻게 `int`를 `byte`로 변환하는가](https://stackoverflow.com/questions/842817/how-does-java-convert-int-into-byte)
자바에서 `int`는 32비트다. `byte`는 8비트다.
자바에서 대부분의 원시형(primitive type)은 부호가 있으며(signed), `byte`, `short`, `int`, `long`은 2의 보수(two's complement)로 인코딩 된다.
이 숫자 체계에서 가장 중요한 비트는 ++숫자의 부호를 결정하는 비트(MSB)++다. 더 많은 수의 비트가 필요하다면 MSB는 새로운 MSB에 그대로 복사된다.
값이 255(10): 1111 1111(2)인 `byte`가 있다면, 
So if you have byte 255: 11111111 and you want to represent it as an int (32 bits) you simply copy the 1 to the left 24 times.

Now, one way to read a negative two's complement number is to start with the least significant bit, move left until you find the first 1, then invert every bit afterwards. The resulting number is the positive version of that number

For example: 11111111 goes to 00000001 = -1. This is what Java will display as the value.

What you probably want to do is know the unsigned value of the byte.

You can accomplish this with a bitmask that deletes everything but the least significant 8 bits. (0xff)

So:

byte signedByte = -1;
int unsignedByte = signedByte & (0xff);

System.out.println("Signed: " + signedByte + " Unsigned: " + unsignedByte);
Would print out: "Signed: -1 Unsigned: 255"

What's actually happening here?

We are using bitwise AND to mask all of the extraneous sign bits (the 1's to the left of the least significant 8 bits.) When an int is converted into a byte, Java chops-off the left-most 24 bits

1111111111111111111111111010101
&
0000000000000000000000001111111
=
0000000000000000000000001010101
이제 부호 비트(제일 왼쪽)가 8번째 비트가 아니라 32번째 비트이기 때문에(즉 양의 부호를 뜻하는 0이기 때문에),자바는 본래의 8비트를 양의 값으로 읽는다.

edited Aug 19 at 5:05
Stephen C

answered May 9 '09 at 8:00
Wayne

1
well done, the best explanation on this subject, Wayne! I'm just looking for the math formalization why in a two's complement representation the sign bit can be copied on the right in order to add bits. It's easy to understand it thinking to the rule of how to obtain the negative of a number. that is: consider all the bits from right to left and write them unchanged till the first 1 comprised. Then invert the subsequent bits. If i consider the missing bit to be 0s, it's easy to understand that they all go to 1. But i was looking for a more 'math' explanation. – AgostinoX Aug 22 '14 at 19:44

Whats hapenning here signedByte & (0xff) is that 0xff is an interger literal, thus signedByte gets promoted to an integer before the bitwise operation is performed. – Kevin Wheeler Nov 8 '14 at 23:40