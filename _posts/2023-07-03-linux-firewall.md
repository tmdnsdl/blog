---
title: "Linux 서버에서 방화벽 설정 방법"
date: 2023-07-03
categories: linux
---

### Linux 서버에서 방화벽 설정 방법

---

Linux 서버에서 방화벽 설정 및 해제하는 방법을 알아보도록 하겠다


###### 방화벽 설정 및 해제

```
* 방화벽 적용 유무 확인
# systemctl status firewalld
- Active : active (running) - 방화벽 작동 중
- Active : inactive (dead) - 방화벽 해제 상태

* 방화벽 설정 및 해제
- 방화벽 설정
# systemctl start firewalld
- 방화벽 해제
# systemctl stop firewalld
- 서버 재시작 시 방화벽 자동 설정
# systemctl enable firewalld
- 서버 재시작 시 방화벽 자동 해제
# systemctl disable firewalld
```

---

###### 방화벽 포트 개방

```
* 기본 방화벽 zone 설정 확인
# firewall-cmd --get-default-zone
* 전체 방화벽 zone 설정 확인
# firewall-cmd --list-all-zone

* 방화벽 zone 추가
# firewall-cmd --permanent --new-zone=zoneName
* 방화벽 zone 삭제
# firewall-cmd --permanent --delete-zone=zoneName

* 방화벽 개방할 포트 추가
# firewall-cmd --permanent --zone=zoneName --add-port=8080/tcp
* 방화벽 개방할 포트 삭제
# firewall-cmd --permanent --zone=zoneName --remove-port=8080/tcp

* 방화벽 포트 설정 후 서비스 재시작
# firewall-cmd --reload
```
