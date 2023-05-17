# C++基础入门

[C++ 实例 | 菜鸟教程 (runoob.com)](https://www.runoob.com/cplusplus/cpp-examples.html)

## C++初识
### 第一个c++程序
### 注释
### 变量



### 常量

**作用**：用于记录程序中不可更改的数据(可在定义时统一修改常量值)

**定义常量的两种方式**：

1. **#define**宏常量：`#define 常量名 常量值`
EG: ```#define PI 3.14```

+ ==通常在文件上方定义，表示一个常量==

2. **const**修饰的变量：`const 数据类型 常量名 常量值`

+ 通常在变量
+ 定义前加关键字const，修饰该变量为常量，不可修改



示例

```c++
#include<iostream>
using namespace std;

//宏常量
#define Day 7
int main()
{
	/*Day = 14;*/  //报错，宏常量不可修改
	cout << "一周有：" << Day<<  "Day"<< endl;

//const修饰变量
	const int month = 12;
	//month = 24;   //报错，常量不可修改
	cout << "一年有：" << month << "month" << endl;
	system("pause");
	return 0;
}
```





### 关键字

**作用：**关键字是C++中预先保留的单词

+ 定义变量或常量的时候，不要用关键字

![](C:\Users\曹建钬\Pictures\Camera Roll\20130806104900234.jpg)

**1. asm**

asm (指令字符串)：允许在 C++ 程序中嵌入汇编代码。

**2. auto**

auto（自动，automatic）是存储类型标识符，表明变量"自动"具有本地范围，块范围的变量声明（如for循环体内的变量声明）默认为auto存储类型。

**3. bool**

bool（布尔）类型，C++ 中的基本数据结构，其值可选为 true（真）或者 false（假）。C++ 中的 bool 类型可以和 int 混用，具体来说就是 0 代表 false，非 0 代表 true。bool 类型常用于条件判断和函数返回值。

**4. break**

break（中断、跳出），用在switch语句或者循环语句中。程序遇到 break 后，即跳过该程序段，继续后面的语句执行。

**5. case**

用于 switch 语句中，用于判断不同的条件类型。

**6. catch**

catch 和 try 语句一起用于异常处理。

**7. char**

char（字符，character）类型，C++ 中的基本数据结构，其值一般为 0~255 的 int。这 256 个字符对应着 256 个 ASCII 码。char 类型的数据需要用单引号 **'** 括起来。

**8.class**

class（类）是 C++ 面向对象设计的基础。使用 class 关键字声明一个类。

**9. const**

const（常量的，constant）所修饰的对象或变量不能被改变，修饰函数时，该函数不能改变在该函数外面声明的变量也不能调用任何非const函数。在函数的声明与定义时都要加上const，放在函数参数列表的最后一个括号后。在 C++ 中，用 const 声明一个变量，意味着该变量就是一个带类型的常量，可以代替 #define，且比 #define 多一个类型信息，且它执行内链接，可放在头文件中声明；但在 C 中，其声明则必须放在源文件（即 .C 文件）中，在 C 中 const 声明一个变量，除了不能改变其值外，它仍是一具变量。如:

```
const double pi(3.14159);
或 
const double pi = 3.14159;
```



**10. const_cast用法：**

```
const_cast<type_id> (expression)
```

该运算符用来修改类型的 const 或 volatile 属性。除了 const 或 volatile 修饰之外， type_id 和 expression 的类型是一样的。常量指针被转化成非常量指针，并且仍然指向原来的对象；常量引用被转换成非常量引用，并且仍然指向原来的对象；常量对象被转换成非常量对象。

**11. continue**

continue（继续）关键字用于循环结构。它使程序跳过代码段后部的部分，与 break 不同的是，continue 不是进入代码段后的部分执行，而是重新开始新的循环。因而它是"继续循环"之意，不是 break（跳出）。

**12. default**

default（默认、缺省）用于 switch 语句。当 switch 所有的 case 都不满足时，将进入 default 执行。default 只能放在 switch 语句所有的 case 之后，并且是可选的。

**13. delete**

delete（删除）释放程序动态申请的内存空间。delete 后面通常是一个指针或者数组 []，并且只能 delete 通过 new 关键字申请的指针，否则会发生段错误。

**14. do**

do-while是一类循环结构。与while循环不同，do-while循环保证至少要进入循环体一次。

**15. double**

double（双精度）类型，C++ 中的基本数据结构，以双精度形式存储一个浮点数。

**16. dynamic_cast**

dynamic_cast（动态转换），允许在运行时刻进行类型转换，从而使程序能够在一个类层次结构安全地转换类型。dynamic_cast 提供了两种转换方式，把基类指针转换成派生类指针，或者把指向基类的左值转换成派生类的引用。

**17. else**

else 紧跟在 if 后面，用于对 if 不成立的情况的选择。

**18. enum**

enum（枚举）类型，给出一系列固定的值，只能在这里面进行选择一个。

**19. explicit**

explicit（显式的）的作用是"禁止单参数构造函数"被用于自动型别转换，其中比较典型的例子就是容器类型。在这种类型的构造函数中你可以将初始长度作为参数传递给构造函数。

**20. export**

为了访问其他编译单元（如另一代码文件）中的变量或对象，对普通类型（包括基本数据类、结构和类），可以利用关键字 extern，来使用这些变量或对象时；但是对模板类型，则必须在定义这些模板类对象和模板函数时，使用标准 C++ 新增加的关键字 export（导出）。

**21. extern**

extern（外部的）声明变量或函数为外部链接，即该变量或函数名在其它文件中可见。被其修饰的变量（外部变量）是静态分配空间的，即程序开始时分配，结束时释放。用其声明的变量或函数应该在别的文件或同一文件的其它地方定义（实现）。在文件内声明一个变量或函数默认为可被外部使用。在 C++ 中，还可用来指定使用另一语言进行链接，这时需要与特定的转换符一起使用。目前仅支持 **C** 转换标记，来支持 C 编译器链接。使用这种情况有两种形式：

```
extern "C" 声明语句

extern "C" { 声明语句块 }
```



**22. false**

false（假的），C++ 的基本数据结构 bool 类型的值之一。等同于 int 的 0 值。

**23. float**

float（浮点数），C++ 中的基本数据结构，精度小于 double。

**24. for**

for 是 C++ 中的循环结构之一。

**25. friend**

friend（友元）声明友元关系。友元可以访问与其有 friend 关系的类中的 private/protected 成员，通过友元直接访问类中的 private/protected 成员的主要目的是提高效率。友元包括友元函数和友元类。

**26. goto**

goto（转到），用于无条件跳转到某一标号处开始执行。

**27. if**

if（如果），C++ 中的条件语句之一，可以根据后面的 bool 类型的值选择进入一个分支执行。

**28. inline**

inline（内联）函数的定义将在编译时在调用处展开。inline 函数一般由短小的语句组成，可以提高程序效率。

**29. int**

int（整型，integer），C++ 中的基本数据结构，用于表示整数，精度小于 long。

**30. long**

long（长整型，long integer），C++ 中的基本数据结构，用于表示长整数。

**31. mutable**

mutable（易变的）是 C++ 中一个不常用的关键字。只能用于类的非静态和非常量数据成员。由于一个对象的状态由该对象的非静态数据成员决定，所以随着数据成员的改变，对像的状态也会随之发生变化。如果一个类的成员函数被声明为 const 类型，表示该函数不会改变对象的状态，也就是该函数不会修改类的非静态数据成员。但是有些时候需要在该类函数中对类的数据成员进行赋值，这个时候就需要用到 mutable 关键字。

**32. namespace**

namespace（命名空间）用于在逻辑上组织类，是一种比类大的结构。

**33. new**

new（新建）用于新建一个对象。new 运算符总是返回一个指针。由 new 创建

**34. operator**

operator（操作符）用于操作符重载。这是 C++ 中的一种特殊的函数。

**35. private**

private（私有的），C++ 中的访问控制符。被标明为 private 的字段只能在本类以及友元中访问。

**36. protected**

protected（受保护的），C++ 中的访问控制符。被标明为 protected 的字段只能在本类以及其继承类和友元中访问。

**37. public**

public（公有的），C++ 中的访问控制符。被标明为 public 的字段可以在任何类

**38.register**

register（寄存器）声明的变量称着寄存器变量，在可能的情况下会直接存放在机器的寄存器中；但对 32 位编译器不起作用，当 global optimizations（全局优化）开的时候，它会做出选择是否放在自己的寄存器中；不过其它与 register 关键字有关的其它符号都对32位编译器有效。

**39. reinterpret_cast**

用法：

```
reinpreter_cast<type-id> (expression)
```

type-id 必须是一个指针、引用、算术类型、函数指针或者成员指针。它可以把一个指针转换成一个整数，也可以把一个整数转换成一个指针（先把一个指针转换成一个整数，在把该整数转换成原类型的指针，还可以得到原先的指针值）。

**40. return**

return（返回）用于在函数中返回值。程序在执行到 return 语句后立即返回，return 后面的语句无法执行到。

**41. short**

short（短整型，short integer），C++ 中的基本数据结构，用于表示整数，精度小于 int。

**42. signed**

signed（有符号），表明该类型是有符号数，和 unsigned 相反。数字类型（整型和浮点型）都可以用 signed 修饰。但默认就是 signed，所以一般不会显式使用。

**43. sizeof**

由于 C++ 每种类型的大小都是由编译器自行决定的，为了增加可移植性，可以用 sizeof 运算符获得该数据类型占用的字节数。

**44. static**

static（静态的）静态变量作用范围在一个文件内，程序开始时分配空间，结束时释放空间，默认初始化为 0，使用时可改变其值。静态变量或静态函数，只有本文件内的代码才可访问它，它的名字（变量名或函数名）在其它文件中不可见。因此也称为"文件作用域"。在 C++ 类的成员变量被声明为 static（称为静态成员变量），意味着它被该类的所有实例所共享，也就是说当某个类的实例修改了该静态成员变量，其修改值为该类的其它所有实例所见；而类的静态成员函数也只能访问静态成员（变量或函数）。类的静态成员变量必须在声明它的文件范围内进行初始化才能使用，private 类型的也不例外。

**45. static_cast**

用法：

```
static_cast < type-id > ( expression ) 
```

该运算符把 expression 转换为 type-id 类型，但没有运行时类型检查来保证转换的安全性。它主要有如下几种用法：

- ① 用于类层次结构中基类和子类之间指针或引用的转换。进行上行转换（把子类的指针或引用转换成基类表示）是安全的；进行下行转换（把基类指针或引用转换成子类表示）时，由于没有动态类型检查，所以是不安全的。
- ② 用于基本数据类型之间的转换，如把 int 转换成 char，把 int 转换成 enum。这种转换的安全性也要开发人员来保证。
- ③ 把空指针转换成目标类型的空指针。
- ④ 把任何类型的表达式转换成void类?

**注意** static_cast 不能转换掉 expression 的 const、volitale、或者 __unaligned 属性。

**46. struct**

struct（结构）类型，类似于 class 关键字，与 C 语言兼容（class 关键字是不与 C 语言兼容的），可以实现面向对象程序设计。

**47. switch**

switch（转换）类似于 if-else-if 语句，是一种多分枝语句。它提供了一种简洁的书写，并且能够生成效率更好的代码。但是，switch 后面的判断只能是int（char也可以，但char本质上也是一种int类型）。switch 语句最后的 default 分支是可选的。

**48. template**

template（模板），C++ 中泛型机制的实现。

**49. this**

this 返回调用者本身的指针。

**50. throw**

throw（抛出）用于实现 C++ 的异常处理机制，可以通过 throw 关键字"抛出"一个异常。

**51. true**

true（真的），C++ 的基本数据结构 bool 类型的值之一。等同于 int 的非 0 值。

**52. try**

try（尝试）用于实现 C++ 的异常处理机制。可以在 try 中调用可能抛出异常的函数，然后在 try 后面的 catch 中捕获并进行处理。

**53. typedef**

typedef（类型定义，type define），其格式为：

```
typedef  类型 定义名;
```

类型说明定义了一个数据类型的新名字而不是定义一种新的数据类型。定义名表示这个类型的新名字。

**54. typeid**

指出指针或引用指向的对象的实际派生类型。

**55. typename**

typename（类型名字）关键字告诉编译器把一个特殊的名字解释成一个类型。在下列情况下必须对一个 name 使用 typename 关键字：

- 1． 一个唯一的name（可以作为类型理解），它嵌套在另一个类型中的。
- 2． 依赖于一个模板参数，就是说：模板参数在某种程度上包含这个name。当模板参数使编译器在指认一个类型时产生了误解。

**56. union**

union（联合），类似于 enum。不同的是 enum 实质上是 int 类型的，而 union 可以用于所有类型，并且其占用空间是随着实际类型大小变化的。

**57. unsigned**

unsigned（无符号），表明该类型是无符号数，和 signed 相反。

**58. using**

表明使用 namespace。

**59. virtual**

virtual（虚的），C++ 中用来实现多态机制。

**60. void**

void（空的），可以作为函数返回值，表明不返回任何数据；可以作为参数，表明没有参数传入（C++中不是必须的）；可以作为指针使用。

**61. volatile**

volatile（不稳定的）限定一个对象可被外部进程（操作系统、硬件或并发线程等）改变，声明时的语法如下：

```
int volatile nVint;
```

这样的声明是不能达到最高效的，因为它们的值随时会改变，系统在需要时会经常读写这个对象的值。因此常用于像中断处理程序之类的异步进程进行内存单元访问。

**62. wchar_t**

wchar_t 是宽字符类型，每个 wchar_t 类型占 2 个字节，16 位宽。汉字的表示就要用到 wchar_t。







### 标识符命名规则


**作用:**C++规定给标识符（变量、常量）命名时，有一套自己的规则

+ 标识符不可以是关键字
+ 标识符是由字母、数字、下划线构成
+ 标识符第一个字符只能是字母或下划线
+ 标识符是区分大小写的

**建议：** 给标识符命名时，争取做到见名知意的效果，方便阅读

























## 数据类型
作用：给变量分配合适的内存空间
** C++**规定在创建一个变量或者常量时

### 整形
### sizeof关键字

**sizeof是一个操作符**

不过其使用方式看起来的确太像一个函数了

语句sizeof(int)就可以说明sizeof的确不是一个函数，因为函数接纳形参（一个变量），世界上没有一个C/C++函数接纳一个数据类型（如int）为"形参"。








### 实型（浮点型）
**作用**:表示小数
浮点型变量分为两种：

+ 单精度 float
+ 双精度double

| 数据类型 | 占用空间 |  有效数字范围   |
| :------: | :------: | :-------------: |
|  float   |  4字节   |   7位有效数字   |
|  double  |  8字节   | 15-16位有效数字 |

**示例**

```c++
#include<iostream>
using namespace std;
int main()
{

	//双精度float
	//单精度double
	float k1 = 3.1415926535f;  //数字后面不写f会默认double类型
	cout << "k1= " << k1 << endl;
	double d1 = 3.1415926535;
	cout << "d1= " << d1 << endl;
    //输出均为3.14159
```



**关于有效数字**

```c++
#include<iostream>
using namespace std;
int main()
{

	double d1 = 3.1415926535;
	//cout 默认输出6位有效数字
	cout << d1 << endl;
	//修改输出精度为9位有效数字
	cout.precision(9);
	cout << d1 << endl;
	//如果想让这个精度表示小数点后的位数
	cout.flags(cout.fixed);//定点法
	cout << d1 << endl;
	cout.unsetf (cout.fixed);//取消定点法
	cout << d1 << endl;
	system ("pause");
	return 0;
}

//输出结果
3.14159
3.14159265
3.141592654
3.14159265
```



**科学计数法**

```c++
//输出0.03和300
#include"math.h"
#include<iostream>
using namespace std;
int main()
{
//科学记数法
	double a = 3e-2;//3*0.1^2
	cout << a << endl;
	double b = 3e2;//3*10^2
	cout << b << endl;
}
```





### 字符型

**作用**：字符型变量用于显示单个字符

**语法**：

```c++
char ch='a'
```

+ 在显示字符型变量时，用单引号将字符括起来，不要用双引号
+ 单引号内只能有一个字符，不可以是字符串
+ c和c++中字符型变量只占1个字节
+ 字符型变量不是把字符本身放到内存中存储，而是将对应的ASCII码放到存储单元



```c++

#include"math.h"
#include<iostream>
using namespace std;
int main()
{
	//字符型变量创建方式
	char ch = 'a';
	cout << ch << endl;
	//字符型变量所占内存大小
	int b;
	b=sizeof(char);
	cout << b << endl;
	//字符型变量常见错误
	char ch2 = "b";//创建字符型变量时，要用单引号
	char ch3 = 'abcdef';//创建字符型变量时，单引号内只能有一个字符

	//字符型变量对应的ASCII码
	//a-97
	//A-65
	cout << (int)ch << endl;//强制将字符型变量a转为整形
    //直接用ASCII码得到字符
    //方法一
	char ch = 97;
	cout << ch << endl;//输出结果为a
    //方法二
    int ch = 97;
	cout << (char)ch << endl;//强制将整型变量a转为字符型
```



### 转义字符

**作用：**用于表示一些不能显示出来的ASCII字符（本质上还是字符串

```c++
#include<iostream>
using namespace std;
int main()
{
	//换行符
	cout << "hello world" << endl;
	cout << "hello world\n";
	cout << "hello world" <<"\n";
	//cout << "hello world" <<'\n' ;直接报错，因为\n是字符串
	cout << "hello world" <<'n' << endl;
	// 反斜杠
	cout << "\\n" << endl;//输出\n
	//cout <<"\" << endl;   无法输出，第一个\告诉后面的要输出一个特殊字符（如\
	cout << "hello \world" << endl;//输出hello world
	cout << "hello \\world" << endl;//输出hello \world
	//水平制表符(有对齐作用
	cout << "aaa\thelloworld" << endl;
	cout << "aaaa\thelloworld" << endl;
	cout << "aaa \thelloworld" << endl;
	cout << "aaaaaaaaaaa\thello world" << endl;
	system("pause");
	return 0;
}
```

输出结果

```c++
hello world
hello world
hello world
hello worldn
\n
hello \world
aaa     helloworld
aaaa    helloworld
aaa     helloworld
aaaaaaaaaaa     hello world
```



### 字符串型

**作用：**用于表示一串字符

1.c风格字符串：(不能忘记”  “）

```c++
char 变量名[]="字符串型"
```

2.c++风格字符串：（需要包含头文件#include<string>）

```c++
string 变量名="字符串值"
```

```c++
#include<iostream>
using namespace std;
#include<string>  //c++风格必须要的
int main()
{
	//1、c风格字符串
	//注意事项 char 字符串名 []
	//注意事项2 等号后面要用双引号包含起来字符串
	char str[] = "hello world";
	cout << str << endl;
    //2、c++风格字符串
	//包含一个头文件  #include<string>
	string str2 = "hello world";
	cout << str2 << endl;
	system("pause");
	return 0;
}
```



### 布尔类型bool



```c++
#include<iostream>
using namespace std;
#include<string>  
int main()
{
	//1.创建bool数据类型
	bool flag = true;
	cout << flag << endl;
	flag = false;
	cout << flag << endl;
	//2.查看bool类型所占内存空间
	cout << sizeof(bool) << endl;
	system("pause");
	return 0;
}
//输出
1
0
1
```



### 数据的输入

**作用：**用于从键盘中获取数据

**关键字**：bin

**语法：**

```c++
cin>>变量；
```

```c++
#include<iostream>
using namespace std;
#include<string>  
int main()
{
//整型
	int a = 0;
	cout << "请给整型变量a赋值" << endl;
	cin >> a;
	cout << a << endl;
//浮点型
	float a = 3.13f;
	cin >> a;
	cout << a << endl;
//字符串型
	string ch = "world";
	cin >> ch;
	cout << ch << endl;
	char str[] = "world";
	cin >> str;
	cout << str << endl;
//字符串型
	char c = 'a';
	cin >> c;
	cout << c << endl;
//布尔类型
	bool flag = false;
	cin >> flag;//bool类型只要是非0的就代表真(输出1)
	cout << flag << endl;
	system("pause");
	return 0;
}

```





## c++格式化输出，c++格式化输出控制（摆脱cout6位的控制）

[C++输入cout与输出cin_C语言中文网 (biancheng.net)](http://c.biancheng.net/cpp/biancheng/view/116.html)

[C++格式化输出，C++输出格式控制_C语言中文网 (biancheng.net)](http://c.biancheng.net/cpp/biancheng/view/2227.html)

 **作用：**在输出数据时，为简便起见，往往不指定输出的格式，由系统根据数据的类型采取默认的格式，但有时希望数据按指定的格式输出，如要求以十六进制或八进制形式输出一个 整数，对输出的小数只保留两位小数等。有两种方法可以达到此目的。一种是使用控制符的方法，第二种是使用流对象的有关成员函数。

  ### 基本的输入&输出函数

  ```c++
  #include <iostream>
  #include <iomanip>
  using namespace std;
  int main()
  {
      cout<<setiosflags(ios::left|ios::showpoint);  // 设左对齐，以一般实数方式显示
      cout.precision(5);       // 设置除小数点外有五位有效数字 
      cout<<123.456789<<endl;
      cout.width(10);          // 设置显示域宽10 
      cout.fill('*');          // 在显示区域空白处用*填充
      cout<<resetiosflags(ios::left);  // 清除状态左对齐
      cout<<setiosflags(ios::right);   // 设置右对齐
      cout<<123.456789<<endl;
      cout<<setiosflags(ios::left|ios::fixed);    // 设左对齐，以固定小数位显示
      cout.precision(3);    // 设置实数显示三位小数
      cout<<999.123456<<endl; 
      cout<<resetiosflags(ios::left|ios::fixed);  //清除状态左对齐和定点格式
      cout<<setiosflags(ios::left|ios::scientific);    //设置左对齐，以科学技术法显示 
      cout.precision(3);   //设置保留三位小数
      cout<<123.45678<<endl;
      return 0; 
  }
  ```

### 控制符
### 流对象的有关成员函数



























## 运算符

### 算数运算符

**作用：**用于处理四则运算

| 运算符 | 术语         | 实例       | 结果    |
| ------ | ------------ | ---------- | ------- |
| +      | 正号         | +3         | 3       |
| -      | 负号         | -3         | -3      |
| +      | 加           | 10+5       | 15      |
| -      | 减           | 10-5       | 5       |
| *      | 乘           | 10*5       | 50      |
| /      | 除           | 10/5       | 2       |
| %      | 取模（取余） | 10%3       | 1       |
| ++     | 前置递增     | a=2;b=++a; | a=3;b=3 |
| ++     | 后置递增     | a=2;b=a++; | a=3;b=2 |
| --     | 前置递减     | a=2;b=--a; | a=1;b=1 |
| --     | 后置递减     | a=2;b=a--; | a=1;b=2 |

eg：

```c++
#include<iostream>
using namespace std;
int main()
{
//加减乘除
	int a = 10;
	int b = 3;
	cout << a + b << endl;
	cout << a - b << endl;
	cout << a * b << endl;
	cout << a / b << endl;//两个整数相除结果依然是整数，将小数部分去除
	int a1 = 10;
	int b1 = 20;//输出0
	cout << a1 / b1 << endl;
	int a3 = 10;
	int b3 = 0;
	//cout << a3 / b3 << endl;//两个数字相除除数不能为0；无法输出，非法操作
//两个小数可以相除吗
	double d1 = 0.5;
	double d2 = 0.22;
	cout << d1 / d2 << endl;//运算结果也可以是小数，还是保持6位原则
	system("pause");
	return 0;
}
```

```c++
#include<iostream>
using namespace std;
int main()
{
	int a = 10;
	int b = 20;
	cout << a % b << endl;//结果为10
	int a1 = 10;
	int a2 = 0;
	//两个数相除除数不可以为0，所以也做不了取模运算
	cout << a1 % a2 << endl;//输出错误
	//c++中两个小数是不可以做取模运算的
	double d1 = 3.14;
	double d2 = 1.1;
	cout << d1 % d2 << endl;
	system("pause");
	return 0;
}
```

```c++
#include<iostream>
using namespace std;
int main()
{
//前置递增
	int a = 10;
	++a;//让变量+1；
	cout << a << endl;
//后置递增
	int b = 10;
	b++;//让变量+1；
	cout << b << endl;
//前置后置的区别
	//前置递增 先让变量+1 然后进行表达式运算
	int a1 = 10;
	int b1 = ++a1 * 10;
	cout << "a1=" << a1 << endl;
	cout << "b1=" << b1 << endl;
	//后置递增 先进行表达式运算，后让变量+
	int a2 = 10;
	int b2 = a2++ * 10;
	cout << "a2=" << a2 << endl;
	cout << "b2=" << b2 << endl;
	system("pause");
	return 0;
}
/*输出结果
11
11
a1=11
b1=110
a2=11
b2=100*/
```



### 赋值运算符

| 运算符 | 术语 | 示例 | 结果 |
| ------ | ---- | ---- | ---- |
| =      |      |      |      |
| +=     |      |      |      |
| -=     |      |      |      |
| *=     |      |      |      |
| /=     |      |      |      |
| %=     |      |      |      |



```c++
#include<iostream>
using namespace std;
int main()
{
	//=
	int a = 10;
	a = 100;
	cout << "a=" << a << endl;
	//+=
	a = 10;
	a += 2;//a=a+2
	cout << "a=" << a << endl;
	//-=
	a = 10;
	a -= 2;//a=a-2
	cout << "a=" << a << endl;
	//*=
	a = 10;
	a *= 2;
	cout << "a=" << a << endl;
	//  /=
	a = 10;
	a /= 2;
	cout << "a=" << a << endl;
	//%=
	a = 10;
	a %= 2;
	cout << "a=" << a << endl;
	system("pause");
	return 0;
}
/*输出结果
a=100
a=12
a=8
a=20
a=5
a=0*/
```



### 比较运算符

**作用：**用于表达式的比较，并返回一个真值或假值；

比较运算符有以下符号：

| 运算符 | 术语 | 示例 | 结果 |
| ------ | ---- | ---- | ---- |
| ==     |      |      |      |
| ！=    |      |      |      |
| <      |      |      |      |
| >      |      |      |      |
| <=     |      |      |      |
| >=     |      |      |      |



```c++
#include<iostream>
using namespace std;
int main()
{
	int a = 10, b = 20;
	//==
	//cout << a == b << endl;(出错)
	cout << (a == b) << endl;
	//!=
	cout << (a != b) << endl;
	//>
	cout << (a > b) << endl;
	//<
	cout << (a < b) << endl;
	//>=
	cout << (a >= b) << endl;
	//<=
	cout << (a <= b) << endl;
	system("pause");
	return 0;
}
/*输出结果0
1
0
1
0
1*/
```



### 逻辑运算符

作用:用于根据表达式的值返回真值或假值

逻辑运算符有以下符号：

| 运算符 | 术语 | 示例 | 结果 |
| ------ | ---- | ---- | ---- |
| ！     |      |      |      |
| &&     |      |      |      |
| \|\|   |      |      |      |

示例1：逻辑非

```c++
#include<iostream>
using namespace std;
int main()
{
	//逻辑运算符非！
	int a = 10;
	//在c++中  除了0都是真
	cout << !a << endl;//输出0
	cout << !!a << endl;//输出1
	system("pause");
	return 0;
}
```

示例2：逻辑与

```c++
#include<iostream>
using namespace std;
int main()
{
	//逻辑运算符与&&
	int a = 10, b = 20, c = 0;
	//在c++中  除了0都是真
	cout << (a&&b) << endl;//输出1
	cout << (a&&c) << endl;//输出0
	cout << (c && a) << endl;//输出0
	cout << (c && c) << endl;//输出0
	system("pause");
	return 0;
}
```

示例3：逻辑或

```c++
#include<iostream>
using namespace std;
int main()
{
	//逻辑运算符与||
	int a = 10, b = 20, c = 0;
	//在c++中  除了0都是真
	cout << (a||b) << endl;//输出1
	cout << (a||c) << endl;//输出1
	cout << (c || a) << endl;//输出1
	cout << (c || c) << endl;//输出0
	system("pause");
	return 0;
}

```



## 程序流程结构

C/C++支持最基本的三种程序运行结构：==顺序结构、选择结构、循环结构==

+ 顺序结构：程序按顺序执行，不发生跳转
+ 选择结构：依据条件是否满足，有选择地执行相应功能
+ 循环结构：依据条件是否满足，循环多次执行某代码



### 选择结构

#### if语句

**作用**：执行满足条件的语句

if语句的三种形式

+ 单行格式if语句

  `if（条件）{条件满足后执行的语句}`

  ```c++
  #include<iostream>
  using namespace std;
  int main()
  {
  	//选择结构 if语句（单行
  	//用户输入分数大于600，输出
  	int score = 0;
  	cout << "请输入一个分数" << endl;
  	cin >> score;
  	//注意事项，if条件后面不要加分号“；”
  	if (score >= 600) { cout << "恭喜您考上了一本大学" << endl; }
  }
  ```

+ 多行格式if语句

`if(条件){条件满足执行的语句}else{否则执行的语句}`

```c++
#include<iostream>
using namespace std;
int main()
{
	//选择结构 if语句（多行
	//用户输入分数大于600，输出
	int score = 0;
	cout << "请输入一个分数" << endl;
	cin >> score;
	//注意事项，if条件后面不要加分号“；”
	if (score >= 600) 
	{
		cout << "恭喜您考上了一本大学" << endl;
	}
	else
	{
		cout << "未考上一本" << endl;
	}
}
```



+ 多条件的if语句

`if(条件1){条件1满足执行的语句}else if（条件2）{条件2满足执行的语句}...else{都不满足执行的语句}`

```c++
#include<iostream>
using namespace std;
int main()
{
	//选择结构 if语句（多行
	int score = 0;
	cout << "请输入一个分数" << endl;
	cin >> score;
	//注意事项，if条件后面不要加分号“；”
	if (score >= 600) 
	{
		cout << "恭喜您考上了一本大学" << endl;
	}
	else if(score>=500)
	{
		cout << "考上二本" << endl;
	}
	else if (score>=400)
	{
		cout << "考上三本" << endl;
	}
	else
	{
		cout << "名落孙山" << endl;
	}
	system("pause");
	return 0;
}
```

+ 嵌套if语句：可以嵌套使用if语句，达到更精准的条件判断

  案例需求：

  + 提示用户输入一个高考考试分数，根据分数做出如下判断

  + 分数如果大于600分视为考上一本，大于500分考上二本，大于400分考上三本，其余视为未考上本科

  + 在一本分数中，如果大于700分，考入北大，大于650分，考入清华，大于600考入人大

示例：

```c++
#include<iostream>
using namespace std;
int main()
{
	//选择结构 if语句（嵌套
	int score = 0;
	cout << "请输入高考考试分数" << endl;
	cin >> score;
	//注意事项，if条件后面不要加分号“；”
	if (score >= 600) 
	{
		if(score>700)
		{
			cout << "恭喜您考上了北大" << endl;
		}
		else if(score>650)
		{cout << "恭喜您考上了清华" << endl; }
	    else { cout << "恭喜您考入人大" << endl; }
	}
	else if(score>=500)
	{
		cout << "考上二本" << endl;
	}
	else if (score>=400)
	{
		cout << "考上三本" << endl;
	}
	else
	{
		cout << "名落孙山" << endl;
	}
	system("pause");
	return 0;
}
```

**练习案例：**

**比较数的大小问题：**给你三个数A,B,C，找到最大的那个数

```c++
#include<iostream>
using namespace std;
int main()
{
	//求最大的数
	double A=0, B=0, C=0;
	cout << "请输入A,B,C对应的值" << endl;
	cin >> A, B, C;
	double max;
	if (A >= B)
	{
		max = A;
	}
	else
		max = B;
	if (max >= C)
		max = max;
	else
		max = C;
	cout << "最大的数为:" << max << endl;
	system("pause");
	return 0;
}
```

#### 三目运算符

**作用**：通过三目运算符实现简单的判断

**语法**：`表达式1？表达式2：表达式3`

**解释：**

如果表达式1的值为真，执行表达式2，并返回表达式2的结果；

如果表达式1的值为假，执行表达式3，并返回表达式3的结果；

**示例**：

```c++
#include<iostream>
using namespace std;
int main()
{
	//三目运算符
	//创建三个变量a b c
	//将a和b比较，将变量大的值赋值给变量c
	int a=20, b=30, c=0;
	c = (a > b ? a : b);
	cout << c << endl;
	//在c++中三目运算符返回的是变量，可以继续赋值
	a > b ? a : b = 100;//最大值对应的变量赋予100
	system("pause");
	return 0;
}
```

#### switch语句

**作用：**执行多条件分支语句

**语法：**case后面的结果不要逻辑运算

```c++
switch（表达式）
{
    case 结果1：执行语句;break;
        
    case 结果2：执行语句;break;
    
    '''
    
    default:执行语句;break;
}
```

一个 **switch** 语句允许测试一个变量等于多个值时的情况。每个值称为一个 case，且被测试的变量会对每个 **switch case** 进行检查。

C++ 中 **switch** 语句的语法：

```c++
switch(expression){
    case constant-expression  :
       statement(s);
       break; // 可选的
    case constant-expression  :
       statement(s);
       break; // 可选的
  
    // 您可以有任意数量的 case 语句
    default : // 可选的
       statement(s);
}
```

**switch** 语句必须遵循下面的规则：

- **switch** 语句中的 **expression** 必须是**一个整型或枚举类型**，或者是一个 class 类型，其中 class 有一个单一的转换函数将其转换为整型或枚举类型。

- 在一个 switch 中可以有任意数量的 case 语句。每个 case 后跟一个要比较的值和一个冒号。

- case 的 **constant-expression** 必须与 switch 中的变量具有相同的数据类型，且必须是一个常量或字面量。

- 当被测试的变量等于 case 中的常量时，case 后跟的语句将被执行，直到遇到 **break** 语句为止。

- 当遇到 **break** 语句时，switch 终止，控制流将跳转到 switch 语句后的下一行。

- 不是每一个 case 都需要包含 **break**。如果 case 语句不包含 **break**，控制流将会 *继续* 后续的 case，直到遇到 break 为止。

- 一个 **switch** 语句可以有一个可选的 **default** case，出现在 switch 的结尾。default case 可用于在上面所有 case 都不为真时执行一个任务。default case 中的 **break** 语句不是必需的。

  示例

  ```c++
  #include<iostream>
  using namespace std;
  int main()
  {
  	//switch语句
  	//给电影打分
  	//10-9经典
  	//8-7非常好
  	//6-5一般
  	//5以下烂片
  	//提示用户给电影评分
  	cout << "请输入您的评分" << endl;
  	//用户进行打分
  	int score = 0;
  	cin >> score;
  	cout << "您打的分数为" << score << endl;
  	//根据用户的输入分数来提示用户最后的结果
  
  	switch (score)
  	{
  	case 10:
  		cout << "您认为是经典电影" << endl;
  		break;//退出当前分支
  	case 9:
  		cout << "您认为是经典电影" << endl;
  		break;
  	case 8:
  		cout << "您认为电影非常好" << endl;
  		break;
  	case 7:
  		cout << "您认为电影非常好" << endl;
  		break;
  	case 6 :
  		cout << "您认为电影一般" << endl;
  		break;
  	case 5 :
  		cout << "您认为电影一般" << endl;
  		break;
  	//case 6||5:
  		//cout << "您认为电影很一般" << endl;
  		//break;
  	default:
  		cout << "烂中烂" << endl;
  		break;
  	}
  	system("pause");
  	return 0;
  }
  //if和switch区别
  //switch 缺点：判断的时候只能是整型或者字符型，不可以是一个区间
  //switch 优点：结构清晰，执行效率高
  ```

### 循环结构

#### while循环语句

**作用**：满足循环条件，执行循环语句

**语法**：`while（循环条件）{循环语句}`

**解释**：只要循环条件的结果为真，就执行循环语句

```c++
#include<iostream>
using namespace std;
int main()
{
	//while循环
	//在屏幕上打印0-9这10个数
	int i = 0;
	//while()中输入循环条件
    //注意事项：在写循环一定要避免死循环
	while ( i <= 9)
	{
		cout << i << endl;
		i++;
	}
	system("pause");
	return 0;
}
```



==while循环练习案例：猜数字==

**案例描述**：系统随机生成一个1到100之间的数字，玩家进行猜测，提示玩家数字过大或过小，如果猜对，恭喜玩家胜利，并且退出游戏。

```c++
#include<iostream>
//time系统时间头文件包含
#include<ctime>
using namespace std;
int main()
{
	//添加随机数种子 利用当前系统时间生成随机数，防止每次随机数都一样
	srand((unsigned int)time(NULL);
	//系统生成随机数
	int num=rand() % 100 + 1;//rand()%100生成0-99的随机数
	//玩家进行猜测
	int val = 0;//玩家输入的数据

	//判断玩家的猜测
	while(1)
	{ 
	cin >> val;
	if (val > num)
	{
		cout << "猜测过大" << endl;
	}
	else if (val < num)
	{
		cout << "猜测过小" << endl;
	}
	else
	{
		cout << "win" << endl;
		break;//break，可以利用该关键字来退出当前循环
	}
	}
	//猜对    退出游戏

	//猜错    提示猜的结果  过大或过小   重新返回第二步
	system("pause");
	return 0;
}
```

**提炼**：

+ 伪随机数

```c++
rand()%100;
```

+ 引入时间，成为完全随机数

 ```c++
  #include<ctime>
 srand(unsigned int)time(NULL);
 int rand()&100；
 ```

#### do...while 循环语句

**作用**：满足循环条件，执行循环语句

**语法**：`do{循环语句}while(循环条件)`

**注意** ：与while的区别在于do...while会先执行一次循环语句，再判断循环条件

```c++
#include<iostream>
//time系统时间头文件包含
#include<ctime>
using namespace std;
int main()
{
	//do...while语句
	//在屏幕中输出0-9这10个数字

	int num = 0;
	do
	{
		cout << num << endl;
		num++;
	} 
    while (num < 10);
    //与while的区别在于do...while会先执行一次循环语句，再判断循环条件
	system("pause");
	return 0;
}
```

**练习案例**：水仙花数

案例描述：水仙花数是指一个3位数，它的每个位上的数字的3次幂之和等于它本身

例如：1^3 +5^3 +3^3=153

请用do...while语句，求出所有3位数中的水仙花数

```c++
#include<iostream>
using namespace std;
int main()
{
	int num = 100;
	do
	{
		if (num == pow(num % 10, 3) + pow((num / 10 % 10), 3) + pow(num / 100, 3))
		{
			cout << num << endl;
		}
		num++;
	} 
	while (num<1000 );
	system("pause");
	return 0;
}
//得到四个水仙花数
153
370
371
407
```

#### for循环语句

**作用：**满足循环条件，执行循环语句

**语法**：`for(起始表达式；条件表达式；末尾循环式){循环语句；}`

```c++
#include<iostream>
using namespace std;
int main()
{
	//for循环
	//从数字0打印到数字9
	for (int i = 0;i<10;i++)
	{
		cout << i << endl;
	}
	//拆分for
	int i = 0;
	for (; ; )
	{
		if (i>=10)
		{
			break;
		}
		cout << i << endl;
		i++;
	}
	system("pause");
	return 0;
}
```

练习案例：敲桌子

案例描述：从1开始数到数字100，如果数字个位含有7，或者十位含有7，或者该数字是7的倍数，我们打印敲桌子，其余数字直接打印输出。

```c++
#include<iostream>
using namespace std;
int main()
{
	for (int i = 1;i<100;i++)
	{
		if (i % 10 == 7 || i / 10 % 10==7 || i % 7 == 0)
		{
			cout << "敲桌子" << endl;
		}
		else
		{ 
		cout << i << endl;
		}
	}
	system("pause");
	return 0;
}
```



#### 嵌套循环

**作用**：在循环体中再嵌套一层循环，解决一些实际问题

```c++
#include<iostream>
using namespace std;
int main()
{
	//利用嵌套循环实现星图
    //外层执行一次，内层执行一周
	for (int i = 0; i < 10; i++)
	{
		for (int j = 0; j < 10; j++)
		{
			cout << "* ";
		}
		cout << "\n";
	}
	system("pause");
	return 0;
}
/*输出结果
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
* * * * * * * * * *
*/
```

案例描述：利用嵌套循环，实现九九乘法表

```c++
#include<iostream>
using namespace std;
int main()
{
	//利用嵌套循环实现九九乘法表
	for (int i = 1; i < 10; i++)
	{
		cout << "|";
		for (int j = 1; j <=i; j++)
		{
			cout<< j << "*" << i << " = " << j * i << "|";
		}
		cout << "\n";
	}
	system("pause");
	return 0;
}
//结果
|1*1 = 1|
|1*2 = 2|2*2 = 4|
|1*3 = 3|2*3 = 6|3*3 = 9|
|1*4 = 4|2*4 = 8|3*4 = 12|4*4 = 16|
|1*5 = 5|2*5 = 10|3*5 = 15|4*5 = 20|5*5 = 25|
|1*6 = 6|2*6 = 12|3*6 = 18|4*6 = 24|5*6 = 30|6*6 = 36|
|1*7 = 7|2*7 = 14|3*7 = 21|4*7 = 28|5*7 = 35|6*7 = 42|7*7 = 49|
|1*8 = 8|2*8 = 16|3*8 = 24|4*8 = 32|5*8 = 40|6*8 = 48|7*8 = 56|8*8 = 64|
|1*9 = 9|2*9 = 18|3*9 = 27|4*9 = 36|5*9 = 45|6*9 = 54|7*9 = 63|8*9 = 72|9*9 = 81|
```

### 跳转结构

#### break语句

**作用**：用于跳出==选择结构==或者==循环结构==

break使用时机

+ 出现在switch条件语句中，作用是终止case并跳出switch

+ 出现在循环语句中，作用是跳出当前的循环语句

+ 出现在嵌套循环中，跳出最近的内层循环语句

示例：

```c++
#include<iostream>
using namespace std;
int main()
{
	//break的使用时机

	//出现在switch语句中
	cout << "请选择副本难度" << endl;
	cout << "1、简单" << endl;
	cout << "2、中等" << endl;
	cout << "3.困难" << endl;
	int select = 0;//创建选择结果的变量
	cin >> select;//等待用户输入
	switch (select)
	{
	case 1:
		cout << "您选择的是普通难度" << endl;
		break;
	case 2:
		cout << "您选择的是中等难度" << endl;
		break;
	case 3:
		cout << "您选择的是困难难度" << endl;
		break;
	defalut:
		break;
	}
	system("pause");
	return 0;
}
```

```c++
#include<iostream>
using namespace std;
int main()
{
	//break的使用时机

	//出现在循环语句中
	for (int i = 0; i < 10; i++)
	{
		if (i > 5) break;
		cout << i << endl;
	}
	system("pause");
	return 0;
}
```

```c++
#include<iostream>
using namespace std;
int main()
{
	//break的使用时机

	//出现在嵌套循环语句中
	for (int i = 0; i < 10; i++)
	{
		for (int j = 0; j < 10; j++)
		{
			//退出内层循环
			if (j == 5)break;
			cout << "* ";
		}
		cout << "\n";
	}
	system("pause");
	return 0;
}
```

#### continue语句

**作用：**在循环语句中，跳过本次循环中尚未执行的语句，继续下一次循环

```c++
#include<iostream>
using namespace std;
int main()
{
	//break的使用时机

	//continue语句
	for (int i = 0; i < 100; i++)
	{
	//如果是奇数输出，偶数不输出
		if (i%2==0)
		{
			continue;//可以筛选条件，执行到此就不再向下执行，执行下一次循环
            //break会退出循环而continue不会
		}
		cout << i << endl;
	}
	system("pause");
	return 0;
}
```

#### goto语句

**作用**：可以无条件跳转语句

**语法**：`goto 标记;`

​          `标记：`

解释：如果标记的名称存在，执行到goto语句时，会跳转到标记的位置

==在程序中不建议使用goto，避免程序混乱==

```c++
#include<iostream>
using namespace std;
int main()
{
	//goto语句
	cout << "1.xxxx" << endl;
	cout << "2.xxxx" << endl;
	goto FLAG;
	cout << "3.xxxx" << endl;
	cout << "4.xxxx" << endl;
	FLAG:
	cout << "5.xxxx" << endl;
	system("pause");
	return 0;
}
//结果
1.xxxx
2.xxxx
5.xxxx
```

## 数组

#### 概述

所谓数组，就是一个集合，里面存放了相同类型的数据元素

特点1：数组中的每个==数据元素都是相同的数据类型==

特点2：数组是由连续的内存位置组成的

#### 一维数组

##### 一维数组定义方式

一维数组定义的三种方式

1`数据类型 数组名[数组长度]`

2`数据类型 数组名 [数组长度]={值1，值2，...}`

3`数据类型 数组名[]={值1，值2..}`

示例

```c++
#include<iostream>
using namespace std;
int main()
{
    //数组
	//1数据类型 数组名[数组长度]
	int arr[5];
	//初始化
	arr[0] = 10;
	arr[1] = 20;
	arr[2] = 30;
	arr[3] = 40;
	arr[4] = 50;
	//访问数据元素
	cout << arr[0] << endl;
	cout << arr[1] << endl;
	cout << arr[2] << endl;
	cout << arr[3] << endl;
	cout << arr[4] << endl;
	cout << arr << endl;
	//2数据类型 数组名[数组长度] = { 值1，值2，... }
	//如果在初始化化数据的时候，没有全部填写完，会用0填补数据
	int arr2[5] = { 10,20,30,40,50 };
	cout << arr2[0] << endl;
	cout << arr2[1] << endl;
	cout << arr2[2] << endl;
	cout << arr2[3] << endl;
	cout << arr2[4] << endl;
	//利用循环  输出数组中的元素
	for (int i = 0; i < 5; i++)
	{
		cout << arr2[i] << endl;
	}
	//3数据类型 数组名[] = { 值1，值2.. }
	//定义数组的时候，必须有初始长度
	int arr3[] = { 90,80,70,60,50,40,30,20 };
	for (int i = 0; i < 8; i++)
	{
		cout << arr3[i] << endl;
	}
    system("pause");
	return 0;
}
```

##### 一维数组名

一维数组名的用途：

1、可以统计整个数组在内存中的长度

2、可以获取数组在内存中的**首地址**

示例：

```c++
#include<iostream>
using namespace std;
int main()
{
	//数组名的用途
	//统计整个数组占用内存的大小
	double arr[10] = { 0,1,2,3,4,5,6,7,8,9 };
	cout << "整个数组所占内存空间为"<<sizeof(arr) << endl;
	cout << "每个元素占用内存空间为" << sizeof(arr[0]) << endl;
	cout << "数组中元素的个数为" << sizeof(arr) / sizeof(arr[0]) << endl;
	//可以通过数组名查看首地址
	cout << "数组的首地址为" << (int)arr << endl;
	cout << "数组中第一个元素的地址为" << (int)&arr[0] << endl;
	cout << "数组中第二个元素的地址为" << (int)&arr[1] << endl;
	//数组名是常量，不可以进行赋值操作
	//arr=10；
	system("pause");
	return 0;
}
```

练习案例1：五只小猪称体重

案例描述：

在一个数组中记录了五只小猪的体重，如int arr[5]={300,350,200,400,250}

找出并打印最重的小猪体重

```c++
#include<iostream>
using namespace std;
int main()
{
	int a[5]={300,350,200,400,250};
	int max = 0;
	for (int i = 0; i < 5; i++)
	{
		if (a[i] >= max)
		{
			max = a[i];
		}
	}
	cout << max << endl;
	system("pause");
	return 0;
}
```

练习案例2：数组元素逆置

案例描述：请声明一个5个元素的素组，并且将元素逆置

(如原数组元素为：1,3,2,5,4逆置后输出为4,5,2,3,1

```c++
#include<iostream>
using namespace std;
int main()
{
//实现数组元素逆置
	int arr[5] = { 1,2,3,4,5 };
	//实现逆置
	//记录起始下标位置
	//记录结束下标位置
	//起始下标和结束下标的元素互换
	//起始位置++结束位置--
	//循环直到起始位置>结束位置
	int start = 0;
	int end = sizeof(arr) / sizeof(arr[0])-1;
	while (start<end)
	{
		int temp = arr[start];
		arr[start] = arr[end];
		arr[end] = temp;
		start++;
		end--;
	}
	for (int i = 0; i < 5; i++)
	{
		cout << arr[i] << endl;
	}
	system("pause");
	return 0;
}
```

##### 冒泡排序

**作用**：最常用的排序算法(最不实用)

```c++
#include<iostream>
using namespace std;
int main()
{
	//利用冒泡排序实现升列
	int arr[9] = { 4,2,8,0,5,7,1,3,9 };
	cout << "排序前" << endl;
	for (int i = 0; i < 9; i++)
	{
		cout << arr[i] << " ";
	}
	cout << '\n';
	//总共排序轮数为 元素个数-1
	for (int i= 0; i < 9 - 1; i++)
	{
		//内层循环对比  次数=元素个数-当前轮数-1
		for (int j = 0; j < 9 - 1; j++)
		{
			//对比交换
			if (arr[j] > arr[j + 1])
			{
				int temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	}
	for (int i = 0; i < 9; i++)
	{
		cout << arr[i] << " ";
	}
}
```



#### 二维数组

二维数组就是在一维数组的基础上再加一个维度

二维数组定义的四种方式

1.`数据类型 数组名[行数] [列数];`

2.`数据类型 数组名[行数][列数]={{数据1，数据2}，{数据3，数据4}}；`

3.`数据类型 数组名[行数][列数]={数据1，数据2，数据3，数据4}；`

4.`数据类型 数组名[][列数]={数据1.数据2，数据3，数据4}；`

建议：==采用第二种更直观，提高代码的可读性==

```c++
#include<iostream>
using namespace std;
int main()
{
	    //1.数据类型 数组名[行数][列数]; 
	int arr[2][3];
	arr[0][0] = 1;
	arr[0][1] = 2;
	arr[0][2] = 3;
	arr[1][0] = 4;
	arr[1][1] = 5;
	arr[1][2] = 6;
		//外层循环打印行数，内存循环打印列数
	for (int i = 0; i < 2; i++)
	{
		for (int j = 0; j < 3; j++)
		{
			cout << arr[i][j] << endl;
		}
	}
		//2.数据类型 数组名[行数][列数] = { {数据1，数据2}，{数据3，数据4} }；
	int arr[2][3] =
	{
		{1,2,3},
		{4,5,6}
	};
		for (int i = 0; i < 2; i++)
		{
			for (int j = 0; j < 3; j++)
			{
				cout << arr[i][j] << endl;
			}
		}
		//3.数据类型 数组名[行数][列数] = { 数据1，数据2，数据3，数据4 }；
	int arr3[2][3] = { 1,2,3,4,5,6 };
	for (int i = 0; i < 2; i++)
	{
		for (int j = 0; j < 3; j++)
		{
		cout << arr[i][j] << endl;
		}
	}
		//4.数据类型 数组名[][列数] = { 数据1.数据2，数据3，数据4 }；
	int arr4[][3] = { 1,2,3,4,5,6 };
	int arr4[2][] = { 1,2,3,4,5,6 };//出错
}
```



##### 二维数组数组名 

+ 查看二维数组所占内存空间
+ 获取二维数组首地址

```c++
#include<iostream>
using namespace std;
int main()
{
	//可以查看占用内存大小
	int arr[2][3] =
	{
		{1,2,3},
		{4,5,6}
	};
	cout << "二维数组所占内存空间为" << sizeof(arr) << endl;
	cout << "二维数组第一行所占用内存为" << sizeof(arr[0]) << endl;
	cout << "二维数组第一个元素所占内存为" << sizeof(arr[0][0]) << endl;
	cout << "二维数组行数为" << sizeof(arr) / sizeof(arr[0]) << endl;
	cout << "二维数组列数为" << sizeof(arr[0]) / sizeof(arr[0][0]) << endl;
	//可以查看二维数组的首地址
	cout <<"二维数组的首地址为"<< (int)arr << endl;
	cout << "二维数组第一行的首地址为" << (int)arr[0] << endl;
	cout << "二维数组第一个数字的首地址为" << (int)&arr[0][0] << endl;
	cout << "二维数组第二行的首地址为" << (int)arr[1] << endl;
}
/*
二维数组所占内存空间为24
二维数组第一行所占用内存为12
二维数组第一个元素所占内存为4
二维数组行数为2
二维数组列数为3
二维数组的首地址为1718613784
二维数组第一行的首地址为1718613784
二维数组第一个数字的首地址为1718613784
二维数组第二行的首地址为1718613796
*/
```



## 函数

### 概述

**作用**：将一段经常使用的代码封装起来，减少重复代码

一个较大的程序，一般分为若干个程序块，每个模块实现特定的功能

### 函数的定义

函数的定义一般分为五个步骤:

1.返回值类型

2.函数名

3.参数列表

4.函数体语句

5.return 表达式

**语法**：

```c++
返回值类型 函数名 (参数列表)
{
    函数体语句；
    return表达式
}
```



示例：

```c++
#include<iostream>
using namespace std;
//整型加法处理器
int add(int num1, int num2)
{
	return num1 + num2;
}
int main()
{
	cout << add(3, 4) << endl;
}
```



+ 返回值类型：一个函数可以返回一个值，在函数定义中
+ 函数名：给函数起个名称
+ 参数列表：使用该函数时，传入的数据
+ 函数体语句：花括号内的代码，函数内需要执行的语句
+ return 表达式：和返回值类型挂钩，函数执行完后，返回相应的数据

### 函数的调用

**功能**：使用定义好的函数

**语法**：`函数名(参数)`

```c++
#include<iostream>
using namespace std;
//函数定义的时候，num1和num2并没有真实的数据，只是一个形式上的参数，简称形参
int add(int num1, int num2)
{
	int sum = num1 + num2;
	cout << num1 << endl;
	return sum;
}
int main()
{
	//main函数中调用add函数
	int a = 10;
	int b = 20;
	//函数调用方法:函数名称（参数）
	//a和b称为实际参数，简称实参
	//当调用函数的时候，实参的值会传递给形参
	int c = add(a, b);
	cout << c << endl;
}

```



### 值传递

+ 所谓值传递，就是函数调用时实参将数值传给形参

+ 值传递时，==如果形参发生，不会影响实参==

示例：

```c++
#include<iostream>
using namespace std;
//值传递
//定义函数，
//如果一个函数不需要返回值，声明的时候可以写void
void swap(int a, int b)
{
	int temp;
	temp = a;
	a = b;
	b = temp;
	cout << a << endl;
	cout << b << endl;
	//return;返回值不需要的时候可以不写retur
}
int main()
{
	int a = 1, b = 2;
	swap(a, b);
	//当我们做值传递的时候，函数的形参发生改变都不会影响实参
	cout << a << endl;
	cout << b << endl;
	system("pause");
	return 0;
}

结果：
2
1
1
2

```

### 函数的常见样式

常见的函数样式有4种：

1.无参无返

2.有参无返

3.无参有返

4,有参有返

```c++
#include<iostream>
using namespace std;
	//函数的常见样式
	//1.无参无返
void text01()
{
	cout << "this is text01" << endl;
}

	//2.有参无返
void text02(int a)
{
	cout << "this is test02=" << a << endl;
}
	//3.无参有返
int text03()
{
	cout << "this is text03" << endl;
	return 100;
}
	//4.有参有返
int text04(int a)
{
	cout << "this is text04" << endl;
	return a;
}
int main()
{
	//无参无返函数调用
	text01();
	//有参无返调用
	text02(1);
	//无参有返调用
	int num1 = text03();
	cout << num1 << endl;
	//有参有返调用
	int num2=text04(1000);
	cout << num2 << endl;
	system("pause");
	return 0;
}
```

### 函数的声明

**作用**：告诉编译器函数的名称及如何调用函数。函数的实际主体可以单独定义



+ 函数的声明可以多次，但定义只能有一次
+ 重定义错误编号compiler error C2084

```c++
#include<iostream>
using namespace std;
//函数的声明
//比较函数，实现两个整型数字的比较，返回较大的值
// 提前告诉编译器函数的存在，可以利用函数的声明
// 函数的声明
//声明可以写多次，但是定义只能有一次
int max(int a, int b);
int max(int a, int b);
int max(int a, int b);
int max(int a, int b);
int max(int a, int b);
int max(int a, int b);
int main()
{
	int a = 10;
	int b = 20;
	cout << max(a, b) << endl;
}
//定义好的函数
int max(int a, int b)
{
	return a > b ? a : b;
}
```

### 函数的分文件编写

**作用**：让代码结构更加清晰

函数分文件编写一般有4个步骤：

1.创建后缀名为.h的头文件

2.创建后缀名为.cpp的源文件

3.在头文件中写函数的声明

4.在源文件中写函数的定义

```c++
//swap.h头文件
void swap(int a, int b);
```

```c++
//swap函数的定义.cpp文件
#include"swap.h"
#include<iostream>
using namespace std;
void swap(int a, int b)
{
	int temp = a;
	a = b;
	b = temp;
	cout << "a=" << a << endl;
	cout << "b=" << b << endl;
}
```

```c++
//主工作区
#include"swap.h"
#include<iostream>
using namespace std;
int main()
{
	swap(1, 2);
}
```

## 指针

[C语言重点——指针篇（一文让你完全搞懂指针）| 从内存理解指针 | 指针完全解析 - 编程指北 - 博客园 (cnblogs.com)](https://www.cnblogs.com/imxiaobei/p/13940005.html)

### 指针的基本概念

**指针的作用**：可以通过指针间接访问内存

+ 内存编号时从0开始记录的，一般用十六进制数字表示

+ 可以利用指针变量保存地址

### 指针变量的定义和使用

指针变量定义语法：` 数据类型*变量名`

```c++
#include<iostream>
using namespace std;
int main()
{
	//1、定义指针
	int a = 10;
	//指针定义的语法：数据类型*指针变量名
	int* p;
	//用p记录指针变量a的地址
	p = &a;
	cout << "a的地址为" << &a << endl;
	cout << "指针p为：" << p<<endl;
	//2、使用指针
	//可以通过解引用的方式来找到指针指向的内存
	//指针前加*代表解引用，找到指针指向的内存中的数据
	*p = 1000;
	cout << "a=" << a << endl;
	cout << "*p=" << *p << endl;
}
```
### 指针所占内存空间

提问：指针也是一种数据类型，那么这种数据类型占多少内存空间呢？

32位操作系统下:4个字节空间大小，不管是什么数据类型

64位：8byte

示例：

```c++
#include<iostream>
using namespace std;
int main()
{
	//指针所占的内存空间大小
	int a = 10;
	//int* p;
	//p = &a;
	int* p = &a;
	cout <<"sizeof int*="<<sizeof(int*) << endl;
	cout << "sizeof p=" << sizeof(p) << endl;
	cout << "sizeof float*=" << sizeof(float*) << endl;
	cout << "sizeof double*=" << sizeof(double*) << endl;
	cout << "sizeof char*=" << sizeof(char*) << endl;
	cout <<"sizeof *p="<< sizeof(*p) << endl;
}
sizeof int *= 8
sizeof p = 8
sizeof float *= 8
sizeof double *= 8
sizeof char *= 8
sizeof * p = 4
```

### 空指针和野指针

**空指针**：指针变量指向内存中编号为0的空间

**用途**：初始化指针变量

**注意**：空指针指向的内存是不可以访问的



**示例1：空指针**

```c++
#include<iostream>
using namespace std;
int main()
{
	//空指针
	//空指针用于给指针变量进行初始化
	int* p=NULL;
	//空指针是不可以进行访问的
	//0~255之间内存编号是系统占用的，因此不可以访问
	*p = 100;
	system("pause");
	return 0;
}

```



**野指针**：指针变量指向非法的内存空间

**示例2**：野指针

```c++
#include<iostream>
using namespace std;
int main()
{
	//野指针
	//在程序中，应该尽量避免野指针
	int* p = (int *)0x1100;
	cout << *p << endl;
	system("pause");
	return 0;
}
```

总结：空指针和野指针都不是我们内存申请的空间，因此不要访问

### const修饰指针

const修饰指针有三种情况：

+ const修饰指针——常量指针

  `const int *p=&a`

  特点：指针的指向可以修改，但指针指向的值不可修改

+ const修饰常量——指针常量

  `int *const p=&a`

  特点：指针的指向不可以改，指针指向的值可以改

+ const既修饰指针，又修饰常量

  `const int *const p=&a`

  特点：指针的指向和指针指向的值都不可以改

```c++
#include<iostream>
using namespace std;
int main()
{
	//const修饰指针常量指针
	int a = 20;
	int b = 10;
	const int* p = &a;
	//指针指向的值不可以改，指向可以改
	p = &b;
	cout << p << endl;
	cout << *p << endl;
	//const修饰常量指针常量
	int*const p2 = &a;
	*p2 = 100;
	//const修饰指针和常量
	const int* const p3 = &a;
	*p3 = 100;//error
	p3 = &b;//error
	system("pause");
	return 0;
}
输出：
000000891578FB64
10
```

### 指针和数组

作用：利用指针访问数组中的元素

示例：

```c++
#include<iostream>
using namespace std;
int main()
{
	//指针和数组
	//利用指针访问数组中的元素
	int arr[10] = { 1,2,3,4,5,6,7,8,9,10 };
	cout << "数组中第一个元素" << arr[0] << endl;
	int* p = arr;//arr就是数组的首地址
	cout << "利用指针访问第一个元素" << *p << endl;
	p++;
	cout << "利用指针访问第二个元素" << *p << endl;
	system("pause");
	return 0;
}
```

### 指针和函数

**作用**：利用指针作函数参数，可以修改形参的值

**示例：**

```c++
#include<iostream>
using namespace std;
//实现两个数字进行互换
void swap01(int a, int b)
{
	int temp = a;
	a = b;
	b = temp;
}
void swap02(int* p1, int* p2)
{
	int temp = *p1;
	*p1 = *p2;
	*p2 = temp;
}
int main()
{
	//指针和函数
	//值传递
	int a = 10;
	int b = 20;
	swap01(a, b);
	cout << "a=" << a << endl;
	cout << "b=" << b << endl;
	//地址传递
	//如果是地址传递，可以修饰实参
	swap02(&a, &b);
	cout << "a=" << a << endl;
	cout << "b=" << b << endl;
	system("pause");
	return 0;
}
```

根据需求选择传递方法

### 指针、数组、函数

案例描述：封装一个函数，利用冒泡排序，实现对整型数组的升序排序

例如数组：int arr[10]={4,3,6,9,1,2,10,8,7,5}

```c++
//冒泡排序
//1.先创建数组
//创建函数，实现冒泡排序
//打印排序好的数组
#include<iostream>
using namespace std;
//参数1;数组首地址，参数2：数组长度
void bubblesort(int* arr, int len)//int *arr可以写成int arr[]
{
	for (int i = 0; i < len - 1; i++)
	{
		for (int j = 0; j < len - i - 1; j++)
		{
			if (arr[j] > arr[j + 1])
			{
				int temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	}

}
//打印数组
void printArray(int* arr, int len)
{
	for (int i = 0; i < len; i++)
	{
		//利用[]索引
		cout << arr[i] << endl;
	}
}
int main()
{
	int arr[10] = { 4,3,6,9,1,2,10,8,7,5 };
	//数组长度
	int len = sizeof(arr) / sizeof(arr[0]);
	bubblesort(arr, len);
	printArray(arr, len);
}
```

### 指针和数组的关系

[(33条消息) 数组名是不是指针？_LudyYuen的博客-CSDN博客_数组名是指针吗](https://blog.csdn.net/ycc541/article/details/44964723)

(1)数组名的内涵在于其指代实体是一种数据结构，这种数据结构就是数组；

(2)数组名的外延在于其可以转换为指向其指代实体的指针，而且是一个指针常量；

(3)指向数组的指针则是另外一种变量类型（在WIN32平台下，长度为4），仅仅意味着数组的存放地址！

```c++
 #include <iostream.h>
 void arrayTest(char str[])
 {
 　cout << sizeof(str) << endl;
 }
 int main(int argc, char* argv[])
 {
 　char str1[10] = "I Love U";
 　arrayTest(str1); 
　 return 0;
 }
```

程序的输出结果为4。不可能吧？

一个可怕的数字，前面已经提到其为指针的长度!

结论1指出，数据名内涵为数组这种数据结构，在arrayTest函数体内，str是数组名，那为什么sizeof的结果却是指针的长度？这是因为：

　　(1)数组名作为函数形参时，在函数体内，其失去了本身的内涵，仅仅只是一个指针；

　　(2)很遗憾，在失去其内涵的同时，它还失去了其常量特性，可以作自增、自减等操作，可以被修改。

　　所以，数据名作为函数形参时，其全面沦落为一个普通指针！它的贵族身份被剥夺，成了一个地地道道的只拥有4个字节的平民。

　　以上就是结论4

## 结构体

### 结构体的基本概念

结构体属于用户==自定义的数据类型==，允许用户存储不同的数据类型

结构体的内存：[(33条消息) C语言结构体占用内存总结_Y-peak的博客-CSDN博客_c语言结构体所占空间](https://blog.csdn.net/Y_peak/article/details/110469575)

### 结构体定义和使用

**语法**：`struct 结构体名{结构体成员列表}；`

**通过结构体创建变量有三种方式**:

+ struct 结构体名 变量名
+ struct 结构体名 = {成员1值、成员2值}

+ 定义结构体时顺便创建变量

```c++
#include<iostream>
using namespace std;
//创建学生数据类型：学生包括（姓名，年龄，分数）
//自定义数据类型：一些类型集合组成的一个类型
//语法 struct 类型名称{成员列表}
struct Student
{
	//成员列表

	//姓名
	string name;
	//年龄
	int age;
	//分数
	int score;
}s3;//3.在定义结构体时顺便创建结构体变量
//通过学生类型创建具体学生
int main()
{
	//1.struct Student s1
	//struct在创建结构体时不可以省略，但创建变量时可以省略
	struct Student s1;
	//给属性赋值，通过.访问结构体变量中的属性
	s1.age = 18;
	s1.name = "张三";
	s1.score = 100;
	cout << s1.age<<s1.name<<s1.score << endl;
	//2.struct Student s2={...}
	struct Student s2 = { "李四",19,80 };
	cout << s2.age << s2.name << s2.score << endl;
	//3.在定义结构体时顺便创建结构体变量
	s3.age = 20;
	s3.name = "王五";
	s3.score = 100;
}
```

+ 定义结构体时的关键字为struct，不可省略
+ 创建结构体变量时，struct可以省略
+ 结构体变量利用操作符"."访问成员

### 结构体数组

**作用**：将自定义的结构体放到数组中，方便维护

**语法**：`struct 结构体名 数组名[元素个数]={{},{},{},{} ~~~ }`

```c++
#include<iostream>
using namespace std;
//结构体数组
//1.定义结构体
struct Student
{
	string name;
	int age;
	int score;
};
int main()
{
//2.创建结构体的数组
	Student stuArray[3]
	{
		{"张三", 18,100},
		{"李四",19,80},
		{"王五",19,80}
	};
//3.给结构体数组中的元素赋值
	stuArray[0].age = 90;
	stuArray[0].name = "赵柳";
	stuArray[0].score = 100;
//4.遍历结构体数组
	for (int i = 0; i < 3; i++)
	{
		cout << stuArray[i].age << stuArray[i].name << stuArray[i].score << endl;
	}
}
```

### 结构体指针

**作用**：通过指针访问结构体中的成员

+ 利用操作符`->`可以通过结构体指针访问结构体属性

示例：

```c++
#include<iostream>
using namespace std;
//结构体指针
//1.定义结构体
struct Student
{
	string name;
	int age;
	int score;
};
int main()
{
	//创建学生的结构体变量
	struct Student s = { "张三",20,100 };

	//通过指针指向结构体变量
	
	struct Student* p = &s;
	//通过指针访问结构体变量中的数据
	//通过结构体指针访问结构体中的属性，可以利用'->'符号
	cout << p->age << p->name << p->score << endl;
```

### 结构体嵌套结构体

**作用**：结构体中的成员可以是另一个结构体

**例如**：每个老师辅导一个学员，一个老师的结构体中，记录一个学生的结构体

```c++
#include<iostream>
using namespace std;
struct student
{
	int age;
	string name;
	int score;
};
struct teacher
{
	int id;//教师编号
	string name;
	int age;
	struct student s1;//学生需要定义在老师的前面
};

int main()
{
	//结构体嵌套结构体
	//创建老师
	teacher t1;
	t1.s1.age = 18;
	cout << t1.s1.age << endl;
	student s1;
	s1.age = 19;//两个s1并不相同
	cout << s1.age << endl;
	cout << t1.s1.age << endl;
	system("pause");
	return 0;
}
18
19
18
```

### 结构体做函数参数

**作用**：将结构体作为参数向函数中传递

传递方式有两种：

+ 值传递
+ 地址传递

示例：

```c++
#include<iostream>
using namespace std;
struct student
{
	int age;
	string name;
	int score;
};
//打印学生信息函数
//值传递
void PrintStudent1(struct student a)
{
	cout << a.age << a.name << a.score << endl;
}
//地址传递
void PrintStudent2(struct student* a)
{
	cout << a->age << a->name << a->score;
}
int main()
{
	//结构体作为函数参数
	//将学生传入到一个参数中，打印学生身上的所有信息
	//创建结构体变量
	student s1 = { 18,"张三",100 };
	PrintStudent1(s1);
	PrintStudent2(&s1);
	system("pause");
	return 0;
}
```

### 结构体中const使用场景

**作用**：用const来防止误操作

示例：

```c++
#include<iostream>
using namespace std;
//const 的使用场景

struct student
{
	int age;
	string name;
	int score;
};
//将形参改为指针可以减少内存空间，而且不会复制一个新的地址出来
void PrintStudent(const student *s1)
{
	s1->age = 100;//报错：加入const之后，不可修改
	cout << s1->age << s1->name << s1->score << endl;
}
int main()
{
	//创建结构体变量
	student s1 = { 18,"张三",100 };
	//通过函数打印结构体变量信息
	//函数体中不小心有写的误操作，会改变实参的值
	system("pause");
	return 0;
}

```

### 结构体案例

#### 案例一

**案例描述**：

学校正在做毕设项目，每名老师带五名学生，总共有三名老师，需求如下：

设计老师和学生的结构体，其中在老师的结构体，有老师的姓名和一个存放5名学生的数组作为成员

学生的成员有姓名、考试分数，创建数组存放3名老师，通过函数给每个老师及所带的学生赋值

最终打印出老师数据以及老师所带的学生数据

```c++
#include<iostream>
#include<ctime>
using namespace std;
//学生结构体
struct Student
{
	string name;
	int score;
};
//老师的结构体定义
struct Teacher
{
	string name;
	struct Student all[5];
};
//给老师和学生赋值的函数
void allocateSpace(struct Teacher tArray[],int len)
{
	//给老师赋值
	string nameseed = "ABCDE";
	for(int i=0;i<len;i++)
	{
		tArray[i].name = "Teacher_";
		tArray[i].name += nameseed[i];
		//通过循环给每名老师所带的学生赋值
		for (int j = 0; j < 5; j++)
		{
			tArray[i].all[j].name = "Student_";
			tArray[i].all[j].name += nameseed[j];
			int random = rand() % 61 + 40;//40~99
			tArray[i].all[j].score = random;
		}
	}
}
//打印所有信息
void printInfo(struct Teacher tArray[],int len)
{
	for (int i = 0; i < len; i++)
	{
		cout << "老师姓名：" << tArray[i].name << endl;
		for (int j = 0; j < 5; j++)
		{
			cout << "\t学生姓名：" << tArray[i].all[j].name <<
				"考试分数：" << tArray[i].all[j].score << endl;
		}
	}
}
int main()
{
	//随机数种子
	srand((unsigned int)time(NULL));
	//创建三名老师的数组
	struct Teacher all[3];
	//通过函数给三名老师赋值，并给老师带的学生信息赋值
	int len = sizeof(all) / sizeof(all[0]);
	allocateSpace(all, len);
	//打印所有老师及所带学生的信息
	printInfo(all,len);
	system("pause");
	return 0;
}
```

#### 案列二

**案例描述**：

设计一个英雄的结构体，包括成员姓名，年龄，性别；创建结构体数组，数组中存放五名英雄

通过冒泡排序的算法，将数组中的英雄按照年龄进行升序排序，最终打印排序后的结果

五名英雄的信息如下：

```c++
{"刘备",23,"男"}
{"关羽",22,"男"}
{"张飞",20,"男"}
{"赵云",21,"男"}
{"貂蝉",19,"女"}
```

示例：

```c++
//主程序
#include<iostream>
#include"BobbleSort.h"
using namespace std;
struct King
{
	string name;
	int age;
	string gender;
};
int main()
{
	struct King boy5[5]
	{
		{"刘备",23,"男"},
		{"关羽",22,"男"},
		{"张飞",20,"男"},
		{"赵云",21,"男"},
		{"貂蝉",19,"女"}
	};
	//升序排序
	int len = sizeof(boy5) / sizeof(boy5[0]);
	BobbleSort(boy5,len);
	print(boy5, len);
}
//头文件
void BobbleSort(struct King array[], int len);
void print(struct King* array, int len);
//冒泡排序函数
#include"BobbleSort.h"
#include<iostream>
using namespace std;
struct King
{
	string name;
	int age;
	string gender;
};
void BobbleSort(struct King array[], int len)
{
	for (int i = 0; i < len - 1; i++)
	{
		for (int j = 0; j < len - i - 1; j++)
		{
			if (array[j].age>array[j+1].age)
			{
				struct King temp = array[j];
				array[j ] = array[j+1];
				array[j+1] = temp;
			}
		}
	}
}
//print结构体函数
#include"BobbleSort.h"
#include<iostream>
using namespace std;
struct King
{
	string name;
	int age;
	string gender;
};
void print(struct King* array, int len)
{
	for (int i = 0; i < len; i++)
	{
		cout << array[i].name << array[i].age << array[i].gender << endl;
	}
}
```

```c++
输出
貂蝉19女
张飞20男
赵云21男
关羽22男
刘备23男
```

## 头文件

[理解 C++ 中的头文件和源文件的作用 | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/cpp-header.html)

[Visual Studio中头文件stdafx.h的作用 - yhjoker - 博客园 (cnblogs.com)](https://www.cnblogs.com/yhjoker/p/8110684.html#:~:text=stdafx.h并不是标准C%2B%2B头文件，也就是说，该文件本质上相当于自定义的一个头文件 ( 这里是VS默认自定义的文件)，与项目的源代码文件存放在同一个文件文件夹下，通过%23include"stdafx.h"引用； 从内容上来说，头文件stdafx.h中可以包含 2.经常使用的但不常更改的特定于项目的包含文件,标准系统包含文件 %3A 即常用的与C标准库对应的头文件，如标准输入头文件stdio.h、字符串头文件string.h等文件。 自定义的包含文件 %3A 即用户根据项目需要自定义的头文件。)

==头文件标准格式==:

```c++
记头文件名字为mine.h，则可以写为：
#ifndef MINE_H
#define MINE_H
#endif
```









### c++编译模式
​        通常，在一个 C++ 程序中，只包含两类文件—— .cpp 文件和 .h 文件。其中，.cpp 文件被称作 C++ 源文件，里面放的都是 C++ 的源代码；而 .h 文件则被称作 C++ 头文件，里面放的也是 C++ 的源代码。
  C++ 语言支持"分别编译"（separatecompilation）。也就是说，一个程序所有的内容，可以分成不同的部分分别放在不同的 .cpp 文件里。.cpp 文件里的东西都是相对独立的，在编译**（compile）**时不需要与其他文件互通，只需要在编译成目标文件后再与其他的目标文件做一次链接（link）就行了。比如，在文件 a.cpp 中定义了一个全局函数 "void a(){}"，而在文件 b.cpp 中需要调用这个函数。即使这样，文件 a.cpp 和文件 b.cpp 并不需要相互知道对方的存在，而是可以分别地对它们进行编译，编译成目标文件之后再链接，整个程序就可以运行了。
​        这是怎么实现的呢？从写程序的角度来讲，很简单。在文件 b.cpp 中，在调用 "void a()" 函数之前，先声明一下这个函数 "void a();"，就可以了。这是因为编译器在编译 b.cpp 的时候会生成一个符号表（symbol table），像 "void a()" 这样的看不到定义的符号，就会被存放在这个表中。再进行链接的时候，编译器就会在别的目标文件中去寻找这个符号的定义。一旦找到了，程序也就可以顺利地生成了。
​        注意这里提到了两个概念，**一个是"定义"，一个是"声明"**。简单地说，"定义"就是把一个符号完完整整地描述出来：它是变量还是函数，返回什么类型，需要什么参数等等。而"声明"则只是声明这个符号的存在，即告诉编译器，这个符号是在其他文件中定义的，我这里先用着，你链接的时候再到别的地方去找找看它到底是什么吧。定义的时候要按 C++ 语法完整地定义一个符号（变量或者函数），而声明的时候就只需要写出这个符号的原型了。需要注意的是，一个符号，在整个程序中可以被声明多次，但却要且仅要被定义一次。试想，如果一个符号出现了两种不同的定义，编译器该听谁的？(重定义)
​        这种机制给 C++ 程序员们带来了很多好处，同时也引出了一种编写程序的方法。考虑一下，如果有一个很常用的函数 "void f() {}"，在整个程序中的许多 .cpp 文件中都会被调用，那么，我们就只需要在一个文件中定义这个函数，而在其他的文件中声明这个函数就可以了。一个函数还好对付，声明起来也就一句话。但是，如果函数多了，比如是一大堆的数学函数，有好几百个，那怎么办？能保证每个程序员都可以完完全全地把所有函数的形式都准确地记下来并写出来吗？

### 什么是头文件

​        很显然，答案是不可能。但是有一个很简单地办法，可以帮助程序员们省去记住那么多函数原型的麻烦：我们可以把那几百个函数的声明语句全都先写好，放在一个文件里，等到程序员需要它们的时候，就把这些东西全部 copy 进他的源代码中。

​        这个方法固然可行，但还是太麻烦，而且还显得很笨拙。于是，头文件便可以发挥它的作用了。所谓的头文件，其实它的内容跟 .cpp 文件中的内容是一样的，都是 C++ 的源代码。但头文件不用被编译。我们把所有的函数声明全部放进一个头文件中，当某一个 .cpp 源文件需要它们时，它们就可以通过一个宏命令 "#include" 包含进这个 .cpp 文件中，从而把它们的内容合并到 .cpp 文件中去。当 .cpp 文件被编译时，这些被包含进去的 .h 文件的作用便发挥了。

举一个例子吧，假设所有的数学函数只有两个：f1 和 f2，那么我们**把它们的定义放在 math.cpp** 里：

```c++
/* math.cpp */
double f1()
{
    //do something here....
    return;
}
double f2(double a)
{
    //do something here...
    return a * a;
}
/* end of math.cpp */
```

并**把"这些"函数的声明放在一个头文件 math.h** 中： 

```c++
/* math.h */
double f1();
double f2(double);
/* end of math.h */
```

在另一个文件main.cpp中，我要调用这两个函数，那么就只需要把头文件包含进来：

```c++
/* main.cpp */
#include "math.h"
main()
{
    int number1 = f1();
    int number2 = f2(number1);
}
/* end of main.cpp */
```

这样，便是一个完整的程序了。需要注意的是，.h 文件不用写在编译器的命令之后，但它必须要在编译器找得到的地方（比如跟 main.cpp 在一个目录下）main.cpp 和 math.cpp 都可以分别通过编译，生成 main.o 和 math.o，然后再把这两个目标文件进行链接，程序就可以运行了。

### include
​     #include 是一个来自 C 语言的宏命令，它在编译器进行编译之前，即在预编译的时候就会起作用。#include 的作用是把它后面所写的那个文件的内容，完完整整地、一字不改地包含到当前的文件中来。值得一提的是，它本身是没有其它任何作用与副功能的，它的作用就是把每一个它出现的地方，替换成它后面所写的那个文件的内容。简单的文本替换，别无其他。因此，main.cpp 文件中的第一句（#include"math.h"），在编译之前就会被替换成 math.h 文件的内容。即在编译过程将要开始的时候，main.cpp 的内容已经发生了改变：

```c++
/* ~main.cpp */
double f1();
double f2(double);
main()
{
    int number1 = f1();
    int number2 = f2(number1);
}
/* end of ~main.cpp */
```

不多不少，刚刚好。同理可知，如果我们除了 main.cpp 以外，还有其他的很多 .cpp 文件也用到了 f1 和 f2 函数的话，那么它们也通通只需要在使用这两个函数前写上一句 #include "math.h" 就行了。


### 头文件应该写什么
​        通过上面的讨论，我们可以了解到，头文件的作用就是被其他的 .cpp 包含进去的。它们本身并不参与编译，但实际上，它们的内容却在多个 .cpp 文件中得到了编译。通过"定义只能有一次"的规则，我们很容易可以得出，**头文件中应该只放变量和函数的声明，而不能放它们的定义**。因为一个头文件的内容实际上是会被引入到多个不同的 .cpp 文件中的，并且它们都会被编译。放声明当然没事，如果放了定义，那么也就相当于在多个文件中出现了对于一个符号（变量或函数）的定义，纵然这些定义都是相同的，但对于编译器来说，这样做不合法。

所以，应该记住的一点就是，**.h头文件中，只能存在变量或者函数的声明，而不要放定义**。即，只能在头文件中写形如：extern int a; 和 void f(); 的句子。这些才是声明。如果写上 int a;或者 void f() {} 这样的句子，那么一旦这个头文件被两个或两个以上的 .cpp 文件包含的话，编译器会立马报错。（关于 extern，前面有讨论过，这里不再讨论定义跟声明的区别了。）

但是，这个规则是有三个例外的: 

+ 头文件中可以写 const 对象的定义。因为全局的 const 对象默认是没有 extern 的声明的，所以它只在当前文件中有效。把这样的对象写进头文件中，即使它被包含到其他多个 .cpp 文件中，这个对象也都只在包含它的那个文件中有效，对其他文件来说是不可见的，所以便不会导致多重定义。同时，因为这些 .cpp 文件中的该对象都是从一个头文件中包含进去的，这样也就保证了这些 .cpp 文件中的这个 const 对象的值是相同的，可谓一举两得。同理，static 对象的定义也可以放进头文件。
+ 头文件中可以写内联函数（inline）的定义。因为inline函数是需要编译器在遇到它的地方根据它的定义把它内联展开的，而并非是普通函数那样可以先声明再链接的（内联函数不会链接），所以编译器就需要在编译时看到内联函数的完整定义才行。如果内联函数像普通函数一样只能定义一次的话，这事儿就难办了。因为在一个文件中还好，我可以把内联函数的定义写在最开始，这样可以保证后面使用的时候都可以见到定义；但是，如果我在其他的文件中还使用到了这个函数那怎么办呢？这几乎没什么太好的解决办法，因此 C++ 规定，内联函数可以在程序中定义多次，只要内联函数在一个 .cpp 文件中只出现一次，并且在所有的 .cpp 文件中，这个内联函数的定义是一样的，就能通过编译。那么显然，把内联函数的定义放进一个头文件中是非常明智的做法。
+ 头文件中可以写类（class）的定义。因为在程序中创建一个类的对象时，编译器只有在这个类的定义完全可见的情况下，才能知道这个类的对象应该如何布局，所以，关于类的定义的要求，跟内联函数是基本一样的。所以把类的定义放进头文件，在使用到这个类的 .cpp 文件中去包含这个头文件，是一个很好的做法。在这里，值得一提的是，类的定义中包含着数据成员和函数成员。数据成员是要等到具体的对象被创建时才会被定义（分配空间），但函数成员却是需要在一开始就被定义的，这也就是我们通常所说的类的实现。一般，我们的做法是，把类的定义放在头文件中，而把函数成员的实现代码放在一个 .cpp 文件中。这是可以的，也是很好的办法。不过，还有另一种办法。那就是直接把函数成员的实现代码也写进类定义里面。在 C++ 的类中，如果函数成员在类的定义体中被定义，那么编译器会视这个函数为内联的。因此，把函数成员的定义写进类定义体，一起放进头文件中，是合法的。注意一下，如果把函数成员的定义写在类定义的头文件中，而没有写进类定义中，这是不合法的，因为这个函数成员此时就不是内联的了。一旦头文件被两个或两个以上的 .cpp 文件包含，这个函数成员就被重定义了。
### 头文件中保护措施
考虑一下，如果头文件中只包含声明语句的话，它被同一个 .cpp 文件包含再多次都没问题——因为声明语句的出现是不受限制的。然而，上面讨论到的头文件中的三个例外也是头文件很常用的一个用处。那么，一旦一个头文件中出现了上面三个例外中的任何一个，它再被一个 .cpp 包含多次的话，问题就大了。因为这三个例外中的语法元素虽然"可以定义在多个源文件中"，但是"在一个源文件中只能出现一次"。设想一下，如果 a.h 中含有类 A 的定义，b.h 中含有类 B 的定义，由于类B的定义依赖了类 A，所以 b.h 中也 #include了a.h。现在有一个源文件，它同时用到了类A和类B，于是程序员在这个源文件中既把 a.h 包含进来了，也把 b.h 包含进来了。这时，问题就来了：类A的定义在这个源文件中出现了两次！于是整个程序就不能通过编译了。你也许会认为这是程序员的失误——他应该知道 b.h 包含了 a.h ——但事实上他不应该知道。

##### 头文件标准写法

**使用 "#define" 配合条件编译可以很好地解决这个问题。在一个头文件中，通过 #define 定义一个名字，并且通过条件编译 #ifndef...#endif 使得编译器可以根据这个名字是否被定义，再决定要不要继续编译该头文中后续的内容。这个方法虽然简单，但是写头文件时一定记得写进去**。

### 头文件和源文件的区别
#### 源文件如何根据 #include 来关联头文件
+ 系统自带的头文件用**尖括号**括起来，这样编译器会在系统文件目录下查找。
+ 用户自定义的文件用**双引号**括起来，编译器首先会在用户目录下查找，然后在到 C++ 安装目录（比如 VC 中可以指定和修改库文件查找路径，Unix 和 Linux 中可以通过环境变量来设定）中查找，最后在系统文件中查找。
#include "xxx.h"（我一直以为 "" 和 <> 没什么区别，但是 tinyxml.h 是非系统下的都文件，所以要用 ""）

#### 头文件如何来关联源文件
这个问题实际上是说，已知头文件 "a.h" 声明了一系列函数，"b.cpp" 中实现了这些函数，那么如果我想在 "c.cpp" 中使用 "a.h" 中声明的这些在 "b.cpp"中实现的函数，通常都是在 "c.cpp" 中使用 #include "a.h"，那么 c.cpp 是怎样找到 b.cpp 中的实现呢？

其实 .cpp 和 .h 文件名称没有任何直接关系，很多编译器都可以接受其他扩展名。比如偶现在看到偶们公司的源代码，.cpp 文件由 .cc 文件替代了。

在 Turbo C 中，采用命令行方式进行编译，命令行参数为文件的名称，默认的是 .cpp 和 .h，但是也可以自定义为 .xxx 等等。

谭浩强老师的《C 程序设计》一书中提到，编译器预处理时，要对 #include 命令进行"文件包含处理"：将 file2.c 的全部内容复制到 #include "file2.c" 处。这也正说明了，为什么很多编译器并不 care 到底这个文件的后缀名是什么----因为 #include 预处理就是完成了一个"复制并插入代码"的工作。

编译的时候，并不会去找 b.cpp 文件中的函数实现，只有在 link 的时候才进行这个工作。我们在 b.cpp 或 c.cpp 中用 #include "a.h" 实际上是引入相关声明，使得编译可以通过，程序并不关心实现是在哪里，是怎么实现的。源文件编译后成生了目标文件（.o 或 .obj 文件），目标文件中，这些函数和变量就视作一个个符号。在 link 的时候，需要在 makefile 里面说明需要连接哪个 .o 或 .obj 文件（在这里是 b.cpp 生成的 .o 或 .obj 文件），此时，连接器会去这个 .o 或 .obj 文件中找在 b.cpp 中实现的函数，再把他们 build 到 makefile 中指定的那个可以执行文件中。

在 Unix下，甚至可以不在源文件中包括头文件，只需要在 makefile 中指名即可（不过这样大大降低了程序可读性，是个不好的习惯哦^_^）。在 VC 中，一帮情况下不需要自己写 makefile，只需要将需要的文件都包括在 project中，VC 会自动帮你把 makefile 写好。

通常，C++ 编译器会在每个 .o 或 .obj 文件中都去找一下所需要的符号，而不是只在某个文件中找或者说找到一个就不找了。因此，如果在几个不同文件中实现了同一个函数，或者定义了同一个全局变量，链接的时候就会提示 "redefined"。

**综上所诉**
.h文件中能包含：
+ 类成员数据的声明，但不能赋值

+ 类静态数据成员的定义和赋值，但不建议，只是个声明就好。

+ 类的成员函数的声明

+ 非类成员函数的声明

+ 常数的定义：如：constint a=5;

+ 静态函数的定义

+ 类的内联函数的定义
  不能包含：

+ 所有非静态变量（不是类的数据成员）的声明

+ 默认命名空间声明不要放在头文件，using namespace std;等应放在.cpp中，在 .h 文件中使用 std::string

  ==有一处小的错误需要指出来==

  **.h** 文件中能包含： **static** 普通变量和普通函数的定义，但是不能包含，**static** 成员函数和成员变量的定义。

  原因在于 **static** 这个关键词其实有两个不同的含义：

  -  **static** 修饰普通的变量和函数时。
  -  **static** 关键字是为了限制可见性。

  举例：

  **void funcA(){ int a =0; a++; printf(a) }**，如果要连续记录调用了多少次，就得使用全局变量，但是全局变量暴露的太多了，其他文件中也能可见，所以，static a 用于仅本文件可见。

  而 static 修饰类的成员变量时，该成员是属于类本身，所有类的实例对象共享。

  ```c++
  class A{
      public:
          static int a;
  }
  ```

  其他文件 include 类定义的头文件 classA.h，本质上相当于复制。假设我们现在不 **#include "classA.h"** 而是直接写。

  例如 a.cpp 写上上述头文件，然后再加上 **int A::a = 3;**, 在 b.cpp 中写上上述头文件，然后再加上 **int A::a = 3;**, 等于是定义了两次，此时发生重定义问题（根源在于 static 成员变量并不限制仅本文件可见），所以头文件中不能包含，static 成员函数和成员变量的定义，只能声明。
  
  
