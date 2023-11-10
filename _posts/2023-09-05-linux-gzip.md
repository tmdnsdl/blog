---
title: "Linux 서버에서 파일 압축 및 압축해제 하는 방법"
date: 2023-09-05
categories: linux
---

### Linux 서버에서 파일 압축 및 압축해제 하는 방법

---

Linux 서버에서 파일 압축 및 압축해제 하는 방법을 알아보도록 하겠다

gzip이라는 명령어를 활용하도록 하겠다.
gzip은 일반 파일만 압축이 가능하며 심볼릭 링크는 압축이 되지 않는다.

```
* gzip 기본 명령어
# gzip [Option] [FILENAME]

* 단일 파일 압축
# gzip filename
* 단일 파일 압축(원본 파일 남겨놓기)
# gzip -k filename
* 복수 파일 압축
# gzip filename1 filename2 filename3
* 디렉토리의 모든 파일 압축
# gzip -r directory

* gz 파일 압축 해제
# gzip -d filename.gz
* gz 파일 압축 해제(압축 파일 남겨놓기)
# gzip -dk filename.gz
* 복수 파일 압축 해제
# gzip -d filename1.gz filename2.gz filename3.gz
* 디렉토리의 모든 파일 압축 해제
# gzip -dr directory
```
