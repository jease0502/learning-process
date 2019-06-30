---
tags: web
---
# IBM CLOUD架站
---

## 簡介
目前提供免費雲端的廠商有很多，像是GOOGLE、騰訊、百度、AWS、IBM等，我這次使用IBM來架站原因在於不須使用信用卡即可使用，並且擁有許多額外功能可以使用，不管是資料運算、資料庫、物聯網、AI等等都可以使用。

而我這次是使用IBM Cloud中的web功能，他提供了php、python、ruby、java、go、asp等應用程式可以供你自己選擇，我這次將使用php進行示範。

---
## 創建方式

- 首先你要先去申請IBM Cloud的帳號，然後進去之後在選單選擇```Cloud Foundry```
![](https://i.imgur.com/nfseLia.jpg)
![](https://i.imgur.com/BBmWeIs.jpg)
- 接下來開始建立程式，在```公用應用程式```這邊按下建立
![](https://i.imgur.com/l8f0v5d.jpg)

- 在頁面中選擇你所要用到的程式，本次示範使用PHP
![](https://i.imgur.com/krn85SV.jpg)

- 進入建立頁面後，開始輸入你要得網頁名稱和選擇伺服器所在地，以及去選擇網域
![](https://i.imgur.com/G3wzgaK.jpg)

>目前所提供選擇地點有：
>達拉斯、雪梨、法蘭克福、倫敦、華盛頓
- 接下來選擇方案，在IBM Cloud 中每個人擁有128mb的使用大小。
![](https://i.imgur.com/Fk31AHD.jpg)
- 這樣就創建結束了~下面將開始介紹如何連接主機與上傳資料

## 連線


### 簡介
在連線前我們需要安裝 ```IBM® Cloud Developer Tools```這套程式，在安裝後也會自東安裝一些工具：

- Homebrew（僅限 Mac）
- Git
- Docker
- Helm
- kubectl
- curl
- IBM Cloud Developer Tools 外掛程式
- IBM Cloud Functions 外掛程式
- IBM Cloud Container Registry 外掛程式
- IBM Cloud Kubernetes Service 外掛程式
- sdk-gen 外掛程式

---
### 開始安裝
- 如果你使用的是windows的話如果不是專業版，請改成使用bash的方式進行連接

步驟一、執行安裝指令

- Mac、Linux
```bash=
curl -sL https://ibm.biz/idt-installer | bash
```
-  Windows 10 Pro
```bash=
Set-ExecutionPolicy Unrestricted; iex(New-Object Net.WebClient).DownloadString('http://ibm.biz/idt-win-installer')
```

步驟二、 驗證安裝
```bash=
ibmcloud dev help
```
步驟三、配置環境

連接至 IBM Cloud 位置中的 API 端點。例如，輸入下列指令以連接至 IBM Cloud 達拉斯的位置：
```bash=
 ibmcloud api https://api.ng.bluemix.net
```
使用 IBM ID 登入 IBM Cloud。
```bash=
 ibmcloud login
```
設定處存空間
```bash=
 ibmcloud target --cf
```
這樣簡單安裝便完成了~

---

### 開始上傳檔案

步驟一、切換到存放檔案夾中
```bash=
cd your_new_directory
```

步驟二、連接並登入 IBM Cloud
```bash=
ibmcloud api https://api.ng.bluemix.net
ibmcloud login -u 信箱 -o 信箱 -s dev
```
步驟三、確認一下你的文檔是否為index.php或是index.html
步驟四、上傳上去
```bash=
bluemix app push 你的網頁專題名稱
```
步驟五、到你的網頁去看看吧~

---