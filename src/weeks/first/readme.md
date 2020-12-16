# 1주차

## JVM이란 무엇인가

- JVM이란?

  JVM(Java Virtual Machine)은 말 그대로 자바 가상 머신으로, 자바 바이트코드를 실행할 수 있는 주체이다. 자바 바이트코드는 플랫폼에 독립적이며, 모든 자바 가상 머신은 자바 가상 머신 규격에 정의된 대로 자바 바이트코드를 실행한다. 따라서 표준 자바 API까지 동일한 동작을 하도록 구현한 상태에서는 이론적으로 모든 자바 프로그램은 CPU나 운영 체제의 종류와 무관하게 동일하게 동작할 것을 보장한다.

  이는 어느 운영체제 상에서도 실행될 수 있게 하는 것과 프로그램 메모리를 관리하고 최적화하는 것을 뜻한다.

  참고 자료

  [https://ko.wikipedia.org/wiki/자바_가상_머신](https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94_%EA%B0%80%EC%83%81_%EB%A8%B8%EC%8B%A0)

  [https://www.itworld.co.kr/news/110837](https://www.itworld.co.kr/news/110837)

## 컴파일 하는 방법

- 컴파일이란?

  컴파일은 개발자가 컴퓨터에게 명령을 내리는데, 그 명령은 0과 1(이진코드)로 이해하고 실행한다. 하지만 개발자는 0과 1로만 명령을 내리기가 어렵기 때문에 정해놓은 규칙에 맞게 명령문을 적고, 컴퓨터가 이해할 수 있도록 이진코드로 변환하는데, 그 사이에서 번역을 해주는 도구를 컴파일러라고한다.

- 컴파일 하는 방법(Java)
    1. 먼저 오라클에 들어가서 JDK(Java Development Kit, 자바 개발 킷)을 다운받는다. [다운로드 링크](https://www.oracle.com/kr/java/technologies/javase-downloads.html)
    2. 환경 변수 설정을 한다.( 시스템 변수에 Path로 jdk설치경로를 설정)
    3. 메모장에 확장자명을 java로 하고 밑의 코드를 적는다.(파일 명은 Hello.java)

        ```java
        Class Hello {
        	public static void main(String[] args) {
        		System.out.println("Hello World!");
        	}
        }
        ```

    4. cmd로 들어가 위의 .java 파일의 경로로 들어간 다음 아래의 명령어를 입력한다.

        ```java
        javac Hello.java
        ```

       명령어를 입력하면 확장자 명이 class인 파일이 하나 생성이 되는데, 이는 소스 코드인 .java 파일을 컴파일러를 통해 바이트 코드로 변환한 파일이다.

    5. 마지막으로 아래의 코드를 입력한다.

        ```java
        java Hello // Hello World!
        ```

자료참고

[https://m.blog.naver.com/white_cap/221003190571](https://m.blog.naver.com/white_cap/221003190571)

[https://zerodark.tistory.com/14](https://zerodark.tistory.com/14)

## 실행하는 방법

- 실행 도구(Intellij) 다운로드
    1. [링크](https://www.jetbrains.com/idea/download/#section=windows)를 통해 Ultimate(유료), Community(무료) 둘중 선택해서 고르면 된다.
    2. 각자의 맞는 운영체제와 환경설정을 맞추어 설치한다.
    3. 위에서 다운받은 jdk 버전에 맞게 설정한다.
    4. 시작한 후 src에 java을 추가하여 시작한다.

## 바이트코드란 무엇인가

- 바이트 코드란 JVM이 이해할 수 있는 언어로 변환된 자바 소스 코드를 의미한다. 말 그대로 명령어의 크기가 1바이트라서 바이트 코드라고 불리기도 한다.

  위의 *컴파일이란?* 의 부분에서 잠시 설명했듯, 컴퓨터(CPU)가 이해할 수 있도록 변환되는데, 이 변환된 것(.class)과 안 된 것(.java)의 차이가 바이트 코드로 바뀌었는지에 대한 차이이다.

참조 자료

[http://tcpschool.com/java/java_intro_programming](http://tcpschool.com/java/java_intro_programming)

## JIT 컴파일러란 무엇이며 어떻게 동작하는지

- JIT 컴파일러란?

  JIT(just-in-time) compiler, JIT 컴파일러는 말 그대로 실제 실행하는 시점에 번역하는 컴파일 기법이다.

  위에서 잠깐 설명했듯 JVM이 개발자가 입력한 코드를 바이트 코드로 변환하여 컴퓨터가 이해할 수 있도록 변환한다고 했었다. 하지만 바이트 코드와 CPU 사이에 JIT 컴파일러가 컴퓨터 프로세스로 직접 보낼 수 있는 명령어로 바꾸어준다. 그래야만 컴퓨터가 읽을 수 있는 형태로 해석이 되는데, 이는 interpreter를 통해 해석이 된다.

  ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbFV3Wt%2FbtqG68RvEaq%2FdUMj5kiqu5Zb0iEIxTGnCK%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbFV3Wt%2FbtqG68RvEaq%2FdUMj5kiqu5Zb0iEIxTGnCK%2Fimg.png)

  자료 출처 : [https://heewon26.tistory.com/207](https://heewon26.tistory.com/207)

- 왜 JIT를 통해 한 번 더 변환이 되는걸까?

  JVM이 동일한 바이트 코드를 반복적으로 해석하다보면 실행 속도에 영향을 미친다. 하지만 JIT 컴파일러를 사용한다면 변환 프로세스를 초래하는 것과는 반대로 원시코드를 실행할 수 있기 때문이다. 게다가 반복되는 내용은 인터프리트 방식으로 기계어 코드를 생성하면서 그 코드를 캐싱하여 같은 함수가 여러 번 불릴 때 매 번 기계어 코드를 생성하는 것을 방지하기도 한다.

- 조금 더 자세히 설명하자면..

  JIT는 동적 컴파일을 한다. 동적 컴파일이란 JVM이 생성한 바이트 코드를 런타임에 바로 기계어로 변환하는 것을 뜻한다. JIT 코드는 일반적인 인터프리터 언어에 비해 좋은 성능을 낸다. 이로인해 다양한 플랫폼에 맞게 컴파일을 할 수 있는 자바의 환경에서는 JIT 컴파일러는 잘 맞는 컴파일러라고 볼 수 있다.

  이러한 프로세스로 알 수 있는 것은, JVM의 바이트 코드 변환과 JIT 컴파일러의 빠른 기계어 번환을 통해 정적 컴파일러 만큼 빠른 성능을 기대할 수 있다는 것이다.

자료참조

[http://tcpschool.com/java/java_intro_programming](http://tcpschool.com/java/java_intro_programming)

[https://ko.wikipedia.org/wiki/JIT_컴파일](https://ko.wikipedia.org/wiki/JIT_%EC%BB%B4%ED%8C%8C%EC%9D%BC)

[https://aroundck.tistory.com/1949](https://aroundck.tistory.com/1949)

[https://heewon26.tistory.com/207](https://heewon26.tistory.com/207)

## JVM의 구성 요소

## JDK와 JRE의 차이