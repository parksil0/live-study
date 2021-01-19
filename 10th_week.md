## Thread 클래스와 Runnable 인터페이스

쓰레드를 구현하는 방법은 Thread 클래스를 상속받는 방법과 Runnable 인터페이스를 구현하는 방법 총 두가지가 있다. 자바의 특징중 하나인 단일상속이라는 특징을 염두하면 클래스를 상속받는 방법보단 Runnable 인터페이스를 구현하는 방법이 일반적이라 볼 수 있다.

Runnable은 말 그대로 인터페이스이기 때문에 인터페이스의 특징인 일관성과 재사용성이라는 부분을 보면 Runnable 인터페이스를 사용하는 것은 객체지향적인 방법이라 생각한다.

- Thread Class

    ```java
    class MyThread extends Thread {
    	public void run() {
    		//...
    	}
    }

    class Main {
    	public static void main(String[] args) {
    		MyThread thread = new MyThread();
    		thread.start();
    	}
    }
    ```

- Runnable Interface

    ```java
    class MyThread implements Runnable {
    	public void run() {
    		//...
    	}
    }

    class Main {
    	public static void main(String[] args) {
    		Thread thread = new Thread(new MyThread());
    		thread.start();
    	}
    }
    ```

  Runnable 인터페이스로 구현한 경우와 Thread 클래스로 구현한 경우의 객체 선언 방법이 다르다. Runnable 인터페이스의 구현 경우,  좌항에서는 Thread 타입의 변수 thread를, 우항에서는 새로운 생성자에 Runnable 인터페이스를 구현한 MyThread 클래스를 매개변수로 선언했다. 위처럼 매개변수에 MyThread클래스를 담으면 상속을 통해 run()을 오버라이딩 하지 않고도 외부로부터 run() 메서드를 제공받을 수 있게 된다.

- start(), run()

  쓰레드를 실행시킬 때 run() 메서드가 아닌 start()메서드를 호출해야한다. 그 이유는 run()메서드는 그저 클래스에 선언된 메서드를 호출하기 때문에 쓰레드의 스케줄링과 관련된 메서드를 실행시켜도 원하는대로 동작하지 않을 가능성이 있다.

    ```java
    public class Main {
        public static void main(String[] args) throws IOException {

            Thread thread1 = new Thread(new MyThread1());
            thread1.run();
            thread1.run();
            thread1.run();
        }
    }

    class MyThread1 implements Runnable {
        @Override
        public void run() {
            System.out.println(Thread.currentThread().getName());
        }
    }

    /*
    	출력결과
    	main
    	main
    	main

    */
    ```

  위는 main 메서드에서 thread1.run() 메서드를 실행시켰을 때의 실행결과이다. 실행되는 쓰레드의 이름이 모두 같은 main 쓰레드이다. 이는 새로운 call stack 을 할당받지 않고 말 그대로 main 쓰레드에서 run()메서드가 실행된 것 뿐이다.

  반면에 start() 메서드는 새로운 쓰레드가 작업을 실행하는데에 필요한 call stack을 생성한 다음 run() 메서드를 호출해서, 생성된 call stack에 run()메서드가 첫 번째로 올라가게 한다. 이는 쓰레드에게 독립적인 작업을 수행하기 위해 자신만의 call stack을 필요로 하기 때문에, 새로운 쓰레드를 생성하고 실행시킬 대마다 새로운 call stack이 생성되고, 쓰레드가 종료되면 작업에 사용된 call stack은 소멸된다.

    ```java
    public class Main {
        public static void main(String[] args) throws IOException {

            Thread thread1 = new Thread(new MyThread1());
            thread1.start();
        }
    }

    class MyThread1 implements Runnable {
        @Override
        public void run() {
            System.out.println(Thread.currentThread().getName());
        }
    }

    /*
    	출력결과
    	Thread-0
    */
    ```

  위의 출력결과를 통해 새로운 call stack을 생성하고 그 뒤에 run() 메서드를 호출한 것을 확인할 수 있다.

  그리고 한 가지 알아야 하는 게, 한번 실행이 종료가 된 쓰레드는 다시 실행할 수 없다. 즉, start()메서드는 단 한번만 호출이 가능하다. 만약 두번 이상 호출하게 되면 IllegalThreadStateException예외가 호출된다.

  당연히 run() 메서드는 여러번 호출해도 문제가 없다. 이유는 말 그대로 클래스의 메서드만 호출되었기 때문이다.

## 쓰레드의 상태

