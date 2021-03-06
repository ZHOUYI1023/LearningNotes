Python是一种解释型语言，比编译型语言运行慢。
以字节编译，生成一种近似机器语言的中间形式。

---

小心命名冲突：module（文件名），类，函数，变量

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

整数在程序中的使用非常广泛，Python为了优化速度，使用了小整数对象池， 避免为整数频繁申请和销毁内存空间。
Python 对小整数的定义是 [-5, 256] 这些整数对象是提前建立好的，不会被垃圾回收。

---

浮点算术：争议和限制
浮点数在计算机硬件中表示为以 2 为基数（二进制）的小数。
大多数的十进制小数都不能精确地表示为二进制小数。这导致在大多数情况下，你输入的十进制浮点数都只能近似地以二进制浮点数形式储存在计算机中。
在以 2 为基数的情况下， 1/10 是一个无限循环小数
0.0001100110011001100110011001100110011001100110011...
因此，在今天的大部分架构上，浮点数都只能近似地使用二进制小数表示，对应分数的分子使用每 8 字节的前 53 位表示，分母则表示为 2 的幂次。
一旦要做精确计算，那么就不应该再单独使用浮点数，而是应该总是使用Decimal('浮点数')。（或者直接上numpy）否则，当你赋值的时候，精度已经被丢失了。
``` python
from decimal import Decimal
a = Decimal('0.1')
b = Decimal('0.2')
c = a + b
print(c)
```

---

eval()对表达式求值，后者可为字符串或内建函数compile()创建的预编译代码对象
``` python
eval('932')
eval('100 + 200') # int('100 + 200') ValueError
```
exec(obj)

``` python
program = 'a = 5\nb=10\nprint("Sum =", a+b)'
exec(program)

program = input('Enter a program:')
exec(program)
```

---

```python
# old school %-formatting
"Hello, %s. You are %s." % (name, age)

# str.format()
"Hello, {}. You are {}.".format(name, age)
# reference variables in any order by referencing their index
"Hello, {1}. You are {0}.".format(age, name)
"Hello, {name}, you are {age}".format(name = name,age = age)
# print dictionary
person = {'name': 'Eric', 'age': 74}
"Hello, {name}. You are {age}.".format(**person)

# f-string
# f-strings are evaluated at runtime
f"Hello, {name}. You are {age}."
f"{2 * 37}"
f"{name.lower()} is funny."
message = f"Hi {name}. " \
...       f"You are a {profession}. " \
...       f"You were in {affiliation}."

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

 闭包: 如果在一个内部函数里，对在外部作用域（但是不在全局作用域）的变量进行引用，那么内部函数就被认为是闭包。
 定义在外部函数内的但由内部函数引用或者使用的变量被称为自由变量。
``` python {highlight=20}
# nested function
def print_msg():
    # print_msg 是外围函数
    msg = "zen of python"

    def printer():
        # printer是嵌套函数
        print(msg)
    printer()
# 输出 zen of python
print_msg()

# Closure 
def another():
    # print_msg 是外围函数
    msg = "zen of python"
    def printer():
        # printer 是嵌套函数
        print(msg)
    return printer

another = print_msg()
# 输出 zen of python
another()()

```
闭包避免了使用全局变量，此外，闭包允许将函数与其所操作的某些数据（环境）关连起来。

``` python
def adder(x):
    def wrapper(y):
        return x + y
    return wrapper

adder5 = adder(5)
# 输出 15
adder5(10)
# 输出 11
adder5(6)

>>> adder5.__closure__
(<cell at 0x103075910: int object at 0x7fd251604518>,)
>>> adder5.__closure__[0].cell_contents
5
```
所有函数都有一个 __closure__属性，如果这个函数是一个闭包的话，那么它返回的是一个由 cell 对象 组成的元组对象。cell 对象的cell_contents 属性就是闭包中的自由变量。

---

nonlocal variable

``` python
def outer():
    x = "local"
    
    def inner():
        nonlocal x
        x = "nonlocal"
        print("inner:", x)
    
    inner()
    print("outer:", x)

