---
description: 객체의 생성과 생성자에 대해 알아보자.
---

# 객체 생성 및 생성자

## 기본적인 클래스 구조 및 생성

* class키워드로 클래스를 선언하며 기본으로 public가시성을 가진다.
* 자바와 달리 객체를 생성시 `new`키워드를 사용하지 않는다.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
class PersonKotlin {
    // empty class
}

fun main() {
    val personKotlin = PersonKotlin()
}
```
{% endtab %}

{% tab title="Java" %}
```kotlin
public class PersonJava {
    public static void main(String[] args) {
        PersonJava personJava = new PersonJava();
    }
}
```
{% endtab %}
{% endtabs %}

## 클래스 생성자

* 하나의 클래스에는 **주요 생성자**와 **보조 생성자**를 가질 수 있다.
* 주요 생성자는 클래스명 뒤에 위치한다.

```kotlin
class PersonKotlin constructor(name: String) {
    val name = name
}

fun main() {
    val p = PersonKotlin("jin")
    println(p.name) // jin
}
```

* 가시성 제한자나 어노테이션이 없다면 `constructor`키워드는 생략 가능하다.

```kotlin
class PersonKotlin (name: String) {
    val name = name
}
```

* 주요 생성자는 자바와 같이 생성자를 가질수 없으며 초기화 및 유효성 검사 코드는 init블록에서 가능하다.

```kotlin
class PersonKotlin (name: String) {
    val name = name
    init {
        // name이 isNotEmpty를 만족하지 않으면 IllegalArgumentException 발생
        require(name.trim().isNotEmpty()) { "require name" }
    }
}

fun main() {
    val p = PersonKotlin("") // IllegalArgumentException: require name
    val p1 = PersonKotlin("jin")
    println(p1.name) // jin
}
```

* 주요 생성자에서는 프로퍼티를 선언 및 초기화를 간소화 할수 있게 해준다.
* 주요 생성자에서 `val`로 생성시 읽기전용\(only get\)이며 `var`로 선언시 읽기 쓰기\(read, write\)가 가능하다.

```kotlin
class PersonKotlin (val name: String, var age: Int) {
}

fun main() {
    val p = PersonKotlin("jin", 31)
    // get
    println("name: ${p.name}, age: ${p.age}") // jin, 31

    // set
    // p.name = "park" // error
    p.age = 21

    println("name: ${p.name}, age: ${p.age}") // jin, 21
}
```

* `constructor`키워드를 이용하여 보조 생성자를 만들 수 있다.
* 멤버 변수\(?\)는 타입추론이 되지 않으니 타입을 명시해 주어야한다. ~~\(당연한건데... 몰랐음;;\)~~

```kotlin
class PersonKotlin {
    val name: String
    constructor(name: String) {
        this.name = name
    }
}

fun main() {
    val p = PersonKotlin("jin")
    println(p.name) // jin
}
```

* 주요 생성자에서 초기화 하지 않은 클래스의 모든 프로퍼티는 반드시 초기화를 해야한다. \(자바의 경우에는 기본값을 초기화해줌\)
  * 주요 생성자에 존재하는 것은 초기화 해주지 않아도 되는듯 하다?!

```kotlin
class PersonKotlin(age: Int) {
    val age: Int = age // ok
}

---
// 클래스명 옆에 괄호를 붙이지 않고 construcotr사용시 constructor자체가
// 주요 생성자가 되어 바로 초기화 시켜줄수 있는것으로 보임
class PersonKotlin {
    val age: Int
    
    constructor(age: Int) {
        this.age = age // ok
    }
}

---
// 아래의 경우 비어있는 주요 생성자가 존재하므로
// 보조 생성자에서 age초기화를 못함.
// 여기서는 age의 초기화를 해주어야한다.
class PersonKotlin() {
    val age: Int // X
    // val age: Int = 0 // O
    
    constructor(age: Int): this() {
        this.age = age // error
    }
}
```

* 주요 생성자와 보조 생성자를 혼합하여 사용할 경우 주요 생성자는 반드시 호출해야한다.

```kotlin
class PersonKotlin(val name: String) {
    // 주요 생성자에 없는것은 임의로 초기화 시켜줘야함.
    var age: Int = 0

    constructor(name: String, age: Int): this(name) {
        this.age = age
    }
}

fun main() {
    val p = PersonKotlin("jin", 31)
    println("name: ${p.name}, age: ${p.age}") // jin, 31
}
```

* 생성자가 가시성 제한자를 가진다면 constructor를 명시해주어야 한다.

```kotlin
class PersonKotlin private constructor() {
}

fun main() {
    val p = PersonKotlin() // error - private constructor
}
```

