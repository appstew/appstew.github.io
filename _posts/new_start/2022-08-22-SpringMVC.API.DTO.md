---
title: SpringMVC.API.DTO
author: appstew
date: 2022-08-22 11:33:00 +0800
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

# this md file is a post template.

## 아침 줌 세션

- Codes황정식 강사님.
- 저번 Controller 어려웠나요? 1.5가 많네요.
- 심화학습에 rest client, RestTemplate
- 심화 학습 하셨을까요? 아닌 분들 1 1이 많네요

- Spring 에서 지원하는 Rest Client
  - RestTemplate
  - WebClient : deprecated

- DTO 란? Data Transfer Object
  - 역직렬화: JSON -> DTO  
  - 직렬화: DTO -> JSON

- CSR 과 SSR. Client and Server side.
  - 여러분들이 학습하는 것은 무엇일까요? CSR.
  - jekyll 같은 built site 깃헙 블로그 는 csr 일까 ssr일까? 잘 모르겠다..알아보자. 또는 가령 티스토리는?

- 그리고 이제 부트캠프가 제가 알기로 22주인데, 22주 안에 이렇게 많은 기능들을 다 배우는 것은 힘든 것이 사실입니다. 실제로 현업에서 쓰이는 많은 기술들 거의 다 있더라구요. 

- 그리고 여러분들 페어활동 너무 부담갖지 않으셨으면 좋겠어요.
  - 실제로 페어는 현업에 가서도 다른 프로그래머랑 옆에 같이 앉아서 하는데, 엄청 부담이고 힘들어요.
  - 자기보다 상대방이 잘해도 부담갖거나 하지 않았으면 좋겠어요.
  - 현업에 가면 그거 말고 코드 리뷰 라는 것도 있어요.

---------


## DTO (Data Transfer Object)

### HTTP 요청/응답에서의 DTO

- 저번 Controller 실습까지의 부분 중 멤버 삭제까지의 기능을 추가한 MemberController.class. DTO 적용 전 상태.
```java
@RestController
@RequestMapping("/v1/members")
public class MemberController {

    // 회원 정보 등록
    @PostMapping
    public ResponseEntity postMember(@RequestParam("email") String email,
                             @RequestParam("name") String name,
                             @RequestParam("phone") String phone) {
        Map<String, String> body = new HashMap<>();

        body.put("email", email);
        body.put("name", name);
        body.put("phone", phone);

        return new ResponseEntity<>(body, HttpStatus.CREATED);
    }

    // 회원 정보 수정
    @PatchMapping("/{member-id}")
    public ResponseEntity patchMember(@PathVariable("member-id") long memberId,
                                      @RequestParam String phone) {

        Map<String, Object> body = new HashMap<>();
        body.put("memberId", memberId);
        body.put("email", "hgd@gmail.com");
        body.put("name", "홍길동");
        body.put("phone", phone);

        return new ResponseEntity<Map>(body, HttpStatus.OK);

    }

    // 한명의 회원 정보 조회
    @GetMapping("/{member-id}")
    public ResponseEntity getMember(@PathVariable("member-id") long memberId) {
        System.out.println("# memberId: " + memberId);

        // not implementation
        return new ResponseEntity<Map>(HttpStatus.OK);
    }

    // 모든 회원 정보 조회
    @GetMapping
    public ResponseEntity getMembers() {
        System.out.println("# get Members");

        // not implementation
        return new ResponseEntity<Map>(HttpStatus.OK);
    }

    // 회원 정보 삭제
    @DeleteMapping("/{member-id}")
    public ResponseEntity deleteMember(@PathVariable("member-id") long memberId) {

        return new ResponseEntity(HttpStatus.NO_CONTENT);
    }

}
```

- IntelliJ Generate Code 기능 사용법 링크: https://www.jetbrains.com/idea/guide/tips/generate-getters-and-setters/

- 현업에서는 아예 lombok 이라는 라이브러리를 이용해 getter/setter 메서드를 자동으로 만들어 사용하는데 이 부분은 추후에 학습


- MemberController 에 DTO 클래스 적용

