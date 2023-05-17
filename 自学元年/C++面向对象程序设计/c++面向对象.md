# a better c

## 宏

### 常量宏

**使用方法：**

```c++
#define PI=3.14
#define STU_CNT=201
```

**作用：消除神仙数**，提供一个情景，在后续代码中如果频繁使用3.14，那读者压根不知道3.14到底是什么意思，因此会定义常量宏

#### **C++宏常量与常量的区别：**

==宏定义==

宏定义是C语言提供的三种预处理中的一种，又称为宏代换、宏替换，简称“宏”，用`#define`定义，如下：

`#define Pi 3.1415926`

宏常量没有类型，它是在编译前即**预编译阶段进行字符替换**，就好比如下的例子：

S = PI * r * r

在预编译阶段，直接将PI替换成3.1415926，同时没有类型安全检查，系统也不会为它分配内存。

宏定义使用`#undef`符号终止宏定义的作用域。

==常量==

常量则是一种标识符，它的值在运行期间恒定不变。常量使用关键字const定义，如下：

`const float PI = 3.14159;`

常量是在运行时进行替换，并且在编译时会进行严格的类型检验，同时系统也会为常量分配内存。



如上所述，C++语言可以用`const` 来定义常量，也可以用`#define`来定义宏常量。但是两者的区别在于：

+ const 常量有数据类型，而宏常量没有数据类型；
+ const 常量在运行时进行替换，宏常量则是在预编译截断进行替换，const 常量在编译阶段会进行类型安全检查，宏常量则不会；
  有些集成化的调试工具可以对const 常量进行调试，但是不能对宏常量进行调试。

==注意事项==

在实际使用中，由于宏常量在预编译时只是进行简单的字符替换，而不会进行编译检查，所有应该特别注意宏常量的使用，譬如如下代码：

```c++
#define N 3 + 2
float a = 2 * N
```

预想的值应该是a=10，但实际结果却是a=8，这是因为宏常量N在预编译阶段直接将字符替换，变成了如下代码：

`float a = 2 * 3 + 2`

这也叫宏定义的“边缘效应”。

另外根据规则：在C++ 程序中只使用const 常量而不使用宏常量，即const 常量完全取代宏常量

#### #define宏定义的边缘效应

**首先看一个案例：**

```c++
#include<iostream>
using namespace std;
#define N 3 + 2
int main()
{
	float a = 2 * N;  //输出8
	float b = N * 2;  //输出7
	cout << a << endl;
	cout << b << endl;
}
```

+ **8是怎么得到的？**：`8=2*3+2`

+ **7是怎么得到的？**：`7=3+2*2`

==类似英语里的就近原则==

+ **如何避免？**：使用括号`define N （3+2）`

### 函数宏

**使用方法：**

`#define Array_Size(a) sizeof(a)/sizeof(a[0])`

`#define Add(a,b)   (a+b) `

**作用：**减少开销

**原理：**

**调用函数时需要把原来主函数内各个局部变量封装之后进入函数，执行完函数后又要对函数栈进行消除，再打开主函数内部继续执行，开销较大，因此产生函数宏。**

**不足：**

**函数宏很可能导致运算结果出 错，这也就是为什么通常函数宏会带多个括号的原因，自己写时需要尽量避免。**

### 控制宏（开关）及在头文件的使用

