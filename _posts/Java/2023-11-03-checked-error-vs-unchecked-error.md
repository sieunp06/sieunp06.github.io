---
title:  "[☕Java] Checked Exception과 Unchecked Exception, 그리고 Exception 종류"
search: false
categories: 
  - Java
tag:
  - 우아한테크코스 프리코스 6기
toc: true
---

> Checked Exception과 Unchecked Exception 알아보면서 Exception 종류도 알아보기

# Exception
자바는 Exception을 두 가지로 구분한다.
- Unchecked Exception
- Checked Exception

간단하게 표현하면, `Unchecked Exception`은 런타임 예외 클래스들이고, `Checked Exception`은 컴파일 예외 클래스들이다.

## Exception의 종류
![Java Exceptions Hierarchy](../../assets/images/post/Java/2023-11-03-Checked-Exception-vs-Unchecked-Exception/Java%20Exception%20Hierarchy.png)

자바의 예외 클래스의 계층 구조를 나타낸 그림이다.

> 이 [링크](https://programming.guide/java/list-of-java-exceptions.html)에서 자바의 Exception들을 확인할 수 있다. <br>
>✔ 표시가 된 exception들은 Checked Exception이다.


# Unchecked Exception과 Checked Exception

## Unchecked Exception
`Unchecked Exception`은 `RuntimeException`을 상속받은 클래스로 에러 처리가 강제되지 않는다.

런타임 단계에서 확인이 가능하다. 개발자가 예외처리를 하지 않더라도 알아서 에러가 발생하게 된다.

대표적으로 다음 Exception이 `Unchecked Exception`에 해당한다.
- IllegalArgumentException
- IllegalStateException
- NullPointerException
- IndexOutOfBoundsException
- ConcurrentModificationException
- UnsupportedOperationException

## Checked Exception
`Checked Exception`은 `RuntimeException`을 상속받는 클래스를 제외하고 `Exception`을 상속 받는 클래스들이 해당한다.

컴파일 시점에서 확인한다. 체크 시점이 컴파일 단계이기 때문에, 예외처리를 하지 않으면 컴파일 자체가 되지 않는다. 

즉,`Checked Exception`은 `Unchecked Exception`과 다르게 `try-catch`나 `throw`로 반드시 에러 처리를 해야 한다.


대표적으로 다음 Exception이 `Checked Exception`에 해당한다.
- IOException
- SQLException
- FileNotFoundException
- ClassNotFoundException
- InterruptedException


# reference
- https://rollbar.com/blog/java-exceptions-hierarchy-explained/
- https://programming.guide/java/list-of-java-exceptions.html
- https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EC%97%90%EB%9F%ACError-%EC%99%80-%EC%98%88%EC%99%B8-%ED%81%B4%EB%9E%98%EC%8A%A4Exception-%F0%9F%92%AF-%EC%B4%9D%EC%A0%95%EB%A6%AC#%EC%98%A4%EB%A5%98error_%EC%99%80_%EC%98%88%EC%99%B8exception
- https://seungjjun.tistory.com/250
- [이펙티브 자바 3/e](https://product.kyobobook.co.kr/detail/S000001033066)