```java
@RestController
@RequestMapping("/v1/members")
public class MemberController {

    // 회원 정보 등록
    @PostMapping
    public ResponseEntity postMember(@RequestBody MemberPostDto memberPostDto) {

        return new ResponseEntity<>(memberPostDto, HttpStatus.CREATED);
    }

    // 회원 정보 수정
    @PatchMapping("/{member-id}")
    public ResponseEntity patchMember(@PathVariable("member-id") long memberId,
                                      @RequestBody MemberPatchDto memberPatchDto) {
        return new ResponseEntity<>(memberPatchDto, HttpStatus.OK);

    }

    // 한명의 회원 정보 조회
    @GetMapping("/{member-id}")
    public ResponseEntity getMember(@PathVariable("member-id") long memberId) {
        System.out.println("# memberId: " + memberId);
        // not implementation
        return new ResponseEntity<>(HttpStatus.OK);
    }

    // 모든 회원 정보 조회
    @GetMapping
    public ResponseEntity getMembers() {
        System.out.println("# get Members");
        // not implementation
        return new ResponseEntity<>(HttpStatus.OK);
    }

    // 회원 정보 삭제
    @DeleteMapping("/{member-id}")
    public ResponseEntity deleteMember(@PathVariable("member-id") long memberId) {
        return new ResponseEntity(HttpStatus.NO_CONTENT);
    }

}
```

- 다음으로 postman 에서 raw, JSON 방식으로 요청
```JSON
{
    "email": "hgd@gmail.com",
    "name" : "홍길동",
    "phone": "010-1111-3333"
}
```

- 유효성 검증 라이브러리 추가
```
//build.gradle
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-validation'
	...
	...
}
```

` 유효성 검증 애너테이션 추가 on MemberPostDto.class

```java
    @NotBlank
    @Email
    @NotBlank(message = "이름은 공백이 아니어야 합니다.")
    @Pattern(regexp = "^010-\\d{3,4}-\\d{4}$",
            message = "휴대폰 번호는 010으로 시작하는 11자리 숫자와 '-'로 구성되어야 합니다.")
```

- 지금까지 사용한 유효성 검증 애너테이션들(@Min(1), @Vaild) 은 Kakarta Bean Validation 이라는 유효성 검증을 위한 표준 스펙에서 지원하는 내장 애너테이션들.

- 내가 놓친 것.

```
@PathVariable이 추가된 변수에 유효성 검증이 정상적으로 수행되려면 (1)과 같이 클래스 레벨에  @Validated 애너테이션을 반드시 붙여주어야 한다는 사실을 기억하기 바랍니다.
```

- 드디어 실습 단계로!

- DTO 구현 실습 과제.

  - [실습 과제 제출 안내](https://urclass.codestates.com/0b67fbff-abed-4fb3-860a-80f73b47cc47?playlist=1978)
  - 제출 기한: 2022.08.29.24:00 까지.

## 오후 줌 세션. 16:30~18:00

- 인텔리제이에서 브레이크포인트 걸고 디버깅.
  - 

- 렌더링.
  - HTML, Javascrip, CSS
  - HTML 이 렌더링 대상.
  - SSR 은 동기적인 통신 및 렌더링. 
    - 예: 공공데잍터포털. 버튼 클릭하거나 하면 파비콘 옆 뱅글뱅글 돌면서 화면이 리프레시됨
  - CSR
    - 프론트엔드에는 css, javascript, html 이 웹서버(Apach, Nginx)에, 웹 애플리케이션(API계층, 서비스 계층, 데이터 액세스 계층)이 Tomcat, Jetty 등 서버에 실리고, 프론트엔드에서 백엔드로 데이터요청하고, 백엔드에서 응답데이터 제공한다.
    - 프론트엔드와 백엔드 분리되어있음

- 프론트엔드와 협업시 CoffeeController 실행 예시
  - resoures 폴더에 coffee.html 등.

- 웹 에이전시 등에서는 SSR 방식을 제공하기도 하지만, 현업에서는 CSR 방식이 많고, 코테에서도 CSR 방식으로 한다.

- CSR 방식 예시
  - resoures 안에 html 파일 따로 없다. 프론트엔드 쪽 프로젝트 폴더에 있을 것이다.
  - 똑같이 Thread.sleep(5000L) 5초 지연 시간 주고
  - ajax 통신.
  - html 등 jetbrans 앱. WS? 인텔리제이는 IJ
  - 

- 프론트엔드 에서도 MVC 같은 걸 사용할까?
  - Angular 프레임워크 같은 경우 Spring 처럼 계층별로 나눠서 구현한다. React 도 가능하긴 하지만, 좀 더 자유롭다.

- 프론트엔드 서버가 따로 없으면, SSR 
  - SSR 은 백엔드에서 웹브라우저로 바로 HTML,javascrip,css 등 제공함
  - 프론트서버랑 백엔드 서버가 데이터 통신이 있으면 CSR

- 아파치 vs 아파치 톰캣
  - 아파치 에는 HTML, CSS, Javascript 같은 정적인 데이터가,
  - 아파치 톰캣은 
    - 톰캣 = 서블릿 컨테이너
  
- 

```java
@DeleteMapping

