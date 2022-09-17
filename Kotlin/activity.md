#### Activity

엑티비티는 안드로이드 4대 컴포넌트 중 하나이다.
그중에서도 UI와 가장 밀접한 관련을 가지고 있기 때문에
사실상 안드로이드 앱에 있어서 가장 기본이 되는 구성 요소이다.
<br>

  **특징**
- 화면에 UI를 표시하는 기본요소이며 대부분의 경우 액티비티는 꽉찬 화면을 구성하지만,
   예외적으로 floating windows, multi-window mode처럼 화면의 일부를 차지하게 할수 있다.

- Activity의 종류 중 하나로 FragmentActivity가 있는데,
   이는 nested fragment,즉 fragment안에 다른 fragment가 있는 경우 사용하기도 한다.

- AppCompatActivity는 안드로이드 하위버전의 안드로이드를 지원하기 위해 사용된다.
  참고로 AppCompatActivity는 FragmentActivity를 상속한다.
<br>

이런 액티비티는 생명주기를 갖는다.

<br>

 **onCreate** 
 - 앱을 실행할때 호출됩니다.

 **onStart**       
 - 엑티비티가 화면에서 보여지기 시작할때 호출됩니다.

 **onResume**  
 -  사용자와 상호작용하거나 화면에 엑티비티가 나타나있고 실행중일때 호출됩니다.

 **onPause**      
  - 엑티비티의 화면 일부가 다른 엑티비티에 의해 가려져 포커스를 떠날 때 호출됩니다.

 **onStop**       
  -  다른 엑티비티의 실행으로 완전히 화면을 가릴 때 호출됩니다.

 **onDestroy**   
 -  엑티비티가 완전히 종료되었을 때 호출됩니다.