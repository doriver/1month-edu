# 파이썬 가상환경
독립적인 프로젝트를 위한 개별적인 공간 <br>
프로젝트마다 다른 버전의 파이썬과 모듈을 사용하는 경우가 많음

## 가상환경 설정( Windows PowerShell 기준 )
```bash
cd workspace # 작업용 폴더로 이동
python -m venv [가상환경 이름] # 가상환경 생성
cd [가상환경 이름]
./Scripts/activate # 가상환경 활성화

# 설치하고싶은 패키지들 설치
pip install numpy pandas matplotlib jupyter 

deactivate # 가상환경 비활성화
```
가상환경 활성화 되면 명령 프롬프트 맨 앞에 ‘(가상 환경 이름)’와 같이 표시된다.

```bash
#  특정 파이썬 버전으로 가상환경 생성하기
py -[버전] -m venv [가상환경 이름] 
```

### ./Scripts/activate 실행시 아래 에러 발생하면
이 시스템에서 스크립트를 실행할 수 없다. 자세한 내용은 about_Execution_Policies(https://go.microsoft.com/fwlink/?LinkID=135170)를 참조하
십시오. <br>
```bash
# 관리자 권한 파워쉘에서 입력
Set-ExecutionPolicy RemoteSigned # 실행 규칙 변경 , 예 or 모두 예
```