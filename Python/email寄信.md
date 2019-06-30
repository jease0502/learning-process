---
tags: python
---
# email寄信
---
## 介紹

當我們需要透過python來寄發信件時，可以使用smtplib這個內建模組來達成這項工作。

---
## 第一次寄信
P.s這邊的訊息只能傳送英文訊息喔~
先從最簡單的寄信開始吧~
```python=
import smtplib
smtp=smtplib.SMTP('smtp.gmail.com', 587)
smtp.ehlo()
smtp.starttls()
smtp.login('你的信箱','你的密碼')
from_addr='你的信箱'
to_addr="收件人信箱"
msg="Subject:Gmail sent by Python scripts\nHello World!"
status=smtp.sendmail(from_addr, to_addr, msg)#加密文件，避免私密信息被截取
if status=={}:
    print("郵件傳送成功!")
else:
    print("郵件傳送失敗!")
smtp.quit()
```
開始講解程式碼吧~
- ```smtplib.SMTP```是用來指定你要用誰家的伺服器進行傳輸信件，我這次是使用gmail，他有指定的port號是587。你如果沒有用他指定的就寄不出去了。
- ```smtp.ehlo()```這個步驟是向郵件主機申請身分，成功的話你才能寄出去，這次一定要的步驟不能省略
- ```msg```你的郵件內容，郵件一共分成標題和內文兩個部分，```Subject:```後面的文字直到\n就是標題，```Hello World!```則是內文

- ```if else```判斷式式用來判斷郵件是否寄發成功
- ```smtp.quit()```當然跟sql資料庫一樣，你把人家開機了當來也要關機，所以這個步驟便是關機步驟

---
當然你也可以幫你的信件加上暱稱，只要更改你的msg就好
```python=
msg="Subject:Gmail sent by Python scripts\n\
From:Your best friend\nTo:收件人\nHello World!"
```
- ```From```將你逆增加的暱稱增加在from後面即可，所以這邊你會有暱稱Your best friend
- ```To```跟前面一樣看到TO統一都是寫收件人

---
當然也可以填寫副本收件人，一樣式修改msg的位置
```python=
Cc:a123@yahoo.com,b1234@gmail.com\n\
```
你只要在mag裡面新增這行，然後把信箱改成你要的就可以了~

---
## 第二次寄信

### 介紹
接些來我們來試試看寄圖片出去吧~
因為```smtplib```無法傳輸影音、圖片，所以我們需要另外一個套件來進行輔助。為了解決這個問題，我們需要```MIME協定```。

---

### MIME
MIME分成兩種格式，一種是type，一種是subtype。

常用的type：
| type | 說明 |
| -------- | -------- |
 text|	 文字
 image|	 圖片
 audio	| 音樂
 video	 |影片
 multipart|	 一部分連結是影片
 message	| 訊息
 application|	 exe和二進位資料
 
 常用的subtype：
 
 |MIME 資料次型態 subtype	| 說明|
 |--|--|
 application/octet-stream|	 二進位資料
 application/pdf	 |Adobe pdf
 application/msword	Microsoft| Word
 text/plain	 |純文字
 text/html	 |HTML 網頁
 image/gif	 |GIF 圖片
 image/png	 |PNG 圖片
 image/jpeg	 |JPEG 圖片
 video/mp4	 |MP4 影片
 video/mpeg	 |MPEG 影片
 video/ogg	 |OGG 影片
 video/webm	 |WEBM 影片
 multipart/x-www-form-urlencoded	| HTTP 以 POST 提交之表單
 multipart/form-data	| HTTP 以 POST 提交之表單有附檔上傳
 
當然python也是有內建模組的，模組名為```email.mime.text```且是可以處理非 ASCII 編碼文字的郵件與二進位檔問題, 其介面如下
```python=
email.mime.text.MIMEText(text [, subtype [, charset]])
```
他的參數有：
1. text:要傳送的資料 (文字, 圖片, 視訊, 檔案等)
2. subtype:資料的次型態, 預設為 "plain" (純文字)
3. charset:資料編碼類型, 預設為 "us-ascii"

