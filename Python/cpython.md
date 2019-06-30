---
tags: python,c
---
# cpython
---
## 介紹
當你在用python編譯一個大的程式時候覺得她處理速度很慢嗎?懷念c的執行速度嗎?懶得重寫C的傳統類庫?想對底層程式碼進行連接嗎?那用試試這個方法吧~

我們介紹兩種方法~
1.ctypes
2.SWIG

---
## CTypes

ctypes提供和C語言兼容的數據類型和函數來加載dll文件，因此在調用時不需對源文件做任何的修改。所以這個方法是最簡單的。

示範
1.兩數相加的C程式碼，保存為test.c
```cpp=
//sample C file to add 2 numbers - int and floats
#include <stdio.h>

int add_int(int, int);
float add_float(float, float);

int add_int(int num1, int num2){
    return num1 + num2;

}

float add_float(float num1, float num2){
    return num1 + num2;

}
```
2.接下來將C文件編譯為.so文件(windows下為DLL)。下面操作會生成adder.so文件
```cmake=
#For Linux
$  gcc -shared -Wl,-soname,test -o test.so -fPIC test.c

#For Mac
$ gcc -shared -Wl,-install_name,test.so -o test.so -fPIC test.c

#FOR Windows 使用MinGW
gcc -shared -o test.dll test.c
```
>windows記得要先安裝MinGW

3.在python中開啟他
```python=
from ctypes import *

#load the shared object file
adder = CDLL('./test.dll')
#Find sum of integers
res_int = adder.add_int(4,5)
print "Sum of 4 and 5 = " + str(res_int)

#Find sum of floats
a = c_float(5.5)
b = c_float(4.1)

add_float = adder.add_float
add_float.restype = c_float
print "Sum of 5.5 and 4.1 = ", str(add_float(a, b))
```
輸出如下：
```python=
Sum of 4 and 5 = 9
Sum of 5.5 and 4.1 =  9.60000038147
```
4.說明
在這個例子中，C包含兩個函數，分別實現了int和float的相加。
我們一開始會先將ctypes套件引入，然後用CDLL來加載我們的C程式碼，然後我們便可以通過用變數adder來對c程式呼叫。當adder.add_int()被呼叫時，內部會對c程式中的add_int進行召喚。ctypes允許我們在調用C函數時使用Python中原本的整數和字符字串型態。然而對於bool跟float必須使用正確的ctype類型才可進行轉換，像是要呼叫adder.add_float()時，我們要先將python中的十進制轉成c_float類型，才能發給c函數。
這種方法雖然簡單，但是有著許多限制，例如不能在c中使用物件導向

---
## SWIG

一般不會採用這種方法，因為大多數情況它會帶來不必要的複雜。而當你有一個C/C++代碼庫需要被多種語言調用時，這將是個非常不錯的選擇。

示範~
```cpp=
#include <time.h>
double My_variable = 3.0;

int fact(int n) {
    if (n <= 1) return 1;
    else return n*fact(n-1);
}

int my_mod(int x, int y) {
    return (x%y);
}

char *get_time()
{
    time_t ltime;
    time(&ltime);
    return ctime(&ltime);
}
```
---
進行編譯
LINUX版
```cpp=
unix % swig -python example.i
unix % gcc -c example.c example_wrap.c \
    -I/usr/local/include/python2.1
unix % ld -shared example.o example_wrap.o -o _example.so
```
WINDOWS版
1.下載SWIG
2.編輯.c、.h、.i檔
.h檔示範
```cpp=
int AddOne(int n);
int Sqrt(int n);
```
.c檔示範
```cpp=
#include "example.h"
int AddOne(int n)
{
    return n+1;
}
int Sqrt(int n)
{
    return n*n;
}
```
.i檔示範
```cpp=
%module example
%{
#include "example.h"
%}
%include "example.h"
```

3.放在同一個資料夾
4.打下面指令
```cmake=
#產生example.py  example_wrap.cxx 兩個檔 檔名計的隨你的檔名更改
swig -c++ -python example.i
#產生example.o 
g++ -O2 -fPIC -c example.cpp
#產生example_wrap.o 如果沒有產生代表你的位置錯了，去找到一個叫做python.h的所在檔案位置
g++ -O2 -fPIC -c example_wrap.cxx -IC:\ProgramData\Anaconda3\include
#產生example.so 動態檔 記住example 前一定要加   _ ，因為windows的位置讀取不能讀取空格，你不加他就找不到了
g++ -shared example.o example_wrap.o -o _example.so
```
5.然後你就可以使用這個套件了~

>可能會噴錯誤
>C:/mingw64/lib/gcc/x86_64-w64-mingw32/6.3.0/include/c++/cmath:1157:11: error: '::hypot' has not been declared\r.    using ::hypot;\r.
>如果看到上面的錯誤去更改C:/mingw64/lib/gcc/x86_64-w64-mingw32/6.3.0/include/c++/cmath他的第1157行改成  using ::_hypot;

---
最後python輸出
```python=
import example
example.fact(5)
120
example.my_mod(7,3)
1
example.get_time()
'Sun Feb 11 23:01:07 1996'
```
我們可以發現，使用SWIG一樣可以達到相同的效果，雖然下了更加的麻煩，但如果你的目標是多語言互相溝通，這個方法是比較方便的。

