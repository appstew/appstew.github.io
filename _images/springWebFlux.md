---
---

[]

|챕터 이름|||
|---|---|---|
|[spring WebFlux|리액티브 프로그래밍||
|[spring WebFlux|project Reactor|||
|[spring WebFlux|spring WebFlux|||
||||
||||
||||

## 리뷰

CSR 은 json 데이터만 프론트에 보내고, SSR 은 다 만들어진 html 을 보낸다.


## [spring WebFlux|리액티브 프로그래밍

- 명령형 프로그래밍
```java
public class ImperativeProgrammingExample {
    public static void main(String[] args){
        // List에 있는 숫자들 중에서 4보다 큰 짝수의 합계 구하기
        List<Integer> numbers = List.of(1, 3, 6, 7, 8, 11);
        int sum = 0;

        for(int number : numbers){
            if(number > 4 && (number % 2 == 0)){
                sum += number;
            }
        }

        System.out.println(sum);
    }
}
```
- 명령형 프로그래밍은 코드가 위에서 아래로 순차적으로 실행된다.


- 선언형 프로그래밍 예시
    - java8~ stream API
```java
public class DeclarativeProgramingExample {
    public static void main(String[] args){
        // List에 있는 숫자들 중에서 4보다 큰 짝수의 합계 구하기
        List<Integer> numbers = List.of(1, 3, 6, 7, 8, 11);

        int sum =
                numbers.stream()
                        .filter(number -> number > 4 && (number % 2 == 0))
                        .mapToInt(number -> number)
                        .sum();

        System.out.println("# 선언형 프로그래밍: " + sum);
    }
}
```
- 선언형 프로그래밍 중 stream 의 경우 메서드가 호출될 때 체인이 실행된다.

## project Reactor

- import reactor.core.publisher.Flux;

- 마블 다이어그램

- 스케줄러(reactor 에서)
    - 쓰레드 관리자
    - reactor 는 기본적으로 non-blocking 통신을 위한 비동기프로그래밍을 위해 탄생했다.
    - java 의 멀티쓰레딩 은 굉장히 복잡하고 어려운데 reactor 의 scheduler 는 이걸 쉽게 도와주는 라이브러리

