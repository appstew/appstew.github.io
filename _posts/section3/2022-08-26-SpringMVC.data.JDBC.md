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

.data.JDBC

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

