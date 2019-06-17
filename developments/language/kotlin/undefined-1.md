---
description: 코틀린의 범위 표현식에 대해 알아본다.
---

# 범위 표현식

## Range Expression

* 코틀린의 범위 표현식은 `..`이나 `rangeTo()`, `downTo()`로 만들어짐.
* 기본적으로 마지막 범위를 포함시키며 증가 또는 감소값은 기본 1이다.

### 숫자 범위

```kotlin
// 두개가 같은 표현
// print 1 ~ 10
for (i in 1..10) println(i)
for (i in 1.rangeTo(10)) println(i)

// 두개가 같은 표현
// print 10 ~ 1
for (i in 10 downTo 1) println(i)
for (i in 10.downTo(1)) println(i)
```

### 문자 범위

```kotlin
// a ~ z
for (c in 'a'..'z') println(c)
// z ~ a
for (c in 'a' downTo 'z') println(c)
```

### Until

* 기본적으로 끝 값을 포함하지만 포함하지 않을때는 `until`을 사용한다.

```kotlin
// print 1 ~ 10
for (i in 1 .. 10) print(i)
// print 1 ~ 9
for (i in 1 until 10) print(i)
```

### Step

* `step`키워드를 이용하여 두 값의 증감값을 설정할수 있다. \(default: 1\)

```kotlin
// print 13579
for (i in 1..10 step 2) print(i)
// print acegikmoqsuwy
for (c in 'a'..'z' step 2) print(c)
```

### first, last, step

| 종류 | 값 |
| :--- | :--- |
| first | 범위 첫 시작 값 |
| last | 범위 마지막 값 |
| step | 범위 증가 값 |

```kotlin
println((1..10 step 3).first) // 9
println((1..10 step 2).last) // 1
println((1..10 step 4).step) // 4
```

### range min, max, sum, average

* 코틀린 범위 표현식에는 내장된 계산식이 존재함.
* 각 계산식의 뜻은 직관적이므로 생략

```kotlin
val r = (1..10)

println(r.min()) // 1
println(r.max()) // 10
println(r.sum()) // 55
println(r.average()) // 5.5
```

## 참조

* [http://zetcode.com/kotlin/ranges/](http://zetcode.com/kotlin/ranges/)

