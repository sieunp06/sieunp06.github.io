---
title:  "๐ [Spring Boot] ์คํ๋ง๋ถํธ localhost ์คํ์ ๋ก๊ทธ์ธ ํ๋ฉด์ด ๋์ฌ ๋"
search: false
categories: 
  - SpringBoot
tag:
  - Error
toc: true
---

> ์ด๊ฑธ ๋ชฐ๋ผ์ ์ปดํจํฐ ์ด๊ธฐํํ ์ฌ๋์ด ์ ๋๋ค.

<br>

## ์ง์ฌ์ผ๋ก ๋นํฉํ๋ ์ฌ๋์ ์๋ก 

์ด์ธ 7์๊ฐ์ด ์ง๋ ์ผ์๋๋ค..

ํ์ ๋ถ๊ป์ security์ thymeleaf dependency๋ฅผ ์ถ๊ฐํด์ฃผ์์..

์ ๋ ๊ทธ๋ฅ ํ์ ๋ฐ๊ณ  localhost๋ฅผ ๋๋ฆฐ ๊ฒ์ด์ฃ ..

๊ทธ๋ฐ๋ฐ..!!!!!!!!

![spring-boot-login-error-2](../../assets/images/post/SpringBoot/230323-spring-boot-login-error-2.png)

(?ใ?)???????????????

๊ตฌํํ์ง๋ ์์ ๋ก๊ทธ์ธ ํ๋ฉด์ด ๋์ค๋ ๊ฒ๋๋ค!!!!!

์๊ทธ๋๋ ํ์์ด ์ต์ํ์ง ์์ ์ ๋ ์ง์ฌ์ผ๋ก ๊ฐ๋ด์ด ์๋ํ์ต๋๋ค.

๋ฌผ๋ก  ํ์์๋ ์ํฅ์ด ์๋ค๋ ๊ฑธ ์๊ณ  ์์์ง๋ง.. ์ด ๋ฌธ์ ๊ฐ ์ง์๋๋ค๋ฉด ์์ผ๋ก์ ๊ฐ๋ฐ ์ผ์ ์ ๋งค์ฐ ํฐ ์ฐจ์ง์ด ์์ ์๋ ์๊ฒ ๋ค๊ณ  ํ๋จํ๊ณ ..

์ ๋ ๋น ๋ฅด๊ฒ ๊ฒฐ์ ์ ๋ด๋ ธ์ต๋๋ค..

`์ด ๊ธฐ ํ`ํ๊ธฐ๋ก..

(๋จธ๋ฆฌ๊ฐ ๋์๋ฉด.. ๋ชธ์ด.. ๊ณ ์.. ์์..)

## ํด๊ฒฐ ๋ฐฉ๋ฒ

์ฌ์ค ํด๊ฒฐ ๋ฐฉ๋ฒ์ด๋ผ๊ณ  ํ๊ธฐ๋ ๋ญํ๊ฒ, ๋น์ฐํ ๋์ค๋ ๊ฑฐ๋ผ๊ณ  ํ๋๋ผ๊ณ ์.

ํน์ `security depency`๋ฅผ ์ถ๊ฐํ์ง ์์ผ์จ๋์?!

๊ทธ๋ฅ ๋ก๊ทธ์ธ ํ๋ฉด์ด ๋์ค๋ฉด

> ์์ด๋ : user
> ๋น๋ฐ๋ฒํธ : [์ฝ์์ฐฝ์ ๋์ค๋ password ์๋ ฅ]

![spring-boot-login-error-3](../../assets/images/post/SpringBoot/230323-spring-boot-login-error-3.png)

๋น๋ฐ๋ฒํธ๋ ์ด๋ฐ ์์ผ๋ก ์ฝ์์ฐฝ์ ๋์ต๋๋ค.

(์ ๋ ์ด๊ฑธ ๋ณด๊ณ ๋ ์ ๋ชฐ๋์๊น์)

![spring-boot-login-error-4](../../assets/images/post/SpringBoot/230323-spring-boot-login-error-4.png)

์ด๋ ๊ฒ ๋ก๊ทธ์ธ ํ์๋ฉด ๋ฉ๋๋ค.

๊ทธ๋ผ ์๋ง ์ ๋์ค์ค๊ฑฐ์์...


-------------------------

![spring-boot-login-error-1](../../assets/images/post/SpringBoot/230323-spring-boot-login-error-1.png)

(๊นจใก๋)

์ใใ ๊ฒฐ๊ณผ์ ์ผ๋ก ๊นจ๋ํ๊ฒ ์ ๋ฆฌํ์ผ๋ฉด ๋์ง ๋ญ~