outer()
# inner:nonlocal
# outer:nonlocal
```

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

* 不可变对象
不可变对象是指对象的内存值不能被改变。数值类型（整数和浮点）、字符串str、元组tuple都是不可型。比如a=1，b=[1]，c={'a':1}，id(a)、id(b[0])、id(1id(c['a'])将输出一样的值，因为1是不可变对象，其在内存不可改变的。

* 可变对象
可变对象是指对象的内存值可以被改变，列list、字典dict、集合set是可变类型。可变对象值的方法是没有返回值的。

* 对象的内存地址
可以使用内置函数id()查看python对象的内存地址。

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

---

locals()的作用是：返回一个字典——这个字典包含该语句所在代码块的局部变量和局部模块。更为准确的说，返回local namespace中的所有东西。

globals()具有相同的作用：返回global namespace中的所有东西（全局变量，全局模块）。
```python
print locals()
print globals()
```

---

Super Function

Inheritance public properties and methods without calling \__init\__
```python
class Vehicle: #defining the parent class
  def display(self): #defining diplay method in the parent class
    print("I am from the Vehicle Class")

class Car(Vehicle): #defining the child class
  #defining diplay method in the parent class
  def display(self): 
    super().display()
    print("I am from the Car Class")

obj1 = Car() #creating a car object
obj1.display() #calling the Car class method printOut()

```
Using with Initializers 
``` python
class Vehicle:
  def __init__(self, make, color, model):
    self.make = make
    self.color = color
    self.model = model
  
  def printDetails(self):
    print("Manufacturer:" , self.make)
    print("Color:" , self.color)
    print("Model:" , self.model)

class Car(Vehicle):
  def __init__(self, make, color, model, doors):
    # Vehicle.__init__(self, make, color, model)
    super().__init__(make, color, model)
    self.doors = doors
        
  def printCarDetails(self): 
    # self.printDetails()   
    super().printDetails()
    print("Name:",self.doors)
    

obj1 = Car("Suzuki","Grey","2015",4) 
obj1.printCarDetails()  
```

---

Python中没有禁止访问类中某一成员的保护机制。
Python通过编码规范而不是语言机制来完成封装，具体而言，Python规定了对变量命名的公约，约定什么样的变量名表示变量是私有的，不应该被访问(而不是不能被访问)。


私有化

* 单下划线
以单个下划线开头的变量或方法应被视为非公开的API
外部的调用者也不应该去访问以单下划线开头的变量或方法

* 双下划线
名称转写(name mangling)：以双下划线开头，并以最多一个下划线结尾的标识符，例如__X，会被转写为_classname__X，其中classname为类名。
进行名称转写则能有效避免子类中方法的命名冲突
定义子类的时候，经常会调用父类的__init__()方法，假如父类的__init__()方法调用了父类的非公开函数__initialize()，当我们在子类中也需要__initialize()函数时会造成父类__init__()的异常行为，而名称转写避免了这一冲突，父类的__init__()实际上调用的是_父类名__initialize()。

Use one leading underscore only for non-public methods and instance variables.

_single_leading_underscore: weak "internal use" indicator. E.g. from M import * does not import objects whose name starts with an underscore.

To avoid name clashes with subclasses, use two leading underscores to invoke Python's name mangling rules.

It should not be used to create a private method. It should be used to avoid your method being overridden by a subclass or accessed accidentally.

Generally, double leading underscores should be used only to avoid name conflicts with attributes in classes designed to be subclassed.

``` python
class A(object):
    def __test(self):
        print "I'm a test method in class A"

    def test(self):
        self.__test()

a = A()
a.test()
# a.__test() # This fails with an AttributeError
a._A__test() # Works! We can access the mangled name directly!

class B(A):
    def __test(self):
        print "I'm test method in class B"

b = B()
b.test()# A.test() will not call B.__test() methods

```

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

if you want to change a class attribute, you have to do it with the notation ClassName.AttributeName. Otherwise, you will create a new instance variable. 

Python's class attributes and object attributes are stored in separate dictionaries__dict__

``` python
class A:
    foo = 'b'
    bar = []

a = A()
b = A()
a.__dict__ # {}

# add instance variable
a.foo = 'c'
A.foo # 'b'
a.foo # 'c'
a.__dict__ # {'foo': 'c'}

# modify class variable from instance
a.bar.append(1)
b.bar # [1]
a.bar # [1]
a.__dict__ # {'foo': 'c'}
b.__dict__ # {}

# overwrite class variable by instance variable
b.bar = 1
b.__dict__ #{'bar': 1}

```
The proper use of \__slots__ is to save space in objects. Instead of having a dynamic dict that allows adding attributes to objects at anytime, there is a static structure which does not allow additions after creation. [This use of \__slots__ eliminates the overhead of one dict for every object.] While this is sometimes a useful optimization, it would be completely unnecessary if the Python interpreter was dynamic enough so that it would only require the dict when there actually were additions to the object.

```python
class A:
    __slots__ = ['x', 'y'] 
a = A()
a.x = 1
a.z = 2 # AttributeError
a.__dict__ # AttributeError

