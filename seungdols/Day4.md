
# Class and Inheritance 

```kt
/**
 * @PACKAGE
 * @Author seungdols
 * @Date 2019-07-12
 */

fun main(args: Array<String>) {

    val customer = Customer("Kotlin")
    println(customer)
}


class Invoice(data: Int) {

}

class Empty


class Person constructor(firstName: String) {

}

class Person2(firstName: String) {

}

class Customer(name: String) {
    init {
        println("This is Customer class. $name")
    }
}

class Person3 {
    constructor(parent: Person3) {

    }
}

class Person4(val name:String) {
    constructor(name: String, parent: Person4) : this(name) {

    }
}
```
