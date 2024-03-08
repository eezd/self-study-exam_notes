# JAVA

> abstract 抽象
>
> interface 定义接口
>
> implements 使用接口
>
> Graphics 图像
>
> `getContentPane`
>
> `e.getSource()` 获取事件对象
>
> `actionPerformed`

```java
class frist{
  public static void main(String[] args){}
}
```



**输入输出**

第一步：创建输入对象`Scanner scanner = new Scanner(System.in);`

第二步：读取输入内容`String message = scanner.nextLine();`

`nextInt()`、`nextDoble()`

```java
public static void main(String[] args) {
  Scanner scanner = new Scanner(System.in);
  System.out.println("enter a line of text to test");
  String message = scanner.nextLine();	// 从键盘中读入一行
  System.out.println(message);
}
```





访问控制权限：

private：私有，修饰类的属性和方法，该成员只能在本类中方法

default：可以被本包其他类访问，但不能别其他包访问

protected：只能被本包及不同包的子类访问

public：所有类都可以访问



局部成员没有访问权限控制

`bb`：之所以错误，因为作用域只在那对花括号中。

```java
public class Test {
  public int aa;	// 正确
  {
  	public int bb;	// 错误,局部成员没有访问权限控制
  }
}
```



封装是一种将抽象性函数式接口的实现细节部分包装、隐藏起来的方法。封装可以被认为是一个保护屏障，防止本类的代码和数据被外部类定义的代码随机访问。



像访问私有属性必须通过 `setter` 和 `getter` 方法设置和获取属性值

```java
class Student{
	private String name;
  public String getName(){
  	return name;
  }
  public void setName(String name){
  	this.name = name;
  }
}
```



> **调用属性可以不用 this**
>
> 可以使用this调用本类属性
>
> this关键字调用成员方法
>
> this调用本类构造函数

构造方法

名称与类名一致。名称前不能有任何返回值类型的声明。不能使用`return`返回一个值。

```java
class Student{
	public Student(){
  }
}
```

构造方法重载

方法名是相同，但参数或参数个数不同。

```java
class Student{
  private String name;
  private int age;
	public Student(){}
	public Student(String n){
  	this.name = n;
  }
	public Student(String n, int a){
  	this.name = n;
    this.age = a;
  }
}
```



> 静态变量或静态方法，均可以用类名调用，不必使用对象实例名。



**数组**

`类型 数组名[] = new 类型[数组大小]`

`类型[] 数组名 = new 类型[数组大小]`

`类型 数组名[] = {值1 ,值2 , ...}`

多维数组

`类型 数组名[][]`

`类型[][] 数组名`

`类型[] 数组名[]`



`类型 数组名[][] = new 类型[一维大小][二维大小]`

`类型 数组名[0] = new 类型[二维大小]`

> 数组错误声明：
>
> `int arr[2][3]`：禁止声明静态数组
>
> `int arr[][] = new int[][4]`：声明顺序应从高维到低维
>
> `int arr[][4] = new int[3][4]`：维数指定只能出现在new运算符之后



**String**

`length()`：字符串长度

`charAt(index)`：字符串index位置的字符

`subString(beginIndex)`：截取从开始位置到结尾的字符



String类

`replace(char oldChar, char newChar)`：将旧的替换成新的

`toLowerCase()`：小写

`toUpperCase()`：大写

`concat(String str)`：str连接至尾部

`startsWith(char prefix)`：prefix是否是字符串前缀

`trim()`：去除前后空白



StringBuffer

`append(String end)`：将str添加到尾部

`replace(int start,int end,String str)`：替换start到end直接的字符为str



**继承**

`is a`：例如从雇员 Employee 派生出经理 Manager ，Manager 具备 Employee 的一般特性，同时 Manager 也具有 Employee 不具备的额外特性。他们的关系就是 `is a`。这就是继承`extends`

格式：**`class 子类 extends 父类`**

只能单继承。不允许多重继承，但是可以多层继承。

继承的时候，子类不能访问父类私有成员。

```java
class A{}
class B extends A{}
class C extends B{}
```



子类重写父类方法的时候，如果父类的方法是public的话，子类的方法就不能是private。

子类可以通过：`super` 调用父类的成员

```java
class Animal{
	String name = "狗";
  void shout(){
  	System.out.println("动物发出叫声")
  }
}
class Dog extends Animal{
	public shout(){
  	super.shout();
    System.out.println("汪汪汪...");
  }
  public void printName(){
  	System.out.println("名字：" + super.name);
  }
}
Dog = dog = new Dog();
dog.shout();
dog.printName();
// 动物发出叫声
// 汪汪汪...
// 名字：狗
```



