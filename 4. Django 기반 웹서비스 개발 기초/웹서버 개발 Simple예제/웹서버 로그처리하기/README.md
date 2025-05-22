# 웹서버 로그처리하기
## 고유 방문자 수 계산하기
```python
visit_ip = []

with open('access_log', 'r') as f:
   logs = f.readlines()
   for log in logs:
      log = log.split()
      ip = log[0]
      if ip not in visit_ip:
         visit_ip.append(ip)

print('고유 방문자수: [%d]' %len(visit_ip))
```
## 총 네트워크 트래픽 계산하기
```python
KB = 1024
total_service = 0

with open('access_log', 'r') as f:
   logs = f.readlines()
   for log in logs:
      log = log.split()
      servicebyte = log[9]
      if servicebyte.isdigit():
         total_service += int(servicebyte)

total_service /= KB
print('총 서비스 용량: %dKB' %total_service)
```
## 사용자별 네트워크 트래픽 계산하기
```python
services = {}

with open('access_log', 'r') as f:
   logs = f.readlines()
   for log in logs:
      log = log.split()
      ip = log[0]
      servicebyte = log[9]
      if servicebyte.isdigit():
         servicebyte = int(servicebyte)
      else:
         servicebyte = 0

      if ip not in services:
         services[ip] = servicebyte
      else:
         services[ip] += servicebyte
# key값 기준으로 정렬
ret = sorted(services.items(), key=lambda x: x[1], reverse=True)

print('사용자IP – 네트워크 트래픽')
for ip, b in ret:
   print('[%s] – [%d]' %(ip, b))
```
