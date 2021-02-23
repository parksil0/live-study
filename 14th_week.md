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

## 제네릭 메소드 만들기

## Erasure

자료참조

자바의 정석 3rd Edition(남궁 성 저)