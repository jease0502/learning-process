---
tags: 演算法
---
# 戴克斯特拉算法(Dijkstra)

## 簡介

在先前的廣度搜索法中我們可以去查找最少的路徑而無法知道最快的路徑，而在戴克斯特拉算法中你可以去找到最快的路徑

接下來分為幾點進行說明

1.權重
2.Dijkstra
3.想法&程式
4.運行時間

---
## 權重
Dijkstra算法用於每條邊都有關聯數字的圖，就像是每個節點到下個節點都會顯示距離多少。而權重的意義是某物的相對重要程度，所以她算是一個相對的概念，而不是絕對的。
舉個例子，當你在算成績時是依照這堂課在一周有幾堂來當作倍率乘以你的分數，以來算出學期成績的，而倍率大小就是你的權重大小。

而一個項目又可因他有沒有用到權重，而分別使用相應的算法
- 沒有用到權重：廣度優先搜索
- 有用到權重：戴克斯特拉算法、貝爾曼福德算法
而權重又可分正負
- 正權重：戴克斯特拉算法
- 負權重：貝爾曼福德算法

---
## Dijkstra

我們以找最快路徑為例，在前面講到的圖中的邊上增加使用該路徑所需時間，以下將寫出查找方法
1.找出最便宜的節點
2.計算該點前往鄰居所花費時間
3.重複此過程直到全部節點都判斷完
4.計算最終路徑

![](https://i.imgur.com/3DHCtbt.jpg)


第一步，我們要去找出到底要去A還是去B，並寫出它們所需時間。
NODE|耗時
|--|--|
|A|6
|B|2
|終點|∞

因為我們還不知道前往終點的時間，所以設為無限大，從圖中可得知B點最快

第二步，找出B點前往A點和終點的時間
NODE|耗時
|--|--|
|A|5
|B|2
|終點|7

我們在圖中找到了一條前往A點的更短路徑，所以我們要去更新表格

第三步，重複
重複第一步：找出最短時間內前往的節點，因為B已經找過了現在剩下A需要查找

NODE|耗時
|--|--|
|A|5
|B|2
|終點|7

重複第二步：查找A點到鄰居的時間，並去更新他
NODE|耗時
|--|--|
|A|5
|B|2
|終點|6

在這個過程中我們找到更快的路徑只需耗時6，所以我們要去更新表格

第四步，在上一步驟中我們已經確認將所有節點RUN過一次了，於是我們就可以確定最快路徑耗時為6，並且最快到終點的路徑也可以確定了。

P.S在廣度搜尋法中所找到的路徑並不會是這條，因為這條路徑抱括了3條路，而有一條前往終點的路只需要經過兩條路即可到達。

---
## 想法&程式

首先我們以剛剛的圖為例子。
![](https://i.imgur.com/3DHCtbt.jpg)
要想解決這個題目，我們需要三個散列表
1.graph圖
2.costs花費
3.parents父節點

![](https://i.imgur.com/avFxVwu.jpg)

![](https://i.imgur.com/aLpWHgP.jpg)

![](https://i.imgur.com/6TvAFEg.jpg)

隨著演算法的進行，我們將持續更新COSTS、PARENTS。首先我們需要實現圖，因此我們可以先寫一個散列表出來
```python=
graph={}
graph["start"]={}
graph["start"]["a"]=6
graph["start"]["b"]=2
```
這樣我們創建了一個散列表並將權重輸入進去了
接下來我們把其他節點跟鄰居添加近來
```python=
#a節點
graph["a"]={}
graph["a"]["fin"]=1
#b節點
graph["b"]={}
graph["b"]["a"]=3
graph["b"]["fin"]=5
#終點，他沒有鄰居
graph["fin"]={}
```
接下來我們要來儲存costs
>在python中如果要儲存無限大可以這樣做 infinity=float("inf")
```python=
infinity=float("inf")
costs={}
costs["a"]=6
costs["b"]=2
costs["fin"]=infinity
```
接下來輪到儲存parents
```python=
parents={}
parents["a"]="start"
parents["b"]="start"
parents["fin"]=None
```
當然也需要一個tmp來儲存資料
```python=
processed=[]
```
準備工作結束~
接下來正式進入演算法了~
在演算法中，我們先將到終點的花費設為無限大，然後再去執行迴圈將你所指定的那個點執行一次，例如(b點)就是只跑他到a、終點。
接下來持續進行判斷是否是最快路徑的遊戲
```python=
def find_lower_cost_node(costs):
    lowest_cost=float("inf")
    lowest_cost_node=None
    for node in costs:#跑過所有點
        cost=costs[node]
        if cost<lowest_cost and node not in processed:#如果找到更快的路徑，且那個節點定沒有用過
            lowest_cost=cost
            lowest_cost_node=node#就把它設為最低(更新資料)
    return lowest_cost_node
```
最後列出所有程式碼~
我們的流程是：持續這個流程直到所有節點都跑過
```flow
st=>start: 只要還有要處理的節點

op=>operation: 獲取離起點最近的節點
op2=>operation: 更新其鄰居耗時
cond=>operation: 如果有鄰居被更新同時更新父節點
e=>end: 將該節點標記成用過了

st->op->op2->cond
cond->e
```

```python=
#先定義會用到的資料
#起點
graph={}
graph["start"]={}
graph["start"]["a"]=6
graph["start"]["b"]=2
#a
graph["a"]={}
graph["a"]["fin"]=1
#b
graph["b"]={}
graph["b"]["a"]=3
graph["b"]["fin"]=5
#終點
graph["fin"]={}
#cost
infinity=float("inf")
costs={}
costs["a"]=6
costs["b"]=2
costs["fin"]=infinity
#parents
parents={}
parents["a"]="start"
parents["b"]="start"
parents["fin"]=None
#tmp
processed=[]

def find_lower_cost_node(costs):
    lowest_cost=float("inf")
    lowest_cost_node=None
    for node in costs:#跑過所有點
        cost=costs[node]
        if cost<lowest_cost and node not in processed:#如果找到更快的路徑，且那個節點定沒有用過
            lowest_cost=cost
            lowest_cost_node=node#就把它設為最低(更新資料)
    return lowest_cost_node

node=find_lower_cost_node(costs)#在還沒處理過的節點找出最快路徑
while node is not None:#這個迴圈將在所有節點都找過後才結束
    cost=costs[node]
    neighbors=graph[node]
    for n in neighbors.keys():#找遍該節點的鄰居
        new_cost=cost+neighbors[n]
        if costs[n]>new_cost:#如果這條路比較快
            costs[n]=new_cost#就更新表格
            parents[n]=node#同時將該鄰居的父節點設成當前節點
    processed.append(node)#將當前節點設定成已使用過
    node=find_lower_cost_node(costs)#找出接下來要跑的節點並循環
print(costs)
print(parents[parents["fin"]]+"-->"+parents["fin"]+"-->"+"fin")
```
最終結果~
```python=
{'a': 5, 'b': 2, 'fin': 6}
b-->a-->fin
```

---
## 運行時間
Dijkstra的大O時間是：O(mlogn)，這個速度其實並沒有很快
