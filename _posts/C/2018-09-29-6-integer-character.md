---
title: (C언어) 6 - 자료형 (1) - 숫자, 문자
date: 2018-09-29T22:00:31+09:00
author: nobbaggu
layout: post
categories: C
image: /images/2018/09/C-썸네일.jpg
tags:
  - ASCII
  - char
  - C언어
  - data type
  - double
  - float
  - int
  - long
  - long long
  - short
  - 실수
  - 아스키코드
  - 자료형
  - 정수
---

<br>

변수를 선언할 때 자료형 을 명시해주는 이유는 다음과 같습니다.

1. **'정수'와 '정수가 아닌 실수'를 표현하는 방식 자체가 다르기 때문에 컴파일러에게 미리 알려줘야한다.**

2. **데이터를 저장할 메모리공간의 크기를 컴파일러에게 알려주어야한다**.

<br>
## 1. 정수 자료형 : 숫자 표현
* * *

C언어에서는 아래와 같은 자료형이 있습니다.

<br>

\<정수\>

|자료형|메모리|표현가능 범위|
|------|------|-------------|
|char|1byte|-128 ~ +127|
|short|2byte|-32,768 ~ +32,767|
|int|4byte|-2,147,483,648 ~ +2,147,483,647|
|long|4byte|-2,147,483,648 ~ +2,147,483,647|
|long long|8byte|-9,223,372,036,854,775,808 ~ +9,223,372,036,854,775,807|

<br>

\<실수\>

|자료형|메모리|표현가능 범위|
|float|4byte|±3.4×10^-37 ~ ±3.4×10^+38|
|double|8byte|±1.7×10^-307 ~ ±1.7×10^+308|

<br>

사실 우리는 **정수형 변수를 선언할 때 보통 int보다 작은 자료형은 잘 쓰지 않습니다. char나 short, int 중 무엇을 쓰던지 사실 CPU의 처리속도는 차이가 거의 나지 않기 때문입니다.** 따라서 메모리를 쥐어짜야하는 경우가 아니라면 대부분의 정수형 자료는 int타입으로 선언합니다.

정수 자료형을 사용하여 표현할 수 있는 숫자의 범위는 그 자료형의 크기가 나타낼 수 있는 경우의 수와 같습니다. 가령 short는 2byte = 16bit이기 때문에 2^16 = 65,536의 경우의 수를 나타낼 수 있습니다. 단, 가장 앞에 오는 최상위 비트(MSB)는 부호를 표현하는데 사용이 됩니다. 나머지 15bit는 정수의 절대크기를 나타내는데 사용됩니다. 2^15 = 32,768 가지의 상태를 나타낼 수 있습니다. 가장 앞의 bit가 0이면 양수, 1이면 음수를 나타냅니다.

음수가 필요없는 경우에는 자료형 앞에 unsigned를 붙여서 해결할 수 있습니다. 예를들어 `unsigned short a;` 라고 선언을 하면 첫번째 bit도 데이터의 크기를 표현하는데 사용이 되기때문에 2^16 = 65,536 가지의 상태를 온전히 데이터의 크기만 표현하는데 사용할 수 있습니다.


<br>
## 2. 정수 자료형 : 문자 표현
* * *

정수 자료형 char는 문자(character)를 표현할 때도 사용됩니다. (물론 다른 정수 자료형도 문자를 나타내는데 사용할 수 있습니다.) 문자가 표현되는 원리를 알려면 ASCII(American Standard Code for Information Interchange)에 대해 알아야합니다. 아스키 코드는 미국표준협회(ANSI)에서 만든 표준 코드체계입니다. 아스키 코드는 문자를 표현하기 위한 약속입니다. 아래 사진은 아스키 코드 테이블입니다.

<br>

![ASCII](https://nobbaggu.github.io/images/2018/09/ASCII.jpg){: width="100%" height="100%"}

~~~ c
int main(void)
{
   char char1 = 'A';
   char char2 = 65;

   printf("The character of char1 is %c\n", char1);
   printf("The ASCII code of char1 is %d\n", char1);
   printf("\n");
   printf("The character of char2 is %c\n", char2);
   printf("The ASCII code of char2 is %d\n", char2);

   return 0;
}
~~~

실행결과

The character of ch1 is A

The ASCII code of ch1 is 65

The character of ch2 is A

The ASCII code of ch2 is 65

계속하려면 아무 키나 누르십시오 . . .

<br>

char1 변수에 'A' 를 저장했습니다. **문자를 대입할때는 ' ' 을 사용합니다**. char2에는 정수 65를 저장했습니다. char1은 'A'로 저장했는데 %d의 서식문자를 사용해 출력을 하면 65가 나옵니다.

반면에 char2에는 정수 65를 저장하였는데 %c의 서식문자를 사용해 출력을 하니 A가 나옵니다. 여기서 알 수 있는건 **char형 변수에 정수를 저장하든 그 정수에 아스키코드상에서 대입이 되는 문자를 저장하든 정확히 같은 행위라는 사실입니다.**

추가로 한 가지를 더 확인을 해보겠습니다.

~~~ c
# include <stdio.h>

int main(void)
{
   char ch1 = 'A';
   printf("%d\n", ch1 + 10);
   printf("%c\n", ch1 + 10);

   return 0;
}
~~~

실행결과

75

K

계속하려면 아무 키나 누르십시오 . . .

char1+10의 출력결과는 75입니다. 'A'에 해당하는 아스키 코드 65에 10을 더했기 때문입니다. char1+10을 %c(문자형태)로 출력하면 'K'가 나옵니다. 아스키코드 75는 문자 'K'이기 때문입니다.

그리고 문자를 표현할 때 char 자료형을 사용하는 이유는 모든 정수 자료형에 문자를 저장할 수 있지만 아스키코드는 0~127의 값 밖에 없기 때문에 char 자료형을 사용하여 모두 표현 가능하기 때문입니다.