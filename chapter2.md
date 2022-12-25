### 코틀린 기초

코틀린은 변수 선언은 val와 var로 나뉜다.
val는 value의 준말로, 값을 가리키며 변경이 불가능하다.
var는 variable의 준말로, 변수를 가리키며 변경이 가능하다.


val을 오해할 수 있는 것이 참조하는 메모리가 변경이 불가능 한 것이기 데이터가 변경이 불가능 한 것은 아니다.

```kotlin
val list = arrayListoOf("java")
lsit.add("kt")
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

코틀린의 기본 가시성은 public이다.

```java
public class Person {
  private String name;

  public Person(String name) {
    this.name = name;
  }

  public String getName() {
    return this.name;
  }
}
```

이 코드를 코틀린으로 변환하면

``` kotlin
class Person(val name: String)
```
이런 간단한 코드로 변환된다.
코틀린은 코드가 없이 데이터만 저장하는 클래스를 틀로 하고 있으며 이를 값 객체라 부른다.


#### 코틀린 프로퍼티

클래스는 데이터를 캡슐화하는데 목적을 두고 있다.

캡슐화
* 객체의 속성과 행위를 하나로 묶고,
* 실제 구현 내용 일부를 내부에 감추어 은닉한다.

즉, 적절한 메서드의 선언으로 객체의 행위를 정의하고, 이를 효과적으로 은닉하는 것을 말한다.


자바에서는 데이터를 필드에 저장하며 멤버 필드는 보통 private이다.
그리고 자바에서는 필드와 접근자를 한데 묶어 프로퍼티라고 부른다.

```Java
public Person {
  private String name;
  public String getName() {
    return this.name;
  }
  public Person(String name) {
    this.name = name;
  }
}

```
에서 필드인 String name, 접근자인 getName이 프로퍼티다.


자바에서는 접근자를 따로 선언해줘야하지만,
코틀린은 그렇지 않다.

코틀린의 프로퍼티는 자바의 필드와 접근자 메서드를 완전히 대신한다.

```kotlin
class Person(
  val name: String, // val로 선언했기 때문에 변경 불가 -> getter만 제공
  val age: Int,
  var isMarried: Boolean //var로 선언 했기 때문에 변경 가능. -> getter, setter 모두 제공
)
```

코틀린은 자바와 다르게 접근자를 사용해 호출하지 않고 프로퍼티를 직접 호출한다.

```java
//Java code
Person person = new Person("bob", 29, false);
String name = person.getName();
```

```kotlin
//kotlin code
Person person = Person("bob", 29, false)
val name = person.name;
```

자바와 다르게 생성자를 호출할 때 new를 사용하지 않는다.
그리고 getter를 호출할 때도 getName이 아닌 프로퍼티를 직접 호출한다.


코틀린에서는 기본으로 제공하는 접근자 외에 커스텀 접근자를 만들 수 있다.

```kotlin
class Rectangle(
  val height:Int,
  val idth: Int
) {
  val isSquare: Boolean
    get() {
      return height == width
    }
    /**
    get() = height == width 도 가능
     */
}
```
isSquare 프로퍼티에는 자체 값을 저장하는 필드가 필요 없으며 오직 자체 구현을 제공하는 게터만 존재한다.


#### 코틀린 enum

```kotlin
enum class Coler(
  val r: Int,
  val g: Int,
  val b: Int
) {
  RED(255, 0, 0),
  ORANGE(255,165,0),
  YELLOW(255,255,0),
  GREEN(0,255,0),
  BLUE(0,0,255),
  INDIGO(75,0,130),
  VIOLET(238,130,238); // <- 세이콜론 필수

  fun rgb() = (r * 256 + g) * 25 + b
}
```

유일하게 세미콜론이 필수인 곳이 enum을 선언할 때이다.
상수 목록과 메서드 정의 사이를 구분하기 위함이다.

자바보다 코틀린의 enum이 뛰어난 이유는 when 때문이다.
when은 자바의 switch의 기능을 제공함과 동시에 더 많은 것을 제공한다.

```kotlin
fun getMnemonic(color: Color) = 
  when(color) {
    Color.RED -> "Richard"
    Color.ORANGE -> "Of"
    Color.YELLOW -> "York"
    Color.GREEN -> "Gave"
    Color.BLUE -> "Battle"
    Color.INDIGO -> "In"
    Color.VIOLET -> "Vain"
  }
```

when 역시 if와 마찬가지로 문이 아니라 식이다.

자바와 달리 각 분기마다 break를 넣지 않아도 되며,
한 분기 안에서 여러 값을 매치 패턴으로 사용할 수도 있다.

```kotlin
fun getWarmth(color: Color) = when(color) {
  Color.RED, Color.ORANGE, Color.YELLOW -> "warm"
  Color.GREEN ->"neutral"
  Color.BLUE, Color.INDIGO, Color.VIOLET -> "cold"
}
```

물론 여기에서 Color를 정적 임포트 하면 훨씬 간단하게 사용할 수 있다.

when 이 switch보다 강력한 것은 이것 때문만이 아니다.

코틀린의 when은 분기조건에 임의의 객체를 허용한다.

```kotlin
fun mix(c1: Color, c2: Color) = 
  when(setOf(c1, c2)) {
    setOf(RED, YELLOW) -> ORANGE
    setOf(YELLOW, BLUE) -> GREEN
    setOf(BLUE, VIOLET) -> INDIGO
    else -> throw Exception("Dirty color")
  }
  ```

집합 set으로 만들어 주는 메서드인 setOf를 사용해서 컬렉션을 구성했고,
컬렉션으로 when문을 구성했다.

인자가 없는 when으로도 구성이 가능하다.

```kotlin
fun mixOptimized(c1: Color, c2: Color) = 
  when {
    (c1 == RED && c2 == YELLOW) || 
    (c1 == YELLOW && c2 == RED) -> 
    ORANGE
    ...
  
  }
```

이런식으로 구성이 가능하다.
다만 인자가 없는 when을 구성할 경우 반드시 분기의 조건은 불리언 결과를 계산하는 식이어야 한다.


 
#### smart cast

코틀린에서는 '스마트 캐스트'라는 기능이 있다.
스마트 캐스트는 컴파일러가 변수의 타입을 인지해 캐스팅 해주는 것이다.

스마트 캐스트를 사용하기 위해서는 먼저 is로 타입을 확인해야 한다.

```kotlin
if(e is Num) {
  e.value
} else if(e is Sum) {
  eval(e.right) + eval(e.left)
}
```
이렇게 e의 타입을 is를 통해서 검사만 해주면 바로 사용이 가능하다.

이 덕분에 if를 간단하게 when으로 변경 가능하다.

```kotlin
fun eval(e: Expr): Int = 
  if(e is Num) {
    e.value
  } else if(e is Sum) {
    eval(e.right) + eval(e.left)
  } else {
    throw new IllegalArgumentException("Unknown expression")
  }

  


fun eval(e:Expr): Int =
  when(e) {
    is Num -> 
      e.value
    is Sum -> 
      eval(e.right) + eval(e.left)
    else ->
      throw IllegalArgumentException("Unknown expression")
  }
```
이렇게 훨씬 가독성 좋게 변경이 가능하다.

