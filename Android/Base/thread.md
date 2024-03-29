#### Thread


#### 기본적 사전 의미

**스레드**
* 동시 작업을 위한 하나의 작업 단위이자 프로세스 내에서 순차적으로 실행되는 실행흐름의 최소 단위이다.

**멀티 스레드**
* 한 프로세스 내에서 둘 이상의 스레드가 동시에 실행되는 것을 말한다.

**멀티 프로세스**
* 여러개의 CPU에서 여러개의 프로세스가 실행되는 것을 의미한다.<br><br>

#### 멀티 스레드를 사용하는 이유

모든 작업들이 UI 스레드에서만 처리되는 경우, 네트워크를 불러오는 등 너무 긴 작업들은 UI 쓰레드에서 블록될 수 있고 UI 쓰레드는 아무것도 할 수 없게 된다. 이렇게 되면 앱이 정상적이여도 **죽은 것처럼** 보이고 ANR 이라는 애플리케이션 응답 없음 에러를 뱉기도 한다. 그래서 UI 스레드를 **블록**되게 하지 않는 게 중요하다. 그럴 때 **멀티 스레드**를 사용한다.<br><br>

#### 메인 스레드에서 UI 작업을 진행해야하는 이유는?
예를 들어 설명을 하자면

이미지를 그리는 스레드 A,
버튼을 그리는 스레드 B,
텍스트를 그리는 스레드 C 가 있을 때

A-B-C 순서대로 스레드가 실행된다면 원하는 UI를 그릴 수 있지만 상대적으로 크기가 작은 텍스트를 가진 C 스레드가 먼저 실행되고 엄청 큰 이미지인 A 스레드가 나중에 실행된다면 원하는 뷰가 나오지 않을 수 있다. 그러므로 UI 작업은 **하나의 스레드**에서만 실행이 되어야 한다. 하나의 스레드는 **메인 스레드**를 얘기하는것이다.<br><br>

---

또한 서브 스레드에서도  UI 작업을 진행할 수 있다고 생각하지만 **handler**를 통해 메인 스레드에 **UI 작업**을 **요청**하는것이지 서브 스레드에서  UI 작업을 진행하는건 아니다.

---
<br>


#### 스레드는 start 와 run 방식이 있는데,

<br>

**start** 방식은 JVM 에서 스레드를 위한 **call stack(stack 영역)을 새로 만들기 때문에**, <u>독립적으로 사용이 가능</u>하고 **run** 방식은 **메인 스레드의 call stack을 사용하기 때문에** <u>run 메소드가 끝날 때 까지 다른 작업을 진행하지 못한다.</u>

<br>

#### 참고
[Android Developers Thread 관련 공식문서](https://developer.android.com/reference/java/lang/Thread)