# C++

## day1

```c++
#include "stdafx.h" // 包含头文件（程序员自定义的头文件用双引号）
#include <iostream> // 包含头文件（系统提供的头文件）
```

- 输出

  - ```C++
    // （1）标准输出
    #include "stdafx.h"
    #include <iostream>
    int main(){
      std::cout << "Hello World" << std::endl;
      system("pause");	// 暂停
    }
    
    // （2）采用引用命名空间输出
    #include "stdafx.h"
    #include <iostream>
    using namespace std;
    int main(){
      cout << "Hello World" << endl; 
      system("pause");	// 暂停
    }
    ```

- 换行符：`\n`

- 输入

  - ```C++
    int x,y;
    cin >> x >> Y;
    cout << "X=" << x << endl;
    cout << "Y=" << Y << endl;
    ```

- 自定义函数

  - ```c++
    void func(int a=5, int b=6)	// 默认参数
    ```



****



- 引用：`&`

  - 也可以叫**引用**，**指向变量**。如果直接输出`&ref`那么就**输出一个地址(这是一个全新的地址)**

  - ```C++
    int x = 10;
    int &ref = x;	//声明普通引用
    cout << "X=" << x << endl;	// 10
    cout << "ref=" << ref << endl;	// 10
    cout << "&ref=" << &ref << endl;	// 0x123456
    ```

  - ref 指向 x，如果 x 的值发生改变，则ref的值也会改变

  - ```C++
    x = 20; // ref是20
    ref = 20; // x也是20
    ```

- 常量：`const`

  - 常量在定义后不能修改。

  - ```c++
    // （1）定义常引用
    int y = 100
    const int &refy = y; // 声明常引用
    // refy = 200 // 这个时候会报错
    y = 200;	// 正确
    
    // （2）定义常量
    const int z = 300; // 定义后不能修改
    ```

- 指针：`*`

  - 指针存放着**变量地址**，如果指针加上`*`则表示**值**。

  - ```C++
    int a1 = 3;	// 一、最简单的赋值
    const int a2 = a1;	// 二、简单的引用
    int *a3 = &a1;	//三、a3的地址存放 着 a1的地址
    // 小提示
    // a1 = 3;
    // &a1 = 0x321
    // a3 = 0x321
    // *a3 = 3
    ```
  
- 指针的赋值

  - ①、简单的赋值

  - ```C++
    int a1 = 3;
    int *a2 = &a1;
    a1 = 5; // 正确
    // 这里*a2必须带星号，这样才表示值
    *a2 = 5 // 正确
    ```
    
  - ②、`const`放在左边指针无法改数据，但放在右边可以改数据

    - 但是`const`放在右边无法改变指针`a5`

  - ```C++
    int a1 = 3;
    const int *a4 = &a1;
    a1 = 5;	// 正确
    *a4 = 5; // 报错，*a4编成常量无法更改数据
    
    int *const a5 = &a1;
    a1 = 5;	//正确
    *a5 = 5; //正确
    int y = 6;
    a5 = y	// 报错,a5变成常量无法改指针
    ```

  - ③、只可以更改a1，`const`在int的左边还是右边是没有区别的。

  - ```C++
    int const *const a6 = &a1;
    const int *const a7 = &a1;
    a1 = 5;	// 正确
    *a6 = 6; // 报错
    a6 = y	// 报错
    ```

- 总结：

  - `const`，位于星号的左边，表示**指针(*a5)作为常量**，但a5不是常量
    - `*a5 = 5`，报错
    - `a5 = y`，可以运行
  - `const`，位于星号的右边，表示**a5作为常量**
    - `a5 = y`，报错
    - `*a5 = 5`，可以运行 



****



函数前面加 `inline`，表示内联函数

```C++
inline void f(){
	cout << "hello \n";
}
int main(){
	f();
}
```



- 函数重载
  
  - 在同一个类中，函数名称相同，但参数列表不相同（参数的类型、个数、以及顺序），称为函数重载
  
  - **返回类型**不能作为函数重载的依据
  
  - ```C++
    int add(int x, int y){
    	return x + y;
    }
    double add(int x, double y){
    	return x + y;
    }
    ```



## 面向对象

状态=属性

行为=函数、方法

将现实世界学生抽象成一个类

类是对象的一个抽象，对象是类的实例。

**抽象是面向对象的基础**

面向对象的特点：封装、继承、多态

