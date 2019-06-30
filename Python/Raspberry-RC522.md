---
tags: python,iot
---
# Raspberry-RC522

---
## 介紹
RC522的用途在於讀取RFID卡片的內容

他的範例程式在[**GITHUB**](https://github.com/miguelbalboa/rfid)上有

以下根據我這次專題用到的程式碼進行解說
對了rc522只支援**python2**

---
## 程式
首先把套件讀近來，他的套件都在github上，如果要使用記得把你的程式放到clone下來的資料夾裡，再進行編譯
>P.S還有一定要插對線，並且raspberry要打開資源排線功能
```python=
import RPi.GPIO as GPIO
import MFRC522
import signal
```
---
先定義如何終止程式，這邊適用Ctrl+C 來停止
```python=
def end_read(signal,frame):
    global continue_reading
    print "Ctrl+C captured, ending read."
    continue_reading = False
    GPIO.cleanup()
```
---
當按下Ctrl+C執行end_read()
```python=
signal.signal(signal.SIGINT, end_read)
```
---
讀取卡片
```python=
while continue_reading:
    # Scan for cards
    (status,TagType) = MIFAREReader.MFRC522_Request(MIFAREReader.PICC_REQIDL)
    # If a card is found
    if status == MIFAREReader.MI_OK:
        print "Card detected"
    # Get the UID of the card
    (status,uid) = MIFAREReader.MFRC522_Anticoll()
```
---
第一個if：把卡號印出，並存起來
第二個if：判斷是否正確，如果錯誤印Authentication error，裡頭驗證是否正確卡號可更改成你的卡號
```python=
 if status == MIFAREReader.MI_OK:
        # Print UID
        print "Card read UID: %s,%s,%s,%s" % (uid[0], uid[1], uid[2], uid[3])
        # This is the default key for authentication
        key = [0xFF,0xFF,0xFF,0xFF,0xFF,0xFF]
        # Select the scanned tag
        MIFAREReader.MFRC522_SelectTag(uid)
        # Authenticate
        status = MIFAREReader.MFRC522_Auth(MIFAREReader.PICC_AUTHENT1A, 8, key, uid)
        # Check if authenticated
        if status == MIFAREReader.MI_OK:
            MIFAREReader.MFRC522_Read(8)
            MIFAREReader.MFRC522_StopCrypto1()
        else:
            print "Authentication error"
```