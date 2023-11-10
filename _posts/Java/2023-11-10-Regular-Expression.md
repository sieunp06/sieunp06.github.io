---
title:  "[☕Java] 정규표현식 어떻게 보는건데"
search: false
categories: 
  - Java
tag:
  - 우아한테크코스 프리코스 6기
toc: true
---

> 정규표현식 드디어 공부한다.

# 정규 표현식(Regular Expression)
> 정규 표현식은 특정한 규칙을 가진 문자열의 집합을 표현하는 데 사용하는 형식 언어이다.

라고~ 위키 백과가 말한다.

이러한 정규 표현식은 보통 전화번호나 이메일이 가진 형식들을 이용해서 유효성을 검사할 때 주로 쓰인다.

## 정규식 문법 - 기호
|기호|설명|예제|
|-------|----------|---------|
|<center>^</center>|문자열의 시작<br>[ ] 안에 있으면 NOT의 의미|`^a`: a로 시작하는 단어<br>`[^a]`: a가 아닌 철자인 문자 하나|
|<center>&</center>|`$` 앞의 문자열로 문자가 끝나는지|`a$`: a로 끝나는 단어|
|<center>[ ]</center>|`[]` 안에 문자가 있는지|`[ab][cd]`: a와 b 중 한 문자 <br> ex) ac ad bc bd|
|<center>[^]</center>|`[]` 안에 `^`가 있으면 NOT의 의미를 가진다.|`[^a-z]`: a와 z 사이의 문자를 제외한 모든 문자|
|<center>^[ ]</center>|`[]` 밖에 `^`가 있으면 시작의 의미를 가진다.|`^[a-z]`: a와 z 사이의 문자로 시작하는 문자|
|<center>-</center>|`-`의 앞, 뒤 사이의 문자를 의미한다.|`[a-z]`: a와 z 사이의 문자 중 하나<br>`[a-z0-9]`: 알파벳 소문자나 0부터 9 사이의 숫자 중 하나|
|<center>\|</center>|또는|`[a\|b]`: a 혹은 b|
|<center>()</center>|그룹, 소문자 안의 문자를 하나의 문자로 인식한다.<br>[자세한 내용은 아래에!](#정규식-문법---그룹)|`01(0\|1)`: 01 뒤에 0 또는 1이 들어간다.<br>ex) 010, 011|
|<center>{}</center>|회수 또는 범위를 나타낸다.<br>[자세한 내용은 아래에!](#정규식-문법---수량)|`a{3}b`: a가 3번 나온 후 b가 온다.<br> ex) aaab|
|<center>\b</center>|공백, 탭, ` , `, ` / ` 등을 나타낸다.|`apple\b`: apple 뒤 공백이나 탭 등이 있다.<br>ex) apple juice (o), applepie (x)|
|<center>\B</center>|`\b`의 반대|`apple\B`: apple 뒤 공백이나 탭 등이 없다.<br>ex) applepie (o), apple juice(x)|
|<center>\d</center>|0 ~ 9 사이의 숫자를 나타낸다.|`apple\d`: apple 뒤 0 ~ 9 사이의 숫자가 있다.<br>ex) apple3 (o), apple3r (x), appler3 (x)|
|<center>\D</center>|`\d`의 반대|`apple\D`: apple 뒤 0 ~ 9 사이의 숫자가 없다.|
|<center>\s</center>|공백이나 탭을 의미한다.|`apple\s`: apple 뒤에 공백이 나타난다.|
|<center>\S</center>|`\s`의 반대|`apple\S`: apple 뒤에 공백이 나타나지 않는다.|
|<center>\w</center>|알파벳 소문자와 대문자, 숫자 그리고 "_"를 의미한다.<br>`[a-zA-z_0-9]`와 동일하다.||
|<center>\W</center>|`\w`의 반대, 즉 `[^a-zA-z_0-9]`와 같다.||

## 정규식 문법 - 수량
|기호|설명|예제|
|---|---|---|
|<center>?</center>|`?` 앞의 문자이 없거나 최대 한개만 존재한다.|`a1?`: 1이 없거나 1개만 있을 수 있다.<br>ex) a (o), a1 (o), a11 (x)|
|<center>*</center>|`*` 앞의 문자이 없을 수도 있을 수도 있다.|`a1*`: 1이 없을 수도 있을 수도 있다.<br>ex) a (o), a1 (o), a11 (o)|
|<center>+</center>|`+` 앞의 문자이 한 개 이상 존재한다.|`a1+`: 1이 한 개 이상 있을 수 있다.<br>ex) a (x), a1 (o), a11 (o)|
|<center>{n}</center>|`{n}` 앞의 문자가 n개 존재한다.|`a{4}`: a가 4개 있다.<br>ex) aaaa|
|<center>{n, m}</center>|`{n, m}` 앞의 문자가 n개 이상 m개 이하 존재한다.|`a{2,4}`: a가 2개 이상 4개 이하 있다.<br>ex)aa (o), aaa (o), aaaa (o), aaaaa (x)|
|<center>{n,}</center>|`{n,}` 앞의 문자가 n개 이상 존재한다.|`a{2,}`: a가 n개 이상 있다.<br>ex) a (x), aa (o), aaa (o)|

## 정규식 문법 - 그룹
|기호|설명|예제|
|--|--|--|
|<center>()</center>|그룹, 소문자 안의 문자를 하나의 문자로 인식한다.|`01(0\|1)`: 01 뒤에 0 또는 1이 들어간다.<br>ex) 010, 011|
|<center>(?:)</center>|그룹에 포함하지 않음.||
|<center>(?=)</center>|=앞 문자를 기준으로 전방 탐색||
|<center>(?<=)</center>|=뒤 문자를 기준으로 후방 탐색||

## 자주 사용되는 정규 표현식
|정규 표현식|설명|
|--|--|
|<center>^[0-9]*$</center>|숫자|
|<center>^[a-zA-Z]*$</center>|알파벳(소문자, 대문자)|
|<center>^[가-힣]*$</center>|한글|
|<center>\\w+@\\w+\\.\\w+(\\.\\w+)?</center>|이메일
|<center>^\d{2,3}-\d{3,4}-\d{4}$</center>|전화번호|
|<center>^01(?:0|1|[6-9])-(?:\d{3}|\d{4})-\d{4}$</center>|휴대전화번호|
|<center>\d{6} \- [1-4]\d{6}</center>|주민등록번호|
|<center>^\d{3}-\d{2}$</center>|우편번호|

# references
- https://ko.wikipedia.org/wiki/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D
- https://www.w3schools.com/java/java_regex.asp
- https://coding-factory.tistory.com/529
- https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EC%A0%95%EA%B7%9C%EC%8B%9DRegular-Expression-%EC%82%AC%EC%9A%A9%EB%B2%95-%EC%A0%95%EB%A6%AC