```

---

\__all__ lets humans know the "public" features of a module(.py)
only affect from xxx import *
If \__all__ is not defined, the set of public names includes all names found in the module's namespace which do not begin with an underscore character ("_"). \__all__ should contain the entire public API. 
It is intended to avoid accidentally exporting items that are not part of the API
``` python
""" cheese.py - an example module """

__all__ = ['swiss', 'cheddar']

swiss = 4.99
cheddar = 3.99
gouda = 10.99

```

``` python
>>> from cheese import *
>>> swiss, cheddar
(4.99, 3.99)
>>> gouda
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'gouda' is not defined
```

``` python
>>> import cheese
>>> cheese.swiss, cheese.cheddar, cheese.gouda
(4.99, 3.99, 10.99)
```

if a package’s \__init__.py code defines a list named \__all__, it is taken to be the list of module names that should be imported when from package import * is encountered.
``` python
""" sound/effects/__init__.py """
__all__ = ["echo", "surround", "reverse"]
```

``` python
from sound.effects import * 
# import the three named submodules of the sound package.
```

not affect from package import specific_submodule



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
 
a[0] = 0 
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

``` python
import copy
z = 1
def adder(x):
    global z
    q = copy.copy(z)
    def wrapper(y):
        return x + y + q
    return wrapper

t1 = adder(1)
print(t1(1))
# 3
z = 3
t2 = adder(1)
print(t1(1), t2(1))
# 3 5
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
三种写法并无区别


```python
# 旧式类
>>> class Foo:
...     pass
...
>>> x = Foo()
>>> x.__class__
<class __main__.Foo at 0x000000000535CC48>
>>> type(x)
<type 'instance'>
```

In Python 3 it is reasonable to refer to an object’s type and its class interchangeably.
``` python
# 新式类
>>> n = 5
>>> d = { 'x' : 1, 'y' : 2 }

>>> class Foo:
...     pass
...
>>> x = Foo()

>>> for obj in (n, d, x):
...     print(type(obj) is obj.__class__)
...
True
True
True
```

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

Remember that, in Python, everything is an object. Classes are objects as well. In general, the type of any new-style class is type.
```python

>>> for t in int, float, dict, list, tuple:
...     print(type(t))
...
<class 'type'>
<class 'type'>
<class 'type'>
<class 'type'>
<class 'type'>

# type is a metaclass, of which classes are instances. 
>>> type(type)
<class 'type'>

```


---

## 跳出多重循环
``` python
# use else in for loop
# 循环体的else分支触发条件是循环正常结束。
# 如果循环内break了，不触发else，则执行下一句外层循环中的break
# 如果正常结束，执行else分支里的continue，直接跳转到外层循环的下一轮，跳过了第二个break。
for i in range(1,100):
    for j in range(1,100):
       break
    else:
       continue
    break
# use flag
exitFlag = False
for i in range(1,100):
    for j in range(1,100):
        exitFlag = True
        break
    if exitFlag:
        break
```

---

Overloading Operator 
```python
class com: 
  def __init__(self, real = 0, imag = 0):
    self.real = real
    self.imag = imag
    
  def __add__(self, other): #overloading the `+` operator
    temp = com(self.real + other.real, self.imag+other.imag)
    return temp
    
  def __sub__(self,other): #overloading the `-` operator
    temp = com(self.real - other.real, self.imag - other.imag)
    return temp

obj1 = com(3, 7)
obj2 = com(2, 5)

obj3 = obj1 + obj2
obj4 = obj1 - obj2

```

---

Duck Typing

To achieve polymorphism without inheritance
开闭原则：
Software entities should be open for extension, but closed for modification.
在设计一个模块的时候，应当使这个模块可以在不被修改的前提下被扩展。


```python
class Dog:
  def Speak(self):
    print("Woof woof")

class Cat:
  def Speak(self):
    print("Meow meow") 

class AnimalSound:
  def Sound(self,animal):
    animal.Speak()
# animal object does not matter in the definition of the Sound method 
# as long as it has the associated behavior speak()

sound = AnimalSound()
dog = Dog()
cat = Cat()

sound.Sound(dog)
sound.Sound(cat) 

```

``` python
class Duck:
    def fly(self):
        print("Duck flying")

class Airplane:
    def fly(self):
        print("Airplane flying")

class Whale:
    def swim(self):
        print("Whale swimming")

for animal in Duck(), Airplane(), Whale():
    animal.fly()

# Duck flying
# Airplane flying
# AttributeError: 'Whale' object has no attribute 'fly'

```

Abstract base classes define a set of methods and properties that a class must implement in order to be considered a duck-type instance of that class.

