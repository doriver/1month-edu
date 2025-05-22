# 소켓 프로그래밍
<img height="400px" src="https://github.com/user-attachments/assets/8c7b8d58-8abb-492b-bda5-c334af2d1226">

## 간단한Server 구현 로직( TCP 소켓 이용 )
```python
import socketserver

HOST = ''
PORT = 9009

class MyTcpHandler(socketserver.BaseRequestHandler):
   # 이 클래스는 서버 하나당 단한번 초기화됩니다.
   # handle() 메쏘드에 클라이언트 연결 처리를 위한 로직을 구현합니다.
   def handle(self):
      print('[%s] 연결됨' %self.client_address[0])

      try:
         while True:
            self.data = self.request.recv(1024)
            if self.data.decode() == '/quit':
               print('[%s] 사용자에 의해 중단' %self.client_address[0])
               return

            print('[%s]' %self.data.decode())
            self.request.sendall(self.data)
      except Exception as e:
         print(e)

def runServer():
   print('+++ 에코 서버를 시작합니다.')
   print('+++ 에코 서버를 끝내려면 Ctrl-C를 누르세요.')

   try:
       server = socketserver.TCPServer((HOST, PORT), MyTcpHandler)
       server.serve_forever()
   except KeyboardInterrupt:
      print('--- 에코 서버를 종료합니다.')

runServer()
```

## 간단한Client 구현 로직( TCP 소켓 이용 )
```python
import socket

HOST = 'localhost'
PORT = 9009

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as sock:
   sock.connect((HOST, PORT))

   while True:
       msg = input('메시지 입력: ')
       if msg == '/quit':
           sock.sendall(msg.encode())
           break

       sock.sendall(msg.encode())
       data = sock.recv(1024)
       print('에코 서버로부터 받은 데이터 [%s]' %data.decode())

print('클라이언트 종료')
```

### 위보다 더 간단한 Server
```python
import socket

HOST = ''
PORT = 9009

def runServer():
   with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as sock:
      sock.bind((HOST, PORT))
      sock.listen(1)
      print('클라이언트 연결을 기다리는 중..')
      conn, addr = sock.accept()

      with conn:
         print('[%s]와 연결됨' %addr[0])
         while True:
            data = conn.recv(1024)
            if not data:
               break
            print('메시지 수신 [%s]' %data.decode())
            conn.sendall(data)

runServer()
```
