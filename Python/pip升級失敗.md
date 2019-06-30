---
tags: python
---
# pip升級失敗
---

解決方法：
1.到cmd輸入
```cmake=
pip -V
```
2.到/Lib/site-packages/，每個人的文件夾位置可能不同
```cmake=
C:\Users\jease\AppData\Roaming\Python\Python36\site-packages
```
3.刪除你目前pip版本的資料夾
4.新建一個sitecustomize.py文件(放在site-packages資料夾裡面)，裡面內容如下：
```python=
# encoding=utf8 
import sys
reload(sys)
sys.setdefaultencoding('gbk') 
```
5.在當前目錄打開powershell，並輸入
```cmake=
pip install --upgrade pip
```
6.電腦重開就可以了
7.進入剛剛的文件夾
```cmake=
C:\Users\jease\AppData\Roaming\Python\Python36\site-packages
```
8.把剛才創建的sitecustomize.py檔案刪除，不然會出現這樣子的錯誤
```cmake=
Error in sitecustomize; set PYTHONVERBOSE for traceback:
NameError: name 'reload' is not defined
```


