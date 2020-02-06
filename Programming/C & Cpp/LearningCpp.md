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

---

switch 
```cpp
// when enumerations are used in a switch statement, many compilers
// issue warnings if one of the enumerators is not handled
// need to (1) add the default or (2) list each value
enum color {RED, GREEN, BLUE};
switch(RED) {
    case RED:   std::cout << "red\n"; break;
    case GREEN: std::cout << "green\n"; break;
    case BLUE:  std::cout << "blue\n"; break;
}
```

---

虚函数：
在无需了解具体子类类型的情况下，通过基类指针调用子类的实现。

Pure Virtual Member Functions：
* The =0 syntax is simply how we tell the compiler that a virtual function will be pure
* If a class doesn’t override the pure virtual function, it becomes an abstract class itself, and you can’t instantiate objects from it

```cpp
#include <iostream>
using namespace std;

// A simple Shape interface which provides a method to get the Shape's area
class Shape {
  public:
  //virtual float getArea(){}
  virtual float getArea() = 0;
};
// A Rectangle is a Shape with a specific width and height
class Rectangle : public Shape {   // derived form Shape class
  private:
  float width;
  float height;

  public:
  Rectangle(float wid, float heigh) {
    width = wid;
    height = heigh;
  }
  float getArea(){
    return width * height; 
  }
};

// A Circle is a Shape with a specific radius
class Circle : public Shape {
  private:
  float radius;

  public:
  Circle(float rad){
    radius = rad; 
  }
  float getArea(){
    return 3.14159f * radius * radius; 
  }
};

// A Square is a Shape with a specific length
class Square : public Shape {
  private:
  float length;

  public:
  Square(float len){
    length = len;
  }
  float getArea(){
    return length * length; 
  }
};

int main() {
  Shape * shape[3];   // Referencing Shape class to Rectangle object

  Rectangle r(2, 6);    // Creating Rectangle object
  shape[0] = &r;   // Referencing Shape class to Rectangle object
  
  Circle c(5);    // Creating Circle object
  shape[1] = &c;   // Referencing Shape class to Circle object

  Square s(10);   // Creating Square object
  shape[2] = &s;     // Referencing Shape class to Circle object

  for(int i=0; i<3; i++)
    cout << shape[i]->getArea() << endl; 
}
```

---

Part-of: Composition
```cpp
#include <iostream>
using namespace std;

class Engine{
  int capacity;
  
  public:
  Engine(){
    capacity = 0;
  }
  
  Engine(int cap) {
    capacity = cap;
  }
  
  void Engine_details() {
    cout << "Engine details: " << capacity << endl;
  }
};

class Tires{
  int No_of_tires;
  
  public:
  Tires(){
    No_of_tires = 0;
  }
  
  Tires(int nt) {
    No_of_tires = nt;
  }
  
  void Tire_details() {
    cout << "Number of tyres: " << No_of_tires << endl;
  }
};

class Doors{
  int No_of_doors;
  
  public:
  Doors(){
    No_of_doors = 0;
  }
  
  Doors(int nod) {
    No_of_doors = nod;
  }
  
  void Door_details() {
    cout << "Number of Doors: " << No_of_doors << endl;
  }
};

class Car{
  Engine Eobj;
  Tires Tobj;
  Doors Dobj;
  string color;
  
  public:
  Car(Engine eng, Tires tr, int dr, string col)
    : Eobj(eng), Tobj(tr), Dobj(dr){
    
    color = col;    
  }
  
  void Car_detail(){
    Eobj.Engine_details();
    Tobj.Tire_details();
    Dobj.Door_details();
    cout << "Car color: " << color << endl;
  }
};

int main(){
  Engine Eobj(1600);
  Tires Tobj(4);
  Doors Dobj(4);
  Car Cobj(Eobj, Tobj, 4, "Black");
  //When Car dies, so does tire, engine and doors too.
  Cobj.Car_detail();
}

```

 Has-A model: Aggregation

