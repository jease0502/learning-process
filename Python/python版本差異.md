---
tags: python,基礎
---
# python版本差異
---
## 介紹

眾所皆知python分成py2和py3兩種版本，那他們又有甚麼不同呢?下面將舉幾個例子介紹

## 編碼
首先先從編碼講起，在PY2中使用的預設編碼為```asscii```而PY3則是使用了UTF-8，原因在於python出生時，unicode還沒出生，所以py2當然部會用unicode啊~

```python=
#python2
sys.getdefaultencoding()
>>>'ascii'

#python3
sys.getdefaultencoding()
>>>'utf-8'
```

## 輸出
在python2時，print是一個一條語句，而在python3時他是函數式。當然你可能會有疑問，py2不適也可以用函式的打法嗎....，下面直接進入示範吧~
```python=
#py2
print("hello")
>>>hello
print "hello"
>>>hello

#py3
print("hello")
```
這樣看可能不明顯我們來看另外一個案例
```python=
print("hello", "world")
>>>('hello', 'world')
```
從這個例子中我們可以發現在這邊，python2把("hello")當作元組了，而在py3中print函數可以接受多個位置參數。

## 字符串
字符串可以說是改變最大的項目之一，這個變動降低了編碼錯誤的產生，在python2中字符串有兩個類型，分別是str、unicode，前者用在文本字符串、後者用在字節序列，不過這兩者界線並沒有明顯的界定出來，所以使得開發者粉混亂。不過在python3中，他將這兩者明顯的區分出來了~
|py2|py3|表現|轉換|作用
|--|--|--|--|--|
|str|byte|字節|encode|處存、傳輸
|unicode|str|字符|decode|展示

## True和False
在py2中有一個很好玩的點，他的```TRUE```和```FALSE```是一個變數，所以我們可以去指派值給他，這是一個很詭異的地方，在PY3把她修正了過來，使得```TRUE```和```FALSE```是固定無法改變的變數了。
```python=
#py2
True=1
print true
>>>1

#py3
True=1
>>> File "<stdin>", line 1
SyntaxError: can't assign to keyword
```
很明顯的在py3他是會噴error的~

## 迭代器

在py2中很多會回傳列表的內建函數，在py3都被改成回傳類似的迭代器的對象，因為迭代器更有效率。像是在py2中有```xrange```和```range```在py3中都合併成```range```，還有字典的```dict.key()```、```dict.values```方法都不再回傳list了，而是像迭代器的```view```對象回傳。還有高階函數```map```、```filter```、```zip```都跟前幾個依樣不再回傳list。。Py2的迭代器必須用```next``` 方法，而Py3改成了```__next__```。

---