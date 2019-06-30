---
tags: c
---
# Windows gcc編譯
---
## 安裝
1.首先安裝MinGW，點取[連結](https://sourceforge.net/projects/mingw/files/)到下載頁面，進行載
2.安裝完畢會跳出一個視窗讓你選擇要安裝的套件，在```mingw32-gcc-g++```上右鍵選擇 ```Mark for Installation```打勾，然候左上角 Installation 選擇 Apply Change 就會開始安裝 C/C++ 編譯器了,

---
## 設定環境變數

將```C:\MinGW\bin```加入到系統環境變數```path```中，才能使用
>在搜尋打環境變數，打開後按下環境變數進行新增或修改
>>如果你的變數裡面已經有path了，則在path上按兩下，直接將```C:\MinGW\bin```新增上去就好

---
## 測試是否安裝完成

在 cmd 輸入``` gcc -v```,如果出現gcc的版本訊息表示成功

---
## 編譯c檔案

1.找到你的c程式碼所在資料夾後，打開```powershell```，輸入```cmd```
2.進行編譯
```bash=
g++ 檔名.c -o 檔名.exe
```
3.執行程式時，直接在```cmd```輸入你的```檔名.exe```即會開始執行

---