```kt
import java.awt.event.MouseAdapter

/**
 * @PACKAGE
 * @Author seungdols
 * @Date 2019-08-13
 */

// object expressions

open class A(x: Int) {
    public open val y: Int = x
}

interface B {}

val ab: A = object : A(1), B {
    override val y = 15
}

class MyRunnabl : Runnable {
    override fun run() {
        println("running")
    }
}

class C {
    private fun foo() = object {
        val x: String = "x"
    }

    fun publicFoo() = object {
        val x: String = "x"
    }

    fun bar() {
        val x1 = foo().x // ok
//        val x2 = publicFoo().x // error
    }
}


class MyClass {
    public fun publicFun() = object {
        var x = 111
    }

    private fun privateFun() = object {
        var x = 222
    }

    fun print() {
//        print(publicFun().x)
        print(privateFun().x)
    }
}

// object declaration
object CountManager {
    var count = 0
}

// companion object

class Test {
    companion object Factory {
        fun create(): Test = Test()
    }
}

object MyClass_1 {
    init {
        println("create MyClass_1")
    }
}

fun main(args: Array<String>) {
    // old version
//   val t = Thread(MyRunnabl())
    // object expression
//    val t = Thread(object : Runnable {
//        override fun run() {
//            println("running")
//        }
//    })

    val t = Thread({ println("running") })

    t.run()

    MyClass().print()

    println()
    CountManager.count++
    println(CountManager.count)

    val instance = Test.create()

    println(MyClass_1)
    println(MyClass_1)
    println(MyClass_1)
}

```
