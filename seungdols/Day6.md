```kt
/**
 * @PACKAGE
 * @Author seungdols
 * @Date 2019-08-06
 */
fun main() {
    val obj = User("Kotlin", 113)
    println(obj)
    val obj1 = NoData("Kotlin", 113)
    println(obj1.toString())

    val oldObj = obj.copy(age = 2)
    println(oldObj)
    val (name, age) = User("seungdols", 29)
    println("${name}, ${age}")

    val demo = Outer.Nested().foo()
    println(demo)
}

data class User(val name: String, var age: Int) {

}

class NoData(var name: String, var age: Int)

class Outer {
    private val bar: Int = 1

    class Nested {
        fun foo () = 2
    }
}
```
