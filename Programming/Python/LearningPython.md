单个*, 如：*parameter是用来接受任意多个参数并将其放在一个元组中。
``` python
def demo(*p):
    print(p)
```
``` python
a, *b, c = (1, 2, 3, 4)  # a is now 1, b is now [2, 3] and c is now 4
```
两个**, 如:**parameter用于接收类似于关键参数一样赋值的形式的多个实参放入字典中（即把该函数的参数转换为字典）。
```python
def demo(**p):
# p is a dictionary
    for i in p.items():
        print(i)

demo(x=1, y=2)
('x', 1)
('y', 2)
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
