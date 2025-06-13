
## Pull Request 기본 흐름
Pull Request : 다른브랜치에서 작업내용을 GitHub에서 병합해달라고 요청하는거
1. 다른 브랜치에서 기능 개발
2. 커밋 및 푸시
3. GitHub에서 PR 생성
4. 코드 리뷰 및 승인
5. 병합(Merge)

## GitHub Actions를 활용한 CI/CD
GitHub Actions : GitHub에서 제공하는 자동화 워크플로우 엔진, 이벤트 기반으로 작업을 자동 실행함
<img src="https://github.com/user-attachments/assets/ca853f7c-e486-46c8-bf60-81e7ffe77946" style="width: 400px">
* on(트리거)에 해당하는 이벤트가 발생했을때, 워크플로우(주로 CI/CD)가 실행됨
```
.github/
└── workflows/
    └── ci-cd.yml     <-- 워크플로우 정의 파일
```
