---
tags: 演算法
---
# 分治算法 D&C

## 介紹
它通過將復雜的問題分解(devide) 成兩個或多個同類型(或相關類型)的子問題，直至達到能直接解決(conquer)的程度(否則繼續分解或遞歸) ，最終合併(combine) 成原始問題的解來實現分治。

## 分治法的適用特徵

- 問題通過分解將問題規模縮小到一定的程度就可以容易地解決
- 問題分解為的若個規模同類型(或相關類型)的子問題具有最優子結構性質。
- 利用該問題分解出的子問題的解可以合併為該問題的解
- 問題所分解出的各個子問題是互斥的，即子問題之間不包含公共的子子問題。

## 基本想法與步驟

在分治策略中，在每個層次遞迴中應用了三個步驟：
1.分解(Divide): 將P分解為較小的子問題P1 ,P2 ,...,Pk
2.解決(Conquer):直接解決、遞迴解決
3.合併(Combine):合併子問題， return(T)
>子問題足夠大需要遞迴時，稱遞迴情況(recursive case)。足夠小可以直接解決，稱基本情況(base case)。如果除了與原問題形式完全一樣的規模更小的子問題外，還需求解不一樣的子問題，將其看做合併。
>遞迴與分治緊密相關，遞迴式很容易刻畫分治算法的時間複雜度。一個遞迴式是一個等式或者不等式，通過更小的輸入上的函數值來描述。

通常，解決這類問題（一直遞歸式，找答案）有三種方法：
1) 數學歸納法(Mathematical Induction)
2) 遞迴樹找規律(Recursion Tree)
3) 主定理(Master Theorem)

## 與二分查找區別
二分查詢的基線條件是陣列只包含一個元素。如果要查詢的值與這個元素相同，就找到了！否則說明它不在陣列中。遞迴條件為把陣列分成兩半，將其中一半丟棄，並對另一半執行二分查詢。

## 程式示範
1.相加add
```python=
def sum(list):
	if list == []:
		return 0
	return list[0]+sum(list[1:])
list=[]
z=eval(input("請輸入幾位數相加"))
for x in range(z):
	y=eval(input())
	list.append(y)
print(sum(list))
```
其中的sum()就是使用分治所寫出來的，舉個例子，我們有[1,2,3]要相加，我們先將list[0]提出來，然後加上原函式，直到遞迴條件結束，在原函式中我們每次都跟新一次list，每次都從第2位開始，使他成為一個新的list，這樣去做遞迴，來達到目標

---
2.數數count
```python=
def count(list):
	if list == []:
		return 0
	return 1+count(list[1:])
list=[1,2,3,4,5,6,7,8,9,10]
print(count(list))
```
跟上面一樣，每次都使list減少一位，直到list為空，才停止動作，每次皆會+1來計算有多少數字在裡頭

---
3. 找最大 max
```python=
def max(list):
	if len(list)==2:
		return list[0] if list[0]>list[1] else list[1]
	sub_max=max(list[1:])
	return list[0] if list[0]>sub_max else sub_max
list=[50,14,45,4,14,2]
print(max(list))
```
跟上面一樣，採用遞迴，當list大小=2時開始進行判斷(2分查詢-)，然後一層一層判斷上去，從後面開始判斷，最後輸出最大值

---