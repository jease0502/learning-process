---
tags: sublime
---
# c 和 c++ 編譯
---
## 簡介
通常打```C```大家都使用```DEC C++```，但是又有誰規定一定要用它呢~這次我們就用```SUBLIME```來編譯```C```與```C++```吧~

---
## 自動排版與美觀

如果你想要讓你的c語言有顏色，你就必須安裝```ctags```這個套件
>當然有可能他本來就會亮，不用裝也沒關西

接下來就是自動排版啦~
只要安裝``` AStyle Formatter Plugin```，然後要使用的話，滑鼠右鍵，然後按下```AStyle Formatter ```接下來選```format```這樣就會自動排版了

---
## 安裝 MinGW

如果你是windows的話，就一定需要這個來輔助她。
我在另外一篇文章中有詳細安裝過程，可以過去查看~
[windows gcc編譯](https://hackmd.io/c/SyTZRvvXV/https%3A%2F%2Fhackmd.io%2Fx-yUyZa0ScmQr-2zgQq3GQ)

---
## 設定sublime 編譯

打開你的 Sublime Text ，按 ```Ctrl + Shift + P``` 打 ```new build system```，把內容全部替換成以下文字，儲存位置不要修改。接下來去存他，檔名自己想一個喜歡的。


```
{
	"working_dir": "$file_path",
	"cmd": "gcc -Wall \"$file_name\" -o \"$file_base_name\"",
	"file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
	"selector": "source.c",
 
	"variants": 
	[
		{	
		"name": "Run",
        	"shell_cmd": "gcc -Wall \"$file\" -o \"$file_base_name\" && start cmd /c \"\"${file_path}/${file_base_name}\" & pause\""
		}
	]
}
```

---
## 設定工具

在sublime本來就有內建的編譯器，只是很弱通常用不到，所以需要另外去安裝一個編譯器，要改變編譯器設定需要去```工具```，然後選擇編譯系統，接下來選取你剛剛取名的名稱，這樣就可以了。

---
## 開始測試~

接下來在剛剛的設定後，你的編譯器以傳換過來了，直接按sublime的內建快速鍵吧~```shift+ctrl+b```，接下來選則有```run```的那個，然後他就會跳出cmd，這就表示你成功了~

---