访问父类构造方法：`super(参数1, 参数2)`

` super()`调用父类构造方法必须位于第一行且只能出现一次 



 `final`：终极变量或终态变量、可用于声明类、属性、方法。需要注意：

修饰的类不能有子类。修饰的方法不能被子类重写。修饰的变量是常量，不能被修改。



声明全局变量：`public static final String NAME = "哈士奇"`

**全局变量必须是大写**



**抽象类**

抽象方法在定义时不需要实现方法体

`abstract void 方法名称(参数)`

包含一个以上的抽象方法的类必须是抽象类

抽象方法只需声明无需实现

**如果一个类继承了抽象类，那么子类必须实现抽象类中的所有抽象方法。**

抽象方法不能使用`private`修饰

```java
abstract class 抽象类名{
	访问权限 abstract 返回值类型 抽象方法名(参数);
  // 无方法体
}

abstract class Animal{
	abstract void shout();
}
class Dog extends Animal{
	// 实现抽象方法
  void shout(){
  	System.out.println("实现抽象方法");
  }
}
```



**接口**

接口是由**全局变量**和**公共的抽象方法**组成，不能包含普通方法。

JDK8以后接口还可以由默认方法和静态方法。（默认->default，静态->static）。这两种都可以拥有方法体。

关键字：`interface`

如果不写`public static final`，接口也会默认添加。

在`implements`的后面声明多个接口，一个类实现多个接口。

```java
public interface 接口名 extends 接口1, 接口2{
	public static final 数据类型 常量名 = 值;
  public default 返回值类型 抽象方法名(参数);
  public abstract 返回值类型 方法名(参数){
  	// 默认方法的方法体
  }
  public abstract 返回值类型方法名(参数){
  	// 类方法的方法体
  }
}
```

```java
interface Animal {
	int ID = 1;	// 全局变量
  String NAME = "哈士奇";
  void shout();	//抽象方法
  static int getID(){	
  	return Animal.ID;
  }
  public void info();	// 静态方法
}
```



**多态**

```java
abstract class Animal{
	abstract void shout();
}
class Dog extends Animal{
  void shout(){
  	System.out.println("Dog实现抽象方法");
  }
}
class Cat extends Animal{
  void shout(){
  	System.out.println("Cat实现抽象方法");
  }
}
```



判断某个对象是否是某个类：`对象 instanceof 类`



**Object**

Object 是所有类的父类，称为**超类**。定义类的时候如果没有通过`extends`指定父类，则默认继承Object类。

常用方法：

两个对象是否相等：`equals()`

返回对象哈希码值：`hashCode()`

返回对象字符串表现形式：`toString()`



**异常**

Throwable是所有异常的子类，他又两个直接的子类就是：Error、Exception

常用方法：

返回异常消息字符串：`getMessage()`

返回异常的简单信息描述：`toString()`

获取异常类名和异常信息，以及异常出现在程序中的位置，将信息输出在控制台：`printStackTrace()`

就算`return;`中止了，但是finally语句还会继续执行，如果想真正中止则：`System.exit(0)`退出当前JAVA虚拟机

```java
try{

}catch(ExptionType(Exception类及子类)e){
	// 对异常处理
}
try{
	// 代码
}catch(ExptionType e){
	System.out.println("异常" + e.getMessage());
  return;
}finally{
	System.out.println("Finally");
}
```



`throws`：抛出异常

```java
public static int res(int x, int y) throws Exception{

}
```



**输入输出流**

导入包：`import java.io.*;`

文件数据流包括：`FileInputStream` 和 `FileOutputStream`

in：读取文件、out：写入文件

对象流：`ObjectInputStream` 和 `ObjectOutputStream`

**流程：创建文件流，然后使用对象流读取文件流**

读写：`readObject()` 和 `writeObject(d)`





**图形界面设计**

设计图形用户界面分三步：**选取组件、设计布局、响应事件**

组件分为：**容器组件**和**非容器组件**



**普通面板（JPanel）**和**滚动面板（JScollPane）**是用途广泛的容器，**面板**不能独立存在，需被添加进其他容器内部。



**四个顶级容器：`JFrame、JApplet、JDialog、JWindow`**



`getContentPane()`：返回框架窗体的**内容窗格对象**

`setVisible(boolean aFlag)`：调整可见和不可见

`pack()`：调整框架大小

```java
// 创建一个Swing,标题是JFrameDemo
JFrame frame = new JFrame("JFrameDemo");
// 创建Button实例，按钮文本为 Press me
JButton button = new JButton("Press me");
// 将按钮放在JFrame中间
frame.getContentPane().add(button, BorderLayout.CENTER);

// 第二种写法
Container con = frame.getContentPane();
Container con = getContentPane();
con.add(buttion);
```



