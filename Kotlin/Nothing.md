#[Kotlin] Nothing

## Nothing

Kotlin에서 `Nothing` 은 다음과 같이 정의되어 있다.

> </br>**Nothing has no instances. You can use Nothing to represent "a value that never exists": for example, if a function has the return type of Nothing, it means that it never returns (always throws an exception).**
>
> ```kotlin
> public class Nothing private constructor()
> ```
>
> </br>

`Nothing` 은 `private 생성자` 로 생성자에 접근 할 수 없어 인스턴스를 가지지 않는다.
`Nothing` 은 어떠한 값이 존재하지 않는다.

</br>

### 특징 및 사용

`Nothing` 은 주로 함수의 리턴 타입으로 사용한다.

#### 1. 반환하지 않는 함수

`Nothing` 을 **무한 루프**나 **항상 예외를 발생시키는 함수**에서 리턴 타입으로 사용하면 함수를 `return(종료)` 하지 않는다.

예를 들어 다음과 같은 코드를 살펴보자.

```kotlin
fun main(){
    infiniteLoop()
    println("end") // Unreachable code
}

fun infiniteLoop(): Nothing {
    while (true) {
        println("Nothing is not always returned.")
    }
}
```

해당 함수는 계속 반복문을 돌기 때문에 함수를 빠져나오지 못할 것이다. `Noting` 을 반환형으로 선언 하면 이를 파악한 컴파일러는 다음 실행 부분인 `println("end")` 이 실행될 수 없음을 파악하고 **Unreachable code** 경고를 띄운다.

대표적으로 `TODO` 함수가 `Nothing` 반환형을 가지는 함수인데, 해당 코드를 구현하지 않으면 경고를 발생시켜 작업이 남아있음을 알릴 때 사용한다.

#### 2. 모든 클래스의 자식 클래스

`Noting` 은 모든 클래스(타입)의 자식 클래스(타입)이다.

_(반대로, Any 는 최상위 루트 타입으로 모든 클래스는 `Any` 를 상속 받는다.)_

엘비스 연산자를 이용한 일반적인 예를 보자.

```kotlin
    val nullableString: String ? = null
    val value : String = nullableString ?: 30 // 30은 오류
```

해당 코드를 보면 `value` 는 **String** 타입으로 지정 되어 있어서 **Int** 타입인 `30` 은 에러가 난다.

</br>

**Nothing** 타입인 `TODO()` 는 `value` 와 연산을 하여도 문제없이 컴파일이 가능하다.
*(이해를 위한 코드이며 실행시, TODO() 에서 NotImplementedError 를 반환한다.)*
```kotlin
    val nullableString: String ? = null
    val value : String = nullableString ?: TODO()
```

#### 3. Null Object 패턴

Kotlin 에서는 null-safety를 지원해서 Null Object 패턴이 필요없다고 생각할 수 있다. 여기서 이야기하는 Null Object 패턴은 조금 다르다.

함수 보면서 Null Object 패턴을 알아보자
```kotlin
fun deleteFiles(files: List<File>? = null) {
    if (files != null) files.forEach { it.delete() }
}
```
다음은 파일 리스트의 값을 전부 삭제하는 함수이다.
파일리스트가 값이 `null` 이 아닌지 확인해주기 위해 조건식으로 체크한다.
**이는 함수내에서 files 를 사용할 때 여러곳에서 `null` 을 확인해야한다.**

이를 방지하기 위해 `Nothing` 을 이용한 `emptyList()` 메소드를 사용하면 간단하게 `null` 체크를 할 필요가 없다.

**기본 라이브러리 함수**
```kotlin
// This function is already defined in the Kotlin standard library
fun emptyList() = object : List<Nothing> {
    override fun iterator(): Iterator<Nothing> = EmptyIterator
    ...
}
```
**사용**

```kotlin
fun deleteFiles(files: List<File> = emptyList()) {
    files.forEach { it.delete() }
}
```


<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

## 📕 참고 문헌

**다음의 링크를 참고했습니다.**

- https://kotlinlang.org/docs/exceptions.html#the-nothing-type
- https://readystory.tistory.com/143
- https://itnext.io/any-unit-nothing-and-all-their-friends-e39613b48235
- https://stackoverflow.com/a/64742576/23145558