---
title:  "🌺 [React][ERROR] [eslint] plugin "react" was conflicted between 'package.json' and 'eslint-config-react-app'"
search: false
categories: 
  - React
tag:
  - Error
toc: true
published: true
---

> 나에게 너무 어려운 프론트엔드

<br>

## [eslint] plugin "react" was conflict between 에러

스프링부트 연습용 프로젝트에 리액트를 사용하는데, vs code로 리액트 코드를 실행시켰더니 발생한 오류다.

전엔 안나왔으면서 왜 지금 갑자기 나오는건진 모르겠지만..!

![error1](../../assets/images/post/React/230225-react-eslint-plugin-error.png)

## 해결 방법

구글링 결과, 나의 경우는 그냥 프로젝트명에 대문자가 포함되어 있어서였다.

리액트는 디렉토리 명에 대문자가 포함되면 안되나보다!

혹시 같은 문제가 발생한 경우, 대문자가 포함된 디렉토리가 있는지 확인해보자!

<br>

- reference

  https://dev.to/iamatifriaz/how-to-fix-error-in-plugin-react-was-conflicted-between-packagejson-and-eslint-config-react-app-365d