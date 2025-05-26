## 파일 전송 서버
```python
import socketserver
from os.path import exists

HOST = ''
PORT = 9009

class MyTcpHandler(socketserver.BaseRequestHandler):
   def handle(self):
      data_transferred = 0
      print('[%s] 연결됨' %self.client_address[0])
      filename = self.request.recv(1024)
      filename = filename.decode()

      if not exists(filename):
         return

      print('파일 [%s] 전송 시작...' %filename)
      with open(filename, 'rb') as f:
         try:
            data = f.read(1024)
            while data:
               data_transferred += self.request.send(data)
               data = f.read(1024)
         except Exception as e:
            print(e)

      print('전송완료[%s], 전송량[%d]' %(filename, data_transferred))

def runServer():
   print('+++ 파일 서버를 시작합니다.')
   print('+++ 파일 서버를 끝내려면 Ctrl-C를 누르세요.')

   try:
      server = socketserver.TCPServer((HOST, PORT), MyTcpHandler)
      server.serve_forever()
   except KeyboardInterrupt:
      print('--- 파일 서버를 종료합니다.')

runServer()
```
## 파일 수신 클라이언트
```python
import socket

HOST = 'localhost'
PORT = 9009

def getFileFromServer(filename):
   data_transferred = 0

   with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as sock:
      sock.connect((HOST, PORT))
      sock.sendall(filename.encode())

      data = sock.recv(1024)
      if not data:
         print('파일[%s]: 서버에 존재하지 않거나 전송중 오류발생' %filename)
         return

      with open('download/'+filename, 'wb') as f:
         try:
            while data:
               f.write(data)
               data_transferred += len(data)
               data = sock.recv(1024)
         except Exception as e:
            print(e)

   print('파일 [%s] 전송종료. 전송량 [%d]' %(filename, data_transferred))

filename = input('다운로드 받을 파일이름을 입력하세요: ')
getFileFromServer(filename)

```