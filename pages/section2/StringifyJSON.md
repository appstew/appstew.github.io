---
layout: StringifyJSON 페어 과제
title: 111
description: >
hide_description: false
toc: true
toc_sticky
---
## 개요


이번 과제에서는 서로 다른 프로그램 사이에서 데이터를 주고받기 위해 사용되는 데이터 타입인 JSON에 대해 학습하고, 실습을 통해 앞서 배운 자바에서 사용하는 데이터 타입을 재귀를 사용하여 직접 JSON타입으로 변경하는 코드를 작성하게 됩니다.

    과제를 시작하기 전에 이전에 학습했던 재귀함수의 동작원리를 복습하세요.
    Java에서 사용하는 다양한 데이터 타입에 대한 이해가 필요합니다.

> 그래서 JSON 이 뭔데?

```java
    String - ""로 묶여야 함
    Number
    Object - {로 시작하고 }로 끝내어 표현함, name뒤에 :를 붙이고 ,로 구분
    Array - [로 시작하고 ]로 끝냄, ,로 값을 구분
    Boolean
    Null
```
```java
///JSON 의 구조
{
    "characters" : [
      {
        "name": "archer",
        "level": 1,
        "inventory": null,
        "hardcore": false
      },
      {
        "name": "knight",
        "level": 8,
        "inventory": ["sword", "shield"],
        "hardcore": true
      }
    ]
}
```




<details>
<summary>학습 목표</summary>

Java에서 제공하는 데이터 타입을 JSON으로 변경하는 기능을 구현할 수 있어야 합니다.

    null을 입력받을 경우, 알맞은 형태의 JSON으로 변환합니다
    Boolean 타입을 입력받을 경우, 알맞은 형태의 JSON으로 변환합니다
    String 타입을 입력받을 경우, 알맞은 형태의 JSON으로 변환합니다
    배열을 입력받을 경우, 알맞은 형태의 JSON으로 변환합니다
    HashMap을 입력받을 경우, 알맞은 형태의 JSON으로 변환합니다
    배열, Map 타입의 요소를 가진 배열이나 Map을 입력받을 경우, 알맞은 형태의 JSON으로 변환합니다.
</details>

## JSON
<details>

JSON
JSON의 탄생 배경

JSON은 JavaScript Object Notation의 줄임말로, 데이터 교환을 위해 만들어진 객체 형태의 포맷입니다. 네트워크를 통해, 어떤 객체 내용을 다른 프로그램에게 전송한다고 가정하겠습니다. 이 객체 내용을 일종의 메신저 혹은 채팅 프로그램에서 쓰는 하나의 메시지라고 한다면, 다음 데이터를 어떻게 전송할 수 있을까요?

1
2
3
4
5
6
Map<String, String> message = new HashMap<>(){{
      put("sender", "김코딩");
      put("receiver", "박해커");
      put("message", "밥먹을래?");
      put("createdAt", "2021-01-12,10:10:10");
    }};

코드 메시지를 담고 있는 데이터 message

메시지 데이터가 전송 가능하려면, 메시지를 보내는 발신자와 메시지를 받는 수신자가 같은 프로그램을 사용하거나, 문자열처럼 범용적으로 읽을 수 있는 형태여야 합니다.

    전송가능한 조건 (transferable condition)

        수신자(reciever)와 발신자(sender)가 같은 프로그램을 사용한다.
        또는, 문자열처럼 범용적으로 읽을 수 있어야 한다.

해당 데이터는 타입 변환을 이용해 String으로 변환할 경우 객체 내용을 포함하지 않습니다. Java에서 객체에 메소드(message.toString())를 시도하면, {createdAt=2021-01-12,10:10:10, receiver=박해커, sender=김코딩, message=밥먹을래?} 라는 결과를 리턴합니다. 해당 형식은 JSON의 형식과 다른 형태로 Java를 사용하지 않는 프로그램에서는 데이터를 정확하게 파악할수 없습니다.

이 문제를 해결하는 방법은 객체를 JSON의 형태로 변환하거나 JSON을 객체의 형태로 변환하는 방법입니다. 여러가지 방법이 존재하지만 해당 스프린트에서는 jackson 라이브러리에서 제공하는 ObjectMapper클래스를 사용하여 JSON형태로 변경하는 방법을 소개합니다.

1
2
3
4
5
6
7
ObjectMapper mapper = new ObjectMapper();
String json = mapper.writeValueAsString(message);

