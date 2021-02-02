## 애노테이션 정의하는 방법

- 애노테이션 정의

  애노테이션을 정의하는 법에 대해 알아보자. 먼저 밑의 예시와 함께 설명하려 한다.

    ```java

    @Retention(RetentionPolicy.RUNTIME)
    @interface Introduce {
        String name() default "user";
        int age() default 0;
    }
    ```

  애노테이션을 정의하는 방법은 위를 보면 알 수 있듯 '@interface 애노테이션 이름 {}'과 같이 정의할 수 있다.

    ```java
    @interface 애노테이션 {
    	
    }
    ```

  구현부를 보면 '타입 이름()'과 같은 형태로 선언되어있는 것을 확인 할 수 있다. 이를 애노테이션의 요소(element)라고 하며, 위의 예시에는 총 두 가지(String name(), int age())로 선언되어있다. 또한 배열로도 선언이 가능하다

    ```java
    @interface 애노테이션 {
    	타입[] 이름();
    	enum 이름();
    }
    ```

  요소를 선언 한 다음의 키워드 'default'는 기본값으로, 기본값이 있는 요소는 애노테이션을 적용할 때 값을 지정하지 않으면 기본값이 사용된다.

    ```java
    @interface 애노테이션 {
    	//타입 이름() default 타입에 맞는 값
    	int age() default 20;
    }
    ```

  바로 위의 예시에서는 기본값을 20으로 지정한 요소이다.

  이외에 애노테이션 요소를 선언할 때 주의사항에 대해 조금 더 알아보자

    - 요소의 타입은 기본형, String, enum, 애노테이션, Class만 허용된다.
    - () 안에 매개변수를 선언할 수 없다.
    - 예외를 선언할 수 없다.
    - 요소를 타입 매개변수로 정의할 수 없다.
    - 애노테이션은 상속이 허용되지 않는다.

      아래는 주의사항을 코드로 나열한 것이다.

        ```java
        @interface precautions extends Annotation{ // 상속이 허용 안됨.
        	EnumSet set() //에러. 기본형, String, enum, 애노테이션, Class 이외의 것이 타입으로 들어감
        	String add(int number1, int number2) // 에러. 매개변수 선언됐음.
        	String devide() throws ArithmeticException; //에러. 예외 선언 안됨.
        	ArrayList<T> list() //에러. 타입 매개변수 정의됨.
        }
        ```

  마지막으로 @Retention은 밑의 소주제에서 따로 다룰 것이다.

- 애노테이션 출력

  다음은 메인 메서드 안에서 어떻게 애노테이션을 정의했는지 알아보려한다.

    ```java
    import java.lang.annotation.Retention;
    import java.lang.annotation.RetentionPolicy;

    @Introduce(name = "Kimbob", age = 20)
    public class Test {
        public static void main(String[] args) {
            Class<Test> testClass = Test.class;
            Introduce intro = (Introduce)testClass.getAnnotation(Introduce.class);

            System.out.println(intro.name());
        }
    }

    /*
    	출력결과
    	Kimbob
    */
    ```

  클래스 위쪽을 보면 맨 처음에 정의한 애노테이션 'Introduce'를 볼 수 있고, 괄호 안에는 요소의 값을 지정하고 있다. 'Test.class'는 클래스 객체를 의미하는 리터럴이다. 클래스에 대한 정보가 담긴 객체를 생성하는데 이 객체를 클래스 객체라고 한다. 갑자기 쌩뚱맞게 클래스 객체에 대해 설명하는가 라고 의문할 수 있겠지만, 클래스 객체에서는 애노테이션에 대한 정보가 포함되어있기 때문에 앞서 잠시 설명한 것이다. 살짝 더 덧붙이자면, 클래스 객체에는 해당 클래스에 대한 모든 정보를 가지고있다.

  위의 클래스 객체에 대해 알았다면, 클래스 객체로 하여금 getAnnotation()이라는 메서드가 코드의 흐름상 어떠한 기능일지에 대해 감을 잡을 것이다.

  ![images/img_14.png](images/img_14.png)

  위는 Class.java의 getAnnotation()메소드에 대한 정보이다.

  다시 위의 코드로 돌아가서 Introduce 타입의 객체 intro를 선언한 것을 알 수 있고, 이 객체로 하여 출력문을 통해 출력된 것을 확인할 수 있다.

## **@retention**

## **@target**

## **@document**

## 애노테이션 프로세서

자료 참조

자바의 정석 3rd Edition(남궁 성 저)