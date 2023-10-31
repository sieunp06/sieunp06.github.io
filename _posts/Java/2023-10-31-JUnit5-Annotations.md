---
title:  "[☕Java] JUnit5의 어노테이션"
search: false
categories: 
  - Java
tag:
  - Test
  - 우아한테크코스 프리코스 6기
toc: true
---

> JUnit5의 어노테이션을 정리해보았다.

우테코 프리코스 2주차 `자동차 경주` 미션에 `JUnit5`와 `AssertJ`를 사용하여 기능 목록이 정상 동작함을 확인하라는 요구사항이 추가되었다. 

공부.. 해야겠지..?


# JUnit5의 어노테이션들

## @Test
해당 메서드가 테스트 메서드임을 나타낸다.
```java
@Test
void test_name() {
}
```

## @Disabled
해당 클래스 또는 메서드를 사용하지 않을 때 사용한다.

## @DisplayName
테스트 클래스나 테스트 메서드의 이름을 정할 수 있다.
```java
@Test
@DisplayName("테스트 이름")
void test_name() {
}
```

## @DisplayNameGeneration
테스트 클래스나 테스트 메서드의 이름을 사용자가 설정한 전략에 따라 알아서 처리하여 이름을 정할 수 있다.
- Standard : 기존 클래스, 메서드 명을 사용한다(기본값)
- Simple : 괄호를 제외시킨다.
- ReplaceUnderscores : 언더스코어(_)를 공백으로 바꾼다.
- IndicativeSentences : 클래스명 + 구분자(", ") + 메서드명을 바꾼다.
```java
@DisplayNameGeneration(DisplayNameGenerator.ReplaceUnderscores.class)
public class A_year_is_not_supported {
}
```
`ReplaceUnderscores`로 설정하였으므로 `A year is not supported`로 테스트 이름이 나타나게 된다.

## @BeforeEach, @AfterEach
테스트 메서드를 실행하기 전후에 실행되어야 하는 메서드에 사용한다.

`@BeforeEach`는 테스트 메서드를 실행되기 전에, `@AfterEach`는 테스트 메서드가 실행된 후에 실행된다.

`@Test`, `@RepeatedTest`, `@ParameterizedTest`, `@TestFactory`가 붙은 메서드가 실행되기 전후에 실행된다.

## @BeforeAll, @AfterAll
`@BeforeEach`와 `@AfterEach`는 각 테스트 메서드마다 실행되지만, 해당 어노테이션은 테스트가 시작되기 전 후에 한번씩만 실행된다.

## @ParameterizedTest
매개변수를 받는 테스트를 작성할 수 있다.
`@Test` 대신에 `@ParameterizedTest`를 입력하면 된다.
### @ValueSource
테스트에 주입할 값을 어노테이션에 배열로 지정한다. 

하나의 테스트에는 하나의 파라미터만 전달할 수 있다.

`@ValueSource`에는 다음 자료형만 사용할 수 있다. 

- `short`, `byte`, `int`, `long`, `float`, `double`, `char`, `boolean`
- `String`, `Class`
```java
@ParameterizedTest
@ValueSource(ints = {1, 2, 3})
void valueSource_test_name(int number) {
}
```
### @CsvSource
`@ValueSource`와 달리 여러 파라미터를 전달할 때 사용한다.

주로 입력 값과 기대 값을 함께 전달하여 테스트할 때 사용한다.

```java
@ParameterizedTest
@CsvSource(value = {"1,2", "2,4", "3,6"})
void test_name(int input, int expected) {
}
```
위 코드는 콤마(,)로 구분하여 `input`과 `expected`로 나뉜다.
```java
@ParameterizedTest
@CsvSource(value = {"1:2", "2:4", "3:6"}, delimiter = ":")
void test_name(int input, int expected) {
}
```
`delimeter` 값을 정의해서 구분자를 `:`로 바꿔줄 수 있다.

### @NullSource, @EmptySource, @NullAndEmptySource
- `@NullSource` : 테스트 메서드에 인수로 `null`을 전달한다.
- `@EmptySource` : 테스트 메서드에 `빈 값`을 전달한다.
- `@NullAndEmptySource` : `null`과 `빈 값` 모두를 전달한다.



### @EnumSource
`Enum`을 테스트 메서드에 전달한다.

```java
@ParameterizedTest
@EnumSource(value = Month.class)
void test_name(Month month) {
}
```

#### names
`names` 속성을 사용하면 값을 선택할 수 있다.
```java
@ParameterizedTest
@EnumSource(value = Month.class, names = {"March", "June"})
void test_name(Month month) {
}
```
`names` 속성에 정규식을 전달할 수도 있다.
```java
@ParameterizedTest
@EnumSource(value = Month.class, names = ".+BER")
void test_name(Month month) {
}
```

#### mode
`names`를 사용하면 `mode` 값을 사용할 수 있다.

`mode`의 종류는 다음과 같다.
- INCLUDE : `names`와 일치하는 모든 Enum 값(기본값)
- EXCLUDE : `names`를 제외한 모든 Enum 값
- MATCH_ANY : 조건을 하나라도 만족하는 Enum 값
- MATCH_ALL : 조건을 모두 만족하는 Enum 값

```java
@ParameterizedTest
@EnumSource(value = Month.class, names = {"March", "June"}, mode = EnumSource.Mode.MATCH_ANY)
void test_name(Month month) {
}
```

## references
- https://junit.org/junit5/docs/current/user-guide/
- https://velog.io/@chaerim1001/Java-JUnit5-%EA%B8%B0%EC%B4%88-%EC%A0%95%EB%A6%AC
- https://velog.io/@ohzzi/junit5-parameterizedtest
- https://velog.io/@new_wisdom/Junit
- https://effortguy.tistory.com/200