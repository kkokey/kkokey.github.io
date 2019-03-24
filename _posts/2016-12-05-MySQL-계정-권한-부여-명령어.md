---
title: MySQL 계정 권한 부여 명령어
date: 2016-12-05 21:36:32
categories: MySQL
tags: 명령어
---

### MySQL에서 권한 부여하는 명령어

 - MySQL에서 권한을 부여할 수 있는 계정으로 사용 가능한 명령어

``` bash
mysql> grant ALL PRIVILEGES on {디비이름}.{테이블이름} to {계정}@{아이피} identified by {패스워드};
```