`JTextField`：文本

`JToggleButton`：切换按钮

`JCheckBox`：复选按钮

`JRadioButton`：单选

可通过`isSelected()`获取按钮状态



**事件处理**

按钮点击事件：点击按钮将发送`ActionEvent`事件对象，需要使用`addActionListener()`为按钮注册事件监听程序并实现`ActionListener`接口

1、导入包：`import java.awt.event;`

2、注册监听对象`事件源.addXXXListener(XXXListener)`

`addActionListener(ActionListener)`

3、实现`public void actionPerformed(ActionEvent e){}`

要注意的是`ActionEvent e`

**鼠标事件**

`mouseDragged(MouseEvent e)`：鼠标拖动时

`mouseMoved(MouseEvent e)`：鼠标移动时

`e.getX()、e.getY()`：X坐标和Y坐标



**绘图**

第一步：创建面板`getContentPane().add(new MyPanel())`

第二步：创建Graphics，`public void paintComponent(Graphics g){}`

第三步：画画`g.drawRect(100 ,50 ,100 ,46)`



drawArc画弧线、

drawLine(x1,y1,x2,y2)直线，x1y1对应一点，x2y2对应一点

drawOval椭圆

drawPolygon折线

drawRect(x,y, width, height)矩形，xy对应左上角的点，长和宽







**线程**

通过类`Thread`实现，一共有4种状态新建（NEW）、可运行状态（RUNNABLE）、死亡（DEAD）、阻塞（BLOCKED）

通过`interrupt()`终止线程

创建线程`Thread(ThreadGroup group, Runable target, String name)`

线程启动时调用`target`的`run()`方法

在派生子类中实现run方法

```java
class NewThread extends Thread{
  public void run(){
    for(int i = 0; i<=5; i++){
      System.out.println(i);
      try{
        sleep(500);
      }catch(InterruptedException e){}
    }
  }
}
```



`public class xyz implements Runnable{}`

Runnable是实现线程的接口，而Thread类实际上就是实现Runnable接口，所以Thread才具有线程功能。



**线程的控制**

start、run、yield终止、isAlive查看是否在运行、sleep(int millsecond)休眠一段时间、wait

wait等待后直到调用该线程的notify或notifyAll方法从能唤醒。

## 真题





> 选择

构建文本域：不可以构建**指定行数**的文本域。

算术右移n位：如果是奇数则 **减1除(2*n)**，偶数 **除(2*n)**。如（85>>1=(85-1)/2=42）

算术左移：直接 **乘(2*n)**



> 填空题

is a：继承

has a：包含

1. char类型的值用**16**位无符号整数表示。
2. 抛出异常：`throws`。
3. 每一个类至少有一个**构造方法**。
4. `subString(num)`：截取Num开始至尾部的字符。
5. 子类和父类是一种**is a**的关系。
6. Reader和Writer类用于**字符**流处理的类。
7. 在Graphics2D类中，绘制线段的类是**Line2D**。
8. 菜单栏构建的方法名字是**JMenuBar**。
9. 通过继承**Thread**类创建线程。



1. double初始值是：**0.0**
2. 数组复制的方法：`arraycopy`
3. 创建 **File** 类的对象后可使用其中方法获取文件信息。
4. 每个事件类型有一个 **监听程序接口** ，规定了接收并处理该类事件方法的规范。
5. 标准对话框的类是 **JOptionPane** 。
6. 释放所有等待线程的方法：**notifyAll**



1. 字符串转小写：`toLowerCase`
2. 字符串转大写：`toUpperCase`
3. A的某个成员变量类型是类B，则他们的关系是 **has a**
4. 在BufferedReader类中，实现按行输入的方法是 **readLine**
5. KeyListener 接口的作用是 **处理键盘事件**
6. Swing组件定义在 **javax.swing**
7. wait()方法的作用让当前线程释放 **对象互斥锁**







> 简答题

1. a算术右移3位后大于2或者b是奇数：`a>>3>2||b%2==1`

2. 

`int a[2][4];`：不正确，不允许声明静态数组

`int[][] b = new int[][4];`：不正确，维数声明顺序应从高维到低维。

3. final类的特点：不能被继承。final方法的特点：方法不能被覆盖。

4. 线程控制方法中的功能

start()：用于启动线程对象。

yield()：强制终止线程的执行。



1. 访问权限

public：可以被其他**任何对象访问**

private：只能在**本类中访问**

protected：只能被**同一包及其子类**的实例对象访问

default：可以被**所在包的各类访问**

