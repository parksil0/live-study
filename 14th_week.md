## 제네릭 사용법

- 제네릭이란?

  제네릭은 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 컴파일 시의 타입 체크를 해주는 기능이다. 객체의 타입을 컴파일 시에 체크하기 때문에 객체의 타입 안전성을 높이고 형변환의 번거로움이 줄어든다.

  타입 안정성을 높인다는 것은 의도하지 않은 타입의 객체가 저장되는 것을 막고, 저장된 객체를 꺼내올 때 원래의 타입과 다른 타입으로 잘못 형변환되어 발생할 수 있는 오류를 줄여준다는 뜻이다.

  결론적으로 제네릭이란, 다룰 객체의 타입을 미리 명시해줌으로써 번거로운 형변환을 줄여준다는 뜻이다.

- 제네릭 클래스 생성

    ```java
    class Box<T> {
        ArrayList<T> list = new ArrayList<T>();
        void add(T item) {
            list.add(item);
        }

        T get(int i) {
            return list.get(i);
        }

        int size() {
            return list.size();
        }

        @Override
        public String toString() {
            return list.toString();
        }
    }
    ```

  위의 코드의 맨 첫줄에 'Box<T>'가 보일 것이다. Box는 원시 타입을, '<T>'는 타입 변수 또는 타입 매개변수를 뜻한다. 이 둘을 합쳐 'Box<T>'를 제네릭 클래스라고 한다.

  여기서 T는 Type(타입)을 뜻한다. T 외에 E, K, V가 있는데 E는 Element를, K와 V는 Key와 Value를 나타낸다.

  예를들어, Element는 보통 배열의 요소로써 ArrayList<E>로 주로 사용되며, Key, Value(키값과 밸류값)는 Map<Key, Value>로 주로 사용된다.

  정리하자면, 상황에 맞게 의미있는 문자를 선택해서 사용되며, 기호의 종류만 다를 뿐 임의의 참조형 타입을 의미한다.

  다시 위의 코드로 돌아가서 T 대신에 원하는 타입을 대입하면 코드가 어떻게 해석되는지를 이해할 수 있을 것이다.

- 제네릭 클래스 객체 생성과 사용

  위의 제네릭 클래스를 이용하여 객체를 선언하고 사용해보자.

    ```java
    public class Test {
        public static void main(String[] args) {
            Box<String> stringBox = new Box<String>();
            stringBox.add("live study");
            stringBox.add(14); // error, required type : string, current type : int
            System.out.println(stringBox.get(0));
        }
    }

    /*
    	출력결과

    	live study

    */
    ```

  위의 제네릭 클래스를 사용하여 객체를 생성하였고, 클래스에서 제공되는 메서드를 통해 제네릭의 특징에 대해 알아보자.

  먼저 제네릭 타입 변수는 String 타입이다. 첫번째 add 메서드에는 String 타입이 매개변수에 들어갔기 때문에 정상적으로 add가 되었지만 그 다음줄에는 String 타입이 아니기 때문에 컴파일 에러를 발생시킨다. 마지막으로 get() 메서드를 통해 출력결과를 알 수 있다.

## 제네릭 주요 개념 (바운디드 타입, 와일드 카드)

- 바운디드 타입

  타입 매개변수 T에 지정할 수 있는 타입의 종류는 모든 종류가 가능하며 그 중 한 종류의 타입만 저장할 수 있다. 게다가 'extends'라는 키워드를 사용하여 타입의 종류를 제한하는 방법도 있다.예를 들어,

    ```java
    public class Test {
        public static void main(String[] args) {
            FruitBox<Grape> list = new FruitBox<>();
        }
    }

    class FruitBox<T extends Fruit> {
        //...
    }

    class Fruit {
        //...
    }

    class Grape extends Fruit {
        //...
    }
    ```

  중간의 'FruitBox' 클래스의 타입지정 부분을 보면 '<T extends Fruit>'이라는 키워드가 보일것이다. 저 부분이 바운디드된 타입이다. Fruit을 포함한 상속받은 자식 클래스들도 타입에 허용이 된다는 뜻이다. 또한 타입 매개변수에 Object를 대입하면 모든 종류의 객체를 저장할 수 있게 된다.

  만일 클래스가 아닌 인터페이스를 구현해야 한다는 제약이 필요하다 하더라도 'implements'가 아닌 'extends'를 사용해야 한다는 점이 바운디드 타입을 사용하면서의 주의해야할 점이다.

  클래스의 자손이면서 인터페이스를 구현해야 한다면 '&' 키워드로 연결할 수 있다.

    ```java
    public class Test {
        public static void main(String[] args) {
            FruitBox<Grape> list = new FruitBox<>();
        }
    }

    class FruitBox<T extends Fruit & Eatable & Cuttable> {
        //...
    }

    class Fruit {
        //...
    }

    class Grape extends Fruit implements Eatable, Cuttable {
        //...
    }

    interface Eatable {

    }

    interface Cuttable {

    }
    ```

  위의 예제에서 처음의 예제와 다른 점이라면, 인터페이스의 추가 부분이다. 그리고 'FruitBox' 클래스의 타입 지정 부분에서 '&' 키워드와 인터페이스가 추가되었다. 위의 코드를 통해 알 수 있는 사실은, 자바 클래스에서의 상속과 인터페이스 구현 부분이 일치한다. 'extends'로 사용할 수 있는 클래스는 하나만 가능하며, 인터페이스는 여러개가 허용된다.

