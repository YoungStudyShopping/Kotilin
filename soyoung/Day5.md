### 8. Inheritance

```kotlin
/* 상속 */
    // 코틀린의 최상위 클래스는 Any
    // 클래스에 상위타입을 선언하지 않으면 Any가 상속됨
    class Example1          // 암시적인 Any 상속
    class Example2 : Any()  // 명시적인 Any 상속

    // Any는 Object와 다른 클래스임...
        // equals(), hashCode(), toString()만 가지고 있다
    // 상속을 해주려면 Open 해줘야 한다
    open class Base(p: Int)
    // 상속 받을때 슈퍼 타입 클래스의 기본 생성자가 있으면 이걸 호출해서 초기화할 수 있다
    class Derived(p: Int) : Base(p)

    // 파생클래스에 기본 생성자가 없으면 각각의 보조생성자에서 상위타입을 super 키워드를 이용해 초기화해줘야 한다
    class MyView : View {
        constructor() : super(1) // 어떻게든 슈퍼타입을 초기화해준다
        constructor(ctx: Int) : this() // super를 호출하지 않고 위임한다
        constructor(ctx: Int, attrs: Int) : super(ctx, attrs)
    }

    // open 어노테이션은 Java의 Final과 반대로, 다른 클래스가 상속할 수 있게 해준다
    // 기본적으로 코틀린의 모든 클래스는 상속되지 못하는 Final이다.

/* 오버라이딩 */
    // 오버라이딩 될 메소느는 open 어노테이션이, 오버라이딩 할 메소드는 override 어노테이션이 요구된다
    open class AA {
        open fun toOverride() {}
        fun notOverride() {}
    }
    class BB : AA() {
        override fun toOverride() {} // 이렇게 상속받을 수 있다
        // override fun notOverride() {} 얘는 오버라이딩 할 수 없다
    }
    // 프로퍼티도 메소드와 같은 방법으로 오버라이딩 할 수 있다

    // 오버라이딩 규칙 : 같은 멤버에 대한 중복된 구현을 상속받은 경우,
        // 상속받은 클래스는 해당 멤버를 오버라이딩하고, 자체 구현을 제공해야 한다
        // 이 때, SUPER + <클래스명>을 통해 상위 클래스를 호출할 수 있다
    // 자바에는 인터페이스에 구현체가 없지만, 코틀린에는 구현체가 있을 수 있음!

    open class A {
        open fun f() { print("A")}
        fun a()      { print("a")}
    }
    interface B {
        fun f() { print("B") }
        fun b() { print("b") }
    }
    class C : A(), B {
        override fun f() { // 반드시 function f를 구현해줘야 한다
            // 상속받은 함수들중의 하나를 호출하고 싶은 경우
            super<A>.f()
        }
        override fun b() {}
    }

/* 추상 클래스 */
    // 구현이 없는 클래스로, 굳이 open을 붙이지 않아도 된다
    abstract class AbsClass {
        abstract fun absFunction()
    }
    class MyClass() : AbsClass() {
        override fun absFunction() {} // 바로 상속받을 수 있음!
        // absFunction()을 구현해줘야 한다
    }
```

