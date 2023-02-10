---
title:  "☕ [Java] 까먹지말자 subString"
search: false
categories: 
  - AWS
tag:
  - AWS Budget
toc: true
---

> 까먹지 말자 Java substring

<br>

# substring
문자열을 자를 때 사용하는 메소드입니다.

문자열의 특정 부분을 자를 때 사용합니당.

<br>

## Method
- String substring(int start)
- String substring(int start, int end)

## String substring(int start)
start부터 끝까지 문자열을 리턴합니다.

|0|1|2|3|4|5|6|7|
|--|--|--|--|--|--|--|--|
|S|i|e|u|n|p|0|6|

start가 3이라면 3부터 끝까지 잘라서 리턴합니다.

즉, 결과는 "unp06"겠죵?

<br>

- ⭕예시
  ```java
  public static void main(String[] args) {
    String str = "Sieunp06";

    System.out.println(str.substring(3));   // unp06
    System.out.println(str.substring(6));   // 06
  }
  ```
  ```
  unp06
  06
  ```
- ❌예시 - 오류 발생
  ```java
  public static void main(String[] args) {
    String str = "Sieunp06";

    System.out.println(str.substring(-1));   // 오류
    System.out.println(str.substring(6));    // 오류
  }
  ```
  - 음수를 입력했을 때
  - length보다 큰 수를 입력했을 때

### String substring(int start, int end)
start부터 end - 1까지의 문자열을 리턴합니다.

|0|1|2|3|4|5|6|7|
|--|--|--|--|--|--|--|--|
|S|i|e|u|n|p|0|6|

start가 3, end가 5라면 3번 index부터 4번 index까지 잘라 문자열을 리턴합니다.

즉, 결과는 "un"입니당

<br>

- ⭕예시
  ```java
  public static void main(String[] args) {
    String str = "Sieunp06";

    System.out.println(str.substring(3, 5));   // un
    System.out.println(str.substring(2, 4));   // eu
  }
  ```
  ```
  un
  eu
  ```