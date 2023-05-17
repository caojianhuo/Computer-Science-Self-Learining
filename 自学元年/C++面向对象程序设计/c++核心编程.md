# C++核心编程

本阶段主要针对c++面向对象编程技术做详细讲解，探讨c+中的核心和精髓

## 内存分配模型

c++程序在执行时，将内存大方向划分为**4个区域**

+ 代码区：存放函数体的二进制代码，由操作系统进行管理的
+ 全局区：存放全局变量和静态变量以及常量
+ 栈区：由编译器自动分配释放，存放函数的参数值，局部变量
+ 堆区：由程序员分配和释放，若程序员不释放，程序结束时由操作系统回收

**内存四区意义**:
不同区域存放的数据，赋予不同的生命周期，给我们更大的灵活编程

### 程序运行前

在程序**编译**后，生成exe可执行程序，**未执行该程序前**分为两个区域

==代码区==：

存放CPU执行的机器指令(01010010)

代码区是共享的，共享的目的是对于频繁被执行的程序，只需要内存中有一份代码即可(老想双击执行，不必要再复制粘贴)

代码区是只读的，使其只读的原因是防止程序意外地修改了它的指令

==全局区==：
全局变量和静态变量存放在此

全局区还包含了常量区，字符串常量和其它常量（const修饰的全局变量）存放在此

==该区域的数据在程序结束后由操作系统释放==

|           全局区中           |           不在全局区中            |
| :--------------------------: | :-------------------------------: |
|           全局变量           |             局部变量              |
|  静态变量`static 数据类型`   | `const`修饰的局部变量（局部常量） |
| `const 全局变量`（全局常量） |                                   |
|          字符串常量          |                                   |

```c++
#include<iostream>
using namespace std;	
//全局变量
int g_a = 10;
int g_b = 10;
//const修饰的全局变量,全局常量
const int c_g_a = 10;
const int c_g_b = 10;
int main()
{
	//全局区
	//全局变量、静态变量、常量
	//创建普通局部变量（只要是写在函数体中的都是局部变量）
	int a = 10;
	int b = 10;
	cout << "局部变量a的地址为" << (int) & a << endl;
	cout << "局部变量b的地址为" << (int) & b << endl;
	cout << "全局变量g_a的地址为" << (int)&g_a << endl;
	cout << "全局变量g_b的地址为" << (int)&g_b << endl;

	//静态变量  在普通变量的前面加static，属于静态变量
	static int s_a = 10;
	static int s_b = 10;
	cout << "静态变量s_a的地址为" << (int)&s_a << endl;
	cout << "静态变量s_b的地址为" << (int)&s_b << endl;

	//常量
	//字符串常量
	cout << "字符串常量的地址为" << (int)&"helloworld" << endl;
	//const修饰的常量
	//const修饰的全局变量
	cout << "全局常量c_g_a的地址为" << (int)&c_g_a << endl;
	cout << "全局常量c_g_b的地址为" << (int)&c_g_b << endl;
	//const修饰的局部变量
	const int c_l_a = 10;
	const int c_l_b = 10;
	cout << "局部常量c_l_a的地址为" << (int)&c_l_a << endl;
	cout << "局部常量c_l_b的地址为" << (int)&c_l_b << endl;
	//c->const,g->global,l->local
	system("pause");
	return 0;
}
```

```c++
//输出结果
局部变量a的地址为-1215302140
局部变量b的地址为-1215302108
全局变量g_a的地址为1001574480
全局变量g_b的地址为1001574484
静态变量s_a的地址为1001574488
静态变量s_b的地址为1001574492
字符串常量的地址为1001565176
全局常量c_g_a的地址为1001565240
全局常量c_g_b的地址为1001565244
局部常量c_l_a的地址为-1215302076
局部常量c_l_b的地址为-1215302044
```

**结论**：

+ c++中在程序运行之前分为全局区和代码区
+ 代码区的特点为只读和共享
+ 全局区中存放全局变量、静态变量和常量
+ 常量区中存放const修饰的全局常量和字符串常量

### 程序运行后

**栈区**：

由编译器自动分配释放，存放函数的参数值、局部变量等

注意事项：**不要返回局部变量的地址，栈区开辟的数据由编译器自动释放**

```c++
#include<iostream>
using namespace std;
//栈区数据注意事项---不要返回局部变量的地址
//栈区数据由编译器管理开辟和释放
int* func(int b)//形参数据也会放在栈区
{
	b = 100;
	cout << &b << endl;
	int a = 10;//局部变量  存放在栈区，栈区的数据在函数执行完后自动释放
	return &a;//返回局部变量的地址
}
int main()
{
	//接受func函数的返回值
	int* p = func(1);
	int* b = func(2);
	cout << *p << endl;//第一次可以打印正确的数据是因为编译器做了保留
	cout << *p << endl;//第二次这个数据就不保留了
}
```

**堆区**：

​		由程序员分配释放，若程序员不释放，程序结束时由操作系统回收       

​		在c++中主要利用new在堆区中开辟内存

```c++
#include<iostream>
using namespace std;
int* func()
{
	//利用new关键字 可以将数据开辟到堆区
	//指针本质也是局部变量，放在栈上，指针保存的数据是放在了堆区
	int*p = new int(10);
	return p;
}
int main()
{
	//在堆区开辟数据
	int* p = func();
	cout << *p << endl;
	system("pause");
}

```

**总结**：

+ 堆区数据由程序员管理和释放
+ 堆区数据利用new关键字进行开辟内存  `new 数据类型（）`->返回一个地址

### new操作符

c++利用==new==操作符在堆区开辟数据

堆区开辟的数据，由程序员手动开辟，手动释放，释放利用操作符==delete==

语法：

`new 数据类型`

利用new函数创建的数据，会返回该数据对应的类型的指针

```c++
#include<iostream>
using namespace std;
//1、new的基本语法
int* func()
{
	//在堆区创建一个整型地数据
	int*p=new int(10);//new返回的是该数据类型的指针
	return p;
}
void text01()
{
	int* p = func();
	cout << *p << endl;
	//堆区的数据，由程序员开辟，程序员管理释放
	//如果想释放堆区的数据，利用关键字delete；
	delete p;
	//cout << *p << endl;//内存已经被释放，再次访问就是非法操作，会报错
}
//2、在堆区中利用new开辟数组
void text02()
{
	//创建10整型数据的数组，在堆区
	int*arr=new int[10];//10代表数组有10个元素
	for (int i = 0; i < 10; i++)
	{
		arr[i] = 100 + i;
	}
	for (int i = 0; i < 10; i++)
	{
		cout << arr[i] << endl; 
	}
	//释放堆区数组
	//释放数组的使用要加[]才可以
	delete[] arr;
}
int main()
{
	text01();
	text02();
	system("pause");	
	return 0;
}

```

## 引用

### 引用的基本使用

**作用**：给变量起别名

**语法**：`数据类型 &别名=原名`

**示例**：

```c++
#include<iostream>
using namespace std;
//引用的基本语法
//数据类型 &别名=原名
int main()
{
	int a = 10;
	//创建引用
	int& b = a;
	cout << "a=" << a << endl;
	cout << "b=" << b << endl;
	cout << "a的地址为" << &a << endl;
	cout << "b的地址为" << &b << endl;
	b = 100;
	cout << "a=" << a << endl;
	cout << "b=" << b << endl;
	cout << "a的地址为" << &a << endl;
	cout << "b的地址为" << &b << endl;
	system("pause");
	return 0;
}

//输出
a=10
b=10
a的地址为000000116A52F914
b的地址为000000116A52F914
a=100
b=100
a的地址为000000116A52F914
b的地址为000000116A52F914
```



### 引用注意事项

+ 引用必须初始化
+ 引用在初始化后，不可以改变

**示例**：

```c++
#include<iostream>
using namespace std;
int main()
{
	int a = 10 ;
	int& b = a;
	//引用必须初始化
	//int& c;//错误代码
	//引用在初始化过后，不可以改变
	int c = 20;
	b = c;//赋值操作而不是更改引用
	cout << "a=" << a << "a的地址为" << &a << endl;
	cout << "b=" << b << "b的地址为" << &b << endl;
	cout << "c=" << c << "c的地址为" << &c << endl;
	int d = 100;
	int& b = d;//C2374:b重定义，多次被初始化
	cout << "b=" << b << "b的地址为" << &b << endl;
	system("pause");
	return 0;
}

```

### 引用做函数参数

**作用**：函数传参时，可以利用引用的技术让形参修饰实参

**优点**：可以简化指针修饰实参

```c++
#include<iostream>
using namespace std;
//交换函数
//值传递
void mySwap01(int a, int b)
{
	int temp = a;
	a = b;
	b = temp;
	cout << "Swap01 a=" << a << endl;
	cout << "Swap01 b=" << b << endl;
}
//地址传递
void mySwap02(int* a, int* b)
{
	int temp = *a;
	*a = *b;
	*b = temp;
}
//引用传递
void mySwap03(int& a, int& b)
{
	int temp = a;
	a = b;
	b = temp;
}
int main()

	int a = 10;
	int b = 20;
	mySwap01(a, b);//值传递，形参不会修饰实参
	cout << "a=" << a << endl;
	cout << "b=" << b << endl;
	mySwap02(&a, &b);//地址传递，形参会修饰实参
	mySwap03(a, b);//引用传递，形参会修饰实参
	cout << "a=" << a << endl;
	cout << "b=" << b << endl;
	system("pause");
	return 0;
}
```

**总结**：通过引用参数产生的效果同按地址传递是一样的，引用的语法更清楚简单

### 引用做函数返回值

**作用**：引用是可以作为函数的返回值存在的

**注意**：不要返回局部变量引用

**用法**：函数调用作为左值

```c++
#include<iostream>
using namespace std;
//引用做函数的返回值
//不要返回局部变量的引用
int& text01()
{
	int a = 10;//局部变量存放在四区中的栈区
	return a;
}
//函数的调用可以作为左值
int& text02()
{
	static int a = 10;//静态变量，存放在全局区，全局区上的数据在程序结束后系统释放
	return a;
}
int main()
{
	int& ref = text01();
	cout << "ref=" << ref << endl;//第一次正确，因为编译器做了保留
	cout << "ref=" << ref << endl;//第二次结果错误，因为a的内存已经释放
	int& ref2 = text02();
	cout << "ref2=" << ref2 << endl;
	//如果函数的返回值是引用，可以做左值
	text02() = 1000;//->操作a=1000
	cout << "ref2=" << ref2 << endl;
	system("pause");
	return 0;
}
//输出
ref=-858993460
ref=-858993460
ref2=10
ref2=1000
```



### 引用的本质

**本质**：引用的本质在c++内部实现的是一个指针常量

```c++
//发现是引用，转换为int* const ref=&a
void func(int& ref)
{
    ref=100;//ref是引用，转换为*ref=100
}
int main()
{
    int a=10;
    //自动转换为int* const ref=&a;指针常量是指针指向不可改，也说明为什么引用不可更改
    int&ref=a;
    ref=20;//内部发现ref是引用，自动帮我们转为：*ref=20；
    func(a);
    return 0;
}
```



### 常量引用

**作用**:常量引用主要用来修饰形参，防止误操作

在函数形参列表中，可以加==const修饰形参==，防止形参改变实参

```c++
#include<iostream>
using namespace std;
//打印数据的函数
void showValue(const int& val)
{
	//val = 1000;只读，防止误操作
	cout <<"val="<< val << endl;
}
int main()
{
	//常量引用
	//使用场景：用来修饰形参，防止误操作
	//int a = 10;
	//加上const之后，编译器将代码更改为 int temp=10 ，const int&ref=temp
	//const int& ref = 10;//
	//ref = 20;//加入const之后变为只读，不可修改
	int a = 100;
	showValue(a);
	cout << "a=" << a << endl;
	system("pause");
	return 0;
}
```



## 函数提高

### 函数默认参数

在c++中，函数中形参列表中的形参是可以有默认值的。

语法：`返回值类型 函数名(参数=默认值){}`

示例：

```c++
#include<iostream>
using namespace std;
//函数的默认参数
//如果我们自己传入数据，就用自己的数据，如果没有，就用默认值
//语法：返回值类型 函数名(形参=默认值){函数体}
int func(int a, int b = 20 , int c = 30)
{
	return a + b + c;
}
//注意事项
//如果某个位置已经有了默认参数，那么从这个位置往后，从左到右都必须有默认值
/*int func(int a=10, int b , int c = 30)
{
	return a + b + c;
}*/
//如果函数的声明有默认参数，函数的实现就不能有默认参数了->重定义默认参数
//声明和实现只能有一个有默认参数
int func2(int a = 10, int b = 10);
int func2(int a = 10, int b = 10)
{
	return a + b;
}
int main()
{
	cout << func(10) << endl;
	cout << func2(10, 10) << endl;
}
```

### 函数占位参数

C++中函数的形参列表中可以有占位参数，用来占位，调用函数时必须填补该位置

**语法**：`返回值类型 函数名（数据类型）{}`

示例：

```c++
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
```

### 函数重载

#### 函数重载概述

**作用**：函数名可以相同，提高复用性

**函数重载满足条件**：

+ 同一个作用域下(比如全局作用下)
+ 函数名称相同
+ 函数参数类型不同或者个数不同或者顺序不同

**注意**：函数的返回值不可以作为函数重载的条件

