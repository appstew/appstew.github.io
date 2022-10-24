---
---

221017 드디어 솔로프로젝트 2주!!

## 개념학습

- 서버의 종류

|name|via||
|---|---|---|
|웹서버|Apache, IIS, NginX||
|웹앱 서버|Tomcat, WebLogic, WebSphere||
|데이터베이스 서버|Oracle, MS-SQL, MySQL||
|파일 전송 서버|VS-FTPD. IIS||
|메일  서버|send-mail, Microsoft Exchange Server||
|인쇄 서버|||
||||
||||
||||


- CORS, CSRF

## To-do App 개발

### jdbc 파트
- be-template-template 과 be-reference-template 복습 겸 참고.

```
// build.gradle
	implementation 'org.springframework.boot:spring-boot-starter-data-jdbc'
	runtimeOnly 'com.h2database:h2'

// aplication.yml
spring:
  h2:
    console:
      enabled: true
      path: /h2     # (1) Context path


## 221020 팀 프로젝트 시작!

- main project
  - 산업군 : 금융, 제조 ,에너지/친환경, 유통/물류, 미디어, 의료/헬스케어, 건설, 교육, 기타(관심 산업군 없음)


  