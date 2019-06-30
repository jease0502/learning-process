---
tags: python
---
# NUMPY
---
### [練習題](https://github.com/PoLun-Wang/Learn_NumPy)

---

Numpy簡單來說就是陣列，也就是拿來算線性代數的??!
它可以用來處理多維度的陣列，一維稱為vector二維陣列為 matrix。
因為他是陣列當然是用LIST啦!

---
## 基本示範:
```python=
import numpy as np
np1 = np.array([1, 2, 3])
np2 = np.array([3, 4, 5])
print(np1 + np2) 
>>> [4 6 8]
print(np1.ndim, np1.shape, np1.dtype)
>>> 1 (3,) int64 => 一維陣列, 三個元素, 資料型別
```
---
## 從檔案取資料：
```python=
npd = np.genfromtxt('data.csv', delimiter=',')
```
---
## 改變陣列維度：
```python=
np3 = np3.reshape([2, 3])
print(np3.ndim, np3.shape, np3.dtype) 
>2 (2, 3) int64
```
---
## 改變陣列型別（bool、int、float、string）：
1.bool 可以包含 True、False
2.int 可以包含 int16、int32、int64。其中數字是指 bits。
3.float 可以包含 16、32、64 表示小數點後幾位。
4.string 可以是 string、unicode。nan 則表示遺失值。
```python=
np3 = np3.astype('int64')
np3.dtype
>>> dtype('int64')
```
---
## 倒序

倒序[::-1]只是單純的把順序反過來，並無數值大小比較
```python=
a = np.arange(10) ** 2
print("a[:,:,-1])=> {0}".format(a[::-1]))
```
>a[:,:,-1])=> [81 64 49 36 25 16  9  4  1  0]


---
## 建立陣列:
建立填滿 0 或 1 的陣列：
```python=
np1 = np.zeros([2, 3]) # array([[ 0.,  0.,  0.], [ 0.,  0.,  0.]])
np2 = np.ones([2, 3]) # array([[ 1.,  1.,  1.], [ 1.,  1.,  1.]])
```
---

## 一維陣列
操作和Python的list類似：
```python=
np3=np.array([1, 2, 3, 4, 5, 6])
print(np3[2]) 
>>> 3
```
---
## 二維陣列：
```python=
np3 = np3.reshape([2, 3])
print(np3[1, 0]) 
>>>4
```
---
## 多維陣列取值
多維陣列在for loop中取值時，會以第一維度為優先！
以二維陣列為例：一層for loop優先獲取的陣列內容，就是第一維度每row的內容！
```python=
b = np.arange(1, 41).reshape(5, 8)
 print()           
for row in b:
    print(row)
```
>[1 2 3 4 5 6 7 8]
[ 9 10 11 12 13 14 15 16]
[17 18 19 20 21 22 23 24]
[25 26 27 28 29 30 31 32]
[33 34 35 36 37 38 39 40]

---
## 矩陣堆疊(Stacking)
這還蠻常用到的…這功能可以方便運算時矩陣串接的需求！
```python=
np.vstack(a, b)：將a, b矩陣沿著垂直軸堆疊！
np.hstack(a, b)：將a, b矩陣沿著水平軸堆疊！
>a = np.arange(1,11).reshape(2,5)
print("a=>\n{0}".format(a))
print()
**水平堆疊**
print("np.vstack((a,a))=>\n{0}".format(np.hstack((a,a))))
print()
**垂直堆疊**
print("np.hstack((a,a))=>\n{0}".format(np.vstack((a,a))))
```
>a=>[[ 1  2  3  4  5][ 6  7  8  9 10]]
np.hstack((a,a))=>[[ 1  2  3  4  5  1  2  3  4  5][ 6  7  8  9 10  6  7  8  9 10]]
 np.vstack((a,a))=>[[ 1  2  3  4  5][ 6  7  8  9 10][ 1  2  3  4  5][ 6  7  8  9 10]]
 
