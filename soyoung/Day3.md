### 5. Control Flow

```kotlin
val a = 5
val b = 3
val c = true
val s = "String"
val collection = listOf(3, 6, 9)

fun main() {
    /* if */
        // if와 else는 Java와 거의 유사하다.
        // if문이 식으로 사용되는 경우에는 값을 반환하는데, 이럴 때는 반드시 else를 동반해야 한다.
        val max1 = if (a > b) a else b
        // int max = (a > b) ? a : b (Java와 다르게 코틀린에는 삼항 연산자가 없다. if 문으로 충분함!)

        // 아래와 같이 브랜치를 가지게 만들 수도 있다.
        // 이럴 경우 브랜치 내에 마지막으로 나오는 값이 반환 값이 된다.
        val max2 = if (a > b) {
            print("Choose a")
            a
        } else {
            print("Choose b")
            b
        }

    /* when */
        // switch 문을 대체한다.
        // 각각의 브랜치의 조건문이 만족될때까지 위에서부터 순차적으로 인자를 비교한다.
        // 조건을 만족하는 브랜치가 실행되기 때문에 break를 써줄 필요가 없다.
        when (a) {
            1 -> print("a == 1")
            2 -> print("a == 2")
            else -> {
                print("으악!")
            }
        }
        // when 또한 식으로 사용해 바로 결과 값을 집어넣어 줄 수 있다.
        // 이럴땐 if와 마찬가지로 else 문이 필수적이다.
        var result = when (a) {
            100 -> "A"
            90 -> "B"
            80 -> "C"
            else -> "F"
        }
        // 컴파일러가 else 문이 없어도 된다고 판단하는 경우 없어도 된다.
        var bool = when (c) {
            true -> "맞다"
            false -> "틀리다"
        }
        // 여러개의 조건에 맞춰서 사용하고 싶을 경우 조건문에 콤마를 사용하면 된다.
        // 브랜치의 조건문에 함수나 식을 사용할 수 있다.
        // range나 collection에 in으로 범위도 검사할 수 있다.
        when (a) {
            0, 1 -> print("이렇게 여러개 추가 가능")
            1 + 3 -> print("4")
            in 1..10 -> print("우와 신기해")
            !in collection -> println("컬렉션도 가능!")

        }
        // is를 이용해서 타입 검사도 가능하다.
        fun hasPrefix(s: Any) = when (s) {
            is String -> s.startsWith("prefix")
            else -> false
        }

    /* For */
    // for문은 iterator를 제공하는 모든 것을 반복할 수 있다 (List나 Array 등등 ...)
    for (item in collection) print(item)

    // 이런 컬렉션을 새로 생성하고 싶으면 operator로 표기된 hasNext()와 next(), iterator() 함수를 가지도록 만들면 된다.
    class MyIterator {
        operator fun hasNext() : Boolean { return true }
        operator fun next(): Int { return 0 }
    }
    class MyData {
        operator fun iterator(): MyIterator {
            return MyIterator()
        }
    }
    // 배열이나 리스트를 반복할 때 인덱스를 이용하고 싶으면 indices나 withIndex 이용
    for (i in collection.indices) {}
    for ((index, value) in collection.withIndex()){
        print("$index: ${value}")
    }

    /* While */
    // Java와 거의 같은데, do-while문에서 body의 지역변수를 조건문이 참조할 수 있음
    do {
        val y = 0
    } while (y != null)
}
```



------

### 6. Package and Return Jumps

```kotlin
/* Pacakge */
// 소스 파일은 패키지 선언으로 시작된다.
// 패키지를 명세하지 않으면 이름이 없는 기본 패키지에 포함된다. -> 패키지에 포함되지 않는게 아니다!
// 이걸 호출할 때는 구냥 호출하면 됨! (다른 파일에 있어도 잘 호출됨)
// 패키지를 지정해주고 싶으면 이렇게 한다.
package foo

// 코틀린에서 기본적으로 포함시키는 패키지들이 있음.
    // kotlin.*
    // kotlin.collections.*
    // kotlin.io.*
    // ...
// 때문에 따로 import 해주지 않아도 된다.

// 기본적으로 포함되는 패키지 외에 임포트하고 싶으면 이렇게 한다.
import foo.*

/* Return and Jumps */
    // return : 함수나 익명 함수에서 반환
    // break : 루프 종료시키기
    // continue : 루프의 다음 단계로 진행

fun main() {
    // 이렇게 보면 비슷하지만, label로 break와 continue를 할 수 있다
    loop@ for (i in 1..10) {
        for (j in 1..10) {
            if (i + j > 12) {
                // break@loop    이렇게 해봤자 바깥 for문 밖으로는 못나간다.
                continue@loop // label을 통해 한번에 나가버릴 수 있다!
            }
        }
    }

    // 코틀린에서는 { 함수 리터럴, 지역함수, 객체 표현식, 함수 } 가 중첩될 수 있다.
    fun foo() {
        var ints = listOf(0, 1, 2, 3)

        ints.forEach(fun(value: Int) {  // 이 fun은 익명함수다. fun 안에 forEach 안에 함수가 중첩되어 있다.
            if (value == 1) return      // 이 return은 foo() 함수가 아니라 익명함수가 반환되도록 한다.
            print(value)
        })
        print("End")

        // 람다로도 풀어서 쓸 수 있다.
        ints.forEach(({
            if (it == 1) return         // [주의] 람다는 함수가 아니기때문에 foo() 함수 자체를 반환하게 되어 0만 찍혀버린다.
            print(it)
        }))                             // 여기서 맨 바깥쪽 () 소괄호는 생략해도 된다.

        // 만약 여기서 람다식만 끝내주고 싶을 때는 label을 사용한다
        ints.forEach label@ {
            if (it == 1) return@label
            print(it)
        }

        // 레이블을 쓰기 귀찮으면 암시적 레이블을 쓰자
        // 암시적 레이블은 람다가 사용된 함수의 이름과 동일하다
        ints.forEach {
            if (it == 1) return@forEach
            print(it)
        }

        // 이와 같이 map 함수로도 레이블을 지정할 수 있다.
        val result = ints.map {
            if (it == 0) {
                return@map "zero"
            }
            "number ${it}"
        }
    }
}
```

