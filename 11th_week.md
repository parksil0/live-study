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

자료 참조

자바의 정석 3rd Edition(남궁 성 저)