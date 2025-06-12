# DRF( Django REST Framework )
## DRF를 이용한 작은 결과물
* [도서정보 API](https://github.com/doriver/PythonSkill01/tree/master/Django/DRF01)
* [Todo List API](https://github.com/doriver/PythonSkill01/tree/master/Django/DRF02)
## Django REST Framework 개요
Django를 기반으로 REST API서버를 만들기 위한 라이브러리
* 설치
```bash
pip install djangorestframework
```

* 직렬화
```python
from rest_framework import serializers
```

* 인증 및 권한 설정
```python
from rest_framework import permissions
```