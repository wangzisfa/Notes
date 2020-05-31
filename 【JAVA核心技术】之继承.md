# 【JAVA核心技术】之继承

# 继承

## 类、超类、子类

子类继承（extends）于父类（超类）

**java中所有继承都是公有继承**。

### 超类与子类的关系

通俗来讲：**通用的方法放在超类中，将具有特殊用途的方法放在子类中** 

#### 覆盖（override）

什么是覆盖：

> 指的是超类中的某些方法与子类中的类似，但有一定差异，则需要通过子类的覆盖来改写超类的方法的做法。

有时进行覆盖时需要访问父类的私有域，则需要借助公有的接口。

关键字**super** ：可以直接访问超类的方法，如：

```java
super.getSalary();
```

### 子类构造器

> 子类在继承超类之后，在调用子类对象时，进行构造对象的方法

如果无显式子类构造器，则会直接调用超类的默认构造器（无参构造器。否则将会报错

下面是子类构造器的一个参考示例：

```java
public class testOri{//两个数字相加
	private double Number1;
	private double Number2;
	//构造函数
	public testOri(double Number1, double Number2) {
		this.Number1 = Number1;
		this.Number2 = Number2;
	}

	public testOri() {
		this.Number1 = 0;
		this.Number2 = 0;
	}
//get set
	public double getNumber1() {
		return this.Number1;
	}
	public double getNumber2() {
		return this.Number2;
	}

	public void setNumber1(double number1) {
		this.Number1 = number1;
	}
	public void setNumber2(double number2) {
		this.Number2 = number2;
	}

	//相加函数
	public double calculateAdd() {
		return getNumber1() + getNumber2();
	}
	public double calculateMinus() {
		return this.Number1 - this.Number2;
	}
	public double calculateMult() {
		return this.Number1 * this.Number2;
	}
}
public class test extends testOri{

	public test(double Number1, double Number2) {
		super(Number1, Number2);
	}

	@Override
	public double calculateAdd() {
		return super.calculateAdd() * 5;
	}

	public double calculateMult2() {
		return super.getNumber1() * 2 + super.getNumber2() * 2;
	}
}
```



什么是静态绑定和动态绑定：

>一个对象变量在运行时可以自动地选择调用哪个方法叫动态绑定
>
>使用关键词 private、static、final  叫静态绑定？

---



### 多继承

java中不支持多继承，多继承实现方式参考 接口

---

### 多态

**子类可以赋给父类，父类不能赋给子类**

---

### 阻止继承：final类和方法

如果某个类被声明为final，则该类不允许被继承，并且其方法全部变为final，但是实例域不变

也可以单独对某个方法进行声明final， 这样的方法不能被覆盖。



---

### 强制类型转换

**子类与父类对象之间的强制类型转换就是多态**

- 当一个 父类对象 和一个 子类对象 同时被初始化之后，将 子类对象 直接赋给 父类是**允许**的。（**没有发生强制类型转换！**
- 当一个父类对象被初始化时使用的是 父类构造器（new parent ，此时 **父类对象 不能直接赋给 子类对象**，并且触发 ClassCastException 异常
- 如果父类对象初始化时使用的是 子类构造器（new son，此时 **父类对象可以通过强制类型转换赋给子类对象**。这样也就是达到了所谓的多态？
- 创建对象时，子类不能直接使用父类构造函数：`son ason = (son) parent();//ERROR!`





---

### 抽象类

> 抽象类相当于将超类提升至了更高一级的层次，它宏观的定义了类的实例域、方法

使用关键字 abstract 定义的类 叫抽象类

```java
public abstract class test{
    public abstract String getDescription();
}
public class aStudentTest extends test{
    private String aStudentName;
    public aStudentTest(String AStudentTest) {
        this.aStudentName = AStudentTest;
    }
    public String getStudentName() {
        return this.aStudentName;
    }
    public void setStudentName(String AstudentName) {
        this.aStudentName = AStudentName;
    }
    
    public String getDescription() {
        System.out.println("This is a student Who's name is " + this.aStudentName);
    }
}
public class aTeacherTest extends test{
     
}
```

注意：

1. 抽象类中可以包含具体方法，但是建议最好将通用的方法和域放在超类中
2. 如果某一类是抽象类，则不会出现该类的对象
3. 抽象类也同普通子类与父类关系一样，遵从 ”多态法则“
4. 抽象类可以引用非抽象子类对象：`test n1 = new aStudentTest("John");`



- [ ] c++纯虚函数与抽象类



关于 getDescription 方法的另一用法：

```java
test[] n1 = new test[3];
test[0] = new aStudentTest("John");
test[1] = new aStudentTest("Mike");
test[2] = new aTeacherTest("Peter");

for (test e : n1) {
    System.out.println(e.getDescription());
}
```

这样直接通过抽象类数组循环访问抽象类方法，并不会因为抽象类方法无参数而无法实现，反而会直接调用子类的相关覆盖方法。

**在 接口 章节中将会看到更多抽象类方法**



---

## 所有类的超类：Object

## ArrayList

> ArrayList 泛型数组列表 能够存储某一类及其子类的类数组方法



创建ArrayList： 

```java
ArrayList<> list = new ArrayList <>();
```

删除某一元素：

```java
list.remove(index);
```



list.toArray();方法

直接将数组元素拷贝至另一数组中。**需要注意的是** toArray方法中的参数类型必须为list继承类，不能是其他非相关类（java.lang.ArrayStoreException: arraycopy: element type mismatch: can not cast one of the elements of java.lang.Object[] to the type of the destination array



### 类型化ArrayList与原始ArrayList的兼容性



---

## 对象包装器与自动装箱

> 有时需要将基本类型包装为对象，而创建的关于基本类型的类就叫做包装器。如int这种基本类型其对应的基本类为 Integer 。6类基本数字类型的类都继承于超类 Number 



java是如何实现自动装箱与拆箱的？

```java
list.get(2);//这是ArrayList中的方法get，表示取在该位置的ArrayList数组中的元素
list.get(Integer.valueOf(2));//这是它的本来样貌

int i = list.get(i);
int i = list.get(i).intValue();
```





## 参数数量可变的方法（…























