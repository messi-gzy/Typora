# C++基础（3）

<a id="0">`目录`</a>

- $\textcolor{#e18a3b}{【一】}$**[类和对象](#1)**

## 一、类和对象

<a id="1"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [封装权限](#1.1)
- $\textcolor{#2a6e3f}{【2】}$ [初始化与释放](#1.2)
- $\textcolor{#2a6e3f}{【3】}$ [对象模型与拷贝](#1.3)
- $\textcolor{#2a6e3f}{【4】}$ [this](#1.4)
- $\textcolor{#2a6e3f}{【5】}$ [友元](#1.5)
- $\textcolor{#2a6e3f}{【6】}$ [运算符重载](#1.6)
- $\textcolor{#2a6e3f}{【7】}$ [继承](#1.7)
- $\textcolor{#2a6e3f}{【8】}$ [多态](#1.8)
- $\textcolor{#2a6e3f}{【9】}$ [虚函数|抽象类](#1.9)
- $\textcolor{#2a6e3f}{【10】}$ [](#1.10)
- $\textcolor{#2a6e3f}{【11】}$ [](#1.11)
- $\textcolor{#2a6e3f}{【12】}$ [](#1.12)

### 1、封装与权限<a id="1.1">💚</a>

面向对象的三大特性 ：`封装`、`继承`、`多态`

#### 1、封装

##### 1、封装的意义

- 将属性和行为作为一个整体，表现生活中的事务
- 将属性和行为加以权限控制

##### 2、实例化对象

```c++
class Circle
{
public:
    double m_dr;
    double Calculate()
    {
        return 2*m_dr*PI;
    }
};
int main() {
    Circle circle;
    circle.m_dr=10;
    cout<<circle.Calculate()<<endl;
    return 0;
}
```

##### 3、意义

属性：成员变量

行为：成员方法

#### 2、权限

##### 1、访问权限

- 公共权限 `public`             类内和类外都可以访问
- 保护权限 `protected`       类内可以访问，类外不可以访问。==子类可以访问父类内容==
- 私有权限 `private`           类内可以访问，类外不可以访问。==子类不可以访问父类内容==

```C++
class Student
{
public:
    string m_strName;
protected:
    char m_chID[18];
private:
    char m_chPassword[64];
};
```

##### 2、struct和class区别

`struct` 默认 ==公共==（public）

`class`   默认 ==私有== （private）



### 2、初始化与释放<a id="1.2">💚</a>

##### 1、构造函数和析构函数

**构造函数** ：`类名（）{}`

- 与类名相同
- **可以有参数，发生重载**
- **自动调用**

**析构函数** ： `~类名（）{}`

- ~+类名
- 不可以有参数，不可以重载
- **在对象销毁时自动调用**

```c++
class Student
{
public:
    string m_strName;
    int m_dID;
    Student(string name,int id)
    {
        cout<<"构造函数"<<endl;
        this->m_strName=move(name);
        this->m_dID=id;
    };
    ~Student()
    {
        cout<<"析构函数"<<endl;
    }
};
```

`作用：释放堆区内存`

##### 2、构造函数的分类

**两种分类** ：

1. 参数：

   - 有参构造

   ```c++
   Student(string name,int id)
   {
       cout<<"构造函数"<<endl;
       this->m_strName=move(name);
       this->m_dID=id;
   };
   ```

   - 无参构造

   ```c++
   Student()
   {
       cout<<"无参构造函数"<<endl;
   };
   ```

2. 类型

   - 普通构造

     ```c++
     Student(string name,int id)
     {
         cout<<"构造函数"<<endl;
         this->m_strName=move(name);
         this->m_dID=id;
     };
     ```

   - 拷贝构造

     ```c++
     Student (const Student &student)
     {
         this->m_strName=student.m_strName;
         this->m_dID=student.m_dID+1;
     }
     ```

**三种调用方式** ：

1. 括号法

   - 默认

     > ```c++
     > Student student_1;
     > ```

   - 有参

     > ```c++
     > Student student_2("a",20);
     > Student s1=Student("a",20);
     > ```

   - 拷贝

     > ```c++
     > Student student_3(student_2);
     > ```

2. 显示法

   ```c++
    Person p2 = Person(10); 
    Person p3 = Person(p2);
   ```

   Student *student=new Student("a",10);
   delete student;

3. 隐式转换法

```
 Person p4 = 10; // Person p4 = Person(10); 
 Person p5 = p4; // Person p5 = Person(p4); 
```

==注意：不能利用 拷贝构造函数 初始化匿名对象 编译器认为是对象声明==    //`Student p5(p4);`

##### 3、拷贝构造函数及调用时机

C++中拷贝构造函数调用时机通常有三种情况

- 使用一个已经创建完毕的对象来初始化一个新对象
- 值传递的方式给函数参数传值
- 以值方式返回局部对象

`拷贝构造函数`

```c++
Student (const Student &student)
{
    this->m_strName=student.m_strName;
    this->m_dID=student.m_dID;
}
```

引用方式：`const Student &student`

==拷贝防止原参数被改变==

##### 4、构造函数调用规则

默认情况下，c++编译器至少给一个类添加3个函数

1．默认构造函数(无参，函数体为空)

2．默认析构函数(无参，函数体为空)

3．默认拷贝构造函数，对属性进行值拷贝

构造函数调用规则如下：

* 如果用户定义有参构造函数，c++不在提供默认无参构造，但是会提供默认拷贝构造

* 如果用户定义拷贝构造函数，c++不会再提供其他构造函数

##### 5、深拷贝和浅拷贝

`浅拷贝`：简单的赋值拷贝操作

`深拷贝`：在堆区重新申请空间，进行拷贝操作

> 浅拷贝问题：堆区的内存被重复释放。
>
> 利用自已的深拷贝解决。

深拷贝：

```c++
Student (const Student &student)
{
    this->m_strName=student.m_strName;
    this->m_dID=new int(*student.m_dID);
}
```

> ==总结：如果属性有在堆区开辟的，一定要自己提供拷贝构造函数，防止浅拷贝带来的问题==

##### 6、初始化列表

**作用：**

C++提供了初始化列表语法，用来初始化属性

**语法：**

`构造函数()：属性1(值1),属性2（值2）... {}`

```c++
string m_strName;
int m_dID;
Student(string name,int id):m_strName(move(name)),m_dID(id)
{

}
```

##### 7、类对象作为类成员

```c++
class A {}
class B
{
    A a；
}
```

![](https://pic.imgdb.cn/item/62de924df54cd3f9372211d3.png)

- 当类中成员是其他类对象时，我们称该成员为 对象成员   
- 构造的顺序是 ：先调用对象成员的构造，再调用本类构造    
- 析构顺序与构造相反

##### 8、静态成员

- 静态变量
  - 所有对象共享同一份数据
  - 在编译阶段分配内存
  - 类内声明，类外初始化
- 静态函数
  - 所有对象共享同一个函数
  - 静态函数只能访问静态成员变量

`静态变量`

1. 类内声明，类外定义

   ```c++
   class CPerson
   {
   public:
       static int m_dShare;
   };
   
   int CPerson::m_dShare=10;  //分配内存
   int main()
   {
       CPerson cPerson;
       cout<<CPerson::m_dShare<<endl;
       return 0;
   }
   ```

2. 访问方式

   - 对象访问

     > ```c++
     > CPerson cPerson;
     > cout<<cPerson.m_dShare<<endl;
     > ```

   - 类名访问

     > ```c++
     > cout<<CPerson::m_dShare<<endl;
     > ```

`静态函数`

1. 静态函数只能访问静态成员

   ![](https://pic.imgdb.cn/item/62dea54ff54cd3f937998297.png)



### 3、对象模型与拷贝<a id="1.3">💚</a>

#### 1、对象模型

##### 1、成员变量和成员函数分开存储

> 空对象占用**1**字节空间，独一无二的空间

> **==只有非静态成员变量属于对象==**

#### 2、深拷贝和浅拷贝

`浅拷贝`：简单的赋值拷贝操作

`深拷贝`：在堆区重新申请空间，进行拷贝操作

> 浅拷贝问题：堆区的内存被重复释放。
>
> 利用自已的深拷贝解决。

深拷贝：

```c++
Student (const Student &student)
{
    this->m_strName=student.m_strName;
    this->m_dID=new int(*student.m_dID);
}
```

> ==总结：如果属性有在堆区开辟的，一定要自己提供拷贝构造函数，防止浅拷贝带来的问题==



### 4、this指针<a id="1.4">💚</a>

#### 1、this指针

 每一个非静态成员函数只会诞生一份函数实例，也就是说**多个同类型的对象会共用一块代码**

那么问题是：这一块代码是如何区分那个对象调用自己的呢？

​    c++通过提供特殊的对象指针，this指针，解决上述问题。**this指针指向被调用的成员函数所属的对象**

​    this指针是**隐含**每一个非静态成员函数内的一种指针

​    this指针**不需要定义**，直接使用即可

​    this指针的用途：

- 当形参和成员变量同名时，可用this指针来区分

  ```c++
  CPerson(int id,string name)
  {
      this->m_dID=id;
      this->m_strName=name;
  }
  ```

- 在类的非静态成员函数中返回对象本身，可使用return *this

  - 返回值

    ![](https://pic.imgdb.cn/item/62dff3e6f54cd3f9375541de.png)

  - **返回引用**

    ![](https://pic.imgdb.cn/item/62dff45ff54cd3f93758f72f.png)

#### 2、空指针调用成员函数

![](https://pic.imgdb.cn/item/62dff569f54cd3f93760d4a8.png)

空指针调用`this`报错

#### 3、const修饰成员函数

**常函数：**

- 成员函数后加const后我们称为这个函数为**常函数**

  ```c++
  void ShowName() const
  {
      cout<<this->m_strName<<endl;
  }
  ```

- 常函数内不可以修改成员属性

  ![](https://pic.imgdb.cn/item/62dff74bf54cd3f93772419e.png)

- 成员属性声明时加关键字mutable后，在常函数中依然可以修改

  ```c++
  mutable int m_dID;
  string m_strName;
  void ShowName() const
  {
      this->m_dID=20;
      cout<<this->m_strName<<endl;
  }
  ```

  <img src="https://pic.imgdb.cn/item/62dff7e3f54cd3f93778ed9d.png" style="zoom:67%;" />

**常对象：**

- 声明对象前加const称该对象为常对象

  ![](https://pic.imgdb.cn/item/62dff874f54cd3f9377eb439.png)

- 常对象只能调用常函数

  <img src="https://pic.imgdb.cn/item/62dff8eaf54cd3f93783540b.png" style="zoom:67%;" />



### 5、友元<a id="1.5">💚</a>



### 6、运算符重载<a id="1.6">💚</a>

### 7、继承<a id="1.7">💚</a>

### 8、多态<a id="1.8">💚</a>

### 9、虚函数|抽象类<a id="1.9">💚</a>

### 10、<a id="1.10">💚</a>

### 11、<a id="1.11">💚</a>

### 12、<a id="1.12">💚</a>

---

[<!--返回目录-->](#1)

[<!--返回总目录-->](#0)

**[README]()**