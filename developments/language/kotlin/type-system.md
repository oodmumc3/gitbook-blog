---
description: 코틀린의 타입 시스템에 대해 알아보자.
---

# 타입 시스템

## **Primitive types**

* 코틀린은 원시 타입과 래퍼 타입을 구별하지 않는다. \(Int, Boolean\)
* NonNullable
  * 컴파일시 자동으로 원시타입 비교일경우 원시타입 사용
  * 메서드를 호출하면 래퍼 클래스로 박싱하여 사용
* Nullable
  * null에는 원시 타입이 들어갈수 없으므로 기본으로 래퍼 클래스를 사용한다.

## Nullable과 NonNullable

* 코틀린에서는 기본 NonNull이다.
* Nullable 변수를 선언하려면 `?`를 붙여서 사용한다.

```kotlin
var nonNull: String = "hello"
nonNull = null // error

var nullable: String? = null
nullable = "hello"
```

## Safe call operator - ?.

* Nullable 변수 사용시 nullpointer가 발생할 수 있으므로 null체크 후에 메서드를 사용할 수 있게 해준다.
* 만약 null인 변수에서 메서드 호출시 NPE를 발생시키지 않고 null만 반환한다.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
fun foo(value: String?) {
    //val length = value.length // error

    val length = value?.length
    println("$length")
}

foo("jin") // 3
foo(null) // null
```
{% endtab %}

{% tab title="Java" %}
```java
public class PersonJava {
    public static void foo(String value) {
        Integer length = null;
        if (value != null) {
            length = value.length();
        }

        System.out.println(length);
    }
    public static void main(String[] args) {
        foo("jin"); // 3
        foo(null); // null
    }
}
```
{% endtab %}
{% endtabs %}

## Elvis operator - ?:

* null 대신 기본값을 반환해주는 연산자이며 생긴 모습이 엘비스의 머리와 비슷하여 엘비스 연산자라 부른다.

```kotlin
fun foo(value: String?) {
    val length = value ?: "" .length
    println("$length")
}

foo("jin") // 3
foo(null) // 0
```

## **Safe casts - as?**

* 형변환 하려는 타입이 맞으면 형변환하고 맞지 않거나 Null이면 null을 할당한다.

```kotlin
fun foo(o: Any?) {
    val s: String? = o as? String
    println(s?.length)
}

foo("jin") // 3
foo(null) // null
```

## **Not-null assertions - !!**

* `!!`사용시 nonnull타입\(val\)으로 변경하거나 NPE에러가 발생한다.

```kotlin
fun foo(s: String?) {
    val value = s!!
    println(value.length) // ?.를 사용하지 않아도 됨
}

foo("jin") // 3
foo(null) // NPE!!
```

## **Any, Any?**

* 코틀린에서는 원시 타입을 포함한 모든 타입의 조상이 Any이다.

  * 원시 타입을 할당할 경우 해당 원시 타입에 부합하는 래퍼 클래스로 박싱된다.

  ```kotlin
  val any: Any = 13 // auto boxing
  ```

* Any 는 null 을 가질 수 없다. null 까지 담으려면 Any? 를 써야 한다.
* Any는 자바의 Object와 대응되지만 `toString()`, `equals()`, `hashCode()`이외의 메서드는 존재하지 않는다. ex\) `wait()`, `notify()`

## Unit \(void\)

* 코틀린의 Unit타입은 자바의 void와 같다.
* 반환타입이 없이 선언한 함수는 암묵적으로 Unit타입을 반환하도록 되어있다.
* `void`와 달리 타입 파라미터\(T\)로 사용 가능하다.

## Nothing

* exception을 던지거나 무한 loop와 같은 절대 `return`을 하지 않는경우 Nothing을 사용한다.

```kotlin
class PersonKotlin constructor(val name: String) {
}

fun fail(message: String): Nothing {
    throw IllegalStateException(message)
}

fun main() {
    val person: PersonKotlin? = PersonKotlin("jin")
    // Nothing을 리턴타임으로 사용하지 않을경우 type mismatch 에러발생
    // require: PersonKotlin, found: Unit
    val p: PersonKotlin = person ?: fail("error")
    println(p.name)
}
```

## 출처

* [https://aroundck.tistory.com/4860?category=639761](https://aroundck.tistory.com/4860?category=639761) \| \[돼지왕 왕돼지 놀이터\]
* [https://umbum.tistory.com/608](https://umbum.tistory.com/608)
* [https://tourspace.tistory.com/115](https://tourspace.tistory.com/115)

