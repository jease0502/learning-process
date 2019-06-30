---
tags: python
---
# PANDAS
---
## PANDAS簡介
Pandas 提供兩種主要的資料結構，Series 與 DataFrame。透過載入至 Pandas 的資料結構物件後，可以透過結構化物件所提供的方法，來快速地進行資料的前處理，如資料補值，空值去除或取代等更多的輸入來源及輸出整合性，例如：可以從資料庫讀取資料進入 Dataframe，也可將處理完的資料存回資料庫。

---
### Pandas 讀取資料
可以從異質資料來源讀取檔案內容，並將資料放入 DataFrame 中，進行資料查看、資料篩選、資料切片等運算

讀取 CSV 檔案:
```python
import pandas as pd 
df = pd.read_csv('shop_list.csv')  
print(df)  
```
讀取 HTML
```python
import pandas as pd 
dfs = pd.read_html('http://rate.bot.com.tw/xrt?Lang=zh-TW')  
dfs[0]  
```
---

### Pandas 提供的資料結構
1.Series：用來處理時間序列相關的資料(如感測器資料等)，主要為建立索引的一維陣列。
2.DataFrame：用來處理結構化(Table like)的資料，有列索引與欄標籤的二維資料集，例如關聯式資料庫、CSV 等等。
3.Panel：用來處理有資料及索引、列索引與欄標籤的三維資料集。

---
#### Series
##### 建立 Series
資料可以的類型如下：array、dictionary、單一資料
```python
import pandas as pd 
select = pd.Series(data, index = idx)將資料讀入 series 中
```

##### 資料為 Array
```python
import pandas as pd  
cars = ["BMW", "BENZ", "Toyota", "Nissan", "Lexus"]
select = pd.Series(cars)  
print(select) 
```
Output 為： 
>0 BMW 
1 BENZ 
2 Toyota 
3 Nissan 
4 Lexus 
dtype: object