- 와일드 카드

  와일드 카드는 기호 '?'로 표현하며, 타입을 지정할 수 없다. 그렇다면 '?' 기호는 Object 타입과는 다를게 없게 된다. 그렇기 때문에 'extends' 또는 'super'로 상한과 하한으로 범위를 지정할 수 있다.

  |종류|설명|
  |---|---|
  |<? extends T>|와일드 카드의 상한 제한, T와 그 자손들만 가능|
  |<? super T>|와일드 카드의 하한 제한, T와 그 조상들만 가능|
  |<?>|제한 없음. 모든 타입이 가능. <? extends Object>와 동일|

## 제네릭 메소드 만들기

메서드의 선언부에 제네릭 타입이 선언된 메서드를 제네릭 메서드라 하며, 제네릭 타입의 선언 위치는 반환 타입 바로 앞이다.

```java
static <T> void sort(List<T> list, Comparator<? super T> c)
```

위는 'Collections.sort()' 메서드이며, 위에서 설명한 제네릭 메서드이다. 제네릭 클래스에 정의된 타입 매개변수와 제네릭 메서드에 정의된 타입 매개변수는 별개의 것이며, 같은 타입 문자 'T'를 사용해도 같은 것이 아니라는 것에 유의해야 한다.

```java
class FruitBox<T extends Fruit> extends Box<T>{
    //...
    static <T> void sort(List<T> list, Comparator<? super T> c) {
        
    }
}
```

클래스에서 정의한 'T'와 메서드에서 정의한 'T'는 타입 문자만 같을 뿐 서로 다른 것이다.

덧붙여 설명하자면 static 멤버에는 타입 매개변수를 사용할 수 없지만, 이처럼 메서드에 지네릭 타입을 선언하고 사용하는 것은 가능하다.

## Erasure

컴파일러는 제네릭 타입을 이용해서 소스파일을 체크하고, 필요한 곳에 형변환을 넣어준다. 그리고 제네릭 타입을 제거한다. 즉, 컴파일 된 파일에는 제네릭 타입에 대한 정보가 없다. 그 이유는 이전의 소스코드와의 호환성을 유지하기 위해서이다.

1. 먼저 제네릭 타입을 제거하기 전 제네릭 타입의 바운드를 제거한다.

```java
//before
class Box<T extends Fruit> { 
	void add(T t) {
		//...
	}
}

//after
class Box {
	void add(Fruit t) {
		//...
	}
}

```

before 부분을 보면 제네릭 타입의 바운드가 있고, after에서는 입력된 타입으로 변환되었다.

2. 제네릭 타입을 제거한 후 타입이 일치하지 않으면, 형변환을 추가한다.

```java
//before
T get(int i) {
	return list.get(i);
}

//after
Fruit get(int i) {
	return (Fruit)list.get(i);
}
```

List의 get() 메서드는 Object 타입을 반환하므로 형변환이 필요한 경우이다.

- 만약 와일드 카드가 포함되어 있는 경우

    ```java
    //before
    static Juice makeJuice(FruitBox<? extends Fruit> box) {
    	String tmp = "";
    	for(Fruit f : box.getList()) {
    		tmp += f + " ";
    	}
    	return new Juice(tmp);
    }

    //after
    static Juice makeJuice(FruitBox<? extends Fruit> box) {
    	String tmp = "";
    	Iterator ite = box.getList().iterator();
    	while(ite.hasNext()) {
    		tmp += (Fruit)ite.next() + " ";
    	}
    	return new Juice(tmp);
    }
    ```

  다음과 같이 적절한 타입으로의 형변환이 추가된다.

자료참조

자바의 정석 3rd Edition(남궁 성 저)