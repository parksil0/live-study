## enum 정의하는 방법

열거형은 상수를 편리하게 선언하기 위한 것으로 여러 상수를 정의할 때 사용하면 유용하다. 게다가 열거형은 갖는 값 뿐만 아니라 타입도 관리하기 때문에 보다 논리적인 오류를 줄일 수 있다.

열거형을 정의하는 방법은 앞에 enum 키워드를 붙이고, 중괄호 안에 상수의 이름을 나열하면 된다.

```java
enum Direction {
    EAST("동", 90),
    WEST("서", 270),
    SOUTH("남", 180),
    NORTH("북", 0);

    private String korean;
    private int num;

    Direction(String korean, int num) {
        this.korean = korean;
        this.num = num;
    }

    public String getKorean() {
        return korean;
    }

    public int getNum() {
        return num;
    }
}
```

위는 방향을 나열한 enum이다. 네 개의 상수(EAST, WEST, SOUTH, NORTH)에 멤버가 추가된 모습을 볼 수 있는데, 멤버를 추가하려면 생성자에 추가해야한다. 그 아래 get 메서드는 추가해도 되고 안해도 된다.

```java
public static void main(String[] args) {
    Direction d1 = Direction.EAST;
    Direction d2 = Direction.WEST;
    Direction d3 = Direction.SOUTH;
    Direction d4 = Direction.NORTH;

    System.out.println("d1: " + d1 + ", " + d1.getKorean() + ", " + d1.getNum());
    System.out.println("d2: " + d2 + ", " + d2.getKorean() + ", " + d2.getNum());
    System.out.println("d3: " + d3 + ", " + d3.getKorean() + ", " + d3.getNum());
    System.out.println("d4: " + d4 + ", " + d4.getKorean() + ", " + d4.getNum());
}

/*
	출력 결과

	d1: EAST, 동, 90
	d2: WEST, 서, 270
	d3: SOUTH, 남, 180
	d4: NORTH, 북, 0
	
	Process finished with exit code 0
*/
```

위는 enum인 Direction을 각각 변수에 담았다. 변수에 담을 때 우항을 보면 Direction. ... 의 형식이다. 이는 enum 자체를 객체로 선언할 수 없다. enum에 정의된 상수를 사용하는 방법은 'enum.상수'이다. 클래스의 static 변수를 참조하는것과 동일하다.

맨 아래 출력결과를 보면 각각의 상수와 멤버들을 전부 확인할 수 있다. 멤버의 값을 확인하려면 get()메서드가 필요하다.

## enum이 제공하는 메소드 (values()와 valueOf())

enum이 제공하는 메서드 중 values()와 valueOf() 메서드에 알아보려 한다.

- values()

  열거형 상수가 선언된 순서대로 포함된 배열을 반환한다. 이 메서드는 상수의 반복문을 통해 하나하나 값을 반환하는 형태로 풀어나갈 수 있다.

    ```java
    for(Direction c : Direction.values()) {
    	System.out.println(c);
    }
    ```

  위는 인텔리제이에서 예시로 values()를 어떻게 코드로 나타내는지에 대해 설명했다. 위는 향상된 for문을 통해 순서대로 처음부터 끝까지 출력할 수 있도록 나타낸 코드이다.

  아래의 예시를 통해 코드를 실행해보자

    ```java
    for(Direction dir : Direction.values()) {
        System.out.println(dir + ", " + dir.getKorean() + ", " + dir.getNum());
    }

    /*
    	출력결과
    	EAST, 동, 90
    	WEST, 서, 270
    	SOUTH, 남, 180
    	NORTH, 북, 0
    */
    ```

  위의 출력결과를 통해 values() 메서드는 enum이 배열 처럼 순서대로 하나하나 출력되는 모습을 볼 수 있다.

## java.lang.Enum

모든 열거형의 조상이 되는 java.lang.Enum 클래스는 10여가지 정도의 메서드가 있지만, 그 중 몇가지 대표적인 메서드를 알아보려한다

- Class<E> getDeclaringClass()

  열거형의 Class객체를 반환한다. 위의 <E>란 Element의 약자로, 배열 요소를 뜻한다.

- String name()

  열거형 상수의 이름을 문자열로 반환한다.

- int ordinal()

  열거형 상수가 정의된 순서를 반환한다. 순서는 0부터 시작한다.

- T valueOf(Class<T> enumType, String name)

  위에서 다룬 내용이니 위의 내용을 확인하면 된다.

위의 네 가지 메서드를 살펴보았는데, 그 외에 values()라는 메서드는 Enum 클래스에 정의되어 있는 메서드는 아니지만 컴파일러가 자동적으로 추가해주는 메서드가 있는데 그 것이 values() 메서드이다. 마찬가지로 values() 메서드도 위에서 다루었으니 확인하면 된다.