```c++
#include<iostream>
using namespace std;
//函数重载
//可以让函数名相同，提高复用性
//函数重载的满足条件：
//1、同一个作用域（全局作用域，不在main函数里
//2、函数名称相同
//3、函数参数类型不同，或者个数不同，或者顺序不同
void func()
{
	cout << "func的调用" << endl;
}
void func(int a)
{
	cout << "func(int a)的调用" << endl;
}
void func(double a)
{
	cout << "func(int a)的调用" << endl;
}
void func(int a,double b)
{
	cout << "func(int a)的调用" << endl;
}
void func(double a, int b)
{
	cout << "func(int a)的调用" << endl;
}
int main()
{
	func();
	func(3.14);
 }
//注意事项：函数的返回值不可以当做函数重载的条件
int func(double a, int b)
{
	cout << "func(int a)的调用" << endl;
}//错误
```

#### 函数重载注意事项

+ 引用作为重载条件
+ 函数重载碰到函数默认参数

```c++
#include<iostream>
using namespace std;
//函数重载的注意事项
//引用作为重载的条件
void fun(int& a)//int &a=10;false
{
	cout << "func(int& a)的调用" << endl;
}
void fun(const int& a)
{
	cout << "func(const int& a)的调用" << endl;
}
//函数重载碰到默认参数
void func2(int a)
{
	cout << "func(int a)的调用" << endl;
}
void func2(int a,int b=10)
{
	cout << "func(int a)的调用" << endl;
}
int main()
{
	//int a = 10;
	//fun(a);
	fun(10);//func(const int& a)的调用
	func2(10);//当函数重载碰到默认参数，出现二意性->为了避免，重载不要默认参数
}
```

## 类和对象

c++面向对象有三大特性==封装、继承、多态==

c++认为==万事万物皆为对象==，对象上有其属性和行为

**例如**：

人可以作为对象，属性有姓名、年龄、身高、体重...,行为有走、跑、跳

车也可以作为对象、属性有轮胎、方向盘、车灯...,行为有载人、放音乐、开空调...

具有相同性质的==对象==，我们可以抽象成为==类==，人属于人类，车属于车类

### 封装

#### 封装的意义

封装是C++面向对象三大类型之一

封装的的意义：

+ 将属性和行为作为一个整体，表现生活中的事物
+ 将属性和行为加以权限控制

**封装意义一：**

在设计类的时候，属性和行为写在一起，表现事物

**语法**：`class 类名{访问权限： 属性/行为}`

**示例1**:设计一个圆类,求圆的周长

```c++
#include<iostream>
using namespace std;
//圆周率
const float PI = 3.14;
//设计一个圆类，求圆的周长
//圆求周长的公式  2*PI*半径
//class 代表设计一个类，类后面紧跟着的就是类的名称
class Circle
{
	//访问权限
	//公共权限
public:
	//属性（用变量就好）
	//半径
	int m_r;
	//行为(通常用函数)
	//获取圆的周长
	double calculateZC()
	{
		return 2 * PI * m_r;
	}
};
int main()
{
	//通过圆类创建具体的圆（对象）
	//实例化（通过一个类 创建一个对象的过程）
	Circle c1;
	//给圆对象的属性进行赋值
	c1.m_r = 10;
	//2*PI*m_r
	cout << "圆的周长为" << c1.calculateZC() << endl;
}
```

**示例2**：设计一个学生类，属性有姓名和学号，可以给姓名和学号赋值，可以显示学生的姓名和学号

```c++
#include<iostream>
using namespace std;
//设计一个学生类，属性有姓名和学号，可以给姓名和学号赋值，可以显示学生的姓名和学号
class Student
{
public://公共权限
	//类中的属性和行为  我们统称为成员
	// 属性  成员属性  成员变量
	// 行为  成员函数  成员方法
	//属性
	string name;//姓名
	int ID;//学号
	//行为
	void showName()
	{
		cout << "学生的姓名为" << name << endl;
	}
	void showID()
	{
		cout << "学生的学号为" << ID <<endl;
	}
	//通过行为给姓名赋值
	void setName(string getname)
	{
		name = getname;
	}
	//给学号赋值
	void setId(int Id)
	{
		ID = Id;
	}
};
int main()
{
	//创建一个具体的学生——实例化对象
	Student s1;
	//给s1对象进行属性的赋值
	//s1.name = "张三";
	s1.setName("张三")；
	s1.ID = 1;
	s1.showID();
	Student s2;
	s2.ID = 2;
}
```

**封装意义二**：

类在设计时，可以把属性和行为放在不同权限下，加以控制

访问权限有三种：

+ public  公共权限
+ protected  保护权限
+ private  私有权限

**示例**:

```c++
#include<iostream>
using namespace std;
//访问权限：
//公共权限public  成员  类内可以访问  类外也可以访问
//保护权限protected  成员  类内可以访问  类外不可以访问  子类可以访问父类中的保护内容
//私有权限private  成员  类内可以访问  类外不可以访问  子类不可以访问父类的私有内容
class Person
{
public:
	//公共权限
	string m_Name;
protected:
	//保护权限
	string m_Car;//汽车
private:
	//私有权限
	int m_password;//银行卡密码
public:
	void func()//类内
	{
		m_Name = "张三";
		m_Car = "拖拉机";
		m_password = 123456;
	}

};
int main()
{
	//实例化具体对象
	Person p1;
	p1.m_Name = "李四";
	p1.m_Car = "奔驰";//保护权限内容，类外不可以访问
	p1.m_password = 123;//私有权限内容，类外不可以访问
	system("pause");
	return 0;
}
```



#### struct和class的区别

在c++中struct和class的唯一区别就在于**默认的访问权限不同**

区别：

+ struct默认权限为公有public
+ class默认权限为私有private

```c++
#include<iostream>
using namespace std;
class C1
{
	int m_A;//默认权限是私有
};
struct C2
{
	int  m_A;//默认权限是共有
};
//struct和class区别
//struct默认权限是公共public
//class 默认权限是私有private
int main()
{
	C1 c1;
	//c1.m_A = 100;//默认私有
	C2 c2;
	c2.m_A = 100;//在struct中默认权限是公共
	system("pause");
	return 0;
}
```



#### 成员类型设置为私有

**优点1**：将所有成员属性设置为私有，可以自己控制读写权限

**优点2**：对于写权限，我们可以检测数据的有效性

示例：

```c++
#include<iostream>
using namespace std;
//成员属性设置为私有
//1、可以自己控制读写权限
//2、对于写可以检测数据的有效性
//设计人类
class Person
{
public:
	//设置姓名
	void setName(string name)
	{
		m_Name = name;
	}
	//获取姓名
	string getName()
	{
		return m_Name;
	}
	//获取年龄
	int getAge()
	{
		m_Age = 0;//初始化为0
		return m_Age;
	}
	//获取心理年龄  可读可写  如果想修改（年龄的范围必须是0~150之间）
	int getAgeH()
	{
		m_AgeH = 0;//初始化为0
		return m_AgeH;
	}
	//设置心理年龄
	void setAgeH(int ageH)
	{
		if (ageH < 0 || ageH > 150)
		{
			m_AgeH = 0;
			cout << "你个老妖精" << endl;
			return;
		}
		m_AgeH = ageH;
	}
	//设置情人  只写
	void setLover(string lover)
	{
		m_Lover = lover;
	}
private:
	//姓名  可读可写
	string m_Name;
	//年龄   只读
	int m_Age;
	//心理年龄  可读可写  如果想修改（年龄的范围必须是0~150之间）
	int m_AgeH;
	//情人  只写
	string m_Lover;
};
int main()
{
	Person p;
	p.setName("张三");
	cout << p.getName() << endl;
	cout << p.getAge() << endl;
	//设置情人为仓井女生
	p.setLover("仓井");
	system("pause");
	return 0;
}
```

**练习案例1**:设计立方体类

设计立方体类(Cube)

求出立方体的面积和体积

分别用全局函数和成员函数判断两个立方体是否相等

```C++
#include<iostream>
using namespace std;
//设计立方体类(Cube)
class Cube
{
public:
	float m_L = 0;
	float m_H = 0;
	float m_W = 0;
//求出立方体的面积和体积
float S()
{
	return 2*(m_L * m_H + m_L *  m_W + m_H * m_W);
}
float V()
{
	return m_L * m_W * m_H;
}
//成员函数判断两个立方体是否相等
void m_equal(Cube c1,Cube c2)
{
	if (c1.m_H == c2.m_H && c1.m_L == c2.m_L && c1.m_W == c2.m_W)
	{
		cout << "两立方体相等" << endl;
	}
	else
		cout << "两立方体不相等" << endl;
}
};
//用全局函数判断两个立方体是否相等
void equal(Cube c1, Cube c2)
{
	if (c1.m_H == c2.m_H && c1.m_L == c2.m_L && c1.m_W == c2.m_W)
	{
		cout << "两立方体相等" << endl;
	}
	else
		cout << "两立方体不相等" << endl;
}
int main()
{
	Cube c1;
	Cube c2;
	c1.m_H = 3.3;
	c1.m_L = 2.5;
	c1.m_W = 5.3;
	c2.m_H = 2.4;
	c2.m_L = 4.6;
	c2.m_W = 9.4;
	cout << "c1立方体的面积为" << c1.S() << endl;
	cout << "c1立方体的体积为" << c1.V() << endl;
	cout << "c2立方体的面积为" << c2.S() << endl;
	cout << "c2立方体的体积为" << c2.V() << endl;
	c1.m_equal(c1, c2);
	equal(c1, c2);
}
```

`标准答案`

+ ==成员函数判断的时候传一个参数就行==

```c++
#include<iostream>
using namespace std;
//立方体设计
//创建立方体类
//设计属性
//设计行为、获取立方体的面积和体积
//分别利用全局函数和成员函数  判断两个立方体是否相等
class Cube
{
public:
	//设置长
	void setL(int l)
	{
		m_L = l;
	}
	//获取长
	int getL()
	{
		return m_L;
	}
	//设置宽
	void setW(int w)
	{
		m_W = w;
	}
	//获取宽
	int getW()
	{
		return m_L;
	}
	//设置高
	void setH(int h)
	{
		m_H = h;
	}
	//获取高
	int getH()
	{
		return m_H;
	}
	//获取立方体面积
	int calculateS()
	{
		return 2 * (m_L * m_H + m_L * m_W + m_H * m_W);
	}
	//获取立方体体积
	int calculateV()
	{
		return m_L * m_W * m_H;
	}
	bool isSameByClass(Cube &c)
	{
		if (m_L == c.getL() && m_H == c.getH() && m_W == c.getW())
		{
			return true;
		}
		else
			return false;
	}
private:
	int m_L;//长
	int m_W;//宽
	int m_H;//高
};
//利用全局函数判断 两个立方体是否相等
bool isSame(Cube& c1, Cube& c2)
{
	if (c1.getL() == c2.getL() && c1.getH() == c2.getH() && c1.getW() == c2.getW())
	{
		return true;
	}
	else
		return false;
}
int main() 
{
	//创建立方体对象
	Cube c1;
	c1.setL(10);
	c1.setH(10);
	c1.setW(10);
	cout << "c1的面积为:" << c1.calculateS() << endl;
	cout << "c1的体积为" << c1.calculateV() << endl;
	//创建第二个立方体
	Cube c2;
	c2.setL(11);
	c2.setH(10);
	c2.setW(10);
	//利用全局函数判断
	bool ret = isSame(c1, c2);
	if (ret)
	{
		cout << "c1和c2是相等的" << endl;
	}
	else
	{
		cout << "c1和c2是不相等的" << endl;
	}
	//利用成员函数判断
	ret = c1.isSameByClass(c2);
		if (ret)
		{
			cout << "成员函数判断:c1和c2是相等的" << endl;
		}
		else
		{
			cout << "成员函数判断:c1和c2是不相等的" << endl;
		}
}
```

**练习案例2**：点和圆的关系

设计一个圆形类(circle)，和一个点类(point)，计算点和圆的关系

```c++
#include<iostream>
using namespace std;
//点和圆的关系
//点类
class Point
{
public:
	//设置x
	void setX(int x)
	{
		m_X = x;
	}
	//获取x
	int getX()
	{
		return m_X;
	}
	//设置y
	void setY(int y)
	{
		m_Y = y;
	}
	//获取y
	int getY()
	{
		return m_Y;
	}
private:
	int m_X;
	int m_Y;
};
//圆类
class Circle
{
public:
	//设置半径
	void setR(int r)
	{
		m_R = r;
	}
	//获取半径
	int getR()
	{
		return m_R;
	}
	//设置圆心
	void setCenter(Point center)
	{
		m_Center = center;
	}
	//获取圆心
	Point getCenter()
	{
		return m_Center;
	}
private:
	//在类中可以让另一个类作为本类中的成员
	int m_R;//半径
	Point m_Center;//圆心
};
//判断点和圆的关系
void isInCircle(Circle& c, Point& p)
{
	//计算两点之间距离的平方
	int distance =
		(c.getCenter().getX() - p.getX()) * (c.getCenter().getX() - p.getX()) + (c.getCenter().getY() - p.getY()) * (c.getCenter().getY() - p.getY());
	//计算半径的平方
	int rDistance = c.getR() * c.getR();
	//判断关系
	if (distance == rDistance)
	{
		cout << "点在圆上" << endl;
	}
	else if (distance > rDistance)
	{
		cout << "点在圆外" << endl;
	}
	else
		cout << "点在圆上" << endl;

}
int main()
{
	//创建圆
	Circle c;
	c.setR(10);
	Point center;
	center.setX(10);
	center.setY(0);
	c.setCenter(center);
	//创建点
	Point p;
	p.setX(10);
	p.setY(10);
	//判断关系
	isInCircle(c, p);

}


```

