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
JVM의 구성요소는 총 네 가지 구성요소를 가지고 있다.

- Class Loader

  자바에서 클래스가 로딩 되는 과정은 클래스 로더가 확장자 .class 파일의 위치를 찾아 그것을 JVM 위에 올려놓는 과정을 뜻한다.

  ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile4.uf.tistory.com%2Fimage%2F999ECB375BE900A016E768](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile4.uf.tistory.com%2Fimage%2F999ECB375BE900A016E768)

  자료 출처 : [https://engkimbs.tistory.com/606](https://engkimbs.tistory.com/606)

  클래스 로더들은 계층적 구조를 가지도록 생성이 가능하고, 각 부모 클래스 로더에서 자식들 로더를 가지는 형태로 클래스 로더를 만들 수 있다.

  위와 같은 구조를 가지고 있다.

  위의 구조 중 부트스트랩 클래스 로더와 확장 클래스 로더에 대해 좀 더 알아보자.

  - 부트스트랩 클래스 로더(Bootstrap Class Loader)

    rt.jar에 있는 JVM을 실행시키기 위한 핵심 클래스들을 로딩한다.

  - 확장 클래스 로더(Extension Class Loader)

    자바의 확장 클래스들을 로딩하는 역할을 한다. 좀 더 자세히 말하자면, classpath에 설정된 경로를 탐색하여 그 곳에 있는 클래스들을 로딩하는 역할을 한다. 즉, 사용자가 개발한 class 확장자 파일을 확장 클래스 로더가 로딩한다.

  - 로딩 요청 위임(순서)

    위의 그림자료를 통해 알 수 있는 건 하나의 구조를 이루고 있다는 것이다. 그 밑의

    > *Bootstrap ← Extension ← System ← User-defined*

    을 보면 어떠한 순서를 암시하는 듯한 느낌을 준다. 이는 Delegate Load Request의 동작 과정에서의 힌트를 얻을 수 있다.

    1. System Loader → Extension Class Loader
    2. Extension Class Loader → Bootstrap Loader

    위의 순서에서 알 수 있는 사실은 맨 위(Bootstrap Loader)에서 찾을 수 없으면 밑으로 계속 요청을 하고 마지막 System Loader에서 못 찾을시 에러를 호출한다.

- Garbage Collector

  가비지 컬렉터란 말 그대로 가비지(쓰레기) 데이터를 수집하는 것을 뜻한다. 좀 더 풀어서 말하자면, 정리되지 않은, 유효하지 않은 메모리(가비지)를 정리해 주는 것이다.

  - Garbage는 어떻게 발생하는가?

      ```java
      public class Main {
          public static void main(String[] args) {
              String url = "https://";
              url += "google.com";
              System.out.println(url); // https://google.com
          }
      }

      ```

    위의 String 타입의 url 변수는 stack에 할당되고, heap에는 타입과 정의된 내용이 할당되었다. 그리고나서 url을 덧붙이는 연산이 수행된 것을 확인할 수 있다.

    여기서 중요한건 heap 에서는 "https://"에 "google.com"을 덧붙여서 할당 되는게 아니라 "https://" 따로 "https://google.com" 따로 할당되게 된다.

    그러므로 원래 처음의 "https://"는 참조하지 않게 되고 새로운 "https://google.com"에 참조하게 된다.

    그렇게 되면 처음의 "https://" 에서는 더이상 어떠한 것도 참조하지 않게 된다.

  - 가비지 컬렉터의 실행 과정

    GC(Garbage Collector)는 먼저 Unreachable Object를 우선적으로 메모리에서 제거한다. Unreachable Object는 stack에서 도달 할 수 없는 heap 영역의 객체를 말하는 것으로, 아까의 예제의 "https://"를 보면 이해가 될 것이다.

    위와 같은 과정을 Mark and Sweep이라고도 한다. GC는 stack의 모든 변수를 스캔하면서 어떤 object를 참조하고 있는지의 과정이 Mark, 그리고나서 Mark 되어있지 않은 모든 object들을 heap에서 제거하는 일을 Sweep이라고 한다.

- Execution Engine

  Class Loader에 의해 JVM으로 load된 class 파일들을 실행하는 Runtime Module이 Execution Engine(실행 엔진)이다. 이는 두가지 실행 방식이 있다.

  1. Interpreter 방식

     바이트 코드를 한 줄씩 해석하여 실행하는 방식으로, 초기에 사용했으며 속도가 느린 단점이 있다.

  2. JIT 컴파일 방식 또는 동적 번역

     초기에 실행한 Interpreter 방식의 단점을 보완한 것이 JIT compiler 방식이다. 하지만 변환의 비용이 발생하기 때문에 Interpreter와 JIT 컴파일러 둘을 혼용하여 실행한다. JIT는 위에 있으니 참고하면 된다.

- Runtime Data Area

  Runtime Data Area는 JVM이 프로그램을 수행하기 위해 운영체제로부터 할당 받는 메모리 영역이다. 이는 다섯개의 영역으로 나뉜다.

  - PC Register

    Thread가 생성될 때마다 생기는 공간으로 Thread가 어떠한 명령을 실행하기 될지에 대한 부분을 기록한다.

    JVM은 Stacks-Base 방식으로 작동하는데, JVM은 CPU에 직접 Instruction을 수행하지 않고, Stack에서 Operand(피연산자)를 뽑아내 이를 별도의 메모리 공간에 저장하는 방식을 취하는데, 이러한 메모리 공간을 PC Register라고 한다.

  - Method Area

    프로그램 실행 중 어떤 클래스가 사용되면, JVM은 해당 클래스의 클래스파일을 읽어서 분석하여 클래스에 대한 정보(클래스 데이터)를 이곳에 저장한다. 이 때, 그 클래스의 클래스변수도 이 영역에 함께 생성된다.

  - Heap

    인스턴스가 생성되는 공간이다. 프로그램 실행 중 생성되는 인스턴스는 모두 이 곳에 생성된다. 즉, 인스턴스 변수들이 생성되는 공간이다.

  - JVM Stacks

    각 쓰레드마다 하나씩 존재하며 쓰레드가 시작될 때 할당된다. 자바 프로그램에서 추가적으로 쓰레드를 생성하지 않았다면 main 쓰레드만 존재하므로 JVM 스택도 하나이다.

    JVM 스택은 메소드를 호출할 때마다 프레임을 추가하고, 메소드가 종료되면 해당 프레임을 제거하는 동작을 수행한다.

    프레임 내부에는 로컬 변수 스택이 있는데, 기본 타입 변수와 참조 타입 변수가 추가되거나 제거된다. 변수가 이 영역에 생성되는 시점은 초기화 될 때, 즉 최초로 변수에 값이 저장될 때이다. 자바에서 초기화를 하지 않으면 안되는 이유는 변수는 선언된 블록에서만 스택에 존재하고 블록을 벗어나면 스택에서 제거되기 때문이다.

  - Native Method Stacks

    자바 외의 언어로 작성된 네이티브 코드를 위한 스택. Java Native Interface를 통해 호출하는 C/C++ 코드를 수행하기 위한 스택이다.

자료참조

[https://engkimbs.tistory.com/606](https://engkimbs.tistory.com/606)
[https://yaboong.github.io/java/2018/06/09/java-garbage-collection/](https://yaboong.github.io/java/2018/06/09/java-garbage-collection/)

[https://velog.io/@litien/가비지-컬렉터GC](https://velog.io/@litien/%EA%B0%80%EB%B9%84%EC%A7%80-%EC%BB%AC%EB%A0%89%ED%84%B0GC)

[https://smjeon.dev/etc/jvm-rda/](https://smjeon.dev/etc/jvm-rda/)[https://www.holaxprogramming.com/2013/07/16/java-jvm-runtime-data-area/](https://www.holaxprogramming.com/2013/07/16/java-jvm-runtime-data-area/)

## JDK와 JRE의 차이
- JRE

  JRE는 JVM이 자바 프로그램을 동작 시킬 때 필요한 라이브러리 파일들과 기타 파일들을 가지고 있다. 즉, 자바 애플리케이션을 실행하기 위한 최소의 실행 환경을 제공한다.

- JDK

  JDK는 JRE에서 제공하는 실행 환경 뿐만 아니라 자바 개발에 필요한 여러가지 명령어 그리고 컴파일러를 포함한다. 즉, 자바로 프로그래밍을 할 수 있고, 컴파일까지도 할 수 있다.

![https://t1.daumcdn.net/cfile/tistory/2232C53C5731E7EC17](https://t1.daumcdn.net/cfile/tistory/2232C53C5731E7EC17)
참고자료

[https://jusungpark.tistory.com/13](https://jusungpark.tistory.com/13)

[https://goodgid.github.io/Java-JDK-JRE/](https://goodgid.github.io/Java-JDK-JRE/)