---
tags: python,sql
---
# MySQL
---
## 連線
首先先給個連線的方法
```python=
conn= MySQLdb.connect(host='',port = ,user='',passwd='',db ='',)
		cur = conn.cursor()
		cur.execute("insert into time values(c,b)")
		cur.close()
		conn.commit()
		conn.close()
```
## 說明
說明:
- conn裡面打的是我要連的mysql的資訊，host是ip位置，port就是你要進去的通道，user你的帳號，password密碼，db你資料庫的名子
- cur = conn.cursor()呼叫一下跟他說你要用了
- cur.execute把資料上傳上去的位置，time是我欄位的名子，一個大的資料庫裏面有很多欄位，所以你要去指定他不然他會不知道丟到哪邊，欄位裡面還有你所設的變數處存格，所以變數放的位置很重要，一放錯就死了。
- cur.close()告訴他你不用了
- conn.commit() 提交也就是資料上傳
- conn.close()把資料庫關起來~

---

接下來是將MYSQL中的資料抓下來整理成CSV檔
```python=
dbQuery='SELECT * FROM root2.time;'
	conn= MySQLdb.connect(host='',port = ,user='',passwd='',db ='',)
	cur=conn.cursor()
	cur.execute(dbQuery)
	result = cur.fetchall()
#Getting Field Header names
	path="/home/pi/MFRC522-python/logindata.csv"
	c = csv.writer(open(path,"wb"))
	for row in result:
   		c.writerow(row)
```
說明：
- dbQuery='SELECT * FROM root2.time;'這行代表著我要進行的動作，我要去選擇root2這個資料表，然後我要裡面的time這筆數據，是SQL刪除指令

- result=cur.fetchall()把抓到的資料存到result裡面

- path存放著我的目的路徑

- 寫入[csv](https://hackmd.io/T5zwkvmgQKevQhIZuEuV6A)可以去看我的csv筆記

- 因為你從資料庫裡頭抓到的資料是橫的，你要改成直的所以需要用個for迴圈來儲存，而不是直接存進去

---

接下來介紹如何清除你要清除的資料吧~
```python=
deleteSql="delete from time "
	sql=deleteSql
	conn=MySQLdb.connect(host='',port = ,user='',passwd='',db ='',)
	cursor=conn.cursor()
	cursor.execute(sql)
	conn.commit()
	cursor.close()
	conn.close()
```
說明：
- deleteSql="delete from time "SQL的刪除指令

---

總而言之，當你要對資料庫做甚麼動作，只要在cursor.execute()中輸入你要的SQL指令即可

---
以下補充一些可能用到的值:
- rollback() 往上滾，也就是取消提交上一筆資料

- cursor用来接收返回值的方法:

- fetchall(self):接收全部返回的结果

- fetchmany(self, size=None):接收size返回的结果，如果size的值大於返回的結果的數量,則會返回cursor.arraysize條數據.

- fetchone(self):返回結果

- scroll(self, value, mode='relative'):移動游標到某一行，如果mode='relative',則表示從當前所在行移動到value條,如果 mode='absolute',則表示從結果集的第一行移動value條.

---
cursor用來執行命令的方法:
- callproc(self, procname, args):用來執行存儲過程,接收的參數為存儲過程名和參數清單,返回值為受影響的行數

- execute(self, query, args):執行單條sql語法,接收的參數為sql語法本身和使用的參數列表,返回值為受影響的行數

- executemany(self, query, args):執行sql語句,但是重複執行參數列表裡的參數,返回值為受影響的行數

- nextset(self):移動到下一個結果集





