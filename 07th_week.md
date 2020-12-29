## package 키워드

- 패키지란?

  패키지는 클래스 또는 인터페이스의 묶음으로, 어떠한 관련이 있는 것들 끼리 그룹 단위로 묶어 놓음으로 효율적으로 관리를 할 수 있도록 해준다. 실제로는 클래스의 풀 네임은 패키지명을 포함한 것이다. 예를들어 String 클래스는 java.lang.String이다.

- 패키지의 특징

  같은 이름의 클래스일 지라도 패키지가 다르다면 상관없어, 이름이 충돌하는 것을 피할 수 있다. 그 이유는 클래스의 풀 네임은 패키지명까지 포함하기 때문이다.

- 패키지 선언 방법

  패키지 선언 방법은 클래스 파일의 제일 상단에 선언해야한다. 그리고 패키지명은 소문자로 명명하는 것을 원칙으로 한다. 패키지는 점(.)을 구분자로 하여 계층구조로 작성해야 한다.

    ```java
    package me.whiteship.Main;
    ```

  위의 예시는 me.whiteship 패키지의 Main 클래스를 뜻한다.

  예외로 상단에 선언을 안하는 경우가 있는데, 패키지 이름이 없는 경우에 해당한다.

자료참조

자바의 정석 3rd Edition(남궁 성 저)

## import 키워드
- import란?

  다른 패키지의 클래스를 사용하려면 패키지명이 포함된 클래스 이름을 사용해야 한다. 하지만 매번 패키지명을 붙여 작성하기엔 매우 불편하다. 이를 위해 import문으로 사용하고자 하는 클래스의 패키지를 미리 명시하기만 하면 클래스이름에서 패키지명은 생략이 가능하다.

  소스코드를 컴파일 할 때 컴파일러는 import문을 통해 소스파일에 사용된 클래스들의 패키지를 알아 낸 다음, 모든 클래스 이름 앞에 패키지명을 붙여준다.

- import문 사용 방법

  import를 선언할 때 클래스의 상단에 위치해야 한다. import선언을 하고난 다음에야 패키지 명을 생략하고 클래스 이름으로만 호출할 수 있다.

    ```java
    package me.whiteship // 1번

    import java.util.Arrays; // 2번

    public class Test {

        public static void main(String[] args) {
            String heights = "100,200,300,400,500";
            String[] arr = heights.split(",");

            System.out.println(Arrays.toString(arr)); // [100, 200, 300, 400, 500]

        }
    }
    ```

  1번은 패키지의 선언이다. 위의 package 키워드 부분을 보면 이해할 수 있다.

  2번은 import를 선언하였다. 선언할 때에는 패키지명 + 클래스 명 임을 알 수 있다. 만약 같은 패키지의 클래스가 두개 이상이라면 클래스 명을 입력하는 대신 '*' 로 하여 그 패키지의 모든 클래스를 import할 수도 있다.

    ```java
    import java.util.Arrays;
    import java.util.Date;
    ```

  위의 코드를

    ```java
    import java.util.*;
    ```

  위와 같이 사용 가능하다.

  다만 반드시 패키지명은 끝까지 입력해야한다. 클래스 명 대신에 '*' 입력이 가능한 것이지, 패키지 명 마저 '*'를 입력하여 사용할 수는 없다.

- static import

  보통 클래스의 static 메소드를 사용할 때에는 '클래스명.static 메소드' 와 같이 사용한다. static 또한 import가 가능하다.

    ```java
    import static java.lang.Math.random;

    public class test {

        public static void main(String[] args) {
    			System.out.println( (ramdom() * 10) + 1 ); // 1 ~ 10 사이의 수를 출력한다.
    		}
    }
    ```

  원래라면 Math.random() 이라고 입력해야 하지만, static import를 선언했기 때문에 위처럼 사용할 수 있다. 만약 특정 static 메소드를 자주 사용해야 하는 경우라면 import를 하는 것이 더 간략한 코드를 짤 수 있다.

자료참조

자바의 정석 3rd Edition(남궁 성 저)

## 클래스패스
- 클래스패스란?

  JVM이 시작될 때 JVM의 클래스 로더는 클래스패스 환경 변수를 호출한다. 그래서 환경 변수에 설정되어있는 디렉토리가 호출되면 그 디렉토리에 있는 클래스들을 먼저 JVM에 로드한다. 그러므로 클래스패스 환경 변수에는 필드 클래스들이 위치한 디렉토리를 등록하도록 한다.

