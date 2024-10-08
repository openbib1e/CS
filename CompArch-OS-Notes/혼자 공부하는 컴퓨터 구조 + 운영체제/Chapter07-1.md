# Chapter07. 보조기억장치

# 07-1. 다양한 보조기억장치

## 하드 디스크

**하드 디스크**(Hard Disk Drive)는 자기적인 방식으로 데이터를 저장하는 보조기억장치다.  
이 때문에 하드 디스크를 **자기 디스크**(magnetic disk)의 일종으로 지칭하기도 한다.

하드 디스크에서 실질적으로 데이터가 저장되는 곳은 동그란 원판처럼 생긴 **플래터**(platter)이다.  
플래터는 자기 물질로 덮여 있어 수많은 N극과 S극을 저장하고, N극과 S극은 0과 1의 역할을 수행한다.

플래터를 회전시키는 구성 요소를 **스핀들**(spindle)이라고 하는데,  
스핀들이 플래터를 돌리는 속도는 분당 회전수를 나타내는 **RPM**(Revolution Per Minute) 단위로 표현된다.  
RPM 15,000인 하드 디스크는 1분에 15,000 바퀴를 회전하는 하드 디스크이다.

**헤드**(head)는 바늘 같이 생긴 부품으로 플래터를 대상으로 데이터를 읽고 쓴다.  
일반적으로 플래터는 여러 겹으로 이루어져 있고, 양면 모두 사용할 수 있기 때문에 플래터당 두 개의 헤드가 사용되고,  
이 모든 헤드는 **디스크 암**(disk arm)에 부착되어 다같이 이동한다.

### 하드 디스크 저장 단위

플래터는 **트랙**(track)과 **섹터**(sector)라는 단위로 데이터를 저장한다.

운동장 달리기 트랙과 비슷하게 플래터를 여러 동심원으로 나누었을 때 하나의 원을 트랙이라 하고,  
이 트랙은 피자처럼 여러 조각으로 나누어지는데, 이 한 조각을 섹터라고 한다.

하나 이상의 섹터를 묶어서 **블록**(block)이라 표현하기도 하고,  
하나의 섹터는 512byte~4096byte 정도의 크기를 갖는다.

플래터는 여러 겹으로 사용될 수 있는데,  
플래터 상에서 같은 트랙이 위치한 곳을 모아 연결한 논리적 단위를 **실린더**(cylinder)라고 부른다.

보통 연속된 정보는 한 실린더에 기록된다.  
첫 번째 플래터 윗면과 뒷면,  
두 번째 플래터 윗면과 뒷면 등등  
이렇게 하나의 실린더에 기록하면 디스크 암을 움직이지 않고 바로 데이터에 접근할 수 있기 때문이다.

### 하드 디스크 데이터 접근 과정

하드 디스크가 저장된 데이터에 접근하는 시간은 크게 `탐색 시간`, `회전 지연`, `전송 시간`으로 나눈다.

- 탐색 시간(seek time)
    - 접근하려는 데이터가 저장된 트랙까지 헤드를 이동시키는 시간
- 회전 지연(rotational latency)
    - 헤드가 있는 곳으로 플래터를 회전시키는 시간
- 전송 시간(transfer time)
    - 하드 디스크와 컴퓨터 간에 데이터를 전송하는 시간

이 시간들은 생각보다 많이 걸린다.  
물론 하드 디스크의 성능은 많이 향상되었지만 다량의 데이터를 탐색하고 읽어 들이는 시간은 생각보다 어마하다.

탐색 시간과 회전 지연을 단축시키기 위해서는 플래터를 빨리 돌려 RPM을 높이는 것도 중요하지만,  
참조 지역성, 즉 접근하려는 데이터가 플래터 혹은 헤드를 조금만 옮겨도 접근할 수 있는 곳에 위치해 있는 것도 중요하다.

## 플래시 메모리

우리가 흔히 사용하는 USB 메모리, SD 카드, SSD는 모두 **플래시 메모리**(flash memory) 기반의 보조기억장치이다.

