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

- reactive streams 는 spec
    - 구현체: reactor, rx java, ..


## project Reactor
```
- 리액티브 프로그래밍을 위한 리액티브 라이브러리
- 리액티브 스트림즈의 구현체
- spring webflux 프레임워크의 핵심  중에 핵심
```

- import reactor.core.publisher.Flux;

- 마블 다이어그램

- 스케줄러(reactor 에서)
    - 쓰레드 관리자
    - reactor 는 기본적으로 non-blocking 통신을 위한 비동기프로그래밍을 위해 탄생했다.
    - java 의 멀티쓰레딩 은 굉장히 복잡하고 어려운데 reactor 의 scheduler 는 이걸 쉽게 도와주는 라이브러리

## spring WebFlux

## 221013 줌 세션

- springMVC 는 blocking I/O 방식
    - 즉 위에서부터 순차적으로 실행하고 위 명령어가 종료되어야 다음 명령어가 실행된다.
    - 이걸로도 왠만한 서비스는 커버가 되고 springMVC 는 어쨌든 확실히 현업이다(2022).
    - 하지만 네카라쿠배나 구글, 넷플릭스 는 webflux 를 사용하고 있고, webflux 도 할줄 아는 게 당연히 낫다.

- 

## webflux

- backpressure - lastest 전략
    - 최신 데이터 위주로 유지

- backpressure - buffer 전략
    - 가장 최근거부터 드랍하되, 

- backpressure - drop oldest 전략
    - 가장 오래된 데이터부터 드랍

## 해깔리는 거 다시 복습..

- 자바 스펙? 라이브러리? 프레임워크?
- 자바 list<string> string[] , 배열 차이
- 스택 큐?
- 자바 스트림 과 리액터의 스트림?
- 해시맵 해시셋 맵 차이. 중복을 방지해주는 것 말고 
- 리액티브 스택
- 서블릿 스택

- Netty 한국인이 만들었다고 한다! 세계적으로 많이 쓰이는데

- spring MVC 와 spring WebFlux 다이어그램 등 보기

- 선언형 명령형

- 람다표현식

- restTemplate 은 http 통신을 하기위한 rest application 이다.

- springMvcMainSampleApplication 을 실행하면 outboundcoffeecontroller 를 실행한다. 즉 포스트만 대신 쓸 수도 있고, 프론트엔드 앱 역할을 한다고 볼 수 있다!!



when i click on dictate here you'll see that a control
opens up at the bottom where i can start dictating 
and as i speak you'll see that
my text is showing up on the word document as i speak


2:37
i'm going to turn off dictation now so
2:39
basically what it does is it takes your
2:41
speech in real time and converts it into
2:43
text unfortunately you're not always
2:45
going to have word online with you let's
2:47
say you're conducting an interview