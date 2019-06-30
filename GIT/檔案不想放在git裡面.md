---
tags: git
---
# 檔案不想放在git裡面
---
## 開始~
- 如果你的檔案裡沒有```.gitignore```檔案的話，就自己創一個吧~
```cmake=
touch .gitignore
```
- 接下來編輯檔案
```cmake=
nano .gitignore
```
- 內容：
```cmake=
#當你不要123.py這個檔時直耶打
123.py

#如果你不要config資料夾下的abc.py的話打
config/abc.py

#如果你不要data資料夾下副檔名為py的文件
/data/*.py

#忽略所有附檔名是.txt的文件
*.txt
```

---
## 介紹~
先說明一個重點，當你已完成第一次push時，你在下次訂定規則後，原本的檔案還是會在github上，所以你如果要把原本已經push上去的檔案忽略掉，需要先將他移出去，這樣才會正常移除
```cmake=
git rm --cached
```
只要有```.gitignore```這個檔案在，即使他沒有commit或是push上去，他就會發揮它的效用，但是建議還是把她push上去比較好。
在新增加檔案時，依但符合```.gitignore```的規定，檔案就會自動忽略。

當你不需要這個規則的時候當然也可以直接忽略它~
```cmake=
git add -f 檔案名稱
```

