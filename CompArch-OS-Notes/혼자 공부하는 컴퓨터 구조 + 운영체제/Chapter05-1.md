# Chapter05. CPU 성능 향상 기법

# 05-1. 빠른 CPU를 위한 설계 기법

## 클럭

더 빠른 CPU를 만들기 위한 방법을 생각해보면,  
앞선 강의에서 CPU의 명령어 사이클은 클럭 신호에 맞춰서 실행되기 때문에 클럭 속도를 높이면 이에 맞춰 명령어 사이클도 빠르게 실행될거라고 생각할 수 있다.

이 말이 언제나 적용되는 건 아니지만 일반적으로 맞는 말이 된다.

클럭 속도는 헤르츠(Hz) 단위로 측정되며 클럭이 1초에 100번 반복되면 클럭 속도는 100Hz가 된다.

실제 CPU에서 기본 속도 2.5GHz, 최대 속도 4.9GHz라고 적혀있는 CPU는 1초데 클럭이 25억번에서 최대 49억번 반복하는 것을 나타낸다.  
CPU는 일정한 클럭 속도를 유지하기보다는 고성능을 요하는 때에 순간적으로 클럭 속도를 높여서 유연하게 조절한다.  
강제로 클럭 속도를 더 끌어올리는 기법을 오버클럭킹(overclocking)이라고 한다.

클럭 속도를 무지막지하게 높여서 CPU의 성능을 올리는 것은 발열 문제가 생겨서 클럭 속도만으로는 한계점이 있다.

## 코어와 멀티코어

클럭 속도를 늘리는 방법 이외에 코어수와 스레드 수를 늘려서 CPU의 성능을 올릴 수 있다.

먼저 코어(core)를 이해하려면 현대적인 관점에서 CPU를 재해석할 필요가 있다.

전통적인 관점에서 `명령어를 실행하는 부품`은 원칙적으로 하나만 존재했기에 CPU를 이렇게 불러왔다.

하지만 기술의 발전으로 CPU 내부에 명령어를 실행하는 부품은 얼마든지 만들 수 있게 되었고,  
명령어를 실행한는 부품은 오늘날 `코어`라는 용어로 사용된다.

즉 CPU는 단순히 명령어를 실행하는 부품에서 `명령어를 실행하는 부품을 여러 개 포함하는 부품`으로 명칭의 범위가 확장됐다.  
코어를 여러 개 포함하는 CPU를 **멀티코어 CPU**(multi-core) 또는 **멀티코어 프로세서**라고 부른다.

당연히 단일 코어보다 멀티 코어의 처리 속도가 더 빠르다.  
2.4GHz 단일 코어 CPU보다 1.9GHz 멀티 코어 CPU의 성능이 더 좋다.

하지만 CPU의 연산 속도가 꼭 코어 수에 비례하여 증가하지는 않는다.  
코어마다 처리할 명령어들을 얼마나 적절하게 분배하느냐에 따라 연산 속도가 달라진다.

## 스레드와 멀티 스레드

스레드(thread)의 사전적인 의미는 `실행 흐름의 단위`인데, CPU에서 사용되는 스레드와 프로그래밍에서 사용되는 스레드는 용례가 다르기 때문에 구분하여 이해해야된다.

### 하드웨어적 스레드

`하나의 코어가 동시에 처리하는 명령어 단위`를 의미한다.

지금까지 학습하면서 CPU하나에 명령어를 하나 처리하는 1코어 1스레드 CPU 관점에서만 봤는데,  
2개의 코어에 각각 2개의 스레드, 즉 2코어 4스레드 CPU 같은 경우에는 한 번의 네 개의 명령어를 처리할 수 있는 CPU를 의미한다.

이처럼 하나의 코어로 여러 명령어를 동시에 처리하는 CPU를 **멀티스레드(multithread)프로세서** 또는 **멀티스레드 CPU**라고 한다.

인텔에서는 멀티스레드 기술을 하이퍼스레딩(hyper-threading)이라는 용어로 지칭한다.

### 소프트웨어적 스레드

`하나의 프로그램에서 독립적으로 실행되는 단위`를 의미한다.  
프로그래밍 언어나 운영체제를 학습할 때 접하는 스레드는 보통 이 소프트웨어적으로 정의된 스레드를 의미한다.

하나의 프로그램은 실행되는 과정에서 한 부분만 실행될 수 있지만 프로그램의 여러 부분이 동시에 실행될 수도 있다.

예를 들어, 워드 프로세서 프로그램을 개발할 때 `1. 입력받은 내용 화면에 보여주는 기능`, `2. 입력한 내용 맞춤법 검사`, `3. 입력한 내용 수시로 저장` 이 세가지 기능이 동시에 수행되길 원한다고 가정하면,

이 기능들을 작동시키는 코드를 각각의 스레드로 만들면 동시에 실행할 수 있다.

### 멀티스레드 프로레서

하나의 코어가 동시에 처리하는 명령어 단위인 멀티스레드 프로세서를 설계하는 일은 매우 복잡하지만 가장 큰 핵심은 **레지스터**이다.

프로그램 카운터, 스택 포인터, 메모리 버퍼 레지스터, 등등 하나의 명령어를 처리하기 위해 꼭 필요한 레지스터를 여러 개 갖고 있으면 하나의 코어로 여러 명령어를 동시에 처리할 수 있게 된다.

2코어 4스레드 CPU가 있을 때 메모리 입장에서는 한 번에 하나의 명령어를 처리하는 CPU가 4개 있는 것처럼 인식이 된다.  
그래서 하드웨어 스레드를 논리 프로세서(logical processor)라고 부르기도 한다.

