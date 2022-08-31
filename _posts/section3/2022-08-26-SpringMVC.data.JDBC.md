---
title: SpringMVC.data.JDBC
author: appstew
date: 2022-08-26 11:33:00 +0800
categories: [codestates, section3]
tags: [codestates]
math: true
mermaid: true
image:
  path: /commons/devices-mockup.png
  width: 800
  height: 500
  alt: Responsive rendering of Chirpy theme on multiple devices.
---

.data.JDBC(8/26~30 금 월 화 3일)

# 8/26 아침 줌 세션.

- 혹시 Java DataBase Connecter
- mysql, MariaDB, Oracle,MSSQL
- 자바에서는 대부분 인터페이스이다.
- JDBC는 데이터 액세스 인터페이스 스펙이고 저런 데이터베이스를 연결해주는 역할.

1. 개인 프로젝트 해보기
- 나프로 임신 테스트 기록 애플리케이션 앵귤러 스프링
- 로또 생성앱 안드로이드
- 샤핑 체커
- 결혼식 기념 앱
2. 방통대, 사이버대 등 컴공 관련 수업 듣기(경험자분 방통대랑 병행 불가, 하면 괴물)
3. 컴퓨터 관련 전공 대학원 다니기(야간대학원)
- 미니 검색엔진
- 쿼드콥터의 센서 대아타 이용한 비행상태분석
- secure Guard System for Family
- Beacon 기술을 이용한 지능형 모바일 물품관리 시스템
4. 꾸준한 블로깅
- 정식님 블로그 itvillage cafe.daum.net/ITVillages
5. 강의 제작(영상 또는 문서)
- 인프런에 이북도 참고
6. 오픈 소스 분석 및 기여

=============
- <질문 내용 시작>

- nodeJS 나 React 등으로 html, css, js 등으로 빌드해도 브라우저 렌더링 엔진 등은 별개인 것 같더라구요. 왠만한 건 다 브라우저에 뜨는데 가끔 어떤 건 브라우저에 애드온을 깔아야 렌더링되는 경우도 있더라구요..

1. end-user 브라우저 엔진 및 최종 렌더링 하는 부분도 프론트 엔드 영역인가요?
2. 브라우저 엔진 및 렌더링 부분은 무슨 키워드로 검색하면 추가 공부나 자료를 찾을 수 있을까요?
- https://appstew.github.io/posts/mermaid.working/
  - mermaid.js CDN 연결했는데 아이패드 사파리에서는 바로 렌더링되지만 크롬,파이어폭스 등에서는 애드온을 깔아야 렌더링 되는 것을 확인함
- https://stendhalgame.org/

- <질문 내용 끝>
  - 자바 기반 웹 게임으로 로그인만 하면 곧바로 브라우저에서 실행이 됨 

- 황정식 님께 디스코드 dm 으로 질문함.
  - 훌륭한 답변 주심

==============

# 8.26 오후 줌 세션

- ErrorResponse.java 리뷰
  - 목적:

- Stream.of(1,2,3)
- List.of(1,2,3,4)
- ErrorResponse of(BinddingResult bindingResult)

- SPI(Service Provider Interface)
  - JDBC 는 인터페이스
  - 예 : Class.forName("com.mysql.jdbc.Driver")

- List.of(1,2,3,4) 와 차이 List.asList(1,3,2)

- JUnit5 테스트
  - baeldung spring slice test

- in-Memory DB
  - 메모리 DB
  - 휘발성, 로컬 테스트 용도
  - 우리가 사용하는 in-Memory DB 는 H2

- H2, JDBC, 모두 예전에 실습했던 stendhalgames.org 에서 사용하던 것이었다!

- java/com/ 대신 java/resources/ 안에 yml 과 h2 데이터베이스 등이 있다.

- HTTP Connection Pool
  - 컨텐츠엔 없음
  - HttpClient
  - HttpComponentsClientHttpRequestFactory
  - server 가 Keep-Alive 지원 필요

