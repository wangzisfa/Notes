# c++入门初级

## 复合类型

### 数组

​		c++数组略有不同于c语言数组，其被定义为复合类型，通过声明类型进行创建

如 `float loans[20]`  该数组loans类型不是数组，**而是float类型数组**。强调了其

是使用float类型创建的。

------

- #### 注意：

  - 如果将`sizeof`运算符用于数组名，得到的是整个数组中的字节数。但如果将 `sizeof` 用于数组元素，得到的则是元素的长度。<!--这更表明了loans是一个数组，而loans[1]只是一个int变量-->

  - c++中如果将数组部分元素初始化，**则剩下的其余元素都为0**

  - **让编译器去做**

    - 如何计算元素个数

    - ```c++
      short things[] = {1, 5, 3, 8};
      int num_elements = sizeof things / sizeof (short)
      ```

  - 数组初始化

    - `unsigned int counts[10] = {};` 
    - `float balances [100] {};`

  - **列表初始化禁止缩窄转换**

    ```c++
    long pilfs[] = {25, 92, 3.0};// not allowed
    char slifs[4] {'h', 'i', 1122011, '0'};// not allowed
    char titles[4] {'h', 'i', 112, '\0'};// allowed
    ```



### 字符串

c++中字符串的定义，只需在字符数组的最后一位加 `'\0'` 即可从字符转换为字符串



- 注意
  - 定义数组时一定要确保数组足够大，以存储字符串中的所有字符——包括 `'\0'` 
  - 字符串截断
    - 在需要停止的位置键入 `'\0' ` 以截断该字符串



#### `cout`

`cout` 是类似于 `printf` 的控制输出函数

#### `cin` 

`cin` 是类似于 `scanf` 的控制输入函数，它会在输入空格和回车时停止向缓冲流中读入数值

#### `getline()` 面向行的输入 

`getline` 每次读取一行输入内容，当读取到 `'\r'` 时停止向缓冲流中读入数值，并丢弃换行符 `'\n' ` 

```c++
char charr[20];
cin.getline(charr,20);//表示将这行的输入全部读取至charr中，这样表示可以用来避免超越数组的边界
					  //句点表示法，getline是istream类的一个类方法，(cin是一个istream对象) 
string str;
getline(cin,str);//没有使用句点表示法，表明这个getline不是类方法，
 				 //它将cin作为参数，指出到哪里去查找输入
				 //同时也没有指出输入字符串长度的参数，
				 //因为string类对象会根据给出字符串的长度自动调整大小
```



#### `get()` 面向行的输入

与 `getline` 十分类似，但不会在结尾处丢弃换行符，而是将换行符保留在输入队列中。**使用需要刷新输入流**

`cin.get(键入的数组名,数据大小)`   



### string类简介       友元函数(later)

c++ 98支持直接用于存储字符串的变量

通过`std::string` 引用

- 初始化方式

  与数组类似

- 赋值，拼接，附加

  - 赋值

    string与string之间可以直接相互赋值，**有别于数组** 

  - 直接、简洁的拼接方式

    `str1 = str2 + str3;` 

- `cstring` 头文件中

  可以使用 `strcmp` `strcat` `strcpy` 等操作

- 其他形式的字符串字面值

  1. c++11中，支持Unicode中的utf-8字符编码方案

  2. 原始(raw)字符串。

     在原始字符串中，**字符表示的就是自己**。如表示换行符的 `\n` 表示的就单单是两个字符。方便的是可以直接打出“。

     具体操作过程：

     ```c++
     #include<iostream>
     using namespace std;
     int main(void) {
         cout << R"(Jim "King" Tutt uses "\n" instead of endl.)" << '\n';//相当于如下
         cout << "Jim \"King\" Tutt uses \" \\n\" instead of endl." << '\n'
     }
     ```



### 结构简介

- 注意：
  - c++中结构体省略struct不会出错



- 结构数组

  创建一个元素为结构的数组 `struct_shuzu gifts[100];` 



### 指针

- c与c++区别 注意：
  - oop强调在运行阶段运行决策 
  - **编译阶段决策和运行阶段决策**区别 :
    - 编译阶段是指编译器将程序组合起来时
    - 运行阶段是指程序运行时
  - 运行阶段的决策提供了灵活性，可以根据当时的情况进行调整，减少内存的浪费



