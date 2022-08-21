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
// 이는 타입이 지정되는 시점이 서로 다르기 때문입니다. 즉, 클래스명 옆에서 선언한 타입 매개변수는 클래스가 인스턴스화될 때 타입이 지정됩니다.
```
```java
// 그러나, 제네릭 메서드의 타입 지정은 메서드가 호출될 때 이루어집니다. 제네릭 메서드를 호출할 때에는 아래와 같이 호출하며, 이 때 제네릭 메서드에서 선언한 타입 매개변수의 구체적인 타입이 지정됩니다. 
Basket<String> basket = new Bakset<>(); // 위 예제의 1의 T가 String으로 지정됩니다. 
basket.<Integer>add(10);                // 위 예제의 2의 T가 Integer로 지정됩니다. 
basket.add(10);                         // 타입 지정을 생략할 수도 있습니다. 
```
```java
// 또한, 클래스 타입 매개변수와 달리 메서드 타입 매개변수는 static 메서드에서도 선언하여 사용할 수 있습니다. 
class Basket {
		...
		static <T> int setPrice(T element) {
				...
		}
}
```
```java
// 제네릭 메서드는 메서드가 호출되는 시점에서 제네릭 타입이 결정되므로, 제네릭 메서드를 정의하는 시점에서는 실제 어떤 타입이 입력 되는지 알 수 없습니다. 따라서 length()와 같은 String 클래스의 메서드는 제네릭 메서드를 정의하는 시점에 사용할 수 없습니다.
class Basket {
    public <T> void print(T item) {
        System.out.println(item.length()); // 불가
    }
}
```
```java
// 하지만 모든 자바 클래스의 최상위 클래스인 Object 클래스의 메서드는 사용가능합니다. 모든 클래스는 Object 클래스를 상속받기 때문입니다. 지금까지 여러분이 사용해본 equals(), toString() 등이 Object 클래스의 메서드에 속합니다. 
class Basket {
    public <T> void getPrint(T item) {
        System.out.println(item.equals("Kim coding")); // 가능
    }
}
```














## 컬렉션 프레임워크


### 개요 

- 컬렉션이란 여러 데이터들의 집합을 의미한다. 이러한 컬렉션들을 다루는 데에 있어 편리한 메서드들을 미리 정의해놓은 것을 컬렉션 프레임워크라고 합니다.

### 컬렉션 프레임워크란?

![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/hY9Gx_qEeirBzawErMPrR-1657734686317.png)

|||||
|--|--|--|--|
|List|List는 데이터의 순서가 유지되며, 중복 저장이 가능한 컬렉션을 구현하는 데에 사용됨|ArrayList, Vector, Stack, LinkedList 등||
|Set|Set은 데이터의 순서가 유지되지 않고, 중복 저장이 불가능한 컬렉션을 구현하는데 사용됨|HashSet, TreeSet 등||
|Map|Map은 키(key)와 값(value)의 쌍으로 데이터를 저장하는 컬렉션을 구현|HashMap, HashTable, TreeMap, Properties 등|데이터의 순서가 유지되지 않으며, 키는 값을 식별하기 위해 사용되므로 중복 저장이 불가능하지만, 값은 중복 저장이 가능합니다.|
|||||
|||||

- Collection 인터페이스
    - 컬렉션 인터페이스에는 아래와 같은 메서드들이 정의되어져 있다. 

| 기능    | 리턴 타입    | 메소드                                            | 설명                                                       |
| ----- | -------- | ---------------------------------------------- | -------------------------------------------------------- |
| 객체 추가 | boolean  | add(Object o) / <br> addAll(Collection c)      | 주어진 객체 및 컬렉션의 객체들을 컬렉션에 추가합니다.                           |
| 객체 검색 | boolean  | contains(Object o) / containsAll(Collection c) | 주어진 객체 및 컬렉션이 저장되어 있는지 여부를 리턴합니다.                        |
|       | Iterator | iterator()                                     | 컬렉션의 iterator를 리턴합니다.                                    |
|       | boolean  | equals(Object o)                               | 컬렉션이 동일한지 여부를 확인합니다.                                     |
|       | boolean  | isEmpty()                                      | 컬렉션이 비어있는지 여부를 확인합니다.                                    |
|       | int      | size()                                         | 저장되어 있는 전체 객체 수를 리턴합니다.                                  |
| 객체 삭제 | void     | clear()                                        | 컬렉션에 저장된 모든 객체를 삭제합니다.                                   |
|       | boolean  | remove(Object o) / removeAll(Collection c)     | 주어진 객체 및 컬렉션을 삭제하고 성공 여부를 리턴합니다.                         |
|       | boolean  | retainAll(Collection c)                        | 주어진 컬렉션을 제외한 모든 객체를 컬렉션에서 삭제하고, 컬렉션에 변화가 있는지의 여부를 리턴합니다. |
| 객체 변환 | Object[] | toArray()                                      | 컬렉션에 저장된 객체를 객체배열(Object [])로 반환합니다.                     |
|       | Object[] | toArray(Object[] a)                            | 주어진 배열에 컬렉션의 객체를 저장해서 반환합니다.                             |


### List<E>

#### List

- List 는 배열과 같이 객체를 일렬로 늘어놓은 구조. 인덱스로 객체를 관리함.

- List 메서드

| 기능    | 리턴 타입        | 메서드                                       | 설명                                                                       |
| ----- | ------------ | ----------------------------------------- | ------------------------------------------------------------------------ |
| 객체 추가 | void         | add(int index, Object element)            | 주어진 인덱스에 객체를 추가                                                          |
|       | boolean      | addAll(int index, Collection c)           | 주어진 인덱스에 컬렉션을 추가                                                         |
|       | Object       | set(int index, Object element)            | 주어진 위치에 객체를 저장                                                           |
| 객체 검색 | Object       | get(int index)                            | 주어진 인덱스에 저장된 객체를 반환                                                      |
|       | int          | indexOf(Object o) / lastIndexOf(Object o) | 순방향 / 역방향으로 탐색하여 주어진 객체의 위치를 반환                                          |
|       | ListIterator | listIterator() / listIterator(int index)  | List의 객체를 탐색할 수 있는ListIterator 반환 / 주어진 index부터 탐색할 수 있는 ListIterator 반환 |
|       | List         | subList(int fromIndex, int toIndex)       | fromIndex부터 toIndex에 있는 객체를 반환                                           |
10
| 객체 삭제 | Object       | remove(int index)                         | 주어진 인덱스에 저장된 객체를 삭제하고 삭제된 객체를 반환                                         |
|       | boolean      | remove(Object o)                          | 주어진 객체를 삭제                                                               |
| 객체 정렬 | void         | sort(Comparator c)                        | 주어진 비교자(comparator)로 List를 정렬                                            |
​

#### ArrayList 

- ArrayList 는 List 인터페이스를 구현한 클래스로, 컬렉션 프레임워크에서 가장 많이 사용됩니다.
- 배열은 크기가 고정되고 변경할 수 없는 반면, ArrayList 는 저장 용량을 초과하여 객체들이 추가되어도 자동으로 저장용량이 늘어난다. 
- 또 리스트 계열 자료구조의 특성을 이어받아 데이터가 연속적으로 존재합니다. 
- 즉, 데이터의 순서를 유지합니다.

- ArrayList 생성 예제

```java
List<타입 매개변수> 객체명 = new ArrayList<타입 매개변수>(초기 저장 용량);

