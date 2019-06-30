---
tags: python
---
# csv讀與寫
---
## 操作說明
操作說明：
- r   以讀方式開啟檔案。檔案的指標將放在檔案開頭。這是預設模式
- w   以寫方式開啟
- a   以追加模式開啟(從EOF開始，必要時建立新檔案)
- r+  以讀寫模式開啟
>打開後可以讀取文件，指針在文件開頭，並保有原內容，追加寫內容時，動作則是追加新內容。
- w+  以讀寫模式開啟
>打開後，清空原有內容，成為一個新的空文件，對這個空文件具有讀寫權限。
- a+  以讀寫模式開啟
>與r+很像但是指針在文件尾巴
- rb  以二進制讀開啟
- wb  以二進制寫開啟
- ab  以二進制追加模式開啟
- rb+ 以二進制讀寫模式開啟
- wb+ 以二進制讀寫模式開啟
- ab+ 以二進制讀寫模式開啟
- rt模式下，python在讀取文本時會自動把\r\n轉換成\n.
- wt模式下，Python寫文件時會用\r\n来表示換行。


---
## 實作
開檔案:
```python=
a=open(file.csv,'w+')
```
寫入
```python=
a.write('this is txt')
```
存檔
```python=
a.close()
```
唯獨觀看
```python=
a=open(file.csv,'r')
line=a.readline()
print(line)  
a.close()

>>>this is txt
```
或是用with as來撰寫

with as是一個判斷式，他用於在一個任務需要事先設置條件，事後進行清理工作時使用。像下面的例子是你要先打開.csv，打開後處理中間的程式，最後去呼叫as後面的程式碼，也就是呼叫c，並去關閉.csv。
P.s 程式中的c是我在這個程式中所取的參考變數，你可以自行更改

```python=
with open("檔名", "w",newline='',encoding='utf-8') as c: 
    writer = csv.writer(c)   #寫一個csv檔
    writer.writerow(['NT'])  #這一行是加入一個行名稱
    c.close()
```
newline是有關於換行相關的程式碼
1.當我不打這一行時:
open("檔名", "rt",encoding='utf-8')
程式碼也就會以預設的universal newline來轉換所有的換行為\n

2.但是如果加了newline=''則會去判斷各種換行方式，像是\n \t \r等，在此時又分為直接print跟用for迴圈print兩種結果。
    第一種直接印:讀取時換行字元不會被轉譯
    第二種用for印:能夠有效辨認每種換行符號
    
3.當然你也可以把newline=''換成newline='\n'，但這樣你如果有一行換行符號為\r你那行就會消失。

4.當你在讀取也可以更懶惰的直接打檔名.read()，這樣你沒有經過任何的轉換，直接打出來的程式碼會有一個問題，不會去讀取換行，這樣子你就不會換行了~