---
## 基本操作
使用布林遮罩來取值：
```python=
np3 = np.array([1, 2, 3, 4, 5, 6])
print(np3 > 3) 
>>>[False False False  True  True  True]
print(np3[np3 > 3]) 
>>> [4 5 6]
```
---
## 加減乘除(取代)：
```python=
np3 = np3.reshape([2, 3])
print(np3.sum(axis=1)) 
>>>將axis=1 橫向加總 [6 15]
```
- sum：矩陣加總
- sum：axis=0或1  算是進階用法，可以指定要加總的維度是哪一個
- cumsum：這是可以拿來對陣列值做出累計加總的效果，可以用在一維陣列上， 數值就可以直接拿來畫出累計趨勢圖喔～
- min：矩陣最小值
- max：矩陣最大值
- mean：矩陣平均值
- .sqrt：元素開平方根
- .exp：矩陣內所有元素進行Exponential function(e)運算
- .add：矩陣或陣列相加

---
## 索引與切片

Indexing 索引的用途不外乎就是為了要從陣列和矩陣中取值，但除此之外有很多種功能！可以取出連續區間，還可以間隔取值！
選取連續區間 [a:b]
選取索引值a到b的資料x[a:b]
a：選取資料的起始索引，不指定表示從頭開始
b：選取資料的結束索引+1，不指定表示直到陣列結束
```python=
a = np.arange(10) ** 2
print("a=> {0}".format(a))
print()
print("a[2:5]=> {0}".format(a[2:5]))
>> a=>[ 0 1 4 9 16 25 36 49 64 81]
>> a[2:5]
>> a[2:5]=>[ 4 9 16]
```

Slicing 切片的用途和索引(Indexing)很像！若能活用便能加快程式撰寫速度！
間隔選取[::c]
以1維陣列來說明x[a: b :c]
a：選取資料的起始索引
b：選取資料的結束索引+1
c：選取資料間隔，以索引值可以被此值整除的元素，不指定表示1
從index為3起算，每數到4的元素值都改為9999，直到第8個元素(index為7)為止
```python=
>a = np.arange(10) ** 2
a[3:8:4]=9999
print("a[3:8:4]=> {0}".format(a))
>>a[3:8:4]=> [0 1 4 9999 16 25 36 9999 64 81]
```
---
## 矩陣分割(Splitting)
將一個陣列或矩陣分割成多個小的矩陣或陣列！
- np.hsplit( matrix, shape/number )：將matrix沿著自己的水平軸分割成指定的形狀(shape)或數量(number)
- np.vsplit( matrix, shape/number )：將matrix沿著自己的垂直軸分割成指定的形狀(shape)或數量(number)

這個函數回傳型別是list！如果還想要利用NumPy的對它操作的話，要把它轉換成numpy.ndarray才行！
```python
a = np.round(np.arange(1, 13).reshape(2, 6)*10, 0)
print("a=>\n{0}".format(a))
print()
print("----hsplit----")
output1 = np.hsplit(a, 3)
i = 0
for smallMatrix in output1:
    print("np.hsplit(a, 3) [{0}]=>\n{1}".format(i, smallMatrix))
    i+=1
print("Type of output1: {0}".format(type(output1)))
newOutput1 = np.array(output1)
print("Shape of output1: {0}".format(newOutput1.shape))
print()
print("----vsplit----")
output2 = np.vsplit(a, 2)
i = 0
for smallMatrix in output2:
    print("np.vsplit(a, 2) [{0}]=>{1}".format(i, smallMatrix))
    i+=1
print()
print("Type of output2: {0}".format(type(output2)))
newOutput2 = np.array(output2)
print("Shape of output2: {0}".format(newOutput2.shape))
```
結果：
>a=>
[[ 10  20  30  40  50  60]
 [ 70  80  90 100 110 120]]
----hsplit----
np.hsplit(a, 3) [0]=>[[10 20][70 80]]
np.hsplit(a, 3) [1]=>[[ 30  40][ 90 100]]
np.hsplit(a, 3) [2]=>[[ 50  60][110 120]]
Type of output1: <class 'list'>
Shape of output1: (3, 2, 2)
----vsplit----
>np.vsplit(a, 2) [0]=>[[10 20 30 40 50 60]]
np.vsplit(a, 2) [1]=>[[ 70  80  90 100 110 120]]
Type of output2: <class 'list'>
Shape of output2: (2, 1, 6)



---

## 重要屬性~
```python=
.ndim
```
>NumPy ndarray 物件的維度

```python=
.shape
```
>ndarry 物件的每一個維度的大小(size)，回傳資料類別為Tuple
```python=
.size
```
>ndarry 物件所組成之array的總元素數量，回應之數值會等於.shape的每個元素相乘