List<String> container1 = new ArrayList<String>();
// String 타입의 객체를 저장하는 ArrayList 생성
// 초기 용량이 인자로 전달되지 않으면 기본적으로 10으로 지정됩니다. 

List<String> container2 = new ArrayList<String>(30);
// String 타입의 객체를 저장하는 ArrayList 생성
// 초기 용량을 30으로 지정하였습니다. 
```

- ArrayList 에 String 객체를 추가, 검색, 삭제하는 예제
```java
public class ArrayListExample {
	public static void main(String[] args) {

		// ArrayList를 생성하여 list에 할당
		List<String> list = new ArrayList<String>();

		// String 타입의 데이터를 ArrayList에 추가
		list.add("Java");
		list.add("egg");
		list.add("tree");

		// 저장된 총 객체 수 얻기
		int size = list.size(); 

		// 0번 인덱스의 객체 얻기
		String skill = list.get(0);

		// 저장된 총 객체 수 만큼 조회
		for(int i = 0; i < list.size(); i++){
			String str = list.get(i);
			System.out.println(i + ":" + str);
		}

		// for-each문으로 순회 
		for (String str: list) {
			System.out.println(str);
		}		

		// 0번 인덱스 객체 삭제
		list.remove(0);
	}
}
```


#### LinkedList

- LinkedList 컬렉션의 데이터는 불연속적으로 존재하며, 이 데이터는 서로 연결되어 있습니다.

![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/y9EtzRjEEVZ9N2kuDHJaV-1657735086144.png)

- LinkedList 에서 데이터를 삭제하려면, 삭제하고자 하는 요소의 이전 요소가 삭제하고자 하는 요소의 다음 요소를 참조하도록 변경하면 됩니다. 링크를 끊어주는 방식이라고 생각하면 됩니다. 

- 배열처럼 데이터를 이동하기 위해 복사할 필요가 없어서 처리 속도가 훨씬 빠릅니다.

```java
public class LinkedListExample {
	public static void main(String[] args) {
		
		// Linked List를 생성하여 list에 할당
		List<String> list = new LinkedList<>();

		// String 타입의 데이터를 LinkedList에 추가
		list.add("Java");
		list.add("egg");
		list.add("tree");

		// 저장된 총 객체 수 얻기
		int size = list.size(); 

		// 0번 인덱스의 객체 얻기
		String skill = list.get(0);

		// 저장된 총 객체 수 만큼 조회
		for(int i = 0; i < list.size(); i++){
			String str = list.get(i);
			System.out.println(i + ":" + str);
		}

		// for-each문으로 순회
		for (String str: list) {
			System.out.println(str);
		}		

		// 0번 인덱스 객체 삭제
		list.remove(0);
	}
}
```

#### ArrayList vs LinkedList

![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/nEoZSvi3dElf26DO80ljB-1657735127303.png)

- 위 그림은 ArrayList 에서 데이터를 추가하는 상황입니다,

- 그림과 같이 다른 데이터를 복사 이동 해야 합니다.

- ArrayList 는 순차쓰기가 빠르지만, 중간 데이터 쓰기/읽기는 느리다.

- 반면 인덱스 방식이므로 검색(읽기)는 빠르다.

```java
즉, ArrayList는 다음과 같은 상황에 강점을 지닙니다. 

    데이터를 순차적으로 추가하거나 삭제하는 경우

        순차적으로 추가한다는 것은 0번 인덱스에서부터 데이터를 추가하는 것을 의미합니다.

        순차적으로 삭제한다는 것은 마지막 인덱스에서부터 데이터를 삭제하는 것을 의미합니다.

    데이터를 읽어들이는 경우
        인덱스를 통해 바로 데이터에 접근할 수 있으므로 검색이 빠릅니다.


