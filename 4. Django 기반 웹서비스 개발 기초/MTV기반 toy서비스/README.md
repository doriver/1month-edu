# MTV기반 toy서비스
## toy서비스
* [사진 목록 보기]()
* [Todo List]()
## Django, MTV 개요

* 가상환경 설정
```bash
  python -m venv [가상환경 이름]
  cd [가상환경 이름]
  ./Scripts/activate
```
* Django 설치 및 확인
```bash
  pip install django
  python -m django --version
```
* Project 생성
```bash
  django-admin startproject [프로젝트 이름] .
```
* app 생성
```bash
  python manage.py startapp [앱 이름]
```
* 웹서버 실행
```bash
  python manage.py runserver
```