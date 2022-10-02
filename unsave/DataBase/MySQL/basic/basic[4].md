# 基础[4]

-  $\textcolor{#e18a3b}{【一】}$**[排序](#1)**
-  $\textcolor{#e18a3b}{【二】}$**[分页](#2)**
- $\textcolor{#e18a3b}{【三】}$**[多表查询](#3)**

## 一、排序

<a id="1">**`目录`**</a>

- $\textcolor{#2a6e3f}{【1】}$ [排序规则](#1.1)
- $\textcolor{#2a6e3f}{【2】}$ [单列排序](#1.2)
- $\textcolor{#2a6e3f}{【3】}$ [多列排序](#1.3)

### 1、排序规则

<a id="1.1">排序规则</a>

> **如果没有使用排序，默认是按添加数据的顺序进行排序的。**

- $\textcolor{SeaGreen}{【1】}$ 使用 ORDER BY 子句排序
  -  **`ASC`（ascend）: 升序** 
  - **`DESC`（descend）:降序**
  - **==如果未指定排序方式，默认 升序==**
- $\textcolor{SeaGreen}{【2】}$ ORDER BY 子句在SELECT语句的结尾。

`举例`

```sql
SELECT employee_id,last_name,salary
    FROM employees
WHERE salary BETWEEN 11000 AND 30000
ORDER BY salary DESC ;
```

### 2、单列排序

<a id="1.2">单列排序</a>

`举例`

```sql
SELECT employee_id,last_name,salary
    FROM employees
WHERE salary BETWEEN 11000 AND 30000
ORDER BY salary DESC ;
```

### 3、多列排序

<a id="1.3">多列排序</a>

![](https://pic.imgdb.cn/item/6329685216f2c2beb1ab0207.png)

`举例`

```sql
SELECT employee_id,last_name,salary,department_id
    FROM employees
WHERE salary BETWEEN 11000 AND 30000
ORDER BY department_id DESC,salary ASC ;
```

> **在第一层排序中，遇到相同的，再按二层排序方法排序，依次排序**

---

## 二、分页

<a id="2">**`目录`**</a>

- $\textcolor{#2a6e3f}{【1】}$ [定义](#2.1)
- $\textcolor{#2a6e3f}{【2】}$ [规则](#2.2) 
- $\textcolor{#2a6e3f}{【3】}$ [拓展](#2.3)

### 1、定义

<a id="2.1">定义</a>

> **分页就是指在数据库获取数据时，只获得我们所需的数据条目**

### 2、规则

<a id="2.2">规则</a>

**`LIMIT`**

#### 2.1、格式

```mysql
LIMIT [位置偏移量,] 行数
```

- $\textcolor{SeaGreen}{【1】}$ 第一个【位置偏移量】参数指示MySQL从哪一行开始显示，是一个可选参数，如果不指定“位置偏移 量”，将会从表中的第一条记录开始**（第一条记录的位置偏移量是0，第二条记录的位置偏移量是 1，以此类推）**；
- $\textcolor{SeaGreen}{【2】}$第二个参数“行数”指示返回的记录条数。

#### 2.2、举例

```sql
--前10条记录：
SELECT * FROM 表名 LIMIT 0,10; 
// 或者
SELECT * FROM 表名 LIMIT 10;
--第11至20条记录： 
SELECT * FROM 表名 LIMIT 10,10;
--第21至30条记录： 
SELECT * FROM 表名 LIMIT 20,10;

###公式
SELECT * FROM table
LIMIT(PageNo - 1)*PageSize,PageSize;
```

#### 2.3、注意

- **$\textcolor{SeaGreen}{【1】}$  LIMIT 子句必须放在整个SELECT语句的最后**
- **$\textcolor{SeaGreen}{【2】}$ ORDER BY 子句在SELECT语句的结尾。**
- $\textcolor{SeaGreen}{【3】}$ 约束返回结果的数量可以 减少数据表的网络传输量 ，也可以提升查询效率 。

### 3、拓展

<a id="2.3">拓展</a>

> MySQL 8.0中可以使用“LIMIT 3 OFFSET 4”，意思是获取从第5条记录开始后面的3条记录，和“LIMIT 4,3;”返回的结果相同。
>
> ```sql
> LIMIT 3 OFFSET 4
> ```
>
> 偏移量为 `4`，条数为 `3`

---

## 三、多表查询

<a id="3">**`目录`**</a>

- $\textcolor{#2a6e3f}{【1】}$ [介绍](#3.1)
- $\textcolor{#2a6e3f}{【2】}$ [分类](#3.2) 
- $\textcolor{#2a6e3f}{【3】}$ [](#3.3)
- $\textcolor{#2a6e3f}{【4】}$ [](#3.4)
- $\textcolor{#2a6e3f}{【5】}$ [](#3.5)
- $\textcolor{#2a6e3f}{【6】}$ [](#3.6)

### 1、介绍

<a id="3.1">介绍</a>

> 多表查询，也称为关联查询，指**两个或更多个表一起完成查询操作**。
>
> 前提条件：这些一起查询的表之间是有关系的（一对一、一对多），它们之间一定是有关联字段，这个 关联字段可能建立了外键，也可能没有建立外键。

`笛卡尔积`

笛卡尔积为两个集合(两张表)中的每条数据进行两两组合的结果。

<img src="https://pic1.imgdb.cn/item/6336f81d16f2c2beb1cdc0bc.png" style="zoom: 67%;" />

==消除笛卡尔积==，**添加条件**

`简单实现`

```sql
SELECT employee_id,department_name
FROM employees,departments
WHERE employees.department_id = departments.department_id
```

`注意`

**==在表中有相同列时，在列名之前加上表名前缀，明确字段所在的表==**

- 使用别名可以简化查询。
- 列名前使用表名前缀可以提高查询效率。
- 使用别名后，就必须使用别名

### 2、分类

<a id="3.2">分类</a>

#### 2.1、等值和非等值连接

##### 1、等值连接

> 多个连接条件与 AND 操作符

```sql
SELECT employee_id,last_name,department_name,city
FROM employees ,departments,locations
WHERE employees.department_id = departments.department_id
AND departments.location_id = locations.location_id;
```

##### 2、非等值连接

> 条件存在区间

```sql
SELECT last_name,salary,grade_level
FROM employees AS e,job_grades AS j
WHERE e.salary BETWEEN j.lowest_sal AND j.highest_sal;
```

#### 2.2、自连接和非自连接

##### 1、自连接

> 字段互相关联
>
> <img src="https://pic1.imgdb.cn/item/6337f89c16f2c2beb1b1a1ca.png" style="zoom:50%;" />

```sql
SELECT  e1.last_name ,e1.employee_id ,e2.manager_id
FROM employees e1,employees e2
WHERE e1.employee_id = e2.manager_id;
```

##### 2、非自连接

> 等值连接

#### 2.3、内连接和外连接

##### 1、内连接

> 合并具有同一列的两个以上的表的行, 结果集中不包含一个表与另一个表不匹配的行

##### 2、外连接

### 3、

<a id="3.3"></a>

### 4、

<a id="3.4"></a>

### 5、

<a id="3.5"></a>

### 6、 

<a id="3.6"></a>



