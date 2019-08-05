# 链接，装载与库
## 第2部分 静态链接
### 第2章 编译和链接
编译+链接=构建Build
预处理 -> 编译 -> 汇编 -> 链接
#### 预编译： 生成.i
处理#开头的预编译指令
删除所有注释
保留#pragma编译器指令 
#### 编译：生成.s
* 扫描scanner -> tokens
* 语法分析parser -> syntax tree
* 语义分析semantic analyzer -> commented syntax tree 标识数据类型
* 源代码优化source code optimizer -> intermediate representation
* 代码生成code generator -> target code 依赖于目标机器 
* 目标代码优化code optimizer -> final target code
#### 汇编： 生成.o
汇编代码转为机器可执行指令
输出目标文件object file
#### 链接： 生成可执行文件.out/
目标文件和库链接
* 地址和空间分配address and storage allocation
* 符号决议symbol resolution
* 重定位 relocation
### 第3章 目标文件
#### 目标文件的格式
类型|windows| linux
---|---|---
存储格式|PE-COFF|ELF
目标文件|.obj|.o
可执行文件|.exe|ELF 
动态链接库|.dll|.so
静态链接库|.lib|.a
#### 目标文件
* file header
* 代码段 .text section
* 程序数据 
    * 已初始化的全局变量和局部静态变量 数据段.data section
    * 未初始化的全局变量和局部静态变量（默认值为0）的预留位置 .bss section 不占空间

- 为什么代码和数据要分开？
    * 指令和数据映射到两个虚存分区，指令只读，数据可读可写
    * CPU数据缓存和指令缓存分离
    * 内存共享 
#### ELF文件结构
* 文件头 ELF Header
* 各个段 数据段，代码段...
* 段表 section header table
* 重定位表 
* 字符串表 字符串长度不固定，把字符串集中存储在一个表，然后用偏移来引用字符串
#### 链接的接口——符号Symbol
在链接中，将函数和变量统称为符号

#### 调试信息

### 第4章 静态链接