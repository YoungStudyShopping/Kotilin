### 3. Basic Syntax

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}

fun sum2(a: Int, b: Int) = a + b
// 몸체가 식인 경우 return 그냥 생략
// return 타입이 추론됨 (Int끼리 더했으니까 결과도 Int)
// return 값이 없으면 Unit 리턴, 생략 가능 (= Java의 void)

// val : value (읽기 전용 변수, final)로 무조건 초기화를 해줘야함!
// var : variable (mutable 변수)

fun parseInt(str: String): Int? {}
fun printProduct(arg: String) {
    val x: Int? = parseInt(arg)
    // 이렇게 null 체크를 꼭 해줘야 한다
}
// 리턴 값이 null일 수도 있으면 null mark를 찍어줘야 한다
// 이걸 안쓰고 null을 리턴하려고 하면 컴파일 에러 발생

fun describe(obj: Any): String =
        when(obj) {
            1 -> "One"
            "Hello" -> "Gretting"
            else -> "Bye"
        }
// 저렇게 타입들이 혼용될 수 있다

when {
    "orange" in fruits -> "fruits"
}
// 저렇게 포함되어있는지 확인할 수 있다


```



___

### 4. Basic Types

```kotlin
// 코틀린에서 모든 것은 객체다

// 숫자
// 코를린에서는 CHAR가 숫자형이 아니다.
// if (c == 1) 이런식으로 쓰면 컴파일 에러
// 코틀린에서는 primitive 타입에 직접 접근할 수 없다.
// underscores 표현
val oneMillion = 1_000_000 // 긴 숫자 표현하기 좋음.

// 코틀린이 자바 플랫폼에서 돌아가는 경우
// 어떤 경우에는 JVM primitive로 저장되고
// Nullable하거나 제네릭은 박싱된다. -> identity를 유지하지 않는다.

fun main() {
    var a: Int = 10000
    var b: Int = 10000
    println("a === b : ${a===b}") // = 3개를 쓰면 두 객체가 같은 오브젝트인지 체크
    println("a == b : ${a==b}")

    var c: Int? = 10000
    println("a === c : ${a===c}")
    println("a == c : ${a==c}")

    /*
    	a === b : true
    	a == b : true
    	a === c : false
    	a == c : true
    */

}

// 코틀린에서 수치형 타입이 서로 다를 때는 명시적으로 변환함수를 써줘야 한다.

// 코틀린에서 배열은 자바와 많이 다름. 배열은 Array 클래스로 표현된다.
// 생성 방법 1. 팩토리 함수 이용, 2. arrayOf 등의 라이브 함수 이용
val type1 = Array(5) { i -> i.toString() }
val type2 = arrayOf("0", "1", "2", "3", "4")

// 특별한 Array 클래스... Primitive 타입의 박싱 오버헤드를 없앤다.
val intArray: IntArray = intArrayOf(1, 2, 3)

// escaped String : 전통적인 방식의 자바 스트링
val escapedString = "Hello World\n"
// raw String
val rawString = """
    자바와 다르다.
    이스케이핑 처리가 필요 없다.
    '이렇게 써줘도 됨'
""".trimIndent()
```

