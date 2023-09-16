---
title:  "CICD 계획 변화에 대해"
search: false
categories: 
  - Lire_Livre
tag:
  - Lire_Livre
  - Plan
  - CICD
toc: true
---

`Lire Livre` 프로젝트의 CI/CD 계획과 구현 과정에 대해 작성해보려고 한다.

# 초기 CSP 선정

> **CSP(Cloud Service Provider)란?**
>
> CSP는 클라우드 컴퓨팅 제공 업체로, 대표적인 해외 업체로는 AWS(amazon), Azure(MS) 등이 존재하며, 국내 업체로는 Naver Cloud Platform 등이 있다.

## AWS와 Github Actions

`Lire Livre` 프로젝트는 `Github Actions`와 `AWS`를 사용하여 CI/CD를 하기로 하였다.

### 선정 이유

`AWS`와 `Github Actions`를 사용하기로 가장 큰 이유는 비슷한 규모(?)의 다른 프로젝트에서 `AWS`와 `Github Actions`를 사용하여 CI/CD를 구축한 경험이 있기 때문이다.

사실 단 두 명의 인원으로 진행하는 팀 프로젝트였고 각자 학교 일정도 있었기 때문에, CI/CD의 경우 경험이 있는 기술을 사용하는 것으로 결정하였다.
### 계획(이었던 것)
사용자에게 맞춤 도서를 추천하는 기능을 구현하기 위해 `Flask`를 사용하여 추천 시스템을 구현하려고 했다.
이에 따라 `spring boot`와 `Flask` 두 개의 인스턴스를 만들어서 사용하려고 했었다.

그런데, 문제가 발생하였다.

# 어라
교양 수업 쉬는 시간이었다. 
내가 무슨 생각이었는지 모르겠지만, `AWS`의 프리티어 정책을 보게 되었다.
(진짜 어쩌다 보게 됐는지 기억 안남)

> **AWS 프리티어 정책**
>
> EC2의 경우, 12개월 동안 매월 최대 750시간을 제공한다.<br>
> https://aws.amazon.com/ko/ec2/?did=ft_card&trk=ft_card

사실 한 달을 30일로 놓고 계산을 해보면 750시간 / 30일 = 약 25시간/일로, 하루에 약 25시간을 가동할 수 있기 때문에, 하나의 인스턴스 가동시간으로 생각하면 넉넉한 시간이다.

그런데, 만약 계획과 같이 `spring boot` 서버와 `flask` 서버 두 개의 인스턴스를 동시에 가동할 경우, 두 인스턴스의 가동 시간이 750시간이 초과되니 요금이 부과될 것 같았다.

## 생각해봤던 것들
학교에 가고 있던 팀원과 교양을 듣고 있던 나는 이 사실에 잠시 "어라" 싶었고, 생각을 했어야 했다.

크게 아래 두 가지 방법을 생각해봤었다.

1. `Flask`로 추천 api를 구현하지 말고, `mahout`을 사용하여 간단한 추천 시스템을 자바로 구현하자.
2. 다른 CSP를 찾아보자.

### mahout
가장 먼저 `Flask`서버를 추천 시스템 구현이 가능한 라이브러리로 대체하는 것을 고려해봤다.

https://mahout.apache.org/
mahout 라이브러리는 하둡(hadoop)위에서 작동되는 머신러닝 라이브러리이다.

간단히 조사를 진행해보니, `Collaborative Filtering`, `User based Recommend`, `Item based Recommend`가 가능한 것 같았다.

### AWS 이외의 다른 CSP
AWS 이외의  다른 CSP도 조사를 해봤었는데, 다른 CSP 모두 AWS와 비슷한 무료 정책을 가지고 있었다.(ㅠㅠㅠ)

# 결론
사실 구현하고자 하는 추천 시스템이 `mahout`을 사용해도 충분할 것 같다는 생각이 들었다.

처음 기획을 할 때, `Item based Recommend` 구현을 원했고, 팀원과 나 모두 `Flask`를 다뤄본 적 없으며 `python`보다는 `java` 숙련도가 더 높기 때문에 `Flask` ai 서버 구현을 포기하고 구현 하려던 기능을 `mahout`으로 구현하기로 결정했다.

다음 글은 `Lire Livre` 프로젝트의 `CI/CD` 구현에 관한 글을 작성할 것 같다!