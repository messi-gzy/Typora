---
typora-root-url: ./..
---

# C++基础（1）

<a id="0">`目录`</a>

- $\textcolor{#e18a3b}{【一】}$**[数据类型](#1)**
- $\textcolor{#e18a3b}{【二】}$**[程序流程](#2)**
- $\textcolor{#e18a3b}{【三】}$**[数组](#3)**
- $\textcolor{#e18a3b}{【四】}$**[函数初级](#4)**
- $\textcolor{#e18a3b}{【五】}$**[指针初级](#5)**
- $\textcolor{#e18a3b}{【六】}$**[结构体](#6)**

> C++ 是一种静态类型的、编译式的、通用的、大小写敏感的、不规则的编程语言，支持过程化编程、面向对象编程和泛型编程。
>
> 标准库：
>
> - 核心语言，提供了所有构件块，包括变量、数据类型和常量，等等。
> - C++ 标准库，提供了大量的函数，用于操作文件、字符串等。
> - 标准模板库（STL），提供了大量的方法，用于操作数据结构等。

## 一、数据类型

<a id="1"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [sizeof](#1.1)
- $\textcolor{#2a6e3f}{【2】}$ [typedef](#1.2)
- $\textcolor{#2a6e3f}{【3】}$ [基本数据](#1.3)
- $\textcolor{#2a6e3f}{【4】}$ [变量作用域](#1.4)
- $\textcolor{#2a6e3f}{【5】}$ [存储字](#1.5)
- $\textcolor{#2a6e3f}{【6】}$ [运算符](#1.6)

### 1、sizeof<a id="1.1">💚</a>

#### 1.1、基本数据类型

|     类型     | 关键字 |
| :----------: | :----: |
|    布尔型    |  bool  |
|    字符型    |  char  |
|     整型     |  int   |
|    浮点型    | float  |
| 双精度浮点型 | double |
|    无类型    |  void  |

#### 1.2、sizeof

<mark>**可以获取各数据类型在内存中所占的字节数**</mark>

`举例`

```cpp
cout << sizeof(int) << endl;    // 4
cout << sizeof(char) << endl;   // 1
cout << sizeof(bool) << endl;   // 1
cout << sizeof(long) << endl;   // 8
cout << sizeof(float) << endl;  // 4
cout << sizeof(double) << endl; // 8
```

`注意`

指针变量的大小与指向对象无关，和计算机内部地址总线相关。

```cpp
int a = 10;
int *p = &a;
cout << sizeof(p) << endl; // 8
long b = 10;
long *p_l = &b;
cout << sizeof(p_l) << endl; // 8
```

`其他基本数据类型所占内存空间`

![](https://s1.ax1x.com/2022/10/25/xRoMAH.png)

### 2、typedef<a id="1.2">💚</a>

**<mark>*typedef*</mark>为一个已有的类型取一个新的名字**

`格式`

typedef + [type] +[new_name]

`举例`

```cpp
typedef int new_int;
new_int a = 20;
cout << sizeof(new_int) << endl; // 4
```

### 3、基础数据<a id="1.3">💚</a>

#### 3.1、char

单个字符（使用单引号引用）（只能放单个字符）

~~不可用双引号~~

`举例`

```c++
char a = 'a';
cout << a << "\t" << sizeof(a) << endl; // a    1
cout << (int)a << endl;                 // 97
```

###### ASCll码表格

<img src="https://pic.imgdb.cn/item/62c2e1ca5be16ec74a7e08f4.png" style="zoom:67%;" />

#### 3.2、字符串型

###### 1、C语言

```c++
char c_char[]="hello world";//双引号 (数组形式)
printf("%s\n",c_char);
```

###### 2、C++

`string 变量名 = "......"`

```c++
string a="hello world!";
cout<<a<<endl;
```

### 4、变量作用域<a id="1.4">💚</a>

- <mark>局部变量</mark>：在**函数或一个代码块内部声明**的变量，它们**只能被函数内部或者代码块内部**的语句使用

- <mark>形参变量</mark>：在**函数参数的定义**中声明的变量。

- <mark>全局变量</mark>：在所有函数外部声明的变量。全局变量的值在程序的整个生命周期内都是有效的。

  全局变量可以被任何函数访问。也就是说，全局变量一旦声明，在整个程序中都是可用的。

- <mark>**当局部变量被定义时，系统不会对其初始化，您必须自行对其初始化。定义全局变量时，系统会自动初始化值**</mark>

`转义字符`

| 转移字符                 | 含义 |
| ------------------------ | ---- |
| 换行                     | \n   |
| 反斜杠                   | \\\  |
| 水平制表符(整齐输出数据) | \t   |
| 警示音                   | \a   |
| 回车                     | \r   |

### 5、存储类<a id="1.5">💚</a>

存储类定义 C++ 程序中变量/函数的范围**（可见性）和生命周期**。这些说明符放置在它们所修饰的类型之前。

| auto | register | static | extern | mutable | thread_local |
| :--: | :------: | :----: | :----: | :-----: | :----------: |

`注意`

- **从 C++ 17** 开始，**auto** 关键字不再是 C++ 存储类说明符，且 **register** 关键字被弃用。
- **thread_local** 是C++11支持

#### 5.1、auto

自 C++ 11 以来，**auto** 关键字用于两种情况：声明变量时根据初始化表达式自动推断该变量的类型、声明函数时函数返回值的占位符。

```cpp
auto f=3.14;      //double
auto s("hello");  //const char*
auto z = new auto(9); // int*
auto x1 = 5, x2 = 5.0, x3='r';//错误，必须是初始化为同一类型


auto a = 10;
cout << sizeof(a) << endl;        // 4
cout << typeid(a).name() << endl; // i
```

#### 5.2、register

​	**register** 存储类用于定义存储在寄存器中而不是 RAM 中的局部变量。这意味着变量的最大尺寸等于寄存器的大小（通常是一个词），且不能对它应用一元的 '&' 运算符（因为它没有内存位置）。

​	寄存器只用于需要快速访问的变量。

#### 5.3、static

**static** 存储类指示编译器在程序的生命周期内保持局部变量的存在，而不需要在每次它进入和离开作用域时进行创建和销毁。因此，使用 static 修饰局部变量可以在函数调用之间保持局部变量的值。

static 修饰符也可以应用于全局变量。当 static 修饰全局变量时，会使变量的作用域限制在声明它的文件内。

#### 5.4、extern

**extern** 存储类用于提供一个全局变量的引用，全局变量对所有的程序文件都是可见的。当您使用 'extern' 时，对于无法初始化的变量，会把变量名指向一个之前定义过的存储位置。

`举例`

```cpp
// test.cpp
int test = 20;

// main.cpp
extern int test;

int main(int argc, char *argv[])
{
    cout << test << endl;// 20
    return 0;
}
```

#### 5.5、thread_local 

使用 thread_local 说明符声明的变量仅可在它在其上创建的线程上访问。 变量在创建线程时创建，并在销毁线程时销毁。 每个线程都有其自己的变量副本。

### 6、运算符<a id="1.6">💚</a>

##### 1、算术运算符

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

##### 2、赋值运算符

| 运算符 | 术语   | 示例      | 结果     |
| ------ | ------ | --------- | -------- |
| =      | 赋值   | a=2;b=3;  | a=2;b=3; |
| +=     | 加等于 | a=0;a+=2; | a=2;     |
| -=     | 减等于 | a=5;a-=3; | a=2;     |
| *=     | 乘等于 | a=2;a*=2  | a=4;     |
| /=     | 除等于 | a=4;a/=2; | a=2      |
| %=     | 模等于 | a=3;a%=2; | a=1;     |

##### 3、三目运算符

a和b 比较 谁大返回谁

```c++
int a=10,b=20,c;
c = a > b ? a:b;
cout<<c<<endl; // c=20
```

---

[<!--返回目录-->](#1)

## 二、程序流程

<a id="2"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [goto](#2.1)
- $\textcolor{#2a6e3f}{【2】}$ [while](#2.2)
- $\textcolor{#2a6e3f}{【3】}$ [for](#2.3)
- $\textcolor{#2a6e3f}{【4】}$ [switch](#2.4)

### 1、goto<a id="2.1">💛</a>

`跳转语句`

```c++
int a=10,b=20;
goto FLAG;
a=30;
FLAG:
cout<<a<<endl; //a=10
```

### 2、while<a id="2.2">💛</a>

```cpp
while(condition)
{
   statement(s);// 语句体
}
```

**condition** 可以是任意的表达式，当为任意非零值时都为真。

- 当条件为真时执行循环。

- 当条件为假时，程序流将继续执行紧接着循环的下一条语句。

### 3、for<a id="2.3">💛</a>

```cpp
for ( init; condition; increment )
{
   statement(s);// 语句体
}
```

下面是 for 循环的控制流：

1. **init** 会首先被执行，且只会执行一次。这一步允许您声明并初始化任何循环控制变量。您也可以不在这里写任何语句，只要有一个分号出现即可。
2. 接下来，会判断 **condition**。如果为真，则执行循环主体。如果为假，则不执行循环主体，且控制流会跳转到紧接着 for 循环的下一条语句。
3. 在执行完 for 循环主体后，控制流会跳回上面的 **increment** 语句。该语句允许您更新循环控制变量。该语句可以留空，只要在条件后有一个分号出现即可。
4. 条件再次被判断。如果为真，则执行循环，这个过程会不断重复（循环主体，然后增加步值，再然后重新判断条件）。在条件变为假时，for 循环终止。

### 4、switch<a id="2.4">💛</a>

- **首先计算出表达式的值**
- 和case依次比较，一旦有对应的值，就会执行相应的语句，在执行的过程中，**遇到`break`就会结束。**
- **如果所有的case都和表达式的值不匹配，就会执行default语句体部分**，然后程序结束掉。

```java
switch (n) {
    case 1:
        语句1;
        break;
    case 2:
        语句2;
        break;
    case 3:
        语句3;
        break;
    case 4:
        语句4;
        break;
    default:
        默认语句
        break;
}
```

<img src="https://pic.imgdb.cn/item/632881bb16f2c2beb1eb5f3c.png" style="zoom:67%;" />

<!--注意-->

- 表达式类型
  
  - 支持 `byte`、`short`、`int`、`char`、`string`、`枚举`
  
  - 不支持 ~~`double`、`float`、`long`~~

- case给出的值不允许重复，==只能为字面量，不可为常量==

- ==**注意 `break`，防止循环穿透**==

[<!--返回目录-->](#2)

## 三、数组

`内存中连续内存空间`

==数组名也是首地址==

<a id="3"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [一维数组](#3.1)
- $\textcolor{#2a6e3f}{【2】}$ [多维数组](#3.2)

### 1、一维数组<a id="3.1">💙</a>

##### 1、定义

```c++
int a[10];
int b[10]={0,0};
int c[]={1,1};
```

##### 2、内存空间

```c++
int ing[10];
cout<<sizeof(ing)<<endl;
```

##### 3、数组长度

```c++
int ing[10];
cout<<sizeof(ing)/sizeof(ing[0])<<endl;
```

##### 4、首地址

```c++
cout<<ing<<endl;
cout<<(long long)ing<<endl;
```

### 2、多维数组<a id="3.2">💙</a>

##### 1、定义

```c++
int a[10][10];
int b[10][10]={{0,0},{1,1,1}};
int c[10][10]={0,0,0};
int d[][10]={0,1,2,3};
```

##### 2、内存空间

```C++
cout<<a<<"\t"<< sizeof(a)<<endl;
```

---

[<!--返回目录-->](#3)

## 四、函数初级

<a id="4"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [声明](#4.1)
- $\textcolor{#2a6e3f}{【2】}$ [使用](#4.2)

### 1、声明<a id="4.1">💜</a>

```cpp
//函数声明
int compere(int a,int b);
//函数定义
int compere(int a,int b)
{
    return a > b ? a : b;
}
```

### 2、使用<a id="4.2">💜</a>

```cpp
cout << compere(2,4) << endl;
```

---

[<!--返回目录-->](#4)

## 五、指针初级

​        <a id="5"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [定义](#5.1)
- $\textcolor{#2a6e3f}{【2】}$ [空指针](#5.2)
- $\textcolor{#2a6e3f}{【3】}$ [野指针](#5.3)
- $\textcolor{#2a6e3f}{【4】}$ [const修饰指针](#5.4)
- $\textcolor{#2a6e3f}{【5】}$ [指针和数组](#5.5)
- $\textcolor{#2a6e3f}{【6】}$ [指针和函数](#5.6)

### 1、定义<a id="5.1">❤</a>

`指针间接访问内存`

`通过指针保存一个地址`

==指针数据类型与原变量类型一致==

```C++
int a=10;
int *p;
p=&a;
```

<!--地址-->

`&a`   `p`

<!--值-->

`*p`

<!--内存-->

指针大小为4字节（32位）

​                    8字节（64位）

### 2、空指针<a id="5.2">❤</a>

##### 1、初始化

```c++
int *p=NULL;
```

##### 2、访问权限

无访问权限，越界访问

### 3、野指针<a id="5.3">❤</a>

指向的内存地址是未知的，操作系统不允许操作此内存。

```cpp
int *p=(int *)0x7fff160addc0;//赋值了任意数，没有意义
```

`注意`

- 野指针本身不会错误
- 操作野指针会发生错误

### 4、const修饰指针<a id="5.4">❤</a>

##### 1、常量指针

> 指针指向可以改，指向的值不可以改
>
> const int *p=&a;

![](https://pic.imgdb.cn/item/62c4459e5be16ec74a11e74b.png)

##### 2、指针常量

> 指针的指向不可以改，指向的值可以改
>
> int  * const  p=&a;

![](https://pic.imgdb.cn/item/62c447f25be16ec74a157ac1.png)

##### 3、即修饰指针也修饰常量

> 指针的指向不可以改，指向的值也不可以改
>
> const int * const p =&a;

![](https://pic.imgdb.cn/item/62c447985be16ec74a14f0ff.png)

### 5、指针和数组<a id="5.5">❤</a>

`指针指向数组首地址，通过++实现数组往后移`

##### 1、定义

```c++
int arr[10]={1,2,3};
int *p=arr;
cout<<*++p<<endl;// 2
```

##### 2、动态数组

```c++
int *a=new int[10];//申请空间
*a=10;
a[1]=20;
cout<<a[0]<<endl;
delete []a;//释放空间
```

### 6、指针和函数<a id="5.6">❤</a>

<img src="https://pic.imgdb.cn/item/62c451815be16ec74a235b91.png" style="zoom: 67%;" />

---

[<!--返回目录-->](#5)

## 六、结构体

<a id="6"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [定义和创建](#6.1)
- $\textcolor{#2a6e3f}{【2】}$ [结构体数组](#6.2)
- $\textcolor{#2a6e3f}{【3】}$ [结构体指针](#6.3)
- $\textcolor{#2a6e3f}{【4】}$ [结构体嵌套结构体](#6.4)
- $\textcolor{#2a6e3f}{【5】}$ [结构体做函数参数](#6.5)
- $\textcolor{#2a6e3f}{【6】}$ [结构体中的const](#6.6)

### 1、定义和创建<a id="6.1">💗</a>

#### 1.1、定义

`一些类型组合成的一个类型`

==C++中可以省略***struct***关键字==

`定义`：

```c++
struct Student
{
 int m_age;
 string m_name;
 double m_score;
};
```

#### 1.2、创建

- struct Student s1;

```cpp
s1.m_name

s1.m_age;
```

`创建并赋初值`

- struct Student s2 = {18,"aaa",23.5};

在定义结构体时就创建结构体变量

<img src="https://pic.imgdb.cn/item/62c4f10f5be16ec74ab07acd.png" style="zoom:67%;" />

### 2、结构体数组<a id="6.2">💗</a>

```cpp
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

### 3、结构体指针<a id="6.3">💗</a>

> $\textcolor{red}{利用操作符}$`->` $\textcolor{red}{访问内容}$

```c++
Student s1={21,"小王",98.66};
Student *p=&s1;
cout<<p->m_name<<endl;
```

### 4、结构体嵌套结构体<a id="6.4">💗</a>

```cpp
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

### 5、结构体做函数参数<a id="6.5">💗</a>

```cpp
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

### 6、结构体中的const<a id="6.6">💗</a>

![](https://pic.imgdb.cn/item/62c509fb5be16ec74acc2106.png)

> 减少拷贝，减少内存开销，只读不可以修改

---

[<!--返回目录-->](#6)

[<!--返回总目录-->](#0)

[返回上一页](../../README.md)

