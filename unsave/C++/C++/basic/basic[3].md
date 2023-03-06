# C++ 基础 (3)

<a id="0">`目录`</a>

- $\textcolor{#e18a3b}{【一】}$**[字符串](#1)**
- $\textcolor{#e18a3b}{【二】}$**[结构体](#2)**
- $\textcolor{#e18a3b}{【三】}$**[共用体](#3)**
- $\textcolor{#e18a3b}{【四】}$**[内存分区](#4)**

## 一、字符串

<a id="1"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [字符串](#1.1)
- $\textcolor{#2a6e3f}{【2】}$ [C字符串](#1.2)
- $\textcolor{#2a6e3f}{【3】}$ [相关函数](#1.3)
- $\textcolor{#2a6e3f}{【4】}$ [C++字符串](#1.4)
- $\textcolor{#2a6e3f}{【5】}$ [格式转换](#1.5)

### 1、字符串<a id="1.1">💚</a>

> C++ 提供了以下两种类型的字符串表示形式：
>
> - C 风格字符串
> - C++ 引入的 string 类类型

字符串在存储上类似字符数组，一般使用 `""`代表字符串， `''`代表单个字符，严格区分。

---

### 2、C字符串<a id="1.2">💚</a>

1. ​	C 风格的字符串起源于 C 语言，并在 C++ 中继续得到支持。字符串实际上是使用 **`null`** 字符 **`\0`** 终止的一维字符数组。因此，一个以 null 结尾的字符串，包含了组成字符串的字符。
2. ​    C语言没有专门用于存储字符串的变量类型，字符串都被存储在 **char 类型的数组**中，**且以字符 `\0`结尾**；这是空字符（null character），C语言用它标记字符串的结束。

#### 2.1、初始化

- ```cpp
  char site[7] = {'R', 'U', 'N', 'O', 'O', 'B', '\0'};
  ```

- ```cpp
  char site[] = "RUNOOB";
  ```

<!--其实，您不需要把 null 字符放在字符串常量的末尾。C++ 编译器会在初始化数组时，自动把 \0 放在字符串的末尾。-->

#### 2.2、长度

> - `sizeof` ：所占空间大小
> - `strlen`：数组长度
>
> `sizeof` 把不可见字符`'\0'` 也计算在内，而 `strlen`运算符给出的是字符串中的字符数，并不计算字符`'\0'` ，

| 字符串                        |     输出     |    sizeof    |    strlen    |
| ----------------------------- | :----------: | :----------: | :----------: |
| c1[] = "abc";                 |     abc      |      4       |      3       |
| c2[] = "abc\0";               |     abc      |      5       |      3       |
| c3[4] = "ab\0"                |      ab      |      4       |      2       |
| c4[4] = "abc\0";              | ==超出长度== | ==超出长度== | ==超出长度== |
| c5[]={'a','b','c,'d'};        |     abcd     |      4       |      4       |
| c6[4]={'a','b','c','d'}       |     abcd     |      4       |      4       |
| c7[]={'a','b','c','\0'}       |     abc      |      4       |      3       |
| c8[4]={'a','b','c','\0'}      |     abc      |      4       |      3       |
| c9[4]={'a','b','\0'}          |      ab      |      4       |      2       |
| c10[4]={'a','b','\0','c'}     |      ab      |      4       |      2       |
| c11[4]={'a','b','c','\0','d'} | ==超出长度== | ==超出长度== | ==超出长度== |

#### 2.3、字符串指针

```cpp
char a[] = "abcd"
char *p = a;// p指向 char 数组 a 的首元素地址，可通过*p 改变数组 a 的内容
```

或

```cpp
const char* str ;
str = "Hello World\0";
```

---

### 3、相关函数<a id="1.3">💚</a>

|         函数          |                             作用                             |
| :-------------------: | :----------------------------------------------------------: |
| **strcpy(str1,str2)** |                复制字符串 str2 到字符串 str1                 |
| **strcat(str1,str2)** |             连接字符串 str2 到字符串 str1 的末尾             |
|   **strlen(str1)**    |                    返回字符串 str1 的长度                    |
| **strcmp(str1,str2)** | 如果 str1 和 str2 是相同的，则返回 0；如果 str1<str2 则返回值为-1；如果 str1>str2 则返回值为1。 |
|  **strchr(str1,ch)**  | 返回一个指针，指向字符串 str1 中字符 ch 的第一次出现的位置。 |
| **strstr(str1,str2)** | 返回一个指针，指向字符串 str1 中字符串 str2 的第一次出现的位置。 |

---

### 4、C++字符串<a id="1.4">💚</a>

> C++ 标准库提供了 **string** 类类型，支持上述所有的操作，另外还增加了其他更多的功能。

#### 4.1、构造函数

- ```cpp
  string str;
  eg:	string s = "ab\0\0c";       
  // s 内容为 ab
  ```

- ```cpp
  string str("ab\0\0c");  		
  // 等价于 str="ab\0\0c"
  ```

- ```cpp
  string str(string s, size_type n);
  eg:	string str("ab\0\0c", 5);  
  //  将"ab\0\0c"的前5个字节存到 str 里
  ```

  > `warning`: 可以看到如果想要在字符串中存储空字符`'\0'`，只能用第3种方式构造。在第3,4种方法中，都限定了字符串长度，此时要格外注意，n不能超出字符串 s 的所含字符个数下标，否则构造出的字符串会包含一些未知字符。

- ```cpp
  string str(string s, char c, size_type n);
  eg:	string str("ab\0\0c", b, 4);  
  //将"ab\0\0c"的 b 位置开头、长度为4字节的字符串存到 str 里
  ```

- ```cpp
  string str(size_type n, char c);
  eg:	string str(4, 'A')  //存储 4 个'A'到s里
  ```

#### 4.2、类函数

```cpp
string str = str1 + str2;// 字符串拼接
str[2];					 // 访问str中的第三个字符，无边界检查，所以推荐使用下一种一种访问方法
str.at(2);				 // 访问str中的第三个字符，有边界检查
str.empty();			 // 判断str是否为空，若 str 为空则返回true，否则返回 false 
str.length()；           // 获取字符串长度
str.size();　　　　　　　  // 获取字符串数量,等价于length()
str.capacity();　　　　　 // 获取容量,容量包含了当前string里不必增加内存就能使用的字符数
str.front();[C++11]		// 返回str的首字符
str.back();	[C++11]		// 返回str的末字符
str.resize(10);　　　　　 
// 表示设置当前string里的串大小,若设置大小大于当前串长度,则用字符\0来填充多余的.
str.resize(10, char c);　 
// 设置串大小，若设置大小大于当前串长度,则用字符c来填充多余的
str.reserve(10);　　　　　
//设置string里的串容量,不会填充数据.
str.swap(str1);        　
//替换str 和 str1 的字符串
str.puch_back('A');    
//在str末尾添加一个'A'字符,参数必须是字符形式
str.append("ABC");     
//在str末尾添加一个"ABC"字符串,参数必须是字符串形式
str.insert(2, "ABC");   
//在str的下标为2的位置,插入"ABC"
str.erase(2);         　
//从下标为2的位置开始删除后面的字符,比如:"ABCD" --> "AB"
str.erase(2, 1);         
//从下标为2的位置删除1个字符,比如: "ABCD"  --> "ABD"
str.clear();            
//清空str内容，str.size()=str().length()=0, 但不同于std::vector::clear，C++标准不显式要求此函数不更改capacity，即不释放分配的内存，若str="ABC", str.capacity()=3
str.replace(2,2, "ABCD"); 
//从下标为2的位置,替换2个字节为"ED",比如："ABCCA" --> "ABEDA"
str.starts_with("as");[C++20]
// 判断str是否以"as"开头，是返回true，否则返回false
str.ends_with("as");[C++20]
// 判断str是否以"as"结尾，是返回true，否则返回false
str.substr(2);	
//结果为 str从 第三个字符开始往后的子串，比如："ASCDS" --> "CDS"
str.substr(2, 2); 
//结果为 str从 第三个字符为开始、第4个字符结束的子串，比如："ASCDS" --> "CD" substr为 [pos, pos+size)
str.find("ah");	
// 返回str中字符串 "ah" 首次出现的位置 str.find(string s, size_type n=0)如果没找到则返回 -1
str.find("as", 2);	
// 从str第三个字符开始寻找 "as" 第一次出现的位置,如果没找到则返回 -1
str.rfind("ah");	
//在str中反向搜索字符串 "ah" 首次出现的位置
str.rfind("as", 2);
// 从str第三个字符开始往后的字符中反向寻找 "as" 第一次出现的位置
str.find_first_of('a');	
//查找 str 中 a 第一次出现的位置；如果str中没有字符 a，则返回std::string::npos(18446744073709551615)
str.find_first_of('a'， 5);	
//从 str 的第六个字符开始查找 a 第一次出现的位置；如果str中没有字符 a，则返回 std::string::npos(18446744073709551615)
str.find_first_not_of('a');	
//查找 str 中第一个非 a 字符的位置；如果str中全是 a，则返回 std::string::npos(18446744073709551615)
str.find_first_not_of('a'， 5);	
//从 str 的第六个字符开始查找 str 中第一个非 a 字符的位置；如果从 str 的第六个字符开始全是 a，则返回std::string::npos(18446744073709551615)
```

---

### 5、格式转换<a id="1.5">💚</a>

> 不同格式字符串的相互转换

#### 5.1、string →  char

- string - > char[]

  ```cpp
  // string -> char[]，只能通过 strncpy() 拷贝实现
  string str = "I Love u";
  char c[] = str;	// wrong!!!!
  char c1[] = "this string should longer than str";	// c1长度必须要大于str长度
  /*#############################################################*/
  strncpy(c1, str.c_str(), str.length()+1); // 不能漏掉 \0 ,所以要加1
  ```

- string - > char*

  ```cpp
  // string -> char*，通过类型转换
  string str = "I Love You";
  const char *c = str.c_str(); // 不可修改版，str.c_str()将 string 类型转化为 const char*
  char *c = const_cast<char*>(str.c_str()); // 可修改版
  ```

#### 5.2、char → string

- char[] - > string

  ```cpp
  // char[] -> string，直接赋值即可
  char a[] = "a s_Q";
  string str = a;	
  ```

- char* - > string

  ```cpp
  // char* -> string，直接赋值
  const char *c = "asd";
  string str = c;
  ```

#### 5.3、string → num 

##### 5.3.1、有符号

- `int stoi(string str);`
- `long stol(string str);`
- `long long stoll(string str);`

##### 5.3.2、无符号

- `unsigned long stoul(string str);`
- `unsigned long long stoull(string str);`

##### 5.3.3、浮点数

- `float stof(string str);`
- `double stod(string str);`
- `long double stold(string str);`

#### 5.4、number → string

函数：<mark>**to_string() **</mark>

---

[<!--返回目录-->](#1)

## 二、结构体

<a id="2"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [定义与创建](#2.1)
- $\textcolor{#2a6e3f}{【2】}$ [结构体数组](#2.2)
- $\textcolor{#2a6e3f}{【3】}$ [结构体指针](#2.3)
- $\textcolor{#2a6e3f}{【4】}$ [结构体嵌套结构体](#2.4)
- $\textcolor{#2a6e3f}{【5】}$ [结构体做函数参数](#2.5)

### 1、定义与创建<a id="2.1">💛</a>

#### 1.1、定义

结构体是一个由用户定义的数据类型，可以容纳许多不同的数据值。`一些类型组合成的一个类型`

#### 1.2、语法

语法： `struct <name> {....}`

<!--举例-->

```cpp
struct Student
{
 int m_age;
 string m_name;
 double m_score;
};
```

#### 1.3、创建

==创建时C++中可以省略***struct***关键字==

-   `创建之后赋初值`

  ```cpp
  struct Student s1;
  
  s1.m_name
  
  s1.m_age;
  ```

-  `创建并赋初值`

  ```cpp
  struct Student s2 = {18,"aaa",23.5};
  ```

- `在定义结构体时就创建结构体变量`

  ```cpp
  struct Student
  {
  	int m_age;
  	string m_name;
  	double m_score;
  }s1;
  ```

---

### 2、结构体数组<a id="2.2">💛</a>

和普通数组相同，只是类型不同。

<!--举例-->

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

---

### 3、结构体指针<a id="2.3">💛</a>

> **$\textcolor{red}{利用操作符}$`->` $\textcolor{red}{访问内容}$**

<!--举例-->

```c++
Student s1={21,"小王",98.66};
Student *p=&s1;
cout<<p->m_name<<endl;
```

---

### 4、结构体嵌套结构体<a id="2.4">💛</a>

<!--举例-->

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

---

### 5、结构体做函数参数<a id="2.5">💛</a>

<!--举例-->

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

---

[<!--返回目录-->](#2)

## 三、共用体

<a id="3"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [定义](#3.1)
- $\textcolor{#2a6e3f}{【2】}$ [创建](#3.2)
- $\textcolor{#2a6e3f}{【3】}$ [匿名共用体](#3.3)
- $\textcolor{#2a6e3f}{【4】}$ [注意](#3.4)

### 1、定义<a id="3.1">💙</a>

​	共用体（`union`）是一种数据格式，它能够**存储不同的数据类型**，**但只能同时存储其中的一种类型**，也就是说，共用体只能存储int、long或double,而结构体可以同时存储int、long和double。共用体的语法与结构体相似，但含义不同。

---

### 2、创建<a id="3.2">💙</a>

```cpp
union val
{
    int int_val;
    long long_val;
    double double_val;
};
```

`创建`

```cpp
val v = {10}; //<-> int_val = 10;
```

---

### 3、匿名共用体<a id="3.3">💙</a>

```cpp
struct widget
{
	char brand[20];
	int type;
	union
	{
		long id_num;
		char id_char[20];
	};
};
```

> ​	匿名共用体没有名称，其成员将成为位于相同地址的变量。显然，每次只有一个成员是当前的成员：由于共用体是匿名的，因此**id_num和id_char**被视为prize的两个成员，**它们的地址相同**，所以**不需要中间标识符**。我们只需要负责确定当前哪个成员是活动的。

---

### 4、注意<a id="3.4">💙</a>

- 当第二次给共用体中的成员赋值后，之前的的值将丢失，也就是说共用体里虽然有三个类型，但每次只能存在一个类型。**由于共用体每次只能存储一个值，因此它必须有足够的空间来存储最大的成员，所以，<mark>共用体的长度为最大成员长度。</mark>**

---

[<!--返回目录-->](#3)

## 四、内存分区

<a id="4"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [代码区](#4.1)
- $\textcolor{#2a6e3f}{【2】}$ [全局区](#4.2)
- $\textcolor{#2a6e3f}{【3】}$ [栈区](#4.3)
- $\textcolor{#2a6e3f}{【4】}$ [堆区](#4.4)

### 1、代码区<a id="4.1">💜</a>

> 程序未运行产生的区域

 存放CPU执行的机器指令（二进制），由操作系统的进行管理

- `共享`：代码区是**共享**的，目的是对于频繁被执行的程序，只需要在内存中有一份代码即可。
- `只读`：代码区是**只读**的，为防止程序意外被修改了指令。

---

### 2、全局区<a id="4.2">💜</a>

> 程序未运行产生的区域

存放全局变量和静态变量以及常量。

- **全局变量**
- **静态常量**
- **常量区**
  1. **字符串常量**
  2. **const 修饰的全局常量**      【const 修饰的局部常量不在全局区】

<!--数据由操作系统释放-->

---

### 3、栈区<a id="4.3">💜</a>

> 程序运行产生的区域

由编译器自动分配释放，存放函数的参数值、局部变量等。在生命周期期间结束后自动释放

- 注意函数不要返回局部变量的地址。

- 栈区数据由编译器管理和开辟

<!--数据由操作系统释放-->

---

### 4、堆区<a id="4.4">💜</a>

> 程序运行产生的区域

<!--由开发者管理操作，需要自已释放-->

- `开辟数据`

  $\textcolor{red}{new}$ <-->$\textcolor{red}{delete}$

- `释放数据`

  $\textcolor{red}{malloc}$ <-->$\textcolor{red}{free}$

<mark>**注意：堆区数据必须自已释放。C++无垃圾回收机制。**</mark>

<!--举例-->

```cpp
int* p = new int(10);
cout << *p << endl;
delete p;
```

- 指针本质为局部变量，在栈区，指向堆区的数据。此数据需要手动释放。

**[内存分区详细内容:airplane:](./stack.md)**

---

[<!--返回目录-->](#4)

[<!--返回总目录-->](#0)

**[README](../../README.md)**

