---
tags: python
---
# GUI介面 thinker

---

當PYTHON程式需要用到GUI介面時，thinker是最簡單學習的一種介面

---

安裝方式：
```
pip install thinker
```
---

會用到的函數介紹

- button	按鈕。
- Canvas	長方形區域。
- Checkbutton	核取按鈕。
- Entry	文字輸入欄。
- Frame	視窗。
- Label	文字標籤。
- LabelFrame	文字標籤視窗。
- Listbox	列表選單。
- Menu	選單列的下拉式選單。
- MenuButton	選單的選項。
- Message	類似 Label ，可多行。
- OptionMenu	下拉式的選項選單。
- PaneWindow	類似 Frame ，可包含其他視窗元件。
- Radiobutton	單選按鈕。
- Scale	拉桿。
- Scrollbar	捲軸。
- Spinbox	微調器
- Text	 文字方塊。
- Toplevel	新增視窗。

示範程式

```python=
import tkinter as tk
from tkinter import ttk
from tkinter.messagebox import showinfo

class Application(ttk.Frame):
    def __init__(self, master):
        ttk.Frame.__init__(self, master)
        self.pack()

        self.button = ttk.Button(self)
        self.button["text"] = "Click Me!"
        self.button["command"] = self.popup_hello
        self.button.pack()
    
    def popup_hello(self):
        showinfo("Hello", "Hello Tk!")

root = tk.Tk()
app = Application(root)
root.mainloop()
```

---
示範圖片：

![](https://i.imgur.com/25RWLyP.png)


