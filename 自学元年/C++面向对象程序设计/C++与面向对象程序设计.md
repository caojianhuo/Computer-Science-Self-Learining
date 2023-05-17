

[C++课程总结](https://blog.csdn.net/piaopu0120/article/details/89473707)

[C++课程总结第二弹](https://blog.csdn.net/weixin_46399567/article/details/117303155)

[c++进阶](http://c.biancheng.net/cpp/biancheng/view/2227.html)

[编译流程](https://blog.csdn.net/qq_52269550/article/details/120613304)

[C++类和对象（class和object） (biancheng.net)](http://c.biancheng.net/cplus/class/)

[C++构造函数初始化列表 (biancheng.net)](http://c.biancheng.net/view/2223.html)

## ==class1==

```c++
#include "stdafx.h"
#include<iostream>
using namespace std
// a better c
//封装
//继承
//多态
//设计模式 
Windows Programming
//L 1.常量宏
#define PI 3.14
#define STU_CNT 201//消除神仙数
//2.函数宏（减少开销 
#define ARRay_SIZE(a) sizeof(a)/sizeof(a[0])
#define ADD(a,b)  (a+b) 
//3.控制宏，开关
# ifdef LOCAL_VER 
cout << "connect ximenzi" <<end1;
#else 
cout <<"conect other type "<< end1;
# endif 
return 0;
//3.1头文件里边有什么 macro  function declaration   struct Node{int date;Node next}
如果多次包含，重定义
标准头文件写法
# ifndef MY_H
# define MY_H
endif  
int main(int argc,char* argv[]) 
{
	int a[STU_CNT]
	
	
	return 0;
}

extern"C" void c_fun()//c++从c中调 

// about function in cpp
// 1.overloading重载     同名函数，不同参数 不能通过返回值重载 
void Print(int i)
{
	
 } 
 void Print(char *str)
 {
 	
 }
 //2.default parameter
 viod f(int a,int b,int c=5) //不允许 void f(int a,int b=1,int c) 
 后续调用可以只a,b调用 
 
 
 
 
 如果声明有，后续就不能有
 viod f(int a,int b=1,int c=5)
 void f(int a,int b=1,int c=5)//需要 void f(int a,int b,int c)
 //占位符//占位参数（int） //需要符合overloading 
 void f3(int)    f3 
 {
 	
 }
```

+ 























## ==class2==

```c++
#include"stdafx.h"
#include<IOSTREAN>
using namespace std;
//a better c
//object-oriented programming
//everything is object万事万物皆面向对象
//封装（1个类）、继承（类与类）、多态（类行为）
//面向过程（事为中心）   面向对象（c++,java,Python)(物中心）
//仅仅是相关数据的集合，与类型相关的操作独立于类型之外
//simular-67 class
//access control    struct不写访问控制默认共有，class不写访问控制默认私有
class Student//self-definition type
{
private：//访问控制符,私有
	//attribute /data member 
	int id;
	char* name;
public://访问控制，公有
	int age；
	void setAge(int aage);
	int getAge
		//method /function member
		void initializeStu(char* aname, int aage);
	//constructor 构造函数、构造器（用于初始化
	Student(char* aname, int aage)
		Student(int aage)//类内部重载，可行
		Student();//默认有的构造函数，不可见，现在是试图模仿，一写就没了//default constructor
};
Student::Student(char* aname, int aage)
{
	age->aage;
	name->aname;

}
Student::Student()
void Student::intializeStu(char* aname, int aage)
{
	age = aage;//蕴含this->age=aage;    //the hidden this pointer
	name = aname;
}
void InitializeStudent(Student* s, char* aname, int aage)
{
	s->age = aage;
}
//占多少内存：runtime-memory   类唯一对象（内存不重要）无穷多
#pragma pack(1)//(放入头文件，可压缩为13bit)为什么不压缩？对性能无利（合并复杂
Struct Test
{
	int i;//4
	double d;//8
	char;//1
	//占24字节（3*8，按大分配
	int i；
	char c;
	double d;
	//占16字节
	void fun()；//不占内存
};
void Test ::fun()

struct Test
{
	int a : 1;
	int b : 1;
	int c : 1;//位结构，按位描述  4bit  int意味着总体是int  a只有一个bit

};




int main(int argc,char*argv[])
{
	int i;
	Student s1,s2;

	s1.intializeStu("Zhangsan",18)//初始化
	s2.intializeStu("Lisi",20)//初始化
	Student s("zhangsan",18)//构造函数初始化
	
	printf("Hello World!\n");
	return 0;

}
```

## ==clsss3==

```c++
//bugs of pointers
//const
//pass by value vs.pass by address
//static
//new delete
//namespace
calss wheel
{
	int i;
}
class SelfDrivingSys
{
	int ii;
};
class Car
{
	Wheel w[4];//value——best(汽车都有的
	Wheel* p_w;//handle--worse
	SlefDrivingSys *p_sys;//--best（汽车可有可无
};

class Test
{
	//attrribute
	int i;//value
	int* p//handle句柄
		public：
		//constructor
		Test(int ai, int aj)；
		//destructor
		Test();//析构不会重载，在消亡时调用，重载——需要传不同参数，析构不需要传
	//如果构造里有动态内存new，一定会有析构
	// 构造里没有new，也可能有析构 析构可以释放本类所有函数调用的一切内存机构
	//构造中不要做与初始化无关的事
	// 析构中不要做与清空内存无关的事
		//使用时机——value or handle?:这个成员是不是必有属性
};
Test：：~Test()
{
	cout << "destructor" << endl;
}
Test::Test(int ai)
{
	i = ai;
	p=NULL//指针必须初始化   
}
Test::Test(int ai, int aj);
{
	i = ai;
	p=new int(aj)
}
int main(int argc, char argv[])
{
	Test t1（1, 2);
	//...
	cout<<"**********"<<endl
	return 0;
}
//memory leak   不可见，对程序没有伤害，机器越来越慢
//问题来源：指针指到一个无限大的空间，最后释放所指的空间怎么释放？--析构


//reference   引用：a safe pointer
//借值之名，行指针之实
void fun(int& m)//传
{
	m++;
}
//memory
//代码区  取决于exe有多大 运行时代码区稳定
// 全局变量区   默认清空，局部变量不清空得赋值   int *p=&g_i;  cout<<"*(p+100)<<endl';"   main()之前全局变量清空   局部变量在main之后
//runtime memory

//stack     vs.     heap(malloc/)
//放堆区（离散）&没有析构（需要有保洁clean一直跟着）——c语言慢
//栈区连续——运行快
//local var            dynamic memory alloc
//连续内存               离散空间
//                       内存碎片化 

//拷贝构造：拿一个已存在的对象生成一个新的  copy construction
//bitwise copy 默认就是  浅拷贝（肤浅 类似c语言memorycopy     倘若出现拷贝对象是带有指针的——后果：一个蚂蚱被两根绳子拉
//logical copy 深拷贝     Test（const Test& t）拷贝构造
//pass by value vs.pass by address
// 功能input                      input/output
//性能  sizeof(value)               sizeof(int)
//其他   拷贝构造                    nothing
// never pass by value(自定义类型class               void fun（Test t）绝对不行
//build-in type爱咋传咋传        self-defintion type
/*
class Test
{
	int i;
	int*j
	Test(const


}
*/

int* fun2()
{
	int a = 10;
	return &a;//拿到一个空内存
}
//常见错误：
//fly pointer永远不要定义一个指针，除非定义为NULL
//re-free不要重复释放
//return address of local variable
//bitwise copy
//写为
if（p!=NULL)
{
	free(p)
}
int main(int arge, char* argv[])
{
	int* pi;
	//直接写int& r;错误——无野引用
	int a = 10;
	int& r = a;//定义了a的一个引用
	r++;
	fun(a);
	cout << a << end;

	return 0;


	//指针是变量，引用是常量   只有常量只有一次机会赋值  
	int* p = &a;
	p = &b;//指针可以改变赋值

	int& r = a;
	r = b;//a=b  &r一直对应a
```

+ attrribute value or handle（传一个值还是一个句柄？）

```c++
#include<iostream>
using namespace std;
#include<stdafx.h>
int g_c
void fun()
{
	static int i = 0;//只被创建一次，不再释放（类似全局)//存储在全局变量区
	i++;
	cout << i << endl;
}

//想要在另一个文件里调用这里的全局变量，全局默认本文件//extern int g_c    extern void str2int()函数默认全文件 可以不写  //external link     
static void str2int()//函数访问范围从全文件改为当前文件no link
//彼此感知
class Test
{
	static
};

//design pattern设计模式23种、3类（构建型模式）、（结构型）、（行为型）
// 单件模式
class Single
{
	static Single* self;//静态成员，不允许初始化，全类共享
	Single();
public:
	static Single*get_instance()
};
Single* Single::get_instance()
{
	if (self == NULL)
		self = new Single();
		return self;
}
Single* Single::self = NULL;
//framework 框架Qt
//constant const
void fun(const int* i)
{
	//仅仅是读一读（input）要用const避免修改
	(*i)++；
}//const修饰不能写入
//const parameter*
//const return value
class Const
{
	//const int i;
	enum{tcp,udp};//枚举型 此时tcp=0，udp=1
	//类中使用在定义本类的常量
public:
	void fun()const;//屁股后面跟const显式声明可调用，常量可调用，变量更行,但只能读，不允许写
	//一旦函数声明为静态，则失去this指针，只允许操作静态成员
};
void Const：：fun() const
{
	cout << j << endl;
	j++;//错误，不可改
}
//const data member
//const function mnmber
//自学：UDP socket完成两个计算机（或两个程序）
//放送内容1.一个字符串
//发送内容2.一个数据对象
sendto
recvform()

int main(int argc,char argv[])
{
	//class private public this
	//constructor destructor copy coins
	//reference
	//static
	//const
	//new delete
	//operator overloading
	//static     与全局有关
	//1.static local var 保值，计数
	static int i = 0;
	cout << &i << endl;
	cout << &g_c << endl;
	//static function  与extern相反
	//static global var      全局变量前再用static的话就算其他文件用extern 链接会失效
	//static data member    彼此感知（全局变量max 、调用函数~~~） 本类所有函数共享的空间
	//static function         可以被类名直接调用
	Ctime ：：GetCurrentTime();
	recvfrom();
	//malloc  free库函数
	//new delete operator 运算符，与+ -同级
	//new=malloc+constructor
	//delete=destructor+free左右有先后
	//   Test *p1=new Test；new delete不可与malloc串用
}
```

[(33条消息) C++ UDP socket编程_ShirleyQueen321的博客-CSDN博客_c++ udp编程](https://blog.csdn.net/weixin_40569991/article/details/82960809)

# ==class5==

```c++
#include<iostream>
using namespace std;
//inheritance&composition
//reuse 代码的重用
//人月：一个程序员工作多少月
//computer
//类与类的关系——继承
//共性与特性
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
	return this->price；
}
void Computer::service
{
	cout << "service" << endl;
}
class Macbook : public Computer
{

};//继承，括号里可以空白
//特性
class Macbook : public Computer
{
public:
	void service()
};
void Mac::service()
{
	if (< 1)
		cout << "new Mac" << endl;
	else
		Computer::service();//reuse   直接写service重调用
}
//父类中定义方法A,子类中又有方法B，那必有A出现——否则是对父类特性的否定
//is a是
//is like a像
class Base//基类
{
public:


};
class Dervied :public Base//延伸类
{
public:
	void fun();
};//错误，不应该只动一部分     削弱父类接口
void Dervied::fun(){}
class Engine
{
public:
	void run();
};
void Engine::run(){}
class Car
{
	Engine e;
public:
	void run();
};
void Car::run()
{
	e.run;
	cout << "car is running" << endl;
}
int main(int argc, char* argv[])
{
	Computer C;
	Macbook mac;
}
//电脑中service有必然关系，汽车run函数和引没有关系
//创建子类对象时调用父类对象时会不会调用父类对象的构造函数---当然会调用！而且是先父类后子类（子类前包着一个父类对象）析构时先子类后父类——先消亡子
//如果父类  需要传参数 子类在构造时Derived::Derived():Base(1)以传参数  称;Base(ai)构造初始化列表 construction initialization list
//如果是组合（上面的car和enigine）  同样会调用enigine构造           如果enigine也没有默认构造需要Car::Car():e(1)
//按定义的顺序初始化Test：：Test(int a):i(a),j(i)

//私有继承,仅为了维持语法正确性——一文不值
class Base
{
public:
	void fun();
};
void Base::fun()
{

}
class Dervied : Base
{

};//=class Dervied : private Base选择私有继承 父类public中的在子类看来就是降级为private    削弱父类接口
//正常继承：
class Dervied :public Base


class Base
{
private://最少见
protected://对类外私有，对子类public
	int i;
public:
};
//多重继承  c++的类可以有多个父类   ----可能会有菱形继承()   事实上也只是混合语法，不该使用  
class Dervied :public Base1,Base2

```

# class6

```C++
//重用——多态性
#include<iostream>
using namespace std;
class Pet
{
	int age;
	char* name;
public:
	//虚函数
	//pure virtual纯虚函数
	//若一个类中含有纯虚函数（有一个就行），则称之为抽象类
	virtual void Speak()=0;
	virtual void Sleep();
	//如何保证多态？一个类有一个虚函数表，一个对象多一个虚指针，指向本类的虚函数
};
//abstract class抽象类不可以实例化（不能有对象）
//用途1.约束一个类家族的共性行为    抽象类
//用途2.连接本不相关的类家族，抽象其共性行为
//Java里只能有一个父类，但可以实现多个接口，->接了两个不相关的类
class NwMsg
{
public:
	virtual void Send() = 0;
	virtual void Recv() = 0;
	virtual void Code() = 0;
	virtual void Decode() = 0;
	//如果继承一个抽象类，也不一定实现所有的四个函数->又产生了抽象类，即不能有实例
};
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
//void Pet::Speak()
//{
//	cout << "Per::Speak" << endl;
//}   
void Pet::Sleep()
{
	cout << "Per::Sleep" << endl;
}
void Dog::Speak()
{
	cout<<"wa" << endl;
}
void Cat::Speak()
{
	cout << "miao" << endl;
}
//binding 绑定：将函数的一次调用，与函数入口地址相互映射的过程，称为绑定
//early binding:前绑定（
//later binding: runtime/dynamic binding
//never pass by value!!!   自定义类型千万不要传value  除了int等固有的
void Needle(Pet& pet)//为什么要是引用？ void Needle(Pet pet)  // 会调用父类的拷贝构造，会成为父类的虚指针，虚指针由构造函数初始化
{
	/*
	if pet is a Dog
	Dog::Speak
	else if pet is a Cat
	Cat::Speak
	*/
	pet.Speak();//多态（多种可能执行的形态）
	//继承是多态的前提
}
//构造函数会是虚函数吗  ->虚函数判断原则：是否有二义性    构造与虚函数无缘，new 啥调啥的构造函数
//析构一定是虚函数   不完善，应该把父类的析构给virtual
//虚函数有损性能  性能：时间复杂，空间复杂：因为多态产生贼多虚指针，损性能
//如果一个类里有一个虚函数，则其他的函数能写成虚函数就写成虚函数(没说纯虚函数)，反正有损性能，则放开虚，即写类的能虚的全虚，构造和static不能虚
class NwMsg
{
public:
};
int main(int arge, char* argv[])
{
	Dog dog;
	//upcasting:向上类型转换  //downcasting 向下类型转换是危险的
	Needle(dog);
	cout << sizeof(Pet) << endl;
	cout << sizeof(dog) << endl;
	Dog dog1, dog2;
	cout << *(int*)&dog1 << endl;
	cout << *(int*)&dog2 << endl;
	Needle(dog1);
	Cat cat;
	memcpy(&pet,&cat,4);
	pet.Speak();
	memcpy(&dog1, &cat, 4);
	dog1.Speak();  //不发生多态
	return 0;
}
//函数名->函数指针，指向函数执行的第一步
```



# 

























