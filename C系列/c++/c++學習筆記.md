# c++學習筆記

## hello world

```cpp=
/*hello.cpp*/
#include <iostream> //頭文件

using namespace std; //命名空間

int main() //主函數
{
	cout << "hello world\n";  //輸出
	return 0;
}
```

## 錯誤
```
error: ‘::main’ must return ‘int’
```
解決方法：
main() 唯一合乎標準的回傳類型是 int:
所以改成```int main```就可以了
