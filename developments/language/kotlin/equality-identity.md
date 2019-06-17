---
description: 동등성 및 동일성의 의미와 코틀린에서의 표현 방법에 대해 알아본다.
---

# 동등성 vs 동일성

## 동일성 및 동등성의 의미

### 동일성 \(equality\)

* 두개의 오브젝트가 완전히 동일한 것을 의미한다.
* 하나의 오브젝트만 존재하는것이며 그 오브젝트를 참조하는 여러개의 레퍼런스 변수를 갖고 있는것을 의미한다. \(정확히 같은 메모리 주소를 가지고 있음\)

### 동등성 \(identity\)

* 동일한 정보를 가지고 있는 오브젝트를 의미한다.
* 메모리상에 각기 다른 오브젝트가 존재하는 것이며 각 오브젝트의 기준에 따라 동등하다고 판단한다.

## 자바와 코틀린의 동등성 연산

### 자바

* 자바에서 원시타입 비교시 `==`를 사용한다.
* 참조변수에서 `==`를 사용할 경우 주소값을 비교한다. \(동일성\)
* 자바에서 두 참조변수의 동등성을 알기 위해서는 `.equals`를 사용해야한다. \(동등성\)

### 코틀린

* 코틀린에서는 자바와 달리 `==`를 사용시 내부적으로 .equals를 호출한다. \(동등성\)
* 주소값을 비교하고 싶다면 `===`을 사용한다. \(동일성\)

{% hint style="info" %}
자바와 코틀린에서의 동등성 연산이 다르니 주의해서 사용해야 한다.
{% endhint %}

{% tabs %}
{% tab title="Java" %}
```java
// String Constant Pool 저장 안되게함
String a = new String("hello");
String b = new String("hello");

System.out.println(a == b); // false
System.out.println(a.equals(b)); // true
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
// String Constant Pool 저장 안되게함
val a = String(StringBuilder("hello"))
val b = String(StringBuilder("hello"))

println(a == b) // true
println(a === b) // false
```
{% endtab %}
{% endtabs %}

## 참조

* [https://kwssite.tistory.com/23](https://kwssite.tistory.com/23)
* [https://yeon-log.tistory.com/7](https://yeon-log.tistory.com/7)
* [https://wooooooak.github.io/kotlin/2019/02/24/kotiln\_%EB%8F%99%EB%93%B1%EC%84%B1%EC%97%B0%EC%82%B0/](https://wooooooak.github.io/kotlin/2019/02/24/kotiln_%EB%8F%99%EB%93%B1%EC%84%B1%EC%97%B0%EC%82%B0/)



