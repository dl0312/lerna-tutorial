# ☝️ Monorepo tutorial

# Monorepo란?
다양한 모듈을 여러개의 레포지터리로 관리하지 않고, 하나의 레포지토리로 관리하는 것을 의미한다.

`Monorepo`를 쓸 상황이 어떤 것이 있을까? 일단 가장 간단한 예시로는 프론트 엔드와 백엔드를 하나의 레포지토리에서 관리하는 것이 있다. 다음으로는 각 프로젝트에서 NPM 모듈 만들어가면서 프로젝트를 진행하는 경우도 있다. 마지막으로 웹과 앱을 만들때 웹 혹은 앱에서 사용했던 로직 혹은 모듈을 공유하기 위해 `Monorepo`를 쓰기도한다.

## Monorepo의 장점
**통일성**이 생긴다 - 여러개의 리포지토리로 관리될 경우 다른 리포지토리의 로직을 보게될 기회가 많이 없기 때문에 코드가 통일되지 않고 중구난방이 된다. 여러 리포지토리로 관리될 경우 같은 기능을 가진 함수가 수십개가 되어 불필요한 공간을 차지할 수 있게된다. 또한 `lerna`를 사용할 경우 반복없이 유일한 `npm` 패키지를 설치하기 때문에 또한 크기를 줄일 수 있다.

# yarn-workspaces

## 사용법
따로 npm 설치할 npm package는 없다.
`package.json` 파일에 `workspaces`를 지정해주는 것만으로 설정은 마무리된다.

여러 `package`들을 `packages`라는 폴더에서 관리하는 방식이 가장 유명하다.

다음의 예시와 같이 보통 @뒤에 `organization`에 해당하는 이름을 `prefix`로 붙여서 각 패키지을 이름짓는다.
```json
{
  "name": "@walnut/iloveyou3000",
  ...
}
```

## 특징
`packages`사이에서는 서로를 `npm` 패키지처럼 불러올 수 있다.

```json
{
  "name": "@walnut/server",
  "version": "1.0.2",
  "main": "index.js",
  "license": "MIT",
  "dependencies": {
    "@walnut/common": "^1.0.1",
    "graphql-yoga": "^1.14.7"
  },
  "scripts": {
    "test": "echo testing server with version: $npm_package_version"
  }
}
```
물론 해당 패키지 안에서 불러온 패키지를 사용할 수도 있다.
```js
const commonFunction = require('@walnut/common')
commonFunction()
```

# lerna
[lerna](https://github.com/lerna/lerna) - 🐉 A tool for managing JavaScript projects with multiple packages.

위에 언급했던 것처럼 여러 리포지토리의 의존성을 묶어주는 역할을 하며, 각 패키지별 업데이트를 도와준다.

`yarn-workspaces`와 같이 사용하려면 `lerna.json`에 다음과 같이 적어주어야한다.
```json
{
  ...
  "npmClient": "yarn",
  "useWorkspaces": true,
  ...
}
```

## 커맨드
```shell
$ lerna bootstrap
```
여러 리포지토리의 의존성을 묶어서 각 패키지별 라이브러리를 중복이 없게 설치해준다.

## References
* 📹[How to Use Lerna](https://www.youtube.com/watch?v=p6qoJ4apCjA)
* 📹[Better code sharing through monorepos?](https://www.youtube.com/watch?v=0_qhdOeMuhk)
* 📹[Marcel Cutts - MonoRepos for the Masses | ReactNext 2018](https://www.youtube.com/watch?v=rdeBtjBNcDI)
* 📹[Uber Technology Day: Monorepo to Multirepo and Back Again](https://www.youtube.com/watch?v=lV8-1S28ycM)
* 📹[Jacob Bass: Modularity and Monorepositories](https://www.youtube.com/watch?v=7Lr8xYPKG5w)
* 📹[Yarn Workspaces Tutorial](https://youtu.be/G8KXFWftCg0) by Ben Awad