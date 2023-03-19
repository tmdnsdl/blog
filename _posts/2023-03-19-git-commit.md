---
title: "Git Local Repository 생성과 github 연동"
date: 2023-03-19
categories: git
---

### Git Local Repository 생성과 github 연동

git 으로 local repository 생성 하여 작업 후에 github repository에 연동하는 방법에 대해 알아보자.

1. 터미널에서 작업 중인 디렉토리에서 git init 명령어를 입력한다
2. github repository를 생성한다
3. git repository 주소(https)를 복사
4. git remote add origin 주소(http) 명령어를 입력한다
5. git remote -v 명령어를 입력한다

```
cd my_work_directory
# c:\my_work_directory
git init
git remote add origin https://github.com/my/test.git
git remote -v
```

---

### github commit and push

1. 작업 중인 디렉토리 최상위에서 git add . 명령어를 입력한다
2. git의 user.name과 user.email을 설정한다
3. git commit -m 명령어로 커밋한다
4. git push origin master 명령어로 push 하여 연동한다

```
# c:\my_work_directory
git add.
git config --global user.name "test"
git config --global user.email "test@example.com"
git commit -m "initial commit"
git push origin master
```
