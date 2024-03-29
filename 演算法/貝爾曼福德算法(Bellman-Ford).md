---
tags: 演算法
---
# 貝爾曼福德算法(Bellman-Ford)

## 簡介
Dijkstra一樣可以處理最短路徑的問題，但無法處理邊的權重是負的情況，求出的最短路徑就可能是錯的。這時候，就需要使用其他的演算法來求解最短路徑，Bellman-Ford算法就是其中最常用的一個。

我將以5點來進行說明
1.負權重
2.鬆弛計算
3.想法
4.程式碼
5.運行時間

---
## 負權重
權重有正當然也有負值，負權重在圖上代表著方向相反，以下圖來示範
![](https://i.imgur.com/Ls1UMDM.jpg)
1.正權重
![](https://i.imgur.com/8g2Qdln.jpg)
2.負權重

---
## 鬆弛計算
先介紹一下鬆弛算法：
鬆弛算法的功用在於找到最短路徑，鬆弛兩個字代表著通過改進近似解來不斷的逼近直到產生最佳解，下面將對他的用法進行說明
在鬆弛計算前如圖(A)，A值是3，B值是8，且權重為2。但在A值加上邊的權重值2時，會得到5，比B的值還小，所以點B的值應改成5。這個過程的意義便是，找到一條通往B點更快的道路，且該路線必須通過A，然後通過權重為2的邊，到達B點。但是你無法保證你一定會找到更快的路徑，在圖B便是說明了這種情況，在圖B中權重為6，所以3+6=9大於B點的8，這表示這條路並沒有比前一條路更快，所以我們不去改變他的值。
![](https://i.imgur.com/i9jySK7.jpg)
![](https://i.imgur.com/S22htdH.jpg)

---
## 想法

### 想法步驟
1.將所有點初始化，也就是每個點保存一個值，表示原點到這個點的距離，將原點的值設為0，其他點設為無限大。
2.接下來開始進行循環處理，將所有邊進行鬆弛算法
3.判斷是否出現負權重，如果出現則返回false，之所以需要考慮是否為負權重是因為這將導致他無法收斂，值無限變小也就無法算出最小值。

### 想法示範
如果我們對下面的圖都進行一次鬆弛計算，他無法預知得到最優的路徑是如何。我們假設他的順序是(s, a)、(s, b)、(s, c)、(a, b)、(b, c)，這樣一輪結束，確實a點、b點、c點都可以得到正確答案，但是順序換成(b, c)、(a, b)、(s, a)、(s, b)、(s, c)，這樣b點就錯了，然而這題是一個迴路，他是沒有終點的。

但在這個例子中會發現a、c的答案無論順序如何都是對的，完成第1次鬆弛計算後，如果起點(s)到任一節點(u)存在一條邊權重為1的最短路徑，那麼從s到u點的（某條）邊權重為1的最短路徑的就一定能解出來。以此類推，如果連續做k次鬆弛計算，如果從s到u存在權重為k的、且沒有比他距離更短的路徑，那是不是也能把其中一條給解出來呢？是的。我們可以用數學歸納法進行證明。假設k-1次後的情況已經知道，再假設s到某點u存在權重為k的最短路徑，且其中一條為[s, m<sub>1</sub>, m<sub> 2</sub>, ..., m<sub>k-2</sub>, u]，那麼，[s, m<sub>1</sub>, m<sub>2</sub>, ..., m<sub>k-2</sub>]肯定是從s到m<sub>k-2</sub>的一條最短路徑（可用反證法證明），進而在第k次處理(m <sub>k-2</sub>, u)的時候，一定會對D[u]和P[u]的值有所改進，兩者的值都會是最終正確的解答而且不會再發生改變了。
![](https://i.imgur.com/TZWDwnK.png)

### 想法總結
對於一個包含n個節點，m條邊的圖, 計算原點到任意點的最短距離，並且最短路徑是不包含迴路的(無論正負權重)，如果有出現迴路則會分別產生兩種情況
1.如果包含正權重迴路：去掉這段迴路便可以得到最短路徑
2.如果包含負權重迴路：每多走一次迴路路徑都會更短，因此不存在最短路徑
因此最短路徑一定不包含迴路，也就是最多包涵n-1條邊，所以進行n-1次鬆弛計算即可。

---
## 程式碼
下面程式裡面的圖是用下面這張圖去寫的喔~
![](https://i.imgur.com/TZWDwnK.png)
```python=
def bellman_ford(G, source):
    dist = {}
    p = {} #path
    max = infinity
    for v in G:
        dist[v] = max  #將點設為無限大完成初始化
        p[v] = None
    dist[source] = 0

    for i in range(len( G ) - 1):
        for u in G:
            for v in G[u]:
                if dist[v] > G[u][v] + dist[u]:
                    dist[v] = G[u][v] + dist[u]
                    p[v] = u    #完成鬆弛計算，p是前一個節點

    for u in G:
        for v in G[u]:
            if dist[v] > dist[u] + G[u][v]:
                return None, None  #判斷是否有迴路

    return dist, p

def test():
    G = {
        's': {'a':  2, 'b':  9, 'c':  1},
        'a': {'b':  3},
        'b': {'c': -1},
        'c': {},
    }
    dist, p = bellman_ford(G, 'a')
    print(dist)
    print(p)

infinity=float("inf")
test()
```
結果~
```python=
{'s': inf, 'a': 0, 'b': 3, 'c': 2}
{'s': None, 'a': None, 'b': 'a', 'c': 'b'}
```
---
## 運行時間
Bellman-Ford的大O時間是：O(nm)，這個速度其實是比DijkstraO(mlogn)還要慢的，但他的優勢在於它能處理負權值的情況。

