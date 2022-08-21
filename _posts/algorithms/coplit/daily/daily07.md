---
layout: post
title: daily07
category: algorithms
tags: coplit
---
# convertListToObject

## 문제

2차원 배열(배열을 요소로 갖는 배열)을 입력받아 각 배열을 이용해 만든 HashMap을 리턴해야 합니다.

## 입력

### 인자 1 : arr

- 배열을 요소로 갖는 배열
- `arr[i]`는 `String` 타입을 요소로 갖는 배열
- `arr[i].length`는 0 또는 2
- String[](https://urclass.codestates.com/codeproblem/016520c1-cb8b-4a00-8daa-456555ee2eb6) arr;

## 출력

- `arr[i]`의 첫 번째 요소를 키, 두 번째 요소를 값으로 하는 `HashMap<String, String>`을 리턴해야 합니다.

## 주의 사항

- 중복되는 키의 경우, 초기의 값을 사용합니다.
- 빈 배열을 입력받은 경우, 빈 HashMap을 리턴해야 합니다.
- `arr[i]`의 길이가 0인 경우, 무시합니다.

## 입출력 예시

```
String[][] arr = new String[]{
  {'make', 'Ford'},
  {'model', 'Mustang'},
  {'year', '1964'},
  {'make', 'Bill'},
};

HashMap<String, String> output = convertListToObject(arr);

System.out.println(output) // -->
{
  "make" = "Ford"
  "model" = "Mustang",
  "year" = "1964"
}
```


