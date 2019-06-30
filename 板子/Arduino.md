---
tags: ARDUINO
---
# Arduino

---

設定腳位
```=
pinMode(腳位,INPUT);
pinMode(腳位,OUTPUT);
```

---

暫停
```=
delay(毫秒)
```

---

寫入
```=
digitalWrite(腳位,HIGH);
digitalWrite(腳位,LOW)
```

---

當你想要知道按鈕按下去是1還是0時，可以用這兩個指令
```=
Serial.begin(band);
```
Serial.begin：序列付初始化
baud:鮑率，傳輸速率，兩裝置鮑率須相同才能正常通訊
```=
Serial.println(val);
```
Serial.println：透過序列阜傳輸顯示並換行
val：要顯示的變數


---

判斷if else
```=
if(條件)：{}

else：{}
```
---

for迴圈
```=
for(int i=x;i<=y;i+=z){}
for(int i=0;i<=10;i++){}
```
---

訊號分為類比跟數位

數位：只能輸出高電位或低電位
類比：可以輸出3.5、4V等以數字表達電位

---
Arduino是模擬類比不是真類比，採用pwm來進行模擬
pwm：透過數位輸出高低電位的比例，在高頻率的狀態下達到類比輸出
pwm腳位：3、5、6、9、10、11

ex.如果要輸出2.5v，他是輸出50%的5v+50%的0v，以達到2.5v

輸出
```=
analogWrite(腳位,value);
```
value：愈輸出的值(0~255)

讀取
```=
analogRead(腳位)
```
analogRead：類比讀取

類比讀取：讀取腳位(A0~A5) 與GND的**電壓差** 0V~5V ，輸出數字為0~1024

---