##### 資料為 Dictionary
```python
Import pandas as pd
dict = {  
    "factory": "Taipei",
    "sensor1": "1",
    "sensor2": "2",
    "sensor3": "3",
    "sensor4": "4",
    "sensor5": "5"
}
select = pd.Series(dict, index = dict.keys())#排序與原 dict 相同   
print(select[0])  
print("=====")  
print(select['sensor1'])  
print("=====")  
print(select[[0, 2, 4]])  
print("=====")  
print(select[['factory', 'sensor1', 'sensor3']])  
```
Output 的資料在下面圖片
![](https://i.imgur.com/zei8Lvy.png)


##### 資料為單一資料:
```python
import pandas as pd
cars = "BENZ"  
select = pd.Series(cars, index = range(3))  
print(select)  
```
Output 為： 
>0 BENZ 
1 BENZ 
2 BENZ 
dtype: object

---
#### Series 的操作 
##### 資料選擇與篩選 
可以針對 dict 或是 array 資料透過透過索引值或標籤，挑選出你所要的值。
```python
import pandas as pd
dict = {  
    "factory": "Taipei",
    "sensor1": "1",
    "sensor2": "2",
    "sensor3": "3",
    "sensor4": "4",
    "sensor5": "5"
}
select = pd.Series(dict, index = dict.keys()) # 排序與原 dict 相同  
print(select[0])  
print("=====")  
print(select['sensor1'])  
print("=====")  
print(select[[0, 2, 4]])  
print("=====")  
print(select[['factory', 'sensor1', 'sensor3']])  
```

##### 資料切片 
透過索引值或標籤，切割需要的值。
```python
import pandas as pd
dict = {  
    "factory": "Taipei",
    "sensor1": "1",
    "sensor2": "2",
    "sensor3": "3",
    "sensor4": "4",
    "sensor5": "5"
}
select = pd.Series(dict, index = dict.keys())     排序與原 dict 相同  
print(select[:2])  
print("=====")  
print(select['sensor2':]) 
```
Output 
![](https://trello-attachments.s3.amazonaws.com/5c1717265e6a400bc9cbd228/5c17cd77524d2171c1bccbd8/ab3e0b7155741c4b9ef4248dedb2bd0f/image.png)

#### 建立 DataFrame 

DataFrame 用來處理結構化(Table like)的資料，有列索引與欄標籤的二維資料集，可以透過 Dictionary 或是 Array 來建立，但也可以利用外部的資料來讀取後來建立，例如：CSV 檔案、資料庫等等。

下列範例會介紹利用 Dictionary 或是 Array 來建立，並使用 DataFrame 的方法來操作資料查看、資料篩選、資料切片、資料排序等運算。

##### 資料為 Dictionary
```python
import pandas as pd
groups = ["Movies", "Sports", "Coding", "Fishing", "Dancing", "cooking"]  
num = [46, 8, 12, 12, 6, 58]
dict = {"groups": groups,  
        "num": num
       }
select_df = pd.DataFrame(dict)
print(select_df)       看看資料框的外觀  
```
Output
![](https://trello-attachments.s3.amazonaws.com/5c1717265e6a400bc9cbd228/5c17cd77524d2171c1bccbd8/9b3af22f26e6352e82ace4f25193c97d/image.png)

##### 資料為 Array
```python
import pandas as pd
arr = groups = [["Movies", 46],["Sports", 8], ["Coding", 12], ["Fishing",12], ["Dancing",6], ["cooking",8]]
df = pd.DataFrame(arr, columns = ["name", "num"])     指定欄標籤名稱  
print(df)  
```
Output 
![](https://trello-attachments.s3.amazonaws.com/5c1717265e6a400bc9cbd228/5c17cd77524d2171c1bccbd8/7f7ac3f21f1238867ec9ac27d83d758a/image.png)
---

#### DataFrame 的操作 
##### 資料描述查看 
可以透過下列方法查看目前資料的資訊
- .shape
- .describe()
- .head()
- .tail()
- .columns
- .index
- .info()
Pandas 的 data frame 資料結構有一些方法或屬性
```python
import pandas as pd
groups = ["Movies", "Sports", "Coding", "Fishing", "Dancing", "cooking"]  
num = [46, 8, 12, 12, 6, 58]
dict = {"groups": groups,"num": num}
select_df = pd.DataFrame(dict)
print(select_df.shape)     回傳列數與欄數  
print("---")  
print(select_df.describe())      回傳描述性統計  
print("---")  
print(select_df.head(3))     回傳前三筆觀測值  
print("---")  
print(select_df.tail(3))      回傳後三筆觀測值  
print("---")  
print(select_df.columns)      回傳欄位名稱  
print("---")  
print(select_df.index)       回傳 index  
print("---")  
print(select_df.info)      回傳資料內容  
```
Output 
![](https://trello-attachments.s3.amazonaws.com/5c1717265e6a400bc9cbd228/5c17cd77524d2171c1bccbd8/9ac2946b1ca6ff1d960ee018fb1ed4fb/image.png =400x400)

##### 資料選擇與篩選 
可以透過下列方法選擇元素中括號 [] 選擇元素，將變數當作屬性選擇loc .iloc 方法選擇使用布林值篩選，Pandas透過使用中括號[]與 .iloc 可以很靈活地從 data frame 中選擇想要的元素，Python 在指定 0:1 時不包含 1，在指定 0:2 時不包含 2
```python
import pandas as pd
groups = ["Movies", "Sports", "Coding", "Fishing", "Dancing", "cooking"]  
num = [46, 8, 12, 12, 6, 58]
dict = {"groups": groups,"num": num}
select_df = pd.DataFrame(dict)
print(select_df.iloc[0, 1]) # 第一列第二欄：組的人數  
print("---")  
print(select_df.iloc[0:1,:]) # 第一列：組的組名與人數  
print("---")  
print(select_df.iloc[:,1]) # 第二欄：各組的人數  
print("---")  
print(select_df["num"]) # 各組的人數  
print("---")  
print(select_df.num) # 各組的人數  
```
Output
![](https://trello-attachments.s3.amazonaws.com/5c1717265e6a400bc9cbd228/5c17cd77524d2171c1bccbd8/cbbcf73090117a026da0084356ad350d/image.png =200x400)

##### 使用布林值來做篩選
```python
import pandas as pd
groups = ["Movies", "Sports", "Coding", "Fishing", "Dancing", "cooking"]  
num = [46, 8, 12, 12, 6, 58]
dict = {"groups": groups,"num": num}
select_df = pd.DataFrame(dict)
out_df = select_df[select_df.loc[:,"num"] > 10] # 選出人數超過 10 的群組  
print(out_df) 
```
Output
![](https://trello-attachments.s3.amazonaws.com/5c1717265e6a400bc9cbd228/5c17cd77524d2171c1bccbd8/f224742701b9f02fd451b35e49ed4983/image.png)

##### 資料排序 
可以使用的方法如下：
1 .sort_index()
2 .sort_values()

---
1 .sort_index()
```python
import pandas as pd # 引用套件並縮寫為 pd
groups = ["Movies", "Sports", "Coding", "Fishing", "Dancing", "cooking"]  
num = [46, 8, 12, 12, 6, 58]
dict = {"groups": groups,"num": num}
select_df = pd.DataFrame(dict)
select_df.sort_index(axis = 0, ascending = True) 
```
透過索引值做排序，axis 可以指定第幾欄，ascending 用於設定升冪或降密
Output
![](https://trello-attachments.s3.amazonaws.com/5c1717265e6a400bc9cbd228/5c17cd77524d2171c1bccbd8/3f82c5766933df0882951488b8f08cbc/image.png =300x300)

---
2 .sort_values()
```python
import pandas as pd 
groups = ["Movies", "Sports", "Coding", "Fishing", "Dancing", "cooking"]  
num = [46, 8, 12, 12, 6, 58]
dict = {"groups": groups,"num": num}
select_df = pd.DataFrame(dict)
select_df.sort_values(by = 'num') #透過指定欄位的數值排序 
```
Output
![](https://trello-attachments.s3.amazonaws.com/5c1717265e6a400bc9cbd228/5c17cd77524d2171c1bccbd8/ef73aebc1f9404330fbc97f68fb19f6a/image.png =300x300)

---

##### DataFrame 處理遺漏值 
###### 判斷是否為空值 
可以使用下列兩種方法來判斷：
1. isnull()
2. notnull()
下列程式我們先讀取一個 CSV 檔案，檔案內的欄位部分會有空值，檔案連結 大家可以自行下載

---
讀取 CSV File
```python
import pandas as pd # 引用套件並縮寫為 pd  
df = pd.read_csv('shop_list2.csv')  
print(df)
讀取後放入 DataFrame
select_df = pd.DataFrame(df)
print(select_df.ix[:, "shop name"].isnull()) 判斷哪些店名是遺失值  
print("---")  
print(select_df.ix[:, "maket size"].notnull()) 判斷哪些市場規模不是遺失值
```
可以透過 ix 方法（利用索引值或欄位）選擇 data frame 區段
Output
![](https://trello-attachments.s3.amazonaws.com/5c1717265e6a400bc9cbd228/5c17cd77524d2171c1bccbd8/bf36c5ab5283f69f5ee6197453bcab2a/image.png =300x300)

##### 處理空值 
可以使用下列兩種方法來填補空值：
1. dropna()
2. fillna()

讀取 CSV File
```python
import pandas as pd
df = pd.read_csv('shop_list2.csv')  
print(df)
讀取後放入 DataFrame
select_df = pd.DataFrame(df)
drop_value = select_df.dropna() # 有遺失值的觀測值都刪除
print(drop_value)  
print("---")  
filled_value = select_df.fillna(0) # 有遺失值的觀測值填補 0
print(filled_value)  
print("---")  
filled_value_column = select_df.fillna({"shop name": "NULL", "maket size": 0}) 依欄位填補遺失值  
print(filled_value_column) 
```
Output
![](https://trello-attachments.s3.amazonaws.com/5c1717265e6a400bc9cbd228/5c17cd77524d2171c1bccbd8/b0c1fbd9694c4d64987271e19c693faf/image.png =300x400)