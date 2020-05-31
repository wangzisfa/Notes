# 【JAVA核心技术】之对象与类

## 面向对象与面向过程之间的区别

### 关注点不同

- 面向对象顾名思义，关注点在对象。可以说一切在类中的方法都围绕着这一类进行。

- 而面向过程则通过对于解决问题的方法的关注而进行。有着**程序=算法+数据结构**的特点。

### 程序设计思路不同

- 面向过程先设计出解决问题的方法，然后再搭建出一个框架。
- 而面向对象的程序设计则先关注于框架的搭建，然后再解决框架内方法的搭建。**（将数据放在第 一位，然后再考虑操作数据的算法。）**

### 解决问题的规模不同

由于设计模式的不同，面向过程与面向对象能够解决的问题规模也有着很大的区别

- 面向过程通常适用于解决较小规模的问题。主要原因在于其无法归纳出一类问题如何解决的方案。时常会因为函数过多而冗杂。耦合度很高
- 面向对象的程序设计适用于解决规模较大的问题。主要原因在于其提供了一个解决一类问题的框架。即**包->类->方法**的逐级过渡，主体思路十分清晰。

## 类

类是构造对象的蓝图

学会使用UML图

### 类与类之间的三种关系

- 依赖(uses-a)
- 聚合(has-a)
- 继承(is-a)

优化程序的关键：**降低耦合度** —— 减少类之间的依赖关系



## 对象

### 对象三特性

- 行为(behavior)
- 状态(state)
- 标识(identity)

### 注意

- 每个对象都保存着描述当前特征的信息
- 作为类的实例，每个对象的标识永远是不同的

---

## 预定义类

虽然java是一个面向对象的语言，但是其很多类都不具有面向对象的特性。而在使用其对象时，就必须**构造**对象，并**指定其初始状态**。

### 构造器——一种特殊的方法（就是指针)

构造并初始化对象

#### 如何创建一个构造器？

方法：

1. 在指定类名前加 `new` ，其后加括号。（仅用一次
2. 如果希望对象多次使用，需要将对象存放在一个变量中：`Date birthday = new Date();` ![image-20200318115141746](C:\Users\hp\AppData\Roaming\Typora\typora-user-images\image-20200318115141746.png)

总的来说，创建构造器就两种方法。直接new出这个类，然后直接引用。或者构造出一个对象变量，然后使对象变量指向（或者说用于存放对象）该对象。

---

**注意** ：不能出现如下：

```java
Date birthday;
String s = birthday.toString();//产生编译错误
```

因为没有初始化变量birthday，需要`Date birthday = new Date(); ` 或者：`birthday = playday;` playday是已有的Date对象。

**对象变量并没有实际包含一个对象，而仅仅引用一个对象**。

---

### 更改器和访问器

通俗的来说，**更改器方法**就是 在某个类中的一个方法，可以通过调用该方法**直接修改当前对象的属性**。

```java
LocalDate aThousandDaysLater = newYearsEve.plusDays(1000);//没有更改newYearsEve对象的内容
someDay.add(Calendar.DAY_OF_MONTH,1000);//直接修改someDay
```



访问器方法：只访问对象，而不修改对象

`LocalDate.getYear`

**注意** ：访问器方法在编写上一定不能直接返回实例域，一定要返回一个**克隆值**。否则将不具有封装的特性。



---

## 自定义类

**主力类** ：没有main方法，却有自己的实例域和实例方法。

**要想创建一个完整的程序，应该将若干类组合在一起，其中只有一个类有main方法。**





- 关于在linux中编译java时的注意：

1. 如果一个源文件中包含多个类，在编译时将包含main方法的类名提供给字节码解释器，以启动这个程序。
2. 如果每个源文件中只包含一个类，也就是所谓的多个源文件使用：
   1. 通配符*， 所有与通配符相匹配的源文件都将被编译成类文件
   2. 直接编译包含main方法的源文件，其他所引用的类会自动查找出该类进行编译。





### 构造器

外部使用时类似指针，而编写构造器时就像给类初始化。

- 构造器总伴随着new操作一起调用

- java对象都是在堆中构造的

- 不能在构造器中定义与实例域重名的局部变量

  ![image-20200321163223184](C:\Users\hp\AppData\Roaming\Typora\typora-user-images\image-20200321163223184.png)

- 其他操作基本与c++类似

#### **注意**

- 父类中如果显式地定义了构造函数，且有参数，那么就必须显式地定义一个无参构造函数，否则子类就会报错！

### 隐式参数与显式参数

```java
number.raiseSalary(5);
```

number为raiseSalary方法的隐式参数（或者称为方法调用的接收者

5 为raiseSalary方法的显式参数



关键字**this** 代表的就是隐式参数，在编写方法时能够清晰地将实例域与局部变量明显的区分出来。

简单的来说就是，this后跟的就是实例域。

```java
public void raiseSalary(double byPercent) {
    double raise = this.salary * byPercent / 100;
    this.salary += raise;
}
```



**注意** ：java所有的方法都必须在类的内部定义



---



## 静态域与静态方法（static

简单的来说，就是当有很多相同类的方法时，他们之间共享一个相同的静态域，**静态域属于类** 而不属于 对象。

### 静态常量

eg：

```java
public class Math {
    public static final double PI = ...;
}
```

可以直接通过Math.PI进行访问，如果关键字static被省略，就只能通过Math类对象进行访问。

---

### 静态方法

最典型的静态方法就是  **main方法**

Math.pow(x, a)

同样是不需要任何Math对象，即没有**隐式参数**





Q:如何初始化某一私有静态域值，并且在初始化后不能再被改变？





关于静态方法和静态域之间的用法实例：

```java
private static String Declare = "helloworld";	
public static String FindDeclare() {
       //s = Declare;
       return Declare;
    }
    public String Find(String s) {
        return Declare;
    }

    public static void main(String args[]) {
        notebook sample = new notebook();
        //构造出String类对象
        String f = new String();
        f = sample.Find(f);//类对象通过非静态方法访问静态域
        //输出该String类对象f的值
        System.out.println(f);
        
        f = sample.FindDeclare();//类对象通过静态方法访问静态域
        System.out.println(f);
        
        //测试能否直接通过类名引用
        f = notebook.FindDeclare();//类名直接通过静态方法访问静态域
        System.out.println(f);
        
        f = notebook.Find();//类名直接通过非静态方法访问静态域（不可以！！）
    }
```



通过以上实例，得出 **静态方法可以不需要类对象而直接通过类名访问** ，非静态方法不可以。



---



## 方法参数

java程序设计语言总是采用**按值调用**， 方法得到的是所有参数值的一个**拷贝**，并且方法不能修改传递给它的任何参数变量的内容。

![image-20200328002930255](C:\Users\hp\AppData\Roaming\Typora\typora-user-images\image-20200328002930255.png)

![image-20200328003309004](C:\Users\hp\AppData\Roaming\Typora\typora-user-images\image-20200328003309004.png)



**方法参数**有两种类型：

- 基本数据类型
- **对象引用** （**按值传递**





---

## 对象构造

### 重载

java中**任何方法都能进行重载**

---

### 默认域初始化

如果构造器没有**显式**地赋值，未赋值的将被自动赋为默认值：0， false， null

**最好明确地对域进行初始化**，这也正是域与局部变量之间的区别！

#### 无参构造器

---



