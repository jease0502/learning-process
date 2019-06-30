---
tags: python,iot
---
# Raspberry 相機

---

## 程式碼~
```python=
start_preview()  預覽
stop_preview()  關閉預覽
capture('你的目錄') 拍照
start_recording() 錄影
stop_recording() 停止錄影
omxplayer 回放
```
當然還有很多參數~
像是調整焦距跟一些參數
```python=
camera.framerate = 15             #幀率
camera.contrast = i               #對比
camera.exposure_mode = 'beach'    #曝光
camera.awb_mode = 'sunlight' 
camera.resolution = (2592, 1944)  #解析度
camera.brightness = 70            #亮度
camera.image_effect = 'colorswap'  
```
## 注解
```python=
camera.annotate_text = "Brightness: %s" % i   
camera.annotate_background = Color('blue')
camera.annotate_foreground = Color('yellow')
camera.annotate_text_size = 50
```
## python範例程式:
```python=
from picamera import PiCamera
from time import sleep

camera = PiCamera()

camera.start_preview()
sleep(5)
camera.capture('/home/pi/Desktop/image.jpg')
camera.stop_preview()

```
當然也可以連拍，就用for迴圈吧!