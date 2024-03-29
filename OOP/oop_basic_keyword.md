객체지향 패러다임이 생겨나면서 이러한 **4가지 특징**을 갖추게 되었고, 이를 잘 이해하여 구현할 필요가 있다. **각 특징을 조금 더 깊이 파헤쳐보려** 한다.

1. **추상화**

- 객체들이 공통적으로 **필요로 하는 속성이나 동작을 하나로 추출**해내는 작업을 뜻한다.

- **추상적인 개념**에 **의존**하여 **설계해야 유연함**을 갖출 수 있다.
즉, **세부적인 사물들의 공통적인 특징을 파악**한 후, 하나의 **묶음**으로 만들어내는 것이 **추상화**다.

2. **캡슐화**

- 정보 은닉화를 통해 높은 응집도, 낮은 결합도를 유지할 수 있도록 설계하는 작업을 뜻한다.

- 쉽게 말하면, 한 곳에서 변화가 일어나도 다른 곳에서 일어나는 사이드 이펙트를 최소화 시키는 것을 의미한다. 즉, 객체 내부의 **어떤 동작에 대한 구현이 어떻게 되어있는지 감추는 것**이다. 이를 통해 외부에서 뭔가 잘못 건드려 객체를 손상시키는 일을 방지할 수 있다.

- 여기서 **응집도**는 모듈의 독립성을 나타내는 개념으로, 모듈 내부 구성요소 간 연관 정도를 뜻하고,
**결합도**는 어떤 기능을 실행할 때 클래스나 모듈에 얼마나 의존적인지를 나타내는 지표를 뜻한다.
객체 간의 독립성을 강조하기 위해 객체지향 프로그래밍이 등장했다. 그런데 결합도가 높아서야 객체지향으로 설계하는 의미가 있을까?

- 따라서 독립적으로 만들어진 객체들 간의 **의존도가 최대한 낮게 만드는 것이 중요**하다. 때문에 소프트웨어 공학적으로, **객체 내의 모듈 간의 요소가 밀접한 관련이 있는 것으로 구성하여 응집도를 높이고**, **결합도를 줄여야 요구사항 변경에 대처하는 좋은 설계**라고 배운다.

**한 줄로 정리하자면** 객체 각각은 독립적으로 작용할 수 있도록 응집도는 강해야 하고 다른 모듈을 참조하는 결합도는 낮아야 한다.

3. **상속**

- 여러 개체들이 지닌 **공통된 특성을 부각시켜 하나의 개념이나 법칙으로 성립**하는 과정을 뜻한다.
상속을 설명할 때 예시로 부모 클래스와 자식 클래스로 설명한다.
부모 클래스의 필드나 메서드를 자식 클래스가 상속받아 사용하거나 약간 변형하여 사용하는걸 뜻한다. 
조금 더 엄밀히 따지면 상속은 **자식 클래스를 외부로부터 은닉**하는 **캡슐화의 일종**이다.

- 상속을 활용하면 상위 클래스의 구현을 활용함으로써, 코드 재사용이 용이해진다. 그러나, 상속을 통한 **재사용을 할 때 나타나는 단점이 명백하다**. 따라서 **객체지향 프로그래밍에서 '코드 재사용'을 목적으로 하는 상속 행위는 엄격히 금한다**.

<br>

1. **부모 클래스의 변경이 불편해짐**
    
    → 부모 클래스에 의존하는 자식 클래스가 많을 때 부모 클래스의 변경이 필요하다면, **이를 의존하는 자식 클래스들이 영향**을 받게 됨
    <br>
2. **불필요한 클래스의 증가**
    
    → 유사 기능 확장시, **필요 이상의 불필요한 클래스**를 만들어야할 수 있음
    <br>
3. **잘못된 상속 사용**
    
    → **같은 종류가 아닌 클래스의 구현을 재사용하기 위해 상속**을 받게 되면, 문제가 발생할 수 있음.상속받는 클래스가 **부모 클래스와 `IS-A` 관계가 아닐 때 발생**
    <br>
    
    **`IS-A` :** 포함 관계를 의미한다. 
                  “한 클래스 A가 다른 클래스 B의 자식 클래스” 임을 이야기한다.
    
                   e.g. 햄스터는 동물이다. (소의 부모 클래스는 동물)
    

### **※ 다시 짚어볼 내용 ※**

---

이런 문제는 구성(Composition)을 통해 해결이 가능하다고 한다.

객체 구성은 객체 내부 필드에서 다른 객체를 참조하는 방식으로 구현된다.
상속에 비해 런타임 구조가 복잡하고 구현이 어렵지만, 변경 시 유연함을 확보할 수 있다는 장점이 크다.
→ **같은 종류가 아닌 클래스를 상속하고 싶을 땐, 객체 컴포지션을 먼저 적용해볼 것**

---

상속은 이런 상황일때만 사용해야한다.

- **`IS-A` 관계가 성립할 때**
- **재사용의 관점이 아닌, 기능의 확장 관점일 때**

**상속을 코드 재사용의 개념으로 이해하면 안 된다**. 코드를 재사용할 수 있다고 무지성으로 상속을 사용하는 경우가 있는데, 이렇게 되면 클래스간 결합도가 너무 높아져 유지보수 효율이 너무 낮아진다. **일반적인 개념을 구체화하는 상황에서 상속을 사용해야한다**.
<br>

4. 다형성

- 서로 다른 클래스의 객체가 같은 동작 수행 명령을 받았을 때, **각자의 특성에 맞는 방식으로 동작**하는 걸 뜻한다.

- **다형성**은 **객체 지향 패러다임의 핵심**이다. 다형성과 상속은 엄청난 시너지를 만들어내는데, 다형성 구현을 통해 코**드를 간결하게 해주고, 유연함을 갖추게** 해준다. 또한, 구체적으로 현재 어떤 클래스 객체가 참조되는 지는 무관하게 **헐렁하게 프로그래밍하는 것이 가능**하다.

- 차를 예시로 설명하자면 기본적인 자동차를 상속하여 페라리, 람보르기니 객체를 생성하였는데, 베기음 재생이라는 메서드를 실행했을 때 서로 다른 베기음을 내는 것이 다형성의 한 부분이다.

- 상속 관계에 있다면, 새로운 자식 클래스가 추가되어도 부모 클래스의 함수를 참조해오면 되기 때문에 다른 클래스에게 영향을 미치지 않는다.