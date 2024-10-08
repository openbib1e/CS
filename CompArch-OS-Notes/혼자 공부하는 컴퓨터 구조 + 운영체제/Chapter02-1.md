# Chapter02. 데이터

# 02-1 0과 1로 숫자를 표현하는 방법

컴퓨터는 0과 1로 모든 정보를 표현하고, 0과 1로 표현된 정보만을 이해할 수 있다.

## 정보 단위
0과 1로 나타내는 가장 작은 정보 단위를 **비트**(bit)라고 한다.

1비트는 0 또는 1, 두 가지 정보를 표현할 수 있다.

2비트는 (0,0), (0,1), (1,0), (1,1) 네 가지 정보를 표현하게 되어 3비트는 여덟 가지 정보를 표현할 수 있다.  
따라서 n비트는 2<sup>n</sup>가지 정보를 표현할 수 있다.

|       |           |
|-------|-----------|
| 1byte | 8bit      |
| 1kB   | 1,000byte |
| 1MB   | 1,000kB   |
| 1GB   | 1,000MB   |
| 1TB   | 1,000GB   |

**바이트**는 여덟 개의 비트를 묶은 단위로 비트보다 한 단계 큰 단위이다.  
1바이트는 8비트와 같으니까 2<sup>8</sup>(256)개의 정보를 표현할 수 있다.

1바이트 1,000개 묶은 단위를 1킬로바이트

1킬로바이트 1,000개 묶은 단위를 1메가바이트

1메가바이트 1,000개 묶은 단위를 1기가바이트

1기가바이트 1,000개 묶은 단위를 1테라바이트

1kB는 1,024byte, 1MB는 1,024kB ... 이런 식으로 표현하는 것은 잘못된 관습이다.  
이전 단위를 1,024개 묶어 표현한 단위는 KiB, MiB, TiB.

### 워드

워드(word)란 CPU가 한 번에 처리할 수 있는 데이터 크기를 의미한다.  
만약 CPU가 한 번에 16비트를 처리할 수 있다면 1워드는 16비트, 한 번에 32비트를 처리할 수 있으면 1워드는 32비트가 된다.

이렇게 정의된 워드의 절반 크기를 하프 워드(half word), 1배 크기를 풀 워드(full word), 2배 크기를 더블 워드(double word)라고 부른다.

따라서 워드의 크기가 큰 CPU는 한 번에 처리할 수 있는 데이터가 많다는 뜻이 된다.

워드 크기는 CPU마다 다르지만, 현대 컴퓨터 워드 크기는 대부분 32비트 또는 64비트로 되어있다.  
인텔 x86 CPU는 32비트 워드 CPU, x64 CPU는 64비트 워드 CPU

## 이진법

수학에서 0과 1만으로 모든 숫자를 표현하는 방법을 이진법(binary)이라고 한다.  
숫자가 1을 넘어가는 시점에 자리 올림을 해서 숫자를 표현하면 된다.

### 이진수 표기
수학적으로 표기할 때는 주로 아래첨자 <sub>(2)</sub>를 사용하고,  
코드 상에서 표기할 때는 주로 이진수 앞에 0b를 붙인다.

이진수 8 표기
1. 1000<sub>(2)</sub>
2. 0b1000

### 이진수의 음수 표현

십진수 음수를 표현할 땐 단순히 숫자 앞에 마이너스 부호를 붙이면 됐지만,  
컴퓨터는 0과 1만 이해할 수 있기 때문에 음수 표현도 0과 1로 해야된다.

