---
title: C++ Project Norm
date: 2023-05-30
tags: Study
---

## File design：

> ```
> ├── main.cpp
> ├── database.h // declaration
> ├── database.cpp // defination
> ├── tuple.h // type
> ├── tuple.cpp
> ├── writer.h // superclass
> ├── writer.cpp
> ├── adiwriter.h // subclass
> ├── adiwriter.cpp
> ├── Makefile
> ├── test.bat // the batch file
> ├── READNE.md
> ```

## Declaration (.h)

> ```c++
> #ifndef _DATABASE_H_
> #define _DATABASE_H_
> 
> #include "tuple.h" // 只需调用声明
> #include "adiwriter.h" // 只需调用实际用到的子类
> #include <iostream>
> #include <string>
> #include <set>
> class Database
> {
> private:
>     std::set<tuple> records;
>     // ...
> public:
>     Database();
>     Database(std::string filename);
>     ~Database();
>     // ...
> }
> 
> #endif
> ```

* ifndef：防止嵌套调用时出现反复调用的情况。

## 类型定义

> ```C++
> class tuple
> {
> public:
>     std::string primaryKey;
>     std::map<std::string, int> keytypes;
>     std::map<std::string, std::string> values;
>     tuple();
>     void setPrimaryKey();
>     friend bool operator <(const tuple &a, const tuple &b);
> };
> ```

* 重载运算符：用于排序与比较。
* 类型定义后使用同struct（不如说就是一个东西）

## 继承类应用

> ```c++
> class Writer
> {
> protected:
>     // ...
> public:
>     Writer();
>     virtual ~Writer();
>     // ...
> };
> ```
>
> ````C++
> class adiWriter : public Writer
> {
>     // ...
> };
> ````

## namespace使用

* namespace命名空间，包含多种关键字，std为常用的命名空间，cin，cout即为其中的关键字
* 若只想使用其中一个：`using std::sort;`
* 在一个代码块内如果有和命名空间相同的变量名，那么使用`using namespace`是无效的。
* 自定义namespace：

> ```c++
> #include <iostream>
> using namespace std;
> namespace NM1
> {
>     int zero = 0;
>     int sum(int x, int y)
>     {
>         return x + y;
>     }
> }
> 
> using namespace NM1;
> 
> int main()
> {
>     cout << sum(3, 4) << zero;
>     return 0;
> }
> ```

* 跨文件使用：同class，不过用`using namespace`调用

## 读写

* `argc` 和 `argv`：命令行参数
  * 第一个参数`argc`，用于参数计数，其值等于命令行中参数的个数；第二个参数`argv`，用于参数向量，是一个指向字符串数组的指针。

>```
>输入：./main.o 123 456
>argc = 3
>argv[0] = "./main.o"
>argv[1] = "123"
>argv[2] = "456"
>// 直接运行程序则argc = 1(运行程序而传入的命令)
>```

​		下面的代码用于读入输入的命令（因为要用batch，所以这样读）

> ```c++
> int main(int argc, char* argv[]){
>     std::string command;
>     if(argc == 1){ // 单条完整命令
>         while(getline(std::cin, command))
>             db.processCommand(command);
>     }
>     else{ // 命令被空格分开
>         for(int i = 1; i < argc; i++)
>             command = command + argv[i] + ' ';
>         db.processCommand(command);
>     }
>     db.exportDatabase();
>     return 0;
> }
> ```

* `iostream`：标准读写流

  * `cin`，`cout`分别是`istream`，`ostream`的对象，我们可以自己创造其他`istream`，`ostream`的对象。
  * `freopen("test.txt","w",stdout)`将标准输出重定向到`test.txt`。

* `fstream`：文件读写流

  > ```c++
  > std::ofstream fout;
  > fout.open("test.txt");
  > fout << "Hello" << endl;
  > fout.close();
  > ```

## Makefile使用

> ```makefile
> # Declare compiler variable
> CXX=g++
> # Declare compilation options
> CXXFLAGS=-Wall -g --std=c++11
> # Declare linking options
> LDFLAGS=
> # Declare source code files
> SRCS=main.cpp tuple.cpp writer.cpp adiwriter.cpp database.cpp
> # Convert source code files to a list of object files
> OBJS=$(SRCS:.cpp=.o)
> # Declare executable name
> TARGET=adif
> # Default target
> all: $(TARGET)
> # Dependencies
> $(TARGET): $(OBJS)
> 	$(CXX) $(LDFLAGS) -o $(TARGET) $(OBJS)
> # Automatically generate dependencies
> .depend: $(SRCS)
> 	rm -f ./.depend
> 	$(CXX) $(CXXFLAGS) -MM $^ > ./.depend
> # Include dependencies
> -include .depend
> # Clean
> clean:
> 	rm -f $(OBJS) $(TARGET) .depend
> ```

## batch文件

* `make.bat`

  * 窗口交互型
  * 没有Makefile，用于编译与生成可执行文件Main

  > ```
  > g++ -c main.cpp -std=c++11 -o main.o
  > g++ -c database.cpp -std=c++11 -o database.o
  > ...
  > g++ -o Main main.o Maze.o Player.o
  > ```

* `test.bat`

  * 指令测试型
  * 有Makefile，用于调用Makefile编译以及输入命令测试。
  * echo为回显在屏幕上的内容
  * 没有echo的为输入的指令，`mingw32-make`调用Makefile
  * pause后，需按任意键才会输入下一条指令

  > ```
  > @echo off
  > echo The version of C++ is C++11
  > mingw32-make
  > echo Compile successfully.
  > pause
  > 
  > echo ./adif -i a.adi
  > adif -i a.adi
  > pause
  > 
  > echo ./adif -s BD8GK
  > adif -s BD8GK
  > pause
  > 
  > echo ./adif -o test.adi
  > adif -o test.adi
  > pause
  > ```