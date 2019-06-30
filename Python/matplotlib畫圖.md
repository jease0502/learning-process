---
tags: python
---
# matplotlib畫圖

---
## matplotlib
---
### 介紹

matplotlib常跟numpy和pandas一起使用

起手示:
```python=
import matplotlib.pyplot as plt
```

---
```python=
plt.figure(figsize=(8,4))
```
這是用來決定你的圖片大小，單位為英寸，前為寬後為 長，所以這張圖的像素為寬8x80 長 4x80，640x320像素。
```python=
plt.plot(x,y,label="$sin(x)$",color="red",linewidth=2)
plt.plot((x,z,"b--",label="$cos(x)$")
```
這是用來畫線的，x,y是指你在圖中的線的x軸y軸，所以你要把資料給這兩個函數，像是你如果要指定x軸是1,2,3則要用list得方式給他，這便會使用到numpy，如果你只要一個變數y的話，他的x軸會自動用0,1,2,3來撰寫。
- label也就是幫你的線條取名子，此名子會在legend中顯示。只要在字符串前後添加$便會去使用內建的latex的數學公式來進行帶入。
- color決定你線條的顏色。
- linewidth決定線條寬度。
- b--代表著線條顏色為藍色，他所畫出來的線條為虛線。

---
當然還有其他函數式:
- xlabel  設置x軸文字
- ylabel  設置y軸文字
- title設置圖表標題
- legend圖標圖示
```python=
plt.getp(lines[1])   可以得到所有的相關設定
plt.getp(lines[0],"color") 可以得到顏色屬性
```
getp的兩種使用方法:
1.指定屬性名:輸出你指定屬性的值
2.不指定屬姓名:打印出所有的值
```pytohn=
subplot(numRows,numCols,plotNum)
```
這個函數是拿來分割區域的
- scatter()是畫散步圖的
- show()拿來show線的
- grid()開啟網格

---

上面都是在介紹一張圖片裡面的參數設定，但是沒有提到如何顯示圖片
最重要步驟是：
```python=
plt.show()
```
這樣就可以得到一張美美的圖片了

---

### 範例圖：
![](https://i.imgur.com/Gukefqa.png)
![](https://i.imgur.com/9sl61QW.png)
![](https://i.imgur.com/KuDr4kO.png)

---
## SEABORN
---
如果你還是嫌matplotlib畫圖太醜，試試看用seaborn吧~

起手式~
```python=
import seaborn as sns
```
範例
```python=
import seaborn as sns
import matplotlib.pyplot as plt
sns.pairplot(data, x_vars= ['GDP','URI','SR'], y_vars='Sales', hight=7, aspect=0.8, kind='reg')
plt.show() 
```
- data, x_vars=['TV','Radio','Newspaper'] x軸資料
- y_vars='Sales'  y軸資料
- hight 定義圖表高度
- hue, col, row  定義data子集的變量，並在不同的子集中畫出來
- markers 定義散點的圖標
- col_wrap  設置每行子圖數量
- order 多項式回歸，設定指數
- logistic  邏輯回歸
- logx    轉化為log(x)
- aspec  線的粗度
- kind 你要畫甚麼~目前這個套件給兩種方法scatter(散點圖)和reg(線圖)

