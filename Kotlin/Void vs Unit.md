# [Kotlin] Void vs Unit

**목차**

1. [코틀린 기본 타입](<#기본-타입(basic-types)>)
2. [Void](#void)
3. [Unit](#unit?)

## 기본 타입(Basic types)

Unit을 살펴보기 전에 코틀린에서의 기본 타입에 대해 알아보자.

> 💡 자바와 다르게 코틀린의 모든 변수들은 객체로 정의된다.

기본 타입에는 `Numbers(Byte, Int 등)`, `Unsigned integer(UByte, UInt 등)`, `Boolean`, `Char`, `String`, `Array` 가 있다.

자바에서 원시 타입(primitive type)을 사용했던 반면에 코틀린에서는 클래스로 기본 타입을 지정하여 사용한다.

## Void

자바에서 `void` 와 `Void`는 차이가 있다.

`void`(소문자) 는 **원시타입**으로 **반환 값이 존재하지 않음**을 이야기하고 `Void` 는 **객체타입**으로 **객체가 존재하지 않음**을 말한다.

따라서 `Void` 에는 리턴 값으로 `null` 을 반환 해야 한다.

## Unit?

[kotlin 공식문서](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/) 에는 다음과 같이 설명한다.

> `Unit` 은 자바에서 `void` 와 대응되는 타입(객체)이다.

참고) `Unit`은 싱글톤 인스턴스이다.

<br/>

코틀린의 기본 함수를 보자.

```kotlin
fun printHello(): Unit {
    println("Hello World!")
}
```

아무런 값을 반환하지 않을 때는 `Unit` 타입으로 지정한다.

<br/>

반환타입이 Unit의 경우는 다음과 같이 생략가능하다.

```kotlin
fun printHello() {
    println("Hello World!")
}
```

### 왜 Unit을 사용하는 가?

그렇다면 코틀린에서는 왜 `Unit` 을 사용하는 것 일까?

앞서 말했듯이 코틀린에서는 변수의 기본타입을 전부 클래스로 감싸 표현하고 있다.

기본적으로 자바에서 **참조형(클래스)으로 아무값도 반환하지 않기 위해**서는 앞서 말한 `Void`를 사용해야 할 것이다.

하지만 이렇게 되면 **`null`을 반환해야 하기 때문에** `void`와 같이 사용하기 어렵다. 따라서 kotlin 에서는 `Unit` 이라는 객체 타입을 지원한다.

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

## 📕 참고 문헌

**다음의 링크를 참고했습니다.**

- https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/
- https://kotlinlang.org/docs/functions.html#single-expression-functions
- https://www.baeldung.com/kotlin/void-type
