# Thread

## Android Developers

[Android Developers : Thread](https://developer.android.com/reference/java/lang/Thread)
#

## Thread란?<br><br>

 Thread는 작업의 흐름이다. 무언가를 백그라운드로 돌려놓고 다른 여러가지 일을 하는 것이 스레드라고 할 수 있다. <br><br>

## Thread의 필요성<br><br>

 외부 Thread 가 없이 Main Thread 만으로만 구현하게 된다면, 이러한 문제가 생긴다. 어떠한 버튼을 눌렀을 때 Main Thread 내부적으로 10초 이상이 걸리는 작업을 한다고 치면, 사용자는 그 일이 끝날 때까지 멈춰있는 화면만 보고 있어야 한다. 그렇기 떄문에 오래 걸리는 작업들을 외부 Thread를 통해 해결한다.<br><br>

 

## Thread 사용법<br><br>

1초 마다 현재 시간을 갱신하는 코드

```
class MainActivity : AppCompatActivity() {

    var clockTextView: TextView? = null

    override fun onCreate(savedInstanceState: Bundle?) {
        // ...

        clockTextView = findViewById(R.id.clock)

        thread(start = true) {
            var cal = Calendar.getInstance()
            var sdf = SimpleDateFormat("HH:mm:ss")

            while (true) {
                val strTime = sdf.format(cal.time)
                clockTextView?.setText(strTime)

                Thread.sleep(1000)
            }
        }
    }
```

 메인 Thread는 할 일을 끝낸 후 다음 일을 진행할 수 있지만 Thread를 많이 사용한다면 여러가지 일을 한 번에 할 수 있다. Thread의 개념이 부족하다면 더욱 공부를 해보는 것이 좋다.