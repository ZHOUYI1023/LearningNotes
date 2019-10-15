Python是一种解释型语言，比编译型语言运行慢。
以字节编译，生成一种近似机器语言的中间形式。

---

Unix系统有一个命令叫env，位于/bin或/usr/bin中，会帮助在系统搜索路径中找到python解释器
在脚本首行写启动指令：
```#!/usr/bin/env python```
或
```#!/bin/env python```

---

添加搜索路径
``` python
import sys
sys.path
sys.path.append('/home/...')
```
---

可以在任何需要放置数据的地方设置一个名称空间。例如函数，模块，类。

---

 ``` python
from module import * # 覆盖当前命名空间中现有的名字，污染命名空间
 ```

---

可调用对象
* 函数
1. 内建函数 Built-in Function
``` python
dir(__builtins__)
```
用c/c++写的，编译过放入python解释器，在__builtin__模块里
在Python中并没有__builtins__这个模块，只有__builtin__模块，__builtins__模块只是在启动Python解释器时，解释器为我们自动创建的一个到__builtin__模块的引用

https://yq.aliyun.com/articles/40788

2. 用户定义的函数 User-Defined Function
3. lambda表达式
* 方法
1. 内建方法 Built-in Method
2. 用户定义的方法 User-defined Method
* 类

---

 in Python 3, decimals are rounded to the nearest even number.
 四舍六入五成双，作用是让统计数据更公平，降低舍入的误差。
 ``` python
round(15.5) # 15
round(16.5) # 15
 ```

---

eval()对表达式求值，后者可为字符串或内建函数compile()创建的预编译代码对象
``` python
eval('932')
eval('100 + 200') # int('100 + 200') ValueError
```
exec obj被执行的对象可以是原始字符串，也可是文件

``` python
exec """
x = 0
print 'x is currently:', x
while x < 5:
    x += 1
    print 'incrementing x to:', x
"""

f = open('xcount.py')
exec f
f.close()

execfile('xcount.py')
```




---

```python
func(positional_args, keyword_args, *tuple_grp_nonkw_args, **dict_grp_kw_args)
```


*args可实现任意无名参数的tuple or list打包，tuple or list 的解包
*args在赋值操作中将元素打包为list,在函数中将元素打包为tuple
**kwargs可实现任意键值对的dict打包，dict 的解
``` python
## 打包
def func(a,*arg,**kwargs):
    print(a)
    print(arg)
    print(kwargs)

func(1,2,3,4,key1=1,key2=2)
func(1,2,3,4,{'key1:1,key2:2'})
func(1,2,3,4,**{'key1:1,key2:2'})

# 输出：1; (2, 3, 4); {'key1': 1, 'key2': 2} 
# 输出: 1; (2, 3, 4, {'key1:1,key2:2'}); {}
# 输出：1; (2, 3, 4); {'key1': 1, 'key2': 2} 

_,*args,_=[1,2,3,4]    #_表示占位，接收一个元素赋值后丢弃

# 输出：[2, 3]  

## 解包
def func1(a,b,*args):
    print(a)
    print(b)
    print(args)

def func2(a,c,**kw):
    print(a)
    print(c)
    print(kw)
    
func1(*[1,2,3,4])
func2(**{'a':1,'b':2,'c':3,'d':4})

# 输出：1; 2; (3, 4)
# 输出：1; 3; {'b': 2, 'd': 4}  
```

---

try-except语句是为了更好地跟踪潜在的错误并在代码里准备好处理异常的逻辑，而不是过滤掉致命错误。
``` python
try:
    let_us_cause_a_NameError
except NameError as err:
    print(err, '--> our error message')
finally:
    print('done')
    
raise IOError("file error")
```

---

 闭包

---

* 什么是Iterable(可迭代对象)？
    * 实现了__iter__方法，并返回迭代器的对象
    * 或者实现了__getitem__方法，并且可以通过下标从0开始依次取值的对象；取值结束后抛出IndexError
* 什么是Iterator(迭代器)？
    * 实现了next()方法或者__next__()的对象；

for语句循环的工作流程是：先判断被循环的是否是Iterable：如果不是，尽管实现了next()，它扔不会去调用，会直接报异常；如果对象有__iter__会使用迭代器；但是如果对象没有__iter__，但是实现了__getitem__，会改用下标迭代的方式。

