# Drawerlayout

## Drawerlayout이란? <br><br>

화면의 각 부분에서 당겼을 때 이름처럼 서랍(Drawer)을 여는 것과 마찬가지로 꺼내는 역할을 수행한다고 하여 Drawerlayout이라 한다.

<img src="https://t1.daumcdn.net/cfile/tistory/9957AE3359E0731211" width="600px" height="350px"><br>

## 사용방법
>다른 레이아웃 파일을 하나 만든 뒤 이런 식으로 코드를 작성하시면 됩니다.<br><br>
이 레이아웃의 이름을 저는 layout_slide_menu로 설정했습니다.

```kotlin

// 슬라이드 화면으로 만들 레이아웃 코드로 작성

<androidx.constraintlayout.widget.ConstraintLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".Main.MainActivity">

    <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:text="광주소프트웨어마이스터고"
            android:textColor="#000"
            android:textStyle="bold"
            android:textSize="18sp" />

    

<androidx.constraintlayout.widget.ConstraintLayout>

```
<br><br>

layout_main

```kotlin
<androidx.drawerlayout.widget.DrawerLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    // ... (메인 엑티비티 레이아웃 코드)

</androidx.drawerlayout.widget.DrawerLayout>
```


>layout_main을 작성 후 메인 엑티비티를 작성합니다

MainActivity
```kotlin
R.id.iv_hamburger -> {
                    // 이미지를 클릭하게 된다면
                    // drawer 열고 닫기
                    if(binding.drawerLayout.isDrawerOpen(ll_drawer)){
                        binding.drawerLayout.closeDrawer(ll_drawer)
                    }else{
                        binding.drawerLayout.openDrawer(ll_drawer)
                    }
                }

                R.id.ll_left_area -> {
                    // drawer 닫기
                    if(binding.drawerLayout.isDrawerOpen(ll_drawer)){
                        binding.drawerLayout.closeDrawer(ll_drawer)
                    }

                }
```

여기서 나온 iv_hamburger는 제가 만든 이미지의 id값이며 첫 번째 if else문은 **이미지 클릭 시** drawer layout이 열리는 것이며 두 번째 if else문은 **빈 곳을 클릭**하게 된다면 drawer layout이 닫히게 되는 코드입니다.<br><br>

일부 코드만 보여드려 이해가 어려울 수 있지만 혹시나 궁금한 점이나 어려운 점이 있다면 저의 깃허브에서 Contact me를 확인해주세요.<br><br>

많이 미흡하지만 봐주셔서 감사합니다.<br><br>

출처 : https://recipes4dev.tistory.com/139