System.out.println(json);
/*
{"createdAt":"2021-01-12,10:10:10","receiver":"박해커","sender":"김코딩","message":"밥먹을래?"}
*/

    writeValueAsString하는 이 과정을 직렬화(serialize)한다고 합니다.

JSON으로 변환된 객체의 타입은 문자열입니다. 발신자는 객체를 직렬화한 문자열을 누군가에게 객체의 내용을 보낼 수 있습니다. 그렇다면 수신자는 이 문자열 메시지를 어떻게 다시 객체의 형태로 만들 수 있을까요? 

1
2
3
4
5
6
7
8
ObjectMapper mapper = new ObjectMapper();
String json = "{\"createdAt\":\"2021-01-12,10:10:10\",\"receiver\":\"박해커\",\"sender\":\"김코딩\",\"message\":\"밥먹을래?\"}";

Map<String, String> deserializedData = mapper.readValue(json, Map.class);
System.out.println(deserializedData);
/*
{createdAt=2021-01-12,10:10:10, receiver=박해커, sender=김코딩, message=밥먹을래?}
*/

코드 직렬화된 JSON에 메소드 readValue을 적용하면 다시 객체의 형태로 변환할 수 있습니다.

    readValue를 적용하는 이 과정을 역직렬화(deserialize)한다고 합니다.

https://3.bp.blogspot.com/-T5tlhDPiZnA/V_0INDboDQI/AAAAAAAABS8/je9dgx6_x2Y-AHgoBUQV5RwdaLyuFhPqwCLcB/s1600/serialize-deserialize-binary-tree.png
[그림] 직렬화와 역직렬화 모식도

이처럼, JSON은 서로 다른 프로그램 사이에서 데이터를 교환하기 위한 포맷입니다. 그리고 JSON 포맷은 자바스크립트을 포함한 많은 언어에서 범용적으로 사용하는 유명한 포맷입니다.
JSON의 기본 규칙

JSON을 얼핏 보기에 자바스크립트의 객체와 별반 다를 바가 없어 보이지만, 자바스크립트의 객체와는 미묘하게 다른 규칙이 있습니다. 자바스크립트의 객체 타입을 학습하지 않았지만, 차이점이 있다는것만 학습하고 넘어가셔도 무방합니다.

 image
[표] JSON과 자바스크립트 객체의 차리


또한 JSON은 키와 값 사이, 그리고 키-값 쌍 사이에는 공백이 있어서는 안됩니다.

    자세한 내용은 JSON 공식 문서을 참고하세요
</details>


## 시작하기
<details>

이번 과제는 재귀를 이용해 메서드 stringify를 직접 구현합니다.

이전 콘텐츠에서 writeValue는 데이터를 JSON으로 변환하는 메서드인 것을 확인했습니다. 이 메서드를 함수의 형태로 직접 구현하기 위해서, 재귀를 사용하세요. JSON은 대표적인 트리 구조를 가지고 있으므로, 전형적인 재귀 탐색이 가능한 구조(객체의 값으로 객체를 포함하는 구조)이기 때문에 재귀 사용을 적극 권장합니다. 어떻게 풀어야 할지 방향이 잘 정해지지 않는다면, 코플릿의 재귀 문제를 풀었던 방법을 다시 상기하세요. 부모와 자식의 구조가 같은 트리 구조를 어떤 조건에서 재귀 호출하면 좋을지 고민해보세요.
Getting Started

이번 과제는 IntelliJ를 사용하여 직접 코드를 작성하고, 테스트를 통해 정확한 코드를 입력했는지 확인할 수 있습니다.
아래 순서에 맞게 진행해주세요.

    repository 주소 에서 fork 및 clone 후 메소드를 작성합니다.
    IntelliJ를 실행합니다.
    열기를 클릭한 이후, 다운받은 폴더를 클릭하고 Open버튼을 클릭합니다.
    신뢰할 수 있는 프로젝트를 클릭합니다.
    src/main/java/stringifyJSON.java 파일을 열면, stringify메서드가 작성되어 있습니다. 해당 메서드에서 // TODO:부분을 직접 채워주세요.
    모두 작성하였다면, src/test/java/stringifyJSON_test.java파일을 실행하여 작성한 코드가 정상적으로 작동하는지 테스트를 진행할 수 있습니다.
    테스트는 아래 그림을 참고하시고, 1번 또는 2번 버튼을 통해 진행할 수 있습니다.

 image
Bare minimum Requirements

    src/main/java/stringifyJSON.java 에서 stringify 함수를 직접 구현해보고, src/test/java/stringifyJSON_test.java 파일을 실행하여 모든 테스트를 통과해야 합니다.

</details>