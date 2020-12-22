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
    }

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
- 메소드 오버라이딩이란?

  조상 클래스로부터 상속받은 메서드의 내용을 변경하는 것을 오버라이딩이라고 한다. 조상 클래스에서 생성된 메서드를 그대로 사용 할 수 있고, 상속받는 클래스에 맞게 변경할 수도 있다. 예시로 흔히 toString() 메서드를 오버라이딩을 통해 변경하는 경우를 생각하면 된다.

    ```java
    public class TestVO {
        String name;
        int age;

    		//....

        @Override
        public String toString() {
            return "test{" +
                    "name='" + name + '\'' +
                    ", age=" + age +
                    '}';
        }
    }
    ```

  위의 코드는 DB와 JAVA간의 변환을 담당하는 DTO(Data Transfer Object)의 일부분이다. 다른 클래스에서 TestVO 클래스의 필드값을 확인하고 싶다면 toString() 메서드를 재정의 하는 방법이 대표적이다. 만약 오버라이딩을 하지 않는다면 객체의 주소값이 반환된다.

- 메소드 오버라이딩시 주의할 점
  - 이름이 같아야 한다.
  - 매개변수가 같아야 한다. (매개변수가 다르다면 오버로딩이 된다.)
  - 반환타입이 같아야 한다.
  - 접근제어자는 조상클래스의 메서드보다 좁은 범위로 변경할 수 없다.
  - 조상 클래스의 메서드보다 많은 수의 예외를 선언할 수 없다.
  - 인스턴스 메서드를 스태틱 메서드로, 또는 그 반대로 변경할 수 없다.

  정리하자면 선언부가 일치해야 한다. 다만 접근 제한자 또는 예외는 제한된 조건 하에 변경이 가능하다.

- 오버로딩(Overloading)과 오버라이딩(Overriding)

  이름이 비슷하다고 헷갈리는 경우가 있다. 하지만 각각의 특징을 이해하면 헷갈리는 부분을 해소할 수 있을 것이다.

  - 오버로딩(Overloading)

    기존에 없던 새로운 메서드를 정의하는 것을 뜻한다.

  - 오버라이딩(Overriding)

    상속받은 메서드의 내용을 재정의하는 것이다.

  - 코드 예시

      ```java
      class Parent {
          void parentMethod() {}
      }

      class Child extends parent {
          void parentMethod() {} // 오버라이딩
          void parentMethod(int n) {} // 오버로딩
      }
      ```

자료참조

자바의 정석 3rd Edition(남궁 성 저)

## 다이나믹 메소드 디스패치 (Dynamic Method Dispatch)
- 다이나믹 메소드 디스패치란?

  다이나믹 메소드 디스패치는 재정의 된 메서드에 대한 호출이 컴파일 타임이 아닌 런타임에 해석되는 프로세스이다. 오버라이드 된 메소드가 참조에 의해 호출 될 때 자바는 참조하는 객체 유형에 따라 실행할 메소드 버전을 판별한다. 만약 런타임과 컴파일타임에 대해 모른다면 간락햐게 알고 넘어가는게 이해에 큰 도움이 된다.

- 런타임과 컴파일타임
  - 런타임

    컴파일 과정을 마친 응용 프로그램이 사용자에 의해 실행되어지는 때를 의미한다.

  - 컴파일타임

    개발자에 의해 개발 언어로 소스코드가 작성되며, 컴파일 과정을 통해 컴퓨터가 인식할 수 있는 기계어 코드로 변환되어 실행 가능한 프로그램이 되는 과정을 의미한다.

  정리하자면 컴파일 타임 → 컴파일 → 런타임 순이라고 보면 된다.

- 예제 코드

    ```java
    interface Parent {
        void method();
    }

    class Child implements Parent {

        @Override
        public void method() {
            System.out.println("method overridden in child method");
        }

        public void childMethod() {
            System.out.println("starting from child method");
        }
    }

    class MainTest {
        public static void main(String[] args) {
            Parent parent = new Child();
            parent.method(); //method overridden in child method
            //parent.childMethod(); //에러
        }
    }
    ```

  Parent 인터페이스에서 메서드 하나를 생성하고 Child 클래스에서 Parent 인터페이스를implement 했다. 인터페이스는 강제성이 있기 떄문에 반드시 override를 해주었고, 재정의하면서 Child 클래스에서 재정의 했다는 내용을 기록하였다.

  그리고 MainTest 클래스에서 Parent parent = new Child(); 를 선언하고 parent.method(); 를 실행시키면 오른쪽의 주석과 같은 결과가 나온다. 하지만 Child 클래스에서 생성한 childMethod() 메서드는 객체 parent가 호출하지 못한다. 여기서 다이나믹 메소드 디스패치의 특징이 확실하게 드러난다. 특징을 확실하게 이해하려면 스태틱 메소드 디스패치에 대해 간략히 알아야한다.

  - 스태틱 메소드 디스패치(Static Method Dispatch)

    컴파일 시점에서, 컴파일러가 특정 메소드를 호출할 것이라는 것을 명확하게 알고있는 경우이다. 이는 런타임 시점이 되지 않아도 이미 결정이 되어있는 상태로, 함수를 오버로딩하여 사용하는 경우, 인자의 타입이나 리턴타입 등에 따라 어떤 메서드가 호출될 지 명확하기 때문에 이 경우 컴파일러가 명확하게 알고있는 경우에 해당한다. 예를들어,

      ```java
      Child child = new Child();
      ```

    위와 같은 코드는 스태틱 메소드 디스패치에 해당한다.

  다시 돌아와서 Parent parent = new Child(); 이 부분이 동적 메소드 디스패치에 해당이 된다. 그 이유는 Child 클래스에 선언된 childMethod() 메소드가 있기 때문이다. 객체 parent는 childMethod() 메서드에 접근할 수 없다. 이는 컴파일 시점에서 객체 parent는 바인딩 되어있는 클래스가 어떤 클래스인지 확실하게 모른다는 뜻이다. 그러므로 디스패쳐는 parent 객체 정의 부분만 보고는 확실한 판단을 내릴수가 없는 것이다. 그렇기 때문에 parent.method();는 런타임 시 호출되고, 다이나믹 메소드 디스패치에 해당한다.

자료참조

[https://riptutorial.com/ko/java/example/28573/동적-메서드-디스패치---예제-코드](https://riptutorial.com/ko/java/example/28573/%EB%8F%99%EC%A0%81-%EB%A9%94%EC%84%9C%EB%93%9C-%EB%94%94%EC%8A%A4%ED%8C%A8%EC%B9%98---%EC%98%88%EC%A0%9C-%EC%BD%94%EB%93%9C)

[https://defacto-standard.tistory.com/413](https://defacto-standard.tistory.com/413)

[https://dd-corp.tistory.com/9](https://dd-corp.tistory.com/9)

## 추상 클래스

## final 키워드

## Object 클래스