---
tags: python
---
# python異常處理、錯誤

---
## 異常處理
```python=
try:
    <程式碼>
except: Exception as e:
    <程式碼>
```

---
## 錯誤整理

Error in sitecustomize; set PYTHONVERBOSE for traceback:
NameError: name 'reload' is not defined--可能是reload語法問題也可能是sitecustomize.py黨產生衝突(anaconda)

BaseException—— 所有異常的基類

SystemExit——解釋器請求退出

KeyboardInterrupt——用戶中斷執行

Exception ——常規錯誤的基類

StopIteration ——迭代器沒有更多的值

GeneratorExit ——生成器(generator)發生異常來通知退出

StandardError ——所有的內建標準異常的基類

ArithmeticError——所有數值計算錯誤的基類

FloatingPointError——浮點計算錯誤

OverflowError——數值運算超出最大限制

ZeroDivisi——除(或取模)零(所有數據類型)

Asserti——斷言語句失敗

AttributeError——對像沒有這個屬性

EOFError——沒有內建輸入,到達EOF 標記

EnvironmentError——操作系統錯誤的基類

IOError——輸入/輸出操作失敗

OSError——操作系統錯誤

WindowsError——系統調用失敗

ImportError——導入模塊/對象失敗

LookupError——無效數據查詢的基類

IndexError——序列中沒有此索引(index)

KeyError——映射中沒有這個鍵

MemoryError——內存溢出錯誤(對於Python 解釋器不是致命的)

NameError——未聲明/初始化對象(沒有屬性)

UnboundLocalError——訪問未初始化的本地變量

ReferenceError——弱引用(Weak reference)試圖訪問已經垃圾回收了的對象

RuntimeError——一般的運行時錯誤

NotImplementedError——尚未實現的方法

SyntaxErrorPython——語法錯誤

Indentati——縮進錯誤

TabErrorTab ——和空格混用

SystemError——一般的解釋器系統錯誤

TypeError——對類型無效的操作

ValueError——傳入無效的參數

UnicodeErrorUnicode ——相關的錯誤

UnicodeDecodeErrorUnicode——解碼時的錯誤

UnicodeEncodeErrorUnicode ——編碼時錯誤

UnicodeTranslateErrorUnicode ——轉換時錯誤

Warning——警告的基類

DeprecationWarning——關於被棄用的特徵的警告

FutureWarning——關於構造將來語義會有改變的警告

OverflowWarning——舊的關於自動提升為長整型(long)的警告

PendingDeprecationWarning——關於特性將會被廢棄的警告

RuntimeWarning——可疑的運行時行為(runtime behavior)的警告

SyntaxWarning——可疑的語法的警告

UserWarning——用戶代碼生成的警
