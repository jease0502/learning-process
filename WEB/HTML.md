---
tags: web
---
# HTML

---
## HTML5基本語法
```htmlmixed=
<!DOCTYPE html>
<html>
<meta charset="utf-8">
<head>
	<title></title>
</head>
<body>

</body>
</html>
```
---
## HTML4與HTML5差別：
HTML5的目的是為了能夠使程式更加簡略，例如為了不一定要將head、body等等打出來直接輸入你所要撰寫的內容即可，部分指令甚至不需要打出封閉符號<\>。
>下面這幾個是不需要再次輸入封閉<\>的
>li、dt、dd、p、rt、rp、optgroup、colgroup、thead、tbody、tfoot、tr、td、th

>下面是不能省略的元素
>area、base、br、col、command、embed、hr、img、input、keygen、link、meta、param、source、track、wbr

>可以省略全部標記的元素
>html、body、head、cplgroup、tbody

>只允許寫結束的元素
>br

以下做個示範
```htmlmixed=
<!DOCTYPE html>
<meta charset="utf-8">
<h1> 內容標題 </h1>
<p> 123456
<br/>145415
```
---
## boolean值
當只寫屬性不寫屬性值時，表示屬性值為true，如果想要該屬性為flase，則可以不寫屬性。另外將屬性名設置為屬性值，或設置成空，屬性值也是true

```htmlembedded=
<!--只寫屬性，不寫屬性值，代表屬性為true-->
<inpute type="checkbox" checked>
<!--不寫屬性，代表為flase-->
<inpute type="checkbox">
<!--寫屬性值=屬姓名，代表屬性為true-->
<inpute type="checkbox" checked="checked">
<!--寫屬性值=空字符串，代表屬性為true-->
<inpute type="checkbox" checked=" ">
```
---
## 屬性值
屬性兩邊可以用雙引號、單引號。在html5中可以在不包括空字符串、<、>、""、''等字符時，屬性值兩邊的引號可以省略，以下用法都是正確的
```htmlmixed=
<input type="text">
<input type='text'>
<input type=text>
```

## HTML4 元素

### 結構元素
用於建構網頁的文檔結構：
- div ：在檔案中定義一段區域  ex.包含框、容器
- span ：在檔案中定義一個區域  ex.行內包含框
- ol ：根據一定排序進行列表
- ul ：沒有排序的列表
- li ：每條列表項
- dl ：以定義的方式進行列表
- dt ：定義列表中的詞條
- dd ：對定義的持條進行解釋
- del ：定義刪除的文本
- ins ：定義插入的文本
- h1~h6 ：標題1到標題6，每個標題字型大小不同，1最大6最小
- p ：定義段落結構
- hr ：定義水平線
---
### 內容元素
內容元素定義元素在文檔中表示內容的語意，一般指文本格式化元素，他們多是行內元素:
- a ：定義超連接
- abbr ：定義縮寫詞
- acronym ：定義取首字母的縮寫詞
- address ：定義地址
- dfn ：定義條目
- kbd ：定義鍵盤鍵
- samp ：定義樣本
- var ：定義變數
- tt ：定義打字機字體
- code ：定義程式代碼
- pre ：定義預定義格式文本，保留原代碼格式
- blockquote ：定義大區域內容引用
- cite ：定義文本
- q ：定義引用短句
- strong ：定義重要文本
- em ：定義文本重要點

---
### 修飾元素
修飾文本顯示效果：
- b ：定義粗體
- i ：定義斜體
- big ：定義文本增大
- small ：定義文本縮小
- sup ：定義文本上標
- sub ：定義文本下標
- bdo ：定義文本顯示方向
- br : 定義換行

以下被廢除的修飾元素：
- center ：定義文本居中
- font ：定義文字的樣式、大小、顏色
- u ：定義文本下划線
- s ：定義刪除線、strike的縮寫
- strile ：定義刪除線

---
## HTML4 屬性

### 核心屬性
- class ：定義類規則或樣式規則
- id ：定義元素的唯一所性
- style ：定義元素的樣式聲明
以下這些元素不擁有核心屬性，一般位於檔案頭部區域，用來定義網頁元信息：html、head、title、base、meta、param、script、style。

---
### 語言屬性
語言屬性主要用來定義元素的語言類型，包括兩個屬性：
- lang ：定義元素的語言代碼或編碼
- dir ：定義文本方向，包括ltr、rtl取值，分別表示從左向右，和右向左
以下這些元素不擁有語言屬性：frameset、frame、iframe、br、hr、base、param、script
```htmlmixed=
<html xmlns="" dir="ltr" xml:lang="zh-tw">
<body id="myid" lang='en-us'
```

---
### 鍵盤屬性
鍵盤屬性定義元素的訪問的方法，包括兩個屬性：
- accesskey ：定義訪問某元素的鍵盤快捷鍵
- tabindex ：定義元素tab鍵索引編號
使用accesskey屬性可以使用快捷鍵(Alt+字母)訪問特定URL，但是目前瀏覽器不能完全支持
```htmlmixed=
<a href="1.html" accesskey="a">按住ALT+A可以回到該頁面 </a>

```
tabindex屬性用來定義元素的tab鍵訪問順序，可以使用tab鍵來進行訪問所有連結和表單元素，訪問時會按照tabindex的大小來決定順序，當訪問到某個連結時，按下enter即可打開連結頁面。
```htmlmixed=
<a href="#" tabindex="1">tab 1 </a>
<a href="#" tabindex="2">tab 2 </a>
<a href="#" tabindex="3">tab 3 </a>
```

---
### 內容屬性
內容屬性定義元素包含內容的附加信息，這些信息對於元素有補充意義，避免因資訊不全被誤解
- alt ：定義元素的替換文本
- title ：定義元素的提示文本
- longdesc ：定義元素包含內容的大段描述信息
- cite ：定義元素包含內容的引用信息
- datetime ：定義元素所包含的時間與日期
alt、title是兩個常用的屬性，分別定義元素替換和題是文本
```htmlmixed=
<a href="URL" title="提示文本">超連結</a>
<img src="URL" alt="替換文本" title="提示文本"/>
```
替換文本並不是用來製作提示的，相反title才是拿來製作額外說明信息的。
當圖像文法顯示時，需要準備替代文字來替換無法顯示的圖片，因此alt屬性只能用在img、area和input元素。對於input元素，alt屬性用來替換，提交按鈕的圖片
```htmlmixed=
<input type="image" src="URL" alt="替換文本" />
```
當瀏覽器被禁止顯示，不支持或無法下載這張圖片時，替換文本給那些看不到圖片的用戶看到說明，是一個很重要的補救說明。
從語意上來說，替換文本應該提供圖片的簡易說明，並保證他在上下文中是有意義的，如果是修飾類的文章，可以使用空值```alt=" " ```

---
### 其他屬性
- rel ：定義當前頁面與其他頁面的關係
- rev ：定義當前頁面與其他頁面之間的連接關係
rel、rev屬性之比對如下
- rel表示從原本的檔案到目標檔案的關係 (index to target)
- rev表示從目標檔案到原本的檔案 (target to index)

以下示範連結到同一個資料夾中的的前一個檔案，
```htmlmixed=
<a href="1.html" rel="prev">連接到資料夾中的前一個檔案</a>
```
---