**如何分文件编写类？**

`类名：：类内函数`

```c++
//点类头文件point.h
#pragma once
#include<iostream>
class Point
{
public:
	//设置x
	void setX(int x);

	//获取x
	int getX();

	//设置y
	void setY(int y);

	//获取y
	int getY();

private:
	int m_X;
	int m_Y;
};
//点类实现point.cpp  ->实现函数
#include"point.h"
//Point::Point作用域下的成员函数->否则默认全局函数
void Point::setX(int x)
{
	m_X = x;
}
//获取x
int Point::getX()
{
	return m_X;
}
//设置y
void Point::setY(int y)
{
	m_Y = y;
}
//获取y
int Point::getY()
{
	return m_Y;
}
//圆类头文件
#include<iostream>
using namespace std;
#include"point.h"
class Circle
{
public:
	//设置半径
	void setR(int r);

	//获取半径
	int getR();

	//设置圆心
	void setCenter(Point center);

	//获取圆心
	Point getCenter();

private:
	//在类中可以让另一个类作为本类中的成员
	int m_R;//半径
	Point m_Center;//圆心
};
//圆类实现circle.cpp
#include"circle.h"
//圆类

//设置半径
void Circle::setR(int r)
{
	m_R = r;
}
//获取半径
int Circle::getR()
{
	return m_R;
}
//设置圆心
void Circle::setCenter(Point center)
{
	m_Center = center;
}
//获取圆心
Point Circle::getCenter()
{
	return m_Center;
}


```



### 对象的初始化和清理

+ 生活中我们买的电子产品都基本会有出厂设置，在某一天我们不用的时候也会删除一些自己信息数据保证安全
+ C++中的面向对象来源于生活，每个对象也都会有初始设置以及对象销毁前的清理数据的设置

