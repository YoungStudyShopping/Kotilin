# Basic Synctax


```kotlin
/**
 * @PACKAGE
 * @Author seungdols
 * @Date 2019-06-28
 */

fun main(args: Array<String>) {
//    val // == java final

//    var // mutable

    val a: Int = 1
    //a = 2
    var b = 2

    val name = "seungdols"

    val introduce = "My name is $name"
    println(introduce)
//

    val condition: Boolean = true

    println(if (condition) condition else "false")

    val x = 3
    if (x in 1..10) {
        println("$x is 3")
    }

    val fruit = listOf("banana", "abocado", "kiwi", "apple").filter { it.startsWith("a") }.sortedBy { it }
        .map { it.toUpperCase() }
    println(fruit)

    // Java 에서 숫자형은 primitive type으로 저장된다.
    // Nullable이나 제네릭의 경우에는 Boxing 된다.
    // Boxing 된 경우에는 identity를 유지 하지 못한다.
    // https://kotlinlang.org/docs/reference/basic-types.html#explicit-conversions
    var number1: Int = 1000
    var number2: Int = 1000
    println("number1 === number2 : ${number1 === number2}")
    println("number1 == number2 : ${number1 == number2}")

    var number3: Int = 1000
    var number4: Int? = 1000
    println("number3 === number4 : ${number3 === number4}")
    println("number3 == number4 : ${number3 == number4}")

    var array: Array<String> = arrayOf("seungdols", "seungdols compnany")
    println(array.get(0))
    println(array[0])

    val array1 = Array(5, { i -> i.toString()})
    val array2 = arrayOf("0", "1", "2", "3", "4")

    // array of primitive type
    val array3: IntArray = intArrayOf(1,2,3)


    val rawString = """
        "'This is raw string of kotlin'"
    """.trimIndent()
    println(rawString)
}



```