[(36条消息) #ifdef与#endif的作用及用法_四月的我的博客-CSDN博客_#ifdef](https://blog.csdn.net/qq_40584593/article/details/85217303)

#### #ifdef与#endif语句

**解决的问题：**

程序运行的过程中，所有的行都会参加编译，但是有时候希望对其中的内容只在满足一定条件才进行编译，也就是对一部分内容指定编译的条件，这就是“条件编译”。有时，希望当满足某条件时对一组语句进行编译，而当条件不满足时则编译另一组语句、

**使用形式：**

```c++
#ifdef 标识符
程序段1
#else
程序段2
#endif
//它的作用是：当标识符已经被定义过(一般是用#define命令定义)，则对程序段1进行编译，否则编译程序段2。
其中#else部分也可以没有，即：
#ifdef
程序段1
#endif
```

示例：

```c++
#include<iostream>
using namespace std;
#define LOCAL_VER
int main()
{
# ifdef LOCAL_VER
	cout << "connect ximenzi" << endl;
# else
	cout << "connect other type" << endl;//颜色偏浅
#endif	
}
//输出connect ximenzi
```

**如果你不想连接ximenzi，只需要把宏定义删除即可**

```c++
#include<iostream>
using namespace std;
int main()
{
# ifdef LOCAL_VER
	cout << "connect ximenzi" << endl;
# else
	cout << "connect other type" << endl;
#endif	
}
//输出connect other type
```

#### 头文件中使用##ifndef...#def...#endif

**头文件标准写法：**

```c++
//头文件名字为mine.h
#ifndef MINE.H
#define MINE.H
...
...
#endif
```

这是为了避免头文件被多次声明，同时声明最好与头文件名字相关，以此保持声明的唯一性。声明中不 可出现 “.” !

**问题来源：**

头文件重复包含，发生重定义:
情景如下

```c++
//                     C.cpp files
 
#include <iostream>
using namespace std;
 
#include "A.h"
#include "B.h"
 
int main(void)
{
 
    add(1, 2);
    sub(45, 45);
    return 0;
}
 
 
//                     A.h files
 
#include <iostream>
using namespace std;
 
int sub(int a, int b)
{
    std::cout << "sub: a-b = " << a - b << std::endl;
    return a - b;
}
 
int add(int a, int b)
{
    std::cout << "sub: a+b = " << a + b << std::endl;
 
    return a + b;
}
 
#endif // _A_H_
 
 
//                        B.h files
 
#include <iostream>
using namespace std;
 
#include "A.h"
 
int mul(int a, int b)
{
    std::cout << "sub: a*b = " << a * b << std::endl;
 
    return a * b;
}
 
```

==报错：==**error C2084: function 'int sub(int,int)' already has a body**，其实是因为main函数调用了两次A.h头文件发生重定义

**解决方法：**

+ 条件编译的`#ifndef...#endif`
+ `#pragma once`

```c++
//                      C.cpp files
 
#include <iostream>
using namespace std;
 
#include "A.h"
#include "B.h"
 
int main(void)
{
 
    add(1, 2);
    sub(45, 45);
    return 0;
}
 
 
//                    A.h files
 
//用于测试头文件的重复包含和重定义的问题
#ifndef _A_H_
#define _A_H_
 
#include <iostream>
using namespace std;
 
int sub(int a, int b)
{
    std::cout << "sub: a-b = " << a - b << std::endl;
    return a - b;
}
 
int add(int a, int b)
{
    std::cout << "sub: a+b = " << a + b << std::endl;
 
    return a + b;
}
 
#endif // _A_H_
 
 
//                        B.h files
 
#ifndef _B_H_
#define _B_H_
 
#include <iostream>
using namespace std;
 
#include "A.h"
 
int mul(int a, int b)
{
    std::cout << "sub: a*b = " << a * b << std::endl;
 
    return a * b;
}
 
#endif // _B_H_
```

 条件编译的`#ifndef...#endif`作用原理：当编译器遇到第2(3,....)遍同样的头文件时，因为已经编译了一次（发现你已经定义过了一个量），在后面在遇到的时候，编译器自动忽略文件中的内容。

```c++
//                       C.cpp
 
#include <iostream>
using namespace std;
 
#include "A.h"
#include "B.h"
 
int main(void)
{
 
    add(1, 2);
    sub(45, 45);
    return 0;
}
 
 
 
//                 A.h
 
//用于测试头文件的重复包含和重定义的问题
//#ifndef _A_H_
//#define _A_H_
#pragma once
 
#include <iostream>
using namespace std;
 
int sub(int a, int b)
{
    std::cout << "sub: a-b = " << a - b << std::endl;
    return a - b;
}
 
int add(int a, int b)
{
    std::cout << "sub: a+b = " << a + b << std::endl;
 
    return a + b;
}
 
//#endif // _A_H_
 
 
//             B.h
 
//#ifndef _B_H_
//#define _B_H_
#pragma once
 
#include <iostream>
using namespace std;
 
#include "A.h"
 
int mul(int a, int b)
{
    std::cout << "sub: a*b = " << a * b << std::endl;
 
    return a * b;
}
 
//#endif // _B_H_
```

`#pragma once`是上述方式的简写

==但是==这样不能解决所有的重定义问题！！！(如下报错a重定义)

```c++
//   A.h

  #ifndef _A_H_
  #define _A_H_
  
  int a = 10;
  
  #include <iostream>
  using namespace std;
 
 int sub(int a, int b)
 {
     std::cout << "sub: a-b = " << a - b << std::endl;
     return a - b;
 }
 
 int add(int a, int b)
 {
     std::cout << "sub: a+b = " << a + b << std::endl;
 
     return a + b;
 }
 
 #endif // _A_H_
 
 
 //    B.h
 
 #ifndef _B_H_
 #define _B_H_
 
 #include <iostream>
 using namespace std;
 //#include "A.h"
 
 int a = 5;
 
 int mul(int a, int b)
 {
     std::cout << "sub: a*b = " << a * b << std::endl;
 
     return a * b;
 }
 
 #endif // _B_H_
```

　    看上面的代码，我们已将a变量的声明放在了条件编译之中，但是还是出现了重定义的问题，这是什么原因呢？在C++静态变量中有三种类型，其中有一种外部链接型的静态变量。而全局变量在声明的时候没有加上修饰词static，因此**这种变量是属于外部链接型的变量**。而**外部链接的变量对于在同一个工程文件的所有文件中都是可见的**，所以**在其中一个文件中定义的外部链接变量a，同时在另一个文件中也定义**。或者在包含头文件的时候重复包含了某一个定义了外部变量的头文件，就会导致在同一个工程文件形成的程序中将包含两个一样的变量。

　　==如何解决呢？==

​		解决的方法就是在a变量前加上extern修饰符即可：`extern` `int` `a = 10;`

因此，在头文件的定义中，我们最好不要将函数定义和变量的声明放到头文件中。但是下面的几种确实为头文件常包含的内容：

+ `函数声明`
+ 使用`#define`或者`const定义的符号常量`
+ `类声明`
+ `结构体声明`
+ `模板声明`
+ `内联函数`


#### 头文件中的内容

**macro**:宏

**function declaration**：函数声明（函数可以反复声明，但只能定义一次）

**struct Node{int date;Node next}**:类的成员函数声明&&成员变量

从概念上讲，头文件的功能是一般用来进行申明的（等函数原型或变量引用，宏定义）。C文件是用来进行定义的（函数定义、变量定义）。#include 是在编译器进行编译之前，即在预编译时把它后面所写的那个文件的内容，完完整整地、 一字不改地包含到当前的文件中来。
实际上C文件中是C语言的源代码，H头文件里也是C语言的源代码，所有符合C语言语法的代码都可以写在H头文件或C文件中。H头文件可以用INCLUDE，C文件也可以用INCLUDE。
（注意：C文件一般不建议使用INCLUDE，因为有的编译器在检查文件依赖性时，当INCLUDE的C文件变化时，不会重新编译C文件。）

+ C文件和H文件都是C语言的源代码，C语言语法中对于变量和函数是不能重复定义的，当C文件或H文件中的源代码中有相关内容时，重复包含会导致编译出错。

+ **如果严格的遵守要求，H头文件中全是申明，重复包含不会有什么问题的**。

+ 规范的按照C文件和H头文件的用法来编码，尽量避免头文件重复包含，避免包含C文件，这样的好处是，代码规范，不易出错，易维护、可读性强、可移植性好。

==好的c++程序员头文件的写法：==

```c++
#ifndef _B_H_
#define _B_H_
 
#include <iostream>
using namespace std;
 
#include "A.h"
 
#define pi 3.1415
 
const int value = 100;
 
int add(int a, int b);
 
class bb
{
    //......
};
 
struct bbb
{
    //......
};
 
inline void bbbb(int a, int b)
{
    cout << "a+b = " << a+b << endl;
}
 
int mul(int a, int b);
//{
//  std::cout << "sub: a*b = " << a * b << std::endl;
//
//  return a * b;
//}
 
#endif // _B_H_
```

类声明和结构体声明在头文件中不会导致重定义是因为类和结构体中创建变量只是在源文件中声明结构体变量的时候。因此不会出现重定义问题.

## extern()函数的使用

[C语言丨正确使用extern关键字详解 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/348762602)

[C/C++中extern关键字详解 - 简书 (jianshu.com)](https://www.jianshu.com/p/111dcd1c0201)

[(36条消息) C/C++中extern关键字详解_big_bit的博客-CSDN博客_c++ extern](https://blog.csdn.net/big_bit/article/details/51595714?utm_source=copy)

### extern修饰变量和函数

在C语言中，修饰符extern用在变量或者函数的声明前，用来说明“此变量/函数是在别处定义的，要在此处引用”。extern声明不是定义，

即不分配存储空间。

```c++
/*  basic_stdy.h */
 
#ifndef_BASIC_STDY_H_
#define_BASIC_STDY_H_
 
//extern int a;                                  //在头文件中声明,必须加上extern，否则就是重定义
//void fun();                                    //不用加extern也可以
 
#endif
/*  basic_stdy.cpp */
#include"basic_stdy.h"
#include<iostream>
using namespace std;
 
int a(2);
 
void fun(){
            cout << a <<endl;
}
/*main.cpp*/
#include<iostream>
#include "basic_stdy.h"
using namespace std;
 
extern int a;                                                 //or不用包含头文件， 变量只要声明即可
extern void fun();                                            //or不用包含头文件， 函数只要声明即可
 
int main(int argc,char **argv){
 
            cout << a << endl;
            fun();
 
            system("pause");
            return 0;
}

```

也就是说，在一个文件中定义了变量和函数， 在其他文件中要使用它们， 可以有两种方式：

+ 使用头文件，然后声明它们，然后其他文件去包含头文件

+ 在其他文件中直接extern

### extern"C"作用(c++和c混合编程)

**首先需要根据不同编译器将c文件连接入工程**

C++语言在编译的时候为了解决函数的多态问题，会将函数名和参数联合起来生成一个中间的函数名称，而C语言则不会，因此会造成链

接时无法找到对应函数的情况，此时C函数就需要用`extern “C”`进行链接指定，这告诉编译器，请保持我的名称，不要给我生成用于

链接的中间函数名。

比如说你用C 开发了一个DLL 库，为了能够让C ++语言也能够调用你的DLL 输出(Export) 的函数，你需要用extern "C" 来强制编译器不要修改你的函数名。

==常常看到以下代码==

```c++
#ifdef __cplusplus  
extern "C" {  
#endif  
  
/**** some declaration or so *****/  
  
#ifdef __cplusplus  
}  
#endif
```

**使用情景：**
1. 现在要写一个c语言的模块，供以后使用（以后的项目可能是c的也可能是c++的），源文件事先编译好，编译成.so或.o都无所谓。头**文件中声明函数标准格式如下：**

```cpp
#ifdef __cpluscplus  
extern "C" 
{  
#endif  
  
//some code  
  
#ifdef __cplusplus  
}  
#endif  
```

也就是把**所有函数声明放在some code的位置**。

如果这个模块已经存在了，可能是公司里的前辈写的，反正就是已经存在了，**模块的.h文件中没有extern "C"关键字，这个模块又不希望被改动的情况下**，可以这样，在你的c++文件中，包含该模块的头文件时加上extern "C", 如下：

```cpp
extern "C" {  
#include "test_extern_c.h"  
} 
```

上面例子中，如果**仅仅使用模块中的1个函数**，而不需要include整个模块时，可以不include头文件，而单独声明该函数，像这样:

```cpp
extern "C"{  
int ThisIsTest(int, int);            
} 
```

**注意:** 当单独声明函数时候， 就不能要头文件，或者在头文件中不能写extern intThisIsTest(int a, int b);否则会有error C2732: 链接规范

与“ThisIsTest”的早期规范冲突，这个错误。

还有就是要注意在*.c文件中不能写成extern"C"intThisIsTest(int x,int y);在C语言的头文件中，对其外部函数只能指定为extern类型，C语言中不支持extern "C"声明，在.c文件中包含了extern "C"时会出现编译语法错误。

**extern"C"的使用要点**

+ 可以是单一语句


  ` extern "C" double sqrt(double);`

+ 可以是复合语句,相当于复合语句中的声明都加了extern"C"

```c++
 extern "C"
   {
     double sqrt(double);
     int min(int, int);
  }
```

+ 可以包含头文件，相当于头文件中的声明都加了extern"C"

```c++
   extern"C"
  {
    ＃include <cmath>
  }
```

+ 不可以将extern"C"添加在函数内部

+ 如果函数有多个声明，可以都加extern"C",也可以只出现在第一次声明中，后面的声明会接受第一个链接指示符的规则。

+ 除extern"C",还有extern"FORTRAN"等。

### 声明OR定义
+ 定义也是声明，extern声明不是定义，即不分配存储空间。extern告诉编译器变量在其他地方定义了。

eg：

```c++
extern int i; //声明，不是定义   
int i; //声明，也是定义
```

+ 如果声明有初始化式，就被当作定义，即使前面加了extern。只有当extern声明位于函数外部时，才可以被初始化。

eg：

`extern double pi=3.1416;` //定义

+ 函数的声明和定义区别比较简单，带有{}的就是定义，否则就是声明。

eg：

```c++
extern double max(double d1,double d2); //声明   
double max(double d1,double d2){}//定义
```

4.除非有extern关键字，否则都是变量的定义。

eg：

```c++
extern inti; //声明   
int i; //定义
```

注: basic_stdy.h中有char glob_str[];而basic_stdy.cpp有char glob_str[]("123456");此时头文件中就不是定义，默认为extern

**程序设计风格：**

1. 不要把变量定义放入.h文件，这样容易导致重复定义错误。

2. **尽量使用static关键字把变量定义限制于该源文件作用域，除非变量被设计成全局**的。

也就是说:可以在头文件中声明一个变量，在用的时候包含这个头文件就声明了这个变量。

## overloading——函数重载

**函数重载满足条件**：

+ 同一个作用域下(比如全局作用下)
+ 函数名称相同
+ 函数参数类型不同或者个数不同或者顺序不同

**注意**：函数的返回值不可以作为函数重载的条件

```c++
void Print(int i)
{
	
} 
void Print(char *str)
{
    
}
//不报错
```

## default parameter——默认参数

`void f(int a,int b,int c=5) //不允许 void f(int a,int b=1,int c)` 
 后续调用可以只传入a,b 

函数声明和函数体里面只允许一个有默认参数的存在——函数声明

## 占位参数

````c++
c++
#include<iostream>
using namespace std;
//占位参数
//返回值类型 函数名（数据类型）{}
//目前阶段的占位参数用不到，后面课程会用到
//占位参数，还可以有默认参数：例如  int = 10
void func(int a,int)
{
	cout << "this is func" << endl;
}
int main()
{
	func(10,10);//占位参数必须填补
 }
````

# Object-oriented programming

**基本理念：**everything is object（万事万物皆面向对象）

**面向对象三大理念：**  

**封装**、**继承**、**多态**

**程序设计有两种方法：**

+ ==面向过程==：以事为中心
+ ==面向对象==：以物为中心(c++,java,python)

**面向对象只是一种方法，甚至C语言也可以面向对象**：(主要靠结构体实现)

[(36条消息) C 语言实现面向对象编程_onlyshi的博客-CSDN博客_c 面向对象](https://blog.csdn.net/onlyshi/article/details/81672279)

**c语言面向对象弊端：**仅仅是相关数据的集合，与类型相关的操作独立于类型之外，会导致命名危机等一系列问题

## 起源——simula-67 class


## 封装（一个类）

在c语言基础上，可以把函数封装到结构体就形成c++的类（c语言struct内是不能有函数定义的，只能定义指针指向函数）

```c++
class Student //self-definition type
{
//attribute /data number
private://访问控制：私有
	char* name;
	int id;
public://访问控制：共有
    int age;
//method /functon member
void intializeStu(char* aname, int aage);
//constructor 构造函数、构造器、用于初始化
    Student(char* aname,int aage);
};
void Student::intializeStu(char* aname, int aage) {
age = aage; //等价于写成 this->age = aage;
name = aname;
}
Student::Student(char* aname,int aage)
{
    this->aage=age;
    this->name=a
}
```



### 强制压缩代码

#### 内存模型Runtime-Memory

类**唯一**而对象可以有无穷多(文件本身占多大内存并不重要)

内存对齐原则：

```c++
#include<iostream>
using namespace std;
struct Test
{
	int i;//4
	double d;//8
	char c;//1
    void func();//不占内存
}
void Test::func() {}
int main()
{
    cout<<sizeof(Test)<<endl;
}
//输出8+8+8=24  按大分配
```

==however==仅仅调换一下顺序

```c++
#include<iostream>
using namespace std;
struct Test
{
	int i;//4
	char c;//1
    double d;//8
    void func();//不占内存
}
void Test::func() {}
int main()
{
    cout<<sizeof(Test)<<endl;
}
//输出8+8=16 
```

#### 如何压缩？

将`pragma pack(1)`放入头文件

```c++
#pragma pack(1)
#include<iostream>
using namespace std;
#include<iostream>
using namespace std;
struct Test
{
	int i;//4
	char c;//1
    double d;//8
    void func();//不占内存
}
void Test::func() {}
int main()
{
    cout<<sizeof(Test)<<endl;
}
//输出13
```

==为什么不默认压缩？==对性能的无利，且合并复杂

#### 位结构

[(38条消息) 关于位结构体及位操作总结_pragma_g的博客-CSDN博客_位结构体](https://blog.csdn.net/pragma_g/article/details/79282400)

```c++
#include<iostream>
using namespace std;
struct Test
{
	int a : 1;
	int b : 1;
	int c : 1;//位结构，按位描述  4byte  int意味着总体是int  a只有一个bite ，只能赋值0和1
};
int main()
{
	cout << sizeof(Test) << endl;
}
//输出4
```

一般硬件接口级常用

#### malloc()函数

头文件：`#include <stdlib.h>`

malloc() 函数用来动态地分配内存空间

**其原型为**：
`void* malloc (size_t size)`;

+ size 为需要分配的内存空间的大小，以字节（Byte）计。

+ malloc() 在堆区分配一块指定大小的内存空间，用来存放数据。这块内存空间在函数执行完成后不会被初始化，它们的值是未知的。如果希望在分配内存的同时进行初始化，请使用 [calloc()](http://c.biancheng.net/cpp/html/134.html) 函数。

+ 返回值：分配成功返回指向该内存的地址，失败则返回 NULL。

由于申请内存空间时可能有也可能没有，所以需要自行判断是否申请成功，再进行后续操作。

如果 size 的值为 0，那么返回值会因标准库实现的不同而不同，可能是 NULL，也可能不是，但返回的指针不应该再次被引用。

注意：**函数的返回值类型是 void *，void 并不是说没有返回值或者返回空指针，而是返回的指针类型未知**。所以在使用 malloc() 时通常需要进行强制类型转换，将 void 指针转换成我们希望的类型，例如：

```c
char *ptr = (char *)malloc(10);  // 分配10个字节的内存空间，用来存放字符
```

示例：

```c
#include <stdio.h>  
/* printf, scanf, NULL */
#include <stdlib.h>  /* malloc, free, rand, system */
int main ()
{   
    int i,n; 
 	char * buffer;
    printf ("输入字符串的长度：");
    scanf ("%d", &i);
    buffer = (char*)malloc(i+1);  // 字符串最后包含 \0  
    if(buffer==NULL) exit(1);  // 判断是否分配成功    
    // 随机生成字符串    for(n=0; n<i; n++)     
    buffer[n] = rand()%26+'a'; 
    buffer[i]='\0'; 
    printf ("随机生成的字符串为：%s\n",buffer);  
    free(buffer);  // 释放内存空间    
    system("pause");
    return 0;
}
```

运行结果：
输入字符串的长度：20
随机生成的字符串为：phqghumeaylnlfdxfirc

该程序生成一个指定长度的字符串，并用随机生成的字符填充。字符串的长度仅受限于可用内存的长度

### access control(访问控制)

当一个对象面对外界的时候，我们不希望外界能够随意修改类内属性，将其私有化时，我们可加关键词：private 和 public。一 般情况不要公有化属性。在 struct 声明下不写访问控制默认公有，而 class 声明下会默认私有。

```c++
class Student {
private:
char* name;
int age;
public:
void setAge(int aage);
Student(char *aname,int aage);//构造函数，构造器
};
```

### 构造函数（初始化）

```c++
#include<iostream>
using namespace std;
class Student
{
private: 
	int id;
	char* name;
public:
	int age;
	void initializeStu(char* aname, int aage);
	Student(char* aname, int aage);
	//Student(int aage);//类内部重载，可行
	Student();//默认有的构造函数，不可见，现在是试图模仿，一写就没了//default constructor
};
Student::Student(char* aname, int aage)
{
	this->age=aage;
	this->name=aname;
}
void Student::initializeStu(char* aname, int aage)
{
	age = aage;//蕴含this->age=aage;    //the hidden this pointer
	name = aname;
}
void InitializeStudent(Student* s, char* aname, int aage)
{
	s->age = aage;
}
int main(int argc, char* argv[])
{
	int i;
	Student s1, s2;
	s1.initializeStu("Zhangsan", 18);//初始化
	s2.initializeStu("Lisi", 20);//初始化
	Student s("zhangsan", 18);//构造函数初始化
	return 0;
}
```

### bugs of pointers

#### 指针何来bug？

**value or handle？**      ->这个成员是不是必有属性

考虑以下情景

```c++
#include<iostream>
using namespace std;
class wheel
{
	int i;
};
class SelfDrivingSys
{
	int ii;
};
class Car
{
	wheel w[4];//value——best(汽车都有的)
	wheel* p_w;//handle--worse
	SelfDrivingSys* p_sys;//--best（汽车可有可无)
};
```

+ 类对象都拥有的属性->value
+ 类对象可有可无的属性->handle

**handle的初始化：**

```c++
#include<iostream>
using namespace std;
class Test
{
	int i;
	int* p;
	Test()
	{
		p = NULL;//指针必须初始化
	}
};
```

**pointer危机**

指针越来越多，造出memory leak（不可见，对程序本身没有伤害名单机器会越来越慢）

**指针指到一个无限大的空间，最后释放所指的空间怎么释放？--析构**

#### 析构函数

```c++
#include<iostream>
using namespace std;
class Test
{
	//attrribute  属性
	int i;//value  值
	int* p;//handle句柄
public:
	//constructor构造
	Test(int ai);
	Test(int ai, int aj);
	//destructor析构
	~Test();//析构不会重载，在消亡时调用，重载——需要传不同参数，析构不需要传
	//如果构造里有动态内存new，一定会有析构
	// 构造里没有new，也可能有析构 析构可以释放本类所有函数调用的一切内存机构
	//构造中不要做与初始化无关的事
	// 析构中不要做与清空内存无关的事
};
Test::~Test()
{
	cout << "destructor" << endl;
}
Test::Test(int ai)
{
	i = ai;
	p = NULL;//指针必须初始化   
}
Test::Test(int ai, int aj)
{
	i = ai;
	p = new int(aj);
}
int main(int argc, char argv[])
{
	Test t1(1, 2);
	//...
	cout << "**********" << endl;
	return 0;
}
```

+ 析构不会重载（**析构不会传参**）
+ 如果构造函数里有new动态内存，必须要自己写析构以释放堆区内存,比如：

```c++
#include<iostream>
using namespace std;
class Person
{
public:
	int* m_Height;
	Person(int height)
	{
		m_Height = new int(height);
	}
	~Person()
	{
		if (m_Height != NULL)
		{
			delete m_Height;
			m_Height = NULL;
		}
	}
};
```

+ 构造里没有new，也可能有析构，析构可以释放本类所有函数调用的一切内存机构

**summary of constructor&&destructor**

+ 构造中不要做与初始化无关的事
+ 析构中不要做与清空内存无关的事

#### 深拷贝

**copy construction（拷贝构造）**：拿一个已存在的对象生成一个新的对象

`Test(const Test&t)`

**bitwise copy（浅拷贝）：**

系统默认


```c++
#include<iostream>
using namespace std;
class Person
{
public:
	int* m_Height;
	Person(const Person &p)
	{
		m_Height = p.m_Height;
	}
	~Person()
	{
		if (m_Height != NULL)
		{
			delete m_Height;
			m_Height = NULL;
		}
	}
};
```

==浅拷贝弊端：==

+ 倘若出现拷贝对象是带有指针的——后果：一个蚂蚱被两根绳子拉
+ 肤浅 类似c语言memorycopy 

**补充-memcpy内存拷贝函数**

定义:

memcpy函数（memory+copy）顾名思义是内存拷贝函数，具体的功能是将src地址处的count个字节拷贝到dest地址处，头文件

`<memory.h> or <string.h>`，其语法为：

`void *memcpy( void *dest, const void *src, size_t count )`;

**logical copy（深拷贝）：**

```c++
#include<iostream>
using namespace std;
class Person
{
public:
	int* m_Height;
	Person(const Person &p)
	{
		m_Height = new int (*p.m_Height);
	}
	~Person()
	{
		if (m_Height != NULL)
		{
			delete m_Height;
			m_Height = NULL;
		}
	}
};
```

**总结：**

| pass by value | pass by address |
| ------------- | --------------- |
| input(只读)   | input/output    |
| sizeof(value) | sizeof(int)     |
| 调用拷贝构造  | nothing         |

==never pass by value:==

除了系统自带类型(整型、浮点型)可以值传递

自定义类型千万不可值传递(**build-in type爱咋传咋传        self-defintion type全部地址传递**)

`void func(Test t)`绝对不行

+ 函数参数有直接变量(如int、char、double等)类型、指针类型和引用类型。

+ 如果参数是变量，传递方式是传值，就是将实参的值复制(复制，意味着空间消耗和时间消耗)到“栈”空间中。

+ 如果参数是指针，传递方式是传址，需将指针复制(同样也消耗空间和时间，对于数组而言，只需存储数组首地址)到“栈”空间中。

+ 如果是引用，则既不是传值，也不是传址，主调函数和被调函数共享参数的存放地址，与全局变量共享方式相同。

+ 对于拷贝(复制)构造函数而言，类对象通常需要较多的存储空间，如果按值传递，必然会较大消耗“栈”空间，也需要较多的时间实施复

  制过程。因为复制构造函数不会修改参数的内容，也不会修改参数的属性，所以构造函数的参数应该是常量引用传递，如 

  `ClassName(const ClassName &obj)`

+ 如果参数是类对象，就是值传递，就要复制，复制就要调拷贝构造函数。这就形成了拷贝构造函数再调拷贝构造函数，无限递归下去。因此只能用引用的方法
  
+ 有时，一些函数（包括拷贝构造函数）参数要求用（不是必须用）常引用，目的是为了避免函数体中无意地修改指针所指对象的值。

#### 常见错误 

+ fly pointer永远不要定义一个指针，除非定义为NULL
+ re-free不要重复释放
+ 不要return address of local variable（局部变量的地址）

#### reference(引用)

+ reference is a safe pointer
+ 借值之名，行指针之实

==注意事项&解释：==

**无野引用：**

```c++
int main(int argc,int argv[])
{
    int &a;//错误，无野引用
    //其实野指针也千万不要定义！   定义为NULL
}
```

**必须初始化,且只能定义一次**

```c++
#include<iostream>
using namespace std;
int main()
{
	int a = 10;
	int b = 20;
	int& r = a;
	int& r = b;//重定义
}
```

**why?pointer可以**

```c++
#include<iostream>
using namespace std;
int main()
{
	int a = 10;
	int b = 20;
	int*p = &a;
	p = &b;//重定义
}
```

==指针是变量，引用是常量   只有常量只有一次机会赋值==

### const

+ constant const

**保证input只读操作**

```c++
void fun(const int* i)
{
	//仅仅是读一读（input）要用const避免修改
	(*i)++；//报错
}//const修饰不能写入
```

+ const parameter*
+ const return value
+ const data member
+ const function member

```c++
class Const {
int j;
enum{tcp,udp}; //枚举型，定义本类常量此时tcp=0，udp=1
//类中使用在定义本类的常量
public:
void fun()const; //屁股后面跟const显式声明可调用，常量可调用，变量更可以调用,但只能读，不允许写
    	//一旦函数声明为静态，则失去this指针，只允许操作静态成员
}
const void Const::fun(){
cout << j << endl;>>
//显示声明，该函数可以被常量调用。
//即没有内存写入删除操作
}
```



### static

**static**与全局有关

+ 储存在全局区（同全局变量）

```c++
#include<iostream>
using namespace std;
int g_i = 0;
int main()
{
    static int i = 0;
    cout << "i的地址： " << &i << endl;
    cout << "g_i的地址： " << &g_i << endl;
}
//输出
i的地址： 00007FF779F8F454
g_i的地址： 00007FF779F8F450
```

+ static local var 保值，计数（只创建一次，不再释放）

```c++
#include<iostream>
using namespace std;
void func()
{
	static int i = 0;
	i++;
	cout << i << endl;
}
int main()
{
	func();//1
	func();//2
}
```

+ static function  与extern相反

**全局变量默认本文件使用：其他文件调用声明时需要extern()**   ->

**函数默认全文件:** 其他文件调用时可以不写extern()   ->external link 

```c++
//源.cpp
int g_c=100;
void str2int(){}
//其他.cpp
extern int g_c;
str2int()
```

在某一文件中将函数或者变量声明为 `global`之后，另外一个文件可以声明`extern` 后直接使用。

==however static会缩小使用范围==

`static void str2int()//函数访问范围从全文件改为当前文件no link`

+ static global var      全局变量前再用static的话就算其他文件用extern 链接会失效
+ static data member    彼此感知（感知能力：全局变量max 、调用函数） 本类所有函数共享的空间
  + 全局变量是程序之间各个变量之间发生联系，彼此感知的重要途径！但还是能不用就不用。
+ static function         可以被类名直接调用

**初始化问题：**

如果将`static`修饰于类内某一个对象时，该变量变成了本类共享的一个空间，此时需要注意**不可将其初始化放置于构造函数**之中，而应该**单独初始化**! 而当`static`修饰类内某个函数时，则该函数**可以被类名直接调用而不用通过对象**。同样地，这个函数被限制失去了`this`指针，即只允许操作静态成员。

```c++
class Test
{
static int i;
int j;
public:
Test(int aj);
static void fun();
}
int Test::i = 100;
Test::Tset(int aj) {
j = aj;
}
int main()
{
Test::fun();
return 0;
}
```


### new &delete库函数

==new delete operator运算符，与+，-同级==

+ C语言时代要创建对象用的是**malloc** 和 **free** ，
+ 如今在C++语言中，`new = malloc + constructor` ，先申请空间(malloc)后再调用构造函数(constructor)。同样 ，`delete = destructor+free`先析构(destructor)之后再释放(free)。这两类不允许串用！

### memory&&runtime memory

**你只需要操心runtime memory！！！**

**memory**

+ ==代码区==  取决于exe有多大 运行时代码区稳定
+ ==全局变量区==   默认清空，局部变量不清空得赋值   `int *p=&g_i;  cout<<*(p+100)<<endl;`   main()之前全局变量清空   局部变量在main之后

**runtime memory**

+ 栈(stack)
+ 堆(heap)

| stack                                | heap                                         |
| ------------------------------------ | -------------------------------------------- |
| 连续、运行快                         | 没有析构（需要有保洁clean一直跟着）——c语言慢 |
| dynamic memory alloc（动态分配内存） | local car                                    |
| 连续内存                             | 离散空间，内存碎片化                         |

## 继承（类与类）

### inheritance(继承)&composition(组合)

**继承：新建一个类继承父类**（继承共性另写特性）

**组合：类内对象为其他类**

**reuse：**代码的重用

**人月：**一个程序员工作多少月

**继承示例：**

```c++
class Computer
{
	int price;
	char* brand;
public:
	int get_price();
	void service();
};
int Computer::get_price()
{
	return this->price;
}
void Computer::service()
{
	cout << "service" << endl;
}
class Macbook:public Computer
{
//do something
int useyears;
public:
void service();
}
void Macbook::servce()
{
if(useyears < 1)
cout << "New Macbook" << endl;
else
Computer::servise; //reuse  直接写service重调用
//父类中定义方法A,子类中又有方法B，那必有A出现——否则是对父类特性的否定  以上为真正的继承
}
```

这样写了之后 Macbook继承了父类Computer 的全部性质。而其本身的特性写在括号里。需要注意的几点是：

+  子类必然调用父类函数，但如果父类函数中有函数重载，而在子类中只声明了其中部分函数，则父类另一部分函数会被冲掉。
+ 当成员中包含另一个类的对象时，同样可以重用该对象里的函数。与子承父类的重定义不同，这时两函数无任何关系。 
+ 创建一个子类对象的时候一定会调用父类的构造函数，先调父类构造函数再调子类构造函数。同样调用析构时先调子类再调父 类。值得注意的是：子类构造函数开头必须写明父类构造函数是如何实现的，例如：

```c++
Deirved::Derived(int ai, int aj):Base(1) //构造初始化变量
{
cout << "construct successfully" << endl;
}
```

+ 如果两个对象组合时，必然调用其内部简单对象的构造函数。如果没有默认构造函数时，应在复杂类的构造函数中写明应如何构造简单类的对象。该语法称为**构造初始化列表**如下代码所示。注意**构造顺序与声明顺序保持一致！**

```c++
class Car 
{
Engine e;
int other;
public:
Car();
}
Car::Car():e(1) //构造初始化列表
{
//super(1) java写法
cout << "construct successfully" << endl;
}
```

**组合示例**:

```c++
class Engine
{
public:
	void run();
};
void Engine::run() {}
class Car
{
	Engine e;
public:
	void run();
};
void Car::run()
{
	e.run();//reuse
	cout << "car is running" << endl;
}
```

==when 继承？when 组合？==

**judged by两者有无必然关系**

在上面的例子中：

+ 电脑中service有必然关系

+ 汽车run函数和engine没有关系

### 继承和组合的构造&析构顺序

**继承：**

+ 创建子类对象时调用父类对象时会不会调用父类对象的构造函数---当然会调用！而且是先父类后子类（子类前包着一个父类对象）析构时先子类后父类——先消亡子

+ 如果父类需要传参数，子类在构造时**需要构造初始化列表 (construction initialization list)**

  `Derived::Derived():Base(1)`以传参数  称Base(ai)为初始化列表 

**组合：**

+ 如果是组合（上面的car和enigine）  同样会调用enigine构造           如果enigine也没有**默认构造**需要Car::Car():e(1)

==初始化顺序：==按定义的顺序初始化`Test：：Test(int a):i(a),j(i)`

**成员是按照他们在类中出现的顺序进行初始化的，而不是按照他们在初始化列表出现的顺序初始化的**，看代码：

```c++
class foo
{
public:
int i ;int j ;
foo(int x):i(x), j(i){}; // ok, 先初始化i，后初始化j
};
```

再看下面的代码：

```c++

class foo
{
public:
int i ;int j ;
foo(int x):j(x), i(j){} // i值未定义
};
```

**这里i的值是未定义的因为虽然j在初始化列表里面出现在i前面，但是i先于j定义，所以先初始化i，而i由j初始化，此时j尚未初始化，所以导致i的值未定义。一个好的习惯是，按照成员定义的顺序进行初始化。**

### 削弱父类接口

+ **继承方式不写，默认私有继承：**

```c++
class Base
{
public:
	void fun();
};
void Base::fun()
{

}
class Dervied : Base//=class Dervied : private Base选择私有继承 父类public中的在子类看来就是降级为private削弱父类接口
{

};
//正常的继承：
class Dervied : public Base
```

**私有继承,仅为了维持语法正确性——一文不值**

+ **基类构造函数有含参构造和默认构造两种，到你延伸类却只改了一种，削弱父类接口**

```C++
class Base//基类
{
public:
	void fun();
	void fun(int i);
};
void Base::fun(){}
void Base::fun(int i){}
class Dervied :public Base//延伸类
{
public:
	void fun();
};//错误，不应该只动一部分     削弱父类接口
void Dervied::fun() {}
```



==基类访问权限使用频率比较==

```c++
class Base
{
private://最少见
protected://对类外私有，对子类共有
public:
};
```

### 多重继承

```c++
class Dervied :public Base1, Base2
```

 c++的类可以有多个父类   ----可能会有菱形继承()   事实上也**只是混合语法，不该使用**,java规定只能有一个父类 

### is a(是)?is like a（像）?

## 多态（类行为）——重用即多态性

### 为什么需要多态？

问题引入

```c++
class Pet
{
	int age;
	char* name;
public:
    void Speak();
}
class Dog :public Pet
{
public:
	void Speak();
};
class Cat :public Pet
{
public:
	void Speak();
};
void Pet::Speak()
{
	cout << "Pet::Speak" << endl;
}
void Needle(Pet& pet)
{
	pet.Speak();
}
int main()
{
	Cat a;
    Dog b;
    Needle(a);
    Needle(b);
}
```

你想要：

```c++
	/*
	if pet is a Dog
	Dog::Speak
	else if pet is a Cat
	Cat::Speak
	*/
```

结果输出了个啥？

```c++
Pet::Speak
Pet::Speak
```

**这是为什么？**

#### binding

+ binding 绑定：将函数的一次调用，与函数入口地址相互映射的过程，称为绑定
+ early binding:前绑定
+ later binding: runtime/dynamic binding
+ 函数名->函数指针，指向函数执行的第一步

上面基类的speak函数便发生了前绑定，导致无法多态（多种可能执行的形态）

### 如何实现多态

#### 前提

**继承是多态的前提**

#### 虚函数

基类函数前加上关键字`virtual`

```c++
class Pet
{
	int age;
	char* name;
public:
    void Speak();
}
class Dog :public Pet
{
public:
	void Speak();
};
class Cat :public Pet
{
public:
	void Speak();
};
void Pet::Speak()
{
	cout << "Pet::Speak" << endl;
}
//never pass by value!!!   自定义类型千万不要传value  除了int等固有的
void Needle(Pet& pet)//为什么要是引用？ void Needle(Pet pet)  // 会调用父类的拷贝构造，会成为父类的虚指针，虚指针由构造函数初始化
{
	pet.Speak();
}
int main()
{
	Cat a;
    Dog b;
    Needle(a);
    Needle(b);
}
//输出
Cat::Speak
Dog::Speak
```

#### 多态实现原理

一个类有一个虚函数表，一个对象多一个虚指针，指向本类的虚函数

#### 构造和析构中的虚函数

+ 构造函数会是虚函数吗  ->虚函数判断原则：是否有二义性    构造与虚函数无缘，new 啥调用啥的构造函数
+ 析构一定是虚函数   不完善，应该把父类的析构给virtual掉
+ 虚函数有损性能  性能：时间复杂，空间复杂：因为多态产生贼多虚指针，损性能
+ 如果一个类里有一个虚函数，则其他的函数能写成虚函数就写成虚函数(没说纯虚函数)，反正有损性能，则放开虚，即写类的能虚的全虚
+ 构造和static不能虚

#### 纯虚函数pure virtual和抽象类

```c++
class Pet
{
	int age;
	char* name;
public:
	//若一个类中含有纯虚函数（有一个就行），则称之为抽象类
	virtual void Speak() = 0;
	virtual void Sleep();
}
```

+ abstract class抽象类不可以实例化（不能有对象）

==抽象类用途：==

+ 约束一个类家族的共性行为
+ 连接本不相关的类家族，抽象其共性行为
+ Java里只能有一个父类，但可以实现多个接口，->接了两个不相关的类

**如果继承一个抽象类，也不一定实现所有的四个函数->又产生了抽象类，即不能有实例**

```c++
class NwMsg
{
public:
	virtual void Send() = 0;
	virtual void Recv() = 0;
	virtual void Code() = 0;
	virtual void Decode() = 0;
};
```

#### 狗说猫话

#### 内存空间

[(38条消息) （二）C++类的内存大小计算_大锅菜～的博客-CSDN博客](https://blog.csdn.net/youtiao_hulatang/article/details/104679840)

#### upcasting & downcasting

[(38条消息) C++中的向上类型转换和向下类型转换_雪岢奇的博客-CSDN博客](https://blog.csdn.net/wangweitingaabbcc/article/details/7720979)

+ upcasting:向上类型转换  
+ downcasting 向下类型转换是危险的

# Design pattern

**设计模式总共有23种、3类（构建型模式）、（结构型）、（行为型）**

以单件模式举例：全局只有一个对象
```c++
class Single
{
static Single* self;//静态成员，不允许类内初始化，全类共享
Single();
public:
static Single* get_instance();
}
Single* Single::get_instance(){
if(self == NULL)
self = new Single();
return self;
}
Single* Single::self = NULL;//类外初始化
int main()
{
	Single *p1 = Single::get_instance();
}
```

**单件模式的构造函数被私有了**

# Qt framework （框架）



# Windows Programming

+ 默认构造函数可以初始化虚指针



