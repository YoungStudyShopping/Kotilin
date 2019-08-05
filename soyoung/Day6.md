### 9. Properties and Fields

```kotlin
/* 프로퍼티 */
    // 클래스의 구성요소로 선언될 수 있다
    // var : mutable
    // val : read-only (immutable)

    // 보기에는 멤버 변수와 비슷해보인다.
    // 프로퍼티 사용은 자바의 필드를 사용하듯이 하면 된다.

    // 기존 자바의 멤버 변수와 다른 점
    /* 프로퍼티 문법
    var <propertyName>[: <PropertyType] [=<property_initializer]
            [<getter>]
            [<setter>]
            게터와 세터 함수는 자동으로 생성된다!
     */
    // PropertyType은 초기값 (initializer)에서 추론 가능한 경우 생략이 가능함
    // getter를 통해 타입 추론이 가능해도 생략이 가능함 (1.1v)

    // 기존의 자바 필드를 사용하듯이 쉽게 사용할 수 있지만, 실제로는 객체지향의 캡슐화를 지향한다!
    // 사용하기 쉽지만 호출 결과가 함수이므로 값의 validation 등을 할 수도 있고...
fun main() {
    var obj = Address()
    println(obj.name) // 이 부분은 실제로 Address의 getName을 호출하게 된다
}

class Address {
    /* 코틀린의 프로퍼티 */
    var name: String = "Soyoung" // default getter, setter를 쓰려면 명시적 초기화 필요
    val city: String = "Seoul"   // default getter를 쓰려면 명시적 초기화 필요. setter는 선언 불가
        /* 실제로 바이트코드를 뜯어보면 아래 코드가 생성된다
            private final String name = "Soyoung"
            public final String getName() { return this.name }
        */

    /* Custom accessors : getter, setter를 재정의한 것 */
        // 프로퍼티 선언 내부에, 일반 함수처럼 선언할 수 있다

        /* 게터 함수나 세터 함수를 재정의 하고 싶으면 */
        var name2: String = "Kotlin"
            get() { return field }
            set(value) { field = value } // val (read-only)의 경우에는 setter 정의 불가!


    // 프로퍼티 가시성 변경하기
        // accessor에 가시성 변경이 필요하거나 어노테이션이 필요한 경우,
        // 기본 accessor는 그대로 두고 body 없는 accessor를 통해서 정의 가능
        /*
        private set
        @Inject set
        private set(value) { field = value }
        */

    /* Backing Fields */
        // 코틀린 클래스는 필드를 가질 수 없는데, 'field'라는 식별자를 통해 접근 가능한 automatic backing field 제공
        // 다른 부분에서는 사용할 수 없고, 프로퍼티의 accessor에서만 사용 가능하다
        // 생성 조건 : accessor 중 1개라도 기본 구현을 사용하거나... custom accessor에서 field 식별자를 참조할 때!
        // (필요 없어 보이면 생성하지 않는다는 소리 같음)
        var counter = 0
        set(value) {
            field = value // 여기서 field가 Backing Field
        }
        /*
        val isEmply: Boolean
            get() = this.size() == 0 // 이럴 경우에는 Backing Fields가 생성되지 않는다
        */

    /* Backing Properties */
        // 명시적으로 객체가 생성될 때
        private var _table: Map<String, Int> = null
        public val table: Map<String, Int> // 내부적으로 동작할 Backing Properties
        get() {
            if (_table == null) {
                _table = HashMap()
            }
            return _table
        }

    /* Compile-Time Constants */
        // const modifier를 이용하면 컴파일 타임 상수를 만들 수 있다
        // 조건 : Top-level || object의 멤버 || String이나 프리미티브 타입으로 초기화

        @Deprecated(MY_CONST_PROPERTY) // 해당 변수에 const가 붙어 있지 않으면 오류가 발생한다
        fun example() {}

    /* Late-Initialized Properties */
        // 일반적으로 프로퍼티는 non-null 타입으로 선언됨
        // non-null을 쓰고싶지만 생성자에서 초기화를 해줄 수가 없는 경우가 있다
        // (ex. DI, Test의 setUp 메소드 등...)
        // 그럴때는 lateinit을 붙여준다
        // 조건 : 클래스의 바디에서 선언 + 기본생성자에서 선언된 건 안됨 + var 프로퍼티만 됨 + non-null 타입만 됨 + 프리미티브 타입 안됨
        lateinit var lateInit: String
}

const val MY_CONST_PROPERTY = "GOING_HOME" // 이렇게 최상단에 있거나.. 째뜬 조건을 만족해야함
```

