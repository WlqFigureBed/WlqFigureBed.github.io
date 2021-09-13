# C++ Primer学习笔记

学习《C++ Primer 第五版》的笔记 2021.09.12

# 第一章 开始

## 编译、运行程序

在不同操作和编译器系统中，运行C++编译器的命令也各不相同，最常用的编译器是GNU编译器和微软Visual Studio编译器。默认情况下，运行GNU编译器的命令是g++：`g++ test.cpp -o test`

其中`-o test`指定了可执行文件的文件名（windows中生成`test.exe`），如果省略了这一句，则会默认生成名为`a.out`的可执行文件。

## 输入、输出

C++语言并未定义任何输入输出(IO)语句，而是包含了一个**标准库**来提供IO机制，例如`iostream库`，包含两个基础类型：`istream`和`ostream`，分别表示输入和输出流，一个流就是一个字符序列，是从IO设备读出或写入IO设备的。

流(stream)：随着时间的推移，字符是顺序生成或消耗的。

标准库定义了4个IO对象：

- cin：istream类型的对象，称为标准输入
- cout：ostream类型的对象，称为标准输出
- cerr：输出警告和错误信息，称为标准错误
- clog：输出程序运行时的一般性信息。

如何告诉我们想要使用iostream库？答：使用#include指令引入**头文件**。

> 头文件：为了使用标准库设施，必须包含相关的头文件。类似的，我们也需要使用头文件来访问为自己的应用程序所定义的类。
>
> 习惯上，头文件根据其中定义的类的名字来命名，通常使用.h作为头文件的后缀，但也可以使用.H、.hpp或.hxx。
>
> 标准库文件通常不含后缀，**编译器一般不关心头文件名的形式**，但有的IDE对此有特定要求。

```cpp
#include<iostream>
int main()
{
    char name[50];
    std::cout << "输入您的名字：" << std:endl;
    std::cin >> name;
    return 0;
}
```

- <<：输出运算符，接收两个运算对象，左侧是一个ostream类型对象，右侧是需要打印的值
- \>>：输入运算符，接收两个运算对象，左侧是一个istream类型对象，右侧是接收对象，从给定的istream中读入输入，存入接收对象
- endl：被称为操作符的特殊值，写入endl的效果是结束当前行，并且与设备关联的缓冲区中的内容刷到设备中。缓冲刷新操作可以保证到目前为止程序所产生的所有输出都真正写入输出流中，而不是仅停留在内存中等待写入流。
- std：该前缀指出名字cout和endl是定义在名为std的**命名空间**(namespace)中的。命名空间用于**避免名字冲突**，标准库定义的所有名字都在命名空间std中。使用**作用域运算符**(`::`)来分割命名空间和名字。

## 注释

两种注释：

```cpp
1. 单行注释
// like this
2. 多行注释
/*
 * Like
 * This
 */
```

## 控制流

```c++
while(condition){
    statement
}
for (int i = 1; i < 10; i++){
    statement
}
if(condition){
    statement
}
```

```c++
// 特殊用法：读取数量不定的输入数据
#include <iostream>
using namespace std;
int main( )
{
    int sum = 0,value =0;
    cout << "按Ctrl + D结束输入！" <<std::endl;
    while(cin>>value)  // 循环语句只有一句，可以省略花括号！
        sum += value;
    cout << "Sum is:" << sum << std::endl;
    return 0;
}
/* 当我们使用一个istream对象作为条件时，其效果是检测流的状态：
    1. 如果流是有效的，那么为true
    2. 当遇到文件结束符（end of file），或遇到一个无效输入时，则为false，结束循环
*/
```

> 从键盘输入文件结束符：
>
> - Windows：Ctrl + Z
> - UNIZ、Mac OS X：Ctrl + D

## 类

类是C++的特性之一，通过定义一个**类（class）**来定义一种数据结构，一个类定义了一个类型，以及与其相关联的一组操作。

