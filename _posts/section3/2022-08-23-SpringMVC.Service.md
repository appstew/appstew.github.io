---
title: SpringMVC.Service
author: appstew
date: 2022-08-23 11:33:00 +0800
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

- section3/be-template-service-layer 에서 MemberController 

## Prompts

> An example showing the `tip` type prompt.
{: .prompt-tip }

> An example showing the `info` type prompt.
{: .prompt-info }

> An example showing the `warning` type prompt.
{: .prompt-warning }

> An example showing the `danger` type prompt.
{: .prompt-danger }



## title [Spring MVC] API 계층

```mermaid
classDiagram
    Spring MVC <|-- API
    Spring MVC <|-- service
    Spring MVC <|-- Data
    %% Spring MVC : +int age
    %% Spring MVC : +String gender
    %% Spring MVC: +isMammal()
    %% Spring MVC: +mate()
    class API{
      1. Controller
      2. DTO
      -controller과제(~8.26)
      -DTO과제(~8.29)
    }
    class service{
      equals.business
      1.서비스(비즈니스)계층
      2.
      -서비스(비즈니스) 과제(~8.30)
    }
    class Data{
      1.
      2.
    }
click API href "https://google.com"
click c href ".#spring-아키텍처"
click D href "./#controller"
click e href "./"
```

### 아침 줌 세션

- 정규표현식 중,
  - 

- MapStruct 라이브러리 이용(예전엔 ModelMapper)

- @RequestBody 
  - @ResponseBody 는 ResponseEntity 를 쓰면 생략할 수 있다.

## 개요 및 학습 사전 준비



## 서비스 계층에서의 DI

### 개요

### 기본. DI 를 통한 서비스 계층 <-> API 계층 연동

- section3/be-template-service-layer 에서 MemberController v2까지 실습 후

```
- @Getter, @Setter , @NoArgsConstructor , @AllArgsConstructor
  - lombok 라이브러리 에서 제공하는 애너테이션들

그런데 코드 3-45는 Spring에서 지원하는 DI 기능을 사용하지 않았기때문에 MemberController와 MemberService가 강하게 결합(Tight Coupling)되어 있는 상태입니다.

Spring의 DI를 사용하면 클래스 간의 결합을 느슨한 결합(Loose Coupling)으로 손쉽게 만들 수 있습니다.

그럼 Spring의 DI를 사용하도록 MemberController를 바꿔볼까요?

클래스 간에 DI가 필요한 이유는 [Spring Framework 기본] 유닛의 [IoC(Inversioin of Control)/DI(Dependency Injection)](https://urclass.codestates.com/15d05644-7d74-4209-a04a-3f514db49649?playlist=2029) 챕터를 참고하세요
```

- v3. DI를 통한 느슨한 결합
  - public MemberController(MemberService memberService) 로 바꿔준 후, MemberService.class 위에 @Service 추가
  - MemberController 위에 @RestController 이 있으므로 Spring Bean.
  - 생성자가 하나이므로 @Autowired 붙이지 않아도 되지만 두개 이상일 경우 @Autowired 붙여야 한다.


### 기본. 매퍼(Mapper) 를 이용한 DTO 클래스 <-> 엔터티(Entity) 클래스 매핑

- MemberController v3 의 문제점
    - MemberController의 핸들러 메서드가 DTO 클래스를 엔티티(Entity) 클래스로 변환하는 작업까지 도맡아서 하고 있다.
    엔티티(Entity) 클래스의 객체를 클라이언트의 응답으로 전송함으로써 계층 간의 역할 분리가 이루어지지 않았다.
    - 결국 DTO 클래스와 엔티티(Entity) 클래스를 서로 변환해주는 누군가 즉, 매퍼(Mapper)가 필요한 상황입니다.

  
-  MemberController v4
   - MemberMapper, MemberResponseDto 클래스를 만들고, MemberController 에 수정사항을 반영하였다. 수정된 코드 설명은 클래스 안에 첨부함.

- MemberMapper 인터페이스 생성후
- MapStruct 의존 라이브러리 설정
```java
dependencies {
	...
	...
	implementation 'org.mapstruct:mapstruct:1.4.2.Final'
	annotationProcessor 'org.mapstruct:mapstruct-processor:1.4.2.Final'
}
```

- 이후 gradle build 하면 build/generated/sources 안에 MemberMapper 인터페이스를 구현하는 MemberMapperImpl 클래스가 자동 생성된다.
  - 이후 MemberController 안에 import com.codestates.member.mapstruct.mapper.MemberMapper; 만 추가하고 주소만 v5로 변경하면 수동으로 만든 MemberMapper 대신 MemberMapper 인터페이스를 자동으로 사용한다.