- Java 데이터 액세스 기술 종류
  - sql 중심 기술
    - 순수 JDBC API 기술 이용
    - iBatis 또는 myBatis(둘다 옛날거, 특히 iBatis...SI..왠만하면 거르자)
    - Spring JDBC
  - ORM(Object-Relational Mapping) 중심 기술
    - Spring Data JDBC
    - JPA
    - Spring Data JPA

- 순수 JDBC API
  - 불편하다. 이해하면 Spring JDBC 가 얼마나 편한지 알 수 있다.
    - 가령 try catch 문을 클래스마다 일일이 써야한다든가.. 

- 구현메서드(가령 ...impl.java) 대신 Spring 에서 JDK 다이나믹 프록시, 리플렉션 API 등 이 알아서 해준다.

- 기존 return enw ResponseEntity(message, HttpStatus.OK);
  - return ResponseEntity.ok(mapper.messageTomessageResponseDto(message)); 와 동일하다

- public ResponseEntity postMessaes(
  @Valid 
)

- db.h2/schema.sql

- 람다와 Stream API
  - 선언형 프로그래밍 예시
    - int sum = .efef.efef().efef()
  - 람다 표현식
    - (String a, String b -> a.equals(b)) 
  - 함수형 인터페이스
    - Predicate<T>, BiFunction<T>

    - ojb::getOtal
    - str::
    - Consumer<String> consumer = System.out::println
    - 

- Stream
  - .of(1m\,2,3,4)
    .filter(n -> n%2!=0)
    .map(n -> n*2)
    .forEach

  - stream.forEach(Systeem.ouut::println); // 최종 연산을 호출해야 그때 비로소 작업한다.


- Collection 은 특정 자료구조로 데이터를 저장
  - 여러번 마색가능, for문 같은 걸로 외부 반복 데이터 추가 삭제 가능
  - eager
- Stream 은 데이터 가공 처리가 주 목적
  - 데이터 추가 삭제 불가 오로지 데이터 소스를 읽어서 소비하기만 한다.
  - operation 메서드 내부에서 보이지 않게 반복
  - lazy & short-curcuit
  - 한번만 탐색가능
  - stream.forEach(Systeem.ouut::println); // 최종 연산을 호출해야 그때 비로소 작업한다.
  - 언제 사용하는 것이 좋을까?
    - 대용량 데이터를 처리할때 가령 몇십만줄 txt js 라든가

- .Lines(Path.of)

## 8/26 아침 줌 세션

- 
- 줌에 한글 채팅안되는거 고쳐야 하는데 바빠서 아직도 못고쳐서 복봍하는중..ㅠ

하다보니 자꾸 html js 욕심이 생기고 몰라서 막히는게 많더라구요..ㅠ

백엔드에서 뭔가 했는데 화면에는 안나오는.

## 8/26 오후 줌 세션

- 오늘 프론트 두명 백엔드 두명 하차했다고 한다..다른 팀원들이 무슨 말하는지 모르겠다고. 첫 입문, 첫 취직은 힘들 것이다.
- build.gradle 
  - implementation 코멘트는 //
  - JPA 는 resources/db.h2/schema.sql 경로를 application.yml 경로 
  지정해줘야한다.
  - data.sql 에 INSERT NEW.. 로 목 데이터 입력 가능
  - 현업에서는 Spring Data JDBC 말고 JPA 쓸 것이다.
  - spring initializer 사이트
  - JPA 는 테이블 생성이 자동
  - at Message.java
  @Id 애너테이션
  private long messageId; ...
  - Bean 은 스프링 컴포넌트 안에 것들
  - at CrudeRepository.java
  Spring Data Jdbc가 기본적으로 Repository 인터페이스를 이미 상속받아서 NoRepositoryBeans으로 중복 빈을 못 만들게 한다네요
  - at MessageService.java
  에서 private messageRepository; 에 final 들어가면 
  - at MessageController.java
  public ResponseEntity postMessages(@Valid @RequestBody MessagePostDto messagePostDto) {
  Message message = 
  messageService.crateMessage(mapper.messageDtoToMessage(messagePostDtio));

  return ResponseEntity.ok(mapper.messageToMessage ..)
  }

