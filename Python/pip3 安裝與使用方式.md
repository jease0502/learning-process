---
tags: python
---
# pip3 安裝與使用方式 
---
## 說明
當你在使用ubuntu時,可能會遇到需要切換python版本進行安裝套件時,無法切換版本,這時候就會需要用到這個功能了～

---
## 方法
今天以python3.5來做示範
首先輸入這兩行進行安裝
```cmake=
wget https://bootstrap.pypa.io/get-pip.py
sudo python3.5 get-pip.py
```
當安裝完成後,使用以下指令即可指定安裝到python3.5
```cmake=
pip3 install 套件
```
