## 선택문

- 선택문이란?

  선택문이란 조건에 따라 그 조건에 해당하는 부분만 실행하는 것으로, switch문이 있다.

- switch

  스위치는 단 하나의 조건식으로 많은 경우의 수를 처리할 수 있고, 표현도 간결하므로 알아보기 쉽다. 그래서 처리할 경우의 수가 많은 경우에는 if문보다 switch문으로 작성하는 것이 좋다. 다만 switch문은 제약조건이 있기 때문에 경우의 수가 많아도 어쩔 수 없이 if문으로 작성해야 하는 경우가 있다.

- switch문의 순서
    1. 조건식을 계산한다.
    2. 조건식의 결과와 일치하는 case문으로 이동한다.
    3. 이후의 문장들을 수행한다.
    4. break문이나 switch문의 끝을 만나면 switch문 전체를 빠져나간다.

    ```java
    switch(조건식) { //1.
    	case 값1 : //2.
    		//조건식의 결과가 값1과 같을 경우 수행될 문장들 //3.
    		break;//4.
    	case 값2 :  //2.
    		//조건식의 결과가 값2과 같을 경우 수행될 문장들 //3.
    		break; //4.
    	default : //2.
    		//조건식의 결과와 일차하는 case문이 없을 때 수행될 문장들 //3.
    }
    ```

  만약 조건식과 일치하는 case문이 하나도 없을 경우 default문으로 이동한다. default문은 if문에서 else와 같은 역할이라고 보면 된다. 보통 default문은 마지막이기 때문에 break를 생략한다.

- switch문 작성시 주의사항

  switch문의 조건식의 결과값이 반드시 정수이어야 하며, 이 값과 일치하는 case문으로 이동하기 때문에 case문의 값 역시 정수이어야 한다. 그리고 중복되지 않아야 한다. 그 이유는 같은 값이면 어디로 이동해야 하는지 알 수 없기 때문이다.

  게다가 case문의 값은 반드시 상수이여야 한다. 변수나 실수, 문자열은 case문의 값으로 사용할 수 없다.

## 반복문

- 반복문이란?

  반복문이란 어떤 작업이 반복적으로 수행되도록 할 때 사용되며, 반복문의 종류로는 크게 for문, while문이 있다

- for문

  for문은 반복 횟수를 알고 있을 때 적합하다.

    ```java
    /*
    	for(초기화;조건식;증감식) {
    		수행될 문장
    	}
    */
    for(int i = 1; i <= 5; i++) {
    	System.out.println(i);
    }

    /*
    	출력결과
    	1
    	2
    	3
    	4
    	5
    */
    ```

  for문의 소괄호 안에는 세미콜론을 기준으로 초기화, 조건식, 증감식을 입력한다. 그 다음 중괄호 안에는 수행 할 문장을 입력한다.

    - 초기화

      반복문에 사용될 변수를 초기화 하는 부분이며 처음에 한번만 수행된다. 보통 변수 하나로 for문을 제어하지만, 둘 이상의 변수가 필요할 때는 콤마를 구분자로 변수를 초기화하면 된다. 단, 두 변수의 타입은 같아야한다.

        ```java
        for(int i = 1, j = 0; i <= 10; i++) {...}
        ```

    - 조건식

      조건식의 값이 true이면 반복을 계속하고, false이면 반복을 중단하고 for문을 벗어난다.

    - 증감식

      반복문을 제어하는 변수의 값을 증가 또는 감소시키는 식이다.

  위의 코드를 해석하자면, i는 1이고 i가 5보다 작거나 같은지(true)를 확인하고, i를 연산 한 다음 문장을 수행한다. 그러다가 중간에 조건식이 false가 되면 for문은 종료된다.

- 향상된 for문

  for문의 새로운 문법으로 아래의 코드를 먼저 보자면,

    ```java
    /*
    	for ( 타입 변수명 : 배열 또는 컬렉션 ) {
    		//반복할 문장
    	}
    */
    int[] arr = {1,2,3,4,5};
    for(int temp : arr) {
    	System.out.println(temp);
    }

    /*
    	출력결과
    	1
    	2
    	3
    	4
    	5
    */

    ```

  위의 문장에서 타입은 배열 또는 컬렉션의 요소의 타입이어야 한다. 배열 또는 컬렉션에 저장된 값이 매 반복마다 하나씩 순서대로 읽혀서 변수에 저장된다. 그리고 반복문의 괄호 내에는 이 변수를 사용해서 코드를 작성한다.

  하지만 향상된 for문은 일반적인 for문과는 달리 배열이나 컬렉션에 저장된 요소들을 읽어오는 용도로만 사용할 수 있다는 제약이 있다.

- while

  for문에 비해 while문은 구조가 간단하다. if문처럼 조건식과 블럭으로만 이루어져 있다. 하지만 if문과 달리 while문은 조건식이 true이면 계속 반복하고, 거짓이되면 while문을 종료한다.

    ```java
    /*
    	while(조건식) {
    		반복할 문장
    	}
    */

    int num = 1;
    while(num <= 3) {
    	System.out.print(num + " ");
    	num++;
    }

    //출력결과
    //1 2 3 
    ```

  조건식은 위의 for문의 조건식과 마찬가지로 true일때에만 반복하고, false가 될 때에는 while문을 종료한다.