- 抽象

  - 抽象是对具体对象（问题)进行概括，抽出这一类对象的公共性质并加以描述的过程。

  - 数据抽象：描述某类对象的属性或状态（对象相互区别的物理量）。

    - `int Hour, int Minute`

  - 代码抽象：描述某类对象的共有的行为特征或具有的功能。

    - `SetTime(), showTime()`

  - 抽象的实现：通过类的声明。

    - ```c++
      class Clock{
        public:
        void SetTime(int NewH,int NewM,int NewS);
        void ShowTime();
        private:
        int Hour,Minute,Second;
      };
      ```

- 类的声明形式

  - ```C++
    class 类名
    {
    	public:
      	公有成员(外部接口)
        void walk(){} // 函数成员
      private:
      	私有成员
        string name; // 数据成员
      protected:
      	保护型成员
    };
    ```

- 在类外定义函数成员：`::`

  - **类名`::`方法名**

  - ```C++
    class Student{
      private:
    	  int age;
      public:
    	  void hello(){};
    };
    void Student::hello(){
    	cout << "你好,"<< age << endl;
    }
    ```

- 构造函数

  - 构造函数的作用是在对象被创建时使用特定的值构造对象，或者说将对象初始化为一个特定的状态。

  - ```C++
    class Student{
      private:
    	  int age;
      public:
    	  void hello(){};
      Student() {	// 构造函数
      	cout << "默认调用" << endl;
      }
      Student(int text) {	// 构造函数
        age = text;
      	cout << "我是age:"<< age << endl;
      }
    };
    int main() {
    	Student s;	// 默认调用无参构造函数
      Student s2();	// 默认调用
      Student s3(3);	// 我是age:2
    }
    ```

- 重载

  - 名称相同，参数列表不同

  - ```C++
    class Max{
    	private:
      	int a, b;
     		int Maxi(int, int);
      public:
      	void Set(int, int);
      	int Maxi();
    };
    // 私有方法求最大值，有参数的
    int Max::Maxi(int x, int y){	
    	return x > y ? x : y;
    }
    // 设置值
    void Max::Set(int t1=0, int t2=0){
    	a=t1;
      b=t2;
    }
    // 这里的Maxi是无参数那么就是共有函数
    // 他调用有参数的Maxi(a,b)，就是调用私有函数比较大小
    int Max::Maxi(){
    	return Maxi(a, b);
    }
    int main(){
    	Max m1;
      m1.Set(1, 2);
      //	调用公有的Maxi(),然后Maxi()在调用他内部私有函数Maxi(a,b)
    	cout << m1.Maxi() << endl;
    }
    ```

  - ```C++
    // 数组声明方式
    class Max{
    	private:
      	int a, b;
     		int Maxi(int, int);
      public:
      	void Set(int, int);
      	int Maxi();
    }A[3];	// 声明数组，包含三个对象
    int main(){
      A[0].Set(1, 2);
      A[1].Set(77, 44);
      A[2].Set(22, 3);
    	cout << A[0].Maxi() << endl;
    }
    ```

- **this**，表示当前类

  - ```C++
    this->x = x;
    ```



****



- 实例化对象指针

  - ```C++
    Student *s7;	// 不会调用构默认造函数
    Student *s8 = new Student();	// 调用默认构造函数
    Student *s9 = new Student();
    s9.show();	// 会报错
    S9->show();	// 正确
    ```

- 声明对象引用， 

  - ```C++
    Student s10;
    Student *s11 = &s10;	// 定义指向对象s10的Student类 类型的指针
    Student &s12 = s11;	// 定义Student类 类型对象s10的引用
    // 三者用法都一样
    s10.hello();
    s11->hello();	// 等价于 s10.hello()
    s12.hello();
    ```



****



- 析构函数：`~`

  - **等构造函数调用完，在调用析构函数**
  
  - ```c++
    class myDate {
    public:
      myDate(){
      	cout << "构造函数" << endl;
      }
      ~myDate(){
      	cout << "析构函数" << endl;
      }
    };
    void main(){
    	myDate my;	// 构造函数
      myDate *my2 = new myDate();	// 构造函数 \n 析构函数
      delete my2;	// 析构函数
      // delete []my2;
    }
    ```



****



- 不完全类

  - ```c++
    class Monly{};	// 空类
    class Mon;	// 不完全类的声明
    
    Monly m;	// 可以
    Monly *m1;	// 可以
    Mon m;	// !不可以!创建不完全类的对象
    Mon *m; // 可以创建不完全类的指针
    ```



