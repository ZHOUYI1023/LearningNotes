Inline Function Uses Guidelines :-
1. Always use inline function when your are sure it will give performance.
1. Always prefer inline function over macros.
1. Don't inline function with larger code size, one should always inline small code size function to get performance.
1. If you want to inline a function in class, then prefer to use inkine keyword outside the class with the function definition.
1. In c++, by default member function declared and defined within class get linlined. So no use to specify for such cases.
1. Your function will not be inlined in case there is differences between exception handling model. Like if caller function follows c++ structure handling and your inline function follows structured exception handling.
1. For recursive function most of the compiler would not do in-lining but microsoft visual c++ compiler provides a special pragma for it i.e. pragma inline_recursion(on) and once can also control its limit with pragma inline_depth.

1. If the function is virtual and its called virtually then it would not be inlined. So take care for such cases, same hold true for the use of function pointers.

---
TODO:
函数指针
指针++

---
TODO:
const int * const a

---
TODO:
sizeof()
1. 基本数据类型
```cpp
sizeof(int)
```
2. 结构体

结构体的sizeof涉及到字节对齐问题。

为什么需要字节对齐？计算机组成原理教导我们这样有助于加快计算机的取数速度，否则就得多花指令周期了。为此，编译器默认会对结构体进行处理（实际上其它地方的数据变量也是如此），让宽度为2的基本数据类型（short等）都位于能被2整除的地址上，让宽度为4的基本数据类型（int等）都位于能被4整除的地址上，依次类推。这样，两个数中间就可能需要加入填充字节，所以整个结构体的sizeof值就增长了。

字节对齐的细节和编译器的实现相关，但一般而言，满足三个准则：
* 结构体变量的首地址能够被其最宽基本类型成员的大小所整除。
* 结构体的每个成员相对于结构体首地址的偏移量（offset）都是成员大小的整数倍，如有需要，编译器会在成员之间加上填充字节（internal adding）。
* 结构体的总大小为结构体最宽基本类型成员大小的整数倍，如有需要，编译器会在最末一个成员后加上填充字节（trailing padding）。

```cpp
struct S1
{
    char a;
    int b;
};
sizeof(S1);//值为8，字节对齐，char之后填充3个byte

struct S2
{
    int a;
    char b;
};
sizeof(S2);//值为8，字节对齐，char之后填充3个byte

struct S3
{    
};
sizeof(S3);//值为1，空结构体也占内存

```
3. 联合体

4. 数组
数组的sizeof值等于数组所占用的内存字节数。
注意：
* 当字符数组表示字符串时，其sizeof值将’/0’计算进去。
* 当数组为形参时，其sizeof值相当于指针的sizeof值。 


5. 指针

在32位计算机中，一个指针变量的返回值必定是4。
```cpp
char *b = "helloworld";  
char *c[10];  
double *d;  
int **e;  
void (*pf)();    
  
cout<<"char *b = /"helloworld/"     "<<sizeof(b)<<endl;//指针指向字符串，值为4  
cout<<"char *b                    "<<sizeof(*b)<<endl; //指针指向字符，值为1  
cout<<"double *d                  "<<sizeof(d)<<endl;//指针，值为4  
cout<<"double *d                  "<<sizeof(*d)<<endl;//指针指向浮点数，值为8  
cout<<"int **e                  "<<sizeof(e)<<endl;//指针指向指针，值为4  
cout<<"char *c[10]                "<<sizeof(c)<<endl;//指针数组，值为40  
cout<<"void (*pf)();              "<<sizeof(pf)<<endl;//函数指针，值为4
```

6. 函数

sizeof也可对一个函数调用求值，其结果是函数返回值类型的大小，函数并不会被调用。
对函数求值的形式：sizeof(函数名(实参表))
```cpp
#include <iostream>  
using namespace std;  
float FuncP(int a, float b)  
{  
    return a + b;  
}  
  
int FuncNP()  
{  
    return 3;  
}  
  
void Func()  
{  
}  
  
int main()  
{  
cout<<sizeof(FuncP(3, 0.4))<<endl; //OK，值为4，sizeof(FuncP(3,0.4))相当于sizeof(float)  
cout<<sizeof(FuncNP())<<endl; //OK，值为4，sizeof(FuncNP())相当于sizeof(int)  
/*cout<<sizeof(Func())<<endl; //error，sizeof不能对返回值为空类型的函数求值*/  
/*cout<<sizeof(FuncNP)<<endl; //error，sizeof不能对函数名求值*/  
return 0;  
}

```




7. string

---
TODO:
memset
memcopy

---
TODO:
智能指针

---

## 指针和引用

如果的确只需要借用一下某个对象的"别名"，那么就用"引用"，而不要用"指针"，以免发生意外。

```cpp
int m; 
int &n = m;



```
非常量引用不能与字面值绑定在一起
```cpp
int &p = 1024;//error
const int &p = 1024;//right
```

* 指针是一个变量，只不过这个变量存储的是一个地址，指向内存的一个存储单元；而引用跟原来的变量实质上是同一个东西，只不过是原变量的一个别名而已。
* 引用在定义的时候必须初始化；
* 引用不可以为空，当被创建的时候，必须初始化，而指针可以是空值，可以在任何时候被初始化。
* 指针是一个实体他在栈中有自己使用的空间，但是引用没有，”sizeof引用”得到的是变量(对象)的大小，而”sizeof指针”得到的是指针本身的大小；
* 指针和引用的自增(++)运算意义不一样；
    * 引用++，改变了这个值本身;
    * 指针++，改变了指针本身，指针本身存储的是地址,该指针指向了别处地址，对变量本身没有影响;
* 引用和指针作为参数的时候不一样。指针的开销更大，所以尽可能的使用引用。
    * 引用作为参数传参不用拷贝，直接在原变量上进行操作，形参和实参实际上是同一个变量，不过形参是实参的别名。
    * 指针作为参数传参时需要在函数栈桢内创建一个形参，形参是利用实参拷贝构造的（系统默认给出的是浅拷贝），形参指向的空间和原指针指向的一致。形参和实参都可以达到改变变量的目的，不过形参和实参两者是不同的两个变量。
* 指针比较灵活复杂一点，容易出错，所以使用的时候必须谨慎。
    * 比如说指针可以指向空，引用不行，所以使用前必须判断是否为空；
    * 指针所指向的地址被释放了以后，指针却还指向该内存，就会出现“野指针”的问题。所以释放了指针所指向的空间之后，最好将指针置空。
    * 指针可以随意加进行++ -- 而不改变变量本身，引用++ -- 会改变变量。

 **指针转引用**
```cpp
int Discover(std::vector<tDeviceInfo>& pDeviceInfo);//函数声明为引用类型
std::vector<DeviceData::DeviceInfo>* mDeviceInfo;//参数声明为指针类型
Discover(*mDeviceInfo); //加上*就是指针转引用
```

**引用的指针no；指针的引用ok**
C++不允许定义引用的指针，因为==引用本身只是与另一个对象绑定在一起的该对象的别名，而并非一个对象==，所以标准规定不能定义指向引用的指针报错：
```cpp
int a = 20;
int &*ptr = &a;// error
```
但是由于指针是个对象，所以定义一个指针的引用是可以的：
```cpp
int a = 20;
int *&b = &a;// ok
```