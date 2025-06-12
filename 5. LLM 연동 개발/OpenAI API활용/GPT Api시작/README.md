# GPT Api시작
### 1. OpenAI 계정 생성, Api 키 발급
* https://auth.openai.com/create-account 에서 계정 생성
* https://platform.openai.com/api-keys 에서 key생성
  * “Create new secret key” 버튼 클릭 → 생성된 키를 복사해서 저장
### 2. GPT Api에 요청 해보기
* Api 키 설정 : 환경변수로 설정(공식 권장 방식)
```bash
$env:OPENAI_API_KEY="your-api-key-here"  # Windows PowerShell
```
* OpenAI의 GPT API는 HTTPS요청 기반의 REST API임
* 요금 구조 : 입력 토큰, 출력 토큰 개수에 따라 각각 부과
<br>

* 예시01( requests, os 이용 )
```python
import requests
import os
api_key = os.getenv("OPENAI_API_KEY")
url = "https://api.openai.com/v1/chat/completions"
headers = {
    "Authorization": f"Bearer {api_key}",
    "Content-Type": "application/json"
}
data = {
    "model": "gpt-4-turbo",
    "messages": [
        {"role": "system", "content": "당신은 유능한 조언자입니다."},
        {"role": "user", "content": "신경망이 어떻게 작동하는지 간단한 용어로 설명하세요."}
    ],
    "temperature": 0.7
}
response = requests.post(url, headers=headers, json=data)
print(response.json())
```
* 예시02( OpenAI 이용 )
```python
from openai import OpenAI

# 환경변수 사용 시 아래 코드로 충분
client = OpenAI()
# 명시적 API 키 전달 (보안에 유의)
# client = OpenAI(api_key="YOUR-API-KEY-HERE")

# 대화 메시지 정의
messages = [
    {"role": "system", "content": "당신은 유능한 조언자입니다."},
    {"role": "user", "content": "신경망이 어떻게 작동하는지 간단한 용어로 최대한 짧게 설명하세요."}
]
# GPT-4o 모델 호출
response = client.chat.completions.create(
    model="gpt-4o",
    messages=messages,
    temperature=0.7,
    max_tokens=300
)
# 출력
print(response.choices[0].message.content)
```