---

生成器是一个带yield语句的函数。一个函数只返回一次，但一个生成器能暂停执行并返回一个中间的结果。生成器的next()方法被调用时，就会从离开的地方继续。Python的for循环带有__next__()调用和对StopIteration的处理。

Yield are used in Python generators. A generator function is defined like a normal function, but whenever it needs to generate a value, it does so with the yield keyword rather than return. If the body of a def contains yield, the function automatically becomes a generator function.

Yield can produce a sequence of values. We should use yield when we want to iterate over a sequence, but don’t want to store the entire sequence in memory.

``` python
# A generator function that yields 1 for first time, 
# 2 second time and 3 third time 
def simpleGeneratorFun(): 
    yield 1
    yield 2
    yield 3

myG = simpleGeneratorFun()  
myG.__next__() # 1
myG.__next__() # 2
next(myG) # 3
next(myG) # StopIteration

for value in simpleGeneratorFun():  
    print(value) 
```

``` python
# A Python program to generate squares from 1 
# to 100 using yield and therefore generator 
  
# An infinite generator function that prints 
# next square number. It starts with 1 
def nextSquare(): 
    i = 1; 
  
    # An Infinite loop to generate squares  
    while True: 
        yield i*i                 
        i += 1  # Next execution resumes  
                # from this point      
  
# Driver code to test above generator  
# function 
for num in nextSquare(): 
    if num > 100: 
         break    
    print(num) 

```
生成器表达式
和列表解析非常相似，基本语法相同；不过并不创建列表，而是返回一个生成器。内存友好。
``` python
gen_object = (expr for iter_var in iterable if cond_expr)
```

---

列表解析 List Comprehension
``` python
[expr for iter_val in iterable]
[expr for iter_val in iterable if cond_expr]

i = 1
print('before: i =', i) # 1
print('comprehension:', [i for i in range(5)])
# the loop control variables are no longer leaked into the surrounding scope
print('after: i =', i) # 1

```

---

Lambda表达式
``` python
a = lambda x, y = 2: x + y
a(3) # 5
a(3,5) # 8 

b= lambda *z: z
b(23, 'xyz') # (23, 'xyz')
b(42) # (42,)
```

---

可变对象值的方法是没有返回值的

---