****



## 继承



- 单继承

  - ```C++
    class <派生类名> : <继承方式> <基类名>{}
    ```

- 多继承

  - ```C++
    class <派生类名> : <继承方式1> <基类名1>, <继承方式2> <基类名2>{}
    ```

- 继承方式：

  - `public`、`protected`、`private`

- 继承方式的解析

  - ```C++
    class Person{
    	public:
      private:
      protected:
    }
    class Student :<继承方式> Person{};
    int main(){}
    ```

  - `public`：除了私有都能访问。

  - `protected`：会自动将基类(Person)中的`public`转变为`protected`，在main中只能访问子类不能访问基类。**换句话说，只能在子类中访问父类的方法和属性。**

  - `private`：将基类(Person)中的`public`和`protected`转变为`private`

- **在子类调用父类方法**

  - ```C++
    class Employee :public Person{
    	public:
      void show(){
      	Person::show(); // 调用父类的show方法
      }
    }
    ```

- 友元函数：`friend`

  - 不是任何类的成员函数，可以直接访问该类的任何成员，包括私有
  - **先声明不完全类**

- 多继承实例

  - ```C++
    class A{
    	public:
      int a;
      A(int x){
      	a = x;
      }
      void showa(){
      	cout << "a=" << a << endl;
      }
    };
    class B{
    	public:
      int b;
      B(int y){
      	b = y;
      }
      void showb(){
      	cout << "b=" << b << endl;
      }
    };
    class C:public A, public B{
      public:
      int c;
      // 这一步：调用父类的构造方法
      C(int x, int y, int z):A(x),B(y){
      	c = z;
      }
    };
    int main(){
    	C c(1,2,3);
      cout << c.a << "," << c.b << "," << c.c << endl;
      c.showa();	// 调用基类的函数
      // 结果：1,2,3
      // 结果：a=1
    }
    ```



## 多态

> 运算符重载分三种
>
> 前缀：`operator +(a,b)` 表示 `a+b`
>
> 中缀：`operator -(a,0)` 表示 `-a`
>
> 后缀：`operator ++(a)` 表示 `a++`

- 运算符重载：`方法名 operator@(参数表)`

  - `@`：符号

  - ```C++
    class MyComplex{
    private:
      int a, b;
    public:
      // 初始化
      MyComplex(int x, int y){
      	a=x;
      	b=y;
      }
      // 运算符重载
      MyComplex operator+(const MyComplex &c);// 成员函数
      friend MyComplex operator-(const MyComplex &c, const MyComplex &c2);// 友员函数
      // 输出
      void show(){
      	cout<< a << "," << b <<endl;
      }
    };
    // 具体重载操作，a和a相加，y和y相加
    MyComplex MyComplex::operator+(const MyComplex &c){
      // 这里的this代表第一个操作数c=1和2
      // 如果是cc=c2+c，那么这里就是c2=3和4
    	return MyComplex(this->a + c.a, this->b + c.b);
    }
    int main(){
    	MyComplex c(1,2), c2(3,4);
      MyComplex cc = c + c2;
      cc.show();// 结果：4,6
    }
    ```

- 成员函数的特点

  - 函数参数：二元运算符只带一个参数（另一个参数隐含为this），一元运算符不带参数。
  - 参数调用：当前对象作为左操作数，函数参数作为右操作数
    - `a.operator + (b)`

- 友元函数的特点：

  - 函数参数：二元运算符带两个参数，一元运算符带一个参数。
  - 函数调用：两个对象都作为函数的参数
    - `operator + (a, b)`

- **虚函数**：`virtual`

  - 指针`pa`不论他指向的是pb对象又或是强制类型转换后指向pb对象，他调用`show()`一直都是调用**基类方法**。总之，编译器看到哪个类的指针，就认为要通过它访问哪个类的成员，编译器不会分析`基类(pa)`指针指向到底是基类对象还是派生类对象。

  - 故，仅仅继承机制不能做到动态多态，需要加上虚函数。当派生类调用同名函数时，会基类中的函数。（虚函数加在基类时）

  - 如果不加虚函数，那么b的输出都是**A-Print**

  - ```C++
    class A{
    	public:
      	void show(){
        	cout<<"A-Print"<<endl;
        }
    };
    class B:public A{
    	public:
      	void show(){
        	cout<<"B-Print"<<endl;
        }
    };
    int main(){
    	A a;
      B b;
      A *pa = &a;
      B *pb = &b;
      pa->show();	// A-Print
      pb->show();	// B-Print
      cout << "-------" << endl;
      // 这里如果没有虚函数，那么就会输出A-Print
      pa = pb;
      pa->show();	// A-Print
      pa = &b;
      pa->show(); // A-Print
    }
    ```

  - ```C++
    class A{
    	public:
      // 虚函数，虚函数不能是静态函数(static)P246
      	virtual void show(){
        	cout<<"A-Print"<<endl;
        }
    };
    ```