---
### 中文寄信~

```subtype```只要將上面表格中斜線後面的部分即可,例如預設是"plain"他就沒有把text寫進去
如果要傳送有中文的訊息，就要用charset並將語言改成"utf-8"(unicode 編碼)這樣才能正常的傳輸中文

```python=
import smtplib
from email.mime.text import MIMEText

mime=MIMEText("你好世界 hollo world!", "plain", "utf-8") #撰寫內文內容，以及指定格式為plain，語言為中文
mime["Subject"]="test測試" #撰寫郵件標題
mime["From"]="嗚嗚嗚" #撰寫你的暱稱或是信箱
mime["To"]="嚶嚶嚶" #撰寫你要寄的人
mime["Cc"]="@gmail.com, @gmail.com" #副本收件人
msg=mime.as_string() #將msg將text轉成str

smtp=smtplib.SMTP("smtp.gmail.com", 587)  #googl的ping
smtp.ehlo() #申請身分
smtp.starttls() #加密文件，避免私密信息被截取
smtp.login("你的信箱", "密碼") 
from_addr="你的信箱"
to_addr=["收信人信箱"]
status=smtp.sendmail(from_addr, to_addr, msg)
if status=={}:
    print("郵件傳送成功!")
else:
    print("郵件傳送失敗!")
smtp.quit()
```

 ---
### html信~

你想要將你信的內文長得很特殊的話，就可以使用這個功能~
```python=
import smtplib
from email.mime.text import MIMEText
# 以下為html內容
html="""
<!doctype html>
<html>
<head>
  <meta charset='utf-8'>
  <title>HTML mail</title>
</head>
<body>
  <b>嚶嚶嚶</b>
</body>
</html>
"""
mime=MIMEText(html, "html", "utf-8")
mime["Subject"]="test測試" #撰寫郵件標題
mime["From"]="嗚嗚嗚" #撰寫你的暱稱或是信箱
mime["To"]="嚶嚶嚶" #撰寫你要寄的人
mime["Cc"]="@gmail.com,@gmail.com" #副本收件人
msg=mime.as_string() #將msg將text轉成str
print(msg)   #看你要不要印出來~

ssmtp=smtplib.SMTP("smtp.gmail.com", 587)  #googl的ping
smtp.ehlo() #申請身分
smtp.starttls() #加密文件，避免私密信息被截取
smtp.login("你的信箱", "密碼") 
from_addr="你的信箱"
to_addr=["收信人信箱"]
status=smtp.sendmail(from_addr, to_addr, msg)
if status=={}:
    print("郵件傳送成功!")
else:
    print("郵件傳送失敗!")
smtp.quit()
```
在第22行把```msg```的資料印出來，你可以看到他會把你內文的細節印出來，你會看到你寄出去的內容，在最下面會有以base64型態編碼成 ASCII 字元進行傳送。

