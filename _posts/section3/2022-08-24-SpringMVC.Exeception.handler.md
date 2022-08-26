---
title: SpringMVC.Exception.handler
author: appstew
date: 2022-08-24 11:33:00 +0800
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

- section3/Execption.handler/be-reference-template-exception-handle/
- section3/Execption.handler/be-homework-exception-handle/


# 8/25 아침 줌 세션.
- 오늘은 실시간 세션이 16시 1시간인데, 오늘 힘들더라도 
stream API 리뷰는 나중에라도 꼭 해드리고 싶어요.
- 오늘 17시에 선배적 참견 시점에 취업하신 분이 얘기하는 게 있는데, 약간 걸러들을 것은 있습니다. 왜냐면 여러분은 자바이지만 그분은 Node.js 이고 그분은 자바스크립트로 프론트 백엔드 둘다 하는 것이라서 좀 다를 것입니다.
- nodeJS 는 싱글 스레이드고, 비동기 입니다. Thred per request, Non blocking 동기,

    실습 코드 작성이 완료 되었으면 아래의 실습 과제 제출 안내에 따라 실습 과제를 제출해주세요.
        실습 과제 제출 안내

    제출 기한
        2022.09.01 24:00 까지

## 페어 프로그래밍
- section3/Execption.handler/be-homework-exception-handle/ 에 주어진 기능 3개를 페어와 같이 구현하였다.
```java
//GlobalExceptionAdvice.java
// 페어와 함께 작성한 코드
        // TODO GlobalExceptionAdvice 기능 추가 1
//        return new ResponseEntity<>(response, HttpStatus.valueOf(e.getExceptionCode().getStatus()));
        return new ResponseEntity<>(response, HttpStatus.valueOf(response.getStatus()));

//        return new ResponseEntity<>(HttpStatus.valueOf(e.getExceptionCode()
//                .getStatus()));
    }
    
    // TODO GlobalExceptionAdvice 기능 추가 2

    @ExceptionHandler
    public ResponseEntity handleHttpRequestMethodNotSupportedException(HttpRequestMethodNotSupportedException e) {
        ErrorResponse response = new ErrorResponse(405, "Method Not Allowed");

//        final ErrorResponse response =ErrorResponse.of(HttpStatus.METHOD_NOT_ALLOWED);식
// 황정식님 방

        return new ResponseEntity<>(response, HttpStatus.METHOD_NOT_ALLOWED);
    }
    // TODO GlobalExceptionAdvice 기능 추가 3
    @ExceptionHandler
    public ResponseEntity handleException(Exception e) {
        ErrorResponse response = new ErrorResponse(500, "Internal Server Error");

        return new ResponseEntity<>(response, HttpStatus.INTERNAL_SERVER_ERROR);
        
    }
```

```java
//줌 세션 황정식 님이 가르쳐주신 코드
//ErrorResponse.java 안에
    private int status;
    private String message;
까지는 같았으나,
    public ErrorResponse(int status, String message) {
        this.status = status;
        this.message = message;
    }
    // 이걸 public 이 아닌 아래처럼 private 으로 하고
    //    public static ErrorResponse of() {
//        return new ErrorResponse()
//    }
    public static ErrorResponse of(ExceptionCode exceptionCode) {
    return new ErrorResponse(exceptionCode.getStatus(), exceptionCode.getMessage());
    }
    public static ErrorResponse of(HttpStatus httpStatus) {
        return new ErrorResponse(httpStatus.value(), httpStatus.getReasonPhrase());
    }
    // 황정식 님이 줌세션에 가르쳐준 방식
```
- 이걸 가지고 GlobalEceptionAdvice.java 에 구현해보기


## 8/25 16:00 줌 세션

오늘 과제는 바로 제출했는데, 페어분이 너무 잘하셔서 Exception.java 등 알려주고 쉽게 3가지 기능구현을 해서 곧바로 제출했는데,
황정식님이 오후 줌 세션에 약간의 다른 코드를 알려주셨다.

## 8/25 17:00 선배적 참견 시점

- 22기 백엔드 수료생 전인섭 님
- 수료 후 한달만에 취업 후 더 좋은 회사로 4개월 후에 취업
- linkedin 으로 제안 받아 싱가폴 소재 회사에 근무 후 비자 문제로 퇴사 후 학업과 병행할 수 있는 프리랜서 개발자로 근무중 : 남양주에서 싱가폴 회사랑 재택근무도 함
- 내가 생각하는 개발 세계란?
  - "공유를 통해 다음엔 좀 더 공학적인 시도를 하는 곳"
  - 

- 자료링크는 매니저님을 통해 추가 공유(디스코드)
- miro flowchart, boards, figzam
- request latency over time

 
- 뭐든지 하면 다 좋고, 그렇지만, 시간과 한계가 있으니, 단계별로 나눠서 하나씩.
  - bare minimum, advanced, nightmare
  - bare minimum: 블로깅
  - advanced : 영어로 검색하고 보기
  - nightmare : 매일 알고리즘 풀기
    - 제 때는 매일 알고리즘 하루에 하나 푸는 사람들이 손에 꼽을 정도였는데, 여러분은 대단하시네요.(데일리 코딩 덕분)
- 영어로 프로필 이력서 만들고, 
한국쪽은 리멤버코리아, 외국쪽은 링크드인 통해서 연락 받을 수 있도록 함
- 신입이 경력 없이 외국취업은 힘들지 않을까..미국이랑 유럽 싱가폴 정도 도전해봤는데, 신입(주니어)은 진짜 개미지옥..
한국에서 경력을 쌓고, 그걸로 하는 것도 나쁘지 않음
- 설문 링크
- FE : [https://urclass.codestates.com/e3dd3357-1e01-40c1-8daf-57e7acae0307?playlist=1813](https://urclass.codestates.com/e3dd3357-1e01-40c1-8daf-57e7acae0307?playlist=1813)
- BE : [https://urclass.codestates.com/b064a3ac-ede7-43de-b6f0-b97aa186bfc0?playlist=1783](https://urclass.codestates.com/b064a3ac-ede7-43de-b6f0-b97aa186bfc0?playlist=1783) 

- 스프링안쓰고 nodejs 랑 java 만드로 브라우저에 뛰우는 코드

- 수강생 시절 피하면 좋은 것들
  - 무리하지 않기
