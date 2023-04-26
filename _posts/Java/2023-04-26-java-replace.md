---
title:  "☕ [Java] 까먹지말자 replace, replaceAll, replaceFirst"
search: false
categories: 
  - Java
tag:
  - Java
toc: true
---

> 까먹지 말자 Java replace, replaceAll, replaceFirst

<br>

# replace와 replaceAll

특정 문자 및 문자열을 치환하는 기능을 하는 메소드입니다. 

replace 말고도 replaceAll과 replaceFirst가 존재합니다.

## Method
- replace(char oldChar, char newChar)
- replace(CharSequence target, CharSequence replacement)
- replaceAll(String regex, String replacement)

## replace(char oldChar, char newChar)
특정 문자 `oldChar`을 `newChar`로 치환합니다.

```java
String text = "mesquite in your cellar";

text = text.replace('e', 'o');

System.out.println(text);
```
```
mosquito in your collar
```
`text`의 모든 `oldChar`이 `newChar`로 치환된 것을 볼 수 있습니다.

## replace(CharSequence target, CharSequence replacement)
특정 문자열을 치환하는 것도 가능할까요?

당연히 가능합니다.

```java
String text = "mesquite in your cellar";

text = text.replace("in", "out");

System.out.println(text);
```
```
mesquite out your cellar
```
`target`이 `replacement`로 치환된 것을 볼 수 있습니다.

## replaceAll(String regex, String replacement)
`replaceAll`은 replace와 마찬가지로 문자열이 치환됩니다.

```java
String text = "mesquite in your cellar";

text = text.replaceAll("in", "out");

System.out.println(text);
```
```
mesquite out your cellar
```
엇 그럼 차이점이 뭘까요?

## replace와 replaceAll의 차이점
replace와 replaceAll은 같은 기능을 하는데 왜 같은 기능을 하는 메서드를 만들었을까요?

`여기서 잠깐..`

둘은 같지 않습니다. 

replace와 replaceAll의 인자값을 살펴보면 replace는 `CharSequence target`, replaceAll은 `Sting regex`인 것을 알 수 있습니다.

- regex(정규 표현식 or 정규식)란?
  - 문자열에서 특정 문자 조합을 찾기 위한 패턴
  - https://learn.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference


예를 들어 정규식으로써의 `.`은 문자열 전체를 의미합니다.

- `replace`
  ```java
  String text = "what..?";

  text = text.replace(".", ",");

  System.out.println(text);
  ```
  ```
  what,,?
  ```
- `replaceAll`
  ```java
  String text = "what..?";

  text = text.replaceAll(".", ",");

  System.out.println(text);
  ```
  ```
  ,,,,,,,
  ```
위 예를 보시면 `replaceAll`을 사용했을 때에는 `.`을 regex로 인식해 모든 문자를 치환한 것을 볼 수 있습니다.

# replaceFirst
`replace`와 `replaceAll`이 문자열 내의 모든 target을 치환한다면, `replaceFirst`는 첫 번째로 해당하는 문자열만 치환합니다.

## Method
- replaceFirst(String regex, String replacement)

## replaceFirst(String regex, String replacement)
```java
String text = "mesquite in your cellar, not in my cellar";

text = text.replaceFirst("in", "on");

System.out.println(text);
```
```
mesquite on your cellar, not in my cellar
```

# Reference
- https://coding-factory.tistory.com/128
- https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html