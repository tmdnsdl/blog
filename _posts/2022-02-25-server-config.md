---
title: "Tomcat 서버 구축 및 설정"
date: 2022-02-25
categories: Server
---

### Tomcat 서버 구축

---

웹 서버를 구축하는데는 주로 톰캣을 이용하여 웹 서버를 구축하게 된다.

이번에는 톰캣 고양이를 사용하여 서버를 구축하는 방법을 알아보자.

---

**Tomcat 8.5 설치**

먼저 톰캣을 설치해야 하는데 이번 포스팅에서는 톰캣 8.5버전을 기준으로 설명하겠다.

<https://tomcat.apache.org/download-80.cgi>

위 링크에서 톰캣 8.5 서버를 다운로드 할 수 있다.
톰캣을 여러개 구동하는 환경을 고려하여 zip 파일로 설치하는 방법을 기준으로 한다.

자신의 운영체제에 맞춰서 zip 파일을 다운로드 한다.
일반적인 경우 64비트 윈도우 운영체제는 64-bit Windows zip 파일을 다운로드 받으면 된다.

zip 파일을 다운로드 받으면 원하는 디렉토리에 압축을 풀어주자.
압축을 푼 다음 bin 폴더에서 startup.bat / shutdown.bat / service.bat 파일을 수정해줘야 한다.

리눅스 운영체제의 경우 sh파일을 변경해야 하나 이번 포스팅에서는 윈도우 환경만 설명하겠다.

---

```
startup.bat

setlocal 위에
set "CATALINA_HOME=C:\Program Files\Apache Software Foundation\Tomcat 8.5.1"
set "CATALINA_BASE=C:\Program Files\Apache Software Foundation\Tomcat 8.5.1"
set "SERVER_NAME=Tomcat Server 8.5.1"
set "JAVA_HOME=C:\Program Files\Java\jdk1.8.0_261"
를 추가해준다.

CATALINA_HOME / CATALINA_BASE는 톰캣 압축을 푼 곳의 디렉토리를 설정해준다.
SERVER_NAME은 원하는 서버 명을 지정해준다.
JAVA_HOME은 jdk가 설치된 디렉토리를 설정해준다.
```

```
shutdown.bat

startup.bat과 마찬가지로 setlocal 위에
set "CATALINA_HOME=C:\Program Files\Apache Software Foundation\Tomcat 8.5.1"
set "CATALINA_BASE=C:\Program Files\Apache Software Foundation\Tomcat 8.5.1"
set "SERVER_NAME=Tomcat Server 8.5.1"
set "JAVA_HOME=C:\Program Files\Java\jdk1.8.0_261"
를 추가해준다.
```

---

톰캣 서버를 여러개 구축하는 경우 윈도우의 서비스에서도 여러개로 작동 되기 때문에
service.bat에서 서비스 명을 적절하게 구분하여 작성해야 한다.

```
service.bat

set DEFAULT_SERVICE_NAME=Tomcat8
set SERVICE_NAME=%DEFAULT_SERVICE_NAME%
서비스 명의 기본값

아래와 같이 바꿔주면 어떤 용도의 서버인지 구분할 수 있게 된다.
set DEFAULT_SERVICE_NAME=Tomcat8
set SERVICE_NAME=Tomcat8.5.1
set DISPLAYNAME=Apache Tomcat 8.5 %SERVICE_NAME%

DISPLAYNAME은 서비스에 올라가는 서비스 명이다.
원하는 서비스명을 지정해서 서버를 구분하면 된다.

```

---

위의 설정이 완료 되었으면 cmd에서 톰캣을 압축해제한 디렉토리의 bin 폴더에서
명령어를 실행하면 톰캣 서비스가 등록된다.

```
cmd 환경에서
cd [톰캣 디렉토리]\bin을 입력
cd C:\Program Files\Apache Software Foundation\Tomcat 8.5.1\bin

경로 설정 후
service.bat install
명령어를 입력하여 서비스를 등록

서비스를 삭제하고 싶은 경우 같은 경로에서
service.bat remove
명령어를 입력하여 서비스를 삭제
```

톰캣을 설치파일(exe)로 다운받아 설치하게 되면 명령어를 입력하지 않아도
알아서 서비스에 톰캣이 등록되지만 여러개의 톰캣 서버를 구축해야 하는 경우는
zip 파일로 위와 같이 설정하여 서비스를 각각 등록 해줘야 한다.

여러개의 톰캣 서버를 구축하는 경우 유의해야 할 사항은 server.xml에서
포트번호를 각각 겹치지 않게 지정해줘야 한다.
Connector port와 redirectPort를 각각 다르게 설정해주어 여러개의 서버를 구축할 수 있다.
