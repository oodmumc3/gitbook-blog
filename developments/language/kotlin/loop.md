---
description: 반복문에 대해서 알아본다.
---

# 반복문

## for

* for 루프의 경우 iterator를 제공하는 모든것을 반복할 수 있음.

```kotlin
val intList = (1..10).toMutableList()
// print 1 ~ 10
for (i in intList) { print(i) }
```

* iterator를 사용하지 않고 index기반으로 for 루프를 사용할 수 있음.

```kotlin
val intList = (1..5).toMutableList()
for (i in intList.indices) { println("index: $i, value: ${intList[i]}") }
```

* `withIndex`로 index와 value를 한번에 사용할수 있음.

```kotlin
val intList = (1..5).toMutableList()
for ((index, value) in intList.withIndex()) { println("index: $index, value: $value") }
```

## while, do ~ while

* 기존 문법과 동일 하므로 설명하지 않음.

## return, break, continue, label

* 코틀린에서는 세가지 점프 연산자를 제공한다.

| 연산자 | 사용법 |
| :--- | :--- |
| return | 가장 가깝게 둘러 싼 함수나 임의 함수에서 리턴한다. |
| break | 가장 가깝게 둘러 싼 루프를 끝낸다. |
| continue | 가장 가깝게 둘러 싼 루프의 다음 반복문으로 넘어간다. |

### break, continue 라벨

* break, continue에 라벨지정시 끝내거나 다음 반복문으로 넘어갈 반복문을 지정할 수 있다.

```kotlin
for (i in intList) {
    for (k in intList) {
        if (k == 2) break
        println("inner for k :: $k")
    }
    println("outer for i :: $i")
}

// inner for k :: 1
// outer for i :: 1
// inner for k :: 1
// outer for i :: 2
// inner for k :: 1
// outer for i :: 3
```

```kotlin
outerLoop@ for (i in intList) {
    for (k in intList) {
        if (k == 2) break@outerLoop // 바깥 루프 빠져나감
        println("inner for k :: $k")
    }
    println("outer for i :: $i")
}

// inner for k :: 1
```

### return 라벨

* return 식은 가장 가깝게 둘러싼 함수에서 return한다.
* 만약 람다 식에서 리턴하고 싶다면 라벨을 붙여서 return을 한정해야 한다.

```kotlin
val intList = (1..3).toMutableList()

fun foo () {
    intList.forEach {
        if (it == 2) return
        print(it)
    }
    println("end of foo function")
}

foo()

// 1
```

* 위의 예에서 forEach 람다 안에서 return시 가장 가까운 foo함수를 빠져나간다.
* 만약 foo가 아닌 forEach를 빠져나가고 싶다면 라벨을 붙인다.

```kotlin
val intList = (1..3).toMutableList()

fun foo () {
    intList.forEach limit@ {
        if (it == 2) return@limit
        print(it)
    }
    println()
    println("end of foo function")
}

foo()

// 1
// 3
// end of foo function
```

{% hint style="info" %}
#### 예상치 못한 결과

위에 내가 생각했던 결과는 다음과 같다.

```text
1 -> end of foo function
```

그런데 실제 결과는 다음과 같다.

```text
1 -> 3 -> end of foo function
```

내가 의도 했던바는 `return@limit`시 `forEach`를 빠져나간 후 다음 로직을 타는 거였는데 실제 코틀린에서는 **조건에 부합하는 부분만 `forEach`에서 제외하고 모두 실행된다.**

이부분 조심해서 사용해야 되겠다.
{% endhint %}

* 모든 라벨을 정의하지 않고 임의의 라벨을 사용할 수 있다.
* 임의 라벨은 전달 받은 함수와 같은 이름으로 사용한다.

```kotlin
...
fun foo () {
    intList.forEach {
        if (it == 2) return@forEach
        print(it)
    }
...
}

// 결과값은 상위와 같음.
```

\*\*\*\*



## 참조

* [http://codesunsoo.blogspot.com/2016/04/kotlin-programming-langauage.html](http://codesunsoo.blogspot.com/2016/04/kotlin-programming-langauage.html)
* [https://javacan.tistory.com/entry/kotlin-11-12-ko-reference](https://javacan.tistory.com/entry/kotlin-11-12-ko-reference)

