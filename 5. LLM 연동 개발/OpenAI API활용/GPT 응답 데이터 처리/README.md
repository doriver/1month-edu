# GPT 응답 데이터 처리
### 1. GPT API 응답 처리 전체 프로세스
```bash
[사용자 입력] → [API 요청 생성] → [OpenAI GPT 응답 수신(JSON)] → [JSON 파싱] → [데이터 가공] → [사용자에게 결과 표시]
```
### 2. GPT API 응답 구조 (기본 JSON 포맷)
```json
{
    'id': 'chatcmpl-BeDrIlPrEggEbUUITmO6jbiwXd5dw', 
    'object': 'chat.completion', 
    'created': 1748926092, 
    'model': 'gpt-4-turbo-2024-04-09', 
    'choices': ' ~ ', 
    'usage': ' ~ ', 
    'service_tier': 'default', 
    'system_fingerprint': 'fp_de235176ee'
}
```
choices에 질문에대한 답변 , usage에 사용된 토큰 개수
### 3. 예제 코드
* 응답 json으로 파징하기
```python
from openai import OpenAI
client = OpenAI()

# 대화 메시지 정의
messages = [
    {"role": "user", "content": "파이썬으로 JSON 파싱하는 간단한 예제를 최대한 짧게 알려줘"},
]

# 1. API 요청: GPT-4o 모델 호출
response = client.chat.completions.create(
    model="gpt-4o",
    messages=messages,
    temperature=0.7,
    max_tokens=300
)

# 2. 응답 JSON 구조 확인
response_json = response.model_dump() # 또는 response_json = response.to_dict()

# 3. 응답 내용 추출
gpt_reply = response_json['choices'][0]['message']['content']

# 4. 사용자에게 가공된 결과 표시
print("GPT 응답 결과:")
print(gpt_reply)
```
* 스트리밍 응답 처리
```python
from openai import OpenAI

# OpenAI 클라이언트 초기화 (환경변수 또는 직접 키 입력)
client = OpenAI()

# 스트리밍 요청
responseStream = client.chat.completions.create(
    model="gpt-4o",  # 또는 "gpt-3.5-turbo"
    messages=[
        {"role": "user", "content": "Django와 Spring의 아키텍쳐에서 가장큰 차이점 1가지만 최대한 짧게 설명해줘"}
    ],
    stream=True
)

# 스트리밍 응답 출력
for chunk in responseStream:
    content = chunk.choices[0].delta.content
    if content:
        print(content, end='', flush=True)
```
* 응답 가공하기
```python
import re

# 응답 파싱 함수 (숫자/알파벳/기호 등 처리)
def parse_list_response(text):
    lines = text.strip().splitlines()
    items = []
    for line in lines:
        match = re.match(r"[\s]*[\d\w][\.\)\s-]+(.*)", line)
        if match:
            items.append(match.group(1).strip())
        else:
            items.append(line.strip())
    return items

# 파싱 및 출력
parsed = parse_list_response("1. 파이썬\n2. 자바스크립트\n3. 자바")

print("\n추천 언어 목록:")
for i, item in enumerate(parsed, start=1):
    print(f"{i}. {item}")
```
