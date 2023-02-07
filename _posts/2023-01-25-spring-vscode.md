---
title: "vscode에서 spring 개발 환경 설정"
date: 2023-01-25
categories: Spring
---

### vscode에서 spring 프로젝트 개발 환경 설정

---

스프링 프로젝트에 흔히 사용하는 Eclipse, IntelliJ와 같은 IDE가 아닌
vscode와 같은 텍스트 에디터로도 스프링 프로젝트를 현업에서 관리하는 경우가 있어
이번에는 vscode에서 spring 프로젝트 개발 환경 설정을 알아보도록 하겠다

---

**기본 환경 설정**

1. Java 설치
- OpenJDK 11(https://developers.redhat.com/products/openjdk/download)
- OpenJDK 1.8(https://developers.redhat.com/products/openjdk/download)
2. Java 환경 변수 편집
3. Git 설치

**vscode 환경 설정**

1. 스프링 프로젝트에 필요한 Extension 설치
- Extension Pack for Java
- Spring Boot Extension Pack
2. setting.json 설정
```
    "java.configuration.runtimes": [
        {
            "name": "JavaSE-11",
            "path": "C:\\Program Files\\Java\\jdk-11",
            "default": true
        },
        {
            "name": "JavaSE-1.8",
            "path": "C:\\Program Files\\Java\\jdk-1.8"
        }
    ],
```
