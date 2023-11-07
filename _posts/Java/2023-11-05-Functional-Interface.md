---
title:  "[☕Java] 함수형 인터페이스와 람다식"
search: false
categories: 
  - Java
tag:
  - 우아한테크코스 프리코스 6기
toc: true
---

> 함수형 인터페이스 처음 보는 사람 다 모여

## 함수형 인터페이스(Functional Interface)란?
`함수형 인터페이스`는 Java 8부터 지원하는 기능으로 추상 메서드가 오직 하나인 인터페이스를 말한다.

```java
@FunctionalInterface
public interface FunctionalInterfacePractice {
    int calculate(int x, int y);
}
```

`함수형 인터페이스`는 추상 메서드가 하나만 있으면 되기 때문에, `default method`와 `static method`가 있어도 된다.
```java
@FunctionalInterface
public interface FunctionalInterfacePractice {
    int calculate(int x, int y);

    static int calPlus(int x, int y) {
        return x + y;
    }

    default int calMulti(int x, int y) {
        return x * y;
    }
}
```

### @FunctionalInterface 어노테이션
`@FunctionalInterface`는 함수형 인터페이스인 것을 나타내기 위해 사용한다.

이 어노테이션이 사용되면 함수형 인터페이스가 아닌 경우, 컴파일 에러를 발생시킨다.

### 함수형 인터페이스와 람다식
함수형 인터페이스를 사용하면 람다식을 사용할 수 있다.

만약 람다식을 사용하지 않는다면, 익명 클래스로 함수형 인터페이스를 사용할 수 있다.
```java
@FunctionalInterface
public interface FunctionalInterfacePractice {
    int calculate(int x, int y);
}
```
```java
MyFunction myFunction = new MyFunction() {
    @Override
    public int calculate(int x, int y) {
        return x + y;
    }
};
System.out.println(myFunction.calculate(5, 6)); // result: 11
```

이 코드를 람다식으로 변경한다면 다음과 같이 변경할 수 있다.
```java
MyFunction myFunction = (x, y) -> x + y;
System.out.println(myFunction.calculate(5, 6)); // result: 11
```

### 

## 대표적인 함수형 인터페이스
자바 내부에 미리 정의된 함수형 인터페이스가 있다. 그 중 대표적인 함수형 인터페이스들을 정리해보려고 한다. 
> [링크](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html)를 누르면 자바 내부에 미리 정의된 모든 함수형 인터페이스들을 확인할 수 있다.
### Function<T, R>
`Function<T, R>`은 T타입 인자를 받아 R타입으로 매핑할 때 사용한다. 즉, 타입 변환이 목적일 때 사용한다.

```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);
}
```
아래 예시는 Integer 타입의 인자를 받아 String 타입으로 반환한다.

```java
Function<Integer, String> function = (age) -> age + "살 입니다.";
System.out.println( function.apply(20));    // result: 20살 입니다.
```

### Consumer\<T>
`Consumer<T>`는 T타입 인자를 받아서 소비한다.

```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);
}
```
아래 예시는 Integer 타입의 매개변수를 받아 이를 출력한다.

```java
Consumer<Integer> consumer = (i) -> System.out.println(i);
consumer.accept(6);     // result: 6
```

### Predict\<T>
`Predict<T>`는 T 타입 인자를 받아서 boolean 값을 반환한다.
```java
@FunctionalInterface
public interface Predicate<T> {
    boolean test(T t);
}
```
Integer 타입의 매개변수가 3보다 클 때 true를, 그렇지 않으면 false를 리턴한다.

```java
Predicate<Integer> predicate = (i) -> i > 3;
System.out.println(predicate.test(6));  // result: true
System.out.println(predicate.test(1));  // result: false
```

### Supplier\<T>
`Supplier<T>`는 매개변수가 필요하지 않고, T 타입 값을 반환한다.
```java
@FunctionalInterface
public interface Supplier<T> {
    T get();
}
```

```java
Supplier<Integer> supplier = () -> 3;
System.out.println(supplier.get());
```

## References
- https://bcp0109.tistory.com/313
- https://tecoble.techcourse.co.kr/post/2020-07-17-Functional-Interface/
- https://docs.oracle.com/javase/specs/jls/se8/html/jls-9.html#jls-9.6.4.9
- https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html
- https://hudi.blog/functional-interface-of-standard-api-java-8/
- https://developer-talk.tistory.com/460