[(35条消息) C++为什么要有构造函数和析构函数_陈树振老师的博客-CSDN博客_c++ 为什么要构造函数](https://blog.csdn.net/chenshuzhenteacher/article/details/8094577)

#### 构造函数和析构函数

对象的初始化和清理也是两个非常重要的安全问题

​		一个**对象或者变量**没有初始状态，对其使用后果是未知

​		同样的使用完一个对象或变量，没有及时清理，也会造成一定的安全问题

c++利用**构造函数**和**析构函数**解决上述问题，这两个函数将会被编译器自动调用，完成对象初始化和清理工作

对象的初始化和清理工作是编译器强制我们要做的事情，因此如果**我们不提供构造和析构，编译器会提供**

**编译器提供的构造和析构是空实现**

+ 构造函数：主要作用在于创建对象时为对象的成员属性赋值，构造函数由编译器自动调用，无需手动调用
+ 析构函数：主要作用在于对象**销毁前**系统自动调用，执行一些清理工作

**构造函数语法：**`类名(){}`

+ 构造函数，没有返回值也不写void
+ 函数名称与类名相同
+ 构造函数可以有参数，因此可以发生重载
+ 程序在调用对象的时候会自动调用构造，无须手动调用，而且只会调用一次



**析构函数语法:**`~类名(){}`

+ 析构函数，没有返回值也不写void
+ 函数名称与类名相同，在名称前加上符号`~`
+ 析构函数不可以有参数，因此不可以发生重载
+ 程序在对象销毁前会自动调用析构，无需手动调用，而且只会调用一次

```c++
#include<iostream>
using namespace std;
//对象的初始化和清理
//1、构造函数  进行初始化操作
//构造和析构都是必须有的实现，如果我们自己不提供，编译器会提供一个空实现的构造和析构
class Person
{
	//构造函数
	//没有返回值，不用void
	//函数名与类名相同
	//构造函数可以有参数，可以发生重载
	//创建对象的时候，构造函数会自动调用，而且只调一次
public:
	Person()
	{
		cout << "Person构造函数的调用" << endl;
	}
	/*
	我不写的话
	自动有
	Person()
	{
	//空
	}
	*/
	//2、析构函数   进行清理的操作
	//没有返回值，不写void
	//函数名和类名相同，在名称前加~
	//析构函数不可以有参数，不可以发生重载
	//对象在销毁前  会自动调用析构函数，而且只会调用一次
	~Person()
	{
		cout << "Person的析构函数调用" << endl;
	}
	/*
	我不写的话
	自动有
	~Person()
	{
	//空
	}
	*/
};

void text01()
{
	Person p;//在栈上的数据，test01执行完毕后，释放这个对象
}

int main()
{
	text01();
	Person P;//在main函数结束后调用
	system("pause");
	return 0;
}
```

```c++
//输出
Person构造函数的调用
Person的析构函数调用
Person构造函数的调用
请按任意键继续. . .
Person的析构函数调用
```

#### 构造函数的分类及调用

**两种分类方式**：

按参数分为：有参和无参

按类型分为：普通构造（除了拷贝构造以外的都叫普通构造）和拷贝构造

**三种调用方式**

​		括号法

​		显示法

​		隐式转换法

示例：

```c++
#include<iostream>
using namespace std;
//1、构造函数的分类及调用
//分类
//按参数分类  无参构造（默认构造） & 有参构造
//按照类型分类    普通构造 & 拷贝构造
class Person
{
public:
	//构造函数
	Person()
	{
		cout << "Person的构造函数的调用" << endl;
	}
	Person(int a)
	{
		age = a;
		cout << "Person的有参构造函数的调用" << endl;
	}
	//拷贝构造函数
	Person(const Person &p)
	{
		//将传入的人身上的所有属性，拷贝到我身上
		cout << "拷贝构造函数的调用" << endl;
		age = p.age;
	}
	~Person()
	{
		cout << "Person的析构函数的调用" << endl;
	}
	int age;
};
//调用
void text01()
{
	//1、括号法
	Person p1;//默认构造函数的调用
	Person p2(10);//有参构造函数的调用
	Person p3(p2);//拷贝构造函数
	cout << "p2的年龄为："<<p2.age << endl;
	cout << "p3的年龄为：" << p2.age << endl;
	//注意事项：
	//调用默认构造函数的时候不要加小括号
	//因为下面这行代码，编译器会认为这是一个函数的声明，不会认为在创建对象
	Person p4();//无输出
	//2、显示法
	Person p5;
	Person p6 = Person(10);//有参构造
	Person p7 = Person(p6);//拷贝构造
	Person(10);//匿名对象   特点：当前的行执行结束后，系统会立即回收掉匿名对象
	cout << "aaaaaa" << endl;//匿名对象的析构在此前打印
	//注意事项2
	// 不要利用拷贝构造函数，初始化匿名对象,编译器会认为Person(p6)==Person p6;认为是对象的声明
	//Person(p6);
	//3、隐式转换法
	Person p8 = 10;//相当于写了Person P8 = Person(10)
	Person p9 = p8;//拷贝构造
}
int main()
{
	text01();
	system("pause");
	return 0;
}
```

```c++
//输出
Person的构造函数的调用
Person的有参构造函数的调用
拷贝构造函数的调用
p2的年龄为：10
p3的年龄为：10
Person的构造函数的调用
Person的有参构造函数的调用
拷贝构造函数的调用
Person的有参构造函数的调用
Person的析构函数的调用
aaaaaa
Person的有参构造函数的调用
拷贝构造函数的调用
Person的析构函数的调用
Person的析构函数的调用
Person的析构函数的调用
Person的析构函数的调用
Person的析构函数的调用
Person的析构函数的调用
Person的析构函数的调用
Person的析构函数的调用
```



#### 拷贝构造函数调用时机

c++中拷贝构造函数调用时机通常有三种情况

+ 使用一个已经创建完毕的对象来初始化一个新对象
+ 值传递方式给函数参数传值
+ 以值方式返回局部对象

```c++
#include<iostream>
using namespace std;
class Person
{
public:
	Person()
	{
		cout << "Person默认构造函数调用" << endl;
	}
	Person(int age)
	{
		cout << "Person有参构造函数调用" << endl;
		m_Age = age;
	}
	Person(const Person& p)
	{
		cout << "Person拷贝函数调用" << endl;
		m_Age = p.m_Age;
	}
	~Person()
	{
		cout << "Person析构构造函数调用" << endl;
	}
	int m_Age;
};
//拷贝构造函数调用时机
//使用一个已经创建完毕的对象来初始化一个新对象
void text01()
{
	Person p1(20);
	Person p2(p1);
	cout << "P2的年龄为" << p2.m_Age << endl;
}
//值传递的方式给函数参数传值
void doWork(Person p)
{

}
void text02()
{
	Person p;
	doWork(p);//调用拷贝构造函数
}
//值方式返回局部对象
Person doWork2()
{
	Person p1;
	cout << (int)&p1 << endl;
	cout << &p1 << endl;
	return p1;//不是返回前面的p1，而是又创建了新的p1
}
void text03()
{
	Person p = doWork2();
	cout << (int) & p << endl;
}
int main()
{
	text01();
	text02();
	text03();
	system("pause");
	return 0;
}
```

```c++
//输出
Person有参构造函数调用
Person拷贝函数调用
P2的年龄为20
Person析构构造函数调用
Person析构构造函数调用
Person默认构造函数调用
Person拷贝函数调用
Person析构构造函数调用
Person析构构造函数调用
Person默认构造函数调用
227669524
000000880D91F614
Person拷贝函数调用
Person析构构造函数调用
227669844
Person析构构造函数调用
```



#### 构造函数调用规则

默认情况下，c++编译器至少给一个类添加三个函数

+ 默认构造函数(无参，函数体为空)
+ 默认析构函数(无参，函数体为空)
+ 默认拷贝构造函数，对属性值进行拷贝

构造函数调用规则如下：

+ ==如果用户定义有参构造函数，c++不再提供默认无参构造，但是会提供默认拷贝构造==
+ ==如果用户定义拷贝函数，c++不会再提供其他函数==

有拷贝构造->必须手动添加默认构造、无参构造函数

有有参构造函数->必须手动添加无参构造函数

示例：

```c++
#include<iostream>
using namespace std;
//构造函数的调用规则
//1、创建一个类,C++编译器会给每个类都添加至少三个函数
//默认构造（空实现）
//析构函数(空实现)
//拷贝构造(值拷贝)

//2、如果我们写了有参构造函数，编译器就不再提供默认构造，依然提供拷贝构造

//如果我们写了拷贝构造函数，编译器就不再提供其他的
class Person
{
public:
	//Person()
	//{
		//cout << "Person的默认构造函数调用" << endl;
	//}
	Person(int age)
	{
		cout << "Person的有参构造函数调用" << endl;
		m_Age = age;
	}
	//Person(const Person& p)                                     默认为Person(const Person& p)  
	//{                                                             {
	//	cout << "Person的拷贝构造函数调用" << endl;                  m_Age = p.m_Age;	
	//	m_Age = p.m_Age;											}
	//}
	~Person()
	{
		cout << "Person的析构函数调用" << endl;
	}
	int m_Age;
};
void text01()
{
	Person p(19);//报错：没有合适的默认构造函数
	p.m_Age = 18;
	Person p2(p);
	cout << "p2的年龄为" << p2.m_Age << endl;
}
void text02()
	{
		Person p(20);//报错：没有合适的默认构造函数
}
int main()
{
	text01();
	text02();
	system("pause");
	return 0;
}
```

```c++
//输出
Person的有参构造函数调用
p2的年龄为18
Person的析构函数调用
Person的析构函数调用
Person的有参构造函数调用
Person的析构函数调用
```

#### 深拷贝与浅拷贝

深浅拷贝是面试经典问题，也是常见的一个坑

**浅拷贝**：简单的赋值拷贝操作(包括一切等号赋值操作)

**深拷贝**：在堆区重新申请空间，进行拷贝操作

```c++
#include<iostream>
using namespace std;
//深拷贝与浅拷贝
class Person
{
public:
	Person()
	{
		cout << "Person默认构造函数调用" << endl;
	}
	Person(int age,int height)
	{
		cout << "Person有参构造函数调用" << endl;
		m_Age = age;
		m_Height = new int(height);
	}
	//自己实现拷贝构造函数，解决浅拷贝带来的问题
	Person(const Person& p)
	{
		cout << "Person拷贝构造函数调用" << endl;
		m_Age = p.m_Age;
		m_Height = p.m_Height;//编译器默认实现就是这行代码，搬运地址，结果重复析构报错
		//深拷贝操作
		m_Height = new int(*p.m_Height);
	}
	~Person()
	{
		//析构代码，把堆区开辟的数据作释放操作
		if (m_Height != NULL)
		{
			delete m_Height;
			m_Height = NULL;
		}
		cout << "Person析构造函数调用" << endl;
	}
	int m_Age;
	int* m_Height;
};
void text01()
{
	Person p1(18,160);
	cout << "p1的年龄：" << p1.m_Age <<"身高为"<<*p1.m_Height << endl;
	Person p2(p1);//18为系统做的浅拷贝工作
	cout << "p2的年龄：" << p2.m_Age << "身高为" << *p2.m_Height<<endl;
}
int main()
{
	text01();//报错：浅拷贝带来的问题：堆区的内存重复释放
}
```

```c++
//输出
Person有参构造函数调用
p1的年龄：18身高为160
Person拷贝构造函数调用
p2的年龄：18身高为160
Person析构造函数调用
Person析构造函数调用
```



==如果属性有在堆区开辟的，一定要自己提供拷贝构造函数，防止浅拷贝带来的问题==

#### 初始化列表

[C++中为什么构造函数初始化列表 - QQLQ - 博客园 (cnblogs.com)](https://www.cnblogs.com/laiqun/p/5776212.html)

**作用**：

c++提供了初始化列表方法，用来初始化属性

**语法**：

`构造函数():属性1(值1)，属性2(值2)...{}`

示例:

```c++
#include<iostream>
using namespace std;
//初始化列表
class Person
{
public:
	//传统初始化操作
	//Person(int a, int b, int c)
	//{
	//	m_A = a;
	//	m_B = b;
	//	m_C = c;
	//}
	//初始化列表初始化属性
	Person(int a,int b,int c):m_A(a),m_B(b),m_C(c) {}
	int m_A;
	int m_B;
	int m_C;
};
void text01()
{
	Person p(1,2,3);
	cout << "m_A=" << p.m_A << endl;
	cout << "m_B=" << p.m_B << endl;
	cout << "m_C=" << p.m_C << endl;
}
int main()
{
	text01();
	system("pause");
	return 0;
}
```

#### 类对象作为类成员

c++中类的成员可以是另一个类的对象，我们称该成员为对象成员

例如：

```c++
class A{}
class b
{
   A a; 
}
```

B类中有对象A作为成员，A为对象成员

那么当创建B对象时，A和B的构造和析构的顺序是谁先谁后？

==当其他类对象作为本类成员，构造的时候先构造其他类对象，再构造自身，析构的顺序与构造相反==

示例：

```c++
#include<iostream>
using namespace std;
//类对象作为类成员
//手机类
class Phone
{
public:
	Phone(string pName)
	{
		cout << "Phone的构造函数调用" << endl;
		m_PName = pName;
	}
	~Phone()
	{
		cout << "Phone的析构函数调用" << endl;
	}
	//手机品牌名称
	string m_PName;
};
//人类
class Person
{
public:
	Person(string name, string pName):m_Name(name),m_Phone(pName)//Phone m_Phone = PName ->隐式转化法
	{
		cout << "Person的构造函数调用" << endl;
	}
	~Person()
	{
		cout << "Person的析构函数调用" << endl;
	}
	//姓名
	string m_Name;
	//手机
	Phone m_Phone;
};
//当其他类对象作为本类成员，构造的时候先构造其他类对象，再构造自身，析构的顺序与构造相反
void text01()
{
	Person p("张三", "苹果MAX");
	cout << p.m_Name << "拿着" << p.m_Phone.m_PName<< endl;
}
int main()
{
	text01();
	system("pause");
	return 0;
}
```

```c++
//输出
Phone的构造函数调用
Person的构造函数调用
张三拿着苹果MAX
Person的析构函数调用
Phone的析构函数调用
```

#### 静态成员  

静态成员就是在成员变量和成员函数前加上关键字static，称为静态成员

静态成员分为：

+ 静态成员变量
  + 所有对象共享同一份数据
  + 在编译阶段分配内存(程序运行前)
  + 类内声明，类外初始化
+ 静态成员函数
  + 所有对象共享同一个函数
  + 静态成员函数只能访问静态成员变量

==静态成员变量==：

**格式**

```c++
//类内声明
class A
{
    static int A;
}
//类外初始化
int A::A=XXX;
//访问方式
void text01()
{
	A a;
    a.A;
    A::A;
}
```



```c++
#include<iostream>
using namespace std;
class Person
{
public:
	//所有对象都共享同一份数据
	//编译阶段就分配了内存
	//类内声明，类外初始化
	static int m_A;
};
void text01()
{
	Person p;
	cout << p.m_A << endl;
}
int main()
{
	text01();
}
//报错：无法解析的外部命令：一般为link时出错
```

```c++
#include<iostream>
using namespace std;
class Person
{
public:
	//所有对象都共享同一份数据
	//编译阶段就分配了内存
	//类内声明，类外初始化
	static int m_A;
};
int Person::m_A=100;//类外初始化
void text01()
{
	Person p;
	cout << p.m_A << endl;
	Person p2;
	p2.m_A = 200;
	//居然是200
	cout << p.m_A << endl;
}
int main()
{
	text01();
}
```

```c++
#include<iostream>
using namespace std;
class Person
{
public:
	//所有对象都共享同一份数据
	//编译阶段就分配了内存
	//类内声明，类外初始化
	int m_A=100;
};
void text01()
{
	Person p;
	cout << p.m_A << endl;
	Person p2;
	p2.m_A = 200;
	//还是100
	cout << p.m_A << endl;
}
int main()
{
	text01();
}
```

```c++
#include<iostream>
using namespace std;
class Person
{
public:
	//所有对象都共享同一份数据
	//编译阶段就分配了内存
	//类内声明，类外初始化
	static int m_A;
	//静态成员变量也是有访问权限的
private:
	static int m_B;
};
int Person::m_A=100;//类外初始化
int Person::m_B = 200;
void text01()
{
	Person p;
	cout << p.m_A << endl;
	Person p2;
	p2.m_A = 200;
	//居然是200
	cout << p.m_A << endl;
}
void text02()
{
	//静态成员变量不属于某个对象上，所有对象都共享同一份数据
	//因此静态成员变量有两种访问方式
	//通过对象进行访问
	Person p;
	cout << p.m_A << endl;
	//通过类名进行访问
	cout << Person::m_A << endl;
	//cout << Person::m_B << endl;类外访问不到私有静态成员
}
int main()
{
	//text01();
	text02();
}
```

==静态成员函数==

```c++
#include<iostream>
using namespace std;
//静态成员函数
//所有的对象都共享同一个函数
//静态成员函数只能访问静态成员变量
class Person
{
public:
	//静态成员函数
	static void func()
	{
		m_A = 100;//静态成员函数可以访问静态成员变量
		cout << "static void func调用" << endl;
		//m_B = 200;//静态成员函数不可以访问非静态成员变量，无法区分是哪个对象的m_B
	}
	static int m_A;
	int m_B;
	//静态成员函数也是有访问权限的
private:
	static void func2()
	{
		cout << "static void func调用" << endl;
	}
};
int Person::m_A = 0;
//有两种访问方式
void text01()
{
	//通过对象访问
	Person p;
	p.func();
	//通过类名访问
	Person::func();
	Person::func2();//类外访问不到私有静态成员函数
}
int main()
{
	text01();
}
```

#### 析构函数功能 

**栈内存**相当于货品展示区，运行速度快，存储量少

**堆内存**相当于货品仓库，运行速度不如栈内存快，但存储量更大

```c++
Student stu1;  //在栈内存内直接分配空间
Student* stu2=new Student();  //在堆内存中分配空间
```

==析构函数==:

+ 对象过期时自动调用的特殊成员函数
+ 析构函数一般用来完成清理工作
+ 析构函数的名称是在类名前加上~
+ 析构函数没有参数且只能有一个
+ 析构函数用来释放对象使用的资源，并销毁对象的非静态(static)数据成员

无论何时一个对象被销毁，都会自动调用其析构函数（隐式结构）

**栈内存内的数据会自动调用析构函数被释放**

**但是堆内存内的数据不会自动调用析构函数，所以不会自动被释放**

**所以当使用堆内存的对象使用完毕时，一定要记得delete，释放内存**

### C++对象模型和this指针

#### 成员变量和成员函数分开存储

在C++中，类内的成员变量和成员函数分开存储

只有非静态成员变量才属于类的对象上

空对象内存为一个字节

```c++
#include<iostream>
using namespace std;
//成员变量和成员函数分开存储
class Person
{
	int m_A;//非静态成员变量   属于类的对象上
	static int m_B;//静态成员变量  不属于类的对象
	void func(){}//非静态成员函数  不属于类的对象
	static void func2() {}//静态成员函数  不属于类的对象
};
int Person::m_B = 100;
void text01()
{
	Person p;
	//空对象占用内存空间为：1
	//C++编译器会给每个空对象也分配一个字节空间，是为了区分空对象占内存的位置
	//每个空对象也应该有一个独一无二的内存地址
	cout << "size of p=" << sizeof(p) << endl;
}
void text02()
{
	Person p;
	cout << "size of p=" << sizeof(p) << endl;
}
int main()
{
	text01();
}
```

#### this指针

我们知道C++中成员变量和成员函数是分开存储的

每一个非静态成员函数只会生成一份函数实例，也就是说多个同类型的对象会共用同一块代码

那么问题是：这一块代码是如何区分哪个对象调用自己的呢？



c++通过提供特殊的对象指针，this指针解决上述问题。**this指针指向被调用的成员函数所属的对象**



this指针是隐含在每一个非静态成员函数内的一种指针

this指针不需要定义，直接使用即可

this指针的用途

+ 当形参和成员变量同名时，可用this指针区分
+ 在类的非静态成员函数中返回对象本身，可用return *this

```c++
#include<iostream>
using namespace std;
//this指针
class Person
{
public: 
	Person(int age)
	{
		age = age;//三个age在编译器里是一个age
		this->age = age;//this指针指向被调用的成员函数所属的对象
	}
	Person& PersonADDAge(Person &p)//引用指向本身内存，不加引用就是拷贝，而拷贝指向另一个内存
	{
		this->age += p.age;
		//this指向p2的指针,而*this指向的就是p2这个对象本体
		return *this;
	}
	int age;
};
//解决名称冲突
void text01()
{
	Person p1(18);
	cout << "p1的年龄为：" << p1.age << endl;
}
//返回对象本身用*this
void text02()
{
	Person p1(10);
	Person p2(10);
	//链式编程思想
	p2.PersonADDAge(p1).PersonADDAge(p1).PersonADDAge(p1);
	cout << "p2的年龄为：" << p2.age << endl;
}
int main()
{
	text01();
	text02();
	system("pause");
	return 0;
}
```

#### 空指针访问成员函数

C++中空指针也是可以调用成员函数，但是要注意到有没有用到this指针

如果用到this指针，需要加以判断保证代码的健壮性

```c++
//提高健壮性
if (this == NULL)
{
	return;
}
//防止传NULL指针崩溃


class Person
{
public:
	void showClassName()
	{
		cout << "this is Person class" << endl;
	}
	void showPersonAge()
	{
		//报错原因是因为传入的指针为NULL
		if (this == NULL)
		{
			return;
		}
		cout << "age=" << m_Age << endl;//相当于cout << "age=" << this->m_Age << endl;
	}
	int m_Age;
};
```

```c++
#include<iostream>
using namespace std;
//空指针调用成员函数
class Person
{
public:
	void showClassName()
	{
		cout << "this is Person class" << endl;
	}
	void showPersonAge()
	{
		//报错原因是因为传入的指针为NULL
		if (this == NULL)
		{
			return;
		}
		cout << "age=" << m_Age << endl;//相当于cout << "age=" << this->m_Age << endl;
	}
	int m_Age;
};
void text01()
{
	Person* p = NULL;
	p->showClassName();//可以正常调用
	p->showPersonAge();//错误  读取访问权限冲突
}
int main()
{
	text01();
}
```

#### const修饰成员函数

const限制只读状态

**常函数：**

+ 成员函数后加const我们称这个函数为常函数
+ 常函数内不可以修改成员属性
+ 成员属性声明加关键字mutable后，在常函数中依然可以修改

**常对象：**

+ 声明对象前加const称该对象为常对象
+ 常对象只能调常函数

```c++
#include<iostream>
using namespace std;
//常函数
class Person
{
public:
	//this指针的本质  是指针常量  指针的指向是不可以修改的
	//Person *const this;
	//const Person *const this;
	//在成员函数
	void showPerson()const
	{
		//this->m_A = 100;//报错
		this->m_B = 100;
	}
	void fun(){}
	int m_A;
	mutable int m_B;//特殊变量，即使在常函数中，也可以修改这个值，加上关键字mutable
};

//常对象
void text01()
{
	const Person p;//在对象前加const，变为常对象
	//p.m_A = 100;
	p.m_B = 100;//特殊值，在常对象中，也可以修改这个值
	//常对象只能调用常函数
	//p.fun();不允许//常对象不可以调用普通成员函数，因为普通成员函数可以修改成员属性
}
```

### 友元

生活中你的家有客厅(Public)，有你的卧室(Private)

客厅里所有来的客人都可以进去，但是你的卧室是私有的，也就是说只有你能进去

但是呢，你也可以允许你的好闺蜜好基友进去

在程序里，有些私有属性也想让类外特殊的一些函数或者类进行访问，就需要用到友元的技术

友元的目的就是让一个函数或者类访问另一个类中的私有成员

友元的关键字为==friend==

友元的三种实现：

+ 全局函数做友元
+ 类做友元
+ 成员函数做友元



#### 全局函数做友元

```c++
#include<iostream>
using namespace std;
//建筑物的类
class Building
{
	//goodGay全局函数是Building好朋友，可以访问Building中私有成员
	friend void goodGay(Building* building);
public:
	Building()
	{
		m_SittingRoom = "客厅";
		m_BedRoom = "卧室";
	}
public:
	string m_SittingRoom;//客厅
private:
	string m_BedRoom;//卧室
};
//全局函数
void goodGay(Building* building)
{
	cout << "好基友的全局函数正在访问" << building->m_SittingRoom << endl;
	cout << "好基友的全局函数正在访问" << building->m_BedRoom << endl;
}
void text01()
{
	Building building;
	goodGay(&building);

}
int main()
{
	text01();
}
```

#### 类做友元

```c++
#include<iostream>
using namespace std;
//类做友元

class Building;
class GoodGay
{
public:
	GoodGay();
	void visit();//参观函数访问Building中的属性
	Building* building;
};
class Building
{
	//goodgay类为本类的好朋友，可以访问本类中的私有成员
	friend class GoodGay;
public:
	Building();
public:
	string m_SittingRoom;//客厅
private:
	string m_BedRoom;//卧室
};
//类外写成员函数
Building::Building()
{
	m_SittingRoom = "客厅";
	m_BedRoom = "卧室";
}
GoodGay::GoodGay()
{
	//创建建筑物对象
	building = new Building;
}
void GoodGay::visit()
{
	cout << "好基友类正在访问：" << building->m_SittingRoom << endl;
	cout << "好基友类正在访问：" << building->m_BedRoom << endl;
}
void text01()
{
	GoodGay gg;
	gg.visit();
}
```

#### 成员函数做友元

```c++
#include<iostream>
using namespace std;
class Building;
class GoodGay
{
public:
	GoodGay();
	void visit();//让visit函数可以访问Building中私有成员
	void visit2();//让visit函数不可以访问Building中私有成员
	Building* building;
};
class Building
{
	//告诉编译器 GoodGay类下的visit成员函数作为本类的好朋友，可以访问私有成员
	friend void GoodGay::visit();
public:
	Building() :m_SettingRoom("客厅"), m_BedRoom("卧室"){};
public:
	string m_SettingRoom;//客厅
private:
	string m_BedRoom;//卧室

};
GoodGay::GoodGay()
{
	building = new Building;
}
void GoodGay::visit()
{
	cout << "visit 函数正在访问：" << building->m_BedRoom << endl;
}
void GoodGay::visit2()
{
	cout << "visit 函数正在访问：" << building->m_SettingRoom << endl;
}
void text01()
{
	GoodGay gg;
	gg.visit();
}
int main()
{
	text01();
}
```

### 运算符重载

运算符重载概念：对已有的运算符重新定义，赋予其另一种功能，以适应不同的数据类型

#### 加号运算符重载

作用：实现两个自定义数据类型相加的运算

**运算符重载也可以发生函数重载**

**实现方式**

+ 成员函数重载+号
+ 全局函数重载+号

==引用的形式传参数==

**代码格式**：

```c++
class A
{
    //成员函数重载
    A operator+(A &a)
    {
        A temp;
        temp = this->x + a.x;
        return temp
	}
    int x;
}
//全局函数重载

int main()
{
    A y1;
    A y2;
    A y =y1+y2;
    //本质上
    A y =y1.operator+(y2)
}
//全局函数重载
 operator+(A &a,A &b)
    {
        A temp;
        temp = b.x + a.x;
        return temp
	}
```

```c++
#include<iostream>
using namespace std;
//加号运算符重载
//成员函数实现
class Person
{
public:
	/*Person personAddPerson(Person* p)
	{
		Person temp;
		temp.age = this->age + p->age;
		return temp;
	}*/
	//成员函数实现
	/*Person operator+(Person& p)
	{
		Person temp;
		temp.age = this->age + p.age;
		return temp;
	}*/
public:
	int age;
};
//全局函数实现
/*Person personAddPerson(Person* p1, Person* p2)
{
	Person temp;
	temp.age = p1->age + p2->age;
	return temp;
}*/
//Person operator+(Person* p1, Person* p2)报错，不要传指针，传引用
Person operator+ (Person& p1, Person& p2)
{
	Person temp;
	temp.age = p1.age + p2.age;
	return temp;
}
//函数重载版本
Person operator+(Person& p1, int num)
{
	Person temp;
	temp.age = p1.age + num;
	return temp;
}
void text01()
{
	Person p1;
	p1.age = 10;
	Person p2;
	p2.age = 20;
	//报错：Person p3 = p1 + p2;
	//Person p3 = p1.personAddPerson(&p2);
	Person p3 = p1 + p2;
	cout << p3.age << endl;
	//Person p4 = personAddPerson(&p2, &p3);
	//本质上
	Person p5 = operator+(p1, p2);
	Person p4 = p2 + p3;
	cout << p4.age << endl;
	//运算符重载也可以发生函数重载
	Person p3 = p1 + 10;//person+int
}
int main()
{
	text01();
}
```

==内置的数据类型的表达式的运算符是不可能改变的==

==不要滥用运算符重载==

#### 左移运算符重载

可以输出自定义数据类型

```c++
#include<iostream>
using namespace std;
//左移运算符重载
class Person
{
	friend ostream& operator<<(ostream& cout, Person& p);
public:
	Person(int a, int b)
	{
		m_A = a;
		m_B = b;
	}
private:
	//利用成员函数重载左移运算符 p.operator<<(cout)简化版本p<<cout
	//不会利用成员函数重载左移运算符，因为无法实现cout在左侧
	//void operator<<(Person &p)
	//{
	//
	//}
	int m_A;
	int m_B;
};
ostream& operator<<(ostream& cout, Person& p)
{
	cout << "m_A " << p.m_A << "m_B " << p.m_B ;
	return cout;
}//本质operator <<(cout,p)简化cout<<p
void text01()
{
	Person p(10,10);
	cout << p << "hello world"<< endl;
}
int main()
{
	text01();
	system("pause");
	return 0;
}
```

#### 递增运算符重载

作用：通过重载递增运算符，实现自己的整型数据

具体实现目标：

```c++
//普通运算符重载：
int a = 10;
cout<<a++<<endl; //11
cout<<a<<endl; //11
int b = 10;
cout<<b++<<endl; //10
cout<<b<<endl;  //11
//类内实现
class MyTnteger
{
public:
    MyInteger()
    {
        m_Num=0;
	}
private:
    int m_Num;
}
MyInteger myint:
cout<<myint<<endl;//0
cout<<++myint<<endl;//1
cout<<myint++<<endl;//1
cout<<myint<<endl;//2
//前置递增
//后置递增
```

```c++
//实现
#include<iostream>
using namespace std;
//重载递增运算符
//自定义整型
class MyInteger
{
	friend ostream& operator<<(ostream& cout, MyInteger myint);
public:
	MyInteger()
	{
		m_Num = 0;
	}
	//重载前置++运算符 返回引用是为了一直对一个数据进行递增操作
	MyInteger& operator++()
	{
		//先进行++
		m_Num++;
		//再讲自身返回
		return *this;
	}
	//重载后置++运算符
	//	void operator++(int)  int 代表占位参数，可以用于区分前置和后置递增
	MyInteger operator++(int)
	{
		//先返回结果
		//先记录当时结果
		MyInteger temp = *this;
		//再递增
		m_Num ++ ;
		//最后将记录结果返回
		return temp;
	}
private:
	int m_Num;
};
//重载左移运算符
ostream& operator<<(ostream& cout, MyInteger myint)
{
	cout << myint.m_Num;
	return cout;
}
void text01()
{
	MyInteger myint;
	cout << ++(++myint) << endl;
	cout << myint << endl;
}
void text02()
{
	MyInteger myint;
	cout << myint++ << endl;
	cout << myint << endl;
}
int main()
{
	text01();
}
```

#### 赋值运算符重载

C++编译器至少给一个类添加4个函数

1.默认构造函数(无参，函数体为空)

2.默认析构函数(无参，函数体为空)

3.默认拷贝构造函数，对属性进行值拷贝

4.赋值运算符operator=,对属性进行值拷贝



如果类中有属性指向堆区，做赋值操作有时会出现深浅拷贝问题

```c++
#include<iostream>
using namespace std;
//赋值运算符重载
class Person
{
public:
	Person(int age)
	{
		m_Age = new int(age);
	}
	~Person()
	{
		if (m_Age != NULL)
		{
			delete m_Age;
			m_Age = NULL;
		}
	}
	//重载  赋值运算符
	Person& operator=(Person& p)
	{
		//编译器提供浅拷贝
		//m_Age=p.m_Age
		//应该先判断是否有属性在堆区，如果有，先释放干净，然后再深拷贝
		if (m_Age != NULL)
		{
			delete m_Age;
			m_Age = NULL;
			//返回对象本身
			return *this;
	    }
		//深拷贝
		m_Age = new int(*p.m_Age);
	}
	int* m_Age;
};
void text01()
{
	Person p1(18);
	Person p2(20);
	Person p3(30);
	p2 = p1;//赋值操作
	p3 = p2 = p1;
	cout << "p1的年龄为： " << *p1.m_Age << endl;
	cout << "p2的年龄为： " << *p2.m_Age << endl;
	cout << "p3的年龄为： " << *p3.m_Age << endl;
}
int main()
{
	text01();
	int a = 10;
	int b = 20;
	int c = 30;
	c = b = a;
	system("pause");
	return 0;
}
```

#### 关系运算符重载

**作用：**重载关系运算符，可以让两个自定义的数据类型对象进行对比操作

```c++
#include<iostream>
using namespace std;
//赋值运算符重载
class Person
{
public:
	Person(string name, int age)
	{
		m_Name = name;
		m_Age = age;
	}
	//重载==号
	bool operator==(Person& p)
	{
		if (this->m_Name == p.m_Name && this->m_Age == p.m_Age)
		{
			return true;
		}
		return false;
	}
	bool operator!=(Person& p)
	{
		if (this->m_Name != p.m_Name || this->m_Age != p.m_Age)
		{
			return true;
		}
		return false;
	}
	string m_Name;
	int m_Age;
};
void text01()
{
	Person p1("Tom", 18);
	Person p2("Tom", 18);
	if (p1 == p2)
	{
		cout << "p1和p2是相等的！" << endl;
	}
	else
	{
		cout << "p1和p2是不相等的！" << endl;
	}
	if (p1 != p2)
	{
		cout << "p1和p2是不相等的！" << endl;
	}
	else
	{
		cout << "p1和p2是相等的！" << endl;
	}
}
int main()
{
	text01();
}

```

#### 函数调用运算符重载

+ 函数调用运算符()也可以重载
+ 由于重载后使用的方式非常像函数的调用，因此**被称为仿函数**
+ 仿函数没有固定写法，非常灵活

```c++
#include<iostream>
using namespace std;
//函数调用运算符重载
//打印输出类
class MyPrint
{
public:
	//重载函数调用运算符
	void operator()(string text)
	{
		cout << text << endl;
	}
};
void MyPrint02(string text)
{
	cout << text << endl;
}
void text01()
{
	MyPrint myprint;
	myprint("hello world");//由于使用起来非常类似于函数调用，因此被称为仿函数
	MyPrint02("hello world");
}
//仿函数非常灵活，没有固定写法
//加法类
class MyAdd
{
public:
	int operator()(int num1,int num2)
	{
		return num1 + num2;
	}
};
void text02()
{
	MyAdd add;
	int ret=add(100, 100);
	cout << ret << endl;
	//匿名函数对象MyAdd()
	cout << MyAdd()(100, 100) << endl;
}
int main()
{
	text01();
	text02();
	system("pause");
	return 0;
}
```

### 继承

**继承是面向对象三大特征之一**

有些类与类之间存在特殊的关系，例如下图所示



![image-20220413185753124](C:\Users\曹建钬\AppData\Roaming\Typora\typora-user-images\image-20220413185753124.png)

我们发现，定义这些类时，下级别的成员除了拥有上一级的共性，还有自己的特性。

这时候可以考虑继承的技术，减少重复代码。

#### 继承的基本语法

例如我们看到很多网站中，都有公共的头部，公共的底部，甚至公共的左侧列表，只有中心内容不同

接下来我们用普通写法和继承的写法来实现网页中的内容，看一下继承存在的意义以及好处

```c++
#include<iostream>
using namespace std;
////普通实现页面
////Java学科视频
//class Java
//{
//public:
//	void header()
//	{
//		cout << "首页、公开课、登录、注册...（公共头部）" << endl;
//	}
//	void footer()
//	{
//		cout << "帮助中心、交流合作、站内地图...（公共底部）" << endl;
//	}
//	void left()
//	{
//		cout << "Java、Python、C++、...(公共分类列表)" << endl;
//	}
//	void content()
//	{
//		cout << "Java学科视频" << endl;
//	}
//};
////Python学科视频
//class Python
//{
//public:
//	void header()
//	{
//		cout << "首页、公开课、登录、注册...（公共头部）" << endl;
//	}
//	void footer()
//	{
//		cout << "帮助中心、交流合作、站内地图...（公共底部）" << endl;
//	}
//	void left()
//	{
//		cout << "Java、Python、C++、...(公共分类列表)" << endl;
//	}
//	void content()
//	{
//		cout << "Python学科视频" << endl;
//	}
//};
//class Cpp
//{
//public:
//	void header()
//	{
//		cout << "首页、公开课、登录、注册...（公共头部）" << endl;
//	}
//	void footer()
//	{
//		cout << "帮助中心、交流合作、站内地图...（公共底部）" << endl;
//	}
//	void left()
//	{
//		cout << "Java、Python、C++、...(公共分类列表)" << endl;
//	}
//	void content()
//	{
//		cout << "C++学科视频" << endl;
//	}
//};
//void text01()
//{
//	cout << "Java的下载视频页面如下" << endl;
//	Java ja;
//	ja.header();
//	ja.footer();
//	ja.left();
//	ja.content();
//	Python py;
//	py.header();
//	py.footer();
//	py.left();
//	py.content();
//	Cpp cpp;
//	py.header();
//	py.footer();
//	py.left();
//	py.content();
//}


//继承实现页面
// 继承的好处：减少重复代码
// class 子类：继承方式 父类
// 子类也叫派生类
// 父类也叫基类
//公共页面类
class BasePage
{
	public:
	void header()
	{
		cout << "首页、公开课、登录、注册...（公共头部）" << endl;
	}
	void footer()
	{
		cout << "帮助中心、交流合作、站内地图...（公共底部）" << endl;
	}
	void left()
	{
		cout << "Java、Python、C++、...(公共分类列表)" << endl;
	}
};
//Java页面
class Java :public BasePage
{
public:
	void content()
	{
		cout << "Java学科视频" << endl;
	}
};
class Python :public BasePage
{
public:
	void content()
	{
		cout << "Python学科视频" << endl;
	}
};
class Cpp :public BasePage
{
public:
	void content()
	{
		cout << "C++学科视频" << endl;
	}
};
//Python页面

//C++页面
void text01()
{
	cout << "Java的下载视频页面如下" << endl;
	Java ja;
	ja.header();
	ja.footer();
	ja.left();
	ja.content();
	Python py;
	py.header();
	py.footer();
	py.left();
	py.content();
	Cpp cpp;
	py.header();
	py.footer();
	py.left();
	py.content();
}
int main()
{
	text01();
	system("pause");
	return 0;
}
```

**继承的语法：**`class 子类：继承方式 父类`

eg：

`class A:Public B`

A称为子类或者派生类

B称为父类或者基类

**派生类中的成员，包含两大部分：**

一类是从基类继承过来的，一类是自己增加的成员

从基类继承过来的表现其共性，而新增的成员表现其个性

#### 继承方式

继承的语法：`class 子类:继承方式 父类`

继承方式一共有三种：

+ 公共继承
+ 保护继承
+ 私有继承

```c++
//父类：
class A
{
public:
    int a;
protected:
    int b;
private:
    int c;//子类不管怎样都不能继承
}
//公有继承
class B:public A
{
public: int a;
protected: int b;
不可访问：
    int c
}
//保护继承
class B:protected A
{
protected: 
    int a;
 	int b;
不可访问：
    int c;
}
//私有继承
class B:private A
{
private: 
    int a;
 	int b;
不可访问：
    int c;
}
```

```C++
#include<iostream>
using namespace std;
//继承方式
//公共继承
class Base1
{
public:
	int m_A;
protected:
	int m_B;
private:
	int m_C;
};
class Son1 :public Base1
{
public:
	void func()
	{
		m_A = 10;//分类中的公共权限成员 到子类中依然是公共权限
		m_B = 10;//父类中的保护权限成员 到子类中依然是保护权限
		//m_C = 10;//父类中的私有权限成员 子类访问不到
	}
};
//保护继承
 
void text01()
{
	Son1 s1;
	s1.m_A = 100;
	s1.m_B = 100;//错误 到Son1中 m_B是保护权限 类外访问不到
}

class Base2
{
public:
	int m_A;
protected:
	int m_B;
private:
	int m_C;
};
class Son2 :protected Base2
{
	void func()
	{
		m_A = 10;//分类中的公共权限成员 到子类中变为公共权限
		m_B = 10;//父类中的保护权限成员 到子类中依然是保护权限
		m_C = 10;//父类中的私有权限成员 子类访问不到
	}
};
void text01()
{
	Son2 s2;
	s2.m_A = 100; //错误 到Son2中 m_A变为保护权限 类外访问不到
	s2.m_B = 100;//错误 在Son2中 m_B是保护权限 类外访问不到
}

class Base3
{
public:
	int m_A;
protected:
	int m_B;
private:
	int m_C;
};
class Son3 :private Base3
{
	void func()
	{
		m_A = 10;//分类中的公共权限成员 到子类中变为私有权限
		m_B = 10;//父类中的保护权限成员 到子类中变为私有权限
		m_C = 10;//父类中的私有权限成员 子类访问不到
	}
};
class GrandSon :public Son3
{
	void func()
	{
		m_A = 10;//无法访问，即使是孙子也访问不到
		m_B = 10;//无法访问
	}
};
void text03()
{
	Son3 s3;
	s3.m_A = 100; //错误 到Son3中 m_A变为私有权限 类外访问不到
	s3.m_B = 100;//错误 在Son3中 m_B变为私有权限 类外访问不到
}
```



#### 继承中的对象模型

问题：从父类继承过来的成员，哪些属于子类对象中？

+ 父类中所有的非静态成员属性都会被子类继承下去
+ 父类中私有成员属性 是被编译器给隐藏了，因此是访问不到，但是确实被继承下去了

示例：

```c++
#include<iostream>
using namespace std;
//继承中的对象模型
class Base
{
public:
	int m_A;
protected:
	int m_B;
private:
	int m_C;
};
class Son :public Base
{
public:
	int m_D;
};
//利用开发人员命令提示工具查看对象模型
//跳转盘符
//跳转文件路径 cd 具体路径下
//查看命名
// cl/d1 reportSingleClassLayout类名 文件名
void text01()
{
	cout << "sizof Son=" << sizeof(Son) << endl;
	//16
	//父类中所有的非静态成员属性都会被子类继承下去
	//父类中私有成员属性 是被编译器给隐藏了，因此是访问不到，但是确实被继承下去了
}
int main()
{
	text01();
}
```

![image-20220416002645280](C:\Users\曹建钬\AppData\Roaming\Typora\typora-user-images\image-20220416002645280.png)

步骤：

+ 利用开发人员命令提示工具查看对象模型
+ 跳转盘符
+ 跳转文件路径 cd 具体路径下
+ 查看命名
+ ` cl /d1 reportSingleClassLayout类名 文件名`cl /d1

#### 继承中的构造和析构顺序

子类继承父类后，当创建子类对象，也会调用父类的构造函数

问题：父类和子类的构造和析构顺序是谁先谁后

+ 继承中的构造和析构顺序如下
+ 先构造父类，再构造子类,析构的顺序与构造的顺序相反	

```c++
#include<iostream>
using namespace std;
//继承中构造和析构顺序
class Base
{
public:
	Base()
	{
		cout << "Base 构造函数" << endl;
	}
	~Base()
	{
		cout << "Base 析构函数" << endl;
	}
};
class Son :public Base
{
public:
	Son()
	{
		cout << "Son 构造函数" << endl;
	}
	~Son()
	{
		cout << "Son 析构函数" << endl;
	}
};
void text01()
{
	//Base b;
	Son s;
	//继承中的构造和析构顺序如下
	//先构造父类，再构造子类,析构的顺序与构造的顺序相反	
}
int main()
{
	text01();
}
```

```c++
//输出
Base 构造函数
Son 构造函数
Son 析构函数
Base 析构函数
```

#### 继承同名成员处理方式

问题：当子类和父类出现同名成员，如何通过子类对象，访问子类或父类中同名的数据呢？

+ 访问子类同名成员  直接访问即可
+ 访问父类同名成员  需要加作用域

```c++
#include<iostream>
using namespace std;
//继承中构造和析构顺序
//继承中同名成员的处理方式
class Base
{
public:
	Base() :m_A(100){}
	int m_A;
	void func()
	{
		cout << "Base 下func()调用" << endl;
	}
	void func(int)
	{
		cout << "Base 下func(int)调用" << endl;
	}
};
class Son :public Base
{
public:
	Son() :m_A(200) {}
	int m_A;
	void func()
	{
		cout << "Son 下func()调用" << endl;
	}
};
//同名成员属性
void text01()
{
	Son s;
	cout << "Son 下 m_A=" << s.m_A << endl;
	//如果通过子类对象  访问到父类同名成员  需要加作用域
	cout << "Base 下 m_A=" << s.Base::m_A << endl;
}
//同名成员函数
void text02()
{
	Son s;
	s.func();//直接调用  调用子类中的同名成员
	//如果发生重载，能不能直接调用
	//s.func(100);//出错
	//如果子类中出现了和父类同名的成员函数，子类的同名成员函数会隐藏掉父类的所有同名成员函数(包括重载的版本)
	// 如果想访问到父类中被隐藏的同名成员函数，需加作用域
	s.Base::func(100);
	//如何调用父类中的同名成员函数
	s.Base::func();
}
int main()
{
	text01();
	text02();
}
```

总结：

+ 子类对象可以直接访问到子类中的同名成员
+ 子类对象加作用域可以访问到父类同名成员
+ 当子类和父类拥有同名的成员函数，子类会隐藏掉父类中的所有同名函数(包括重载)，加作用域可以访问到父类中同名函数

#### 同名静态成员处理方式

问题：继承中同名的静态成员在子类对象上如何进行访问？

静态成员和非静态成员出现同名，处理方法一致

+ 访问子类同名成员  直接访问即可
+ 访问父类同名成员  需要加作用域

```c++
#include<iostream>
using namespace std;
//继承中的同名静态成员处理方式
class Base
{
public:
	static int m_A;
	static void func()
	{
		cout << "Base static void func()" << endl;
	}
	static void func(int)
	{
		cout << "Base static void func()" << endl;
	}
};
int Base::m_A = 100;
class Son:public Base
{
public:
	static int m_A;
	static void func()
	{
		cout << "Son static void func()" << endl;
	}
};
int Son::m_A = 200;
//同名静态成员属性
void text01()
{
	//1、通过对象来访问数据
	Son s1;
	cout << "Son下 m_A =" << s1.m_A << endl;
	cout << "Base下 m_A=" << s1.Base::m_A << endl;
	//2、通过类名访问数据
	cout << "Son下m_A" << Son::m_A << endl;
	cout << "Base 下m_A" << Base::m_A << endl;
	//第一个：：代表通过类名方式访问  第二个：：代表访问父类作用域下
	cout << "Base 下m_A" << Son::Base::m_A << endl;
}
//同名静态成员函数
void text02()
{
	Son s;
	s.func();
	s.Base::func();
	//通过对象的方式
	Son::func();
	//通过类名的方式访问
	Son::Base::func();
	//子类中出现和父类同名静态成员函数，也会隐藏父类中所有同名成员函数
	//如果想访问父类中被隐藏的同名成员，需要加作用域
	Son::Base::func(100);
}
int main()
{
	text01();
	text02();
}
//输出
Son下 m_A =200
Base下 m_A=100
Son下m_A200
Base 下m_A100
Base 下m_A100
Son static void func()
Base static void func()
Son static void func()
Base static void func()
Base static void func()
```

总结：同名静态成员处理方式和非静态成员处理方式一样，只不过有两种访问的方式（通过对象和通过类名）

#### 多继承语法

C++允许一个类继承多个类

语法：`class 子类 ：继承方式 父类1，继承方式 父类2`

多继承可能会引发父类中有同名成员出现，需**加作用域**区分

**C++实际开发中不建议使用多继承**

```c++
#include<iostream>
using namespace std;
//多继承语法
class Base1
{
public:
	Base1() :m_A(100) {}
	int m_A;
};
class Base2
{
public:
	Base2() :m_A(100) {}
	int m_A;
};
//子类需要继承Base1和Base2
class Son :public Base1, public Base2
{
public:
	Son():m_C(300),m_D(400){}
	int m_C;
	int m_D;
};
void text01()
{
	Son s;
	cout << "Size of Son = " << sizeof(s) << endl;//16
	//cout << "m_A=" << s.m_A << endl;//出现二义性
	//当父类中出现同名成员，需要加作用域区分
	cout << "Base1 m_A:" << s.Base1::m_A << endl;
	cout << "Base2 m_A:" << s.Base2::m_A << endl;
}
int main()
{
	text01();
}
```



#### 菱形继承

**菱形继承概念：**

​		两个派生类继承同一个基类

​		又有某个类同时继承者两个派生类

​		这种继承被称为菱形继承，或者钻石继承‘

菱形继承产生的问题(例如 羊和驼继承了动物，而羊驼同时继承羊和驼)：

+ 羊继承了动物的数据，驼同样继承了动物的数据，当羊驼使用数据时，就会产生二义性
+ 羊驼继承自动物的数据继承了两份，其实我们应该清楚，这份数据我们只需要一份就可以

```c++
#include<iostream>
using namespace std;
//多继承语法
//动物类
class Animal { public:int m_Age; };
//利用虚继承可以解决菱形继承的问题
//继承之前加上关键字virtual变为虚继承
//vbptr: v-virtual  b-base ptr-pionter:虚基类指针   指向vbtable虚基类表（表中记录偏移量）
//Animal称为 虚基类
//羊类
class Sheep:virtual public Animal{};
//鸵
class Tuo:virtual public Animal{};
//羊驼
class SheepTuo :public Sheep, public Tuo {};
void text01()
{
	SheepTuo st;
	st.Sheep::m_Age = 18;
	st.Tuo::m_Age = 28;
	//当菱形继承，两个父类拥有的相同数据，需要加以作用域区分
	cout << "st.Sheep::m_Age=" << st.Sheep::m_Age << endl;
	cout << "st.Tuo::m_Age=" << st.Tuo::m_Age << endl;
	cout << "st.m_Age=" << st.m_Age << endl;
	//这份数据我们知道 只要有一份就可以了，菱形继承导致数据有两份，资源浪费
}
int main()
{
	text01();
}
```

#### 继承的虚函数表？

### 多态

#### 多态的基本概念

多态是C++面向对象三大特征之一

多态分为两类：

+ 静态多态：函数重载和运算符重载属于静态多态，复用函数名
+ 动态多态：派生类和虚函数实现运行时多态

静态多态和动态多态的区别：

+ 静态多态的函数地址早绑定 - 编译阶段确定函数地址
+ 动态多态的函数地址晚绑定 - 运行阶段确定函数地址

多态满足条件

+ 有继承关系
+ 子类重写父类中的虚函数

多态使用条件

+ 父类指针或引用指向子类对象

重写：函数返回值类型   函数名   参数列表  完全一致称为重写

```c++
//地址早绑定而导致预期功能无法实现
#include<iostream>
using namespace std;
//多态
//动物类
class Animal
{
public:
	void speak()
	{
		cout << "动物在说话" << endl;
	}
};
//猫类
class Cat :public Animal
{
public:
	void speak()
	{
		cout << "小猫在说话" << endl;
	}
};
//执行说话的函数
//地址早绑定，在编译阶段确定函数地址
void doSpeak(Animal &animal)
{
	animal.speak();
}	
void text01()
{
	Cat cat;
	doSpeak(cat);//动物在说话
}
```

```c++
#include<iostream>
using namespace std;
//多态
//动物类
class Animal
{
public:
	//虚函数
	virtual void speak()
	{
		cout << "动物在说话" << endl;
	}
};
//猫类
class Cat :public Animal
{
public:
	void speak()
	{
		cout << "小猫在说话" << endl;
	}
};
//狗类
class Dog :public Animal
{
public:
	void speak()
	{
		cout << "狗在说话" << endl;
	}
};
//执行说话的函数
//地址早绑定，在编译阶段确定函数地址
//如果想执行让猫说话，那么这个函数地址不能提前绑定，需要在运行阶段进行绑定，地址晚绑定
//动态多态满足条件
//1、有继承关系
//2、子类要重写父类中的虚函数
//重写：函数返回值类型  函数名  参数列表  完全相同

//动态多态的使用
//父类的指针或者引用指向子类对象

void doSpeak(Animal &animal)
{
	animal.speak();
}	
void text01()
{
	Cat cat;
	doSpeak(cat);//猫在说话
	Dog dog;
	doSpeak(dog);//狗在说话
}
```

#### 多态的原理剖析

![image-20220416214954954](C:\Users\曹建钬\AppData\Roaming\Typora\typora-user-images\image-20220416214954954.png)

#### 多态案例——计算器类

案例描述：

分别用普通写法和多态技术，设计实现两个操作数进行运算的计算器类

多态的优点：

+ 代码组织结构清晰
+ 可读性强
+ 利于前期和后期的拓展以及维护

```c++
#include<iostream>
using namespace std;
//分别利用普通写法和多态技术实现计算器
//普通写法
class Calculator
{
public:
	int getResult(string oper)
	{
		if (oper == "+")
		{
			return m_Num1 + m_Num2;
		}
		else if (oper == "-")
		{
			return m_Num1 - m_Num2;
		}
		else if (oper == "*")
		{
			return m_Num1 * m_Num2;
		}
		//如果想拓展新的功能，需要修改源码
		//在真实的开发中  提倡 开闭原则
		//开闭原则：对拓展进行开放，对修改进行关闭
	}
public:
	int m_Num1;//操作数1
	int m_Num2;//操作数2
};
void text01()
{
	//创建计算器对象
	Calculator c;
	c.m_Num1 = 10;
	c.m_Num2 = 10;
	cout << c.m_Num1 << "+" << c.m_Num2 <<"=" <<c.getResult("+") << endl;
}
//利用多态实现计算器
//多态好处
// 1、组织结构清晰
// 2、可读性强
// 3、对于前期和后期拓展以及维护性高
//实现计算器抽象类
class AbstractCalculator
{
public:
	virtual int getResult()
	{
		return 0;
	}
	int m_Num1;
	int m_Num2;
};
//加法计算器类
class AddCalculator :public AbstractCalculator
{
public:
	int getResult()
	{
		return m_Num1 + m_Num2;
	}
};
//减法计算器类
class SubCalculator :public AbstractCalculator
{
public:
	int getResult()
	{
		return m_Num1 - m_Num2;
	}
};
//乘法计算器类
class MulCalculator :public AbstractCalculator
{
public:
	int getResult()
	{
		return m_Num1 * m_Num2;
	}
};
void text02()
{
	//多态使用条件
	//父类指针或者引用指向子类对象
	AbstractCalculator* abc = new AddCalculator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 10;
	cout << abc->m_Num1 << "+" << abc->m_Num2 <<"=" << abc->getResult() << endl;
	//用完记得销毁
	delete abc;
	//减法运算
	abc = new SubCalculator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 10;
	cout << abc->m_Num1 << "-" << abc->m_Num2 << "=" << abc->getResult() << endl;
	//用完记得销毁
	delete abc;
	//乘法运算
	abc = new MulCalculator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 10;
	cout << abc->m_Num1 << "*" << abc->m_Num2 << "=" << abc->getResult() << endl;
	//用完记得销毁
	delete abc;
} 
int main()
{
	text01();
	text02();
}
```

#### 纯虚函数和抽象类

在多态中，通常父类中虚函数的实现是毫无意义的，主要都是调用子类重写的内容

因此可以将虚函数改为**纯虚函数**

纯虚函数语法：`virtual 返回值类型 函数名 （参数列表）=0`

当类中有了纯虚函数，这个类也称为抽象类

**抽象类语法**

+ 无法实例化对象
+ 子类必须重写抽象类中的纯虚函数，否则也属于抽象类

```c++
#include<iostream>
using namespace std;
//纯虚函数和抽象类
class Base
{
public:
	//纯虚函数
	//只要有一个纯虚函数，这个类就称为抽象类
	//抽象类特点
	//1、无法实例化对象
	//2、抽象类的子类 必须要重写父类中的纯虚函数，否则也属于抽象类
	virtual void func() = 0;

};
class Son :public Base
{
public:
	virtual void func()
	{
		cout << "func函数调用" << endl;
	}
};
void text01()
{
	//Base b;//抽象类无法实例化对象
	//new Base;//抽象类无法实例化对象
	Son s;//子类必须重写父类中的纯虚函数，否则无法实例化对象
	Base* base = new Son;
	base->func();
}
int main()
{
	text01();
}
```

#### 多态案例——制作饮品

制作饮品的大致流程为：煮水-冲泡-倒入杯中-加入辅料

利用多态技术实现本案例，提供抽象类制作饮品基类，提供子类制作咖啡和茶叶

```c++
#include<iostream>
using namespace std;
//多态案例2 制作饮品
class AbstractDrinking
{
public:
	//煮水
	virtual void Boil() = 0;
	//冲泡
	virtual void Brew() = 0;
	//倒入杯中
	virtual void PourInCup() = 0;
	//加入辅料
	virtual void PutSomething() = 0;
	//制作饮品
	void makeDrink()
	{
		Boil();
		Brew();
		PourInCup();
		PutSomething();
	}
};
//制作咖啡
class Coffee :public AbstractDrinking
{
public:
	//煮水
	virtual void Boil()
	{
		cout << "煮农夫山泉" << endl;
	}
	//冲泡
	virtual void Brew()
	{
		cout << "冲泡咖啡" << endl;
	}
	//倒入杯中
	virtual void PourInCup()
	{
		cout << "倒入杯中" << endl;
	}
	//加入辅料
	virtual void PutSomething()
	{
		cout << "加入糖和牛奶" << endl;
	}
};
//制作茶叶
class Tea :public AbstractDrinking
{
public:
	//煮水
	virtual void Boil()
	{
		cout << "煮农夫山泉" << endl;
	}
	//冲泡
	virtual void Brew()
	{
		cout << "冲泡茶叶" << endl;
	}
	//倒入杯中
	virtual void PourInCup()
	{
		cout << "倒入杯中" << endl;
	}
	//加入辅料
	virtual void PutSomething()
	{
		cout << "加入枸杞" << endl;
	}
};
//制作函数
void doWork(AbstractDrinking* abs)
{
	abs->makeDrink();
	delete abs;//释放，防止内存释放
}
void text01()
{
	//制作咖啡
	doWork(new Coffee);
	cout << "----------------" << endl;
	//制作茶叶
	doWork(new Tea);
}
int main()
{
	text01();
}
```

#### 虚析构和纯虚析构

多态使用时，如果子类中有属性开辟到堆区，那么父类指针在释放时无法调用到子类的析构代码



解决方式：将父类的析构函数改为**虚析构**或**纯虚析构**

虚析构和纯虚析构共性：

+ 可以解决父类指针释放子类对象
+ 都需要具体的函数实现

虚析构和纯虚析构的区别：

+ 如果是纯虚析构，该类属于抽象类，无法实例化对象

虚析构语法：

`virtual ~类名(){}`

纯虚析构语法：

`virtual ~类名()=0;`

`类名：：~类名(){}`

```c++
#include<iostream>
using namespace std;
//虚析构和纯虚析构
class Animal
{
public:
	Animal()
	{
		cout << "Animal 构造函数调用" << endl;
	}
	//纯虚函数
	virtual void speak() = 0;
	//利用虚析构可以解决 父类指针释放子类对象时不干净的问题
	//virtual ~Animal()
	//{
	//	cout << "Animal 虚析构函数调用" << endl;
	//}
	//纯虚析构 需要声明也需要实现
	//有了纯虚析构之后，这个类也属于抽象类，无法实例化对象
	virtual ~Animal() = 0;
};
Animal::~Animal()
{
	cout << "Animal 纯虚析构函数调用" << endl;
}
class Cat :public Animal
{
public:
	Cat(string name)
	{
		cout << "小猫的构造函数调用" << endl;
		m_Name = new string(name);
	}
	virtual void speak()
	{
		cout << *m_Name << "小猫在说话" << endl;
	}
	string* m_Name;
	~Cat()
	{
		if (m_Name != NULL)
		{
			cout << "Cat析构函数的调用" << endl;
			delete m_Name;
			m_Name = NULL;
		}
	}
};
void text01()
{
	Animal* animal = new Cat("Tom");
	animal->speak();
	//父类指针在析构的时候 不会调用子类中析构函数，导致子类如果有堆区属性，出现内存泄漏
	delete animal;
}
int main()
{
	text01();
}
//输出
Animal 构造函数调用
小猫的构造函数调用
Tom小猫在说话
Cat析构函数的调用
Animal 纯虚析构函数调用
```

+ 虚析构或纯虚析构就是用来解决通过父类指针释放子类对象
+ 如果子类中没有堆区数据，可以不写虚析构或纯虚析构
+ 拥有纯虚析构函数的类也属于抽象类

#### 多态案例——电脑组装



## 文件操作

# 内存模型

我们可能都知道，C++中空类的大小是1。

```c++
#include <iostream>

class EmptyA {};

int main() {
    std::cout << "sizeof EmptyA " << sizeof(EmptyA) << std::endl;
    return 0;
};
```
结果如下：

`sizeof EmptyA 1`
然而在C语言中空结构体的大小是0，空结构体大小是0我们貌似可以理解，但为什么到C++中，空类的大小却是1呢？

原因如下：

实际上，这是**类结构体实例化**的原因，空的类或结构体同样可以被实例化，如果定义对空的类或者结构体取sizeof()的值为0，那么该空的类或结构体实例化出很多实例时(创建出很多对象)，在内存地址上就不能区分该类实例化出的实例，所以，**为了实现每个实例在内存中都有一个独一无二的地址，编译器往往会给一个空类隐含的加一个字节**，这样空类在实例化后在内存得到了独一无二的地址，所以空类所占的内存大小是1个字节。

 如果现在有这样一种情况

```c++
#include <iostream>

class EmptyA {};

class B : public EmptyA {
    int b;
};

int main() {
    std::cout << "sizeof B " << sizeof(B) << std::endl;
    return 0;
};
结果如下 :
sizeof B 4
```

一个类的实例化对象所占空间的大小？ 注意不要说类的大小,是类的对象的大小。
首先，类的大小是什么？确切的说，类只是一个类型定义，它是没有大小可言的。 用sizeof运算符对一个类型名操作，得到的是具有该类型实体的大小。add charles 空结构体：struct d{} 的sizeof也是1。
如果

```
Class A; A obj; 1
```

那么sizeof(A)==sizeof(obj) 那么sizeof(A)的大小和成员的大小总和是什么关系呢，很简单，一个对象的大小大于等于所有非静态成员大小的总和。
为什么是大于等于而不是正好相等呢？超出的部分主要有以下两方面：
\1) C++对象模型本身 对于具有虚函数的类型来说，需要有一个方法为它的实体提供类型信息(RTTI)和虚函数入口，常见的方法是建立一个虚函数入口表，这个表可为相同类型的对象共享，因此对象中需要有一个指向虚函数表的指针，此外，为了支持RTTI，许多编译器都把该类型信息放在虚函数表中。但是，是否必须采用这种实现方法，C++标准没有规定，但是这几户是主流编译器均采用的一种方案。
\2) 编译器优化 因为对于大多数CPU来说，CPU字长的整数倍操作起来更快，因此对于这些成员加起来如果不够这个整数倍，有可能编译器会插入多余的内容凑足这个整数倍，此外，有时候相邻的成员之间也有可能因为这个目的被插入空白，这个叫做“补齐”(padding)。所以，C++标准紧紧规定成员的排列按照类定义的顺序，但是不要求在存储器中是紧密排列的。
基于上述两点，可以说用sizeof对类名操作，得到的结果是该类的对象在存储器中所占据的字节大小，由于静态成员变量不在对象中存储，因此这个结果等于各非静态数据成员（不包括成员函数）的总和加上编译器额外增加的字节。后者依赖于不同的编译器实现，C++标准对此不做任何保证。
C++标准规定类的大小不为0，空类的大小为1，当类不包含虚函数和非静态数据成员时，其对象大小也为1。 如果在类中声明了虚函数（不管是1个还是多个），那么在实例化对象时，编译器会自动在对象里安插一个指针指向虚函数表VTable，在32位机器上，一个对象会增加4个字节来存储此指针，它是实现面向对象中多态的关键。而虚函数本身和其他成员函数一样，是不占用对象的空间的。 我们来看下面一个例子：（此例子在Visual C++编译器中编译运行）

