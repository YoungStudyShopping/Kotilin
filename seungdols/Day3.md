

# control flow 

```kotlin
/**
 * @PACKAGE
 * @Author seungdols
 * @Date 2019-07-02
 */

fun main(args: Array<String>) {
    var a = 1
    var b = 2
    val max = if (a > b) a else b

    val max2 = if (a > b) {
        println("Choose a")
        a
    } else {
        println("Choose b")
        b
    }

    val choise = "seungdols"
    when (choise) {
        "seungdols" -> println("choise === ${choise}")
        "company" -> println("choise === ${choise}")
        else -> {
            println("None")
        }
    }
    var score = 80
    var result = when (score) {
        100 -> "A"
        90 -> "B"
        80 -> "C"
        else -> "F"
    }

    var isReview = true
    var res = when (isReview) {
        true -> "true"
        false -> "false"
    }

    var x = 1
    when (x) {
        0, 1 -> println("x === 0 or x === 1")
        else -> println("ohterwise")
    }

    val vaildNumbers = listOf(1, 2, 3)
    when (x) {
        in vaildNumbers -> println("X is vaild")
        in 1..10 -> println("x is in the range")
        !in 10..20 -> println("x is not include")
    }

    fun hasPrefix(x: Any) = when (x) {
        is String -> x.startsWith("prefix") // smart casting
        else -> false
    }

    val collection = listOf(1, 2, 3, 4, 5)
    for (item in collection) {
        println(item)
    }

    val myData = MyData()
    myData.iterator()

    for (item in myData) {
        println(item)
    }


    val array = arrayOf("A", "B", "C")
    for (i in array.indices) {
        println("$i: $array[$i]")
    }

    for ((index, value) in array.withIndex()) {
        println("$index: ${value}")
    }

    fun sum(a: Int, b: Int): Int {
        println("a: $a, b: $b")
        return a + b
    }

    // label 식별자 + @
    loop@ for (i in 1..10) {
        println("-----i: $i")
        for (j in 1..10) {
            println("j: $j")
            if (i + j > 12) {
                break@loop
            }
        }
    }

    foo()

    fooLambda()
    fooLambdaWithLabel()
}

fun foo() {
    var ints = listOf(1, 2, 3, 4, 5)
    ints.forEach(fun(value: Int) {
        if (value == 1) return
        println(value)
    })
    println("End")
}

fun fooLambda() {
    var ints = listOf(1, 2, 3, 4, 5)
    ints.forEach({
        if (it == 1) return
        println(it)
    })
    println("End")
}

fun fooLambdaWithLabel() {
    var ints = listOf(1, 2, 3, 4, 5)
//    ints.forEach label@ {
//        if (it == 1) return@label
//        println(it)
//    }
    ints.forEach {
        if (it == 1) return@forEach // name label
        println(it)
    }
    println("End")
}

class MyIterator {
    val data = listOf(1, 2, 3, 4, 5)
    var idx = 0
    operator fun hasNext(): Boolean {
        return data.size > idx
    }

    operator fun next(): Int {
        return data[idx++]
    }
}

class MyData {
    operator fun iterator(): MyIterator {
        return MyIterator()
    }
}
```
