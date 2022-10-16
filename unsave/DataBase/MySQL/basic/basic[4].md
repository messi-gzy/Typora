# 基础[4]

<a id="0">`目录`</a>

- $\textcolor{#e18a3b}{【一】}$**[排序](#1)**
- $\textcolor{#e18a3b}{【二】}$**[分页](#2)**
- $\textcolor{#e18a3b}{【三】}$**[多表查询](#3)**

## 一、排序

<a id="1">**<!--目录-->**</a>

- $\textcolor{#2a6e3f}{【1】}$ [排序规则](#1.1)
- $\textcolor{#2a6e3f}{【2】}$ [单列排序](#1.2)
- $\textcolor{#2a6e3f}{【3】}$ [多列排序](#1.3)

### 1、排序规则<a id="1.1">💚</a>

> **如果没有使用排序，默认是按添加数据的顺序进行排序的。**

- $\textcolor{SeaGreen}{【1】}$ 使用 ORDER BY 子句排序
  - **`ASC`（ascend）: 升序** 
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

### 2、单列排序<a id="1.2">💚</a>

`举例`

```sql
SELECT employee_id,last_name,salary
    FROM employees
WHERE salary BETWEEN 11000 AND 30000
ORDER BY salary DESC ;
```

### 3、多列排序<a id="1.3">💚</a>

![](https://pic.imgdb.cn/item/6329685216f2c2beb1ab0207.png)

`举例`

```sql
SELECT employee_id,last_name,salary,department_id
    FROM employees
WHERE salary BETWEEN 11000 AND 30000
ORDER BY department_id DESC,salary ASC ;
```

> **在第一层排序中，遇到相同的，再按二层排序方法排序，依次排序**

[<!--返回目录-->](#1)

---

## 二、分页

<a id="2">**<!--目录-->**</a>

- $\textcolor{#2a6e3f}{【1】}$ [定义](#2.1)
- $\textcolor{#2a6e3f}{【2】}$ [规则](#2.2) 
- $\textcolor{#2a6e3f}{【3】}$ [拓展](#2.3)

### 1、定义<a id="2.1">💚</a>

> **分页就是指在数据库获取数据时，只获得我们所需的数据条目**

### 2、规则<a id="2.2">💚</a>

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

### 3、拓展<a id="2.3">💚</a>

> MySQL 8.0中可以使用“LIMIT 3 OFFSET 4”，意思是获取从第5条记录开始后面的3条记录，和“LIMIT 4,3;”返回的结果相同。
> 
> ```sql
> LIMIT 3 OFFSET 4
> ```
> 
> 偏移量为 `4`，条数为 `3`

[<!--返回目录-->](#2)

---

## 三、多表查询

<a id="3">**<!--目录-->**</a>

- $\textcolor{#2a6e3f}{【1】}$ [介绍](#3.1)
- $\textcolor{#2a6e3f}{【2】}$ [等值和非等值连接](#3.2) 
- $\textcolor{#2a6e3f}{【3】}$ [自连接和非自连接](#3.3)
- $\textcolor{#2a6e3f}{【4】}$ [内连接和外连接](#3.4)
- $\textcolor{#2a6e3f}{【5】}$ [UNION](#3.5)
- $\textcolor{#2a6e3f}{【6】}$ [JOIN ON](#3.6)
- $\textcolor{#2a6e3f}{【7】}$ [其他](#3.7)

### 1、介绍<a id="3.1">💛</a>

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

---

### 2、等值和非等值连接<a id="3.2">💛</a>

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

---

### 3、自连接和非自连接<a id="3.3">💛</a>

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

---

### 4、内连接和外连接<a id="3.4">💛</a>

#### 1、内连接

> 合并具有同一列的两个以上的表的行, 结果集中不包含一个表与另一个表不匹配的行

```sql
SELECT employee_id,department_name
FROM employees,departments
WHERE employees.department_id = departments.department_id
```

`SQL99`

```sql
SELECT last_name,department_name,d.location_id
FROM employees e INNER JOIN departments d
    on e.department_id = d.department_id
JOIN locations l
    on d.location_id = l.location_id
```

#### 2、外连接

> 两个表在连接过程中除了返回满足连接条件的行以外还返回左（或右）表中不满足条件的 行 ，这种连接称为左（或右） 外连接。没有匹配的行时, 结果表中相应的列为空(NULL)。

##### 2.1、左外连接

​    则连接条件中左边的表也称为主表 ，右边的表称为从表 。两个表在连接过程中除了返回连接条件的行以外**还返回左表中不满足条件的行**。

`SQL92`

```sql
SELECT last_name,department_name
FROM employees ,departments
WHERE employees.department_id = departments.department_id(+);
```

`SQL99`

```sql
SELECT last_name,department_name
FROM employees e LEFT OUTER JOIN departments d
    on e.department_id = d.department_id
```

##### 2.2、右外连接

​    则连接条件中右边的表也称为主表 ，左边的表称为从表 。两个表在连接过程中除了返回连接条件的行以外**还返回右表中不满足条件的行**。

`SQL92`

```sql
SELECT last_name,department_name
FROM employees ,departments
WHERE employees.department_id(+) = departments.department_id;
```

`SQL99`

```sql
SELECT last_name,department_name
FROM employees e RIGHT OUTER JOIN departments d
    on e.department_id = d.department_id
```

##### 2.3、满外连接

---

### 5、UNION<a id="3.5">💛</a>

#### 1、定义

> 合并查询结果利用`UNION`关键字，**可以给出多条SELECT语句，并将它们的结果组合成单个结果集**。合并时，==两个表对应的列数和数据类型必须相同，并且相互对应==。各个SELECT语句之间使用`UNION`或`UNION ALL`关键字分隔。

#### 2、语法

```sql
SELECT column,...FROM table1 
UNION [ALL]
SELECT column,... FROM table2
```

#### 3、区别

##### 1、UNION

> UNION 操作符返回两个查询的结果集的并集，**去除重复记录**。

![](https://pic1.imgdb.cn/item/633be25f16f2c2beb1bc47f9.png)

##### 2、UNION ALL

> UNION ALL操作符返回两个查询的结果集的并集。对**于两个结果集的重复部分，不去重**。

<img src="https://pic1.imgdb.cn/item/633be32b16f2c2beb1bd9f1c.png" style="zoom:50%;" />

---

### 6、JOIN ON<a id="3.6">💛</a>

`语法`

```sql
#实现查询结果是
A SELECT 字段列表 
FROM A表 [..](LEFT OUTER | RIGHT OUTER | INNER)JOIN B表 
ON 关联条件
WHERE 等其他子句;
```

<img src="https://pic1.imgdb.cn/item/633be45e16f2c2beb1c00ded.png" style="zoom:67%;" />

##### 1、左上

> 左外连接

```sql
SELECT employee_id,last_name,department_name 
FROM employees e LEFT JOIN departments d 
ON e.`department_id` = d.`department_id`;
```

##### 2、右上

> 右外连接

```sql
SELECT employee_id,last_name,department_name 
FROM employees e RIGHT JOIN departments d 
ON e.`department_id` = d.`department_id`;
```

##### 3、左中

```sql
#A - A∩B 
SELECT employee_id,last_name,department_name 
FROM employees e LEFT JOIN departments d 
ON e.`department_id` = d.`department_id` 
WHERE e.`department_id` IS NULL
```

##### 4、右中

```sql
#B-A∩B 
SELECT employee_id,last_name,department_name 
FROM employees e RIGHT JOIN departments d 
ON e.`department_id` = d.`department_id` 
WHERE d.`department_id` IS NULL
```

##### 5、左下

> 满外连接

```sql
SELECT employee_id,last_name,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
UNION ALL 
SELECT last_name,department_name,e.department_id
FROM employees e LEFT OUTER
    JOIN departments d
        on e.department_id = d.department_id
WHERE e.department_id IS NULL;
```

##### 6、右下

```sql
#左中图 + 右中图 A ∪B- A∩B 或者 (A - A∩B) ∪ （B - A∩B） 
SELECT employee_id,last_name,department_name 
FROM employees e LEFT JOIN departments d 
ON e.`department_id` = d.`department_id` 
WHERE d.`department_id` IS NULL 
UNION ALL 
SELECT employee_id,last_name,department_name
FROM employees e RIGHT JOIN departments d 
ON e.`department_id` = d.`department_id` 
WHERE e.`department_id` IS NULL
```

---

### 7、其他<a id="3.7">💛</a>

#### 7.1、自然连接

`NATURAL JOIN`

> 自动查询两张连接表中所有**相同的字段** ，然后进行**等值连接** 。

`SQL92`

```sql
SELECT employee_id,last_name,department_name
FROM employees e JOIN departments d 
ON e.`department_id` = d.`department_id` 
AND e.`manager_id` = d.`manager_id`;
```

`SQL99`

```sql
SELECT employee_id,last_name,department_name 
FROM employees e NATURAL JOIN departments d;
```

#### 7.2、USING

> `USING` 指定数据表里的**==同名字段进行等值连接==**。但是只能配合`JOIN`一起使用

`SQL92`

```sql
SELECT employee_id,last_name,department_name
FROM employees e JOIN departments d 
ON e.`department_id` = d.`department_id` 
AND e.`manager_id` = d.`manager_id`;
```

`SQL99`

```sql
SELECT employee_id,last_name,department_name 
FROM employees e JOIN departments d 
USING (department_id);
```

---

[<!--返回目录-->](#3)

[<!--返回总目录-->](#0)

**[返回上一页🥣](../../README.md)**
