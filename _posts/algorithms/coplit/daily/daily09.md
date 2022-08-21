---
layout: post
title: daily09
category: algorithms
tags: coplit

---

```java
package com.codestates.coplit; 
import java.util.*;

public class Solution { 
    public boolean ABCheck(String str) {
    // TODO:
String s = str.toLowerCase();
//Boolean result;

    for (int i = 0; i<s.length()-4; i++) {
    if (s.charAt(i) == 'a' && s.charAt(i+4) == 'b') return true; // result = true;
    else if (s.charAt(i) == 'b' && s.charAt(i+4) == 'a') return true; // result = true;
    return false; // result = false;
}
// return result;
    }
}
```

- 이렇게 풀었더니 
- java:16: error: missing return statement
- 에러가 떠서 // 뒷 부분처럼 result boolean 변수를 만들고 했더니
- variable result might not have been initialized
- 왜 .. ?
- 그리고 혹시 몰라 구글링 후
- https://www.baeldung.com/java-error-variable-initialized
- 결과는? 
- 오류는 발생하지 않았으나 테스트 중 몇개를 통과하지 못했다.
- 그리고 

```java
package com.codestates.coplit; 
import java.util.*;

public class Solution { 
    public boolean ABCheck(String str) {
    // TODO:
if (str.length() == 0) return false;
String s = str.toLowerCase();
Boolean result = true;

    for (int i = 0; i<s.length(); i++) {
    if (s.charAt(i) == 'a' && s.charAt(i+4) == 'b')  {result = true;}
    else if (s.charAt(i) == 'b' && s.charAt(i+4) == 'a')  {result = true;}
     else {result = false;}
}
return result;
    }
}
```

- 여전히 몇개의 테스트를 통과하지 못한다. 이해가 안된다. 다음에 다시 보자.