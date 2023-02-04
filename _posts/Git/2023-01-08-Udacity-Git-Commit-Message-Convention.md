---
title:  "🐱 Udacity의 Git Commit Message Convention"
search: false
categories: 
  - Git
tag:
  - Commit Message
toc: true
---

> 🔥Udacity의 Git Commit Message Style Guide에 대해 간단히 알아보자!🔥

<br>

# Udacity의 Git Commit Message Style Guide
Udacity에서는 이상적인 Commit Message에 대한 의견이 다양하게 존재하기 때문에, 혼란을 줄이기 위해 학생들이 따를 수 있도록 Git Commit Message에 대한 가이드를 내놓았습니다.

<br>

## 🌟메세지의 구조
Udacity에서 권장하는 구조는 이 세 가지로 이루어져 있습니다.

- Type: Subject (필수)
- Body (선택)
- footer (선택)

보시다시피 Type과 Subject는 필수적으로 작성해야 하고, Body와 footer는 선택적으로 필요하다고 판단되면 작성하시면 됩니다.

각각의 구조에 대해서 자세히 알아봅시다!

<br>

## ✨Message Type

총 7가지로 이루어져 있습니다.

[깃 모지(Gitmoji)](https://gitmoji.dev/)를 사용해서 이 타입들을 이모지로 표현하는 방식을 대신 하기도 합니다.

> feat: 새로운 기능 추가 <br>
> fix: 버그 수정 <br>
> docs: 문서 수정 <br>
> style: 포맷 수정, 세미콜론(;) 추가 등, 코드의 내용이 수정되지 않을 때 <br>
> refactor: 리팩토링을 했을 때(기능 변경은 없어야 함.) <br>
> test: 테스트 코드 추가, 테스트 리팩터링 등을 수행했을 때 <br>
> chore: 빌드 작업, 패키지 관리자 구성 등을 수행했을 때 <br>

<br>

## ✨Subject
- 50자 이하여야 하며, 대문자로 시작하고 마침표로 끝나지 않아야 한다.
- 명령형을 사용하여 커밋이 하는 일을 설명한다.
- 명령문을 사용하고, 과거형을 사용하지 않는다.

<br>

## ✨Body
- 선택 사항
- Subject에서 담지 못한 상세 내역을 작성한다.
- 72자 이내로 작성해야 한다.
- 이 커밋이 뭔지, 왜 이 커밋을 했는지에 대해 작성한다.

<br>

## ✨Footer
선택 사항
이슈 트래커 ID를 레퍼런스 한다.
 
<br>
<br>

## 💎Reference
- [https://udacity.github.io/git-styleguide/]()