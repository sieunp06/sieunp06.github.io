---
title:  "✅ [What Todo]Spring boot와 React 연동하기"
search: false
categories: 
  - SpringBoot
toc: true
---

> spring boot와 react를 연동해보자!

<br>

# Dailius 첫 프로젝트
컴퓨터공학과에 진학한 고등학교 동창과 작년에 github organization을 만들었었다.

만들어놓고 서로 바빠서 프로젝트를 진행하지 못하고 있었는데, 이번에 본격적으로 프로젝트를 진행하기 전 간단한 Todo 웹 서비스를 만들어보기로 결정했다.

이번 Todo 서비스는 `Spring Boot`와 `React`를 사용하여 개발하기로 했기 때문에, 이 둘을 연동하는 방법에 대해 찾아보았다.

# Spring Boot와 React 연동하기
시작하기 전에, `Spring Boot` 프로젝트가 이미 생성되어 있고, `React`도 다운받아져 있다는 가정하에 작성한 글임을 참고 바란다.

## 1. `Spring Boot` 프로젝트에 `React` 프로젝트 만들기
우선 만들어진 `Spring Boot` 프로젝트에 `React` 프로젝트를 만들어야 한다.

터미널에 `React` 프로젝트를 만드는 코드를 입력한다.

```
npx create-react-app frontend
```
`frontend`라는 이름의 `React` 폴더를 만든다는 의미다!

나는 `root` 경로에 바로 `frontend`를 만들어줬는데, 다른 블로그 글들을 보니 `main` 아래에 만드는 경우도 있었다.

그런 경우엔 터미널에 이렇게 입력하면 된다.

```
cd src/main
npx create-react-app frontend
```
`src/main`으로 이동해서 `frontend`라는 이름의 `React` 폴더를 만든다는 의미이다.

![Spring boot와 React 연동1](../../assets/images/post/SpringBoot/230521-SpringBoot-React-%EC%97%B0%EB%8F%991.png)

`root` 아래에 `frontend`가 잘 만들어진 것을 확인할 수 있다.

## 2. `Proxy` 설정하기

지금은 `React`와 `Spring Boot`가 각각 3000번과 8080번 포트를 사용하기 때문에 프록시를 설정해 줘야한다.

`📃package.json`

![Spring boot와 React 연동2](../../assets/images/post/SpringBoot/230521-SpringBoot-React-%EC%97%B0%EB%8F%992.png)

```
"proxy": "http://localhost:8080"
```
이 코드를 추가했는데, url과 포트를 적으면 된다고 한다.

## 3. 연동을 확인하기 위한 Controller 작성하기
연동 테스트용 controller를 만들어줬다.

![Spring boot와 React 연동3](../../assets/images/post/SpringBoot/230521-SpringBoot-React-%EC%97%B0%EB%8F%993.png)

`📃HelloWorldController`

![Spring boot와 React 연동4](../../assets/images/post/SpringBoot/230521-SpringBoot-React-%EC%97%B0%EB%8F%994.png)

`📃App.js`

```
import logo from './logo.svg';
import './App.css';
import {useEffect, useState} from "react";

function App() {
    const [message, setMessage] = useState([]);

    useEffect(() => {
        fetch("/hello")
            .then((response) => {
                return response.json();
            })
            .then(function (data) {
                setMessage(data);
            });
    }, []);

    return (
        <div className="App">
            <header className="App-header">
                <img src={logo} className="App-logo" alt="logo"/>
                <p>
                    Edit <code>src/App.js</code> and save to reload.
                </p>
                <a
                    className="App-link"
                    href="https://reactjs.org"
                    target="_blank"
                    rel="noopener noreferrer"
                >
                    Learn React
                </a>
                <ul>
                    {message.map((text, index) => <li key={`${index}-${text}`}>{text}</li>)}
                </ul>
            </header>
        </div>
    );
}

export default App;
```

`localhost:3000` 포트를 실행하면 연동이 완료되어 다음과 같은 화면이 나타난다.

![Spring boot와 React 연동5](../../assets/images/post/SpringBoot/230521-SpringBoot-React-%EC%97%B0%EB%8F%995.png)

## 4. Gradle을 이용해서 프로젝트 빌드하기
아래 코드를 `build.gradle`의 끝에 추가해준다.

`📃build.gradle`
```
def frontendDir = "$projectDir/frontend"

sourceSets {
	main {
		resources {
			srcDirs = ["$projectDir/src/main/resources"]
		}
	}
}

processResources {
	dependsOn "copyReactBuildFiles"
}

task installReact(type: Exec) {
	workingDir "$frontendDir"
	inputs.dir "$frontendDir"
	group = BasePlugin.BUILD_GROUP
	if (System.getProperty('os.name').toLowerCase(Locale.ROOT).contains('windows')) {
		commandLine "npm.cmd", "audit", "fix"
		commandLine 'npm.cmd', 'install'
	} else {
		commandLine "npm", "audit", "fix"
		commandLine 'npm', 'install'
	}
}

task buildReact(type: Exec) {
	dependsOn "installReact"
	workingDir "$frontendDir"
	inputs.dir "$frontendDir"
	group = BasePlugin.BUILD_GROUP
	if (System.getProperty('os.name').toLowerCase(Locale.ROOT).contains('windows')) {
		commandLine "npm.cmd", "run-script", "build"
	} else {
		commandLine "npm", "run-script", "build"
	}
}

task copyReactBuildFiles(type: Copy) {
	dependsOn "buildReact"
	from "$frontendDir/build"
	into "$buildDir/resources/main/static"
}
```

이제 `localhost:8080`을 실행해보면 연동이 정말 완료된 걸 확인할 수 있다!

# Reference
- [https://7942yongdae.tistory.com/136](https://7942yongdae.tistory.com/136)
- [https://velog.io/@u-nij/Spring-Boot-React.js-%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD-%EC%84%B8%ED%8C%85](https://velog.io/@u-nij/Spring-Boot-React.js-%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD-%EC%84%B8%ED%8C%85)
- [https://kth990303.tistory.com/210](https://kth990303.tistory.com/210)