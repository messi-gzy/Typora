# C++基础（2）

<a id="0">`目录`</a>

- $\textcolor{#e18a3b}{【一】}$**[内存分区](#1)**
- $\textcolor{#e18a3b}{【二】}$**[引用](#2)**
- $\textcolor{#e18a3b}{【三】}$**[函数中级](#3)**
- $\textcolor{#e18a3b}{【四】}$**[类和对象](#4)**

## 一、内存分区

<a id="1"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [代码区](#1.1)
- $\textcolor{#2a6e3f}{【2】}$ [全局区](#1.2)
- $\textcolor{#2a6e3f}{【3】}$ [栈区](#1.3)
- $\textcolor{#2a6e3f}{【4】}$ [堆区](#1.4)

### 1、代码区<a id="1.1">💚</a>

存放函数体的二进制代码，由操作系统的进行管理

- 共享
- 只读

### 2、全局区<a id="1.2">💚</a>

存放全局变量和静态变量以及常量。

- 全局变量
- 静态常量
- 常量区

1. 字符串常量
2. const 修饰的变量

<!--数据由操作系统释放-->

### 3、栈区<a id="1.3">💚</a>

由编译器自动分配释放，存放函数的参数值、局部变量等。

<!--编译器由编译器管理和开辟-->

> 函数参数和局部变量等，在生命周期期间结束后自动释放

### 4、堆区<a id="1.4">💚</a>

由程序员分配和释放。

<!--由开发者管理操作，需要自已释放-->

`开辟数据`

$\textcolor{red}{new}$ <-->$\textcolor{red}{delete}$

获取和释放堆内存

[内存分区详细内容:airplane:](../../../DailyNotes/day_2.md)

[<!--返回目录-->](#1)

## 二、引用

<a id="2"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [定义](#2.1)
- $\textcolor{#2a6e3f}{【2】}$ [注意事项](#2.2)
- $\textcolor{#2a6e3f}{【3】}$ [函数参数](#2.3)
- $\textcolor{#2a6e3f}{【4】}$ [函数返回值](#2.4)
- $\textcolor{#2a6e3f}{【5】}$ [引用的本质](#2.5)
- $\textcolor{#2a6e3f}{【6】}$ [常量引用](#2.6)

### 1、定义<a id="2.1">💛</a>

`给变量起别名`

数据类型 &别名 = 原名

```cpp
int a=10;
int &b=a;
b=20;
cout<<a<<endl;// 20
```

### 2、注意事项<a id="2.2">💛</a>

|     引用     |     指针     |
| :----------: | :----------: |
|  必须初始化  | 可以不初始化 |
|   不能为空   |   可以为空   |
| 不能更换目标 | 可以更换目标 |

##### 1、引用必须初始化

<img src="https://pic.imgdb.cn/item/62c597f75be16ec74a80f714.png" style="zoom:67%;" />

##### 2、不可以更改

**<mark>初始化后不可以再更改为其他的引用</mark>**

<img src="https://pic.imgdb.cn/item/62c598895be16ec74a81ca92.png" style="zoom: 67%;" />

### 3、函数参数<a id="2.3">💛</a>

```cpp
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

### 4、函数返回值<a id="2.4">💛</a>

##### 1、不可以返回局部变量的引用

![](https://pic.imgdb.cn/item/62c6f3fef54cd3f93703d0dc.png)

##### 2、引用可以作为左值

```cpp
int &Swap() {
    static int a = 10;
    return a;
}

int main(int argc, char const *argv[]) {
    int a = 10, c = 30;
    int &x = Swap();
    cout << x << endl; //  10
    Swap() = 100;
    cout << x << endl; // 100
    return 0;
}
```

### 5、引用的本质<a id="2.5">💛</a>

> int &ref=a; ------->int * const ref=&a;(指针常量)
>

指向的值可以改，指针指向不可以改。

### 6、常量引用<a id="2.6">💛</a>

![](https://pic.imgdb.cn/item/62c6f9faf54cd3f9370c6c1b.png)

![](https://pic.imgdb.cn/item/62c6fa6ff54cd3f9370d119b.png)

`值传递会占用多余内存，常量引用防止误操作`

[<!--返回目录-->](#2)

## 三、函数中级

<a id="3"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [带默认参数](#3.1)
- $\textcolor{#2a6e3f}{【2】}$ [函数占位参数](#3.2)
- $\textcolor{#2a6e3f}{【3】}$ [内联函数](#3.3)
- $\textcolor{#2a6e3f}{【4】}$ [函数重载](#3.4)

### 1、带默认参数<a id="3.1">💙</a>

1. 如果传参就用所传的参数

2. 传参数从左往右（第一个之后必须都得有默认参数）

   <img src="https://pic.imgdb.cn/item/62c824b4f54cd3f93755da7a.png" style="zoom:67%;" />

3. 形参必须从右往左

4. **缺省参数不能同时在声明和实现中出现**

   <img src="https://pic.imgdb.cn/item/62c8250bf54cd3f9375666d7.png" style="zoom:67%;" />

### 2、函数占位参数<a id="3.2">💙</a>

```cpp
void func(int a,int,int )
{

}
int main() {
    func(10,10,10);
    return 0;
}
```

### 3、内联函数<a id="3.3">💙</a>



### 4、函数重载<a id="3.4">💙</a>

`函数名可以相同，提高复用性`

##### 1、条件

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

##### 2、注意事项

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

---

[<!--返回目录-->](#3)

[<!--返回总目录-->](#0)

[返回上一页](../../README.md)

