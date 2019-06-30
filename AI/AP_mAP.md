---
tags: AI
---
# AP/mAP



|          | 真實情況 有| 真實情況 沒有| 
| -------- | -------- | -------- |--
| 偵測情況 有  | 是A且被模型判斷為A(TP)  | 不是A且被模型判斷為A(FP)    |
|偵測情況 沒有| 是A且被模型判斷為A(TP)  |  是A但被模型判斷為不是A(FN)|


Precision: 
 所有被檢測為目標=所有被模型判斷為A
 =是A且被模型判斷為A(TP) + 不是A且被模型判斷為A(FP)
 
 Recall:
 資料中的所有目標=資料中為A
 =是A且被模型判斷為A(TP) + 是狗A被模型判斷為不是A(FN)
 
**AP**[average precision]

根據不同rank下去計算precision和recall得到下表。

![](https://i.imgur.com/Be9504R.png)

將表畫成以下圖形

![](https://i.imgur.com/oA7kzci.png)

AP就是計算這條precision-recall curve下的面積(area under curve, AUC)。

VOC 2010之前的方法在算AP部分時會做一個小轉換。
就是選取Recall>=0, 0.1, 0.2,…, 1，這11的地方的Precision的最大值。
這邊的p等於precision，r={0, 0.1,…, 1}


VOC 2010之後的方法在recall的決斷值又做了修正，就是選取Recall>=0, 0.14, 0.29, 0.43, 0.57, 0.71, 1，這7的地方的Precision的最大值。


下圖表為轉兩個方法換後的結果。

此例子VOC 2010之前的AP=(1+1+1+1+0.833+0.833+0.833+0+0+0+0)/11=6.433/11= 0.591

此例子VOC 2010之後的AP=(1+1+1+0.833+0.833+0+0)/7=4.666/7= 0.667

**mAP**
物體偵測不可能只偵測一種東西，假設在資料庫有80種東西。mAP就是每一種物體的AP算完後的平均值。


**IOU (intersection over union)**
IOU計算方式就是兩個物件的重疊(overlap)/交集比例。
IOU就是「兩個物件的交集」除上「兩個物件的聯集」