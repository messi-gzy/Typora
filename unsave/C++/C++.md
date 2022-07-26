# C++

---

## 一、目录

---

## 二、基础

---

#### 1、数据类型

##### 1、sizeof

查看占用内存大小

```c++
int a=10;
cout<<sizeof(a)<<endl;
```

##### 2、char

单个字符（使用单引号引用）（只能放单个字符）

~~不可用双引号~~

```c++
char a='a';
cout<<a<<"\t"<<sizeof(a)<<endl;
cout<<(int)a<<endl;
```

###### ASCll码表格

<img src="https://pic.imgdb.cn/item/62c2e1ca5be16ec74a7e08f4.png"  />

---

##### 3、转义字符

| 转移字符                 | 含义 |
| ------------------------ | ---- |
| 换行                     | \n   |
| 反斜杠                   | \\\  |
| 水平制表符(整齐输出数据) | \t   |
| 警示音                   | \a   |
| 回车                     | \r   |

##### 4、字符串型

###### 1、C语言

```c++
char a[]="hello world!";//双引号 (数组形式)
cout<<a<<endl;
```

###### 2、C++ 

`string 变量名 = "......"`

```c++
string a="hello world!";
cout<<a<<endl;
```

---

##### 5、运算符

###### 	1、算术运算符

- ++a /--a  `先自身++/--，再表达式运算`

  ```c++
  int a=10;
  int b=a++ * 10; //a=11  b=100
  ```

- a++ / a-- `先表达式运算，再自身++/--`

  ```c++
  int a=10;
  int b=++a * 10; //a=11  b=110
  ```

###### 	2、赋值运算符

| 运算符 | 术语   | 示例      | 结果     |
| ------ | ------ | --------- | -------- |
| =      | 赋值   | a=2;b=3;  | a=2;b=3; |
| +=     | 加等于 | a=0;a+=2; | a=2;     |
| -=     | 减等于 | a=5;a-=3; | a=2;     |
| *=     | 乘等于 | a=2;a*=2  | a=4;     |
| /=     | 除等于 | a=4;a/=2; | a=2      |
| %=     | 模等于 | a=3;a%=2; | a=1;     |

###### 	3、三目运算符

a和b 比较 谁大返回谁

```c++
int a=10,b=20,c;
c = a > b ? a:b;
cout<<c<<endl; // c=20
```

---

#### 2、程序流程

##### 1、goto语句

`跳转语句`

```c++
int a=10,b=20;
goto FLAG;
a=30;
FLAG:
cout<<a<<endl; //a=10
```

---

#### 3、数组

`内存中连续内存空间`

==数组名也是首地址==

##### 1、一维数组

###### 	1、定义

```c++
int a[10];
int b[10]={0,0};
int c[]={1,1};
```

###### 	2、内存空间

```c++
int ing[10];
cout<<sizeof(ing)<<endl;
```

###### 	3、数组长度

```c++
int ing[10];
cout<<sizeof(ing)/sizeof(ing[0])<<endl;
```

###### 	4、首地址

```c++
cout<<ing<<endl;
cout<<(long long)ing<<endl;
```

---

##### 2、二维数组

###### 	1、定义

```c++
int a[10][10];
int b[10][10]={{0,0},{1,1,1}};
int c[10][10]={0,0,0};
int d[][10]={0,1,2,3};
```

###### 	2、内存空间

```C++
cout<<a<<"  "<< sizeof(a)<<endl;
```

---

#### 4、函数

##### 1、声明

```c++
//函数声明
int compere(int a,int b);
//函数定义
int compere(int a,int b)
{
    return a > b ? a : b;
}
```

`声明可多次，定义就一次`

---

#### 5、指针

`指针间接访问内存`

`通过指针保存一个地址`

##### 1、定义

==指针数据类型与原变量类型一致==

```C++
int a=10;
int *p;
p=&a;
```

###### 	1、地址

`&a`   `p`

###### 	2、值

`*p`

###### 	3、内存

指针大小为4字节（32位）

​					8字节（64位）

---

##### 2、空指针

###### 	1、初始化

```c++
int *p=NULL;
```

###### 	2、访问权限

无访问权限，越界访问

##### 3、野指针

```c++
int *p=(int *)0x1100;
```

---

##### 4、***const***修饰指针

###### 1、常量指针

> 指针指向可以改，指向的值不可以改
>
> const int *p=&a;

