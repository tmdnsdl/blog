---
title: "Node.js module이란?"
date: 2022-03-04
categories: Nodejs
---

### Node.js module

---

**node_modules**

이번에는 node.js의 모듈과 설치 방법에 대해 알아보겠다.

Spring에서 라이브러리들을 관리하기 위해 사용되는 maven, gradle과 같이
node.js의 모듈들을 관리하기 위해 npm(node package manager)을 사용하게 된다.

npm i [module명] --save의 커맨드로 npm의 모듈을 편하게 추가 시킬 수 있다.

원하는 모듈을 검색하여 간단하게 추가 시킬 수 있다.

---

**module 설치/재설치**

git을 사용하여 node.js의 프로젝트를 관리하는 경우

gitignore로 인해 git clone으로 가져올때 node_modules은 가져오지 않게 된다.

node 모듈을 설치 혹은 재설치를 하고 싶은 경우

1. 프로젝트 내의 package-lock.json 파일 삭제
2. node_modules 폴더 삭제
3. 프로젝트 경로에서 npm install 명령어 실행

을 진행하여 node 모듈을 설치할 수 있다.
