#### Null


#### Null Safety란?<br>

- Null을 안전하게 처리한다는 뜻이다. 코틀린의 특징 중 하나이며 Null은 안전하지 않기 때문에 코틀린에서 Null을 안전하게 사용될 수 있도록 구성하고 있다.<br>


 - Null을 사용하게 되면 NullPointerExceptionError가 뜬다. 에러가 뜨지 않게 하기위해 우리는 그에 맞게 사용하는 문법을 사용한다.<br><br>

#### 😠사용방법😃 <br><br>

####  ? : 물음표 앞의 값이 Null이 아니라면 이 문장을 실행한다

**button?.setOnClickListener**<br><br>

####  !! : 느낌표 앞의 값이 Null이 아님을 확신할 때 이 문장을 실행한다

**button!!.setOnClickListener**<br><br>

```
Int, Double, Float, Class     -> Null이 될 수 없는 타입
Int?, Double?, Float?, Class? -> Null이 될 수 있는 타입
```
<br>
 Null Safety를 사용하는 방법은 총 2가지이다. 물음표와 느낌표 2개이다. 물음표는 Null이 아니라면 실행하지만 느낌표는 Null이 아닐 때 무조건 실행하기 때문에 쓰다가 오류가 발생할 수도 있다. 100% 확신할 수 있는 건 없기 때문에 느낌표를 사용하는 건 추천하지 않는다.<br><br>

#### 참고
[Android Developers Null 관련 공식문서](https://kotlinlang.org/docs/reference/null-safety.html)