![](https://i.imgur.com/l9ocOAq.jpg)

---
### 寄送檔案
```python=
import smtplib
from email.mime.text import MIMEText

#讀取檔案
with open("test.txt", "rb") as file:
    filecontent=file.read()

mime=MIMEText(filecontent, "base64", "utf-8")   
mime["Content-Type"]="application/octet-stream"   
mime["Content-Disposition"]='attachment; filename="test.txt"' 
mime["Subject"]="test測試" #撰寫郵件標題
mime["From"]="嗚嗚嗚" #撰寫你的暱稱或是信箱
mime["To"]="嚶嚶嚶" #撰寫你要寄的人
mime["Cc"]="@gmail.com,@gmail.com" #副本收件人
msg=mime.as_string() #將msg將text轉成str
print(msg)

smtp=smtplib.SMTP("smtp.gmail.com", 587)  #googl的ping
smtp.ehlo() #申請身分
smtp.starttls() #加密文件，避免私密信息被截取
smtp.login("你的信箱", "密碼") 
from_addr="你的信箱"
to_addr=["收信人信箱"]
status=smtp.sendmail(from_addr, to_addr, msg)
if status=={}:
    print("郵件傳送成功!")
else:
    print("郵件傳送失敗!")
smtp.quit()

```
注意：在```mime["Content-Disposition"]='attachment; filename="test.txt"' ```當你的檔名用雙引用，你整個屬性就必須使用單引號，如果檔案是單引號，整個屬性就必須使用雙引號

---
## 寄送圖片 
如果要寄送圖片的話，需要再增加一個模組``` email.mime.image.MIMEImage ```
他的公式是```email.mime.image.MIMEImage(_imagedata[, _subtype[, _encoder[, **_params]]])```

所以我們總共需要三個：
```python=
import smtplib
from email.mime.text import MIMEText
from email.mime.image import MIMEImage
```
圖檔將以binary二進制方式讀取後傳給MIMEImage，跟傳送文字檔一樣，我們要去指定content-type屬性為```application/octet-stream```，

然而程式碼又可用兩種方式撰寫：
- 第一種是用2進制的方式傳送
- 第二種是使用直接傳送圖片

第一種程式碼：
```python=
import smtplib
from email.mime.text import MIMEText
from email.mime.image import MIMEImage

with open("test1.jpg", "rb") as file:
    filecontent=file.read()

mime=MIMEImage(filecontent)
mime["Content-Type"]="application/octet-stream"  
mime["Content-Disposition"]='attachment; filename="test1.jpg"'   #寫你的檔案名讓他可以找到
mime["Subject"]="test測試" #撰寫郵件標題
mime["From"]="嗚嗚嗚" #撰寫你的暱稱或是信箱
mime["To"]="嚶嚶嚶" #撰寫你要寄的人
mime["Cc"]="@gmail.com, @gmail.com" #副本收件人
msg=mime.as_string() #將msg將text轉成str
print(msg)

smtp=smtplib.SMTP("smtp.gmail.com", 587)  #googl的ping
smtp.ehlo() #申請身分
smtp.starttls() #加密文件，避免私密信息被截取
smtp.login("你的信箱", "密碼") 
from_addr="你的信箱"
to_addr=["收信人信箱"]
status=smtp.sendmail(from_addr, to_addr, msg)
if status=={}:
    print("郵件傳送成功!")
else:
    print("郵件傳送失敗!")
smtp.quit()
```
第一種沒有任何bug，任何收件軟體都收的到，但第二種就不是了~

第二種程式碼：
```python=
import smtplib
from email.mime.text import MIMEText
from email.mime.image import MIMEImage

with open("test1.jpg", "rb") as file:
    filecontent=file.read()

mime=MIMEImage(filecontent, "image/jpeg")
mime["Content-Type"]="image/jpeg"
mime["Content-Disposition"]='attachment; filename="test1.jpg"'
mime["Subject"]="Gmail sent by Python scripts(圖片附檔測試)"
mime["From"]="Your best friend"
mime["To"]="mailgroup"
#mime["Cc"]="mycompanymail@blablabla.com.tw"
msg=mime.as_string()
print(msg)

smtp=smtplib.SMTP("smtp.gmail.com", 587)  #googl的ping
smtp.ehlo() #申請身分
smtp.starttls() #加密文件，避免私密信息被截取
smtp.login("你的信箱", "密碼") 
from_addr="你的信箱"
to_addr=["收信人信箱"]
status=smtp.sendmail(from_addr, to_addr, msg)
if status=={}:
    print("郵件傳送成功!")
else:
    print("郵件傳送失敗!")
smtp.quit()
```
很莫名其妙的當我使用windows的收件軟體收郵件，圖片會自動消失，但是當我使用gmail收件時，圖片卻是存在的，這代表圖片有確實寄發出去，但是因為神秘原因消失了，所以如果要避免這個問題，建議使用方法一~

---


