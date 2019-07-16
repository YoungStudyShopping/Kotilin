```kt

package study.seungdols.kotlins

/**
 *
 * @PACKAGE study.seungdols.kotlins
 * @AUTHOR  seungdols
 * @DATE    2019-07-16
 */

class Example1 // 암시적인 상속

class Example2 : Any() // 명시적인 상속


// Any class는 Object class와 다르다.

fun main(args: Array<String>) {
    val bb = CC()
    bb.test()
    bb.f()
}


open class AA {
    open fun test() {
        println("test")
    }

    open fun f() {
        println("test AA")
    }
}

interface BB {
    fun f() {
        println("test CC")
    }
}

class CC : AA(), BB {
    override fun test() {
        println("BB test")
    }

    override fun f() {
        super<AA>.f()
        super<BB>.f()
    }
}

```
