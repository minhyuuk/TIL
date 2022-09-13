#### Context




##### Context는 안드로이드 4대 컴포넌트 **中 하나**이다.

난 여기서 Context 가 정확히 어떤 역할을 하는 지 몰랐다.
누군가가 물어보면 정확하게 대답하지 못할 거 같았다.
그래서 공부좀 해보려고 한다.<br><br>

#### Android Context?
어플리케이션에 대해 현재 상태를 나타내는 역할을 하는데,
**"앱이 흘러가는 맥락"** <- 정도로 해석하면 어느 정도 이해가 된다.<br><br>

#### Context 기능

어플리케이션의 현재 상태를 갖고 있음. 
시스템이 관리하고 있는 액티비티, 어플리케이션의 정보를 얻기 위해 사용한다.
안드로이드 시스템 서비스에서 제공하는 API(리소스, DB, Shared Preferences 등)에 접근하기 위해 사용한다. -> **getResource()** 같은 메소드를 얘기한다.
**Activity**, **Application** 클래스는 **Context** 클래스를 상속받은 클래스이다.<br><br>

- Context 는 안드로이드 앱개발에 있어 필수적인 사항이고, 매우 중요하기 때문에 이를 정확히 이해하고 올바르게 사용하는 것이 중요하다.
- Context 의 잘못된 사용은, 메모리 릭 문제로 이어질 수 있기 때문에 정말 주의해야한다.

이러한 Context 는 크게 두 가지로 나뉜다.<br><br>

#### 종류

- activity → Activity의 기본정보
- application → application의 기본정보

이렇게 두 종류의 Context 가 존재하기 때문에,
가끔 어디에 어떤 Context 를 사용해야 할지 헷갈리는 경우가 있다.<br><br>

#### ;) Application Context ;)
Activity 에서 applicationContext 라는 프로퍼티를 통해 얻을 수 있는 싱글톤 인스턴스이다.
(Java 에선 getApplicationContent()라는 메소드를 통해 얻을 수 있다.)
이 Context 는 어플리케이션 라이프사이클과 묶여있어, 현재 Context 가 종료되고 나서도
Context 가 필요한 작업이나, 액티비티 범위를 벗어난 곳에 Context 가 필요한 작업에 적합하다.<br><br>

---

어플리케이션 내에 싱글톤 객체를 만드려고 하는데 이 객체가 Context 를 필요로 할 때, Application Context 를 사용하면 된다. 만약 이런 상황에 Activity Context 를 넘겨주게 되면, Activity 에 대한 참조를 메모리에 남겨두며 GC (Garbage Collected) 되지 않은 채 메모리 leak(누수)이(가) 발생할 것이다.<br><br>

**예시**
**Q. 어플리케이션 전역에서 사용할 어떤 라이브러리를 MainActivity 에서 초기화 할 때 Context 가 필요하다. 어떤 Context 를 넘겨줘야 할까?**

**A. Application Context**
**-> 만일 Activity Context 를 넘겨주게 되면, MainActivity 에 대한 참조가 메모리 상에서
Garbage Collect 되지 않아** ***메모리 릭이 발생하기 때문이다.***

따라서, 오랫동안 지속되거나 앱 전역에서 사용될 녀석의 경우 Application Context 를 넘겨주면 된다.

#### ;) Activity Context ;)
해당 Context 는 이름 그대로 액티비티 안에서만 사용이 가능하다. 특정 **Activity 의 LifeCycle** 에 종속되어 있다. 이 녀석은 Activity 스코프 내에서 사용될 때 넘겨주거나, Activity 와 같은 객체를 생성할때 넘겨준다. 즉, Activity 가 소멸되면 해당 __Context__ 도 같이 소멸되는 것이다.

---

Application Context 는 Activity Context 가 지원하는 모든 것을 지원하지 않는다.
만능처럼 보이지만 절대 아니다. 따라서 GUI (View Component 등) 관련 동작들에 있어
Application Context 는 오류를 발생할 확률이 높다.

Activity 는 Garbage Collection 이 가능하지만, Application 은 앱 프로세스가 살아있는 동안 계속하여 남아있다.

따라서, Application Context 를 활용한 객체를 메모리에서 할당 해제하지 않고 있을 경우,
**메모리 릭(Memory leak)** 을 발생할 가능성이 농후하다.

#### 참고
[Android Developers Context 관련 공식 문서](https://developer.android.com/reference/kotlin/android/content/Context)
[Android Context, 너 대체 뭐야?](https://velog.io/@haero_kim/Android-Context-%EB%84%88-%EB%8C%80%EC%B2%B4-%EB%AD%90%EC%95%BC)