- spring jdbc 가 어려운 이유. DDD(Domain Driven Design, 도메인 주도 설계)
  - 한마디로 모든 기능을 도메인 모델 위주로 돌아가는 설계 기법
  - 도메인이란?
    - 비즈니스적인 어떤 업무 영역
    - 우리가 실제로 현실 세계에서 접하는 각각의 업무 영역
  - 코드로 이해

- 빈약한 도메인 모델
  - MemberService(서비스 클래스) 서비스 클래스에 기능 집중@Service

  - Member(도메인 엔티티 클래스) - 기능이 없는 빈약한 도메인 모델

- 풍부한 도메인 모델

- 에그리거트(Aggregate)란?
  - 배달 주문 앱의 도메인 모델 예
    - 회원, 주문, 음식, 배달, 결제 기능 <- 도메인들
  - 애그리거트는 가령,
    - 회원 - 회원 정보, 회원포인트
    - 주문 - 배달 주문자 정보, 배달 음식 정보, 주문 정보, 배달 추적 정보, 배달 주소 정보
    - 음식 - 음식 정보
    - 결제 - 결제 정보
  - aggregate root 은 회원 정보, 주문 정보, 음식 정보, 결제 정보

- 기존의 avg, sum count() 를 aggregate function 이라고 하는데 이거랑은 다른 의미의 쓰임이다.

- 테이블과 테이블이 join 하기 위해서는 foreign key 필요, ORM 에서 핵심은 foreign key

- 가령 member_id(기본키)
email: varchar(100) not null
name: varchar(100) not null
phone: varchar(20) not nul

ORDER_COFFEE
order_id(외래키:주문): bigint not null
coffee_id(외래키:커피):bigint not null
quantity: int not null

COFFEE
coffee_id(기본키):bigint
kor_name: varchar(100) not null
eng_name: varchar(100) not null
price: int not nuall

- 도메인 엔티티 설계(DDD 적용전)
  - Member.java 에서 Order.java 로 불러오기
  - at private 
  
  AggregateReference<Member, Long> memberId;

- Set<CoffeeRef> orderCoffees = new LinkedHashSet<>();
  - 그냥 Set 은 키 중복을 방지하지만 순서는 저장하지 않는다,
  대신 위와 같이 하면 순서도 저장해준다. 다만 약간의 로직이 추가되므로 약간의 연산 지연이.



# 8/30 화요일 아침 줌 세션
- spring JDBC 뿐만 아니라 https://spring.io/projects/spring-data 에 들어가면 스프링이 제공하는 데이터 기술이 나열되어있다.
손가락
- 
- 오늘 실습과제 중, h2 중 db 기술과 페이지네이션 기능이 포함되어 있다!

- 서울에 IT 단지
  - 구로디지털,가산디지털,판교,강남,성숫동(쏘카)
  - 실리콘밸리는 물가가 너무 비싼 대신 연봉 10만달러 이상
  - 한국은 3500~2억,3억
  - 

# 8/30 화요일 오후 줌 세션(16:30~18:00)
- SpringMVC.data.JDBC 과제 페어와 함께 완성하고 제출함
- 지금 실시간 세션에는 아바타 실습(공지사항 구현하기) 는 be-reference-JDBC 에 필기겸 수정 작성했다. 현재 Notice 패키지 안에만 수정
- 아래 Order 에서 Member의 memberId 변수를 가져오는 방식을 자세히 보고 기억하자.
```java
package com.codestates.order.entity;

import ...
@Getter
@Setter
@Table("ORDERS")
public class Order {
    @Id
    private long orderId;

    // 테이블 외래키처럼 memberId를 추가해서 참조하도록 한다..
    private AggregateReference<Member, Long> memberId;
    // 
```
```java
public class Member {
    @Id
    private Long memberId;
```



## 