- 쓰레드의 상태

  아래는 쓰래드의 생성부터 소멸까지의 과정을 다섯가지로 분류하였다. 아래는 다섯가지 상태의 간략한 특징들을 나열해보았다.

  추가로, 쓰레드의 상태를 확인하고 싶다면, Thread의 getState() 메서드를 통해 확인이 가능하다.
  
  |상태|설명|
  |:---|:---|
  |NEW(생성)|쓰레드가 생성되고 아직 start()가 호출되지 않은 상태|
  |RUNNABLE(실행 대기)|실행 중 또는 실행 가능한 상태|
  |BLOCKED(일시정지)|동기화블럭에 의해서 일시정지된 상태(lock이 풀릴 때까지 기다리는 상태)|
  |WAITING<br/> TIMED_WAITING(일시정지)|쓰레드의 작업이 종료되지는 않았지만 실행가능하지 않은(unrunnable) 일시정지 상태. TIME_WAITING은 일시정지시간이 지정된 경우를 의미한다.|
  |TERMINATED(소멸)|쓰레드의 작업이 종료된 상태|


- 쓰레드의 상태 제어 메서드

  쓰레드 프로그래밍이 어려운 이유는 동기화와 상태를 제어하는 일이 까다롭기 때문이다. 효율적으로 쓰레드를 관리하기 위해서 쓰레드의 상태를 제어하는 것이 중요한데, 상태를 제어하는 메서드에 대해 알아보자
  
  |메서드|설명|
  |:---|:---|
  |static void sleep(long millis)<br/> static void sleep(long millis, int nanos)|지정된 시간(천분의 일초 단위)동안 쓰레드를 일시정지시킨다. 지정한 시간이 지나고 나면, 자동적으로 다시 실행대기상태가 된다.|
  |void join()<br/> void join(long millis)<br/> void join(long millis, int nanos)|지정된 시간동안 쓰레드가 실행되도록 한다. 지정된 시간이 지나거나 작업이 종료되면 join()메서드를 호출한 쓰레드로 다시 돌아와 실행을 계속한다.|
  |void interrupt()|sleep(), join()에 의해 일시정지상태인 쓰레드를 깨워서 실행대기상태로 만든다. 해당 쓰레드에서는 InterruptedException이 발생함으로써 일시정지상태를 벗어나게 된다.|
  |void stop()|쓰레드를 즉시 종료시킨다.|
  |void suspend()|쓰레드를 일시정지시킨다. resume()메서드를 호출하면 다시 실행대기상태가 된다.|
  |void resume()|suspend()에 의해 일시정지상태에 있는 쓰레드를 실행대기상태로 만든다.|
  |static void yield()|실행 중에 자신에게 주어진 실행시간을 다른 쓰레드에게 양보(yield)하고, 자신을 실행대기상태가 된다.|

- 쓰레드의 생성부터 소멸까지의 과정

  과정을 담고 있지만, 반드시 과정대로 쓰레드가 수행되진 않는다.

  ![자바 쓰레드 생명주기 및 상태](https://howtodoinjava.com/wp-content/uploads/2016/04/Java-Thraed-Life-Cycle-States.jpg "자바 쓰레드 생명주기 및 상태") 
  
  *위의 사진은 아래의 글을 참고하며 볼때 이해하기 쉽도록 첨부한 자료입니다.*
  
  1. NEW

     쓰레드를 생성하고 start() 메서드를 호출하면 바로 실행되는 것이 아니라, 실행대기열에 저장되어 자신의 차례가 될 때까지 기다려야한다. 실행대기열은 큐(queue) 구조로 되어있어, 순서대로 쓰레드가 실행된다.

  2. RUNNABLE

     실행대기상태에 있다가 자신의 차례가 되면 실행상태가 된다. 만약 주어진 실행시간이 다 되거나 yield() 메서드를 만난다면 다시 실행 대기 상태가 되고, 다음 차례의 쓰레드가 실행된다.

  3. WAITING, BLOCKED

     실행 중 suspend(), sleep(), wait(), join(), I/O block에 의해 일시정지상태가 될 수 있다. (I/O block은 입출력 작업에서 발생되는 지연상태를 의미한다. 일례로, 사용자의 입력대기상태로 예시를 들 수 있는데, 입력을 마치면 실행대기상태가 된다.)

     지정된 일시정지시간이 다 되거나(time-out), notify(), resume(), interrupt() 메서드가 호출되면 일시정지상태를 벗어나 다시 실행대기열에 저장되어 자신의 차례를 기다리게 된다.

  4. TERMINATED

     실행을 모두 마치거나 stop() 메서드가 호출되면 쓰레드는 소멸된다.

## 쓰레드의 우선순위

## Main 쓰레드

## 동기화

## 데드락

자료참조

자바의 정석 3rd Edition(남궁 성 저)

[https://codingdog.tistory.com/entry/java-thread-start-vs-run-어떤-차이가-있을까요](https://codingdog.tistory.com/entry/java-thread-start-vs-run-%EC%96%B4%EB%96%A4-%EC%B0%A8%EC%9D%B4%EA%B0%80-%EC%9E%88%EC%9D%84%EA%B9%8C%EC%9A%94)