---
title:  "π± [Error][Github Blog] did not find expected key while parsing a block a block mapping at line 2 column 1"
search: false
categories: 
  - Git
tag:
  - Github Blog
toc: true
---

> μ ν¬μ€νμ΄ μλλ νλλ°..

<br>

## did not find expected key while parsing a block a block mapping at line 2 column 1 

![error-1](../../assets/images/post/Git/230225-error-1.png)

μλ¬ λ©μΈμ§λ₯Ό λ³΄λ©΄ line 2 column 1μ΄ λ¬Έμ λΌλλ°, νμΈν΄λ³΄λ `title`μ΄μλ€.

κ΅¬κΈλ§ ν΄λ³΄λ μ λͺ©μ λ°μ΄νκ° ν¬ν¨λμ΄ μμ΄ λ°μνλ μλ¬λΌκ³  νλ€.

![error-2](../../assets/images/post/Git/230225-error-2.png)

λ°μ΄νλ₯Ό μ­μ νλΌκ³  νλλ° νΉμ `\"`λ‘ λ°κΎΈλ©΄ λ κΉ μΆμ΄μ λ°κΏλ΄€λ€!

![error-3](../../assets/images/post/Git/230225-error-3.png)


## μλ¬ μμΈ
- `title`μ λ°μ΄νκ° ν¬ν¨λμ΄ μμ΄μ λ°μν¨.

## ν΄κ²° λ°©λ²
λ μ€ νλ μ ννλ©΄ λ  κ² κ°λ€!

- λ°μ΄νλ₯Ό μ­μ νλ€.
- `"`λ₯Ό `\"`λ‘ λ³κ²½νλ€.
  - μ 
    ```
    title: λ°μ΄νλ₯Ό "λ°μ΄ν"
    ```
  - ν
    ```
    title: λ°μ΄νλ₯Ό \"λ°μ΄ν\"
    ```


Reference
- https://younginshin115.github.io/debug/1-debug-blog4/