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

## register
不能对它应用一元的 '&' 运算符（因为它没有内存位置）
Unless you are working on embedded systems where you know how to optimize code for the given application, there is no use of register variables.

## auto
auto存储类是所有局部变量默认的存储类。

## static
* 使用 static 修饰局部变量可以在函数调用之间保持局部变量的值
* 当 static 修饰全局变量时，会使变量的作用域限制在声明它的文件内
* 静态函数只能在声明它的文件中可见，其他文件不能引用该函数。不同的文件可以使用相同名字的静态函数，互不影响

==非静态函数可以在另一个文件中直接引用，甚至不必使用extern声明==
有的公司编码规范明确规定只用于本文件的函数要全部使用static关键字声明，这是一个良好的编码风格。


## extern
普通全局变量对整个工程可见，其他文件可以使用extern外部声明后直接使用。也就是其他文件不能再定义一个与其相同名字的变量了。

* 对变量而言，如果你想在本源文件中使用另一个源文件的变量，就需要在使用前extern声明该变量，或者在头文件中用extern声明该变量；

* 对函数而言，如果你想在本源文件中使用另一个源文件的函数，就需要在使用前用声明该变量，声明函数加不加extern都没关系，所以在头文件中函数可以不用加extern

### extern 变量
```c
extern int a;//声明一个全局变量a, 可重复声明

int a; //定义一个全局变量
extern int a =0 ;//定义一个全局变量a 并给初值。
int a =0;//定义一个全局变量a,并给初值，
```
当你要引用一个全局变量的时候，你就要声明，extern int a;这时候extern不能省略，因为省略了，就变成int a;这是一个定义，不是声明。

extern 指针变量
```c
// 函数指针
// 在header中声明
extern void (*current_menu)(int);
// 在一个源文件中定义
void (*current_menu)(int) = &the_func_i_want;
```

### extern函数

声明的时候用extern说明这是一个声明
定义的时候用extern，说明这个函数是可以被外部引用的
但由于函数的定义和声明是有区别的，定义函数要有函数体，声明函数没有函数体，所以函数定义和声明时都可以将extern省略掉

---

## 回调函数
函数指针变量可以作为某个函数的参数来使用的，回调函数就是一个通过函数指针调用的函数。(为什么不直接调用？因为回调可随意更换)
```c
#include <stdlib.h>  
#include <stdio.h>
 
// 回调函数
void populate_array(int *array, size_t arraySize, int (*getNextValue)(void))
{
    for (size_t i=0; i<arraySize; i++)
        array[i] = getNextValue();
}
 
// 获取随机值
int getNextRandomValue(void)
{
    return rand();
}
 
int main(void)
{
    int myarray[10];
    populate_array(myarray, 10, getNextRandomValue);
    for(int i = 0; i < 10; i++) {
        printf("%d ", myarray[i]);
    }
    printf("\n");
    return 0;
}

```
typedef函数指针
```c
typedef void (*sighandler_t)(int);
sighandler_t signal(int signum, sighandler_t handler);
```

```c
#include <stdlib.h>  
#include <stdio.h>
 
// 回调函数
typedef int (*getNextValue)(void)

void populate_array(int *array, size_t arraySize, getNextValue getNextRandomValue)
{
    for (size_t i=0; i<arraySize; i++)
        array[i] = getNextRandomValue();
}
 
// 获取随机值
int getNextRandomValue(void)
{
    return rand();
}
 
int main(void)
{
    int myarray[10];
    populate_array(myarray, 10, getNextRandomValue);
    for(int i = 0; i < 10; i++) {
        printf("%d ", myarray[i]);
    }
    printf("\n");
    return 0;
}


```

---

## 结构体中的函数指针
C语言中的struct是最接近类的概念，但是在C语言的struct中只有成员，不能有函数，但是可以有指向函数的指针
```c
#include <stdio.h>
struct DEMO{
    int x,y;
    int (*func)(int,int); //函数指针
};
 
int add1(int x,int y){
    return x*y;
}
 
int add2(int x,int y){
    return x+y;
}
 
void main(){
    struct DEMO demo;
    demo.func=add2; //结构体函数指针赋值
    printf("func(3,4)=%d\n",demo.func(3,4));
    demo.func=add1;
    printf("func(3,4)=%d\n",demo.func(3,4));
}

```

---
## implicit type conversion
### 整数提升
```c
//把小于 int 或 unsigned int 的整数类型转换为 int 或 unsigned int 
int  i = 17;
char c = 'c';
int sum;
sum = i + c; // char->int

```
### 算术转换
```c
int  i = 17;
char c = 'c';
float sum;
// 隐式地把两边值强制转换为相同的类型
// 编译器首先执行整数提升
// 如果操作数类型不同，被转换为下列层次中出现的最高层次的类型
sum = i + c;// 整数提升char->int, 算术转换int->float
```
## explicit type conversion
### 强制类型转换

```c
int sum = 17, count = 5;
double mean;
//强制类型转换运算符的优先级大于除法
//因此 sum 的值首先被转换为 double 型，然后除以 count，得到一个类型为 double 的值。
mean = (double) sum / count;

```

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
* arr是数组名，数组名表示数组首元素的地址， *arr得到的是arr[0]
* &arr就是数组指针，指针的指向是整个数组, *&arr得到的是arr

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