```cpp
#include <iostream>
#include <string>
using namespace std;

class Country{
  string name;
  int population;

  public:
  Country(string n, int p){
    name = n;
    population = p;
  }
  string getName(){
    return name;
  }
};

class Person {
  string name;
  Country* country; // A pointer to a Country object

  public: 
  Person(string n, Country* c){
    name = n;
    country = c;
  }

  string printDetails(){
    cout << "Name: " << name << endl;
    cout << "Country: " << country->getName() << endl;
  }
};

int main() {
  Country* country = new Country("Utopia", 1);
  {
    Person user("Darth Vader", country);
    user.printDetails();
  }
  // The user object's lifetime is over
  //the country object lives on even after the user goes out of scope
  cout << country->getName() << endl; // The country object still exists!
}

```

Association
A friend function is an ==independent function== which has access to the variables and methods of its befriended class (including private).

```cpp
class Teacher;  // Making this friend of a student class
 
class Student
{
private:
	string Std_name;
	vector<Teacher *> tr;
	void addTeacher(Teacher * teach);
 
public:
	Student(string name) {
		 Std_name = name;
	}
 
	string getName() const { 
    return Std_name; 
  }
 
  friend ostream& operator<<(ostream &out, const Student &std);
  
  // Making teacher friend of this class to access addTeacher function
	friend class Teacher;
};
 
class Teacher {
private:
	string tr_name;
	vector<Student *> stdnt;
 
public:
	Teacher (string name) {
		tr_name = name;
	}
 
	void addStudent(Student *st)
	{
		// Teacher will add this student to course
		stdnt.push_back(st);
		
		// Student will also add this teacher for connection
		st->addTeacher(this);
	}
  
  friend ostream& operator<<(ostream &out, const Teacher &tchr);
 
	string getName() const {return tr_name;}
};
 
void Student::addTeacher(Teacher *teach){
	tr.push_back(teach);
}
 
ostream& operator<<(ostream &out, const Student &std) {
	int length = std.tr.size();
	if (length == 0)
	{
		out << std.getName() << " is not registered in any course";
		return out;
	}
 
	out << std.Std_name << " is taught by: ";
	for (int count = 0; count < length; ++count)
		out << std.tr[count]->getName() << ' ';
 
	return out;
}


ostream& operator<<(ostream &out, const Teacher &tchr)
	{
		int length = tchr.stdnt.size();
		if (length == 0)
		{
			out << tchr.tr_name << " is not teaching any class";
			return out;
		}
 
		out << tchr.tr_name << " is teaching: ";
		for (int count = 0; count < length; ++count)
			 out << tchr.stdnt[count]->getName() << ' ';
 
		return out;
	}
 

int main()
{
	// Creating a Students outside the scope of the Teacher
	Student *s1 = new Student("John");
	Student *s2 = new Student("Stacy");
	Student *s3 = new Student("Sarah");
 
	Teacher *t1 = new Teacher("Henry");
	Teacher *t2 = new Teacher("Neil");
  Teacher *t3 = new Teacher("Steve");

	t1->addStudent(s1);
	t2->addStudent(s1);
	t1->addStudent(s3);
 
	cout << *t1 << endl;
	cout << *t2 << endl;
  cout << *t3 << endl;
	cout << *s1 << endl;
	cout << *s2 << endl;
	cout << *s3 << endl;
}
```

---

```cpp
template <class T>
class Score
{
private:
    T value;
public:
    static int counter;
    Score()  {counter++;}
};
 
template<class T>
int Score<T>::counter = 0;
 
int main()
{
    Score<int> x;
    Score<int> y;
    Score<double> z;
    cout << Score<int>::counter<< endl;
    cout << Score<double>::counter<< endl;
    return 0;
}
```

1、const：类型常量与指针常量

const int 等价于 int const 但不等价于int *const；前两个是类型常量，后一个是指针常量。

2、模板

函数模板：

template <class type> ret-type func-name(parameter list){ // 函数的主体}

类模板：

template <class type> class class-name {...}

模板用于自由类型编程，目的是通用算法与具体类型无关。

3、注释小技巧

//*

注释内容

//*/

通常注释内容由/**/包括起来。在*/前增加两个/后，不改变注释；此后，在/*前增加一个/变为//*，此时原注释首行与尾行都变为单行注释，如此即可方便打开注释内容进行重用。如果要恢复原来的注释，可再次删除首行中的一个/，即又可快速恢复原注释。

4、inline

内联是以代码膨胀（复制）为代价，仅仅省去了函数调用的开销，从而提高函数的

执行效率。

