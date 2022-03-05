---
title: "React 프로젝트 github-pages에 올리기"
date: 2022-03-05
categories: React
---

### React 프로젝트 github-pages에 올리기

---

웹에서도 프로젝트를 무료로 빌드할 수 있는 github-pages를 이용하여
React 프로젝트를 빌드하는 법을 알아보자.

이번 포스팅에서는 node.js / vscode / git 을 사용하여 진행한다.

---

**package.json**

```
react 프로젝트의 package.json 파일의 name 위에
"homepage": "https://tmdnsdl.github.io/react-page",
를 추가시켜준다.

package.json의 scripts에
"predeploy": "npm run build",
"deploy": "gh-pages -d build"
를 추가시켜 준다.
```

---

**gh-pages**

package.json 수정이 끝나고 gh-pages에 deploy하기 위해서는
먼저 gh-pages의 모듈을 추가시켜줄 필요가 있다.

```
// node_modules에 gh-pages 추가
cd [프로젝트 경로]
npm i gh-pages --save

// 프로젝트 빌드
cd [프로젝트 경로]
npm run deploy
```

명령어로 npm run deploy를 입력하게 되면 프로젝트를 github-pages에
빌드하는 작업이 진행되고 deploy가 진행된다.

명령어 창에 Published가 나오게 되면 작업이 완료된 것이다.

작업이 완료되면 github에서 내 리포지토리의 settings에서
Pages에서 Branch가 gh-pages로 변경이 되있을 것이다.

변경이 되어있지 않다면 Branch를 gh-pages로 변경을 해주면
publish 된 사이트에서 내 프로젝트를 확인할 수 있다.
