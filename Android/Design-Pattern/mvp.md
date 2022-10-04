### MVP 란?

MVP 패턴은 Model + View + Presenter를 합친 용어이다.
Model 과 View 는 MVC 패턴과 동일하고, Controller 대신 Presenter 가 존재한다.

MVP 의 핵심 설계는 MVC 와 다르게 UI(View) 와 로직(Model)을 분리하고,
서로 간에 상호작용을 다른 객체(Presenter)에 그 역할을 줌으로써, 
서로의 영향을(의존성)을 최소화하는 것에 있다.
<br>

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fcc72f60-1a26-4511-8e00-98355a8468c6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221002%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221002T144729Z&X-Amz-Expires=86400&X-Amz-Signature=2e13aa4da41476261122177a2a2b71b879fa48bef5174247f84a4e2b3c87dde1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject" width="600px" height="350px">

### 구조

**Model**

Model 은 APP 에서 사용되는 data를 처리한다. (비지니스 로직)
View 또는 Presenter 등 어떤 요소에도 의존적이지 않고 독립적이다.

**View**
View는 사용자에게 보여지는 UI를 나타낸다. (Android 에서 Activity, Fragment)
Model 로부터 data 를 받아 사용자에게 보여주는 역할을 하고
Presenter 를 이용해 데이터를 주고받는다. 그러므로 Presenter 에 매우 의존적이다.

**Presenter**

Presenter 는 View 에서 요청한 정보로 Model 을 가공하여 View 에 전달한다.
View 와 Model 사이를 연결해주는 연결다리 역할을 한다.

<br>

### 동작
1. 사용자의 Action 이 View 를 통해 들어온다.
2.  View 는 Data 를 Presenter 에 요청한다.
3.  Presenter 는 Model 에 데이터를 요청한다.
4.  Model 은 Presenter 에게 받은 요청에 대한 응답을 보낸다.
5.  Presenter 는 View 에게 Model 에서 받았던 데이터를 보낸다.

<br>

---

<br>

### MVP 의 특징

Presenter 와 View 는 서로 1:1 관계이며
Presenter 는 View 와 Model 의 인스턴스를 가지고 있어 둘을 연결하는 역할을 합니다.

<br>

### MVP 의 장점?

- MVC 와 달리 코드가 매우 깔끔해진다.
- Presenter 를 통해서 데이터를 전달 받기 때문에 Model 과 View 간의 결합도를 낮추면 새로운 기능 추가 및 변경을 해야 할 때 관련된 해당 부분만 수정하면 되기 때문에 확장성이 좋아진다.
- 테스트 코드 작성하기 편리해지기 때문에 더 쉽게 안전한 코딩이 가능하다.
- UI 와 Data 각각 구현 파트를 나누기 떄문에 해야 할 일이 명확해지며 그 결과로 쉽고 빠르게 개발이 가능하다.

<br>

### MVP 의 단점?

- View 와 Model 의 의존 관계를 해결했지만, Presenter 사이의 의존성이 높은 단점이 존재한다.
- 앱이 커지면 커질수록 View 와 Presenter 사이의 의존도가 강해진다.