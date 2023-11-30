---
title:  "[🥝Node.js] npm install 옵션들"
search: false
categories: 
  - Nodejs
tag:
  - npm
toc: true
---

> 궁금해서 찾아본 npm install 옵션들


# npm package install
다음 형식의 명령어를 사용하여 패키지를 설치한다.
```
npm install <module-name> <options>
```

# install options
## --global / -g
```
npm install --global <package>
```
```
npm install -g <package>
```
`-g` 옵션은 패키지를 전역에 설치할 때에 사용한다.
- 패키지를 전역으로 설치했을 때, `package.json`에 추가되지 않기 때문에 협업 시 문제가 발생할 수 있다.

## --save / --save-prod / -P (default)
```
npm install <package> --save
```
`--save` 옵션은 `package.json`의 dependencies에 모듈을 추가한다.
`dependencies`에 추가되기 때문에, `--production` 빌드 시 해당 패키지가 포함되어 빌드된다.

- npm5 이후로는 `--save`를 쓰지 않아도 자동으로 추가된다.

## --save-dev / -D
```
npm install <package> --save-dev
```
`--save-dev` 옵션은 `package.json`의 devDependencies에 모듈을 추가한다.
`devDependencies`에 추가되기 때문에, `--production` 빌드 시 해당 패키지는 포함되지 않는다. 즉, 개발 과정에 필요한 패키지들을 설치할 때 이 옵션을 사용한다.

예를 들어 아래 패키지들을 설치할 때 사용한다.
- Prettier
- ESLint

## --save-optional / -O
```
npm install <package> --save-optional
```
`--save-optional` 옵션은 optionalDependencies에 모듈을 추가한다.

## --no-save
```
npm install <package> --no-save
```
`--no-save` 옵션은 dependencies에 모듈을 추가하지 않는다.

## --save-exact / -E
```
npm install <package> --save-exact
```
`--save-exact`는 정확히 일치하는 버전의 패키지를 추가한다.

`@version`을 사용하여 특정 버전을 설치할 수 있다.
```
npm install <package>@<version>
```
```
npm install packagename@1.4.2
```
## --save-bundle / -B
```
npm install <package> --save-bundle
```
`--save-bundle`은 bundleDependencies에 추가한다.