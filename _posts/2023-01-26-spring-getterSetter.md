---
title: "vscode에서 spring 프로젝트 getter, setter 자동 생성하기"
date: 2023-01-26
categories: Spring
---

### vscode에서 getter, setter 자동 생성하기

---

스프링 프로젝트에 흔히 사용하는 Eclipse, IntelliJ에서는
Constructor나 getter, setter를 자동으로 생성해주는 기능이 내장 되어있으나
vscode의 경우 Extension을 설치하여 getter, setter를 자동으로 생성할 수 있다.

---

### Getter and Setter Generator

vscode 마켓플레이스에서 getter로 검색하면 Getter and Setter Generator라는
Extension을 확인 할 수 있다.

설치를 눌러서 설치 하면 바로 사용할 수 있다.

```
private String test_id;
private String test_subject;
private String created_datetime;
private String updated_datetime;
private boolean check_delete;
```

위와 같이 getter, setter를 만들 변수를 드래그 하여 vscode에서 F1을 누르면 명령어를 입력할 수 있는데
generate를 입력하면 보이는 Generate get and set methods 항목을 선택 하면 자동으로 getter, setter가 완성이 된다.

```
private String test_id;
private String test_subject;
private String created_datetime;
private String updated_datetime;
private boolean check_delete;

public String getTest_id() {
    return this.test_id;
}

public void setTest_id(String test_id) {
    this.test_id = test_id;
}

public String getTest_subject() {
    return this.test_subject;
}

public void setTest_subject(String test_subject) {
    this.test_subject = test_subject;
}

public String getCreated_datetime() {
    return this.created_datetime;
}

public void setCreated_datetime(String created_datetime) {
    this.created_datetime = created_datetime;
}

public String getUpdated_datetime() {
    return this.updated_datetime;
}

public void setUpdated_datetime(String updated_datetime) {
    this.updated_datetime = updated_datetime;
}

public boolean isCheck_delete() {
    return this.check_delete;
}

public void setCheck_delete(boolean check_delete) {
    this.check_delete = check_delete;
}
```
