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

## 쓰레드의 우선순위

## Main 쓰레드

## 동기화

## 데드락

자료참조

자바의 정석 3rd Edition(남궁 성 저)

[https://codingdog.tistory.com/entry/java-thread-start-vs-run-어떤-차이가-있을까요](https://codingdog.tistory.com/entry/java-thread-start-vs-run-%EC%96%B4%EB%96%A4-%EC%B0%A8%EC%9D%B4%EA%B0%80-%EC%9E%88%EC%9D%84%EA%B9%8C%EC%9A%94)