* 不可变对象
不可变对象是指对象的内存值不能被改变。Python中变量以引方式指向对象，如果变量引用了不可变对象，当改变该变量时于其所指的对象的值不能被改变，相当于把原来的值复制一份改变，这会开辟一个新的地址，变量再指向这个新的地址，即引用了新的对象数值类型（整数和浮点）、字符串str、元组tuple都是不可型。比如a=1，b=[1]，c={'a':1}，id(a)、id(b[0])、id(1id(c['a'])将输出一样的值，因为1是不可变对象，其在内存不可改变的。

* 可变对象
可变对象是指对象的内存值可以被改变，变量（准确的说是引用改变后，实际上是其所指的值直接发生改变，并没有发生复制为，也没有开辟新的内存地址，通俗点说就是原地改变。列list、字典dict、集合set是可变类型。
* 对象的内存地址
可以使用内置函数id()查看python对象的内存地址。下面是一些意事项：
(1) python中所有数字、字符串、list等值，创建时会分配内空间，变量通过引用的方式使用它们。比如a=1和b=1，id(a)和i(b)的输出一样，表示a和b都指向相同的内存地址，即引用了同个不可变对象；但是a=[1]和b=[1]，id(a)和id(b)将输出不一的值，a和b指向的是不同的内存地址，即引用了不同的可变对象说明各可变对象是相互独立的，在内存中有独立的内存地址；
(2) 可用 is 判断两个对象的id（即内存地址）是否一样，用== 判断两个对象的值是否一样。None值也有内存地址；
(3) list、set对象有各自的独立内存空间，他们的各元素以引的方式指向可变、不可变对象；
(4) 函数形参的默认值，在内存中会开辟独立的内存空间。比如试代码中test函数的param参数，其默认值是空list，如果调用未传参，则param指向内存中预先分配好的地址，该地址存储的list类型的值；当调用时传参为a，则param引用了a指向的内存间；
(5) python使用引用计数和垃圾回收来释放内存对象，每个内存象都维护了一个引用计数，包括各种数字、字符串、list、set类型值，以及类实例对象等等，当这些对象的引用计数为 0 时，被解释器回收内存。每次对对象进行引用操作，都会导致其引用数加1， 如下面测试代码中的整数1，列表a、b、c、d、n都引用整数1，以及test函数中的append操作，都会导致数字1的引用计加1；
(6) copy和deepcopy方法都创建了新的内存对象，如测试代码的b和c都是新的变量，其各个元素可能是指向同一个内存空间。值操作是指向同一个内存块，同时增加引用计数。copy是浅拷贝deepcopy是深拷贝，特别对于可变对象，copy是以引用的方式指同一个可变对象，而deepcopy会开辟新的内存地址，也就是创建新的可变对象。
---

``` python
f = open('C:\windows\temp\readme.txt','r')
# IOError due to \t and \r
f = open(r'C:\windows\temp\readme.txt','r')
```

---

Simple way to get input data from console
```python
input_string_var = input("Enter some data: ") # Returns the data as a string
```
``` python
type((1))   # => <class 'int'>
type((1,))  # => <class 'tuple'>
```

___

You can find out which functions and attributes are defined in a module.
``` python
import math
dir(math)
```
If you have a Python script named math.py in the same folder as your current script, the file math.py will be loaded instead of the built-in Python module. This happens because the local folder has priority over Python's built-in libraries.

___

``` python
class Human:
    # A class attribute. It is shared by all instances of this class
    species = "H. sapiens"
    # Note that the double leading and trailing underscores denote objects
    # or attributes that are used by Python but that live in user-controlled
    # namespaces. Methods(or objects or attributes) like: __init__, __str__,
    # __repr__ etc. are called special methods (or sometimes called dunder methods)
    # You should not invent such names on your own.
    def __init__(self, name):
        self.name = name
        self._age = 0

    def say(self, msg):
        print("{name}: {message}".format(name=self.name, message=msg))

    def sing(self):
        return 'yo... yo... microphone check... one two... one two...'

    # A class method is shared among all instances
    # They are called with the calling class as the first argument
    @classmethod
    def get_species(cls):
        return cls.species

    # A static method is called without a class or instance reference
    
    @staticmethod
    def grunt():
        return "*grunt*"

    # 只有@property表示只读。
    # 同时有@property和@x.setter表示可读可写。
    # 同时有@property和@x.setter和@x.deleter表示可读可写可删除。
    # A property is just like a getter.
    # It turns the method age() into an read-only attribute of the same name.
    # There's no need to write trivial getters and setters in Python, though.
    # Python内置的@property装饰器就是负责把一个方法变成属性调用的
    @property
    def age(self):
        return self._age
    #@property本身又创建了另一个装饰器@age.setter，负责把一个setter方法变成属性赋值
    # This allows the property to be set
    # 还可以定义只读属性，只定义getter方法，不定义setter方法就是一个只读属性：
    @age.setter
    def age(self, age):
        self._age = age

    # This allows the property to be deleted
    @age.deleter
    def age(self):
        del self._age
```
___

```python
# 不使用property的方法，比较繁琐

class Student(object):
    #实例的变量名如果以__开头，就变成了一个私有变量（private），只有内部可以访问
    #一个下划线开头的实例变量名，比如_name，这样的实例变量外部是可以访问的
    #但是，按照约定俗成的规定，意思就是，请把我视为私有变量，不要随意访问。
    #不能直接访问__name是因为Python解释器对外把__name变量改成__Student__name
    #不同版本的Python解释器可能会把__name改成不同的变量名
    def __init__(self, name, score):
        self.__name = name
        self.__score = score

    def print_score(self):
        print('%s: %s' % (self.__name, self.__score))
    #外部代码要获取name和score     
    def get_name(self):
        return self.__name

    def get_score(self):
        return self.__score
    #又要允许外部代码修改score
    def set_score(self, score):
        self.__score = score
    #在方法中，可以对参数做检查，避免传入无效的参数
    def set_score(self, score):
        if 0 <= score <= 100:
            self.__score = score
        else:
            raise ValueError('bad score')
```

```python
class C(object):
    @staticmethod
    def f(): #不强制要求传递参数
        print('runoob')
 
C.f()          # 静态方法无需实例化,为类量身定制的，但是实例非要使用，也不会报错
cobj = C()
cobj.f()        # 也可以实例化后调用

class Date:
    def __init__(self,year,month,day):
        self.year=year
        self.month=month
        self.day=day
    @staticmethod
    #如果在@staticmethod中要调用到这个类的一些属性方法，只能直接类名.属性名或类名.方法名。 
    def now(): #用Date.now()的形式去产生实例,该实例用的是当前时间
        t=time.localtime() #获取结构化的时间格式
        return Date(t.tm_year,t.tm_mon,t.tm_mday) #新建实例并且返回
    @staticmethod
    def tomorrow():#用Date.tomorrow()的形式去产生实例,该实例用的是明天的时间
        t=time.localtime(time.time()+86400)
        return Date(t.tm_year,t.tm_mon,t.tm_mday)

a=Date('1987',11,27) #自己定义时间
b=Date.now() #采用当前时间
c=Date.tomorrow() #采用明天的时间

print(a.year,a.month,a.day)
print(b.year,b.month,b.day)
print(c.year,c.month,c.day)

```

* @staticmethod 不需要访问和类相关的属性或数据；如果你定义了一个方法它的返回值永远和类的属性及实例无关，结果永远不变，就用@staticmethod
* @classmethod 可以访问和类相关（不和实例相关)的属性；如果你定义了一个方法它的返回值和只和类的属性有关，结果可变 .就用@classmethod 

