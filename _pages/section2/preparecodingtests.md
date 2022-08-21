---
layout: page
title: 코딩테스트준비
description: >
hide_description: false
toc: true
---

```java
- 소단원은 
{알고리즘, 의사코드, 시간복잡도, Greedy, implementation-Simulation, Brute-Force, Binary Search Algorithm, Algorithm with Math, 정규표현식
- 7/28~29 동안 Math 이전까지의 챕터와 코플릿1~4 번을 혼자 풀고,
- 8/1 월요일 페어와 Math 부분 5~9번을 같이 풀게 되어 있다.
```

## Algorithm

- 알고리즘이란 무엇일까?

> 앞으로 우리가 개발자로서 만나게 될 대부분의 개발 태스크는 알고리즘 문제만큼 어렵지 않습니다. 그러나 새로운 문제에 봉착했을 때, 전략과 알고리즘을 구상하여 실제로 코드로 구현해 보는 경험은 매우 중요합니다. 많은 기업에서 주니어 개발자를 채용할 때에, 알고리즘 풀이를 통해 지원자의 역량을 가늠합니다. 알고리즘 풀이를 통해 지원자의 로직과 문제해결 방식을 확인하고, 이를 통해 개발자다운 사고방식을 보게 됩니다.<div/>by 코드스테이츠

## 의사코드

- 의사코드를 쓰면 어떤 장점이 있을까?
    1. 시간이 단축된다.
    2. 디버깅에 용이하다.
    3. 프로그래밍 언어를 모르는 사람과 소통할 수 있다.  
<br>

- 의사코드는 왜 구체적으로 써야 할까?
    - 의사코드를 실제 코드로 옮기는 과정에서 컴퓨터는 구체적이고 세세한 부분까지 요구하기 때문에  
<br>

- 의사코드를 쓰는 양식이 있나요?
    1. 자연어(영어나 한국어 등)만 사용
    2. 자연어와 프로그래밍 언어를 조합하여 사용  
        ex) if(공기누설이 없다면) return;


### 의사코드 예제

## 시간복잡도(Time Complexity)

![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/Tui5G_7wCwi72RhCtX3-Q-1650954357901.png)

- 시간복잡도란?
    - 알고리즘 문제를 풀다 보면 해답을 찾는 것 못지 않게 효율적으로 문제를 해결했는지도 중요할 것이다.
    - "이것보다 효율적인 방법은 없을까?" "이게 제일 좋은 방법이 맞나?"
    - '효율적인 방법' 을 고민한다는 것은 '시간 복잡도' 를 고민한다는 것과 같은 말이다.
- 이번 챕터에서는 시간 복잡도와 Big-O 표기법에 대해 배울 것이다.

- 시간 복잡도를 표기하는 방법은 다음과 같다.
    1. Big-O : 가장 느린 접근
    2. Big-Ω : 가장 빠른 접근
    3. Big-θ : 둘 사이의 평균

### Big-O
1. O(1)
- 입력값이 아무리 증가해도 소요 시간은 항상 일정함

```java
public int O_1_algorithm(int[] arr, int index) {
  return arr[index];
}

int[] arr = new int[]{1,2,3,4,5};
int index = 1;
int results = O_1_algorithm(arr, index);
System.out.println(results); // 2
```

2. O(n)
- 입력값이 증가함에 따라 같은 비율로 소요 시간이 늘어남

```java
public void O_n_algorithm(int n) {
	for(int i = 0; i < n; i++) {
	// do something for 1 second
	}
}

public void another_O_n_algorithm(int n) {
	for(int i = 0; i < n * 2; i++) {
	// do something for 1 second
	}
}
```

3. O(log n)
- BST 에선 원하는 값을 탐색할 때, 노드를 이동할 때마다 경우의 수가 절반으로 줄고, O(log n)의 시간 복잡도를 가진 알고리즘(탐색기법) 이라고 할 수 있다.


```java
//예: up & down 게임
1.    1~100 중 하나의 숫자를 플레이어1이 고른다 (30을 골랐다고 가정합니다).
2.    50(가운데) 숫자를 제시하면 50보다 작으므로 down을 외친다.
3.    1~50중의 하나의 숫자이므로 또다시 경우의 수를 절반으로 줄이기 위해 25를 제시한다.
4.    25보다 크므로 up을 외친다.
5.    경우의 수를 계속 절반으로 줄여나가며 정답을 찾는다.
```

4. O(n^2)

-말그대로 입력값의 증가에 따라 시간이 입력값의 제곱의 비율로 증가하는 시간복잡도.

```java
public void O_quadratic_algorithm(int n) {
	for(int i = 0; i < n; i++) {
		for(int j = 0; j < n; j++) {
			// do something for 1 second
		}
	}
}

public void another_O_quadratic_algorithm(int n) {
	for(int i = 0; i < n; i++) {
		for(int j = 0; j < n; j++) {
			for(int k = 0; k < n; k++) {
				// do something for 1 second
			}
		}
	}
}
```

5. O(2^n)

- Big-O 표기법 중 가장 느린 시간 복잡도를 지닌다.
- 즉 구현한 알고리즘의 시간 복잡도가 O(2^n) 이라면 다른 접근 방식을 고민해야 한다는 의미이다.

```java
public int fibonacci(int n) {
	if(n <= 1) {
		return 1;
	}
	return fibonacci(n - 1) + fibonacci (n - 2);
}
// 재귀로 구현한 피보나치..
// n 을 40만 두어도 수초가 걸리는 것을 볼 수 있고, n이 100 이상이면 평생 결과를 반환받지 못할 수도..
// 언젠가 시간이 난다면 직접 테스트해보고 싶다.
```

6. Advanced 

- 내용이 이해가 안되거나 오타 또는 오류일 가능성이 있다.


## 탐욕 알고리즘(Greedy)

