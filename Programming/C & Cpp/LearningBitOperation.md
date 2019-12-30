无符号的移位操作为逻辑移位，即高位舍弃，低位补0；高位补0，低位舍弃。
有符号的整数类型的移位操作为算数移位，也就是最高位保持不变，负数高位移位后还是保持“1”，正数移位后还是保持“0”，而其他位和逻辑移位一样。
C语言不支持浮点数的移位操作

& 按位与
| 按位或
^ 按位异或（相同0，不同1）
异或常被认作不进位加法
逆运算是它本身(a xor b) xor b = a
~ 按位取反
\>> 右移，除以2取整
<< 左移，乘2


1. 指定的某一位数置1
```c
#define setbit(x,y)  x|=(1<<y)
```

2. 指定的某一位数置0
```c
#define clrbit(x,y)  x&=~(1<<y)
```

3. 指定的某一位数取反

```c
#define reversebit(x,y)  x^=(1<<y)
```

4. 获取的某一位的值
```c
#define getbit(x,y)   (x &= (1<<y))
```

浮点数的移位
使用串口/IIC/CAN等通信时，需要将数据一字节一字节的发送，对于浮点数来说，就需要将浮点数分解成字节

``` c
float a;
uint32_t *data = (uint32_t *)&a;
```

```c
//浮点数的移位操作
#include "stdint.h"
#include "stdio.h"


int main(void)
{
    double  val = 48646.1123;
    double  Result = 0;

    uint8_t data2[8];

    // convert double into 8 uint8
    for (int i = 0;i < 8;i++) 
    {
        data2[i] = ((*(uint64_t *)&val) >> (8 * i)) & 0xff;
    }

    // recover double from 8 unint 8
    for (int i = 0;i < 8;i++) 
    {
        (*(uint64_t *)&Result) = (*(uint64_t *)&Result) << 8 | data2[7 - i];
    }

    printf("%f", Result);
    return 0;
}

```
Union: a single variable, i.e., same memory location, can be used to store multiple types of data
```c

//使用联合体达到移位操作效果
#include "stdio.h"
#include "stdint.h"
#include "string.h"
int main(void)
{
    union
    {
        uint8_t data[8];
        double  val;
    }test,test2;

    double x=5.1;
    double re;
    int i;

    test.val=x;
    for(i=0;i<8;i++)
    {
        test2.data[i]=test.data[i];
    }
    re=test2.val;

    printf("%f",re);
    return 0;
}

```