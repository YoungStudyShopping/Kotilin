# 5. Control Flow

Today

- if else 문 한줄코드

```kotlin
    val max = if (a>b) a else b
    
    val max2 = if(a>b) {
            print("choose a")
            a
        } else {
            print("choose b")
            b
        }
 ```

- 삼항연산자가 없다. if문이 이 역할을 잘 할수있다.

- when

```kotlin
    when(x) {
            1 -> print("x == 1")
            2 -> print("x == 2")
            else -> {
                print("x is neither 1 nor 2")
            }
        }
    
    var res = when(x) {
            100 -> "A"
            90 -> "B"
            80 -> "C"
            else -> "F"
        } // 변수에 바로 할당 가능
    
    var res2 = when(isTrue) {
            true -> "맞다"
            false -> "틀리다"
        } // 이렇게하면 else를 쓸필요가없다.
    
    when(x) {
            0,1 -> "0 or 1" // 조건 여러개.
    				parseInt(x) -> print("encode ${x}")
            else -> "not"
        }
    
    val number = listOf(3,6,9)
        when(number) {
            in validNumbers -> print("valid이다")
            in 1..10 -> print("1,10사이에있")
            !in 10..20 -> print("10,20사이에없")
            else -> print("not")
        }
    
    fun hasPrefix(x:Any) = when(x) {
        is String -> x.startsWith("prefix") // 자동으로 타입캐스팅이된다.
        else -> false
    }
    
    when{
            x.isOdd -> print()
            x.isOrder -> print()
     }
 ```

- break문 쓸필요 없다.
- when에 인자가 없으면 논리연산으로 처리됨.

```kotlin
for

    var collection = listOf(1,23,4,5,5,6,7,7,8)
    collection.iterator()
    for(item in collection) {
        
    }
    
    val array6 = arrayOf(1,2,3,45,66,7,3)
    array6.iterator()
    for(i in array6) {
        
    }
    
    val array = arrayOf(1,2,3,4,5)
    for(i in array.indices) {
        print(array[i])
    }
    
    for((index, value) in array.withIndex()) {
        print("${index} ${value}")
    }
```


- iterator를 반환하면 for-each를 사용할수있다.

# 6. package return and jump

- 패키지는 명세하지않으면 기본패키지에 포함된다.
- 기본패키지는 import없이 그냥 쓰면된다.
- 기본적으로 import되는 패키지들이 있다. kotlin.* 등등..

```kotlin
    import test.pkg.printPack as bBar
    
    fun main(args: Array<String>) {
        bBar()
    }

    loop22@ for(i in 1..10) {
            for(j in 1..10) {
                if(i+j>12) {
                    break@loop22
                }
            }
        }
```

- loop레이블을 사용해서 jump할수있다.

```kotlin
    a.forEach(
        fun(value:Int) {
            if(value == 1) return
            print(value)
        }
    ) // 0, 2, 3
        
    a.forEach() {
        if(it == 1) return
        print(it)
    } // 0
    
    a.forEach label@{
        if(it == 1) return@label
        print(it)
    } // 0, 2, 3
    
    a.forEach {
        if(it == 1) return@forEach
        print(it)
    } // 0, 2, 3
    
    
    var b = a.map {
        if(it == 0) return@map
    }
```

- 람다식은 return이 forEach까지 끝난다. 람다는 함슈가아니다. 가장 가까운 함수를 종료시켜버린다.
- 함수식은 함수만 끝내버린다. 1빼고 다출력
- label을 사용하면 람다식만 종료시킬수있다. `@label`
- 커스텀 label 을 안달고 가장 근처 루프문의 이름을 적어도된다. `@map` `@forEach`