- 虚函数与析构函数

  - 析构函数会先调用自己的析构函数，然后在调用父类的析构函数。

- 纯虚函数 

  - 不能进行实例化！但是可以创建指针

  - 就会变成抽象类

  - `vitural void show()=0`

  - 子类继承了父类，如果想要使用父类的纯虚函数，必须进行重写，就可以实例化了。

  - ```C++
    class A{
    	public:
      	virtual void show()=0;// 纯虚函数
    };
    class B::public A{
    	public:
      // 重写父类纯虚函数
      void show(){
      	cout<<"B-show"<<endl;
      }
    };
    int main(){
      // A a; // 会报错
    	// A *a;	// 可以
      B b;
      b.show();
      // 这样做是可以的
      A *a=new BB;
      a->print();
    }
    ```

  - **抽象类至少含有一个虚函数，而且至少有一个虚函数是纯虚函数。**



## I/O

`iostream`：所有输入输出流的基本信息

`iomainip`：带参数流操作符

`fstream`：处理文件相关



`in`：文件输入，从文件中读取

`out`：文件输出，向文件中写入



- 写入文件：`freopen`

  - 简单的将`x=`输入到文本里面

  - ```C++
    #include <iostream>
    #include <string>
    using namespace std;
    
    int main(){
    	int x;
    	cin >> x ;
    	freopen("text.txt","w",stdout);
    	cout << "x=" << x <<endl;
    }
    ```

- 读取文件

  - ```C++
    int main(){
    	int x;
    	freopen("text.txt","r",stdin);
    	for(int count = 0; count<3; count++){
    		cin>>x;
    		cout << "文本的值为:" << x <<endl;	
    	}	
    }
    ```

- 打开文件：`open`

- 关闭文件：`close`

  - in：读取；out：覆盖；app：附加；

  - ```C++
    #include <iostream>
    #include <string>
    #include <fstream>>	// 处理文件 
    using namespace std;
    
    int main(){
    	ifstream inFile;	// 写入文件流
    	
    	ofstream outFile("2.txt", ios::out);	// 读取
    	inFile.open("1.txt",ios::in);	// 写入
    	
    	if(inFile){
    		cout<<"OK"<<endl;
    		// 获取内容,一行一行的读取 
    		string str;
    		getline(inFile,str);
    		cout<<str<<endl;
    		// 将1文件写入到2文件中
    		outFile << str <<endl;
    		// 关闭文件 
    		inFile.close();
    	}
    }
    ```



**总结**

`ifstream inFile("1.txt", ios::in)`和`inFile.open("1.txt",ios::in)`是一样的。

第一步：导入头文件`#include <fstream>>`

第二步：读/写文件流

可以这么理解，in是**文件输入流类，读取文件**。文件写入/输出流是相对于C++来说。C++的**输入流**就是文件的输出那么就是**读取文件**。

`ifstream`：读取文件

`ofstream`：写入文件

第三步：读取文件

**将文件写入到str中**

`string str`

`getline(inFile, str)`：从当前字符开始读取，直到最后

`ch = inFile.get()`：读取一个字符

第四步：写入文件，

`outFile<<str<<endl`

最后：关闭文件`inFile.close()`

```c++
#include <iostream>
#include <string>
#include <fstream>>	// 处理文件 
using namespace std;

int main(){
	ifstream inFile;	// 读取文件流
	
	ofstream outFile("2.txt", ios::out);	// 写入
	inFile.open("1.txt",ios::in);	// 读取
	
	if(inFile){
		cout<<"OK"<<endl;
		// 获取内容,一行一行的读取 
		string str;
		getline(inFile,str);
		cout<<str<<endl;
		// 将1文件写入到2文件中
		outFile << str <<endl;
		// 关闭文件 
		inFile.close();
	}
}
```



`eof`：判断输入流是否结束



## 模板