![](https://pic.imgdb.cn/item/62c4459e5be16ec74a11e74b.png)

---

###### 2、指针常量

> 指针的指向不可以改，指向的值可以改
>
> int  * const  p=&a;

![](https://pic.imgdb.cn/item/62c447f25be16ec74a157ac1.png)

---

###### 3、即修饰指针也修饰常量

> 指针的指向不可以改，指向的值也不可以改
>
> const int * const p =&a;

![](https://pic.imgdb.cn/item/62c447985be16ec74a14f0ff.png)

---

##### 5、指针和数组

`指针指向数组首地址，通过++实现数组往后移`

###### 1、定义

```c++
int arr[10]={1,2,3};
int *p=arr;
cout<<++*p<<endl;// 2
```

###### 2、动态数组

```c++
int *a=new int[10];//申请空间
*a=10;
a[1]=20;
cout<<a[0]<<endl;
delete []a;//释放空间
```

---

##### 6、指针和函数

![](https://pic.imgdb.cn/item/62c451815be16ec74a235b91.png)

---

#### 6、结构体

##### 1、定义

`一些类型组合成的一个类型`

> #### **$\textcolor{blue}{结构体}$**
>
> ==C++中可以省略***struct***关键字==
>
> 定义：
>
> ```c++
> struct Student
> {
>     int m_age;
>     string m_name;
>     double m_score;
> };
> ```

---

##### 2、创建

- struct Student s1;

> s1.m_name
>
> s1.m_age;

- struct Student s2 = {18,"aaa",23.5};

> 赋初值

- 在定义结构体时就创建结构体变量

> <img src="https://pic.imgdb.cn/item/62c4f10f5be16ec74ab07acd.png" style="zoom:67%;" />

---

##### 3、结构体数组

```c++
struct Student
{
    int m_age;
    string m_name;
    double m_score;
};

int main() {
    struct Student student[5]
    {
        {18,"aaa",98.5},
        {19,"bbb",98.5},
        {20,"ccc",98.5}
    };
    for(int i=0;i<sizeof(student)/ sizeof(student[0]);i++)
    {
        cout<<student[i].m_name<<endl;
    }
    return 0;
}
```

---

##### 4、结构体指针

> $\textcolor{red}{利用操作符}$`->` $\textcolor{red}{访问内容}$

```c++
Student s1={21,"小王",98.66};
Student *p=&s1;
cout<<p->m_name<<endl;
```

---

##### 5、结构体嵌套结构体

```c++
struct Student
{
    int m_age;
    string m_name;
};
struct Teacher
{
    int m_age;
    string m_name;
    double m_score;
    struct Student student;
};
int main() {
    Teacher teacher={21,"maxin",98.0,{12,"gzy"}};
    cout<<teacher.student.m_name<<"\t"<<teacher.m_name<<endl;
    return 0;
}
```

---

##### 6、结构体做函数参数

```c++
void Printf_1(struct Teacher teacher)//值传递
{
    cout<<teacher.student.m_name<<"\t"<<teacher.m_name<<endl;
};
void Printf_2(struct Teacher *teacher)//地址传递
{
    cout<<teacher->student.m_name<<"\t"<<teacher->m_name<<endl;
};

int main() {
    Teacher teacher={21,"maxin",98.0,{12,"gzy"}};
    Printf_1(teacher);
    Printf_2(&teacher);
    return 0;
}
```

---

##### 7、结构体中 *const* 使用

![](https://pic.imgdb.cn/item/62c509fb5be16ec74acc2106.png)

> 减少拷贝，减少内存开销，只读不可以修改

---



## 三、进价

---

#### 1、内存分区

![](https://pic.imgdb.cn/item/62c53b3f5be16ec74a06063a.jpg)

---

##### 1、代码区

- 共享
- 只读

##### 2、全局区

- 全局变量
- 静态常量
- 常量区

1. 字符串常量
2. const 修饰的变量

`数据由操作系统释放`

----

##### 3、栈区

`编译器由编译器管理和开辟`

> 函数参数和局部变量等，在生命周期期间结束后自动释放

##### 4、堆区

`由开发者管理操作，需要自已释放`

###### 1、开辟数据

> ### $\textcolor{red}{new}$<-->$\textcolor{red}{delete\\\free()}$

获取和释放堆内存

---



#### 2、引用

`给变量起别名`

> 数据类型 &别名 = 原名

##### 1、定义

```c++
int a=10;
int &b=a;
b=20;
cout<<a<<endl;
```

---

##### 2、注意事项

| 引用         | 指针         |
| ------------ | ------------ |
| 必须初始化   | 可以不初始化 |
| 不能为空     | 可以为空     |
| 不能更换目标 | 可以更换目标 |

---

###### 1、引用必须初始化

![](https://pic.imgdb.cn/item/62c597f75be16ec74a80f714.png)

---

###### 2、不可以更改

> ### $\textcolor{blue}{初始化后不可以再更改为其他的引用}$

<img src="https://pic.imgdb.cn/item/62c598895be16ec74a81ca92.png" style="zoom: 67%;" />

---

##### 3、做函数参数

```c++
void Swap(int &a,int &b)
{
    int temp=a;
    a=b;
    b=temp;
}

int main() {
    int a=10,c=30;
    Swap(a,c);
    cout<<a<<" "<<c<<endl;
    return 0;
}
```

---

##### 4、函数返回值

###### 1、不可以返回局部变量的引用

![](https://pic.imgdb.cn/item/62c6f3fef54cd3f93703d0dc.png)

###### 2、引用可以作为左值

<img src="https://pic.imgdb.cn/item/62c6f3fef54cd3f93703d0df.png" style="zoom: 50%;" />

---

##### 5、引用的本质

> int &ref=a; ------->int * const ref=&a;(指针常量)
>
> 指向的值可以改，指针指向不可以改。

##### 6、常量引用

![](https://pic.imgdb.cn/item/62c6f9faf54cd3f9370c6c1b.png)

![](https://pic.imgdb.cn/item/62c6fa6ff54cd3f9370d119b.png)

`值传递会占用多余内存，常量引用防止误操作`



#### 3、函数初级

##### 1、带有默认参数的函数

1. 如果传参就用所传的参数

2. 传参数从左往右（第一个之后必须都得有默认参数）

   <img src="https://pic.imgdb.cn/item/62c824b4f54cd3f93755da7a.png" style="zoom:67%;" />

3. 形参必须从右往左

4. **缺省参数不能同时在声明和实现中出现**

   <img src="https://pic.imgdb.cn/item/62c8250bf54cd3f9375666d7.png" style="zoom:67%;" />

> #### $\textcolor{red}{**缺省参数不能同时在声明和实现中出现**}$

##### 2、函数占位参数

```c++
void func(int a,int,int )
{
    
}
int main() {
    func(10,10,10);
    return 0;
}
```

`返回值类型 函数名 （数据类型）{}`

##### 3、内联函数

##### 4、函数重载

`函数名可以相同，提高复用性`

###### 1、条件

- 同一个作用域
- 函数名称相同
- 参数类型不同、个数不同、顺序不同

> #### $\textcolor{red}{函数的返回值不可以作为函数重载的条件}$

```c++
int add(int a,double b)
{}
int add(int a,int b)
{}
```

###### 2、注意事项

1. 引用作为函数重载

   ```c++
   void add(int& a){}
   ----
   int a=10;
   add(a);
   ```

   ```c++
   void add(const int& a){}
   ----
   add(10);
   ```

2. 默认参数

![](https://pic.imgdb.cn/item/62c98ccbf54cd3f93720c883.png)



#### 4、类和对象

面向对象的三大特性 ：`封装`、`继承`、`多态`

##### 1、封装

###### 1、封装的意义

- 将属性和行为作为一个整体，表现生活中的事务
- 将属性和行为加以权限控制

###### 2、实例化对象

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

###### 3、意义

属性：成员变量

行为：成员方法

###### 4、访问权限

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

###### 5、struct和class区别

`struct` 默认 ==公共==（public）

`class`   默认 ==私有== （private）



##### 2、初始化和释放

###### 1、构造函数和析构函数

**构造函数** ：`类名（）{}`

- 与类名相同
- 可以有参数，发生重载
- 自动调用

**析构函数** ： `~类名（）{}`

- ~+类名
- 不可以有参数，不可以重载
- 在对象销毁时自动调用

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

###### 2、构造函数的分类

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
   
   
   Student *student=new Student("a",10);
   delete student;
   ```

3. 隐式转换法

   ```c++
    Person p4 = 10; // Person p4 = Person(10); 
    Person p5 = p4; // Person p5 = Person(p4); 
   ```

==注意：不能利用 拷贝构造函数 初始化匿名对象 编译器认为是对象声明==    //`Student p5(p4);`

###### 3、拷贝构造函数及调用时机

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



###### 4、构造函数调用规则

默认情况下，c++编译器至少给一个类添加3个函数

1．默认构造函数(无参，函数体为空)

2．默认析构函数(无参，函数体为空)

3．默认拷贝构造函数，对属性进行值拷贝

构造函数调用规则如下：

* 如果用户定义有参构造函数，c++不在提供默认无参构造，但是会提供默认拷贝构造

* 如果用户定义拷贝构造函数，c++不会再提供其他构造函数



###### 5、深拷贝和浅拷贝

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



###### 6、初始化列表

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



###### 7、类对象作为类成员

```c++
class A {}
class B
{
    A a；
}
```

![](https://pic.imgdb.cn/item/62de924df54cd3f9372211d3.png)

- 当类中成员是其他类对象时，我们称该成员为 对象成员   
-  构造的顺序是 ：先调用对象成员的构造，再调用本类构造    
- 析构顺序与构造相反



###### 8、静态成员

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



##### 3、对象模型与**this**指针

###### 1、成员变量和成员函数分开存储

> 空对象占用**1**字节空间，独一无二的空间

> **==只有非静态成员变量属于对象==**



###### 2、***this*** 指针

​	每一个非静态成员函数只会诞生一份函数实例，也就是说**多个同类型的对象会共用一块代码**

那么问题是：这一块代码是如何区分那个对象调用自己的呢？

​	c++通过提供特殊的对象指针，this指针，解决上述问题。**this指针指向被调用的成员函数所属的对象**

​	this指针是**隐含**每一个非静态成员函数内的一种指针

​	this指针**不需要定义**，直接使用即可

​	this指针的用途：

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



###### 3、空指针调用成员函数

![](https://pic.imgdb.cn/item/62dff569f54cd3f93760d4a8.png)

空指针调用`this`报错



###### 4、const修饰成员函数

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



##### 4、友元

