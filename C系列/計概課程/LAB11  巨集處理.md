---
tags: 計概
---

# LAB11  巨集處理

## 甲班嚶嚶嚶


### greater

寫一支名為greater的巨集
傳入兩個參數並取得較大的那一個
提示：三元運算子(?:)

輸入：傳入兩個參數


輸出：取得較大的那一個

輸入範例：

greater(20,30)

輸出範例：
30

```cpp=
#define greater(x,y) ((x)>(y)?(x):(y)) 
```

---
### division

寫一支名為division的巨集
傳入兩個參數a,b
並取得a除以b的結果

輸入：傳入兩個參數a,b

輸出：取得a除以b的結果

輸入範例：
division(30,5)
輸出範例：
6

```cpp=
#define division(x,y) ((x)/(y))
```

---
### PRINT

寫一支名為PRINT的巨集傳入一個字串

輸入：傳入一個字串
輸出：輸出該字串到螢幕上

輸入範例：
有一個字串char str[20]="Hello World!";
PRINT(str)
輸出範例：
Hello World!

```cpp=
#define PRINT(str) printf("%s",str);
```


## 乙班嗚嗚嗚

### Larger

請完成名為Larger的巨集

功能：
傳入兩個參數
得到較大的參數

輸入：傳入兩個參數
輸出：得到數值較大的參數

輸入範例：
Larger(10, 5)
輸出範例：10

```cpp=
#define Larger(x,y) ((x)>(y)?(x):(y)) 
```

### Exponent
請完成名為Exponent的巨集

功能：
傳入兩個參數
第一個參數為係數
第二個參數為2的指數
兩參數相乘
得到運算結果

例如：
第一個參數為10
第二個參數為5
運算為10 * 2^5 = 320
運算為10 * 2^5 = 320
得到320


輸入：
傳入兩個參數
第一個參數為係數
第二個參數為2的指數

輸出：
兩參數相乘
得到運算結果

輸入範例：
Exponent(10, 5)
輸出範例：
320
```cpp=
#define Exponent(x,y) ((1<<y)*(x))
```

### Mod
請完成名為Mod的巨集

功能：
傳入兩個參數
得到運算結果

例如：
第一個參數為10
第二個參數為3
運算為10 % 3 = 1
得到1


輸入：
傳入兩個參數


輸出：
兩數做mod
得到運算結果


輸入範例：
Mod(10, 3)
輸出範例：
1
```cpp=
#define Mod(x,y) ((x)%(y))
```

### Print

請完成名為Print的巨集

功能：
傳入一個參數(字元陣列)
印出該參數所含的字串

輸入：傳入一個參數(字元陣列)


輸出：印出該參數所含的字串


輸入範例：
char str[100] = "This is macro!";
測試平台自動使用巨集
Print(str)
輸出範例：
This is macro!

```cpp=
#define Print(str) printf("%s",str);
```