### 使用`new`来分配内存 && 使用 `delete` 释放内存

​	**new**和**delete**的使用方法类似与c语言中的**malloc**与**free**两者之间的调用关系



#### 传统的变量地址指针与new对比：

```c++
int hhh;
int *ptr = &hhh;//传统
```

 `int *pn = new int;//new`  

#### 使用new来定义动态数组

```c++
int n;
cin >> n;
int *ptr = new int [n];
for (int i = 0; i < n; i++) 
    cin >> ptr[i];
for (int u = 0; u < n; u++) 
    cout << ptr[u] << endl;
free [] ptr;
```



-  注意：

  - 在使用指针进行**读值**时，**不要轻易直接使用指针**进行递增或者递减操作。否则在delete指针的时候会导致指针指向的并不是数组的首位，无法释放内存空间。（需要进行指针复位操作

  - 在c++中同样可以使用变长数组（vla），即操作如下：

    ```c++
    int n;
    	cin >> n;
    	int array[n];
    	int i = 0;
    	for (;i < n; i++)
    		cout << array[i] << endl;
    ```

    这样操作比较方便，但是由于处于栈内存中，比较小。



## 函数

### 内联函数

<u>*为什么需要引入内联函数？*</u>

在函数的运行阶段，每当函数在被调用时，系统会首先将该函数的形参变量、返回值等进行**载入内存操作**，如果一个函数很小却在整个程序中执行很多次，那么可想而知，这部分所占用的内存空间将相当之大。**为了避免这种内存浪费**，而引入了内联函数。

<u>*如何来写一个内联函数呢？*</u>

```c++
inline int Max(int a, int b) {
    if (a > b) return a;
    return b;
}
```

*<u>编译器又是如何实现的呢？</u>*

```c++
//如果需要执行一个语句
k = Max(n1, n2);
//编译器则会认为
if (n1 > n2) 
    tmp = n1;
else tmp = n2;
k = tmp;
```



### 函数的缺省参数

c++中，定义函数的时候可以让**最右边的连续若干个参数**有缺省值，那么调用函数的时候，若相应位置不写参数，参数就是缺省值

```c++
void func(int x1, int x2 = 2, int x3 = 3) {}
func(10);//可以
func(10, 8);//可以
func(10, , 8);//不行.
```

优点：

1. 提高了函数的可扩展性
2. 避免了多次调用函数后，不断修改参数的麻烦

### 函数重载

`cin.get()` 是一种类似于c语言中的gets() 或 getch() 又或是 getchar() 的变体。总的来说，`cin.get() ` 介绍了c++中的函数常用模式，**函数重载**。

<u>*什么是**函数重载**呢？*</u>

一个或多个函数，名字相同，然而参数个数或参数类型不同，这就叫做函数的重载。

```c++
int Max(double f1, double f2) {}
int Max(int n1, int n2) {}
int Max(int n1, int n2, int n3) {}
```

重载后的函数，在调用时会根据**重载函数的参数**来决定使用的到底是哪个函数。

Q:什么是二义性？



### 和并调用

```c++
char str[100];
	cin.get(str,100).get();
	cout << str << endl;
```



## 类和对象的基本概念

### 结构化程序设计（面向过程的程序设计

​				程序 = 数据结构 + 算法

结构化程序设计的不足：

1. 结构化程序设计中，函数和其所操作的数据结构，没有直观的联系。
2. 随着程序规模的增加，程序逐渐难以理解，很难一下子看出来
   - 某个数据结构到底有哪个函数可以对它进行操作？
   - 某个函数到底是用来操作哪些数据结构的？
   - 任何两个函数之间存在怎样的调用关系？
3. 没有封装和隐藏的概念，不利于函数的维护和扩充
4. 难以查错
5. 重复利用率低
6. 函数与变量之间的关系复杂

## 面向对象的程序设计

面向对象的程序设计 = 类 + 类 + 类 + 类....

程序设计的过程就是设计类的过程

从客观事物中抽象出类：                                                                                                                                                                                          		设计一个”矩形类“

```c++
#include<iostream>
using namespace std;

class CRectangle{
    public:
    int w, h;
    int Area() {
        return w * h;
    }
    int Perimeter() {
        return 2 * (w + h);
    }
    void Init(int w_, int h_) {
        w = w_;
        h = h_;
    }
};//分号

int main(void) {
    int w, h;
    CRectangle r;
    cin >> w >> h;
    r.Init(w, h);
    cout << r.Area() << endl << r.Perimeter();
    return 0;
}
```