```c++
#include <iostream>
using namespace std;
class A { };
class B {
char ch;
void func() { }
};
class C {
char ch1; //占用1字节
 char ch2; //占用1字节
 virtual void func() { }
};
class D {
 int in;
 virtual void func() { }
};
 void main() {
A a;
B b;
C c;
D d;
cout<<sizeof(a)<<endl;//result=1   
cout<<sizeof(b)<<endl;//result=1   //对象c扩充为2个字，但是对象b为什么没扩充为1个字呢（空类的对象一个字节，含一个char的类类对象也为一个字节。）？因为B类只有一个成员变量，普通成员函数不占用内存。
cout<<sizeof(c)<<endl;//result=8   
//对象c实际上只有6字节有用数据，但是按照上面第二点编译器优化，编译器将此扩展为两个字（add charles 字节对齐），即8字节
cout<<sizeof(d)<<endl;//result=8   
}  123456789101112131415161718192021222324252627
```

综上所述：
一个类中，虚函数、成员函数（包括静态与非静态）和静态数据成员都是不占用类对象的存储空间的。
对象大小= vptr(可能不止一个，这个很难确定，不过试过，类中定义了一个virtual函数，仍然为占用4个字节) + 所有非静态数据成员大小 + Aligin字节大小（依赖于不同的编译器）