```python
#使用@staticmethod或@classmethod，就可以不需要实例化，直接类名.方法名()来调用
#类方法是给类用的，类在使用时会将类本身当做参数传给类方法的第一个参数
#@classmethod因为持有cls参数，可以来调用类的属性，类的方法，实例化对象等，避免硬编码
class A(object):  
    bar = 1  
    def foo(self):  
        print 'foo'  
     
    @staticmethod  
    def static_foo():  
        print 'static_foo'  
        print A.bar  
     
    @classmethod  
    def class_foo(cls):  
        print 'class_foo'  
        print cls.bar  
        cls().foo()  
###执行  
A.static_foo()  
A.class_foo()  

```
---
When a Python interpreter reads a source file it executes all its code.
This name check makes sure this code block is only executed when this module is the main program.

``` python
if __name__ == '__main__':
```

---

* 直接赋值：其实就是对象的引用（别名）。
* 浅拷贝(copy)：拷贝父对象，不会拷贝对象的内部的子对象。
* 深拷贝(deepcopy)： copy模块的deepcopy方法，完全拷贝了父对象及其子对象。

```python
import copy
a = [1, 2, 3, 4, ['a', 'b']] #原始对象
 
b = a                       #赋值，传对象的引用
c = copy.copy(a)            #对象拷贝，浅拷贝
d = copy.deepcopy(a)        #对象拷贝，深拷贝
 
a.append(5)                 #修改对象a
a[4].append('c')            #修改对象a中的['a', 'b']数组对象
 
print( 'a = ', a )
print( 'b = ', b )
print( 'c = ', c )
print( 'd = ', d )
```
```
# 结果
('a = ', [1, 2, 3, 4, ['a', 'b', 'c'], 5])
('b = ', [1, 2, 3, 4, ['a', 'b', 'c'], 5])
('c = ', [1, 2, 3, 4, ['a', 'b', 'c']])
('d = ', [1, 2, 3, 4, ['a', 'b']])
```

---

* Python 2.x中默认都是经典类，只有显式继承了object才是新式类
* Python 3.x中默认都是新式类，不必显式的继承object
也就是说：
``` python
class Person(object):
    pass
class Person():
    pass
class Person:
    pass
```
三种写法并无区别，推荐第一种

---

新式类是采用广度优先搜索，旧式类采用深度优先搜索
```python
class A():
    def __init__(self):
        pass
    def save(self):
        print "This is from A"
class B(A):
    def __init__(self):
        pass
class C(A):
    def __init__(self):
        pass
    def save(self):
        print  "This is from C"
class D(B,C):
    def __init__(self):
        pass
fun =  D()
fun.save()
```
经典类的答案： This is from A
新式类的答案： This is from C

---