Abstract methods must be defined in child classes for proper implementation of inheritance.

``` python
from abc import ABC, abstractmethod

class Shape(ABC): #Shape is a child class of ABC
  @abstractmethod
  def area(self):
    pass
  
  @abstractmethod
  def perimeter(self):
    pass

class Square(Shape):
  def __init__(self, length):
    self.length = length

shape=Shape()
# this will code will not compile 
# since Shape has abstract methods without method definitions in it

square = Square(4)
# this will code will not compile 
# since abstarct methods have not been defined in the child class, Square

```

---

Aggregation
```python

class Country:
  def __init__(self, name = None, population = 0):
    self.name = name
    self.population = population
  
  def printDetails(self):
    print ("Country Name:",  self.name)
    print ("Country Population",  self.population)
  
class Person:
  def __init__(self, name, country):
    self.name = name
    self.country = country
  
  def printDetails(self):
    print("Person Name:", self.name)
    self.country.printDetails()

c = Country("Wales", 1500)
p = Person("Joe", c)
p.printDetails()

del c 
print("")
p.printDetails()

```


Composition
```python
class Engine:
  def __init__(self,capacity=0):
    self.capacity=capacity
  
  def printDetails(self):
    print("Engine Details:",self.capacity)

class Tires:
  def __init__(self,tires=0):
    self.tires=tires
  
  def printDetails(self):
    print("Number of tires:",self.tires)

class Doors:
  def __init__(self,doors=0):
    self.doors=doors
  
  def printDetails(self):
    print("Number of doors:",self.doors)

class Car:
  def __init__(self,eng,tr,dr,color):
    self.eObj=Engine(eng)
    self.tObj=Tires(tr)
    self.dObj=Doors(dr)
    self.color=color
  
  def printDetails(self):
    self.eObj.printDetails()
    self.tObj.printDetails()
    self.dObj.printDetails()
    print("Car color:",self.color)

car=Car(1600,4,2,"Grey")
car.printDetails()
```

---

python中的文件都会生成pyc文件，包括模块也是这样，所以调用模块的时候，实际上会调用模块.pyc文件；在这个前提下，如果将文件名命名成跟模块名一样，在同一目录下就会生成一个跟模块名一样的pyc文件，系统就直接调用这个文件了，所以就会出现模块中属性错误，如AttributeError: 'module' object has no attribute 'Differ'


---

``` python
# file handling 

# 1) without using with statement 
# An exception during the file.write() call in the first implementation can prevent the file from closing properly
file = open('file_path', 'w') 
file.write('hello world !') 
file.close() 

# 2) without using with statement 
file = open('file_path', 'w') 
try: 
	file.write('hello world') 
finally: 
	file.close() 

# using with statement 
# there is no need to call file.close() when using with statement.
with open('file_path', 'w') as file: 
	file.write('hello world !') 

```
 The name xfile here is used to refer to the file descriptor returned by the \__enter__() method.
As soon as the code inside the with block is executed, the \__exit__() method is called.
``` python
# a simple file writer object 

class MessageWriter(object): 
	def __init__(self, file_name): 
		self.file_name = file_name 
	
	def __enter__(self): 
		self.file = open(self.file_name, 'w') 
		return self.file

	def __exit__(self): 
		self.file.close() 

# using with statement with MessageWriter 

with MessageWriter('my_file.txt') as xfile: 
	xfile.write('hello world') 

```

``` python
from contextlib import contextmanager 
  
class MessageWriter(object): 
    def __init__(self, filename): 
        self.file_name = filename 
  
    @contextmanager
    def open_file(self): 
        try: 
            file = open(self.file_name, 'w') 
            yield file
        finally: 
            file.close() 
  
# usage 
message_writer = MessageWriter('hello.txt') 
with message_writer.open_file() as my_file: 
    my_file.write('hello world') 

```

---

``` python
import json

data = {}
data['people'] = []
data['people'].append({
    'name': 'Scott',
    'website': 'stackabuse.com',
    'from': 'Nebraska'
})
data['people'].append({
    'name': 'Larry',
    'website': 'google.com',
    'from': 'Michigan'
})
data['people'].append({
    'name': 'Tim',
    'website': 'apple.com',
    'from': 'Alabama'
})

with open('data.txt', 'w') as outfile:
    json.dump(data, outfile)

with open('data.txt') as json_file:
    data = json.load(json_file)
    for p in data['people']:
        print('Name: ' + p['name'])
        print('Website: ' + p['website'])
        print('From: ' + p['from'])
        print('')

json.dumps(data, sort_keys=True, indent=4)
    
```