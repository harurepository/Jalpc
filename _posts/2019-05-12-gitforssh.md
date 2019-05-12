---
title: "Git사용을 위한 SSH Key"
date: 2019-05-12 20:49:00 +0900
categori: Unity
---

Git에 비밀번호 없이 접속하기 위해서는 SSH Key를 만들어 Git 서버에 넣어 인증된 사용자가 되어야한다. 즉, Git에서 접속하기 위해선 Git을 사용할 PC나 맥에서 SSH Key를 생성하여 Git서버에 입력해 놓아야 ssh 접속을 수행할때 해당 키를 바탕으로 접속을 수행하게 되는것이다.
먼저 Git을 사용할 Mac의 터미널을 연다.

---
```console
ssh-keygen -t rsa
```---
위 명령어를 입력하게 되면

Enter file in which to save the key (/Users/username/.ssh/id_rsa):

라고 나오게 된다. 키를 저장할 경로를 입력해달라는 이야기인데 그냥 엔터를 입력하면 괄호 안에 위치한곳에 만들겠다는 이야기다. 그냥 엔터치자.

Enter passphrase (empty for no passphrase):

비밀번호를 입력해달라는것인데 권장은 10~30문자인데, 자동로그인을 하려면 그냥 엔터를 입력하여 생략한다.

---
```console
Enter same passphrase again:
```
---

한번더 같은 비밀번호를 입력해달라는 이야기이니 엔터로 다음을 진행하자.

---
```console
+—[RSA 2048]—-+
| o . .|
| o = +.|
| . + = +|
| . = X o.|
| B O.o|
| . + B B.|
| . + O E O|
| = . + Xo|
| +.o|
+—-[SHA256]—–+
```
---
대략 이런 이상한 문구를 복 된다면 완료되었다. 이제 위의 생성하겠다 했던 경로(/Users/username/.ssh/id_rsa)로 가서 ls를 입력해보자

---
```console
id_rsa    id_rsa.pub    known_hosts
```
---
위와 같이 3개의 파일이 보인다면 완료 되었다. id_rsa는 개인키, id_rsa.pub은 공개키이다.
Git으로 접속하기 위해서는 id_rsa.pub 파일을 FTP로든 메일로든 어떤방식으로든 간에 Git서버에 전송한다.
전송된 id_rsa.pub 파일을 Git 유저의 .ssh 폴더에 넣어 둔다.

---
```console
authorized_keys  id_rsa.pub  known_hosts
```
---
키를 넣게 되면 ~/.ssh 폴더에는 위와 같이 authorized_keys와 함께 id_rsa.pub이 위치하게 된다.

---
```console
cat id_rsa.pub >> authorized_keys
```
---
위 명령어를 입력하여 승인된 키로 보내어진 공개키를 입력한다. 아무 메세지 없이 다음 명령대기줄이 생긴다면 입력 완료이다.
이제 Git에서 아무 입력없이 되는지 진행을 하면 완료이다.
이 포스트는 Jenkins를 위한 설정이므로 Jenkins가 아무 입력없이 잘 진행되는지 테스트를 하면 완료이다.
Job에서 Git 설정이 완료되었다면 아무 에러 메세지 없이 완료 되는지 테스트 해보자.
Jenkins에서 정상적으로 체크아웃이 완료 되었다. 완료이다.
