---
layout: page
title: [Java]기초
description: >
hide_description: false
toc: true

---

### StringBuilder
```java

public class Main {
    public static void main(String[] args) {
        StringBuilder stringBuilder = new StringBuilder();
        stringBuilder.append("문자열 ").append("연결");
        String str = stringBuilder.toString();
        System.out.println(stringBuilder);
        System.out.println(str);
    }
}
```

- string.delete(4,8)
- 4~7인덱스 문자열을 삭제한다.


- str.concat("수업") 이미 있다. 그러나 
- stringBuilder.append("문자열")("문자열");
- 즉 concat() 보다 StringBuilder append() 가 내부 처리 속도가 빠르다고 한다.

