# Chapter03. 그리디
- 이것이 취업을 위한 코딩테스트다 With 파이썬 

## 그리디 알고리즘
- 그리디 알고리즘(Greedy)은 탐욕법이라고도 한다.
- 현재 상황에서 지금 당장 좋은 것만 고르는 방법
- 문제를 풀기 위한 최소한의 아이디어를 떠올릴 수 있는 능력 요구
- 정당성 분석이 중요하며 단순히 가장 좋아보이는 것을 반복적으로 선택해도 최적의 해를 구할 수 있는지 검토

### 예제 3-1 거스름돈
- [백준 5585 : 거스름돈](https://www.acmicpc.net/problem/5585)

#### Swift 풀이
```swift
import Foundation

var change = 1000 - Int(readLine()!)! // 1000엔 - 지불할 돈
let coins = [500, 100, 50, 10, 5, 1] // 잔돈

var count = 0 // 잔돈 개수

for coin in coins {
    count += change / coin
    change %= coin
}

print(count)
```

### 실전 문제 - 큰 수의 법칙

'큰 수의 법칙'은 일반적으로 통계 분야에서 다루어지는 내용이지만 동빈이는 본인만의 방식으로 다르게 사용하고 있다.

동빈이의 큰 수의 법칙은 다양한 수로 이루어진 배열이 있을 때 주어진 수들을 M번 더하여 가장 큰 수를 만드는 법칙이다.

단, 배열의 특정한 인덱스(번호)에 해당하는 수가 연속해서 K번 초과하여 더해질 수 없는 것이 이 법칙의 특성이다.

예를 들어 순서대로 2, 4, 5, 4, 6으로 이루어진 배열이 있을 때 M이 8이고, K가 3이라고 가정하자.

이 경우 특정한 인덱스의 수가 연속해서 세 번까지만 더해질 수 있으므로 큰 수의 법칙에 따른 결과는 6+6+6+5+6+6+6+5인 46이 된다.

단, 서로 다른 인덱스에 해당하는 수가 같은 경우에도 서로 다른 것으로 간주한다.

예를 들어 순서대로 3, 4, 3, 4, 3으로 이루어진 배열이 있을 때 M이 7이고, K가 2라고 가정하자. 이 경우 두 번째 원소에 해당하는 4와 네 번째 원소에 해당하는 4를 번갈아 두 번씩 더하는 것이 가능하다.

결과적으로 4+4+4+4+4+4+4인 28이 도출된다.

배열의 크기 N, 숫자가 더해지는 횟수 M, 그리고 K가 주어질 때 동빈이의 큰 수의 법칙에 따른 결과를 출력하시오.

- 입력 조건
    - 첫째 줄에 N(2 <= N <= 1,000), M(1 <= M <= 10,000), K(1 <= K <= 10,000)의 자연수가 주어지며, 각 자연수는 공백으로 구분한다.
    - 둘째 줄에 N개의 자연수가 주어진다. 각 자연수는 공백으로 구분한다. 단, 각각의 자연수는 1 이상 10,000 이하의 수로 주어진다.
    - 입력으로 주어지는 K는 항상 M보다 작거나 같다.
- 출력 조건
    - 첫째 줄에 동빈이의 큰 수의 법칙에 따라 더해진 답을 출력한다.

#### Swift 풀이
```swift
import Foundation

let array = readLine()!.split(separator: " ").map{ Int(String($0))! } // 공백으로 구분하여 입력받기

let n = array[0] // 배열의 크기
let m = array[1] // 숫자 더해지는 횟수
let k = array[2] // 연속으로 더할 수 있는 횟수

var numbers = readLine()!.split(separator: " ").map{ Int(String($0))! } // 숫자 배열

numbers.sort() // 숫자 정렬

let num1 = numbers[n-1] // 가장 큰 수
let num2 = numbers[n-2] // 두 번째로 큰 수

var result = 0

for count in 1 ... m {
	if count % k == 0 {
		result += num2
	} else {
		result += num1
	}
}

print(result)
```

### References
- [이것이 취업을 위한 코딩테스트다 with 파이썬](https://www.youtube.com/playlist?list=PLRx0vPvlEmdAghTr5mXQxGpHjWqSz0dgC)