플래시 메모리는 범용성이 넓기 때문에 보조기억장치로만 활용된다고 하기엔 어렵다.  
실제로 주기억장치 중 하나인 ROM에도 사용된다.

플래시 메모리는 크게 `NAND 플래시 메모리`와 `NOR 플래시 메모리`가 있다.  
각각 NAND 연산을 수행하는 회로와 NOR 연산을 수행하는 회로를 기반으로 만들어진 메모리를 뜻한다.  
이 둘 중 **대용량 저장 장치로 많이 사용되는 플래시 메모리는 NAND 플래시 메모리**이다.

플레시 메모리에는 **셀**(cell)이라는 단위가 있다.  
플래시 메모리에서 데이터를 저장하는 가장 작은 단위로, 이 셀이 모여 MB, GB, TB 용량을 갖는 저장 장치가 된다.

한 셀에 몇 비트를 저장할 수 있는지에 따라 플래시 메모리 종류가 나뉜다.

| 이름                       | 셀당 bit |
|------------------------|:------:|
| SLC(Single Level Cell)   | 1비트    |
| MLC(Multiple Level Cell) | 2비트    |
| TLC(Triple Level Cell)   | 3비트    |
| QLC(Quad Level Cell)     | 4비트    |

- SLC
    - 한 셀로 두 개의 정보 표현
    - 비트의 빠른 입출력
    - 긴 수명
    - 용량 대비 고가격
- MLC
    - 한 셀로 네 개의 정보 표현(대용량화 유리)
    - SLC보다 느린 입출력
    - SLC보다 짧은 수명
    - SLC보다 저렴
    - 시중에서 많이 사용
- TLC
    - 한 셀로 여덟 개의 정보 표현(대용량화 유리)
    - MLC보다 느린 입출력
    - MLC보다 짧은 수명
    - MLC보다 저렵
    - 시중에서 많이 사용

### 플래시 메모리 저장 단위

**셀**(cell)들이 모여서 **페이지**(page)가 되고,  
페이지가 모여 **블록**(block)이 되고,  
블록이 모여 **플레인**(plane)이 되고,  
플레인이 모여 **다이**(die)가 된다.

플래시 메모리에서 `읽기와 쓰기는 페이지 단위`로 이루어지고, `삭제는 블록 단위`로 이루어진다.

여기서 페이지는 세 개의 상태를 가질 수 있다.

- Free
    - 어떤 데이터도 저장하고 있지 않아 새로운 데이터를 저장할 수 있는 상태
- Valid
    - 이미 유효한 데이터를 저장하고 있는 상태
- Invalid
    - 유효하지 않는 데이터(쓰레기값)를 저장하고 있는 상태
    - 플래시 메모리는 하드 디스크와 달리 덮어쓰기가 불가능하기 때문에 나타날 수 있는 상태

4개의 페이지로 구성된 한 블록이 있을 때,  
이 블록에 A와 B가 두 페이지로 저장되어 있다면 C라는 새로운 데이터를 저장할 때  
읽기와 쓰기는 페이지 단위로 이루어지기 때문에 한 페이지에 C가 저장될 수 있다.

만약 A 데이터가 저장된 곳에 새로운 A'를 저장하고 싶다면 플래시 메모리는 덮어쓰기가 불가능하기 때문에  
A는 Invalid 상태가 되어 쓰레기값이 되고, 남은 페이지 자리에 A'가 저장된다.

결과적으로 이 블록의 Valid 페이지는 B, C, A'가 된다.

이렇게 쓰레기값이 많아지면 불필요한 용량을 차지하기 때문에 낭비가 일어난다.  
이러한 쓰레기값을 정리하기 위해 SSD를 비롯한 플래시 메모리는 **가비지 컬렉션**(garbage collection)기능을 제공한다.

가비지 컬렉션은 유효한 페이지들만을 새로운 블록에 복사하고 기본 블록을 삭제하여 공간을 정리하는 기능이다.