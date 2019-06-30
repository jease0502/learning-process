---
tags: python,基礎
---
# python簡介
---
## 簡介
python是目前較為流行的幾種語法之一，無論是架站、機器學習、數據整理，都可以使用python，且他擁有大量的套件可供使用者愉快地去使用他~
接下來就讓我們開始愉快地來打python吧~

## 版本

以目前來說```PYTHON```主要分成```PY2```以及```PY3```,他們有著些許差異，像是編碼、字符串、輸出、語法、優化等等。他們的差異我放在其他頁面中，建議等全部學習完再閱讀兩者差異。

## 編譯器

而在編譯器方面PYTHON又有多種編譯器，以下便將幾種常用的編譯器整理出來~
目前編譯器有分成多種：

- CPython
    - 目前最為廣泛的編譯器
    - 使用c語言進行編譯
- PyPy
    - 用RPython實現的解釋器。
    - RPython是Python的子集。
    - 具有靜態類型。
    - 這個解釋器的特點是即時編譯，支持多重後端（C, CLI, JVM）。
    - PyPy旨在提高性能，同時保持最大兼容性（參考CPython的實現）。
- Jython
    - Jython是一個將Python代碼編譯成Java字節碼的實現，運行在JVM 上。
    - 跟Python的套件一樣，導入並使用任何Java類。
- IronPython
    - IronPython是一個針對.NET框架的Python實現。
    - 它可以用Python和.NET framewor k的庫，也能將Python代碼暴露給.NET框架中的其他語言。

## 體驗

在python有一個很有趣的套件，你可以透程式來控制它移動，以下就來體驗吧～
```python=
import turtle

turtle.pensize(4)
turtle.pencolor('red')
turtle.forward(100)
turtle.right(90)
turtle.forward(100)
turtle.right(90)
turtle.forward(100)
turtle.right(90)
turtle.forward(100)
turtle.mainloop()
```
利用上面的程式一行一行的輸入到python自帶的編譯器裡頭，你會發現它會先畫出一條線然後右轉劃線在右轉劃線，直到畫出一個正方形，而這個套件是由```Logo```語言中的一部份而來。

![](https://i.imgur.com/3KmX31P.png)

>ps 學過ros的一定覺的跟小海龜很像