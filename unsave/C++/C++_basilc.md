# C++ 基础

---

## 一、目录

---

## 二、基础

---

### 1、数据类型

#### 1、sizeof

查看占用内存大小

```c++
int a=10;
cout<<sizeof(a)<<endl;
```

#### 2、char

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

#### 3、转义字符

| 转移字符                 | 含义 |
| ------------------------ | ---- |
| 换行                     | \n   |
| 反斜杠                   | \\\  |
| 水平制表符(整齐输出数据) | \t   |
| 警示音                   | \a   |
| 回车                     | \r   |

#### 4、字符串型

##### 1、C语言

```c++
char a[]="hello world!";//双引号 (数组形式)
cout<<a<<endl;
```

##### 2、C++ 

`string 变量名 = "......"`

```c++
string a="hello world!";
cout<<a<<endl;
```

---

#### 5、运算符

##### 	1、算术运算符

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

##### 	2、赋值运算符

| 运算符 | 术语   | 示例      | 结果     |
| ------ | ------ | --------- | -------- |
| =      | 赋值   | a=2;b=3;  | a=2;b=3; |
| +=     | 加等于 | a=0;a+=2; | a=2;     |
| -=     | 减等于 | a=5;a-=3; | a=2;     |
| *=     | 乘等于 | a=2;a*=2  | a=4;     |
| /=     | 除等于 | a=4;a/=2; | a=2      |
| %=     | 模等于 | a=3;a%=2; | a=1;     |

##### 	3、三目运算符

a和b 比较 谁大返回谁

```c++
int a=10,b=20,c;
c = a > b ? a:b;
cout<<c<<endl; // c=20
```

---

### 2、程序流程

#### 1、goto语句

`跳转语句`

```c++
int a=10,b=20;
goto FLAG;
a=30;
FLAG:
cout<<a<<endl; //a=10
```

---

### 3、数组

`内存中连续内存空间`

==数组名也是首地址==

#### 1、一维数组

##### 	1、定义

```c++
int a[10];
int b[10]={0,0};
int c[]={1,1};
```

##### 	2、内存空间

```c++
int ing[10];
cout<<sizeof(ing)<<endl;
```

##### 	3、数组长度

```c++
int ing[10];
cout<<sizeof(ing)/sizeof(ing[0])<<endl;
```

##### 	4、首地址

```c++
cout<<ing<<endl;
cout<<(long long)ing<<endl;
```

---

#### 2、二维数组

##### 	1、定义

```c++
int a[10][10];
int b[10][10]={{0,0},{1,1,1}};
int c[10][10]={0,0,0};
int d[][10]={0,1,2,3};
```

##### 	2、内存空间

```C++
cout<<a<<"  "<< sizeof(a)<<endl;
```

---

### 4、函数

#### 1、声明

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

### 5、指针

`指针间接访问内存`

`通过指针保存一个地址`

#### 1、定义

==指针数据类型与原变量类型一致==

```C++
int a=10;
int *p;
p=&a;
```

##### 	1、地址

`&a`   `p`

##### 	2、值

`*p`

##### 	3、内存

指针大小为4字节（32位）

​					8字节（64位）

---

#### 2、空指针

###### 	1、初始化

```c++
int *p=NULL;
```

##### 	2、访问权限

无访问权限，越界访问

#### 3、野指针

```c++
int *p=(int *)0x1100;
```

---

#### 4、***const***修饰指针

##### 1、常量指针

> 指针指向可以改，指向的值不可以改
>
> const int *p=&a;

![](https://pic.imgdb.cn/item/62c4459e5be16ec74a11e74b.png)

---

##### 2、指针常量

> 指针的指向不可以改，指向的值可以改
>
> int  * const  p=&a;

![](https://pic.imgdb.cn/item/62c447f25be16ec74a157ac1.png)

---

##### 3、即修饰指针也修饰常量

> 指针的指向不可以改，指向的值也不可以改
>
> const int * const p =&a;

![](https://pic.imgdb.cn/item/62c447985be16ec74a14f0ff.png)

---

#### 5、指针和数组

`指针指向数组首地址，通过++实现数组往后移`

##### 1、定义

```c++
int arr[10]={1,2,3};
int *p=arr;
cout<<++*p<<endl;// 2
```

##### 2、动态数组

```c++
int *a=new int[10];//申请空间
*a=10;
a[1]=20;
cout<<a[0]<<endl;
delete []a;//释放空间
```

---

#### 6、指针和函数

![](https://pic.imgdb.cn/item/62c451815be16ec74a235b91.png)

---

### 6、结构体

#### 1、定义

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

#### 2、创建

- struct Student s1;

> s1.m_name
>
> s1.m_age;

- struct Student s2 = {18,"aaa",23.5};

> 赋初值

- 在定义结构体时就创建结构体变量

> <img src="https://pic.imgdb.cn/item/62c4f10f5be16ec74ab07acd.png" style="zoom:67%;" />

---

#### 3、结构体数组

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

#### 4、结构体指针

> $\textcolor{red}{利用操作符}$`->` $\textcolor{red}{访问内容}$

```c++
Student s1={21,"小王",98.66};
Student *p=&s1;
cout<<p->m_name<<endl;
```

---

#### 5、结构体嵌套结构体

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

#### 6、结构体做函数参数

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

#### 7、结构体中 *const* 使用

![](https://pic.imgdb.cn/item/62c509fb5be16ec74acc2106.png)

> 减少拷贝，减少内存开销，只读不可以修改

---