## EnumSet

EnumSet은 Set 인터페이스를 기반으로, enum 요소들을 보다 빠르고 강력하게 결과를 도출하는 역할을 한다.

![https://www.baeldung.com/wp-content/uploads/2018/10/EnumSet-1-2.jpg](https://www.baeldung.com/wp-content/uploads/2018/10/EnumSet-1-2.jpg)

자료참조 : [https://www.baeldung.com/wp-content/uploads/2018/10/EnumSet-1-2.jpg](https://www.baeldung.com/wp-content/uploads/2018/10/EnumSet-1-2.jpg)

위의 사진 자료를 보면 알 수 있듯, AbstractSet을 extend 했고, 그 위에는 Set 인터페이스를 implement한 것을 볼 수 있다. 다음은 EnumSet을 사용할 때 주의사항에 대해 알아보려 한다.

- enum만 포함할 수 있으며 모든 값은 같은 클래스의 enum이여야 한다.
- null값을 추가할 수 없다. 만약 추가한다면 NPE를 던질 것이다.
- thread-safe하지 않다. 그러므로 동기화를 해야한다.
- 요소들은 enum에서 정의된 순서에 따라 저장된다.
- EnumSet은 fail-safe iterator를 사용하기 때문에 복제를 하는 중에 컬렉션이 수정되더라도 ConcurrentModificationException을 던지지 않는다.

다음은 메서드에 대해 알아보자.

|이름|설명|
|:---|:---|
|static allOf(Class<E> elementType)|파라미터의 모든 요소들을 반환한다.|
|static complementOf(EnumSet<E> s)|지정된 enum에 포함되지 않은 모든 요소를 가진 집합을 반환한다.|
|static copyOf(Collection<E> c)<br> copyOf(EnumSet<E> s)|파라미터와 같은 EnumSet을 반환한다.|
|static noneOf(Class<E> elementType)|빈 enumSet을 반환한다.|
|static of(E e)|enum의 특정 요소를 반환한다.|



위의 EnumSet과 메서드들을 종합하여 예시를 통해 알아보자.

```java
public static void main(String[] args) {
    EnumSet<Direction> es = EnumSet.allOf(Direction.class);
    System.out.println("es: " + es);

    EnumSet<Direction> es2 = EnumSet.copyOf(es);
    System.out.println("es2: " + es2);

    EnumSet<Direction> es3 = EnumSet.of(Direction.NORTH, Direction.EAST);
    System.out.println("es3: " + es3);

    EnumSet<Direction> es4 = EnumSet.noneOf(Direction.class);
    System.out.println("es4: " + es4);

		EnumSet<Direction> es5 = EnumSet.complementOf(es3);
    System.out.println("es5: " + es5);
}

/*
	출력결과
	es: [EAST, WEST, SOUTH, NORTH]
	es2: [EAST, WEST, SOUTH, NORTH]
	es3: [EAST, NORTH]
	es4: []
	es5: [WEST, SOUTH]
*/
```

열거형 Direction을 통해 위의 EnumSet을 이용하여 코드를 구성해보았다. 메서드를 소개할 때 공통점은 모두 static 메서드이다. 그리고 위의 코드를 보았을 때 모두 new 연산자를 사용하지 않고 구현 객체를 반환받았다. 그 이유는 abstract 클래스이기 때문이다. 그 외로, 대표적으로 편의와 확장성, 유지보수의 이점때문이라고 보면 된다. 말 그대로 Enum에 Set 인터페이스를 구현했기 때문에 일일이 new 연산자를 사용하여 구현하기보단, Set에 담는다는 목적으로 allOf() 라는 메서드를 사용하면 쉽게 반환받고 사용할 수 있다.

es3 코드를 보면, Direction.NORTH, Direction.EAST로 객체를 구현했지만 출력결과를 보면 EAST, NORTH라고 출력이 되었다. 그 이유는 EnumSet의 주의사항에서 다룬 '*요소들은 enum에서 정의된 순서에 따라 저장된다.*' 라는 특징 때문이다.

그 외 나머지는 메서드 설명에 비교하여 보면 크게 어려움은 없을 것이다.

자료 참조

자바의 정석 3rd Edition(남궁 성 저)

[http://alecture.blogspot.com/2012/11/enumset.html](http://alecture.blogspot.com/2012/11/enumset.html)

[https://www.baeldung.com/java-enumset](https://www.baeldung.com/java-enumset)

[https://docs.oracle.com/javase/8/docs/api/](https://docs.oracle.com/javase/8/docs/api/)

[https://siyoon210.tistory.com/152](https://siyoon210.tistory.com/152)