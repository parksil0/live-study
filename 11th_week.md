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

## java.lang.Enum

## EnumSet

자료 참조

자바의 정석 3rd Edition(남궁 성 저)