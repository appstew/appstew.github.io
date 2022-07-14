---
layout: page
title: [Java]Collection
description: >
hide_description: false
toc: true
toc_sticky
---
{TOC}

0. this unordered seed list will be replaced by toc as unordered list
   {:toc}

## 제네릭
```java
class Basket {
    private String item;

    Basket(String item) {
        this.item = item;
    }

    public String getItem() {
        return item;
    }

    public void setItem(String item) {
        this.item = item;
    }
}
// 이런 상황에서
```
```java
class BasketString { private String item; ... }
class BasketInteger { private int item; ... }
class BasketChar { private char item; ... }
class BasketDouble { private double item; ... }
...
// 원래이렇게 써야 되는데 
```

### 제네릭이란?

```java
class Basket(T) {
    private T item;

    public Basket(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }
    
    public void setItem(T item) {
        this.item = item;
    }
}
// 이렇게 줄일 수 있고
```
```java
//용법
Basket<String> basket1 = new Basket<String>("기타줄");
Basket<Integer> basket2 = new Basket<Integer>(1);

class Basket<K, V> { ... } // K, V 등을 타입 매개변수 라고 부른다.
```

### 제네릭 클래스

```java
class Basket<T> {
	private T item1; // O 
	static  T item2; // X 
}
//[중요] 위처럼 제네릭 클래스 변수에는 static 을 쓸 수 없다.
//제네릭 클래스 변수에 static 을 사용한다면, Basket<String> 으로 만든 인스턴스와, Basket<Integer>로 만든 인스턴스가 공유하는 클래스 변수의 타입이 서로 달라지게 되므로, 타입 매개변수를 사용할 수 없다.
```
```java
// 제네릭 클래스의 사용
Basket<String>  basket1 = new Basket<String>("Hello");
Basket<Integer> basket2 = new Basket<Integer>(10);
Basket<Double>  basket3 = new Basket<Double>(3.14);
```
```java
//위 코드는 아래와 같이 써도 된다.
Basket<String>  basket1 = new Basket<>("Hello");
Basket<Integer> basket2 = new Basket<>(10);
Basket<Double>  basket2 = new Basket<>(3.14);
```

### 제한된 제네릭 클래스

```java
// 제네릭 클래스를 사용할 때에도 다형성을 적용할 수 있다.
class Flower { ... }
class Rose extends Flower { ... }
class RosePasta { ... }

class Basket<T> {
    private T item;

    public T getItem() {
        return item;
    }

    public void setItem(T item) {
        this.item = item;
    }
}

public static void main(String[] args) {
		
        Basket<Flower> flowerBasket = new Basket<>();
		flowerBasket.setItem(new Rose());      // 다형성 적용
		flowerBasket.setItem(new RosePasta()); // 에러
        
		Basket<Rose> roseBasket = new Basket<>();
		Basket<RosePasta> rosePastaBasket = new Basket<>();
}
```
```java
class Flower { ... }
class Rose extends Flower { ... }
class RosePasta { ... }

class Basket<T extends Flower> { // 차이
    private T item;
	
		...
}

public static void main(String[] args) {

		// 인스턴스화 
		Basket<Rose> roseBasket = new Basket<>();
		Basket<RosePasta> rosePastaBasket = new Basket<>(); // 에러
}
```
```java
interface Plant { ... }
class Flower implements Plant { ... }
class Rose extends Flower implements Plant { ... }

class Basket<T extends Plant> {
    private T item;
	
		...
}

public static void main(String[] args) {

		// 인스턴스화 
		Basket<Flower> flowerBasket = new Basket<>();
		Basket<Rose> roseBasket = new Basket<>();
}
```
```java
interface Plant { ... }
class Flower implements Plant { ... }
class Rose extends Flower implements Plant { ... }

class Basket<T extends Plant & Flower> {
    private T item;
	
		...
}

public static void main(String[] args) {

		// 인스턴스화 
		Basket<Flower> flowerBasket = new Basket<>();
		Basket<Rose> roseBasket = new Basket<>();
}
// 만약, 특정 클래스를 상속받으면서 동시에 특정 인터페이스를 구현한 클래스만 타입으로 지정할 수 있도록 제한하려면 아래와 같이 &를 사용하여 코드를 작성해주면 된다.
```

### 제네릭 메서드
```java
// 제네릭 메서드의 타입 매개변수 선언은 반환 타입 앞에서 이루어지며,
// 해당 메서드 내에서만 해당 타입 매개변수를 사용할 수 있다.
class Basket {
		...
		public <T> void add(T element) {
				...
		}
}
```
```java
// 제네릭 메서드의 타입 매개변수와 제네릭 클래스의 타입 매개변수는 같은 문자를 사용하더라도 서로 별개로 간주된다.
class Basket<T> {                        // 1 : 여기에서 선언한 타입 매개변수 T와 
		...
		public <T> void add(T element) { // 2 : 여기에서 선언한 타입 매개변수 T는 서로 다른 것입니다.
				...
		}
}
```

















## 컬렉션 프레임워크