**c++空类实例大小不是0原因？**
初学者在学习面向对象的程序设计语言时，或多或少的都些疑问，我们写的代码与最终生编译成的代码却　大相径庭，我们并不知道编译器在后台做了什么工作．这些都是由于我们仅停留在语言层的原因，所谓语言层就是教会我们一些基本的语法法则，但不会告诉我们为什么这么做？今天和大家谈的一点感悟就是我在学习编程过程中的一点经验，是编译器这方面的一个具体功能．
首先：我们要知道什么是类的实例化，所谓类的实例化就是在内存中分配一块地址．
那我们先看看一个例子：

```c++
#include<iostream.h>
class a {};
class b{};
class c:public a{
 virtual void fun()=0;
};
class d:public b,public c{};
int main()
{
 cout<<"sizeof(a)"<<sizeof(a)<<endl;
 cout<<"sizeof(b)"<<sizeof(b)<<endl;
 cout<<"sizeof(c)"<<sizeof(c)<<endl;
 cout<<"sizeof(d)"<<sizeof(d)<<endl;
 return  0;}
程序执行的输出结果为：
sizeof(a) =1
sizeof(b)=1
sizeof(c)=4
sizeof(d)=8 #charlse# 这里错误，这个调试中是4

#charles#下列是例子
#include <iostream>
using namespace std;

class a {};
class b1{};
class b{
char a;
};
class c:public a{
 virtual void fun()=0;
};
class d:public b,public c{};
class e:public b1,public c{};
int main()
{
 cout<<"sizeof(a)"<<sizeof(a)<<endl;
 cout<<"sizeof(b)"<<sizeof(b)<<endl;
 cout<<"sizeof(c)"<<sizeof(c)<<endl;
 cout<<"sizeof(d)"<<sizeof(d)<<endl;#这种情况是8
 cout<<"sizeof(e)"<<sizeof(e)<<endl;#这种情况是4
 return  0;
}12345678910111213141516171819202122232425262728293031323334353637383940414243
```

