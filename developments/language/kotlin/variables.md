---
description: 코틀린의 변수 사용법에 대해 알아본다.
---

# 변수

## 변수 선언 방식

* **val / var**

| 방식 | 타입 |
| :--- | :--- |
| val \(value\) | 불변 \(자바의 final과 같음\) |
| var \(variable\) | 가변 |

```kotlin
val test ="hello"
test = "world" // error

var test1 = "hello"
test1 = "world" // ok
```

## 기본 타입

* 자바와 코틀린의 큰 차이점중 하나는 **코틀린**의 경우 **모든것이 객체임.**
  * 이로인해 자바와는 다르게 **원시 타입이 없음**

### 숫자

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xD0C0;&#xC785;</th>
      <th style="text-align:left">&#xAE38;&#xC774;</th>
      <th style="text-align:left">&#xBE44;&#xACE0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Long</td>
      <td style="text-align:left">64</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Int</td>
      <td style="text-align:left">32</td>
      <td style="text-align:left">&#xC815;&#xC218; &#xCCB4;&#xACC4;&#xC758; &#xAE30;&#xBCF8;&#xAC12;</td>
    </tr>
    <tr>
      <td style="text-align:left">Short</td>
      <td style="text-align:left">16</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Byte</td>
      <td style="text-align:left">8</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Double</td>
      <td style="text-align:left">64</td>
      <td style="text-align:left">
        <p>&#xBD80;&#xB3D9;&#xC18C;&#xC218;&#xC810; &#xC218; &#xCCB4;&#xACC4;</p>
        <p>&#xAE30;&#xBCF8;&#xAC12;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Float</td>
      <td style="text-align:left">32</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>```kotlin
val int = 123
val long = 123456L
val double = 1234
val float = 12.34F
```

* 코틀린은 자동으로 값을 확장하지 않으므로 명시적으로 변환해야함.
* 자바의 경우 자동으로 형변환 해줌.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val otherInt = 123
val otherLong = otherInt
println(otherLong.javaClass.kotlin.qualifiedName) // kotlin.Int

val otherLong2 = 123.toLong()
println(otherLong2.javaClass.kotlin.qualifiedName) // kotlin.Long
```

* **to형변환\_타입\(\)**
{% endtab %}

{% tab title="Java" %}
```java
public class Variable {
    public static void main(String[] args) {
        int otherInt = 123;
        long otherLong = otherInt;
        System.out.println(((Object)otherLong).getClass().getName()); // java.lang.Long
    }
}
```
{% endtab %}
{% endtabs %}

## 불리언

* 논리곱과 논리합은 느슨하게 평가되어 왼쪽에서 조건을 만족시 오른쪽은 평가하지 않는다.

```kotlin
val boolean = 1 < 2
```

## 문자 및 문자열

### 문자

* 단일 문자를 나타낸다.
* 문자 리터럴은 \` 와 같은 단일 따옴표를 사용한다.
* 자바에서처럼 숫자로 다뤄지지 않는다.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val char = 'A'
val char2: Char = 12 // Error!
```
{% endtab %}

{% tab title="Java" %}
```java
char a = 12; // OK!
```
{% endtab %}
{% endtabs %}

### 문자열

* 자바와 같이 불변으로 생성됨.
* 이중 따옴표 또는 삼중 따옴표로 생성됨.

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xC774;&#xC911; &#xB530;&#xC634;&#xD45C;</th>
      <th style="text-align:left">&#xC0BC;&#xC911; &#xB530;&#xC634;&#xD45C;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#xC774;&#xC2A4;&#xCF00;&#xC774;&#xD504;&#xB41C; &#xBB38;&#xC790;&#xC5F4;
        &#xC0DD;&#xC131;
        <br />&#xAC1C;&#xD589;&#xACFC; &#xAC19;&#xC740; &#xD2B9;&#xC218;&#xBB38;&#xC790;&#xB294;
        &#xBC18;&#xB4DC;&#xC2DC; &#xC774;&#xC2A4;&#xCF00;&#xC774;&#xD504;&#xB418;&#xC57C;&#xD568;.</td>
      <td
      style="text-align:left">
        <p>&#xC6D0;&#xC2DC; &#xBB38;&#xC790;&#xC5F4; &#xC0DD;&#xC131;</p>
        <p>&#xC774;&#xC2A4;&#xCF00;&#xC774;&#xD504;&#xAC00; &#xD544;&#xC694;&#xCE58;
          &#xC54A;&#xC73C;&#xBA70; &#xBAA8;&#xB4E0; &#xBB38;&#xC790; &#xD3EC;&#xD568;
          &#xAC00;&#xB2A5;</p>
        <p>&#xC791;&#xC131;&#xD55C; &#xADF8;&#xB300;&#xB85C; &#xCD9C;&#xB825;&#xB41C;&#xB2E4;&#xACE0;
          &#xC0DD;&#xAC01;&#xD558;&#xBA74; &#xB41C;&#xB2E4;.</p>
        </td>
    </tr>
  </tbody>
</table>```kotlin
val twoQuote = "Hello\nKotlin"
val threeQuote = """Hello\nKotlin
HiHI
"""
```

{% tabs %}
{% tab title="이중 따옴표" %}
```kotlin
val twoQuote = "Hello\nKotlin"
```

**결과**

Hello

Kotlin
{% endtab %}

{% tab title="삼중 따옴표" %}
```kotlin
val threeQuote = """Hello\nKotlin
HiHI
"""
```

**출력**

Hello\nKotlin

HiHI
{% endtab %}
{% endtabs %}

## 문자열 템플릿

* 표현식과 문자열 리터럴을 혼합하기 위해 손쉬운 방법을 제공
* 접두사로 $기호를 사용하며 표현식의 경우 ${표현식}으로 사용한다.

```kotlin
val hello = "Hello"
val kotlin = "kotlin"
println("$hello ${kotlin.toUpperCase()}") // Hello KOTLIN
```

## 참조 사이트

* [코틀린\(Kotlin\) 4. 변수와 타입](https://blog.naver.com/lth9036/221465111524)\|**작성자** [bbaktaeho](https://blog.naver.com/lth9036)

