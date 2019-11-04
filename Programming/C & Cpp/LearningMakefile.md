# 跟我一起写Makefile笔记
## Chapter 1 概述
make是一个命令工具，是一个解释makefile中指令的命令工具
源文件 -> 编译 compile -> 目标文件.o/.obj -> 链接 link -> 可执行文件
每个源文件对应一个目标文件
目标文件打包，Archive文件.a/库文件.lib
链接时主要链接函数和全局变量

## cc命令
命令 | 例子 | 功能
--- | --- | ---
cc -c | cc -c foobar.c | 生成目标文件.o
cc -o | cc -o foobar foobar.c | 生成可执行文件
cc -g | cc -g foobar.c | 产生一个可调试的可执行文件

## Chapter 2 makefile介绍
* 如果工程没有编译过，所有.c文件都要被编译和链接
* 如果工程的某几个.c文件修改，只编译被修改的.c文件，并链接目标程序
* 如果工程的头文件被修改，需编译引用了这几个头文件的.c文件，并链接目标程序

make可以自动根据文件修改情况，编译和链接

### makefile规则
```makefile
target ... : prerequisites ...
    command

```

prerequisites中如果有一个以上的文件比target文件要新的话，command所定义的命令就会被执行

在Makefile 中的命令，必须要以Tab 键开始

---

* object file centric
```makefile
objects = main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o

edit : $(objects)
    cc -o edit $(objects)

main.o : defs.h
# main.o : main.c defs.h
#   cc -c main.c
kbd.o : defs.h command.h
command.o : defs.h command.h
display.o : defs.h buffer.h
insert.o : defs.h buffer.h
search.o : defs.h buffer.h
files.o : defs.h buffer.h command.h
utils.o : defs.h

.PHONY : clean #.PHONY 表示clean 是一个“伪目标”
    -rm edit $(objects) #减号的意思是，某些文件出现问题，但不要管，继续做后面的事

```

* header file centric
```makefile
objects = main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o

edit : $(objects)
    cc -o edit $(objects)

$(objects) : defs.h
kbd.o command.o files.o : command.h
display.o insert.o serach.o files.o : buffer.h

.PHONY : clean
clean :
    -rm edit $(objects)
```

---

要指定特定的Makefile，使用make 的-f 和--file 参数，如：
```
make -f Make.Linux 
make --file Make.AIX
```

---

引用其他的Makefile
```makefile
include filename
```
filename可以是当前操作系统Shell的文件模式（可以包含路径和通配符）。

---

显示命令
用@ 字符在命令行前，那么这个命令将不被make显示出来 (只显示结果)
```makefile
@echo 正在编译X模块
```
执行命令
```makefile
exec:
    cd /home/hchen; pwd
```

---

嵌套执行make

---

条件判断

* ifeq / ifneq
```makefile
libs_for_gcc = -lgnu
normal_libs =

ifeq ($(CC),gcc)
    libs=$(libs_for_gcc)
else
    libs=$(normal_libs)
endif

foo: $(objects)
    $(CC) -o foo $(objects) $(libs)
```

* ifdef / ifndef
```makefile
foo =
ifdef foo
    frobozz = yes
else
    frobozz = no
endif
```
