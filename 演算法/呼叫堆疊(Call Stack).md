---
tags: 演算法
---
# 呼叫堆疊(Call Stack)

簡單來說呼叫堆疊就是指當我們在處理一個程式時，裡面有著其他程式，我們就需要先暫停這個程式，然後去執行這個突然出現的程式，執行完後才能繼續執行原本暫停的程式

---
例子：
```python=
def great(name):
    print("hello"+name+"?")
    great2(name)
    print("getting ready to say bye")
    bye()
def great2(name):
    print("how are you"+name+"?")
def bye():
    print("ok bye")
name=input("input")
great(name)
```
在上面的例子中，我們在執行great()時，會遇到great2()和bye()兩個function，我們便需要去暫停great()，去執行great2(0)然後繼續執行great()的print指令，再去執行bye()，然後才是程式結束，這樣的動作便是呼叫堆疊