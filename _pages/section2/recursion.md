---
layout: page
title: [자료구조/알고리즘]재귀
description: >
hide_description: false
toc: true
toc_sticky
---
{TOC}

## 시작하면서
- 배울 것:
    1. 재귀함수의 필요성, 재귀함수를 사용하기 위한 코드
    2. 재귀함수와 반복문의 차이 이해
    3. 재귀 함수의 동작 원리와 예제
- 과제:
    1. 페어와 함께 코플릿
    2. JSON 
    3. StringifyJSON


## 재귀 함수의 이해
### 재쉬 함수란
```java
public void recursion() {
  System.out.println("This is");
  System.out.println("recursion!");
  recursion();
}
//실행 시 두 sout 이 반복된다.
```
```java
1. 재귀함수의 장점
- 반복문과 변수를 여러개 사용할 필요가 없으므로, 코드가 간결해지고, 수정이 용이해진다.
2. 재귀함수의 단점
- 반복문에 비해 더 많은 메모리를 사용
- 메서드 종료 이후 복귀를 위한 스위칭 비용이 발생
3. 재귀함수를 사용하기 위한 조건
- 문제의 크기를 작은 단위로 쪼갤 수 있어야 한다.
- 재귀 호출이 종료되는 시점이 존재해야 한다.
```
### 다르게 생각하기
```java
//기존에 자연수로 이루어진 리스트(배열)의 합을 구하는 알고리즘은 
public int arrSum(int[] arr) {
  int sum = 0;
  for(int i = 0; i < arr.length; i++) {
    sum += arr[i];
  }
  return sum;
}
//이었다.
```
```java
public int arrSum (int[] arr) {
  // 빈 배열을 받았을 때 0을 리턴하는 조건문
  //   --> 가장 작은 문제를 해결하는 코드 & 재귀를 멈추는 코드
  if (arr.length == 0) {
    return 0;
  }

  // 배열의 첫 요소 + 나머지 요소가 담긴 배열을 받는 arrSum 함수
  //   --> 재귀(자기 자신을 호출)를 통해 문제를 작게 쪼개나가는 코드
	return arr[0] + arrSum(arr);
}
```




## 재귀적 사고 연습하기
### 1.재귀함수의 동작원리
```java
이 부분은 텍스트로 되어있는데 글만 읽어서는 무슨 말인지 이해가 되지 않는다. 예제를 풀면서 이해해야겠다.
```
```java
public int arrSum(int[] arr) {
  //Base Case : 문제를 더 이상 쪼갤 수 없는 경우 (재귀의 기초)
  if (arr의 길이가 0인 경우) {
    return 0;
  }
  /*
  * Recursive Case : 그렇지 않은 경우
  * 문제를 더 이상 쪼갤 수 없는 경우
  * head: 배열의 첫 요소
  * tail: 배열의 첫 요소만 제거된 배열
  */
  return head + arrSum(tail);
}
```
```java
public type recursive(input1, input2, ...) {
  // Base Case : 문제를 더 이상 쪼갤 수 없는 경우
  if (문제를 더 이상 쪼갤 수 없을 경우) {
    return 단순한 문제의 해답;
  }
  // recursive Case
  // 그렇지 않은 경우
  return 더 작은 문제로 새롭게 정의된 문제
  // 예1. someValue + recursive(input1Changed, input2Changed, ...)
  // 예2. someValue * recursive(input1Changed, input2Changed, ...)
}
```
```java
위 두 예제 역시 이해가 되지 않는다..다음 예제를 살펴보자.
```

### 예제 - 구구단
```java
다음을 인텔리제이로 돌려보자.
```
//반복문으로 구현한 구구단 메서드
```java

public class test {
	public static void main(String[] args) {

		# 2단부터 시작하고 9단까지 실행하며 반복문이 한번 돌때마다 1씩 증가 시킵니다.
		for(int i=2; i < 10; i++) {
			System.out.println(i + "단을 출력 합니다.");
            
  	         	# 위에서 i의 값이 2라면 2x1 ~ 2x9 까지 진행 합니다.
    		        # 이 반복문(j)이 종료되면 위의 반복문 변수 i가 1 증가하여 다시 3x1 ~ 3x9 까지 진행하는 식으로 9단까지 반복 합니다
			for(int j=1; j < 10; j++) {
				System.out.println(i + " x " + j + " = " + i * j);
			}
			System.out.println();
		}	
	}
}
출처: https://nirsa.tistory.com/159 [Nirsa:티스토리]
```


// 재귀 호출로 구현한 구구단 메서드
```java
public class Main {
    public static void Gugudan(int level, int count) {
        if(count > 9) {
            return;
        }
        System.out.printf("%d x %d = %d\n", level, count, level*count);
        Gugudan(level, ++count); //++count 는 전위 증감연산자
    }
// \n 은 줄바꿈
    public static void main(String[] args) {
        Gugudan(9,1);
    }
}



```


## 연습문제 with pair

## 과제/ StringifyJSON

## 마치면서:회고