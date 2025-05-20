# 컴퓨터의 외부 및 내부 IP 확인
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
