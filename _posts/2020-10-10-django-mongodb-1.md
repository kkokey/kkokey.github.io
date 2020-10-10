---
title: 'django 와 mongoDB 연동 (1)'
date: 2020-10-10 19:39:00
categories: info
tags: python django 장고 mongodb mac pyenv virtualenv homebrew bashrc bash_profile poetry
comments: true
---

안녕하세요 괴짜 개발자 namedboy 입니다. 😎
django로 mongoDB를 연동해본적 있으신가요?

이번에 프로젝트를 진행하면서 django와 mongoDB를 연동하는데 꽤나 어려움을 겪어서 이렇게 정리해두려고 합니다.

django와 mongoDB를 연동 하려면 먼저 django와 mongoDB를 설치해야겠죠?ㅎ

일단 저는 mac을 사용하고 있으니 mac을 기준으로 설명하고 다른 운영체제의 경우 참고할 링크를 추가해 두겠습니다.

## python

django를 사용하기 위해서는 python이 설치가 되어 있어야 합니다.

Mac에는 python이 기본으로 설치가 되어 있습니다. 

기본으로 설치된 파이썬의 버전은 2.7인데 저는 3.7.5를 기본으로 세팅해두고 사용하기 위해 pyenv를 설치하고 global 버전dmf 3.7.5로 설정해두었습니다.

> - 보통 python을 쓰는 경우 패키지 관리를 위해 사용하는 라이브러리가 있습니다.  
> - 제가 아는 방법만 해도 virtualenv,  pyenv, poetry 등 다양하게 존재하고 사용 방법과 장단점등이 모두 다르기 때문에 "pyhton 의존성 관리" 또는 "python 패키지 관리" 등의 검색을 통해 각자의 방법을 찾으시면 좋겠습니다.  
> - 이 포스팅에서는 pyenv와 pyenv-virtualenv를 사용했습니다.  

Mac에서는 패키지를 편하게 설치하기 위해 homebrew를 사용하는데 설치해주시면 간단한 명령어로 편하게 패키지들을 설치할 수 있습니다.
Homebrew는 아래 명령어를 통해 설치할 수 있습니다.

```bash
# Homebrew 공식 홈페이지 : https://brew.sh/index_ko
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

homebrew를 설치하면 `brew install pyenv pyenv-virtualenv` 명령어로 pyenv와 pyenv-virtualenv를 설치 할 수 있습니다.

설치 후에는 `pyenv` 명령어로 설치 되었는지 확인하실 수 있습니다.
또 아래 명령어로 설치가 가능한 목록을 확인 할 수 있죠.

```bash
$ brew install pyenv pyenv-virtualenv

$ pyenv install -ll--list
```

그 리스트에서 원하는 버전을 생각하시고 아래 명령어로 설치해주시면 됩니다.

```bash
$ pyenv install 3.8.5
```

저는 3.8.5로 설치를 했습니다.
아래 내용이 보이고 설치가 완료되었네요.

```bash
python-build: use openssl@1.1 from homebrew
python-build: use readline from homebrew
Downloading Python-3.8.5.tar.xz...
-> https://www.python.org/ftp/python/3.8.5/Python-3.8.5.tar.xz
Installing Python-3.8.5...
python-build: use readline from homebrew
python-build: use zlib from xcode sdk
Installed Python-3.8.5 to /Users/aron/.pyenv/versions/3.8.5
```

설치한 이후에는 아래 처럼 .bashrc 또는 .zshrc 에 터미널을 실행시 자동으로 실행되도록 설정을 해줍니다.

```bash
# vi ~/.zshrc

# pyenv config
export PYENV_PATH=$HOME/.pyenv
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```

아래 명령어로 현재까지 설치된 python 버전을 확인 하고 세팅할 수 있습니다.

```bash
# 설치된 python 버전 확인
$ pyenv versions

# 기본으로 사용하고자 하는 pyhton 버전 선택
$ pyenv global 3.8.5

# python이 제대로 설치가 되었다면 pip --version 명령어가 실행 가능
$ pip --version
pip 20.1.1 from /Users/aron/.pyenv/versions/3.8.5/lib/python3.8/site-packages/pip (python 3.8)
```

pip 까지 설치가 잘 되었다면 이제 Django를 설치할 차례입니다.

프로젝트로 사용할 폴더를 하나 생성하고 `pip install Django==3.1.2` 을 실행시켜 줍니다.

```bash
# 아래 명령어로 환경에서 사용할 파이썬 버전을 세팅할 수 있습니다.
# pyenv virtualenv <python version> <virtualenv name>
# 아래 명령어로 python 환경을 세팅해둡니다.
$ pyenv virtualenv 3.7.5 django-project

$ mkdir django-project
$ cd django-project

# local 명령어로 해당 프로젝트를 사용할 때 해당 파이썬 버전을 사용하도록 설정해 줍니다.
$ pyenv local django-project
$ pip install Django==3.1.2
```

django까지 설치 하고 나면 아래 명령어로 내가 원하는 버전으로 설치가 되었는지 확인합니다.

```bash
$ python
Python 3.7.5 (default, Dec 10 2019, 12:26:40)
[Clang 11.0.0 (clang-1100.0.33.12)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import django
>>> print(django.get_version())
3.1.2
>>> exit()

# 또는 아래 명령어로도 확인이 가능합니다.
$ python -m django --version
```

django가 설치된 걸 확인하셨으면 이제 django-admin을 사용해 mongodb와 연동할 django 샘플 프로젝트를 생성해봅시다.

샘플 프로젝트는 `django-admin startproject django_mongodb` 명령어로 간단하게 생성할 수 있습니다.

더 많은 정보를 알고 싶다면 [링크]([https://docs.djangoproject.com/ko/3.1/intro/tutorial01/](https://docs.djangoproject.com/ko/3.1/intro/tutorial01/))를 방문해 보세요.

이제 해당 프로젝트로 이동하여 간단한 `django_mongodb` 프로젝트 서버를 실행해 봅시다.

```bash
# 만들어진 프로젝트 폴더로 들어갑니다.
$ cd django_mongodb 

# 먼저 migrate를 해주어야 합니다.
# 서버 실행을 위한 관련 데이터베이스와 테이블을 생성해줍니다.
$ python [manage.py](http://manage.py/) migrate

# 서버 실행
$ python manage.py runserver

Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
October 10, 2020 - 10:36:11
Django version 3.1.2, using settings 'django_mongodb.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

마지막 메시지가 뜬다면 성공입니다.

메시지 내용 안에 있는 링크로 접속해보면 아래 화면처럼 보여질 겁니다.

![django](https://firebasestorage.googleapis.com/v0/b/github-blog-39e5f.appspot.com/o/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-10-10%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%207.37.12.png?alt=media&token=e439b798-f53c-40e8-b352-a63e6e9ab206)

그럼 다음 포스트에서는 django와 mongodb를 직접적으로 연결하는 내용을 다루겠습니다.

궁금하거나 이상한 내용은 댓글로 남겨주세요!