- 模板是一个将数据类型参数化的工具，把**一般性的算法**和**对数据类型的实现**区分开

- 模板分为：**函数模板**和**类模板**

- 函数模板：`template<模板参数>
  返回类型 函数模板名(参数表){}`

  - T是什么类型不重要，数据是什么类型T就是什么类型，`typename T`：是占位符

  - ```C++
    template<typename T>
    T abs(T x){
    	return x<0 ? -x:x;
    }
    int main(){
    	cout << abs(-5) << endl;
    }
    ```

- 关于参数表，以下几种方式都可以

  - ```c++
    T abs(T x)
    T abs(const T& x)
    int abs(T &x)
    void abs(T &x)
    ```

- 类模板：`template<模板参数>; class 类模块名{类体定义};`

  - 按照字母排顺序，T在J的后面

  - ```C++
    // 创建模板
    template<class T1, class T2>
    class Pair{
    	public:
      	T1 first;	// 对应string
      	T2 second;	// 对应Int
      	Pair(T1 k, T2 v):first(k), second(v){} // 重载
    	  // 小于号，运算符重载
      	bool operator<(const Pair<T1, T2> &p) const;
    };
    template<class T1, class T2>
    bool Pair<T1, T2>::operator<(const Pair<T1, T2> &p) const{
    	return first<p.first;
    };
    int main(){
    	Pair<string, int> student1("Tom", 19);
     	Pair<string, int> student2("Jim", 25);
      bool a = student1<student2;
      if(a == 0){
    	  cout << student1.first << "位于" << student2.first<<"之前" <<endl;
      }
      else{
      	cout << student1.first << "位于" << student2.first<<"之后" <<endl;
      }
    }
    ```



****



- 附：
  - `aa=4,bb=5；a = aa++, b = a * ++bb;`
    - a=4,b=24
  - 加号在后面表示**先赋值**在做运算
  - 加号在前面表示**先运算**在赋值





## 真题

> 选择题重点归纳

提供默认值是**从右到左**的顺序提供。

主函数的实参和被调函数的形参是按**从左到右**的顺序匹配。

**引用**：给变量起别名。

函数调用时参数的两种传递方式：**传值和传引用**。

内联函数：`inline`

c++是**结构化程序设计方法**又称**面向过程设计方法**

结构化设计采用**自顶向下、逐步求精和模块化**的思想。

c++程序的结构：类的定义、类中成员函数的实现、主函数main

标识符的**作用域**是指标识符在程序中的有效范围，**可见性**是指程序在哪个区域里可以使用。

在声明类的构造函数时可以同时给出函数体，该构造函数称为：**内联函数**。

当不定义构造函数时，系统会自动添加构造函数，称为：**默认构造函数**。

`static`说明自动变量，根据定义位置不同分为：**静态全局变量和静态局部变量**。

静态变量存储在**全局数据区**。

类的静态成员包括：**静态成员变量和静态成员函数**。



不能把其他类的**私有成员函数**声明为友元函数。友元函数不受类中的**访问权限关键字**的限制。

友元函数的关系是**单向**的。

表达式由**运算符和操作数**构成。

重载：`operator`。

不能重载的运算符：`.`、`.*`、`->*`、`::`、`sizeof`、`?:`、`#`。

类编写新的类的方式：**继承和组合**。



文件IO：`ifstream`、`ofstream`、`fstream`



**输入输出流**

`istream`：输入操作

`ostream`：输出操作

`istream`、`ostream`和共同派生出`iostream`



**其他**

`delete[] ss;`：释放动态对象数组



****



> 填空题

1. 面向对象的程序设计方法，最重要是使程序的**复用性**大大提升。
2. 函数调用时参数的传递为“传引用”，是传递对象的**地址**。
3. 从逻辑关系上看，C++程序结构包括**类的定义**、**类中成员函数的实现**及**主函数/main**。
4. 程序创建一个对象时，系统自动调用**构造函数**初始化该对象。
5. 声明虚函数成员：“**virtual 函数返回值类型 函数名（形参表）**”。
6. 将s=C++，输出为“@@@C++”这样的格式，输出语句是：“count << **setfill("@")**<<setw(6)<<s;”。



