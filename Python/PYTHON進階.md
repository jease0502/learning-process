---
tags: python
---
# PYTHON進階

---

## lambda運算式
### 介紹
他跟def的功能一樣，都可以用來定義涵式，下面做個示範

1.先用def
```python=
def max(m, n):
    return m if m > n else n
print(max(10, 3))
>>>10
```
2.使用lambda
```python=
max = lambda m, n: m if m > n else n
print(max(10, 3))
>>>10
```
lambda的公式：lambda arg1, arg2,.... :  expression

注意：
1.lambda是運算是不是陳述句
2.在：後必須是運算式
3.不能有區塊
4.小運算用lambda大運算用def

---

### 仿switch
下面將結合dic和lambda來模擬
```python=
score = int(input('請輸入分數：'))
level = score // 10
{
    10 : lambda: print('Perfect'),
    9  : lambda: print('A'),
    8  : lambda: print('B'),
    7  : lambda: print('C'),
    6  : lambda: print('D')
}.get(level, lambda: print('E'))()
```
在上例中dic中的值式使用lambda所建立的物件，使用get()來設計模擬if else判斷，如果符合裡面的條件就執行裡面的，如果都不符合才執行print('E')

---

## filter()

公式：filter(function, sequence)

傳入booling值來作為條件，並重複執行並收集所有list中元素為true的元素，並放到list中

```python=
def fn(x):
    return x if x>5 else None

a=[1,2,3,4,5,6,7,8,9]
b=filiter(fn,a)
print(b)
>>>[6, 7, 8, 9]
```
---

## map()
公式：map(function, sequence)

將所有元素個別傳到function中進行處理，再將結果以list作為回傳值，並且可使用不只一個list
```python=
def square(x) :
    return x ** 2
map(square, [1,2,3,4,5])
>>>[1, 4, 9, 16, 25]
map(lambda x: x ** 2, [1, 2, 3, 4, 5])
>>>[1, 4, 9, 16, 25]

map(lambda x, y: x + y, [1, 3, 5, 7, 9], [2, 4, 6, 8, 10])
>>>[3, 7, 11, 15, 19]
```
---

## reduce()
公式：reduce(function, sequence)

reduce會依序先取出兩個元素，套入function處理後再與list下一個元素一同作為參數繼續處理，持續動作直到元素都不處理完。

```python=
def add(x, y) :      
    return x + y
reduce(add, [1,2,3,4,5])
>>>15
reduce(lambda x, y: x+y, [1,2,3,4,5])
>>>15
```


---

## list
```python=
list[1:]
```
取位置1後面的資料

---
### 列表推導式
它的結構是在一個中括號裡包含一個表達式，然後是一個for語句，然後是0個或多個for或者if語句。那個表達式可以是任意的，意思是你可以在列表中放入任意類型的對象。返回結果將是一個新的列表，在這個以if和for語句為上下文的表達式運行完成之後產生。
規範
```python=
variable = [out_exp for out_exp in input_list if out_exp == 2]
```
示範：
```python=
multiples = [i for i in range(30) if i % 3 is 0]
print(multiples)
# Output: [0, 3, 6, 9, 12, 15, 18, 21, 24, 27]
```
也可以拆開來寫
```python=
squared = []
for x in range(10):
    squared.append(x**2)
```
分開來：
```python=
squared = [x**2 for x in range(10)]
```

---
## if 的進階應用
```python=
#拿來回傳直時使用
def larger(num1, num2):
    return num1 if num1 > num2 else num2
#一般判斷式使用
a = 10
b = 20
c = a if a > b else b
print(c)
```
if他可以用在return數值或是等號後面，作為一個回傳數值時，拿來補充判斷用

---

## 元組tuple

```python=
t1=(13,'th',2)
print(t1[0]) #13
print(t1*2)  #(13,'th',2,13,'th',2)
print(t1+t1) #(13,'th',2,13,'th',2)
print(t1[1:3]) #(13,'th')
```

跟list不一樣的點在於，它裡面的資料無法改變，如果要改變，需先將他變成list在換回來

```python=
t1=(13,'th',2)
t2=list(t1)
t2[0]=1
t1=tuple(t2)
print(t1) #(1,'th',2)
```

---

## _main_

1.確認模組呼叫狀態
2.寫函數測試

模塊有一些內置屬性，用於完成特定的任務，如__name__、__doc__。每個模塊都有一個名稱，例如，__name__用於判斷當前模塊是否是進程的入口，如果當前進程正在被使用，__name__的值為“__main__”。通常給每個模塊都添加一個條件語句，用於單獨測試該模塊的功能。例如，創建一個模塊myModule。

```python=
if __name__=="__main__":
        print("myModule作為主進程運行")
else:
        print("myModule被另一個模塊調用")

>>>myModule作為主進程運行
```

---

### 自動補0
```python=
c=input("input 4 number")
c=c.rjust(4,"0")
```
自動排序，並且排序成文字
```python=
"".join(sorted(c))
"".join(sorted(c)[::-1])
```

---

### 基礎的class物件
```python=
class myc
    r=1.0
    def _init_(self,r):
        self.r=_r
    def A(self):
        return (3.14*self.r*self.r)
    def C(self):
        return (2*3.14.self.r)
x=myc(3.0)
```

---
