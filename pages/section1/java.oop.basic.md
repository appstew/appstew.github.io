---
layout: page
title: [Java]객체지향 프로그래밍 기초
description: >
hide_description: false
toc: true

---

{TOC}
0. this unordered seed list will be replaced by toc as unordered list
   {:toc}
> 레퍼런스 파일: hrd/section1/java.oop.basic/

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

```topojson
{
  "type": "Topology",
  "transform": {
    "scale": [0.0005000500050005, 0.00010001000100010001],
    "translate": [100, 0]
  },
  "objects": {
    "example": {
      "type": "GeometryCollection",
      "geometries": [
        {
          "type": "Point",
          "properties": {"prop0": "value0"},
          "coordinates": [4000, 5000]
        },
        {
          "type": "LineString",
          "properties": {"prop0": "value0", "prop1": 0},
          "arcs": [0]
        },
        {
          "type": "Polygon",
          "properties": {"prop0": "value0",
            "prop1": {"this": "that"}
          },
          "arcs": [[1]]
        }
      ]
    }
  },
  "arcs": [[[4000, 0], [1999, 9999], [2000, -9999], [2000, 9999]],[[0, 0], [0, 9999], [2000, 0], [0, -9999], [-2000, 0]]]
}
```

```stl
solid cube_corner
  facet normal 0.0 -1.0 0.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 1.0 0.0 0.0
      vertex 0.0 0.0 1.0
    endloop
  endfacet
  facet normal 0.0 0.0 -1.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 0.0 1.0 0.0
      vertex 1.0 0.0 0.0
    endloop
  endfacet
  facet normal -1.0 0.0 0.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 0.0 0.0 1.0
      vertex 0.0 1.0 0.0
    endloop
  endfacet
  facet normal 0.577 0.577 0.577
    outer loop
      vertex 1.0 0.0 0.0
      vertex 0.0 1.0 0.0
      vertex 0.0 0.0 1.0
    endloop
  endfacet
endsolid
```

**The Cauchy-Schwarz Inequality**

$$\left( \sum_{k=1}^n a_k b_k \right)^2 \leq \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)$$

**Here is some math!**

```math
\sqrt{3}
```


## 클래스와 객체

- 예제 파일:  SimpleCalculatorTest

```java
// 클래스는 객체를 생성하는 데 사용되는 하나의 틀
// 인스턴스: 클래스를 통해 생성된 객체
public class ExampleClass {
    int x = 10; // (1)필드
    void printX() {...} // (2)메서드
    ExampleClass {...} // (3)생성자
    class ExampleClass2 {...} // (4)이너 클래스
} 
// SimpleCalculatorTest.java
// 변수와 메서드
// CarTest.java
```

## 필드와 메서드

```java
// 변수는 크게 클래스 변수, 인스턴스 변수, 지연 변수
class Example { // => 클래스 영역
    int instanceVariable; // 인스턴스 변수
    static int classVariable; // 클래스 변수(static 변수, 공유변수)

    void method() { // => 메서드 영역
        int localVariable = 0; // 지역 변수. {}블록 안에서만 유효
    }
}
// Example.classVariable 로 사용할 수 있다
// 
// static 으로 만든 정적 변수 또는 메서드는 클래스명으로 호출된다.
// 아닌 경우 해당 변수가 포함된 클래스의 new 인스턴스로 호출된다.
// static 으로 만든 변수는 모든 인스턴스 사이에 값이 공유된다.
// StaticTest.java StaticFieldTest.java
//
// 매개 변수.
public static int add(int x, int y) { // 메서드 시그니처
    int result = x + y; // 메서드 바디
    return result;
}
// 메서드의 반환 타입이 void 가 아닌 경우는 바디{}안에 반드시 해당 반환 타입을 반환하는 return 문이 존재해야 한다. 
int getNumSeven() { // 매개변수가 없는 메서드
    return 7;
}
//
void printHello() { // 반환타입이 void인 메서드
    System.out.println("hello!");
}
// 즉 void 는, 반환 값이 없는 메서드를 의미
// 
// 메서드 오버로딩
// Overloading.java
```

![](../../img/windows_capture/2022-07-12-13-59-20-ozz3Hgv47FZY0Xsmh6j3--1651922487400.png)

=================

## 생성자

```java
// 생성자: 인스턴스 초기화 에 사용되는 특수한 메서드
// 1.생성자의 이름은 반드시 클래스의 이름과 같아야 한다.
// 2.생성자는 리턴 타입이 없다. 그러면서도 void 를 쓰지 않는다. 
// 생성자 오버로딩 예제: ConstructorExample.java CarTest.java
// 매개변수가 있는 생성자 예제: ConstructorExample.java
//
// this vs this()
// this() 메서드 는
// 1.생성자의 내부에서만 사용할 수 있고,
// 2.반드시 생성자의 첫 줄에 위치해야 한다.
// 예제: ConstructorExample.java
// 
```

## 내부 클래스

| 종 류                               | 선언 위치                              | 사용 가능한 변수            |
| --------------------------------- | ---------------------------------- | -------------------- |
| 인스턴스 내부 클래스(instance inner class) | 외부 클래스의 멤버변수 선언위치에 선언(멤버 내부 클래스)   | 외부 인스턴스 변수, 외부 전역 변수 |
| 정적 내부 클래스(static inner class)     | 외부 클래스의 멤버변수 선언위치에 선언(멤버 내부 클래스)   | 외부 전역 변수             |
| 지역 내부 클래스(local inner class)      | 외부 클래스의 메서드나 초기화블럭 안에 선언           | 외부 인스턴스 변수, 외부 전역 변수 |
| 익명 내부 클래스(anonymous inner class)  | 클래스의 선언과 객체의 생성을 동시에 하는 일회용 익명 클래스 | 외부 인스턴스 변수, 외부 전역 변수 |

```java
class Outer { // 외부 클래스

    class Inner {
        // 인스턴스 내부 클래스    
    }

    static class StaticInner {
        // 정적 내부 클래스
    }

    void run() {
        class LocalInner {
        // 지역 내부 클래스
        }
    }
}
// 내부 클래스 예제: innerClass.java
// 정적 내부 클래스: staticInnerClass.java
// 지역 내부 클래스: localInnerClass.java
```

## 심화 실습 - 텍스트 스타크래프트 프로그램

> dfdf

```java
//be-oop-reference/encapsulation, inheritance
//
//인텔리j Command+enter 로  getter setter 등 입력가
ㄴㅇㄴㅇ
ㅇㄷㅇㅇ
ㅈㅇㅈ
ㅈㅇㅈ
```

```
노래
super fantastic 페퍼톤스
```

1클래스내

2패키지내 

3다른 패키지의하위클래스

4패키지 외

접근구별자

private 1

default 12

protected 123

public 1234