为什么会出现这种结果呢？初学者肯定会很烦恼是吗？类a，b明明是空类，它的大小应该为为０，为什么　编译器输出的结果为１呢？这就是我们刚才所说的实例化的原因（空类同样可以被实例化），每个实例在内存中都有一个独一无二的地址，为了达到这个目的，编译器往往会给一个空类隐含的加一个字节，这样空类在实例化后在内存得到了独一无二的地址．所以a，b的大小为１．
而类c是由类a派生而来，它里面有一个纯虚函数，由于有虚函数的原因，有一个指向虚函数的指针（vptr），在３２位的系统分配给指针的大小为４个字节，所以最后得到c类的大小为４．
类d的大小更让初学者疑惑吧，类d是由类b，c派生迩来的，它的大小应该为二者之和５，为什么却是８呢？这是因为为了提高实例在内存中的存取效率．类的大小往往被调整到系统的整数倍．并采取就近的法则，里哪个最近的倍数，就是该类的大小，所以类d的大小为８个字节．
当然在不同的编译器上得到的结果可能不同，但是这个实验告诉我们初学者，不管类是否为空类，均可被实例化（空类也可被实例化），每个被实例都有一个独一无二的地址．
我所用的编译器为vc++ 6.0．

下面我们再看一个例子．

```c++
#include<iostream.h>
class a{
pivate: 
int data;
};
class b{ 
private:
     int data;
  static int data1;
};
 int b::data1=0;
 void mian(){
 cout<<"sizeof(a)="<<sizeof(a)<<endl;
 cout<<"sizeof(b)="<<sizeof(b)<<endl;
}123456789101112131415
```