다음과 같은 상황에서 ArrayList는 효율적이지 못합니다. 

    중간에 데이터를 추가하거나, 중간에 위치하는 데이터를 삭제하는 경우
        추가 또는 삭제 시, 해당 데이터의 뒤에 위치한 값들을 뒤로 밀어주거나 앞으로 당겨주어야 합니다.
```

![](https://s3.ap-northeast-2.amazonaws.com/urclass-images/otYh6ONO9GRELle0ohRlA-1657735168396.png)

- 한편 LinkedList 에 위 그림처럼 Apple , Mango 사이에 데이터를 추가하려면
    1. Mango 객체가 생성됨
    2.Apple 의 Next 에 Mango 주소값이 저장됨
        a. 이때, Mango의 Prev 에 Apple 의 주소값이 저장됨
    3. Mango의 Next 에 Orange 의 주소값이 저장됨
        a. 이때, Orange의 Prev 에 Mango 값의 주소값이 저장됨

- 이처럼 next와 prev에 저장되어있는 주소값만 변경하면 되므로, 

- 중간 데이터 추가/삭제 에는 LinkedList가 ArrayList 보다 빠르다.

- 하지만 검색은 ArrayList보다 느리다.

```java
/// LinkedList 가 강점을 가지는 상황
    중간에 위치하는 데이터를 추가하거나 삭제하는 경우
        데이터를 중간에 추가하는 경우, Prev와 Next의 주소값만 변경하면 되므로, 다른 요소들을 이동시킬 필요가 없습니다.


결론적으로, 데이터의 잦은 변경이 예상된다면 LinkedList를, 데이터의 개수가 변하지 않는다면 ArrayList를 사용하는 것이 좋습니다.
```