if(coffees.containsKey(coffeeId))
coffees.remove coffeeId;

else return new ResponseENtiry(HttpStatus.OK);
...
```
- DTO 실습과제 일부

```java
@Range(min= 100, max= 50000)
@NotBlank
@Pattern(regexp = "~~", 
message = "커피명은 어쩌고~")
private String engName;
// Cafe Latte, Cafe    Latte, Cafe Latte     , 
...
```

- 그리고 NotSpaceValidator 안에 구현된거.
  - Null 은 포스트맨에서 가령 아예 키부터 주지 낳았을 경우.

```java
private Optional<@Range(min=100, max=5000) Integer> price = Optional.empty();
```

/members/1

service.update(dto)

service.update(dto, memberId)


- obsidian
  - 플러그인, 테마 등
  - 처음 러닝커브만 지나면 노션보다 훨씬 낫고 좋다고?
  - 컴퓨터에서도 한번 써봐야겠다. 
  - [markdown monster](https://markdownmonster.west-wind.com/docs/_5ef0x96or.htm) 발견.
  

- 깃헙 블로그는 csr? ssr? 
  - 이게 생각보다 어렵다. 구글에서 ssr csr 차이 예시 구분 방법 등 한글로 검색해보아도, 나오든 거의 모든 글들이 똑같은 내용만 담고 있다..
  네이버 블로그는 2020년부터 ssr 로 전환했다는 것만 어디서 확인했을 뿐, ssr, csr 이론적인 설명 차이 등만 있고 구체적으로 무슨 사이트가 정확히 csr 이다 ssr 이다 하는 설명은 찾을 수 없었다.
  - 또한 정적 웹사이트는 csr, 동적 웹사이트는 ssr 이라고 하지만 여전히 해깔린다..
  - 한가지 확실한 것은 가령 stendhal 같은 자바 웹 게임은 분명 csr 일 것이다.
  - 아무튼 혹시 몰라 영어로 검색해보았다. [이 글](https://stackoverflow.com/questions/62329411/how-to-see-whether-a-website-is-client-side-rendered-or-server-side-rendered) 에서 말하길, 
  - "현실적으로, ssr 과 csr 사이에 뚜렷한 구분법은 없다. 대부분 csr 이라 부를 웹사이트도 여전히 서버로 html 을 전송할 것이다. 때로는 엄청 많은 양을. 그리고 대부분 ssr 이라 부를 웹사이트도 여전히 유저입력에 따라 약간의 html 수정이 발생한다."
  - "브라우저에서 view source 와 관리자도구의 element inspector 안의 내용이 완전히 동일하면, 이는 100% SSR.  
  약간의 차이가 있으면 약간 csr 적이고, 차이가 크다면 ssr 보다는 csr 에 가깝다고 볼 수 있다."
  - ctrl+U 로 소스에서 코드 양이 적으면 csr, 이미 (거의) 모든 컨텐츠를 갖고 있다면 이는 ssr.
  - 실제로 stendhal game 은 소스의 양이 291페이지밖에 안되고 csr임을 다시 확인할 수 있다.
  - 가령 built 데이터로 구동하는 깃헙 블로그와 velog의 경우, 페이지마다 소스 코드가 바뀌고, 그 페이지에서 필요한 모든 코드를 각 소스에 가지고 있는 것을 보아 ssr 인듯. 그럼 벨로그나 깃헙 블로그가 동적 블로그라고?
  - stendhal game 은 역시 장소를 이동해도, 소스코드가 계속 동일하고 짧다. 그래서 csr임이 다시 확인되지만, 정적 웹사이트라고?

- 아무튼 CSR 과 SSR 을 어느정도 구분은 할 수 있을 것 같다.
  - 나중에 정적 웹사이트 vs 동적 웹사이트 에 대해 좀 더 알아보자.
  - 그런데, 가령 github pages 가 SSR, 즉 server-side-rendering 인데, 조금 전에 파이어폭스에서 mermaid renderer 애드온을 깔은 후에야 비로소 mermaid charts 가 렌더링 되는 것은 왜일까? 어떻게 이해해야 할까?











  