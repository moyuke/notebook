---
title: OOP Homework
date: 2023-05-30
tags: class

---

## W1

（ ）不是面向对象程序设计的主要特征。

A.封装

B.继承

C.多态

**D.结构**



关于C++与C 语言关系的描述中，（ ）是错误的。

A.C 语言是C++语言的一个子集

B.C 语言与C++语言是兼容的

C.C++语言对C 语言进行了一些改进

**D.C++语言和C 语言都是面向对象的**



下列关于cin和cout的说法中，错误的是____。

A.cin用于读入用户输入的数据

B.cout用于输出数据

**C.cin比C语言中的scanf()函数更有优势，它可以读取空格**

D.cout通常与<<运算符结合



关于delete运算符的下列描述中，（）是错误的。

A.它必须用于new返回的指针；

B.使用它删除对象时要调用析构函数；

**C.对一个指针可以使用多次该运算符；**

D.指针名前只有一对方括号符号，不管所删除数组的维数。



以下程序中，new语句干了什么。

int** num;

num = new int* [20];

A.分配了长度为20的整数数组空间，并将首元素的指针返回。

B.分配了一个整数变量的空间，并将其初始化为20。

**C.分配了长度为20的整数指针数组空间，并将num[0]的指针返回。**

D.存在错误，编译不能通过。



以下程序存在的问题是：

```c++
void fun()
{
 int *num1, *num2;
 num1 = new int[10];
 num2 = new int[20];
 num1[0] = 100;
 num2[0] = 300;
 num1 = num2;
 delete [] num1;
}
```

A.num2不能给num1赋值

B.num2最初指向的空间没有释放

**C.num1最初指向的空间没有释放**

D.程序没有问题



关于new 和 delete 关键字功能的叙述，不正确的是（ ）