---

## 悬挂指针/野指针
指针指向非法的内存地址，那么这个指针就是悬挂指针，也叫野指针。
* 使用未初始化的指针
* 指针所指的对象已经消亡
* 指针释放后之后未置NULL
对指针进行free和delete，只是把指针所指的内存空间给释放掉，但并没有把指针本身置空，此时指针指向的就是“垃圾”内存。
* 在C语言中，realloc函数使用不当

---

## Dynamic Memory Allocation
https://www.programiz.com/c-programming/c-dynamic-memory-allocation


---

### union

共用体是一种特殊的数据类型，允许您在相同的内存位置存储不同的数据类型。您可以定义一个带有多成员的共用体，但是任何时候只能有一个成员带有值。共用体提供了一种使用相同的内存位置的有效方式。

* the size of a union variable will always be the size of its largest element
```c
union unionJob
{
   //defining a union
   char name[32];
   float salary;
   int workerNo;
} uJob;

int main()
{
   printf("size of union = %d bytes", sizeof(uJob));
   return 0;
}

```
Output
```
size of union = 32

```

* Only one union member can be accessed at a time 
```c
union Job
{
   float salary;
   int workerNo;
} j;
int main()
{
   j.salary = 12.3;
   j.workerNo = 100;
   printf("Salary = %.1f\n", j.salary);
   printf("Number of workers = %d", j.workerNo);
   return 0;
}

```
Output
```
Salary = 0.0
Number of workers = 100
```

---

结构体对齐

所有的成员在分配内存时都要与所有成员中占内存最多的数据类型所占内存空间的字节数对齐。
假如这个字节数为 N，那么对齐的原则是：
* 理论上所有成员在分配内存时都是紧接在前一个变量后面依次填充的
* 如果一行中剩下的空间不足以填充某成员变量，则该成员变量在分配内存时另起一行分配

但有时候为了增强程序的可读性,需要没有规律地写

``` c
struct Align12{
    char c1;
    int i1;
    char c2;
};

struct Align8{
    char c1;
    char c2;
    int i1;
};

struct Align16{
    char c1;
    char c2;
    char c3;
    char c4;
    char c5;
    int i1;
    char c6;
};

```

---

字符串数组不能用"="直接赋值, 即s="Good News!"是不合法的。所以应分清字符串数组和字符串指针的不同赋值方法。 

字符串指针
```c
char *str;
str = "This is a C string.";
```

1、定义的时候直接用字符串赋值
```c
char a[10]="hello";
```
2、定义的时候逐个赋值
```c
char a[10]={'h','e','l','l','o'};
```
3、利用strcpy
``` c
char a[10]; 
strcpy(a, "hello");
```

易错情况：
```c
char a[10]; 
a[10] = "hello";//一个字符怎么能容纳一个字符串？况且a[10]也是不存在的！
a = "hello";//a虽然是指针，但是它已经指向在堆栈中分配的10个字符空间，现在这个情况a又指向数据区中的hello常量，这里的指针a出现混乱
```

---

* 运算符共分为15级，1级优先级最高，15级优先级最低
* 同一优先级的运算符，运算次序由结合方向所决定。(结合性：2 13 14 是从右至左 其他都是 从左至右)
* 简单记就是：！ > 算术运算符 > 关系运算符 > && > || > 赋值运算符

```
括号成员第一;            //括号运算符[]() 成员运算符. ->

全体单目第二;            //所有的单目运算符比如++、 --、 +(正)、 -(负) 、指针运算*、&
乘除余三,加减四;         //这个"余"是指取余运算即%

移位五，关系六;          //移位运算符：<< >> ，关系：> < >= <= 等

等于(与)不等排第七;      //即== 和!=

位与异或和位或;   "三分天下"八九十;     //这几个都是位运算: 位与(&)异或(^)位或(|) 

逻辑或跟与;              //逻辑运算符:|| 和 &&

十二和十一;             //注意顺序:优先级(||) 底于 优先级(&&) 

条件高于赋值;           //三目运算符优先级排到13 位只比赋值运算符和","高

逗号运算级最低!         //逗号运算符优先级最低 
```

---

结构体的不完整声明
```c

struct B;    //对结构体B进行不完整声明
 
//结构体A中包含指向结构体B的指针
struct A
{
    struct B *partner;
    //other members;
};
  
//结构体B中包含指向结构体A的指针，在A声明完后，B也随之进行声明
struct B
{
    struct A *partner;
    //other members;
};
```
---

enum类型

1. 枚举常量（也就是花括号中的常量名）默认第一个枚举常量的值为0，往后每个枚举常量依次递增1
2. 在部分显示说明的情况下，未指定的枚举名的值将依着之前最有一个指定值向后依次递增
3. 一个整数不能直接赋值给一个枚举变量，必须用该枚举变量所属的枚举类型进行类型强制转换后才能赋值
4. 同一枚举类型中不同的枚举成员可以具有相同的值
5. 同一个程序中不能定义同名的枚举类型，不同的枚举类型中也不能存在同名的枚举成员
```c
enum week{Mon = 1, Tues, Wed, Thurs}num;

num = (enum week)10;
printf("%d", num);

```

