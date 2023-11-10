---
title: "Linux 서버에 GitLab 구축하기"
date: 2023-10-06
categories: git
---

### Linux 서버에 GitLab 구축 및 데이터 이전 방법

---

이번에는 폐쇄망 Linux 서버(Redhat 8.4)에
GitLab을 구축하고 데이터 이전 하는 법을 알아보겠다

설치파일 경로: <https://packages.gitlab.com/gitlab/gitlab-ce/>
사용 버전 : 15.11.4

rpm 파일을 원하는 버전으로 다운로드 후 설치를 진행한다

---

#### 사전 작업

1. 내부 폐쇄망에서 사용하기 위해 방화벽 정책 등록
2. perl 패키지 설치

```
1. 방화벽 정책 등록
* GitLab에서 사용할 포트 등록
# sudo firewall-cmd --permanent --add-port=80/tcp
* 방화벽 포트 등록 확인
# sudo firewall-cmd --list-all

2. perl 패키지 설치
# sudo yum install -y perl
```

사전 작업이 완료 되면 GitLab rpm 파일을 SFTP로 Linux 서버에 업로드하여 설치를 진행한다.

---

#### GitLab 설치

```
* rpm 설치파일이 있는 경로에서 설치 진행
# sudo rpm -ivh fileName.rpm
```

설치 진행 시 추가로 필요한 패키지가 있다고 나오면 해당 패키지를 설치 후에 진행한다.

설치가 완료 되면 설정 파일에서 extenal_url을 설정해야 한다.
설정 파일 경로는 /etc/gitlab/gitlab.rb 파일이 기본 경로로 지정되있다.

설정 파일을 vi 등의 텍스트 에디터를 사용하여 external_url를 검색하여
설정할 ip나 도메인 주소를 입력하고 파일을 저장한다.

추가로 gitlab에서 사용하는 포트가 해당 폐쇄망 서버에서 사용하는 포트와
중복이 되면 안되므로 port로 검색을 하여 gitlab에서 사용하는 포트와 중복되는지
여부를 체크 후 중복되면 포트를 겹치지 않게 텍스트 에디터로 수정하고 파일을 저장한다.

---

#### 데이터 이전

GitLab의 데이터를 이전하는 방법에 대해 알아보겠다.

```
* 기존에 사용하던 GitLab이 위치한 서버에서 다음과 같이 명령어를 입력
# sudo gitlab-backup create
```

GitLab의 백업 데이터의 경로는 /var/opt/gitlab/backups가 기본 경로로 지정되있다.

백업 데이터는 tar 파일로 저장되있으며 해당 tar파일을 다운로드 하여 데이터를 이전 할 Linux 서버에 옮겨
백업 파일로 restore를 실행한다

```
1. gitlab 프로세스 중지
# sudo gitlab-ctl stop puma
# sudo gitlab-ctl stop sidekiq
2. gitlab 프로세스 중지 확인
# sudo gitlab-ctl status
3. gitlab restore
# sudo gitlab-backup restore BACKUP=1223232424_2023_10_06_15.11.4-ce
* tar 파일명 : 1223232424_2023_10_06_15.11.4_gitlab_backup.tar
```