```python=
.dtype
```
>ndarray 物件內組成元素的型態

```python=
.itemsize 
```
>陣列中每一個元素的大小(Bytes)
>>ex: int16=>16/8=2 Bytes
```python=
.data
```
>這是一個存有實際陣列元素的緩衝，通常我們不需要使用這個屬性，因為我們可以使用index存取這些元素。
```python=
.zeros( (陣列各維度大小用逗號區分) )
```
>建立全為0的陣列，可以小括號定義陣列的各個維度的大小！
>>zeros=>[[0. 0. 0. 0. 0.]
```python=
.ones( (陣列各維度大小用逗號區分) )
```

>用法與np.zeros一樣
>>ones=>[[1. 1. 1. 1. 1.]
```python=
np.empty( (陣列各維度大小用逗號區分) )
```

>用法與np.zeros一樣，但唯一的差別是NumPy不會初始化陣列內元素的初始值，所以內容將會是不確定的。
>>e = np.empty( (2, 5) )
e=>[[25.  25.5 26.  26.5 27. ]

```python=
np.arange( 起始值, 結束值, 步幅, 資料型別 )
```

>也是產生一維陣列，和np.array()的差別在於arange擁有較大的彈性，而且元素數值是自動化產生！步幅決定每隔多少數值產生一個元素(等差的概念)。
>>r1 = np.arange(25, 30, .5)
r1=>[25.  25.5 26.  26.5 27.  27.5 28.  28.5 29.  29.5]
```python=
np.linspace( 起始值, 結束值, 起始與結束的區間內要產生幾個元素 )
```
>這個在畫線時還蠻常用到的！只要給定陣列的區間(起始值、結束值)，就可以要求在這個區間內產生幾個元素！
>in = np.linspace(3, 5, 9)
```python=
print("lin=>\n{0}".format(lin))
```
>lin=>[3.3.253.5 3.75 4.4.25 4.5  4.75 5.  ]
```python=
.set_printoptions( 列印選項 )
```
>這是一個全域設定，以下會說明各個不同的選項代表的意義與控制的項目。
```python=
.set_printoptions( threshold=元素門檻值 )
```
>NumPy預設值是1000。意思是如果陣列元素值沒有超過門檻值的話，NumPy就會讓Python將所有元素列印出來！
當陣列元素數量到達一定量的時候，就可能會需要用到這個方法！

```python=
np.set_printoptions( precision=浮點數列印精度 )
>控制陣列內容微幅點數時的列印精度(小數位數)，下列範例看得出來這個方法是會自動四捨五入的喔！
```
```python=
np.set_printoptions( edgeitems=省略列印內容時要顯示的元素數量 )
```
>當列印陣列時需要省略內容，edgeitems會決定要印出來的元素有幾個。

```python=
np.set_printoptions( linewidth=每一行要印出幾個字元 )
```
>這只是單純決定列印陣列時每一行字的字元數上限喔，並不影響列印其他內容的每一行字元數上限！
>
```python=
np.set_printoptions( suppress=是否要抑制顯示小數位 )
```
>其實這個我不太知道該怎麼解釋才夠完全，但我對這個功能的理解是用來“抑制顯示小數位數”，而預設值是False(代表不要抑制顯示小數位，就是通通給我顯示)。
```python=
np.set_printoptions( nanstr=當陣列元素值出現NaN時所顯示的字串 )
```
>當陣列元素值出現not-a-number時要顯示的內容為何。沒錯，這個也可以改！
```python=
np.set_printoptions( infstr=當陣列元素值出現inf時所顯示的字串 )
```
>當陣列元素值出現inf(無限大)時要顯示的內容為何。

```python=
np.set_printoptions( sign=控制正負號 )
```
>當sign=’+’時，就會連正數都會加上正號；當sign=’-‘時(預設值)，就是只有數值<0時，才會加上負號！

```python=
np.set_printoptions( formatter={ 使用lambda函數客製列印陣列元素的格式 } )
```
>元素內容格式也能客製，甚至能在列印時改變數值呢！

---
關鍵字
all：各種型別都套用格式
float_kind：只套用floatxx
int_kind：只套用intxx
str_kind：只套用字串

---



