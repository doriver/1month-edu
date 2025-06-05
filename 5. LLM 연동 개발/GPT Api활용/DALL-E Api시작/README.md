# DALL-E Api시작
* DALL·E : 텍스트를 이미지로 바꿔주는 Text-to-Image 모델
* DALL-E Api로 이미지 생성 해보기 01
```python
import requests
# OpenAI API Key
API_KEY = "your_openai_api_key"
# 요청 헤더
headers = {
    "Authorization": f"Bearer {API_KEY}",
    "Content-Type": "application/json"
}
# 요청 바디
payload = {
    "model": "dall-e-3",
    "prompt": "a futuristic city skyline at sunset",
    "n": 1,
    "size": "1024x1024",
    "quality": "standard"
}
# 이미지 생성 요청
response = requests.post(
    "https://api.openai.com/v1/images/generations",
    headers=headers,
    json=payload
)
# 응답 처리
if response.status_code == 200:
    image_url = response.json()['data'][0]['url']
    print("이미지 URL:", image_url)
      
    # 이미지 다운로드 (선택 사항)
    img_data = requests.get(image_url).content
    with open("generated_image.png", "wb") as f:
        f.write(img_data)
        print("이미지가 'generated_image.png'로 저장되었습니다.")
else:
    print("오류:", response.status_code, response.text)
```
* DALL-E Api로 이미지 생성 해보기 02
```python
from openai import OpenAI
# OpenAI 클라이언트 초기화 (환경 변수 사용 권장)
client = OpenAI()

# 이미지 생성 요청
response = client.images.generate(
    model="dall-e-3",
    prompt="a futuristic city at ocean",
    n=1,
    size="1024x1024",
    quality="standard"
)

# 이미지 URL 추출
image_url = response.data[0].url
print("이미지 URL:", image_url)

# 이미지 다운로드 (선택 사항)
import requests
img_data = requests.get(image_url).content
with open("generated_image02.png", "wb") as f:
    f.write(img_data)
    print("이미지가 'generated_image02.png'로 저장되었습니다.")
```
