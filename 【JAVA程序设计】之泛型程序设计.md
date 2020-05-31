# 【JAVA程序设计】之泛型程序设计

Q：

1. 返回类型和类型参数到底顺序是怎么样的：

   A：如果 返回值 有 类型参数，就不需要在 返回值前 声明出 类型参数

2. 







---

> 使用泛型机制编写的代码要比那些杂乱地使用 Object 变量，然后再进行强制类型转换的代码具有更好的安全性和可读性。

泛型很像 C++ 中 的模板



---

泛型意味着编写的代码可以被很多不同类型的对象所重用



## 泛型与ArrayList

在出现泛型之前，就有了 ArrayList 类，它只维护一个 Object 类，也就是说所有元素进去都是 Object 的原始类，在需要时进行强制类型转换，**并且没有错误检查**

### 关于强制类型转换

强制类型转换在 继承 章节已经有所了解，这里只说一点：

- 子类向父类转换后，**并不会丢失数据**。也就是说在转换之后，子类中父类没有的数据被**隐藏**，当需要再重新转换为子类时，没有数据丢失。

### 

### 类型参数

Java SE 7后 ArrayList 添加了类型参数：

```java
ArrayList<String> n1 = new ArrayList<>();
//或者
ArrayList<String> n1 = new ArrayList();
```



> 使程序具有更好的可读性和安全性



### 通配符类型

在 继承 章节中了解了不能出现：

```java
son ason = (son) new parent();//Error
```

同样对于 ArrayList 类：

```java
ArrayList<son> ason = 
```









## 简单泛型类

### 泛型类

定义一个泛型类：

```java
public class aGenericity<T, K> {//T, K 为类型变量
    private T first;
}
```



Tips：

1. 类型变量大多为大写：

   ​	E 表示集合的元素类型

   ​	K,V 分别表示表的关键字与值的类型

   ​	T 表示 “任意类型”

2. 用具体的类型替换类型变量就可以实例化泛型类型，可以将结果想象为带有构造器的普通类



> 泛型类可以看作普通类的工厂



## 泛型函数

```java
double middle = ArrayAlg.getMiddle(3.14, (double)2, (double) 3);
//或者
Number middle = ArrayAlg.getMiddle(3.14, 2, 3);

public static <T> T getMiddle(T...a) {//<>中是类型参数， 类型参数后跟返回类型 方法名 方法参数
		return a[a.length / 2];
}
```

这里 getMiddle 函数的参数是 T ，T 表示是某一种类型的参数，如果此时传入的参数不同类 **就会报错** 。所以应考虑以上两种方法来修补参数的类型



### 类型限定

关于类型 T ，可以是任何类型。但如果该泛型函数内部使用了一些**限定类型的方法**时，T 类型就有可能出问题。比如：想要实现 compareTo 方法，就需要进行限定（因为某些类并没有继承 Comparable方法）



>通过设置限定，可以实现确定类 T 实现了 Comparable 方法



```java
public class test{
    public static <T extends Comparable & Serializable> Pair<T> minmax(T...a) {
        //<T extends Comparable & Serializable> 在这里就表示限定，后跟返回类型 Pair<T>，方法名和方法参数
    }
}
```

Tips：

1. 如果想添加多个限定，限定之间应该使用 & 符号进行分隔。
2. 限定不仅限于 接口，也可以是某个类



## 继承

泛型继承并不像普通类之间的继承那么简单。

如果某个泛型类的 类型参数 是另一个泛型类 中 类型参数 的 子类 或 父类，不能直接使用 多态性。

需要使用 **类型限定符** 。

### 通配符类型

分为 **超类型限定**`<? super T>` 和  **子类型限定**`<? extends T>` 