### 실습. 서비스 계층과 API 계층의 연동 실습

과제 be-homework-mapper
  - 2022.08.30 24:00까지
  - 220830 제출완료

## 오후 줌 세션

- DispatcherServlet.class, FrameworkServlet.class, HttpServlet.class

- HttpMessageConverter
  - Request Body 를 java 객체로 변환해준다.
  - Java 객체를 Response Body 로 변환해준다.
  - DTO 에 setter 메서드가 필요없음

- Java Bean Spec, RMI(Remote Method In), objectMapper, CRUD,

- 서비스 클래스를 Spring Bean 에 등록하는 방법
  - @Service
  - @Component

- 생성자 기반 DI
```java
    private final MemberService memberService;
    private final MemberMapper mapper;
    //

    public MemberController(MemberService memberService, MemberMapper mapper) {
        this.memberService = memberService;
        this.mapper = mapper;
    }
// 만약 MemberController() 괄호 안에 파라미터를 여러개 쓰는 경우도 있고, 아닐 경우 밑에 public 으로 또 만들 수 있다. 이때는 아마 @Autowired 붙여야?

```
- setter 기반 DI
  - setter 를 통해 DI 되는 객체를 바꿔야 될 경우
    - 흔하지 않음

- DTO 클래스와 Entity 클래스 분리 이유
  - REST API 스펙의 독립성 확보 
    - a
    - 패스워드 같은 민감한 데이터 분리
  - 계층별 관심사 분리
  - 코드 구성의 단순화

- Mapper 종류
  - MapStruct, JMapper, ModelMapper
  - www.baeldung.com
- MapStruct vs ModelMapper
  - ModelMapper: 런타임에 실행
  - MapStruct: 컴파일 타임에 매핑 구현체 모두 생성

- MemberResponseDto 안에 @NoArgs @AllArgs rombok 
  - @NoArgs : 파라밑터 없는거 알아서 만들어줌
  - @AllArgs 아래거 생략가능
    ```java
    public MemberResponseDto(long parameter, ...) {
      this.efef = efef;
      this.efef = ef;
    
    }
    ```
- MapStruct 가 매핑을  
  -     

- CofferService.java 안에 있는 데이터. stub, 또는 목업데이터

- Stream API 리뷰

```
//질문: @Email 유효성 검증에서 ‘@‘는 빠지면 안 되는데 ‘.’는 빠져도 되더라구요. 어디를 뜯어보면 확인할 수 있나요? 
//답변: 
```

```
//질문: 궁금한 게 있습니다. Mapper 라이브러리가 설명만 봤을 때는 엄청나게 편해보였는데, 막상 사용해보니 Entity와 DTO의 멤버가 다른 경우(예를 들어 유저에게 아이디 패스워드 네임 이메일이 있는데 UserDto에서는 네임과 이메일만 가져올 경우) 일일히 옵션으로 매핑 처리를 해줘야하고 그에 맞는 DTO도 별도로 만들어줘야해서 수작업으로 Entity To Dto 클래스를 만들어서 매핑해주는 것에 비해 큰 이점이 있는지 잘 모르겠다는 생각이 들었는데, 실무에서는 거의 매퍼를 사용하나요? 
//답변:
```

### 수업 종료 후 추가공부

- .java .class 차이점
  - .java 는 프로그램 작성시, .class 는 빌드된 파일로서, JVM 에서 프로그램 구동 시 사용된다.
  - .class 파일은 .java 코드를 보안 이유로 바이트 코드 바꾼 것이고 또한 이걸 실행하는 것이 속도가 더 빠르다.
![](../../img/fedora_hrd/java_class_difference.png)

- github pages 는 SSR 이고 mermaid.min.js 까지 제공하는데 왜 크롬과 파폭 등 브라우저 단에서는 렌더링 애드온이 필요한 걸까?
  - [kiroki.io](https://kroki.io/)
    - [cheat sheet](../../img/fedora_hrd/kroki.io_printPDF.pdf)
      - Excalidraw[]
      - Graphviz
      - [PlantUML](https://plantuml.com/starting)
  - https://gojs.net/latest/intro/ 여기서 나중에좀 천천히 읽고 실습해보자.
  - about:debugging#/runtime/this-firefox 에서 Markdown Diagrams 소스코드, 디버깅툴 보기
  - 그리고 schema, 자료구조 시각화 자료 등, 시간 날때 알아보자.
  - markdownMonster
  - Obsidian
  - [intelliJ Diagram exmaple](../../img/fedora_hrd/beandiagram.svg)
    - <details>![](../../img/fedora_hrd/beandiagram.svg)
    </details>

==================
