引用变量是一个别名，也就是说，它是某个已存在变量的另一个名字。

一旦把引用初始化为某个变量，就可以使用该引用名称或变量名称来指向变量。

引用必须在定义时初始化，并且一旦绑定到一个变量后，就不能再绑定到其他变量。

int a = 10;
int &ref = a;  // ref 是 a 的引用
- `int &ref` 表示 `ref` 是一个 `int` 类型的引用。
- `ref` 是 `a` 的别名，对 `ref` 的操作会直接作用于 `a`。
## C++ 引用 vs 指针

引用很容易与指针混淆，它们之间有三个主要的不同：
	- 不存在空引用，引用必须连接到一块合法的内存。
	- 一旦引用被初始化为一个对象，就不能被指向到另一个对象。指针可以在任何时候指向到另一个对象。
	- 引用必须在创建时被初始化。指针可以在任何时间被初始化。
	- 引用的对象必须是一个变量，而指针必须是一个地址。

## 引用作为参数
```
#include <iostream>
using namespace std;
 
// 函数声明
void swap(int& x, int& y);
 
int main ()
{
   // 局部变量声明
   int a = 100;
   int b = 200;
 
   cout << "交换前，a 的值：" << a << endl;
   cout << "交换前，b 的值：" << b << endl;
 
   /* 调用函数来交换值 */
   swap(a, b);
 
   cout << "交换后，a 的值：" << a << endl;
   cout << "交换后，b 的值：" << b << endl;
 
   return 0;
}
 
// 函数定义
void swap(int& x, int& y)
{
   int temp;
   temp = x; /* 保存地址 x 的值 */
   x = y;    /* 把 y 赋值给 x */
   y = temp; /* 把 x 赋值给 y  */
  
   return;
}
```

## 引用作为返回值
通过使用引用来替代指针，会使 C++ 程序更容易阅读和维护。C++ 函数可以返回一个引用，方式与返回一个指针类似。
```
#include <iostream>
using namespace std;

// 返回对静态变量的引用
int& getStaticRef() {
    static int num = 5; // 静态变量
    return num;
}

int main() {
    int& ref = getStaticRef(); // 获取对静态变量的引用
    cout << "初始值：" << ref << endl;

    ref = 10; // 修改静态变量的值

    cout << "修改后的值：" << ref << endl;
    cout << "再次调用函数后的值：" << getStaticRef() << endl;

    return 0;
}
```
**当返回一个引用时，要注意被引用的对象不能超出作用域。所以返回一个对局部变量的引用是不合法的，但是，可以返回一个对静态变量的引用。**