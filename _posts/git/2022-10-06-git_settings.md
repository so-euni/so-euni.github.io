---
categories: Git
title: Git 세팅 및 로컬-원격 저장소 연결
tags: [git]
---

1. git 저장소 초기화<br>
git init<br><br>

2. 필요에 따라 git config 세팅<br>
git config (--global) user.name "user-name"<br>
git config (--global) user.email email@email.com<br><br>

3. git 저장소 로컬로 복제<br>
git clone https://github.com/*.git (public)<br>
git clone https://user-name@github.com/*.git (private)<br><br>

4. 로컬 <-> 원격 저장소 연결<br>
git remote -v <br>
git remote add origin github.com/*.git<br><br>

5. 원격 저장소 pull<br>
git pull origin master