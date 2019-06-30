---
tags: git
---
# Git
---
## 第一次上傳
step1.前往你的github創建新的專案
step2.clone下來你的資料夾
```cmake=
git clone 你的網頁
```
step3.cd 到你clone下來的資料夾
```cmake=
cd file
```
step4.把你要上傳的資料丟到這個資料夾裡面
step5.輸入```git add -A``` 把所有資料進行預備上傳的動作
step6.輸入```git commit -a -m “add test”```備註一下這次上傳的資料
step7.輸入```git push```把檔案上傳上去

---
## 第二次上傳
step1.連線到你的github
```cmake=
git remote add 使用分支 網址
```
使用分支的地方如果你沒有設定分支的話那就填```origin```就可以了

step2.確認是否連線成功與名稱是否相同
```cmake=
git remote -V
```
step3.上傳
```cmake=
git push
```
---