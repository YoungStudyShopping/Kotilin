### 7. Class

```kotlin
import java.util.*

/* 클래스 */
    // 코틀린에서 클래스와 상속은 구별해야 함
    class Soyoung(height: Int) {}
    // 헤더와 바디는 옵션으로 생략 가능하다 (아예 중괄호까지 생략 가능!)
    class Empty


/* 기본 생성자 */
    // 코틀린에서는 기본 생성자와 보조 생성자가 분리된다.
    // 기본 생성자 (Primary Constructor) 클래스 별로 1개만 가질 수 있으며, 헤더의 일부가 된다
    class Person constructor(firstName: String) {}
    // 어노테이션이나 접근지정자가 없으면 constructor 키워드는 생략할 수 있다
    class Person2 (firstName: String) {}
    // 기본 생성자는 코드를 가질 수 없고, 초기화를 하고싶으면 init 블록 안에서 써야한다
    class Customer(name: String) {
        init {
           // 기본 생성자의 내용은 여기에 들어간다!
        }
        // println("이름: $name") 이렇게 쓸 수 없다. 바디에 들어갈 수 있는 건 한정돼있음!
    }
    // 프로퍼티는 하나의 이름으로 getter와 setter가 자동으로 생성된다(?)
    class HasProperty() {
        var property1: String = "" // 초기화를 해줘야 한다. 객체를 생성하고 여기에 값 할당 가능
    }
    // 프로퍼티의 선언 및 초기화는 기본 생성자에서 간단한 구문으로 사용 가능하다
    class HasProperty2(property: String) {} // 이렇게 써줘도 위와 똑같이 동작한다


/* 보조 생성자 */
    // 보조 생성자 (Secondary Constructor)는 클래스의 body 내에 선언하며, 여러개 가질 수 있다
    // 기본 생성자 없이 보조 생성자가 여러 개 있을수 있다
    // 클래스가 기본 생성자를 가지고 있으면, 각각의 보조 생성자는 기본 생성자를 직간접적으로 위임해줘야 한다
        // 직접적 : 기본 생성자에 위임
        // 간접적 : 다른 보조생성자에 위임
    class Secondary (val name: String) {
        constructor(name: String, parent: Secondary) : this(name) {
            // 여기서 this(name)은 이 클래스의 기본 생성자를 호출한다
        }
        constructor() : this("박소영", Secondary()) {
            // 이렇게 다른 보조 생성자를 호출할 수 있음!
        }
    }


/* 생성된 기본 생성자 */
    // 생성된 기본 생성자 (Generated Primary Constructor)
    // 클래스에 기본 생성자와 보조 생성자를 하나도 선언하지 않으면 만들어진다
    // 매개변수가 없고 public임!
    // public이 아닌 걸 만들고 싶으면 따로 기본 생성자를 만들어줘야 한다

    // 클래스의 멤버
        // 생성자와 초기화 블록
        // 함수
        // 프로퍼티
        // 내부 클래스 (Nested and Inner Class)
        // 오브젝트 선언 (Object Declarations) -> 자바와 많이 다름

fun main() {
    // val obj = Person() 기본 생성자 안에 파라미터가 있기 때문에 넘겨줘야 한다
    // 코틀린에는 new 키워드가 없다. 생성자를 일반 함수처럼 호출하면 된다
    val obj = Person("soyoung")
    println(obj)
}
```

