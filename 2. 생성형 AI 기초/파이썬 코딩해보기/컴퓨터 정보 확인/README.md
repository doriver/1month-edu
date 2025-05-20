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