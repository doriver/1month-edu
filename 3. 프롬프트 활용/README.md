# AI로 파이썬 코딩해보기
## 목차
* [컴퓨터의 외부 및 내부 IP 확인](#컴퓨터의-외부-및-내부-ip-확인)
* [텍스트를 음성으로 변환하기](#텍스트를-음성으로-변환하기)
* [QR 코드 생성기](#qr-코드-생성기)
* [컴퓨터 정보 확인](#컴퓨터-정보-확인)
## 컴퓨터의 외부 및 내부 IP 확인
* 외부 IP주소 : 통신회사에서 들어오는 외부 인터넷 회선에 할당되는 ip주소
* 내부 IP주소 : 외부 IP주소를 받아 공유기에 연결된 각각의 컴퓨터와 휴대폰에 할당되는 ip주소
```
파이썬으로 컴퓨터의 내부 및 외부 IP를 한 번에 확인하는 코드를 작성해줘
```
```python
import socket
import requests

def get_internal_ip():
    try:
        # UDP 소켓을 사용하여 내부 IP 주소 가져오기
        with socket.socket(socket.AF_INET, socket.SOCK_DGRAM) as s:
            s.connect(("8.8.8.8", 80))
            internal_ip = s.getsockname()[0]
        return internal_ip
    except Exception as e:
        print(f"내부 IP 가져오기 오류: {e}")
        return None

def get_external_ip():
    try:
        # 외부 IP를 가져오는 공용 API 요청
        response = requests.get("https://api64.ipify.org?format=json")
        data = response.json()
        return data["ip"]
    except Exception as e:
        print(f"외부 IP 가져오기 오류: {e}")
        return None

def main():
    internal_ip = get_internal_ip()
    external_ip = get_external_ip()
    
    print("🖥️ IP 주소 정보")
    print(f"내부 IP 주소: {internal_ip}")
    print(f"외부 IP 주소: {external_ip}")

if __name__ == "__main__":
    main()
```
## 텍스트를 음성으로 변환하기
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
## QR 코드 생성기
```
파이썬으로 QR 코드를 생성하는 코드를 작성해줘
```
```python
import qrcode

def generate_qr(data, filename="qrcode.png", size=10, border=4):
    try:
        # QR 코드 객체 생성
        qr = qrcode.QRCode(
            version=1,
            error_correction=qrcode.constants.ERROR_CORRECT_H,
            box_size=size,
            border=border,
        )
        
        # 데이터 추가
        qr.add_data(data)
        qr.make(fit=True)
        
        # QR 코드 이미지 생성
        img = qr.make_image(fill_color="black", back_color="white")
        
        # 이미지 저장
        img.save(filename)
        print(f"✅ QR 코드가 '{filename}'로 저장되었습니다.")
        
    except Exception as e:
        print(f"❌ 오류 발생: {e}")

# 테스트
data = "https://www.naver.com"
generate_qr(data)
```
## 컴퓨터 정보 확인
```
파이썬으로 CPU, RAM, 네트워크의 사용량을 1초마다 출력하는 프로그램을 작성해줘.
```
```python
mport psutil
import time
import os

def monitor_system(interval=1):
    try:
        while True:
            # CPU 사용량 (%)
            cpu_usage = psutil.cpu_percent(interval=0.5)
            
            # RAM 사용량 (MB, %)
            ram = psutil.virtual_memory()
            ram_used = ram.used / (1024 ** 2)
            ram_total = ram.total / (1024 ** 2)
            ram_percent = ram.percent
            
            # 네트워크 사용량 (bytes)
            net = psutil.net_io_counters()
            net_sent = net.bytes_sent / (1024 ** 2)
            net_recv = net.bytes_recv / (1024 ** 2)
            
            # 화면 지우기 (운영체제에 따라)
            os.system('cls' if os.name == 'nt' else 'clear')
            
            # 결과 출력
            print(f"🖥️ 시스템 모니터링 (업데이트 간격: {interval}초)")
            print("=" * 40)
            print(f"CPU 사용량: {cpu_usage:.2f} %")
            print(f"RAM 사용량: {ram_used:.2f} MB / {ram_total:.2f} MB ({ram_percent:.2f} %)")
            print(f"네트워크 전송: {net_sent:.2f} MB")
            print(f"네트워크 수신: {net_recv:.2f} MB")
            print("=" * 40)
            
            # 지정한 간격만큼 대기
            time.sleep(interval)
    
    except KeyboardInterrupt:
        print("\n모니터링 종료")
        
# 실행
monitor_system(interval=1)
```
