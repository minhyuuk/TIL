# 구글 I/O 리뷰_V2

### Compose Function Paradigm (선언형 패러다임)
- 뷰 계층 구조를 수동으로 업데이트 할 때 복잡성을 선언형 모델을 사용함으로써 방지할 수 있다. 선언형 모델을 사용하면 사용자 인터페이스 빌드 및 업데이트에 관련된 엔지니어링도 크게 줄일 수 있는 장점이 있다.

### 선언형 vs 명령형
- 카운트가 __99개 이상__ 이면 __불__ 이 보이게 하고 카운트가 __0개 이상__ 이면 __종이__ 가 보이게 코드를 작성해 선언형과 명령형을 비교해보겠습니다. ~~메일 앱에 읽지 않은 메세지 아이콘을 표시하는 UI의 코드입니다.~~ 
<br>
<br>

 > ### 명령형
  ``` kotlin
    // Imperative (명령형)
  fun updateCount(count:Int){
    if(count > 0 && !hasBadge()){
        addBadge()
    } else if(count == 0 && hasBadge()){
        removeBadge()
    }
   if(count > 99 && !hasFire()){
         addFire()
        setBadgeText("99+")
    } else if (count <= 99 && hasFire()){
        removeFire()
    }
    if(count > 0 && ! hasPaper()){
        removePaper()
    } else if(count == 0 && hasPaper()){
        addPaper()
    }
    if(count <= 99){
        setBadgeText("$count")
    }
  } 
  ```
명령형은 변경한 로직을 수동으로 하나하나 컨트롤 헤애힙니다.
<br><br>

> ### 선언형
``` kotlin
// Declarative (선언형)
@Composable 
fun BadgeEnvelope(count: Int){
    Envelope(fire = count> 99, paper = count > 0){
        if(count > 0){
            Badge(text = "$count")
        }
    }
}
```
 하지만 선언형은 값이 바뀔 때마다 재평가하며 필요할 때마다 업데이트 하므로 요소를 제거하거나 숨길 필요가 없습니다. UI를 선택하는 방식이 아닌 원하는 UI를 설정하는 방식이라 생각하면 편합니다. 또한 ``` Composable ``` 어노테이션  (@Composable) 을 사용하면 이 함수가 데이터를 UI로 변환하기 위한 함수라는 것을 Compose 컴파일러로 알려주는 역할을 합니다. 또한 __return 값을 아무 것도 반환하지 않습니다__.