A.C++程序的内存空间，可以分为代码区(text segment）、静态存储区(Data Segment)、栈区(Stack)、堆区(Heap)。new关键字用于从堆区中动态申请创建对象所需的内存空间。

B.new动态申请内存空间成功后，返回该内存区域的首地址；同时，也会自动调用相关类的构造函数。

C.delete用于删除new建立的对象，并释放指针所指向的内存空间，同时，也会自动调用对象的析构函数。

**D.B * ptr=new B(5)；delete ptr; 假设上述语句中，new申请的内存空间首地址为Addr,存放ptr指针变量值的内存空间首地址为 PAddr，则执行delete ptr 语句后，Addr、PAddr指向的内存区域均会被系统收回。**



用new关键字动态申请一个三维数组，则下列语句正确的是（ ）

A.`float *fp; fp= new float[10][25][10];`

**B.`float (* fp)[25][10]; fp=new float[10][25][10];`**

C.`float (* fp)[10]; fp=new float[10][25][10];`

D.`float *fp [25][10]; fp= new float[10][25][10];`



下列语句中，不能连续输出3个值的是。

A.cout<<x<<y<<z;

**B.cout<<x,y,z;**

C.cout<<x; cout<<y; cout<<z;

D.cout<<(x,y,z)<<(x,y,z)<<(x,y,z);



在C++中，cin是（）。

A.预定义的类

B.预定义的函数

C.一个标准的语句

**D.预定义的对象**

------

## W2

假定AA为一个类，a()为该类公有的函数成员，x为该类的一个对象，则访问x对象中函数成员a()的格式为（）

A.x.a

**B.x.a()**

C.x->a()

D.(*x).a()



下列关于类定义的说法中，正确的是

**A.类定义中包括数据成员和函数成员的声明**

B.类成员的缺省访问权限是保护的

C.数据成员必须被声明为私有的

D.成员函数只能在类体外进行定义



下列关于类和对象的叙述中，错误的是

**A.一个类只能有一个对象**

B.对象是类的具体实例

C.类是对某一类对象的抽象

D.类和对象的关系是一种数据类型与变量的关系



Resolver `::` is used to:

A.Define a member function outside class declaration

B.Access a member of a namespace

C.Access a static member of a class

**D.All of the others**



类的实例化是指（ ）。

A.定义类

**B.定义对象**

C.调用类的成员函数

D.访问对象的数据成员



C＋＋函数的声明和定义可以分开。函数声明不需要( )。

A.返回类型

B.函数名

C.参数表

**D.函数体**



首先需要在问题域中识别出若干个（ ）

A.函数

**B.类**

C.文件

D.过程

---

## W3

---

## W4

若有下面的语句：

```C++
vector<int> v;
for (int i = 0; i < 4; i++)
    v.push_back(i + 1);
cout << v.size() << endl;
```

则执行后程序的输出结果是

A.1

B.2

C.3

**D.4**



设有定义 `vector<string> v(10);`
执行下列哪条语句时会调用构造函数?

A.

```
v[0] += "abc";
```

B.

```
v[0] = "2018";
```

**C.**

```
v.push_back("ZUCC");
```

D.

```
cout << (v[1] == "def");
```



设有如下代码段:

```
std::map<char *, int> m;
const int MAX_SIZE = 100;
int main() {
    char str[MAX_SIZE];
    for (int i = 0; i < 10; i++) {
        std::cin >> str;
        m[str] = i;
    }
    std::cout << m.size() << std::endl;
}
```

读入10个字符串，则输出的 `m.size()` 为

A.0

**B.1**

C.10



下列关于STL的描述中，错误的是。

A.STL的内容从广义上讲分为容器、迭代器、算法三个主要部分

B.STL的一个基本理念就是将数据和操作分离

C.STL中的所有组件都由模板构成，其元素可以是任意类型

**D.STL的容器、迭代器、算法是三个完全独立的部分，彼此也无任何联系**



下列创建vector容器对象的方法中，错误的是。

A.

```
vector<int> v(10);
```

B.

```
vector<int> v(10, 1);
```

C.

```
vector<int> v{10, 1};
```

**D.**

```
vector<int> v = (10, 1);
```



下列选项中，哪一项不是迭代器。

A.输入迭代器

B.前向迭代器

C.双向迭代器

**D.删除迭代器**



设void f1(int * m，long & n)；int a；long b；则以下调用合法的是（）。

A.f1(a，b)；

**B.f1(&a，b)；**

C.f1(a，&b)；

D.f1(&a，&b)；



下面程序片段,哪一个是正确的?

A.int n=4; int &r=n*3;

B.int m=5; const int &r=m; r=6;

C.int n=8; const int &p=n; int &q=p ;

**D.int n=8; int &p=n; const int q=p ;**



下面程序段 int a=1,b=2; int &r=a; r=b; r=7; cout<<a<<endl; 的输出结果是?

A.1

B.2

**C.7**

D.无法确定



已知：float b = 34.5； ，则下列表示引用的方法中，正确的是（ ）。

**A.float &x = b；**

B.float &y = 34.5；

C.float &z；

D.int &t = &b;

---

## W5

在C++语言中引入内联函数（inline function）的主要目的是降低空间复杂度，即缩短目标代码长度。

T

**F**



主程序调用内联函数（inline）时，不发生控制转移，无需保存和恢复环境变量等，因此，节省了系统开销。内联函数的声明以及最终的生效，是由程序员决定的。

T

**F**



int Sum (int a,int b=5,int c); 这个函数原型的声明没有什么不合适的地方。

T

**F**



两个以上的函数，具有相同的函数名，且形参的个数或形参的类型不同，或返回的数据类型不同，则称之为函数的重载。

T

**F**



带有默认值的函数F的函数原型为F(int x=5, int x=9, int y, float m=10.0)，则该函数在编译时会报错。

**T**

F



如果默认参数的函数声明为“ void fun(int a,int b=1,char c='a',float d=3.2);”，
则下面调用写法正确的是（ ）。

A.fun();

**B.fun(2,3);**

C.fun(2, ,'c',3.14)

D.fun(int a=1);



重载函数在调用时选择的依据中，错误的是（）。

**A.函数的参数**

B.参数的类型

C.函数的名字

D.函数的类型



在（ ）情况下适宜采用inline定义内联函数。

A.函数体含有循环语句

B.函数体含有递归语句

**C.函数代码少、频繁调用**

D.函数代码多、不常调用



在C++中，关于下列设置缺省参数值的描述中，（）是正确的。

A.不允许设置缺省参数值；

**B.在指定了缺省值的参数右边，不能出现没有指定缺省值的参数；**

C.只能在函数的定义性声明中指定参数的缺省值；

D.设置缺省参数值时，必须全部都设置；



下面说法正确的是（）。

A.内联函数在运行时是将该函数的目标代码插入每个调用该函数的地方

**B.内联函数在编译时是将该函数的目标代码插入每个调用该函数的地方**

C.类的内联函数必须在类体内定义

D.类的内联函数必须在类体外通过加关键字inline定义



对定义重载函数的下列要求中，（ ）是错误的。

A.要求参数的个数不同

B.要求参数中至少有一个类型不同

**C.要求函数的返回值不同**

D.要求参数个数相同时，参数类型不同



当一个函数功能不太复杂，但要求被频繁调用时，选用____。

A.重载函数

**B.内联函数**

C.递归函数

D.嵌套函数



如有函数定义：void func(int x = 0, int y = 0){ …. }，则下列函数调用中会出现问题的是____。

**A.func(1,2, 3);**

B.func(1,2);

C.func(1);

D.func();



以下有关函数的叙述中正确的是（ ）。

A.函数必须返回一个值

B.函数体中必须有return语句

**C.两个同名函数，参数表相同而返回值不同不算重载**

D.函数执行中形参的改变会改变实参



以下选项中，是正确的函数默认形参设置的是。

A.int fun(int a,int b,int c);

**B.int fun(int a,int b,int c=1);**

C.int fun(int a,int b=1,int c);

D.int fun(int a=1,int b,int c);

------

## W6

Order of initialization in the initial list is the order of their declaration in the list.

T

**F**



类的组合关系可以用“Has-A”描述；类间的继承与派生关系可以用“Is-A”描述。

**T**

F



一个类的友元函数是这个类的成员。

T

**F**



在C++语言中引入内联函数（inline function）的主要目的是降低空间复杂度，即缩短目标代码长度。

T

**F**



主程序调用内联函数（inline）时，不发生控制转移，无需保存和恢复环境变量等，因此，节省了系统开销。内联函数的声明以及最终的生效，是由程序员决定的。

T

**F**



一个函数功能不太复杂，但要求被频繁调用，可选用（ ）。

**A.内联函数**

B.重载函数

C.递归函数

D.嵌套函数



在（ ）情况下适宜采用inline定义内联函数。

A.函数体含有循环语句

B.函数体含有递归语句

**C.函数代码少、频繁调用**

D.函数代码多、不常调用



下面说法正确的是（）。

A.内联函数在运行时是将该函数的目标代码插入每个调用该函数的地方

**B.内联函数在编译时是将该函数的目标代码插入每个调用该函数的地方**

C.类的内联函数必须在类体内定义

D.类的内联函数必须在类体外通过加关键字inline定义



如果默认参数的函数声明为“ void fun(int a,int b=1,char c='a',float d=3.2);”，
则下面调用写法正确的是（ ）。

A.fun();

**B.fun(2,3);**

C.fun(2, ,'c',3.14)

D.fun(int a=1);



在C++中，关于下列设置缺省参数值的描述中，（）是正确的。

A.不允许设置缺省参数值；

**B.在指定了缺省值的参数右边，不能出现没有指定缺省值的参数；**

C.只能在函数的定义性声明中指定参数的缺省值；

D.设置缺省参数值时，必须全部都设置；



决定C++语言中函数的返回值类型的是（）

A.return语句中的表达式类型

B.调用该函数时系统随机产生的类型

C.调用该函数时的主调用函数类型

**D.在定义该函数时所指定的数据类型**



如有函数定义：void func(int x = 0, int y = 0){ …. }，则下列函数调用中会出现问题的是____。

**A.func(1,2, 3);**

B.func(1,2);

C.func(1);

D.func();



以下选项中，是正确的函数默认形参设置的是。

A.int fun(int a,int b,int c);

**B.int fun(int a,int b,int c=1);**

C.int fun(int a,int b=1,int c);

D.int fun(int a=1,int b,int c);



对于以下关于友元的说法

A.如果函数fun被声明为类A的友元函数，则该函数成为A的成员函数

B.如果函数fun被声明为类A的友元函数，则该函数能访问A的保护成员，但不能访问私有成员

C.如果函数fun被声明为类A的友元函数，则fun的形参类型不能是A。

**D.以上答案都不对**



对于类之间的友元关系：

A.如果类A是类B的友元，则B的成员函数可以访问A的私有成员

B.如果类A是类B的友元，则B也是A的友元。

C.如果类A是类B的友元，并且类B是类C的友元，则类A也是类C的友元。

**D.以上答案都不对。**



友元的作用是

**A.提高程序的运用效率**

B.加强类的封装性

C.实现数据的隐藏性

D.增加成员函数的种类



下面关于友元的描述中，错误的是：

A.友元函数可以访问该类的私有数据成员

B.一个类的友元类中的成员函数都是这个类的友元函数

C.友元可以提高程序的运行效率

**D.类与类之间的友元关系可以继承**



已知类A是类B的友元，类B是类C的友元，则：

A.类A一定是类C的友元

B.类C一定是类A的友元

C.类C的成员函数可以访问类B的对象的任何成员

**D.类A的成员函数可以访问类B的对象的任何成员**



不属于类的成员函数的是（ ） 。

A.构造函数

B.析构函数

**C.友元函数**

D.复制构造函数



若类A被说明成类B的友元，则（ ） 。

A.类A的成员即类B的成员

B.类B的成员即类A的成员

C.类A的成员函数不能访问类B的成员

**D.类B不一定是类A的友元**



在下列关键字中,用以说明类中公有成员的是（ ）。

**A.public**

B.private

C.protected

D.friend



Suppose a class is defined without any keywords such as public, private and protected，all members default to

A.public

B.protected

**C.private**

D.static



Who can access a private member of a class?

A.Only member functions of that class.

**B.Only member functions of that class and friend functions or member functions of friend classes**

C.Only member functions of that class and derived classes

D.None of the others



静态成员函数没有：

A.返回值

**B.this指针**

C.指针参数

D.返回类型



For the code below:

```
class A {
  static int i;
  //...
};
```

Which statement is NOT true?

**A.All objects of class A reserve a space for i**

B.All objects of class A share the space of i

C.i is a member variable of class A

D.i is allocated in global data space

---

## W7

In C++, inheritance allows a derived class to directly access all of the functions and data of its base class.

T

**F**



One class can have more than one super classes.

**T**

F



write the output of the code below.

1.the output at //1 is `1`

2.the output at //2 is `2`

3.the output at //3 is `7`

4.the output at //4 is `0`

5.the output at //5 is `0`

```c++
#include <iostream>
#include <string>
using namespace std ;

class Testing
{
private:
    string words; 
    int number ;
public:
    Testing(const string & s = "Testing")
    {
        words = s ;
        number = words.length();
        if (words.compare("Testing")==0)
            cout << 1;
        else if (words.compare("Heap1")==0)
            cout << 2;
        else
            cout << 3;
    }
    ~Testing()
    {
        cout << 0;
    }
    void show() const
    {
        cout << number;
    }
};
int main()
{
    Testing *pc1 , *pc2;
    pc1 = new Testing ;          //1
    pc2 = new Testing("Heap1");  //2
    pc1->show();   //3
    delete pc1 ;   //4
    delete pc2 ;   //5
    return 0;
}
```



For the code segment below, in the main(),

1. the output at //1 is `114`
2. the output at //2 is `303062`
3. the output at //3 is `115`
4. the output at //4 is `303062`

```c++
class A{
    int i;
public:
    A(int ii=0):i(ii) { cout << 1; }
    A(const A& a) {
        i = a.i;
        cout << 2;     
    }
    void print() const { cout << 3 << i; }
};

class B : public A {
    int i;
    A a;
public:
    B(int ii = 0) : i(ii) { cout << 4; }
    B(const B& b) {
        i = b.i;
        cout << 5;
    }
    void print() const {
        A::print();
        a.print();
        cout << 6 << i;    
    }
};

int main()
{
    B b(2);        //1
    b.print();    //2
    B c(b);        //3
    c.print();    //4
}
```

---

## W8

虚函数是用virtual 关键字说明的成员函数。

**T**

F



将构造函数说明为纯虚函数是没有意义的。

**T**

F



抽象类是指一些没有说明对象的类。

T

**F**



动态绑定是在运行时选定调用的成员函数的。

**T**

F



因为静态成员函数不能是虚函数，所以它们不能实现多态。

**T**

F



在多继承中，派生类的构造函数需要依次调用其基类的构造函数，调用顺序取决于定义派生类时所指定的各基类的顺序。

**T**

F



类的组合关系可以用“Has-A”描述；类间的继承与派生关系可以用“Is-A”描述。

**T**

F



虚函数具有继承性。

**T**

F



静态成员函数可以声明为虚函数。

T

**F**



如果一个类的函数全部都是纯虚函数，则这个类不能有自己类的实现（包括引用和指针），只能通过派生类继承实现。

T

**F**



Which one is the characteristic of abstract class?

A.May have virtual functions

B.May have constructors overloaded

C.May have friend function

**D.Can not make instance of this class**



Given:

```
class A {
    A() {};
    virtual f() {};
    int i;
};
```

which statement is NOT true:

A.i is private

B.f() is an inline function

C.i is a member of class A

**D.sizeof(A) == sizeof(int)**



Given:

```
class A {
    A() {}
    virtual f() = 0;
    int i;
};
```

which statement below is **NOT** true:

A.i is private

B.Objects of class A can not be created

C.i is a member of class A

**D.sizeof(A) == sizeof(int)**



Given:

```
class X {
    int i;
    virtual void f() {};
};
```

If sizeof(int *) == sizeof(int) == 4, then sizeof(X)==?

A.4

B.6

**C.8**

D.Undetermined



如果一个类至少有一个纯虚函数，那么就称该类为（）。

**A.抽象类**

B.虚函数

C.派生类

D.具体类



假设A为抽象类，下列声明（）是正确的。

A.A fun(int);

**B.A *p;**

C.int fun(A);

D.A Obj;



在创建派生类对象时，构造函数的执行顺序是( )。

A.对象成员构造函数、基类构造函数、派生类本身的构造函数

**B.基类构造函数、对象成员构造函数、派生类本身的构造函数**

C.基类构造函数、派生类本身的构造函数、对象成员构造函数

D.派生类本身的构造函数、基类构造函数、对象成员构造函数



派生类中的私有成员

若采用私有继承方式，则派生类对象中的私有成员不可能为 ▁▁▁▁▁。

**A.基类中定义的私有成员**

B.基类中定义的保护成员

C.基类中定义的公有成员

D.派生类中新增的私有成员



以下说法正确的是？

A.在虚函数中不能使用this指针

**B.在构造函数中调用虚函数，不是动态联编**

C.抽象类的成员函数都是纯虚函数

D.构造函数和析构函数都不能是虚函数

---

## W9

当用一个对象去初始化同类的另一个对象时,要调用拷贝构造函数。

**T**

F



对象间赋值将调用拷贝构造函数。

T

**F**



下列各类函数中，不是类的成员函数的是

A.构造函数

B.析构函数

**C.友元函数**

D.拷贝构造函数



设类AA已定义，假设以下语句全部合法，哪些语句会触发调用拷贝构造函数（ ）。

```
AA a, b; //1
AA c(10, 20); //2
AA d(c); //3
AA e = d; //4
```

A.2

B.3

C.4

**D.3 和 4**



假设MyClass是一个类，则该类的拷贝初始化构造函数的声明语句为（ ）

A.MyClass&(MyClass x);

B.MyClass(MyClass x);

**C.MyClass(MyClass &x);**

D.MyClass(MyClass *x);



下列关于异常类的说法中，错误的是。

**A.异常类由标准库提供，不可以自定义**

B.C++的异常处理机制具有为抛出异常前构造的所有局部对象自动调用析构函数的能力

C.若catch块采用异常类对象接收异常信息，则在抛出异常时将通过拷贝构造函数进行对象复制，异常处理完后才将两个异常对象进行析构，释放资源

D.异常类对象抛出后，catch块会用类对象引用接收它以便执行相应的处理动作



下列哪一个说法是错误的?

A.当用一个对象去初始化同类的另一个对象时,要调用拷贝构造函数

B.如果某函数有一个参数是类A的对象,那么该函数被调用时,类A的拷贝构造函数将被调用

C.如果函数的返回值是类A的对象时，则函数返回时，类A的拷贝构造函数将被调用

**D.拷贝构造函数必须自己编写**



假设A是一个类的名字,下面哪段程序不会用到A的拷贝构造函数？

**A.A a1,a2; a1=a2;**

B.void func( A a) { cout<<"good"<< endl; }

C.A func() { A tmp; return tmp;}

D.A a1; A a2(a1);



如果某函数的返回值是个对象 ，则该函数被调用时，返回的对象？

**A.是通过拷贝构造函数初始化的**

B.是通过无参数的构造函数初始化的

C.用哪个构造函数初始化，取决于函数中return 语句是怎么写的

D.不需要初始化

---

## W11

多数运算符可以重载，个别运算符不能重载，运算符重载是通过函数定义实现的。

**T**

F



对每个可重载的运算符来讲，它既可以重载为友元函数，又可以重载为成员函数，还可以重载为非成员函数。

T

**F**



对单目运算符重载为友元函数时，可以说明一个形参。而重载为成员函数时，不能显式说明形参。

**T**

F



重载运算符可以保持原运算符的优先级和结合性不变。

**T**

F



预定义的提取符和插入符是可以重载的。

**T**

F



重载operator+时，返回值的类型应当与形参类型一致。
比如以下程序中，operator+的返回值类型有错：

class A {

```
int x;
```

public:

```
 A(int t=0):x(t){     }

    int operator+(const A& a1){ return x+a1.x;  }
```

};

T

**F**



重载关系运算符一般都返回true或false值。

**T**

F



The operator `::` can not be overloaded.

**T**

F



若重载为友元函数，函数定义格式如下：

<类型>operator<运算符>（<参数列表>）

{

<函数体>

}

T

**F**



下列运算符中，（ ）运算符不能重载。

A.＆＆

B.[ ]

**C.::**

D.<<



下列关于运算符重载的描述中，（ ）是正确的。

A.运算符重载可以改变操作数的个数

B.运算符重载可以改变优先级

C.运算符重载可以改变结合性

**D.运算符重载不可以改变语法结构**



为了能出现在赋值表达式的左右两边，重载的"[]"运算符应定义为：

A.A operator [ ] (int);

**B.A& operator [ ] (int);**

C.const A operator [ ] (int);

D.以上答案都不对



在C++中不能重载的运算符是

**A.?:**

B.+

C.\-

D.<=



下列关于运算符重载的表述中，正确的是（）。

A.C++已有的任何运算符都可以重载

B.运算符函数的返回类型不能声明为基本数据类型

**C.在类型转换符函数的定义中不需要声明返回类型**

D.可以通过运算符重载来创建C++中原来没有的运算符



能用友元函数重载的运算符是（）。

**A.+**

B.=

C.[]

D.->



下列哪一项说法是不正确的?

A.运算符重载的实质是函数重载

B.运算符重载可以重载为普通函数,也成员可以重载为成员函数

C.运算符被多次重载时,根据实参的类型决定调用哪个运算符重载函数

**D.运算符被多次重载时,根据函数类型决定调用哪个重载函数**



如何区分自增运算符重载的前置形式和后置形式？

A.重载时，前置形式的函数名是++operator，后置形式的函数名是operator ++

**B.后置形式比前置形式多一个 int 类型的参数**

C.无法区分，使用时不管前置形式还是后置形式，都调用相同的重载函数

D.前置形式比后置形式多一个 int 类型的参数



下列关于运算符重载的描述正确的是（ ）。

A.运算符重载可以改变操作数的个数

B.可以创造新的运算符

**C.运算符可以重载为友元函数**

D.任意运算符都可以重载



在重载一个运算符时，如果其参数表中有一个参数，则说明该运算符是( )。

A.一元成员运算符

B.二元成员运算符

C.一元友元运算符

**D.二元成员运算符或一元友元运算符**



下列关于运算符重载的描述中，错误的是（）。

A.运算符重载不改变优先级

**B.运算符重载后，原来运算符操作不可再用**

C.运算符重载不改变结合性

D.运算符重载函数的参数个数与重载方式有关



若需要为xv类重载乘法运算符,运算结果为xv类型,在将其声明为类的成员函数时,下列原型声明正确的是_________。

A.xv*(xv);

B.operator*(xv);

**C.xv operator*(xv);**

D.xv operator*(xv,xv);



下列运算符中，不可以重载的是（ ）。

A.new

B.++

**C..***

D.[]

---

## W13

pair类模板的作用是将两个数据组成一个数据，用来表示一个二元组或一个元素对，两个数据可以是同一个类型也可以是不同的类型。

**T**

F



现有声明：

template

class Test{...};

则以下哪一个声明不可能正确。

**A.Test a;**

B.Test < int> a;

C.Test < float> a;

D.Test< Test < int> > a;



Given:

```
template < class T >
void swap( T& x, T& y ) {
   T temp = x;
   x = y;
   y = temp;
}
int i,j;
float f,m;
```

Which statement is incorrect?

A.swap(i,j);

B.swap(j,i);

C.swap(f,m)

**D.swap(i,f);**



Given:

```
void f(int i) { cout << "Func1" << endl; }
template<class T>
void f(T t) { cout << "Func2" << endl; }
main() {
    f(2);
}
```

The result is :

**A.Func1**

B.Func2

C.`*nothing*`

D.undetermined



下列的模板说明中，正确的是。

A.template < typename T1, T2 >

B.template < class T1, T2 >

**C.template < typename T1, typename T2 >**

D.template ( typedef T1, typedef T2 )



关于类模板，描述错误的是。

**A.一个普通基类不能派生类模板**

B.类模板可以从普通类派生，也可以从类模板派生

C.根据建立对象时的实际数据类型，编译器把类模板实例化为模板类

D.函数的类模板参数需生成模板类并通过构造函数实例化



建立类模板对象的实例化过程为。

A.基类-派生类

B.构造函数-对象

**C.模板类-对象**

D.模板类-模板函数



下列有关模板的描述，错误的是____。

A.模板把数据类型作为一个设计参数，称为参数化程序设计

B.使用时，模板参数与函数参数相同，是按位置而不是名称对应的

C.模板参数表中可以有类型参数和非类型参数

**D.类模板与模板类是同一个概念**



模板函数的真正代码是在哪个时期产生的____。

A.源程序中声明函数时

B.源程序中定义函数时

**C.源程序中调用函数时**

D.运行执行函数时



类模板的使用实际上是将类模板实例化成一个____。

A.函数

B.对象

**C.类**

D.抽象类



声明模板的关键字为____。

A.static

**B.template**

C.typename

D.class



下列对模板的声明，正确的是____。

A.template<T>

B.template<class T1, T2>

**C.template<class T1, class T2>**

D.template<class T1, class T1>



下列选项中，哪一项是类模板实例化的时期____。

**A.在编绎时期进行**

B.属于动态联编

C.在运行时进行

D.在连接时进行



下列选项中，哪一个函数可以定义为对许多数据类型完成同一任务____。

**A.函数模板**

B.递归函数

C.模板函数

D.重载函数



一个____允许用户为类定义一种模式，使得类中的某些数据成员及某些成员函数的返回值能取任意类型。

A.函数模板

B.模板函数

**C.类模板**

D.模板类



下列关于pair<>类模板的描述中，错误的是。

A.pair<>类模板定义头文件utility中

B.pair<>类模板作用是将两个数据组成一个数据，两个数据可以是同一个类型也可以是不同的类型

**C.创建pair<>对象只能调用其构造函数**

D.pair<>类模拟提供了两个成员函数first与second来访问这的两个数据



模板的使用是为了（）。

**A.提高代码的可重用性**

B.提高代码的运行效率

C.加强类的封装性

D.实现多态性



假设声明了一下的函数模板：

```
template<class T>
T max(T x, T y)
{
    return  (x>y)?x:y;
}
```

并定义了int i; char c;
错误的调用语句是（）。

A.max(i,i);

B.max(c,c);

C.max((int)c,i);

**D.max(i,c);**

---

## W14

If you are not interested in the contents of an exception object, the catch block parameter may be omitted.。

**T**

F



catch (type p) acts very much like a parameter in a function. Once the exception is caught, you can access the thrown value from this parameter in the body of a catch block.。

**T**

F



异常处理的catch{ }语句块必须紧跟try{ }语句块之后，这两个语句之间不能插入另外语句。

**T**

F



有如下语句序列

```
第1行：    int a=1;
第2行：    try{
第3行：       if(a==1) throw(a);
第4行：       a++;
第5行：    }
第6行：    catch(int b){
第7行：       cout << “error! a = ” << b << endl;
第8行：    }
```

以上语句的第6行有编译错误，只能写成catch(int)。

T

**F**



One of the major features in C++ is （ ） handling,which is a better way of handling errors.

A.data

B.pointer

C.test

**D.exception**



What is wrong in the following code?

```
  vector<int> v;
  v[0] = 2.5;
```

A.The program has a compile error because there are no elements in the vector.

B.The program has a compile error because you cannot assign a double value to v[0].

**C.The program has a runtime error because there are no elements in the vector.**

D.The program has a runtime error because you cannot assign a double value to v[0].



If you enter 1 0, what is the output of the following code?

```C++
#include "iostream"
using namespace std;

int main()

{
  // Read two integers

    cout << "Enter two integers: ";

  int number1, number2;

  cin >> number1 >> number2;

  try
  {
    if (number2 == 0)
      throw number1;

    cout << number1 << " / " << number2 << " is "
      << (number1 / number2) << endl;

    cout << "C" << endl;
  }
  catch (int e)
  {
    cout << "A" ;
  }

  cout << "B" << endl;

  return 0;
}
```

A.A

B.B

C.C

**D.AB**



The function what() is defined in ______________.

**A.exception**

B.runtime_error

C.overflow_error

D.bad_exception



Which of the following statements are true?

**A.A custom exception class is just like a regular class.**

B.A custom exception class must always be derived from class exception.

C.A custom exception class must always be derived from a derived class of class exception.

D.A custom exception class must always be derived from class runtime_error.



Suppose Exception2 is derived from Exception1. Analyze the following code.

```c++
try {
statement1;

statement2;

statement3;
}

catch (Exception1 ex1)
{
}

catch (Exception2 ex2)
{
}
```

**A.If an exception of the Exeception2 type occurs, this exception is caught by the first catch block.**

B.If an exception of the Exeception2 type occurs, this exception is caught by the second catch block.

C.The program has a compile error because these two catch blocks are in wrong order.

D.The program has a runtime error because these two catch blocks are in wrong order.



Suppose that statement2 throws an exception of type Exception2 in the following statement:

```c++
try {
statement1;
statement2;
statement3;
}

catch (Exception1 ex1)
{
}

catch (Exception2 ex2)
{
}

catch (Exception3 ex3)
{
statement4;
throw;
}
statement5;
```

A.statement2

B.statement3

C.statement4

**D.statement5**



Suppose that statement3 throws an exception of type Exception3 in the following statement:

```c++
try {
statement1;
statement2;
statement3;
}

catch (Exception1 ex1)
{
}

catch (Exception2 ex2)
{
}

catch (Exception3 ex3)
{
statement4;
throw;
}

statement5;
```

Which statements are executed after statement3 is executed?

A.statement2

B.statement3

**C.statement4**

D.statement5



下列关于异常处理的说法不正确的是（ ）。

A.异常处理的throw与catch通常不在同一个函数中，实现异常检测与异常处理的分离。

B.catch语句块必须跟在try语句块的后面，一个try语句块后可以有多个catch语句块。

**C.在对函数进行异常规范声明时，若形参表后没有任何表示抛出异常类型的说明，它表示该函数不能抛出任何异常。**

D.catch语句块中，catch(…)表示该catch可以捕捉任意类型的异常，必须将catch(…)放在catch结构的最后。



以下关于异常处理的描述错误的是（）。

A.C++程序中出现异常时，编译器不会进行提示

B.将可能产生异常的代码放在try语句块内

C.使用catch关键字接收并处理异常

**D.重抛异常可以在try语句块或者catch语句块中调用throw实现**



下列关于异常的描述中，错误的是（）。

**A.编译错属于异常，可以抛出**

B.运行错属于异常

C.硬件故障也可当异常抛出

D.只要是编程者认为是异常的都可当异常抛出



下列关于异常类的说法中，错误的是。

**A.异常类由标准库提供，不可以自定义**

B.C++的异常处理机制具有为抛出异常前构造的所有局部对象自动调用析构函数的能力

C.若catch块采用异常类对象接收异常信息，则在抛出异常时将通过拷贝构造函数进行对象复制，异常处理完后才将两个异常对象进行析构，释放资源

D.异常类对象抛出后，catch块会用类对象引用接收它以便执行相应的处理动作



下列关于重抛异常的描述中，错误的是。

A.处理不了的异常，可以通过在catch结构中调用throw重新抛出异常，将当前异常传递到外部的try-catch结构中

B.重抛异常时只能从catch语句块或从catch块中的调用函数中完成

**C.重抛的异常可以被同一个catch语句捕捉**

D.可以单独使用throw关键字完成异常重抛



下列关于断言的描述中，错误的是。

A.断言是调试程序的一种手段

B.若断言情况发生，一般会终止程序

C.在C++中，宏assert()用来在调试阶段实现断言

**D.断言在程序调试与发布版本中都可以使用断言**



C++处理异常的机制是由（）3部分组成。

A.编辑、编译和运行

**B.检查、抛出和捕获**

C.编辑、编译和捕获

D.检查、抛出和运行

---

