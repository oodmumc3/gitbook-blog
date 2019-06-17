---
description: 분기문인 if와 when에 대해 알아본다.
---

# 분기문 \(if, when\)

## IF

* if문의 경우 자바에서 사용하던 if문과 문법은 같음.
* 코틀린의 경우 if문은 표현식이므로 값을 반환할수 있음. \(삼항식이 없음\)
* 중괄호 사용시 마지막에 쓴 변수가 반환됨.

```kotlin
// 삼항식 대용
val max = if (a < b) b else a
println(max) // 10

val result = if (a < b) {
    //... some doing
    b
} else {
    //... some doing
    a
}
println(result) // 10
```

## WHEN

* 자바의 switch와 비슷함.
* `break;` 문이 필요하지 않으며 `default:` 문은 `when`의 `else`문과 같다.
* when을 사용할때 인자를 받거나 받지 않고 사용할수 있으며 if와 같이 표현식으로 값을 반환할수 있다.
* 반환값을 가지는 경우 모든 경우의 조건을 정의해야만 한다.

```kotlin
val score = 80

// no return
// print B
when(score) {
    in 100..80 -> println("A")
    !in 100..80 -> println("B")
    else -> println("F")
}

// return
val grades = when(score) {
    in 100..80 -> "A"
    !in 100..80 -> "B"
    else -> "F"
}
println(grades) // B


// no argument
// print B
when {
    score in 100..80 -> println("A")
    score !in 100..80 -> println("B")
    else -> println("F")
}
```

## 참조

* [https://altongmon.tistory.com/583](https://altongmon.tistory.com/583)
* [http://blog.naver.com/PostView.nhn?blogId=nww731&logNo=221365445749](http://blog.naver.com/PostView.nhn?blogId=nww731&logNo=221365445749)
* [https://dybz.tistory.com/175](https://dybz.tistory.com/175)

