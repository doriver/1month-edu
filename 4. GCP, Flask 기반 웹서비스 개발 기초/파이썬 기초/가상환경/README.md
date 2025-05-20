## 가상환경 설정( Windows 기준 )
가상환경 : 독립적인 프로젝트를 위한 개별적인 공간
```bash
cd workspace # 작업용 폴더로 이동
python -m venv [가상환경 이름] # 가상환경 생성
cd [가상환경 이름]
./Scripts/activate # 가상환경 활성화

# 설치하고싶은 패키지들 설치
pip install numpy pandas matplotlib jupyter 

deactivate # 가상환경 비활성화
```

#### ./Scripts/activate 실행시 아래 에러 발생하면
이 시스템에서 스크립트를 실행할 수 없다. 자세한 내용은 about_Execution_Policies(https://go.microsoft.com/fwlink/?LinkID=135170)를 참조하
십시오. <br>
```bash
Set-ExecutionPolicy RemoteSigned # 실행 규칙 변경 , 예 or 모두 예
```