```java
Pair<? extends parent> getValue();
//equalsTo
parent = ?;
//相当于这样传递出的 ？类型可以是 parent 类型的子类型或者自身，这时在任何 Pair 类中都不存在 ClassCastException（任何 Pair 类型是指： Pair<parent> Pair<son> Pair<daughter>等 存在于类型参数中的子类型或自身

setValue(Pair<? extends parent>);
//equalsTo
parent = ?;//OK
son = ?;//Error， ? 可以是 parent 类型，这样就会产生ClassCastException
```



```java
setValue(Pair<? super son>);
//equalsTo
parent = ?;//ok, ? 可以是 son 类型的超类新或自身
son = ?;//ok, ? 可以是自身

Pair<? super son> getValue();
son = ?;//Error ，如果 ? 类型为 parent 类型就会出现ClassCastException
```

通过上面两个例子可以看出，使用通配符时，**超类型限定 **只能用来 设置形参的值，也就是 **写入** 。而子类型限定则只能用来 传递值 也就是 **读取** 。

通配符类型可以出现在 类 的 返回值 中，也可以 在 参数列表 中体现。

**值得注意的是**， 通配符类型 可以极大的提高 某个类 的 **复用性**，较于传统的普通类而言，普通类在编写过程中就必须限定出 类型限定 的具体类型，而 通配符类型 能够 使用 类型限定中 不仅限于 `? extends XX || ? super XX` XX 这一种 类型，也可以是 XX 类型的 子类型 或 父类型。**但是** ，类型的实例**不能混用** ，也就是 一旦编译器确定了这个 ？ 是什么类型，就固定是什么类型，在这个实例中就 不能使用 其他类型了。



### 真正的继承

类继承 和 方法继承

```java
//类继承
public class Test<T extends Comparable> {
	private T test;
    public Test() {
        this.test = null;
    }
    public Test(T test) {
        this.test = test;
    }
    public void setTest(T test) {
        this.test = test;
    }
    public T getTest() {
        return this.test;
    }
}

//错误演示
public class Testson<T, V> extends Test<T extends Comparable> {
    ...//这里继承到的Test 后跟的类型参数 仅仅代表的是Testson 中的 T。实际上，Test 中的T 是无法传过来的。但是可以通过 类型限定 的类型，直接根据该类型给出参数就可以
}

//正确演示
public class Testson<V extends Number> extends Test {
    private V number;
    public Testson() {
        super();//这里得到了父类实例域中的 T
        this.number = null;
    }
    public Testson(String string, V number) {
        super(string);//这里无需类型转换，并且设置的是父类实例域 T
        this.number = number;
    }
}
```







## 泛型代码与虚拟机

> 虚拟机中没有泛型类型对象，所有对象都属于普通类

### 类型擦除（erased

> 无论何时定义一个泛型类型，都自动提供了一个相应的原始类型 （**raw type**），原始类型的名字就是删去类型参数后的泛型类型名。擦除类型变量，并替换为**限定类型** （若无限定类型的变量使用 Object

类型擦除后的代码：

```java
public class Pair {
    private Object first;
    private Object second;
    
    public Pair(Object first, Object second) {
        this.first = first;
        this.second = second;
    }
    
    public Object getFirst() { return this.first; }
    public Object getSecond() { return this.second; }
    
    public void setFirst(Object newValue) { this.first = newValue; }
    public void setSecond(Object newValue) { this.second = newValue; }
}
```



Tips：

1. 如果涉及到原始类型替换， 且有**限定** ，则使用限定的第一个类型变量来替换。所以应该尽量将 **标签接口** 放在边界列表的末尾
2. 接第一点，编译器在必要时也要向后面的 类型变量 插入 强制类型转换



### 翻译泛型表达式 && 方法

#### 泛型表达式

编译器将方法调用翻译为两条虚拟机指令：

- 调用原始方法
- 强制类型转换

#### 泛型方法

**合成桥方法**









## 错误

![image-20200424125249632](C:\Users\hp\AppData\Roaming\Typora\typora-user-images\image-20200424125249632.png)





![image-20200424125354723](C:\Users\hp\AppData\Roaming\Typora\typora-user-images\image-20200424125354723.png)