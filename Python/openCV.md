---
tags: python
---
# openCV

---

## 介紹

----

OpenCV在影像處理方面應用廣泛，可以讀取儲存圖片、視訊、矩陣運算、統計、影像處理等，可用在物體追蹤、人臉辨識、傅立葉轉換、紋理分析、動態視訊的影像處理等。

---

首先先從安裝開使吧~

----

方法一

>wget http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-armv7l.sh

>sudo /bin/bash Miniconda3-latest-Linux-armv7l.sh
sudo nano /home/pi/.bashrc

在檔案最下方加入
>export PATH="/home/pi/miniconda3/bin:$PATH"
>source ~/.bashrc
>sudo chown -R pi miniconda3

>conda config --add channels rpi
>conda install python=3.6

>pip install opencv-python
>conda install -y -c conda-forge opencv

檢查:
python
import cv2
cv2.__version__

如果成功顯示，代表安裝成功

---

方法二

>https://www.pyimagesearch.com/2017/09/04/raspbian-stretch-install-opencv-3-python-on-your-raspberry-pi/

除了安裝opencv以外還要安裝安裝Dlib
>pip install numpy
pip install scipy
pip install scikit-image
pip install dlib

---