자료참조

[https://blog.opid.kr/62](https://blog.opid.kr/62)

## CLASSPATH 환경변수
- 클래스패스 환경변수 추가

  제어판 → 시스템 → 고급 시스템 설정 → 환경변수로 들어가면 아래와 같은 화면이 보일 것이다.

  ![https://t1.daumcdn.net/cfile/tistory/2213D74253DB3DCC06](https://t1.daumcdn.net/cfile/tistory/2213D74253DB3DCC06)

  출처 : [https://blog.opid.kr/62](https://blog.opid.kr/62)

  새로 만들기를 클릭한 후 변수 이름은 'CLASSPATH'로, 값은 설치된 경로의 lib를 경로로 설정한다.

자료참조

[https://blog.opid.kr/62](https://blog.opid.kr/62)
## classpath 옵션
- 클래스패스 옵션이란?

  컴파일러가 컴파일 하기 위해 필요로 하는 클래스 파일들을 찾기 위해 컴파일 시 경로를 지정해주는 옵션이다.

- 일반적인 옵션 사용 방법

    ```java
    javac -classpath /*클래스파일 경로*/ /*자바파일 경로*/
    ```

  자바파일을 클래스파일로 컴파일시키는 명령문이다. 자바파일의 경로가 'C:Java'에 있고, 클래스파일로 변환된 파일을 'C:Class'로 설정한다면,

    ```java
    javac -cp C:Class C:Java
    ```

  위와같이 입력할 수 있다. 또한 '-classpath'를 'cp'로 줄여서 사용 가능하다.

  그리고, 여기서 주의해야 할 점은 각 경로 사이에 한 칸의 공백이 있다는 점이다.

- 환경변수를 이용한 사용 방법

    ```java
    javac -cp ".;lib" Test.java
    ```

  위는 클래스패스를 이용하여 자바파일을 클래스파일로 컴파일하는 명령어이다. 가운데 ".;lib"는 위에서 클래스패스 변수 값으로 등록했던 경로이다.

    ```java
    java -cp ".;lib" Test
    ```

  위의 코드는 클래스패스에서 Test라는 클래스파일을 실행하는 명령어이다.

  위의 코드 중간에 경로 구분자인 세미콜론(';')이 있는 것을 볼 수 있다. 이는 윈도우에서는 세미콜론이 쓰이며, 리눅스와 맥에서는 세미콜론이 아닌 콜론(':')을 사용한다는 차이점을 알아두어야 한다.

자료참조

[https://velog.io/@welloff_jj/200913TIL](https://velog.io/@welloff_jj/200913TIL)

[https://payoff.tistory.com/401](https://payoff.tistory.com/401)

## 접근지시자

- 접근 지시자란?

  접근 지시자는 멤버 또는 클래스에 사용되어, 해당하는 멤버 도는 클래스를 외부에서 접근하지 못하도록 지시하는 역할을 한다.
  public, protected, default, private 총 네개의 접근지시자가 있다. 이중 default는 생략이 가능하다.
  ![https://t1.daumcdn.net/cfile/tistory/11791C404E74C2B719](https://t1.daumcdn.net/cfile/tistory/11791C404E74C2B719)
  자료 출처 : [https://t1.daumcdn.net/cfile/tistory/11791C404E74C2B719](https://t1.daumcdn.net/cfile/tistory/11791C404E74C2B719)

  - public

    접근 제한이 없음

  - protected

    같은 패키지 내에서, 다른 패키지의 자손 클래스에서 접근 가능

  - default

    같은 패키지 내에서 접근 가능

  - private

    같은 클래스 내에서 접근 가능
  
    |제어자|같은 클래스|같은 패키지|자손 클래스|전체|
    |:------|:---|:---|:---|:---|
    |public|O|O|O|O|
    |protected|O|O|O|X|
    |default|O|O|X|X|
    |private|O|X|X|X|
- 대상에 따른 사용 가능한 접근 지시자
  
  |대상|사용가능한 접근 제어자|
  |:------|:---|
  |클래스|public, default|
  |메서드|public, protected, default, private|
  |멤버변수|public, protected, default, private|
  |지역변수|없음|
    
  

자료참조

자바의 정석 3rd Edition(남궁 성 저)