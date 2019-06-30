---
tags: c
---
# Windows: 如何將C語言源代碼編譯成dll動態鏈接庫
---
## 流程

- 1.撰寫c的code
- 2.進行編譯

## 編譯

### Visual Studio

(1). 選擇"檔案" > "新增" > "專案"。
(2). 選擇"Visual C++" > "Win32" > "Win32主控台應用程式"，並且修改專案的"名稱"後按"確定"。
(3). 直接按"下一步>"。
(4). 選擇"DLL"後按"完成"。

### MinGW（gcc）
[下載連結](https://sourceforge.net/projects/mingw/files/latest/download)

安裝MinGW之後，就可以在Windows平台上使用gcc了。用gcc將上述Test.c編譯成Test.dll的命令是：
```cmake=
gcc -shared -o Test.dll Test.c  
```