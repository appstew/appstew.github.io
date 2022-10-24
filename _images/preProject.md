---
---

preProject
(연습프로젝트)
221021 드디어 팀프로젝트!!


|ㄱ|ㄱ|ㄱ|
|---|---|---|
| FE BE 공통 줌 세션 | https://us02web.zoom.us/j/87378179244?pwd=L2llaFlOOG9NbFl0NjNWMUpsem4rdz09 | 018_BE_조지선|
| zep링크2 | https://zep.us/play/ykAY6A| https://zep.us/play/2YvXMJ |
|preProject|team18|NotFound|
|상시 커뮤니케이션 채널|||
|화상 커뮤니케이션 채널|||
|상시채널(디스코드)|https://discord.gg/ztGEnMjC||
|노션 팀별 공간|https://www.notion.so/82a7bd5989fb4aadbfc741791387db12?v=a8acec2cab0d4357a2571bec33c597f9&p=a014c9a400234e80b91085371221c834&pm=s|https://codestates.notion.site/Pre-Project-3d380dd015e54a7b8ce2a30d03a9af27|
||||
|코드스테이츠 수강생 프로젝트들|https://github.com/orgs/codestates-seb/projects||
|pre 깃헙 리포|https://github.com/codestates-seb/seb40_pre_018| 로컬 주소: /javatest/hrd/idea/preProject |
|깃헙 프로젝트 관련 숙지사항|https://urclass.codestates.com/content/883e9063-89ee-4e08-ad15-890e20f0debe?playlist=2722||
||||

https://github.com/Qone2

https://intrepidgeeks.com/#%EA%B2%8C%EC%9E%84%20%EA%B0%9C%EB%B0%9C
https://www.appgamekit.com/education

https://www.google.com/search?client=firefox-b-d&q=%ED%8C%8C%EC%9D%B4%EC%96%B4%ED%8F%AD%EC%8A%A4+%EC%A7%9C%EC%A6%9D
https://eclipse4j.tistory.com/94
너무 공감된다..파폭이 캐시된 페이지를 보여주는데 그럴 때도 있고 아닐 때도 있어서 ..
https://intrepidgeeks.com/tutorial/annoying-cache-for-firefox-3
http://kb.mozillazine.org/Browser.cache.check_doc_frequency
해결 방안은 간단하다.about:config에서 4Browser.cache.check_doc_frequency의 값이 1로 수정됨
이 키 값의 의미는 다음과 같습니다.0 （ ）
1 everytime( ， )
2 never( )
3 when out of date (default)( ， )
https://github.com/Dev-illage/Devillage

- Pre-Project
  - 프로젝트와 기술에 대한 이해, 연습 개념
  - 팀 커뮤니케이션 이해 및 연습
  - 기간: 10월 20일(목) ~ 11월 7일(월) 13일
  - 
- Main Project
  - 기간: 11월 8일(화) ~ 12월 7일(수) 22일
  - 프로젝트 기획 및 협업
  - 기술 적용
  - 이슈 파악 및 문제 해결
  - 포트폴리오로서의 기능



## 상시 커뮤니케이션 
- zep, slack, 디스코드, 오픈채팅
- 하루 최소 4시간 유지(상시 답변)
 - 1~5시

## 화상 커뮤니케이션
- 비슷

## 공용 줌
- 존과 맵
- 전체공간맵, 스터디홀, 

## 안내사항

- main project 부터는 집체교육으로 스마트폰에서 hrd QR 로그인을 해야한다.
- 9~6 시 30분이내에 응답하여야 한다.
- zep, 디스코드, 슬랙, 카톡 오픈채팅방
- zep 에서 화상은 on, 마이크는 필요할때만 on
- 


https://zep.us/play/2YvXMJ

https://codestates.notion.site/SEB-40th-Project-642bce529c294c8f92770ed51bd1e8f7

## preProject 개발환경 구축 사항

1. 최소 요구 사항
- localhost 상에서 프론트엔드 static files 와 백엔드 스프링부트 서버 를 연결하여 localhost 상에서 확인.

- 필요시 ngrok 을 활용하여 fe 개발자가 be 개발자 서버에 접근하도록 할 수도 있음

2. aws 배포 환경 구축 
  - aws 그룹 계정 생성
  - 2-1. EC2 에 클라이언트 서버 모두 배포
  - 2-2. s3에 클라이언트 정적 파일, EC2에 서버 배포


- 

## kanban, 그리고 github issue, milestone

- 깃헙 리포지토리 setting > features > issues > set up templates
- 이슈, 마일스톤, 생성해보기

- git add 는 스테이징 이고, git reset 으로 취소 
- git diff 는 스테이징되지 않은 변경사항을 보여줌
- 이후는 git commit 등 진행
- 내가 쓰던 git branch -M branch-name 은 git checkout -b branch-name 과 동일한듯 하다. 아직 확실하진 않음

```
비교 및 검사

로그 및 변경 사항을 검사할 수 있습니다.

# 브랜치B에 없는 브랜치A의 모든 커밋 히스토리를 보여줍니다.
$ git log branchB..branchA

# 해당 파일의 변경 사항이 담긴 모든 커밋을 표시합니다. (파일 이름 변경도 표시)
$ git log --follow [file]

# 브랜치A에 있지만 브랜치B에 없는 것의 변경 내용(diff)을 표시합니다. (branch간 상태 비교)
$ git diff branchB...branchA
```

## git flow, github flow, gitlab flow, Coz' Git flow
- preProject 에서는 cos' git flow

![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/vEAcD2ryoNSo-6dGo_MIW-1660886461321.jpeg)

# Unit3 - project 관리하기

### 221024 아침 줌 세션

- README.md
- 각종 개발에 필요한 메타정보
  - package.json / build.gradle, setting.gradle
  - .gitignore
  - .env
  - LICENSE
- .gitignore 에 secretKey, .idea/ 등   
- toast UI

- 칸반
  - goJS 에서 처음 접해본 것!
  - 일본어 칸반(간판) 에서 유래했다. 
  - 

- 기존의 git checkout -M 같은 용도로 최근에 git switch -c(create) 로 나옴



github.com/codestates-seb/seb39_main_056

