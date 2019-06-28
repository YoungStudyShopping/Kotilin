`Unit` == void 리턴타입없으면 기본으로 Unit

`val` == final 타입

`var` == mutable 변수. 값을 할당,변화 모두가능.

`"$a is not $b = ${a+b}"` 문자열 템플릿

```kotlin
fun main(args: Array<String>) {
    println("hello world")
    val a: Int =1
    val b = 2
    val c: Int
    c = 3
//    c = 4
    /*
    * /*
    *
    * ㅇㅇ주석
    * */
    *
    * */
    val x = 3
    val items = listOf("apple", "banana", "kiwi")


    items
            .filter { it -> it.startsWith("a") }
            .sortedBy{it}
            .map{it.toUpperCase()}
//            .forEach()

    var aa:Int =1000
    var bb:Int =1000
    print("${aa === bb}, ${aa == bb}")

    val a2:Int = 1
    val b2:Long = a.toLong()
    val i:Int = b.toInt()

    var array:Array<String> = arrayOf("apple", "banana")
    print(array.get(0))
    print(array[0])
    print(array.size)

    val array2 = Array(5, {i->i.toString()})
    val array3 = arrayOf("1","b")

    val s = """
        djfksfla
        djfaksdfjas
        fasdjfkldsfasd
        fasdfjasdf
        메롱메로메올@_@@@@@
        하하하하핳하핳ㅎㅎ
    """.trimIndent()
}

fun sum(a: Int, b:Int):Int {
    return a+b
}

fun sum2(a: Int, b: Int) = a + b

fun printSum(a:Int, b:Int): Unit {
    println("sum of $a and $b is ${a+b}")
}

fun printSum2(a:Int, b:Int) {
    println("sum $a $b ${a+b}")
}

fun maxOf(a: Int, b: Int) = if(a>b) a else b

fun parseInt(str: String): Int? {
    return null
}

fun getStringLength(obj: Any): Int? {
    if(obj is String) {
        return obj.length
    }
    return 0
//    return obj.length
}

//fun describe(obj: Any):String {
//    when(obj) {
//        1 -> "One"
//        "hello" -> "hi!"
//    }
//}

```
