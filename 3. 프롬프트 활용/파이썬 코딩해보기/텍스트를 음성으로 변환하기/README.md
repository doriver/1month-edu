# 텍스트를 음성으로 변환하기
```
파이썬을 이용해서 한글 텍스트를 한글 음성으로 변환하는 코드를 작성해줘. API가 아닌 무료로 사용할 수 있는 라이브러리를 사용하도록 해.
```
```python
import pyttsx3

def text_to_speech(text):
    # 음성 엔진 초기화
    engine = pyttsx3.init()

    # 음성 속성 설정 (목소리, 속도, 볼륨 등)
    engine.setProperty('rate', 150)  # 속도 (기본값: 200)
    engine.setProperty('volume', 1.0)  # 볼륨 (0.0 ~ 1.0)
    
    # 기본 음성 설정 (Windows의 경우 Ko-KR 음성 엔진 필요)
    voices = engine.getProperty('voices')
    for voice in voices:
        if "ko-KR" in voice.languages:  # 한글 음성 필터링
            engine.setProperty('voice', voice.id)
            break
    
    # 텍스트 읽기
    engine.say(text)
    engine.runAndWait()

# 테스트 문장
text = "안녕하세요, 파이썬으로 한글 음성을 출력합니다."
text_to_speech(text)
```