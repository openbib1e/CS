# Chapter06. 메모리와 캐시 메모리

# 06-1. RAM의 특징과 종류

주기억장치에는 크게 RAM과 ROM, 두 가지가 있고,  
'메모리'라는 용어는 그 중 RAM을 지칭하는 경우가 많다.

## RAM의 특징

RAM에는 실행할 프로그램의 명령어와 데이터가 저장된다.

RAM에 저장된 명령어와 데이터는 전원을 끄면 모두 날아가고 이를 **휘발성 저장 장치**(volatile memory)라고 한다.

반면, 전원이 꺼져도 저장된 내용이 유지되는 저장 장치를 **비휘발성 저장 장치**(non-volatile memory)라고 하고,  
하드디스크, SSD, CD-ROM, USB 등과 같은 보조기억장치가 대표적인 비휘발성 저장 장치이다.

비휘발성 저장 장치에 `보관할 대상`을 저장하고, 휘발성 저장 장치에 `실행할 대상`을 저장한다.

CPU는 실행하고 싶은 프로그램이 보조기억장치에 있다면 이를 RAM으로 복사하여 저장한 뒤 실행한다.

## RAM의 용량과 성능

CPU가 실행하고 싶은 프로그램이 보조기억장치에 있다면 이를 RAM으로 가져와하는데,  
RAM 용량이 적다면 보조기억장치에서 실행할 프로그램을 가져오는 일이 잦아져서 실행 시간이 길어지게 된다.

RAM 용량이 충반히 크다면 보조기억장치에서 많은 데이터를 가져와 미리 RAM에 저장할 수 있다.  
이는 동시에 많은 프로그램을 실행하는데 유리하다.

실행할 프로그램을 책에 비유해보자면,  
보조기억장치는 책이 꽂혀 있는 책장과 같고,  
RAM은 책을 읽을 수 있는 책상과 같다.

책상이 크다면 책장으로부터 많은 책을 미리 책상으로 가져와 여러 권을 동시에 읽을 수 있기 때문에 책을 가지러 왔다 갔다 하는 시간을 절약할 수 있다.

이처럼 `RAM 용량이 크면 많은 프로그램들을 동시에 빠르게 실행하는 데 유리`하다.

RAM의 용량에 따라 프로그램 실행 속도는 비례하게 빨라지지는 않는다.  
RAM 용량이 커지면 프로그램 실행 속도가 어느 정도 증가하는 것은 맞지만, 용량이 필요 이상으로 커졌을 때 속도가 그에 비례하여 증가하지는 않는다.

## RAM의 종류

1. DRAM
    - Dynamic RAM
    - 저장된 데이터가 동적으로 사라지는 RAM
    - 데이터 소멸을 막기 위해 주기적으로 재활성화 필요
    - 소비 전력이 비교적 낮고, 저렴하고, 집적도가 높기 때문에 대용량 설계에 용이하여 일반적으로 DRAM을 사용함
2. SRAM
    - Static RAM
    - 저장된 데이터가 정적인(사리지지 않는) RAM
    - DRAM보다 일반적을 속도가 높지만, 상대적으로 소비 전력과 가격이 높고, 집적도가 낮음
    - 대용량으로 설계할 필요는 없으나 빨라야 하는 장치에 사용

|           | **DRAM**   | **SRAM** |
|-----------|------------|----------|
| **재충전**   | 필요함        | 필요 없음    |
| **속도**    | 느림         | 빠름       |
| **가격**    | 저렴함        | 비쌈       |
| **집적도**   | 높음         | 낮음       |
| **소비 전력** | 적음         | 높음       |
| **사용 용도** | 주기억장치(RAM) | 캐시 메모리   |

3. SDRAM
    - Synchronous DRAM
    - 발전된 형태의 DRAM
    - 클럭 신호와 **동기화된** DRAM
    - SDR SDRAM(Single Data Rate SDRAM)이라고 부르기도 함
4. DDR SDRAM
    - Double Data Rate SDRAM
    - 발전된 형태의 SDRAM
    - 최근 가장 대중적으로 사용하는 RAM
    - 대역폭(data rate, 데이터를 주고받는 길의 너비)을 넓혀 속도를 빠르게 만든 SDRAM
    - DDR2 SDRAM은 DDR SDRAM보다 두 배 넓은 SDR SDRAM. 즉 SDRAM보다는 네 배 넓음
    - 최근에 흔히 사용하는 메모리는 DDR4 SDRAM으로 SDR SDRAM보다 열여섯 배 넓은 대역폭을 가짐