### 对象的内存分配

和结构变量相同，对象所占用的内存空间大小，就等于所有成员变量的大小之和。（不计成员函数所占用的内存空间

每个对象都有各自的内存空间。一个对象的某个成员变量被改变了，不会影响到其他的对象。



### 对象间的运算

只能进行 = 赋值，不能使用其他的如： == ！=  <= 等。**除非这些运算符进行了重载**。

Q：什么是运算符重载？



### 类的用法

类的具体用法与结构体相似。

#### 特殊用法

引用名.成员名

```c++
CRectangle r2;
CRectangle & rr = r2;
rr.w = 5;
rr.Init(5, 4);
```

`& rr` 是引用，就相当于给对象重新起了个名字。

**下面是一个函数调用时的例子**

```c++
void PrintRectangle(CRectangle & r) {
	cout << r.Area() << "," << r.Perimeter();
}
CRectangle r3;
r3.Init(5,4);
PrintRectangle(r3);
```

#### 类的成员函数

类的成员函数和类的定义可以分开写

```c++
class CRectangle {
    public:
    int w, h;
    int Area();
    int Perimeter();
    void Init (int w_, int h_);
};
//成员函数体可以在class外写
int CRectangle::Area() {
    
}
```

#### 类成员的访问范围

**-private**：私有成员，只能在成员函数内访问。设置私有成员的机制，叫“**隐藏**”

**-public**：公有成员，可以在任何地方访问

**-protected**：保护成员，以后再说																																		值得注意的是，如果**无访问范围**，则会被视为**私有成员**。

<u>**在类的成员函数内部**</u>，能够访问：

1. 当前对象的全部属性、函数
2. 同类其他对象的全部属性、函数

<u>**在类的成员函数以外的地方**</u>，只能够访问该类对象的公有成员。

Q：假设有一类，该类的某一对象的成员函数能否访问同类的另一对象的私有成员变量或私有成员函数？

#### 成员函数的重载及参数缺省

此处的函数重载与参数缺省和前面所介绍的保持一致。

唯一需要注意的是，避免函数重载时出现的二义性：

```c++
class Location {
    private:
    int x, y;
    public:
    void valueX(int val = 0) {//参数缺省
        x = val;
    }
    int valueX() {//出现二义性
        return x;
    }
};
```



### 构造函数

- 是成员函数的一种
  - 名字与类名相同，可以有参数，不能有返回值（void也不行
  - *<u>作用</u>* 是**对对象进行初始化**，如给成员变量赋初值
  - 如果定义类时没写构造函数，则编译器生成一个默认的**无参数**的构造函数
- 如果定义了构造函数，则编译器不生成默认的无参数构造函数
- **对象生成时构造函数自动被调用**。对象一旦生成，就再也不能在其上执行构造函数
- 一个类可以有多个构造函数

```c++
class Complex{
    private:
    double real, imag;
    public:
    Complex(double r, double i = 0);
};
Complex::Complex(double r, double i) {
    real = r;
    imag = i;
}
Complex c1;//error 缺少构造函数的参数
Complex* pc = new Complex;//error，缺少参数
Complex c1(2);
Complex c1(2, 4), c2(3, 5);
Complex* pc = new Complex(3, 4);
```

​	

#### 构造函数重载

```c++
class Complex{
    private:
    double real, imag;
    public:
    void Set(double r, double i);
    Complex(double r, double i = 0);
    Complex(double r);
    Complex(Complex c1, Complex c2);
};
Complex::Complex(double r, double i) {
    real = r;
    imag = i;
}
Complex::Complex(double r) {
    real = r;
    imag = 0;
}
Complex::Complex(Complex c1, Complex c2) {
    real = c1.real + c2.real;
    imag = c1.imag + c2.imag;
}
```



#### 构造函数在数组中的使用

```c++
class Test {
    public:
    Test(int n) {}
    Test(int n, int m) {}
    Test() {}
};
Test array1[3] = {1, Test(1, 2)};//最终生成三个初始化后的对象
Test array2[3] = {Test(2, 3), Test(1, 2), 1};//最终生成三个初始化后的对象
Test* pArray[3] = {new Test(4), new Test(1, 2)};//最终生成2个初始化后的对象
```

  