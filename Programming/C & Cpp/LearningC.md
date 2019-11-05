使用*.c文件实现模块的功能, 使用*.h文件暴露单元的接口, 外部模块只需包含*.h文件就可以使用相应的功能

头文件的写法：
1. 为用户提供调用接口
为用户提供调用接口，这种头文件中声明了模块中需要给其他模块使用的函数和数据。
* 一个模块一个接口，不能几个模块用一个接口。
* 文件名为和实现模块的 c 文件相同。
* 尽量不要使用 extern 来声明一些共享的数据。因为这种做法是不安全的，外部其模块的用户可能不能完全理解这些变量的含义，最好提供函数访问这些变量。
* 尽量避免包含其他的头文件，除非这些头文件是独立存在的。
* 不要包含那些只有在可执行文件中才使用的头文件，这些头文件应该在.c文件中包含。
* 接口文件要有面向用户的充足的注释。从应用角度描述每个暴露的内容。
* 接口文件在发布后尽量避免修改，即使修改也要保证不影响用户程序。
2. 多个代码文件使用一个接口文件
这种头文件用于那些认为一个模块使用一个文件太大的情况。
* 多个代码文件组成的一个模块只有一个接口文件。因为这些文件完成的是一个模块。
* 使用模块下文件命名 <系统名><模块名命名>。
* 不要滥用这种文件。
* 有时候也会出现几个 .c 文件用于共享数据的 .h 文件，这种文件的特点是在一个 .c 文件里定义全局变量，而在其他 .c 文件里使用，要将这种文件和用于暴露模块接口的文件区别。
* 一个模块如果有几个子模块，可以用一个 .h 文件暴露接口，在这个文件里include 包含每个子模块的接口文件。

3. 说明性头文件
这种头文件不需要有一个对应的代码文件，在这种文件里大多包含了大量的宏定义，没有暴露的数据变量和函数。
* 包含一些需要的概念性的东西。
* 命名方式，定义的功能 .h。
* 不包含任何其他的头文件。
* 不定义任何类型。
* 不包含任何数据和函数声明。

---

在c语言的很多库函数中，函数原型中，参数类型都是size_t。
size_t的定义在<stddef.h>, <stdio.h>, <stdlib.h>, <string.h>, <time.h>和<wchar.h>这些标准C头文件中，也出现在相应的C++头文件, 等等中，你应该在你的头文件中至少包含一个这样的头文件在使用size_t之前。

---
Exceptions to array decaying into a pointer：

In C99 there are two fundamental cases, namely:
* when it's the argument of the & (address-of) operator.
* when it's the argument of the sizeof operator.

Furthermore, in C11, the newly introduced alignof operator doesn't let its array argument decay into a pointer either.

In C++, there are additional rules, for example, when it's passed by reference.

---

* Register Variable
Unless you are working on embedded systems where you know how to optimize code for the given application, there is no use of register variables.

* Static Variable

* External Variable

* Automatic Variable

---

### 指针常量
```c
int *p = (int *) 0x12345678;
```

### void *型指针
void *型指针作为一种通用的指针，可以和其它任何类型的指针(函数指针除外)相互转化而不需要类型强制转换
```c
int a = 10; 
char b = 'x'; 

void *p = &a; // void pointer holds address of int 'a' 
p = &b; // void pointer holds address of char 'b' 

```
malloc() and calloc() return void * type and this allows these functions to be used to allocate memory of any data type
```c
int *x = malloc(sizeof(int) * n);
```
Note that the above program compiles in C, but doesn’t compile in C++. In C++, we must explicitly typecast return value of malloc to (int *).

void pointers cannot be dereferenced
``` c
int a = 10; 
void *ptr = &a; 
// printf("%d", *ptr); // compile error
printf("%d", *(int *)ptr); //explicitly typecast
```

The C standard doesn’t allow pointer arithmetic with void pointers.However, in GNU C it is allowed by considering the size of void is 1.

对于一个不确定要指向何种类型的指针，在定义它之后最好把它初始化为NULL，并在解引用这个指针时对它进行检验，防止解引用空指针。

### 零指针常量
一个具有0值的整形常量表达式，或者此类表达式被强制转换为void *类型，则称为空指针常量，它可以用来初始化或赋给任何类型的指针。

ANSI C还定义了一个宏NULL，用来表示空指针常量。
大多数C语言的实现中NULL是采用后面这种方式定义的：
```c 
#define  NULL  ((void *)0)
```

### 指向指针的指针
指针是一种变量，它也有自己的地址，所以它本身也是可用指针指向的对象。
``` c
int n  = 500;
int *p = &n;
int **pp = &p;
printf("%d\n%d\n%d\n", n, *p, **pp);

```

### 字符串指针
本质是将这个字符串的首地址存放到了指针内
``` c
int main(){
    char str1[] = "This is a C string.";
    char str2[] = "This is a C string.";
    char *str3 = "This is a C string.";
    char *str4 = "This is a C string.";
 
    if(str1 == str2)
        printf("str1 and str2 are same\n");
    else
        printf("str1 and str2 are not same\n");
       
    if(str3 == str4)
        printf("str3 and str4 are same\n");
    else
        printf("str3 and str4 are not same\n");
    return 0;
}
```
输出:
```
str1 and str2 are not same
str3 and str4 are same
```
* 这里str3和str4指针指向的是同一个常量字符串。C/C++语法上会把常量字符串存储到单独的一个内存区域，当几个不同的指针同时指向同一个字符串时，他们实际会指向同一块内存（这个字符串的首地址）。所以这几个指针其实是同一个指针。
* 用相同的常量字符串对不同的数组进行初始化时就会在内存中开辟出不同的区域。指向其各自首地址的指针也就是不同的指针了。

## 数组指针 and 指针数组
### 数组指针
它的本质是指针，指针的指向是一个数组；二维数组也是一个数组指针。
```c
int (*arr)[20]
```

### arr and &arr
* arr是数组名，数组名表示数组首元素的地址
* &arr就是数组指针，指针的指向是整个数组

二者指向的地址是相同的但类型不同
* arr+1是指向数组第二个元素的指针。
* &arr+1是指向下一个数组，跨过了整个数组，步距为数组元素的大小之和。

---

## 一维数组传参
数组
```c
int arr[10] = {0};
// method 1 
// 编译器会把函数的参数名arr识别为*arr的指针
// 与其数组大小无关，所以数组大小的参数省略书写也是完全可以的。
void test(int arr[]);
// method 2
void test(int arr[10]);
// method 3
// 编译器会把传入函数的数组参数隐式转化为指针*arr
void test(int *arr);
```

## 二维数组传参
```c
int arr[3][5] = {0};
// method 1
void test(int arr[3][5]);
// method 2
// C语言规定二维数组行数可以省略，但列数不可省
void test(int arr[][5]);
```
数组指针
```c
int arr[3][5] = {0};
// 数组指针，可以正确传参
void test(int (*arr)[5])

```

---

对指针进行初始化时常用的有以下几种方式：
1.采用NULL或空指针常量
``` c
int *p = NULL;
char *p = 2-2;
float *p = 0;
```
2.将一个对象的地址赋给一个指针
``` c
int i = 3;  
int *ip = &i；
```
3.将一个指针常量赋给一个指针
``` c
long *p = (long *)0xfffffff0;
```
4.将一个数组名赋给一个相同类型的指针
```c
char ary[100]; 
char *cp = ary;
```
5.将一个指针的地址赋给一个指针
```c
int i = 3;  
int *ip = &i；
int **pp = &ip;
```
6.将一个字符串常量赋给一个字符指针
```c
char *cp = "abcdefg";
```