2. Swing中4个顶层容器

**JFrame、JApplet、JDialog、Jwindow**

3. 线程的组成和调度方法：**虚拟CPU、执行代码、处理数据**。采用**抢占式调度方法**



1. 检测错误

`a = method1(f);`：错误，没有实例化

`static float method1`：错误

2. 请写出为文本文件abc.txt创建BufferedReader对象in的代码。

**关键点：通过`FileReader`读取文件。****

```java
BufferedReader in = new BufferedReader(new FileReader("abc.txt"));
```

3. 请写出创建Font类型对象fn的代码，fn的属性值是Courier字体，BOLD样式，20磅字号。

关键点：设置字体样式需要`Font.BOLD`

`Font fn = new Font("Courier", Font.BOLD, 20)`



## 大题

约数（因子）：A可以整除B

最大公约数：A和B，可以被C整除，18和30的最大公约数是6



201910-27，统计整数出现次数，`arrCount[arr[i]-1]++`之所以要-1，是因为arr实际存储数据的范围是0到999，而整数范围是1到1000，如果出现1000则需要-1，放在999的位置。



**操作文件**

`FileOutputStream f = new FileOutputStream("data.dat")`

`ObjectOutputStream s = new ObjectOutputStream(f)`

题目可能会给你前面，你补后面。

写入：`s.writeObject(d)`，d是你要写入的数据，题目会给你的。

写入完需要关闭：`s.close()`

如果题目使用try捕获，可补充：`catch(IOException e)`

打印捕获信息：`e.printStackTrace()`



**线程**

如果题目是定义了一个线程类，则需要`class MyThrd implements Runnable{}`

记住`Runnable`

线程类的方法名字是固定：`run`

显示当前线程的名称：`Thread.currentThread().getName()`

记住`getName()`，获取当前线程名称。



**框架**

题目问你除了框架外还有什么组件?各几个？则按照下面关键字找

JButton按钮、JRadioButtion单选框

`String[] buttionTxt = {...}`：代表每个按钮的name，有几个名称就有几个按钮



201910-28，addActionListener(**new mMonitor**)，这里之所以填`new mMonitor`是因为我自定义事件，而下面则是`class mMonitor implements ActionListener{}`，这里必须使用接口`ActionListener`



201904-27，MyPanel类在面板上放置一个列表，点击列表的选项，将值保存在seleItem

`class MyPanel extends JPanel implements ???`，???的答案需要看下面的例子，找到`addListSelectionListener`，结果???就是`ListSelectionListener`

`public void valueChanged(??? e)`，根据 **E** 可判断出是事件，则填`ListSelectionEvent`

`seleItem = list.???.toString();`，根据前面seleItem得出这里填**选项的值**，`getSelectedValue()`



**程序设计**

1. 将arr行列互换，结果保存在arr2中

第一步：arr2的行就是**arr[0]的个数**，而列呢就是**长度**

```java
// 第一步，创建arr2数组
int[][] arr2 = new int[arr[0].length][arr.length];
// 第二步，创建2个for循环遍历就是了
```



**程序设计->框架题**

1. 点击按钮，将a和b的文本域中的字符串放在c中，如果结果是空则c文本域显示NULL

获取a和b的字符串：`a = test1.getText();b = test2.getText()`

拼接起来：`c=a+b`

如果c是空则显示NULL：

```java
if(c.length()!=0){
  text3.setText(c);
}else{
  text3.setText("NULL");
}
```

总结：该题要点是获取字符串``getText`和设置字符串`setText`



2. 菜单窗口，File下拉菜单，有Opton...和Exit 2个菜单，而Exit菜单有快捷键

总结：分三步走，给frame添加菜单窗口`setJMenuBar()`，给菜单窗口添加信息`barMain.add()`

```java
// 题目有已经帮你定义好了，barMain、menuFile、itemOpen、itemExit
// 第一步，设置菜单窗口
barMain = new JMenuBar();
frame.setJMenuBar(barMain);

// 第二步，添加下拉菜单
menuFile = new JMenu("File");
barMain.add(menuFile);

// 第三步，给下拉菜单添加菜单
itemOpen = new JMenuItem("Open...");
itemExit = new JMenuItem("Exit", KeyEvent.VK_X);
menuFile.add(itemOpen);
menuFile.add(itemExit);
```



3. 实现按钮的点击事件，Copy按钮将tfs内容复制到tft，Clear功能是清空

关键点：如何知道点击的是哪个按钮？通过 `e.getSource()` 获取事件对象

```java
if(e.getSource() == bCopy)
  tft.setText(tfs.getText());
else
  tft.setText("");
  tfs.setText("");
```