- do-while문

  do-while문은 while문의 변형으로 기본적인 구조는 while문과 같으나 조건식과 블럭의 순서를 바꾸어놓은 것이다. 그래서 while문과 반대로 블럭을 먼저 수행한 후에 조건식을 평가한다.

  while문과의 차이점이라면 while문은 한번도 수행되지 않을 수 있지만, do-while문은 최소 한번은 수행 될 것을 보장한다.

    ```java
    public class Main {
        public static void main(String[] args) {
            int randomNum = (int)(Math.random() * 10) + 1;
            int input = 0;

            Scanner sc = new Scanner(System.in);

            do{
                System.out.print("숫자를 입력하세요 : ");
                input = Integer.parseInt(sc.nextLine());

                if(input != randomNum) {
                    System.out.println("틀렸습니다.");
                }

            } while(!(input == randomNum));

            System.out.println("정답입니다.");
        }
    }
    ```

  먼저 do 안의 구현부부터 시작하고, while문에서의 조건식이 true가 아니라면 다시 do로 올라가 반복하는 구조이다. 위는 랜덤 숫자를 저장한 randomNum의 숫자를 맞추는 코드로, while문의 조건식을 보면 같은지에 ! 연산자를 붙여 false를 유도하여 do-while문을 종료하도록 코드를 짰다.

- break

  break문이란 자신이 포함된 가장 가까운 반복문을 벗어난다. 주로 if문과 함께 사용되어 특정 조건을 만족하면 반복문을 벗어나도록 한다.

    ```java
    while(true) {
    	if(num < 100) {
    		break;
    	}
    	//...
    }
    ```

  위의 코드에서 if문이 true가 되면 break문을 수행되어 가장 가까운 while문을 종료시킨다.

- continue

  continue문은 반복문 내에서만 사용될 수 있으며, 반복이 진행되는 도중에 continue문을 만나면 반복믄의 끝으로 이동하여 다음 반복으로 넘어간다. for문의 경우 증감식으로 이동하며, while문과 do-while문의 경우 조건식으로 이동한다.

  주로 if문과 함께 사용되어 특정 조건을 만족하는 경우에 continue문 이후의 문장들을 수행하지 않고 다음 반복으로 넘어가서 계속 진행하도록 한다.

    ```java
    while(true) {
    	if(num < 100) {
    		continue;
    	}
    	//...
    }
    ```

  위의 코드의 경우 if문의 true가 되면 continue문을 수행하는데, 그 밑의 코드들은 수행하지 않고 다음 반복으로 넘어가게 된다.

# **과제 (옵션)**

## **과제 0. JUnit 5 학습하세요.**

- 인텔리J, 이클립스, VS Code에서 JUnit 5로 테스트 코드 작성하는 방법에 익숙해 질 것.
- 이미 JUnit 알고 계신분들은 다른 것 아무거나!
- [더 자바, 테스트](https://www.inflearn.com/course/the-java-application-test?inst=86d1fbb8) 강의도 있으니 참고하세요~

## **과제 1. live-study 대시 보드를 만드는 코드를 작성하세요.**

- 깃헙 이슈 1번부터 18번까지 댓글을 순회하며 댓글을 남긴 사용자를 체크 할 것.
- 참여율을 계산하세요. 총 18회에 중에 몇 %를 참여했는지 소숫점 두자리가지 보여줄 것.
- [Github 자바 라이브러리](https://github-api.kohsuke.org/)를 사용하면 편리합니다.
- 깃헙 API를 익명으로 호출하는데 제한이 있기 때문에 본인의 깃헙 프로젝트에 이슈를 만들고 테스트를 하시면 더 자주 테스트할 수 있습니다.

## **과제 2. LinkedList를 구현하세요.**

- LinkedList에 대해 공부하세요.
- 정수를 저장하는 ListNode 클래스를 구현하세요.
- ListNode add(ListNode head, ListNode nodeToAdd, int position)를 구현하세요.
- ListNode remove(ListNode head, int positionToRemove)를 구현하세요.
- boolean contains(ListNode head, ListNode nodeTocheck)를 구현하세요.

## **과제 3. Stack을 구현하세요.**

- int 배열을 사용해서 정수를 저장하는 Stack을 구현하세요.
- void push(int data)를 구현하세요.
- int pop()을 구현하세요.

## **과제 4. 앞서 만든 ListNode를 사용해서 Stack을 구현하세요.**

- ListNode head를 가지고 있는 ListNodeStack 클래스를 구현하세요.
- void push(int data)를 구현하세요.
- int pop()을 구현하세요.

## **과제 5. Queue를 구현하세요.**

- 배열을 사용해서 한번
- ListNode를 사용해서 한번.