执行结果为：

```c++
sizeof(a)=4;
sizeof(b)=4;12
```

为什么类b多了一个数据成员，却大小和类a的大小相同呢？因为：类b的静态数据成员被编译器放在程序的一个global data members中，它是类的一个数据成员．但是它不影响类的大小，不管这个类实际产生　了多少实例，还是派生了多少新的类，静态成员数据在类中永远只有一个实体存在，而类的非静态数据成员只有被实例化的时候，他们才存在．但是类的静态数据成员一旦被声明，无论类是否被实例化，它都已存在．可以这么说，类的静态数据成员是一种特殊的全局变量．
所以a，b的大小相同．

下面我们看一个有构造函数，和析构函数的类的大小，它又是多大呢？

```c++
#include<iostream.h>
class A{
public :
 A(int a){
  a=x;}
 void f(int x){
  cout<<x<<endl;}
 ~A(){}
private:
   int x;
   int g;
   };
class B{
public:
 private:
 int  data; int data2;
 static int xs;
};
int B::xs=0;
void  main(){
 A s(10);
 s.f(10);
 cout<<"sozeof(a)"<<sizeof(A)<<endl;
 cout<<"sizeof(b)"<<sizeof(B)<<endl;
}12345678910111213141516171819202122232425
```

程序执行输出结果为：

```c++
sizeof(a) 8
sizeof(b) 812
```

它们的结果均相同，可以看出类的大小与它当中的构造函数，析构函数，以及其他的成员函数无关，只与它当中的成员数据有关．
从以上的几个例子不难发现类的大小：
１．为类的非静态成员数据的类型大小之和．
２．由编译器额外加入的成员变量的大小，用来支持语言的某些特性（如：指向虚函数的指针）．
３．为了优化存取效率，进行的边缘调整（字节对齐）．
４　与类中的构造函数，析构函数以及其他的成员函数无关．



**1.[Effective C++原则07]：为多态基类声明virtual 析构函数。**

[如果不]: 如果不声明为析构函数，可能出现的结果如下：Derived对象的成分没有被销毁，形成资源泄露、在调试上会浪费很长时间。

 

class CSimpleClass 

 

1. { 
2. **public**: 
3. CSimpleClass(){ cout << "CSimpleClass" <<endl; } 
4. ~CSimpleClass() { cout <<"~CSimpleClass" << endl; } 
5. **private**: 
6. }; 
7.   
8. **class** CDerived : **public** CSimpleClass 
9. { 
10. **public**: 
11. CDerived() { cout << "CDerived" << endl; } 
12. ~CDerived() { cout << "~CDerived" << endl; } 
13. **private**: 
14. }; 
15.   
16. int main() 
17. { 
18. CSimpleClass *pSimple = **new** CDerived; 
19. **delete** pSimple; 
20.   
21. **return** 0; 
22. } 

执行结果如下：

![img](https://img-my.csdn.net/uploads/201210/14/1350175128_6776.jpg)

显然，CDerived 对象没有被析构！

**1、** **造成上述不同的原因何在？**

“C++标准”明确指出，当派生类对象经由一个基类指针pBaseObject被删除，而该基类带有一个non-virtual析构函数，其结果未有定义（即不可预知）。实际执行时，如上面第一个图示，会产生bug，派生类的对象没有被销毁。

这就形成诡异的“局部销毁”对象，形成资源泄露。

 

**2、** **什么时候需要基类析构函数声明为虚函数？什么时候不需要基类的析构函数为虚函数？**

​    该问题涉及析构函数何时应该为虚函数。注意：对于上面的基类BaseClass，

​    若析构函数不为虚函数，sizeof(BaseClass) = 1。

​    若析构函数为虚函数，sizeof(BaseClass) = 4。

​    至于为什么包含构造函数、非虚析构函数的类的大小为1个字节。解释如下：

​    空类类的大小比如BaseClass没有构造、析构函数，本来sizeof(BaseClass)应该为0，但是我们声明该类型实例的时候，必须在内存中占用一定的空间，否则无法使用这些实例。至于占用多少内存，由编译器决定，visual studio中每个空类型的实例占用1个字节的空间。

​    而加上构造函数、析构函数或其他非虚类型的函数以后呢？由于这些非虚类型的函数的地址只与类有关，而与类的实例无关，编译器**不会因为非虚函数的增加而添加任何额外的信息。**

​    那么为什么析构函数变成虚函数后，大小就变成4个字节了呢？主要原因是：C++一旦发现类中有虚函数，就会为该类生成虚函数表，并在该类型的每一个实例中添加指向虚函数表的指针。在32位机器上，一个指针占4个字节的空间，所以求sizeof大小为4。而在64位机器上，一个指针占用8个字节的空间，因此sizeof大小为8。

​    即为类析构函数声明为虚析构函数是以付出内存为代价的。所以，无端将所有类的析构函数声明为虚函数，就向从未声明它们是虚函数一样，都是错误的。

 

**总结如下:**

（1）带多态性质的基类应用声明一个虚析构函数。如果类中带有任何虚函数，它就应该拥有一个虚析构函数；

（2）设计类的目的如果不作为基类，或者不是为了具备多态性，就不应该声明虚析构函数。

——参考《Effective C++》条款7；《剑指Offer》

 

 

**2.[Effective 原则09]：绝不在构造和析构过程中调用virtual函数。**

【原因】:base class的执行更早于derived class的构造函数，当base class的构造函数执行的时候derived class的成员变量尚未初始化。

【如果不】：执行的结果不会动态联编，依然执行其所在层的虚函数。

【示例如下】:

1. **class** CSimpleClass 
2. { 
3. **public**: 
4. ​    CSimpleClass() { cout << "CSimpleClass"<< endl; foo();} //调用了本层的foo  
5. ​    **virtual** ~CSimpleClass() { cout <<"~CSimpleClass" << endl; foo();} //调用了本层的foo  
6. ​    **virtual** **void** foo() { cout << "CSimpleClass::foo()" << endl; } 
7. **private**: 
8. }; 
9.   
10. classCDerived : **public** CSimpleClass 
11. { 
12. **public**: 
13. ​    CDerived() { cout <<"CDerived" << endl; foo(); } 
14. ​    ~CDerived() { cout <<"~CDerived" << endl; foo(); } 
15. ​    **void** foo() { cout<< "CDerived::foo()" << endl; } 
16. **private**: 
17. }; 
18.   
19. int main() 
20. { 
21. ​    CSimpleClass *pSimple = **new** CDerived; 
22. ​    **delete** pSimple; 
23.   
24. ​    **return** 0; 
25. }  

执行结果如下：

![img](https://img-my.csdn.net/uploads/201210/14/1350175233_2869.jpg)

 

**3.综合1,2的笔试题如下：**

1. **class** CBase 
2. { 
3. **public**: 
4. ​    CBase(){ cout << "CBase ctor" << endl; foo(); }  //调用本层的foo  
5. ​    ~CBase() { cout<< "CBase dtor" << endl; foo(); } //未加virtual，且调用本层的foo  
6. **private**: 
7. ​    virtualvoid foo(){ cout << "Base::foo()" << endl; } //  
8. }; 
9.   
10. **class** CDerived : **public** CBase 
11. { 
12. **public**: 
13. ​    CDerived(){cout << "CDerived ctor" << endl; foo(); } 
14. ​    ~CDerived(){cout << "CDerived dtor" << endl; foo(); } 
15.   
16. **private**: 
17. ​    **virtual** **void** foo(){ cout << "Derived::foo()" << endl; } 
18. }; 
19.   
20. int main() 
21. { 
22. ​    CBase*pBase = **new** CDerived; 
23. ​    **delete** pBase; 
24.   
25. ​    **return** 0; 
26. } 

结合原则1,2.正确的输出结果是：

![img](https://img-my.csdn.net/uploads/201210/14/1350175330_6811.jpg)

显然，1.CDerived的析构函数不会被调用，因为CBase的析构函数非虚函数。

2.在CBase的构造和析构函数中调用虚函数，仅会执行本层的定义，不会下调。还是遵照**[Effective** **原则09]****：绝不在构造和析构过程中调用virtual函数为上策。**

地址早绑定？

函数指针？

为什么虚析构不像虚函数那样会覆盖基类析构？
