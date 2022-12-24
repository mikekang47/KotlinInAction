### 코틀린 기초

코틀린은 변수 선언은 val와 var로 나뉜다.
val는 value의 준말로, 값을 가리키며 변경이 불가능하다.
var는 variable의 준말로, 변수를 가리키며 변경이 가능하다.


val을 오해할 수 있는 것이 참조하는 메모리가 변경이 불가능 한 것이기 데이터가 변경이 불가능 한 것은 아니다.

```kotlin
val list = arrayListoOf("java")
lsit.add("kotlin")
```
가능하다.

코틀린은 문자열을 편리하게 다룰 수 있다.

```kotlin
val name = "sihoo"
println("Hello $name")
```
쉽게 가능하다.


더 재미있는 것은 kotlin에서 if는 문이 아니라 식이다.
if는 값을 만들어 내며 다른 식의 하위 요소로 계산에 참여할 수 있다.
```kotlin
fun max(a: Int, b: Int): Int {
  return if(a>b) a else b
}
``` 