1. C++支持两种多态分别是**编译时**的多态性和**运行时**的多态性。
2. 不需要函数返回任何值时，函数类型定位是**void**。
3. 指针使用成员有两种方法“->”**指向运算符**和“.”**成员访问运算符**。
4. 使用类的一个对象初始化该类的另一个对象时，可以调用**复制或拷贝**构造函数完成此功能。
5. 一个类拥有多个构造函数，他们的关系是**重载**。
6. 在面向对象的程序设计中，将一组对象的共同特性抽象出来形成**类**。
7. 对赋值运算符进行重载时，应声明为**类成员**函数。
8. String类的**Find**方法返回查找到的字符串在主串的位置。
9. 取子字符串“substr(5, 3)”，第一个参数意思是**在字符串中在第5个位置截取子串**。
10. 复制构造函数的参数，是**引用类自己**的对象。
11. 类模板用来表示具有**相同处理方法**的模板类对象集。
12. this指针指向**调用函数的对象**。
13. 若数组名作为函数调用的实参传入，则实际上传递给实参的是**数组首地址**。
14. 内联函数在编译时是将函数的**函数体**替换其调用表达式。
15. C++可以建立一个通用函数，其函数类型和形参类型不具体指定，用一个虚拟的类型代表。这个通用函数称为**函数模板**。



1. **float(39)/4=9.75**
2. 不允许使用逻辑非操作符，则关系表达式x+y>5的相反表达式是**x+y<=5**。
3. 双目运算符作为类的成员函数重载时有**1**个参数。
4. 一个派生类只有一个唯一的基类，这样的继承关系为**单继承**。
5. 动态分配一个类型为Worker的具有n个元素的数组，由r指向该动态数组，则表达式应为：`Worker *r = new Worker[n];`。
6. 对象是类的**实例**。
7. 面向对象将属性特征的数据和对数据进行操作的**方法**封装在一起。
8. 对象成员是指对象所属类中定义的成员，包括**数据成员**和**引用类自己**。
9. 构造函数的功能是在**创建对象**时初始化对象。
10. `(*fp).score`等价于`fp->score`。
11. 类AB有一个静态数据成员bb，不通过对象名访问该成员：`AB::bb`。
12. OOA中使用**对象**映射问题域中的事务。
13. 定义重载函数应该在**参数类型**或**参数个数**上有所不同。
14. **友元函数**不属于成员函数。





## 大题



> 202010

39：数值类型只输出前面一部分：`setprecision(num)`

41：y是全局变量，value()参数的`&z`他是地址。因为将`x`作为参数传入并且`return z`返回的是`x`的地址，所以得出`value(x)=10`=`x=10`。

44、

1：`Point A(1,2)`对象1构造，合理

2：`Point B(A)`对象2构造，合理。因参数是地址故调用下面的`Point::Point(Point& p)`。因为`Point A`父类原本的X=1，所以X自加1变成2。

3：`Point C(A)`对象2构造，合理。

4-6：因为**构造调用完毕**，开始调用析构，可以理解成洋葱模型，**从内到外**。故输出对象2、2、1被析构。



最后一题：

`strcpy(a, b);`：字符串复制，b复制到a。b指向的字符串复制到a指向的空间。

关键点1，子类继承父类，子类的构造方法后面必须也继承于父类（`Student():School()`）

关键点2，子类继承父类时，`参数列表前面必须相同`，如（`Student(int n, char *s):School(n,s)`）

```c++
class School{
  public:
  	School(int n, char *s){
      Number = n;
      strcpy(name, s);
    }
  protected:
  	int Number;
  	char name[8];
}
class Student: public School{
  public:
  	Student(int n, char *s, char *s1, double t):School(n,s){
      strcpy(Class_Num, s1);
      Total = t
    }
  	void Display(){
      // 输出即可
    }
  private:
  	char Class_Num[10];
  	double Total;
}
```





> 201910

51，这题很经典，结果是

a2b3

END:8

END:0

换行

要注意！！换行这必须要写出来。

**要点**：`A x;`这样也是代表该类A已经在运行了，然后后面跟上了`, y(2,3)`，前面`x`的析构函数需要等y执行才会运行。

**END:0代表的是x的析构函数**

`A(int aa, int bb) : a(aa), b(bb)`：这里是代表初始化列表，等价于`a=aa`。

```c++
#include <iostream>
using namespace std;
class A
{
  int a, b, c;

public:
  A() { a = b = c = 0; }
  A(int aa, int bb) : a(aa), b(bb)
  {
    cout << "a" << a << "b" << b << endl;
  }
  ~A()
  {
    cout << "END:" << c << endl;
    c++;
  }
};
int main()
{
  A x, y(2, 3);
  return 0;
}
```















