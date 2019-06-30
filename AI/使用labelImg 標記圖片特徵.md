---
tags: AI
---
# 使用labelImg 標記圖片特徵
---
首先先去這邊下載labelImg，[連結](https://tzutalin.github.io/labelImg/)

p.s.我是使用1.5.2windows 

---
## 標記名稱設定

在data資料夾裡有一個文件predefined_classes，他是在存放你要標記的標籤名稱，像是他預設裡面會有dog、person、cat、tv、car，這些便是他的預設標籤。

---
## 加入圖片

在data資料夾中創建一個img資料夾，並將圖片放進去，圖片名稱不限

---
## XML檔處存位置

圖片在標記後都會產生一個xml檔，我們需要創建一個annotation資料夾來存放資料

---
## 開始標記

1.開啟exe檔
2.點選open dir 決定圖片的存放位置
3.點選Change Save Dir 決定XML檔存放位置
4.新增標記方框需要點Create RectBox 即可用滑鼠標記你的目標位置
5.按下SAVE 即可儲存標記
6.按下NEXT Image繼續標記下一張圖片

p.s標記是一件很辛苦的事情，別心急~

---


