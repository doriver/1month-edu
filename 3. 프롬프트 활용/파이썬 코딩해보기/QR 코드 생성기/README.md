# QR 코드 생성기
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