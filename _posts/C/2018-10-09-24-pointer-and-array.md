---
title: (C언어) 24 - 포인터와 배열
date: 2018-10-09T17:32:05+09:00
author: nobbaggu
layout: post
categories: C
tags:
  - array
  - C언어
  - pointer
  - 배열
  - 배열 이름
  - 연산
  - 주소값
  - 포인터
---

<br>

이번 내용의 결론은 **"배열은 포인터이고, 포인터는 배열이다."** 가 됩니다.

<br>
## 1. 포인터와 메모리
* * *

**포인터는 데이터가 있는 위치를 가르키는 변수입니다. 직관적으로 생각했을 때 포인터를 +1 증가시키는 행위는 다음 데이터를 가르키도록 하게 될 겁니다. 다음 데이터는 자료형의 크기만큼 위치를 이동시킨 곳에 있습니다.**


![1-11](https://nobbaggu.github.io/images/2018/09/1-11.jpg){: width="80%" height="80%"}

ptr은 data1을 가르킵니다. 정확히는 data1의 첫 번째 byte를 가르킵니다. ptr에 +1을 더하면 4byte를 뛰어넘어 다음 데이터를 가르킵니다. 메모리공간에는 1byte당 하나의 주소값이 할당이 됩니다. 따라서 위 그림의 경우에는 4byte를 뛰어넘기때문에 주소값도 +4 증가합니다.

~~~ c
#include <stdio.h>

int main(void)
{
    int num = 10;
    int * ptr = &num;
    
    printf("%#x, %d\n", ptr, ptr);
    printf("%#x, %d\n", ptr+1, ptr+1);
    printf("%#x, %d\n", ptr+2, ptr+2);
    printf("%#x, %d\n", ptr+3, ptr+3);
    printf("%#x, %d\n", ptr+4, ptr+4);
    
    return 0;
}
~~~

실행결과

0xaffd14, 11533588


0xaffd18, 11533592


0xaffd1c, 11533596


0xaffd20, 11533600


0xaffd24, 11533604


계속하려면 아무 키나 누르십시오 . . .

<br>

위 코드의 결과에서 알 수 있는 건 **"포인터의 증가/감소 연산은 포인터형의 크기만큼 메모리에서의 위치 이동이며 그만큼 주소값이 증가/감소 한다"** 입니다.

<br>
## 2. 배열의 이름은 포인터다
* * *

**배열의 이름은 포인터이며 배열 원소들 중 가장 첫 번째 원소를 가르킵니다.** 그리고 배열도 포인터처럼 \* 연산자를 사용한 연산이 가능하고, 포인터 또한 배열처럼 대괄호 \[ \]를 통한 index값으로 다룰 수 있습니다.

~~~ c
#include <stdio.h>

int main(void)
{
    int iarr[] = {0,1,2,3,4,5,6,7,8,9,10};
    double darr[] = {0.0, 1.1, 2.2, 3.3, 4.4, 5.5, 6.6, 7.7, 8.8, 9.9, 10.10};
    
    printf("%#x, %d\n", iarr, iarr);
    printf("%#x, %d\n", iarr+1, iarr+1);
    printf("%#x, %d\n", iarr+2, iarr+2);
    printf("%#x, %d\n", iarr+3, iarr+3);
    printf("%#x, %d\n", iarr+4, iarr+4);
    
    printf("\n");
    
    printf("%#x, %d\n", darr, darr);
    printf("%#x, %d\n", darr+1, darr+1);
    printf("%#x, %d\n", darr+2, darr+2);
    printf("%#x, %d\n", darr+3, darr+3);
    printf("%#x, %d\n", darr+4, darr+4);
    
    return 0;
}
~~~

실행결과

0x12ff974, 19921268

0x12ff978, 19921272

0x12ff97c, 19921276

0x12ff980, 19921280

0x12ff984, 19921284

<br>
0x12ff914, 19921172

0x12ff91c, 19921180

0x12ff924, 19921188

0x12ff92c, 19921196

0x12ff934, 19921204

계속하려면 아무 키나 누르십시오 . . . 

<br>

int형 배열의 이름은 +1씩 증가연산을 시킬때마다 가르키는 주소값이 +4만큼 증가하면서 다음 원소를 가르키고 double형 배열의 이름은 가르키는 주소값이 +8만큼 증가하면서 다음 원소를 가르킵니다. **배열 이름의 +1 증가연산의 결과는 배열 원소들의 자료형 크기만큼의 값의 증가이다'**는 결론이 나옵니다.

배열 이름은 포인터 연산자 \* 역시도 당연히 사용 가능합니다.

~~~ c
#include <stdio.h>

int main(void)
{
    int arr[] = {0,1,2,3,4,5,6,7,8,9,10};
    
    printf("arr[0] = %d, *arr = %d\n", arr[0], *arr);
    printf("arr[1] = %d, *(arr+1) = %d\n", arr[1], *(arr+1));
    printf("arr[2] = %d, *(arr+2) = %d\n", arr[2], *(arr+2));
    printf("arr[3] = %d, *(arr+3) = %d\n", arr[3], *(arr+3));
    printf("arr[4] = %d, *(arr+4) = %d\n", arr[4], *(arr+4));
    
    return 0;
}
~~~

실행결과

arr\[0\] = 0, \*arr = 0

arr\[1\] = 1, \*(arr+1) = 1

arr\[2\] = 2, \*(arr+2) = 2

arr\[3\] = 3, \*(arr+3) = 3

arr\[4\] = 4, \*(arr+4) = 4

계속하려면 아무 키나 누르십시오 . . .

<br>

배열의 이름 arr가 포인터라면, \*arr를 통해 포인터인 arr가 가르키는 메모리 주소의 data(배열 arr의 가장 첫 번째 원소)에 접근할 수 있어야합니다. arr\[0\]과 \*arr의 값이 같습니다. 정말로 배열의 이름은 가장 첫 번째 원소를 가르키는 포인터였던 것입니다.

<br>
## 3. 포인터도 배열처럼 index 연산이 가능하다
* * *

위에서는 배열 이름이 포인터이기 때문에 포인터의 연산이 모두 가능한 것을 확인했습니다.

그리고 반대로 **포인터 변수 역시 배열과 같은 방법으로 index값을 이용하여 메모리공간에 접근이 가능합니다.**

~~~ c
#include <stdio.h>
int main(void)

{
    int arr[] = {0,1,2,3,4,5};
    int * ptr = &arr[0]; //ptr이 arr[0]의 위치를 가르키도록 초기화
    
    printf("arr[0] = %d, ptr[0] = %d\n",arr[0], ptr[0]);
    printf("arr[1] = %d, ptr[1] = %d\n",arr[0], ptr[1]);
    printf("arr[2] = %d, ptr[2] = %d\n",arr[0], ptr[2]);
    printf("arr[3] = %d, ptr[3] = %d\n",arr[0], ptr[3]);
    printf("arr[4] = %d, ptr[4] = %d\n",arr[0], ptr[4]);
    
    return 0;
}
~~~

실행결과

arr\[0\] = 0, ptr\[0\] = 0

arr\[1\] = 0, ptr\[1\] = 1

arr\[2\] = 0, ptr\[2\] = 2

arr\[3\] = 0, ptr\[3\] = 3

arr\[4\] = 0, ptr\[4\] = 4

계속하려면 아무 키나 누르십시오 . . .

<br>

포인터도 배열처럼 index를 이용하여 ptr\[0\], ptr\[1\], ptr\[2\], . . . 와 같이 index를 통한 값의 참조가 가능합니다. 결국은 서로가 서로의 연산을 이용할 수 있는겁니다.

정리하자면,

**배열의 이름은 가장 첫 번째 원소를 가르키는 포인터이며 \*연산이 가능하다. 그리고 배열 이름의 포인터형은 배열의 원소들의 자료형과 같다. 또한 포인터 역시 배열처럼 index를 이용한 데이터의 접근이 가능하다.**

위의 결론을 수식으로 표현하면 C언에서 포인터와 배열의 중요한 관계식이 나옵니다.

~~~ c
arr[i] = *(arr+i)
*(ptr+i) = ptr[i]
~~~

<br>
## 4. 포인터와 배열의 차이
* * *

사실 **배열=포인터의 관계가 성립하는 것은 아닙니다. 말하자면 배열은 말 그대로 데이터를 담고있는 바구니이고 포인터는 첫 번째 데이터를 가르키는 포인터 변수일 뿐입니다.** 하지만 배열의 이름 자체는 포인터이기 때문에 연산이나 데이터의 접근 방법에 있어서 유사성이 있는것입니다.

<br>

![2-4](https://nobbaggu.github.io/images/2018/09/2-4.jpg){: width="80%" height="80%"}

<br>

또한 배열의 이름과 포인터는 size가 다릅니다.

~~~ c
#include <stdio.h>

int main(void)
{
    int iarr[] = {1,2,3,4,5,6,7};
    double darr[] = {1.1, 2.2, 3.3, 4.4, 5.5, 6.6, 7.7};
    
    int * iptr = &iarr[0];
    double * dptr = &darr[0];
    
    printf("size of iarr : %d\n", sizeof(iarr));
    printf("size of iptr : %d\n", sizeof(iptr));
    printf("size of darr : %d\n", sizeof(darr));
    printf("size of dptr : %d\n", sizeof(dptr));
    
    return 0;
}
~~~

실행결과

size of iarr : 28

size of iptr : 4

size of darr : 56

size of dptr : 4

계속하려면 아무 키나 누르십시오 . . . 

<br>

iarr는 크기가 4byte인 int형 정수를 7개 담고 있으므로 28byte가 나오고 darr는 크기가 8byte인 double형 실수 7개를 담고 있으므로 56byte가 나옵니다. 하지만 포인터의 크기는 항상 4byte가 나옵니다. 이유는 포인터의 개념을 생각해보시면 알 수 있습니다.

포인터는 메모리공간의 주소값을 저장하는 변수입니다. 주소값의 크기는 항상 4byte이기 때문에 sizeof 연산의 결과가 4가 나온겁니다. 4byte는 32bit이고 8개의 hex값으로 나타낼 수 있습니다. 가령 0x11ff2310 같은 값 말입니다. 제가 사용하는 컴파일러는 주소값을 32bit로 표현하도록 설정되어있습니다. 만약 제 컴파일러가 64bit의 주소값을 사용하도록 설정을 하면 모든 포인터의 sizeof 연산의 결과는 8이 나올겁니다. 이는 운영체제때문이 아닙니다. x64의 운영체제도 32bit 컴파일을 할 수 있고 16bit 컴파일도 가능합니다. 16bit로 컴파일러에서는 모든 포인터의 sizeof 연산결과는 2가 나올겁니다.

포인터의 크기와 포인터의 연산은 헷갈릴 수 있습니다. 포인터의 크기는 메모리상의 주소를 나타내기 위해 사용하는 bit수와 관련이 있으며 컴파일 설정에 따라 달라지는 값이고 증가 감소 연산은 포인터가 가르키는 자료형의 크기에 따라 달라지는 겁니다.

<br>

포인터는 변수포인터와 상수포인터로 나뉩니다. **배열의 이름은 상수 포인터이기 때문에 가르키는 곳을 변경할 수 없습니다.** 배열의 이름은 자신의 원소 중 가장 첫 번째 원소만 가르킬 수 있는 상수 포인터입니다.

![3-3](https://nobbaggu.github.io/images/2018/09/3-3.jpg){: width="80%" height="80%"}

배열 이름은 상수 포인터이기 때문에 위 사진과 같이 다른 변수의 주소를 대입하려고 시도하니 오류가 납니다.