# 基础[6]

<a id="0">`目录`</a>

- $\textcolor{#e18a3b}{【一】}$**[面向对象（下）](#1)**

## 面向对象（下）

<a id="1"><!--目录--></a>

- $\textcolor{#2a6e3f}{【01】}$ [static](#1.1)
- $\textcolor{#2a6e3f}{【02】}$ [类中代码块](#1.2)
- $\textcolor{#2a6e3f}{【03】}$ [final](#1.3)
- $\textcolor{#2a6e3f}{【04】}$ [抽象类|方法](#1.4)
- $\textcolor{#2a6e3f}{【05】}$ [接口](#1.5)
- $\textcolor{#2a6e3f}{【06】}$ [内部类](#1.6)
- $\textcolor{#2a6e3f}{【07】}$ [包装类](#1.7)

---

### 1、static<a id="1.1">💛</a>

> 开端：我们有时候希望无论是否产生了对象或无论产生了多少对象的情况下，**某些特定的数据在内存空间里只有一份**（唯一）

#### 1.1、介绍

​	静态变量：某些特定的数据在内存中只有一份，而且能被一个类的所有实例对象共享。可以使用类名.变量名的形式来访问。当然也可以先实例化对象在用对象.变量名访问

​	**它可以被类的每个实例化共享访问**

​	注意： static关键字只用于修饰 成员变量，不能用于修饰局部变量

#### 1.2、作用范围

1. **使用范围**：java static关键字可以用在变量、方法、代码块和嵌套类伤。

2. **作用范围**：static关键字属于类，而不是类的实例

   静态(static)修饰如下：

   - 变量：称为类变量、静态变量
   - 方法：称为类方法、静态方法
   - 代码块：称为静态代码块
   - 嵌套类：称为静态内部类

3. 被修饰后的成员具备以下特点：

   - 随着类的加载而加载 
   - 优先于对象存在 
   - 修饰的成员，被所有对象所共享 
   - 访问权限允许时，可不创建对象，直接被类调用

#### 1.3、静态变量

`类变量`（~~实例变量~~）

##### 1、区别

###### 1.1、静态变量

- 运行时，Java 虚拟机只为静态变量分配一次内存，加载类过程中完成静态变量的内存分配。
- 在类的内部，可以在任何方法内直接访问静态变量。
- 在其他类中，可以通过类名访问该类中的静态变量。

###### 1.2、实例变量

- 每创建一个实例，Java 虚拟机就会为实例变量分配一次内存。
- 在类的内部，可以在非静态方法中直接访问实例变量。
- 在本类的静态方法或其他类中则需要通过类的实例对象进行访问。

##### 2、特点

- **静态变量可以被类的所有实例共享**，因此静态变量可以作为实例之间的共享数据，增加实例之间的交互性。
- 如果类的所有实例都包含一个相同的常量属性，则可以把这个属性定义为静态常量类型，从而节省内存空间。

#### 1.4、静态方法

`类方法`（~~实例方法~~）

##### 1、区别

1. 静态方法，属于类，而不属于类的对象。
   - 它通过类直接被调用，无需创建类的对象。
   - **静态方法中，==不能使用 this | super关键字，也不能直接访问所属类的实例变量和实例方法==；**
   - **静态方法中，==可以直接访问所属类的静态变量和静态方法==。**
   - 同this 关键字，super 关键字也与类的实例相关，静态方法中不能使用 super 关键字。
2. 实例方法，可直接访问所属类的静态变量、静态方法、实例变量和实例方法。

##### 2、特点

###### 2.1、优点

1. 属于类级别，无需创建对象就即可直接使用，使用方便。
2. 全局唯一，内存中唯一，静态变量可以唯一标识某些状态。
3. 类加载时候初始化，常驻在内存，调用快捷方便。

###### 2.2、缺点

1. 静态方法不能调用非静态的方法和变量。
2. 不能使用this和super关键字。

###### 2.3、静态方法与静态变量适用场景

1. 静态方法，最适合工具类中方法的定义；比如文件操作，日期处理方法等。
1. 静态方法，适合入口方法定义；比如单例模式，因从外部拿不到构造函数，所以定义一个静态的方法获取对象非常有必要。
1. 静态变量适合全局变量的定义；举例：用一个布尔型静态成员变量做控制标志。

#### 1.5、静态类

​	`java`中一个类要被声明为static的，只有一种情况，就是**静态内部类（内嵌类）**。如在外部类声明为static的，程序会编译都不会通过。

- 静态内部类，跟静态方法一样，只能访问静态成员变量和方法，不能访问非静态方法和属性。
- 普通内部类，可以访问任意外部类的成员变量和方法。
- **静态内部类，可以声明普通成员变量和方法，而普通内部类不能声明static成员变量和方法。**
- 静态内部类，可以单独初始化。

> 静态内部类：
>
> ```java
> Inner i = new Outer.Inner();
> ```
>
> 普通内部类：
>
> ```java
> Outer o = new Outer();
> Inner i = o.new Inner();
> ```

---

### 2、类中代码块<a id="1.2">💛</a>

> **对Java类或对象进行初始化**

#### 2.1、静态代码块

> 用**static** 修饰的代码块

- 可以有输出语句。 
- 可以对类的属性、类的声明进行初始化操作。 
- **不可以对非静态的属性初始化**。即：不可以调用非静态的属性和方法。 
- 若有多个静态的代码块，那么按照**从上到下的顺序依次执行**。 
- **静态代码块的执行要先于非静态代码块。** 
- **静态代码块随着类的加载而加载，且只执行一次。**

#### 2.2、非静态代码块

> 不用**static** 修饰的代码块

- 可以有输出语句。 
- 可以对类的属性、类的声明进行初始化操作。 
- **除了调用非静态的结构外，还可以调用静态的变量或方法。** 
- 若有多个非静态的代码块，那么按照**从上到下的顺序依**次执行。 
- **静态代码块的执行要先于非静态代码块。** 
- **每次创建对象的时候，都会执行一次。且先于构造器执行**。

`注意`

> ```sql
> -- static 代码块
> -- 普通代码块
> -- 构造方法
> -- 普通代码块
> -- 构造方法
> ```
>
> 静态代码块只会调用一次
>
> 非静态代码块每次创建对象的时候，都会执行一次

#### 2.3、执行顺序

![](https://pic.imgdb.cn/item/639dbf70b1fccdcd36a63fc0.png)

---

### 3、final<a id="1.3">💛</a>

> Java中，final 表示最终，也可以称为完结器，表示对象是最终形态的，不可改变的意思。

#### 3.1、修饰变量

- 常量名要大写，内容不可修改
- **final**标记的变量(成员变量或局部变量)即称为常量。

#### 3.2、修饰函数

- **final**标记的方法**不能被子类==重写==**

#### 3.3、修饰类

- **final **标记的类**不能被继承**。提高安全性，提高程序的可读性。 

  例：String类、System类、StringBuffer类

---

### 4、抽象类|方法<a id="1.4">💛</a>

> ​	普通类是一个完善的功能类，可以直接产生实例化对象，并且在普通类中可以包含有构造方法、普通方法、static方法、常量和变量等内容。而抽象类是指在普通类的结构里面增加抽象方法的组成部分。
>
> ​	那么什么叫抽象方法呢？在所有的普通方法上面都会有一个“{}”，这个表示方法体，有方法体的方法一定可以被对象直接使用。**而抽象方法，是指没有方法体的方法**，同时抽象方法还必须使用关键字**abstract**做修饰。
>
> ​	而拥有抽象方法的类就是抽象类，**抽象类要使用abstract关键字声明**。**含有抽象方法的类必须被声明为抽象类。**

`注意`

- 抽象类不能被实例化。抽象类是用来被继承的，抽象类的子类**必须重写父类的抽象方法**，并提供方法体。若没有重写全部的抽象方法，仍为抽象类。
- **不能用abstract修饰变量、代码块、构造器；**
- **不能用abstract修饰私有方法、静态方法、final的方法、final的类。**

---

### 5、接口<a id="1.5">💛</a>

> Java接口是一系列方法的声明，是一些方法特征的集合，**一个接口只有方法的特征没有方法的实现，因此这些方法可以在不同的地方被不同的类实现，而这些实现可以具有不同的行为（功能）**。
>
> 就像一个类一样，一个接口也能够拥有方法和属性，但是在接口中声明的方法默认是抽象的。（**即只有方法标识符，而没有方法体**）。
>
> **==接口不能被实例化==**

`为什么要用接口？`

- 接口被用来描述一种抽象。
- 因为Java不像C++一样支持多继承，所以Java可以通过实现接口来弥补这个局限。
- 接口也被用来实现解耦。
- 接口被用来实现抽象，而抽象类也被用来实现抽象，为什么一定要用接口呢？接口和抽象类之间又有什么区别呢？原因是抽象类内部可能包含非final的变量，但是在接口中存在的变量一定是final，public,static的。

#### 5.1、定义及使用

<!--定义-->

```java
public interface InterStudy {
    public static final int MAX_SPEED = 100;
    public void getFileData();
    public void getFileData(int a);
}
```

<!--实现类使用-->

关键字 `implements`

```java
public class TestInterface implements InterStudy{
    @Override
    public void getFileData() {

    }
    @Override
    public void getFileData(int a) {

    }
}
```

> `注意`
>
> **实现类必须重写接口的全部方法，否则需要声明为抽象类**

#### 5.2、特点

- 接口中的方法都是抽象的，没有方法体，**所以不能直接实例化**
- 一个类可以实现不止一个接口。
- 一个接口可以继承于另一个接口，或者另一些接口，接口也可以继承，并且可以多继承。
- 一个类如果要实现某个接口的话，那么它必须要实现这个接口中的所有方法。
- 接口中所有的方法都是抽象的和public的，所有的属性都是public,static,final的。
- 接口用来弥补类无法实现多继承的局限。
- 接口也可以用来实现解耦。

---

### 6、内部类<a id="1.6">💛</a>

> **类的内部建立新的类**

#### 6.1、普通内部类

```java
public class OuterEasy {
    public int outField1 = 1;
    protected int outField2 = 2;
    int outField3 = 3;
    private int outField4 = 4;

    public void getOutMessage() {
        InnerEasy innerEasy = new InnerEasy();
        System.out.println(innerEasy.field1);
        System.out.println(innerEasy.field2);
        System.out.println(innerEasy.field3);
        innerEasy.field4++;
        System.out.println(innerEasy.field4);
    }
    public class InnerEasy {
        public int field1 = 5;
        protected int field2 = 6;
        int field3 = 7;
        private int field4 = 8;
        public void getInnerMessage() {
            System.out.println(outField1);
            System.out.println(outField2);
            System.out.println(outField3);
            outField4++;
            System.out.println(outField4);
        }
    }
}


public class Main {
    public static void main(String[] args) {
        OuterEasy outerEasy = new OuterEasy();
        outerEasy.getOutMessage();
        OuterEasy.InnerEasy innerEasy = outerEasy.new InnerEasy();
        innerEasy.getInnerMessage();
    }
}
```

##### 1、注意

- 内部类可以由**private , protected**定义
- **内部类对象可以访问外部类对象中所有访问权限的字段，同时，外部类对象也可以通过内部类的对象引用来访问内部类中定义的所有访问权限的字段**
- 普通内部类不可以定义静态变量|函数

##### 2、实例方式

```java
OuterEasy outerEasy = new OuterEasy();
OuterEasy.InnerEasy innerEasy = outerEasy.new InnerEasy();

外部类 xxx = new 外部类(...);
外部类.部类 = xxx.new 内部类(...);
```

#### 6.2、静态内部类

```java
public class OutStatic {
    public int out1;
    protected int out2;
    private int out3;
    int out4;

    public void getInner(){
        System.out.println(InnerStatic.innerOut4);
    }
    public static class InnerStatic {
        public int innerOut1;
        protected int innerOut2;
        private int innerOut3;
        static int innerOut4;
        
    }
}
```

##### 1、注意

- 只要在具有访问权限的地方，我们就可以通过 `类名.静态成员名` 的形式来访问这个静态成员
- 静态内部类也是作为一个外部类的静态成员而存在，**创建一个类的静态内部类对象不需要依赖其外部类对象**
- 静态内部类不能访问外部类的非静态成员变量和方法

##### 2、实例化

```java
OutStatic.InnerStatic innerStatic = new OutStatic.InnerStatic();
// 不需要通过外部类实例化创建，不需要依赖外部类对象。

外部类.内部类 xxx = new 外部类.内部类();
```

#### 6.3、匿名内部类

> 该类没有名字（但是系统会分配一个代号在内存中）
>
> 为什么使用？
>
> ​	在实际开发中，我们常常遇到这样的情况：一个接口/类的方法的某个实现方式在程序中只会执行一次，但为了使用它，我们需要创建它的实现类/子类去实现/重写。此时可以使用匿名内部类的方式，可以**无需创建新的类，减少代码冗余**。

<!--原方式-->

```java
public class Test {
    public static void main(String[] args) {
        B b = new B();
        b.eat();
    }
}
interface A{
    public void eat();
}
class B implements A{
    @Override
    public void eat() {
        System.out.println("eat.....");
    }
}
```

<!--匿名内部类-->

```java
public class Test {
    public static void main(String[] args) {
        new A(){
            @Override
            public void eat() {
                System.out.println("正在调用eat方法");
            }
        }.eat();
    }
}
interface A{
    public void eat();
}

------or
    
public class Test {
    public static void main(String[] args) {
        A a = new A(){
            @Override
            public void eat() {
                System.out.println("eat....");
            }
            public void drink(){
                System.out.println("drink.....");
            }
        };
        a.eat();
        a.drink();
    }
}
interface A{
    public void eat();
    public void drink();
}
```

##### 1、注意

1. 使用匿名内部类时，我们必须是继承一个类或者实现一个接口，但是两者不可兼得，同时也只能继承一个类或者实现一个接口。
2. 匿名内部类中是不能定义构造函数的。
3. 匿名内部类中不能存在任何的静态成员变量和静态方法。
4. 匿名内部类为局部内部类，所以局部内部类的所有限制同样对匿名内部类生效。
5. 匿名内部类不能是抽象的，它必须要实现继承的类或者实现的接口的所有抽象方法。

---

### 7、包装类<a id="1.7">💛</a>

#### 7.1、概述

​	Java有8种基本数据类型：**整型(byte、short、int、long)、浮点型(float、double)、布尔型boolean、字符型char，相对应地，Java提供了8种包装类Byte、Short、Integer、Long、Float、Double、Boolean、Character。包装类创建对象的方式就跟其他类一样。**

- Java一切都是对象。Java语言是面向对象的编程语言，而基本数据类型声明的变量并不是对象，为其提供包装类，增强了Java面向对象的性质。

- 如果只有基本数据类型，使用时是很不方便的，比如，在集合类中，无法将int 、double等类型放进去的，因为集合的容器要求元素是Object类型。


- 包装类还为基本类型添加了属性和方法，丰富了基本类型的操作。如当我们想知道int取值范围的最小值，我们需要通过运算，如下面所示，但是有了包装类，我们可以直接使用Integer.MAX_VALUE即可。

#### 7.2、自动装箱、拆箱

<!--基本写法-->

```java
Integer num1 = new Integer(1);	//基本数据类型转为包装类
Integer integer = Integer.valueOf(10);//基本数据类型转为包装类
int num2 = num1.intValue();		//包装类型转为基本数据类型
System.out.println(num1 +"	"+ num2);
```

`自动装箱 | 拆箱`

```java
//包装类中的自动装箱拆箱机制
Integer  num1 = 1;		//自动装箱
int num2 = num1;		//自动拆箱
System.out.println(num1 +"	"+ num2);
```

#### 7.3、优缺点

##### 1、优点

-  首先，Java语言是一个面向对象的语言，但是Java中的基本数据类型却是不面向对象的，将每个基本数据类型设计一个对应的类进行代表，这种方式增强了Java面向对象的性质。


- 其次，如果仅仅有基本数据类型，那么在实际使用时将存在很多的不便，很多地方都需要使用对象而不是基本数据类型。比如，在集合类中，我们是无法将int 、double等类型放进去的，因为集合的容器要求元素是Object类型。而包装类型的存在使得向集合中传入数值成为可能，包装类的存在弥补了基本数据类型的不足。

- 此外，包装类还为基本类型添加了属性和方法，丰富了基本类型的操作。如当我们想知道int取值范围的最小值，我们需要通过运算，如下面所示，但是有了包装类，我们可以直接使用Integer.MAX_VALUE即可。

##### 2、缺点

> 为何保留基本数据类型

​	用new关键字创建的对象是存储在堆里的，我们通过栈中的引用来使用这些对象，所以，对象本身来说是比较消耗资源的。对于经常用到的类型，如int等，如果我们每次使用这种变量的时候都需要new一个对象的话，就会比较笨重了。所以，Java提供了基本数据类型，这种数据的变量不需要使用new在堆上创建，而是直接在栈内存中存储，因此会更加高效。

---

[<!--返回目录-->](#1)

[<!--返回总目录-->](#0)

**[README](../../README.md)**



