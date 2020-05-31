# 【JAVA核心技术】之接口、lambda表达式、内部类

## 接口

引言：

在java程序设计中，各个类之间会相互引用内部方法。而接口正是一种用于规范这种方法的方式。



> 以 java.util.Arrays; 中规定的 sort() 方法为例，要想在类中使用 sort() 方法，首先需要在类声明中使用关键字引入接口。其次需要在类中实现其所要求的接口方法（即 int compareTo(Object other) ）



接口本身是定义在规范这个接口的类中的。如下：

>```java
>public interface Comparable{
>    int compareTo(Object other);
>}
>```



要想在某个类中使用该接口，需要以下步骤：

1. 在类声明中使用 implements 关键字
2. 对接口中的所有方法进行定义

>```java
>public int compareTo(Object other) {
>    ...
>}
>```



### 接口的特性

- 可以声明接口类型的变量，并且这个变量可以引用使用了这个接口的变量
- 接口可以使用 instanceof 关键字 用于判断一个对象是否使用了这个接口
- 接口同样可扩展、可继承，也可以在接口中包含常量。（ **接口中的域被设置为 public static final** 
- 接口同样可以不含有任何方法
- 一个类可以有多个接口



- [ ] Cloneable



### 关于多重继承

很抱歉，java不支持多重继承。

也就是说不能：

```java
public class Test extends TestOri, TestOrigin;//nope :( 
```

这样也同样解释了为什么不直接把 接口 写入 超类 中（因为一个类只能继承于一个类



**但是**，接口可以进行多重继承，并将这些 接口 在类中进行实现。



### 接口中的静态方法

> 目前为止，通常的做法都是将静态方法放在伴随类中。在标准库中，你会看到成对出现的接口和实用工具类，如：Collection/Collections 或 Path/Paths



- [ ] 什么是伴随类？
- [ ] 意义？



书上例：

>```java
>public interface Path{
>    public static Path get(String first, String... more) {
>        return FileSystem.getDefault().getPath(first, more);
>    }
>}
>```



### 默认方法

作用：为接口提供一个默认实现（修饰符：**default**

>```java
>public interface Comparable<T> {
>    default int compareTo(T other) {
>        return 0;
>    }
>}
>```



#### 默认方法冲突



### 接口回调



### comparator接口



### 对象克隆



## lambda表达式

参数->表达式



lambda表达式 能够替代一部分代码片段

在测试类中实现了某个接口，便可以通过使用 lambda表达式 进行相关的简化操作



用法：

```java
package InterfaceFuc;

import java.util.Timer;

public class TestNumber {
	private int var1;
	private int var2;

	public TestNumber() {
		this.var1 = -1;
		this.var2 = -1;
	}

	public TestNumber(int var1, int var2) {
		this.var1 = var1;
		this.var2 = var2;
	}

	public void setVar1(int var1) {
		this.var1 = var1;
	}

	public void setVar2(int var2) {
		this.var2 = var2;
	}

	public int getVar1() {
		return var1;
	}

	public int getVar2() {
		return var2;
	}

	public void showMult(int var1, int var2, NumberInterface numberInterface) {
		System.out.println(numberInterface.MultNumbers(var1, var2));
	}

	public static void main(String[] args) {
		TestNumber testNumber = new TestNumber(10, 11);
		testNumber.showMult(testNumber.getVar1(), testNumber.getVar2(), (int n1, int n2)->testNumber.getVar1()+testNumber.getVar2());
	}
}

---接口如下：

package InterfaceFuc;

public interface NumberInterface {
	public int MultNumbers(int var1, int var2);
}

```





### 方法引用

三种：

1. 对象方法（Object::instanceMethod
2. 类静态方法（class::staticMethod
3. 类方法（class::instanceMethod





### 构造器引用



### 变量作用域





### 处理lambda表达式



### comparator



## 内部类

类内部的类、函数内部类





### 使用内部类访问对象状态



### 内部类的特殊语法规则



### 局部内部类



### 由外部方法访问变量



### 匿名内部类



### 静态内部类

















































