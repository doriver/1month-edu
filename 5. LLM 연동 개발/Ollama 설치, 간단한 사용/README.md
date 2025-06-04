# Ollama 설치, 간단한 사용
### 1. https://ollama.com/download 에서 ollama다운로드
### 2. 설치 확인, 모델 다운
![ollama설치후](https://github.com/user-attachments/assets/ba7c9f4e-8e43-4465-a4c6-25b92d0c91ac)
### 3. ollama 사용 예제
* 예제1
```python
import ollama
response = ollama.chat(model='openchat', messages=[
    {
        'role': 'user',
        'content': '하늘은 왜 푸른지 설명해줘.',
    },
])
print(response['message']['content'])
```
* 예제2
```python
import requests

def query_ollama(model_name, prompt):
    url = "http://localhost:11434/api/generate"
    headers = {"Content-Type": "application/json"}
    data ={
        "model": model_name,
        "prompt": prompt,
        "stream": False
    }

    response = requests.post(url, headers=headers, json=data)
    response.raise_for_status()
    response_data = response.json()
    print(response_data)

if __name__ == "__main__":
    model = "openchat"
    prompt = "하늘은 왜 푸르게 보일까?"
    query_ollama(model, prompt)
```
* 예제3
```python
import requests
import argparse

def query_ollama(model_name, prompt):
    url = "http://localhost:11434/api/generate"
    headers = {"Content-Type": "application/json"}
    data ={
        "model": model_name,
        "prompt": prompt,
        "stream": False
    }

    response = requests.post(url, headers=headers, json=data)
    response.raise_for_status()
    response_data = response.json()
    print(response_data['response'])

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Input prompt.")
    parser.add_argument("prompt", type=str)

    model = "openchat"
    args = parser.parse_args()
    query_ollama(model, args.prompt)
```
![ollama예제](https://github.com/user-attachments/assets/6bd23d7f-fee1-4bc5-9fd6-a917e44b710b)
