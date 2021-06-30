# Resource

## Android Developers

[Android Developers : Resource](https://developer.android.com/guide/topics/resources/providing-resources?hl=ko)
#



 리소스는 코드에서 사용하는 추가 파일과 정적인 콘텐츠이다. 예를 들어 비트맵, 레이아웃 정의, 사용자 인터페이스 문자열, 애니메이션 지침 등이 있다. 리소스를 사용하게 되면 오류를 고칠 때 순조롭게 고칠 수 있고 #define과 같은 개념이라 생각하면 편하다.


**Resource**는 총 세 부분으로 나뉜다.

colors는 **색깔**을 지정 

strings는 **text에 넣을 값**을 지정

styles는 **테마**를 꾸민다

#
## Colors에 대한 예시
### res → values 경로로 이동

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="colorPrimary">#6200EE</color>
    <color name="colorPrimaryDark">#3700B3</color>
    <color name="colorAccent">#03DAC5</color>
    <color name="textview_color">#DF4D4D</color>
</resources>
```

이런 식으로 색깔 또는 텍스트를 지정해 가져다 오는 형식으로 사용된다. <br><br>

## 사용하는 이유?<br><br>

 Resource를 사용하지 않게 된다면 위험하다. 나중에 레이아웃을 10.. 아니 100개 넘게 사용하게 된다. 100개 파일을 전부 수정하고 고칠 때 하나하나 찾으러 가는 건 큰 손해이다. 이런 결손을 방지하기 위해 Resource를 사용한다.