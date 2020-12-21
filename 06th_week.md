## 자바 상속의 특징

- 유지 보수에 용이하다.

  상속의 특징 중 하나로, 클래스를 재사용하여 클래스를 작성하면 보다 적은 양의 코드로 새로운 클래스를 작성할 수 있어 코드의 추가 및 변경이 용이하다. 또한 재사용성을 높이고 중복을 제거하여 용이한 유지보수에 도움이 된다.

- 단일 상속

  자바에서는 다중 상속을 지원하지 않고, 오직 단일 상속만을 허용한다. 그 이유는 클래스 간의 관계가 매우 복잡해진다는 것과 서로 다른 클래스로부터 상속받은 멤버간의 이름이 같은 경우 구별할 수 있는 방법이 없다는 단점을 가지고있다.

  예를 들어 클래스 A와 클래스 B 둘 다 playMusic()이라는 메소드가 두 메서드를 구별할 수 있는 방법은 없다.

- 상속에 제한이 없다.

  말 그대로 상속을 받은 클래스를 새로운 클래스에서 상속을 받을 수 있으며, 상속에 제한이 없다.

자료참조

자바의 정석 3rd Edition(남궁 성 저)

## super 키워드

- super

  상속 받은 멤버와 클래스 내의 멤버와 이름이 같을 때는 super를 붙여 구별할 수 있다. 조상의 멤버와 자신의 멤버를 구별하는데 사용된다는 점을 제외하고는 super와 this는 근본적으로 같다. 모든 인스턴스 메서드에는 자신이 속한 인스턴스의 주소가 지역변수로 저장되는데, 이것이 참조변수인 this와 super값이 된다.

    ```java
    class Test {
    	public static void main(String[] args) {
    		Child child = new Child();
    		child.method();
    	}
    }

    class Parent {
    	int num = 100;
    }

    class Child extends Parent {
    	int num = 200;

    	void method() {
    		System.out.println("num = " + num);
    		System.out.println("this.num = " + this.num); // 200
    		System.out.println("super.num = " + super.num); // 100
    	}
    }
    ```

- super()

  super 옆에 소괄호가 붙으면 생성자를 뜻한다. 이는 조상 클래스의 생성자를 호출하는데 사용된다. 자손 클래스의 인스턴스를 생성하면, 자손의 멤버와 조상의 멤버가 모두 합쳐진 하나의 인스턴스가 생성된다. 그래서 자손 클래스의 인스턴스가 조상 클래스의 멤버들을 사용할 수 있게된다. 이 때 조상 클래스 멤버의 초기화 작업이 수행되어야 하기 때문에 자손 클래스의 생성자에서 조상 클래스의 생성자가 호출되어야 한다.

  자손 클래스의 생성자의 첫 줄에는 조상 클래스의 생성자를 호출해야하는데, 그 이유는 자손 클래스의 멤버가 조상 클래스의 멤버를 사용할 수 있기 때문에 먼저 초기화가 되어있어야 한다.

  조상클래스는 또다른 조상클래스를 호출해서 결국 Object 클래스의 생성자까지 도달하면 호출은 완료된다.

  아래는 호출방법과 사용예제, 출력결과이다.

    ```java
    class Test {
    	public static void main(String[] args) {
    		Child child = new Child();
    		child.method();
    	}
    **}

    class Parent {
    	int num1;
    	
    	public Parent() {
    		num1 = 1;
    	}
    	
    	public Parent(int a) { //1번
    		num1 = a;
    	}
    }

    class Child extends Parent {
    	int num2;

    	public Child() { // 2번
    		super(5); 
    		num2 = 2;
    	}

    	void method() { //3번
    		System.out.println("num1 : " + num1); //5
    		System.out.println("num2 : " + num2); //2
    	}
    }
    ```

  마지막 Child 클래스의 method() 메서드 안에 출력 부분을 보면 num1의 값이 5인 것을 알 수 있다. 그 이유는 2번의 super(5) 때문이다. 또한 Child 클래스에서 num1을 선언하지 않아도 상속관계이기 때문에 조상 클래스의 필드에 선언된 변수를 사용할 수 있다.

  2번의 super(5)는 조상 클래스의 생성자를 호출했다. 중요한 건 매개변수에 값이 있다는 것이다. 이는 매개변수가 있는 생성자를 호출하였기 때문에 조상 클래스의 필드 변수는 매개변수가 있는 1번의 생성자에 의해 값이 대입되었다.

  만약 2번의 super() 생성자가 매개변수가 없는 기본 생성자였다면 3번을 호출하였을 때 num1의 값은 1로 출력되었을 것이다.

  또한 2번에서 super() 생성자를 호출하지 않아도 num1의 값은 1로 출력될 것이다. 그 이유는 자동으로 super()를 생성해주기 때문이다.

자료참조

자바의 정석 3rd Edition(남궁 성 저)

[http://www.tcpschool.com/java/java_inheritance_super](http://www.tcpschool.com/java/java_inheritance_super)

## 메소드 오버라이딩

## 다이나믹 메소드 디스패치 (Dynamic Method Dispatch)

## 추상 클래스

## final 키워드

## Object 클래스