0과 1만으로 음수를 표현하는 방법 중 가장 널리 사용되는 방법은 **2의 보수**(two's complement)를 구해 이 값을 음수로 간주하는 방법이다.

2의 보수의 사전적 의미는 '어떤 수를 그보다 큰 2<sup>n</sup>에서 뺀 값'을 의미한다.

예를 들어 11<sub>(2)</sub>의 2의 보수는 11<sub>(2)</sub>보다 큰 2<sup>n</sup>,  
즉 100<sub>(2)</sub>에서 11<sub>(2)</sub>을 뺀 01<sub>(2)</sub>이 되는 것.

하지만 이렇게 사전적 의미로는 이해하기가 조금 어렵고 복잡하기 때문에  
단순하게 `모든 0과 1을 뒤집고, 거기에 1을 더한 값`으로 이해하면 간단하게 이진수의 음수 표현이 가능하다.

같은 예를 들어,  
11<sub>(2)</sub>의 모든 0과 1을 뒤집으면 00<sub>(2)</sub>이고,  
거기에 1을 더한 값은 01<sub>(2)</sub>이 된다. 즉, 11<sub>(2)</sub>의 2의 보수(음수 표현)는 01<sub>(2)</sub>이 된다.

### 플래그

이진수만으로는 이 값이 음수인지 양수인지 구분할 수 없다.  
-1011<sub>(2)</sub>을 표현하기 위한 음수 0101<sub>(2)</sub>과 십진수 5를 표현하기 위한 양수 0101<sub>(2)</sub>은 똑같이 생겼기 때문이다.

그래서 컴퓨터 내부에서 어떤 수를 다룰 때 양수와 음수를 구분하는 **플래그**(flag)를 사용한다.  
이 플래그는 CPU 내부에 플래그 레지스터가 존재해서 구분할 수 있게 한다.

## 십육진법

이진법을 이용해서 컴퓨터가 이해하는 숫자 정보를 직접 표현할 수 있었다.  
하지만 이진법은 0과 1만으로 모든 숫자를 표현하다 보니 숫자의 길이가 너무 길어진다는 단점이 있다.(십진수 32는 100000<sub>(2)</sub>)

그래서 데이터를 표현할 때 이진법 이외에 십육진법도 자주 사용한다.  
십육진법은 수가 15를 넘어가는 시점에 자리 올림을 하는 표현 방식으로 십진수 10, 11, 12, 13, 14, 15는 각각 A, B, C, D, E, F로 표기한다.

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 |
|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|----|----|----|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A  | B  | C  | D  | E  | F  | 10 | 11 |

우리가 편하게 쓰는 십진법도 있는데 굳이 십육진법을 사용하는 주된 이유 중 하나는,  
`이진수를 십육진수로, 십육진수를 이진수로 변환하기 쉽기 때문`이다.

### 십육진수 표기

이진법과 마찬가지로 숫자 뒤에 아래첨자 <sub>(16)</sub>를 붙이거나 숫자 앞에 0x를 붙여 구분한다.

십육진수 15 표기
1. 15<sub>(16)</sub>
2. 0x15

### 십육진수를 이진수로 변환하기

십육진수는 한 글자당 16종류(0~9, A~F)의 숫자를 표현할 수 있다.  
따라서 십육진수 숫자 하나를 이진수로 표현하려면 총 4비트가 필요하게 된다.

십육진수를 이루고 있는 한 글자를 4비트의 이진수로 변환하고 그것들을 그대로 이어 붙이면 십육진수를 이진수로 변환한 값이 된다.

예를 들어 1A2B<sub>(16)</sub>이라는 십육진수가 있을 때,  

| 십육진수 | 1<sub>(16)</sub>   | A<sub>(16)</sub>   | 2<sub>(16)</sub>   | B<sub>(16)</sub>   |
|------|--------------------|--------------------|--------------------|--------------------|
| 이진수  | 0001<sub>(2)</sub> | 1010<sub>(2)</sub> | 0010<sub>(2)</sub> | 1011<sub>(2)</sub> |

십육진수 각 숫자를 4비트 이진수로 바꾸고 이 숫자들을 모두 이어붙인 0001101000101011<sub>(2)</sub>이 1A2B<sub>(16)</sub>를 이진수로 표현한 값이 된다.

### 이진수를 십육진수로 변환하기

이진수 숫자를 네 개씩 끊고, 끊어 준 네 개의 숫자를 하나의 십육진수로 변환한 뒤 그대로 이어 붙이면 된다.

| 이진수  | 1101<sub>(2)</sub> | 0101<sub>(2)</sub> |
|------|--------------------|--------------------|
| 십육진수 | D<sub>(16)</sub>   | 5<sub>(16)</sub>   |

11010101<sub>(2)</sub>이라는 이진수를 십육진수로 변환하면 D5<sub>(16)</sub>가 된다.

이진수를 십진수로 변환할 때는 이렇게 간단하지 않기 때문에 이진수를 십육진수로 묶어 표현하는 것.
