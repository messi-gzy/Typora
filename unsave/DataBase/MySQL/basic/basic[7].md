# 基础[7]

<a id="0">`目录`</a>

- $\textcolor{#e18a3b}{【一】}$**[约束](#1)**

- $\textcolor{#e18a3b}{【二】}$**[视图](#2)**

  ## 一、约束

<a id="1"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [概述](#1.1)
- $\textcolor{#2a6e3f}{【2】}$ [非空约束](#1.2)
- $\textcolor{#2a6e3f}{【3】}$ [唯一性约束](#1.3)
- $\textcolor{#2a6e3f}{【4】}$ [PRIMARY KEY约束](#1.4)
- $\textcolor{#2a6e3f}{【5】}$ [自增列](#1.5)
- $\textcolor{#2a6e3f}{【6】}$ [FOREIGN KEY](#1.6)
- $\textcolor{#2a6e3f}{【7】}$ [CHECK 约束](#1.7)
- $\textcolor{#2a6e3f}{【8】}$ [DEFAULT 约束](#1.8)

### 1、概述<a id="1.1">💚</a>

#### 1.1、数据完整性

​	**数据完整性**（Data Integrity）是指数据的精确性（Accuracy）和可靠性（Reliability）。它是防止数据库中 存在不符合语义规定的数据和防止因错误信息的输入输出造成无效操作或错误信息而提出的。

​	为了保证数据的完整性，SQL规范以约束的方式对表数据进行额外的条件限制。从以下四个方面考虑：

- `实体完整性（Entity Integrity）` ：例如，同一个表中，不能存在两条完全相同无法区分的记录 
- `域完整性（Domain Integrity）` ：例如：年龄范围0-120，性别范围“男/女” 
- `引用完整性（Referential Integrity）` ：例如：员工所在部门，在部门表中要能找到这个部门
- `用户自定义完整性（User-defined Integrity）` ：例如：用户名唯一、密码不能为空等，本部门 经理的工资不得高于本部门职工的平均工资的5倍。

#### 1.2、约束

约束是表级的强制规定。
可以<mark>**在创建表时规定约束（通过 CREATE TABLE 语句）**</mark>，或者在表创建之后通过 ALTER TABLE 语句规定 约束。

#### 1.3、约束分类

##### 1、根据约束数据列的限制

约束可分为： 

- 单列约束：每个约束只约束一列 

- 多列约束：每个约束可约束多列数据 

##### 2、根据约束的作用范围

约束可分为：

- 列级约束：只能作用在一个列上，跟在列的定义后面 
- 表级约束：可以作用在多个列上，不与列一起，而是单独定义

##### 3、根据约束起的作用

约束可分为：

- NOT NULL 非空约束，规定某个字段不能为空 
- UNIQUE 唯一约束，规定某个字段在整个表中是唯一的
-  PRIMARY KEY 主键(非空且唯一)约束
-  FOREIGN KEY 外键约束 
- CHECK 检查约束 
- DEFAULT 默认值约束

> <mark>查看表中的约束</mark>
>
> ```sql
> SELECT *
> FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS
> WHERE TABLE_NAME = '表名';
> ```

---

### 2、非空约束<a id="1.2">💚</a>

#### 2.1、作用

**限定某个字段/某列的值不允许为空**

#### 2.2、特点

> **NOT NULL**

- 默认，所有的类型的值都可以是NULL，包括INT、FLOAT等数据类型 
- 非空约束只能出现在表对象的列上，**只能某个列单独限定非空，不能组合非空** 
- 一个表可以有很多列都分别限定了非空
- 空字符串''不等于NULL，0也不等于NULL

#### 2.3、添加约束

```sql
CREATE TABLE NOT_NULL(
    id INT NOT NULL ,
    last_name VARCHAR(20) NOT NULL,
    email VARCHAR(25),
    salary DECIMAL(10,2)
);
```

#### 2.4、删除约束

```sql
alter table 表名称 modify 字段名 数据类型 NULL;
#去掉not null，相当于修改某个非注解字段，该字段允 许为空
# or 
alter table 表名称 modify 字段名 数据类型;
#去掉not null，相当于修改某个非注解字段，该字段允许为空
```

---

### 3、唯一性约束<a id="1.3">💚</a>

#### 3.1、作用

**用来限制某个字段/某列的值不能重复。**

> <mark>**UNIQUE**</mark>

#### 3.2、特点

- 同一个表可以有多个唯一约束。
- 唯一约束**可以是某一个列的值唯一，也可以多个列组合的值唯一**。
- 唯一性约束允许列值为空。
- 在创建唯一约束的时候，如果不给唯一约束命名，就默认和列名相同。 
- MySQL会给唯一约束的列上默认创建一个唯一索引。

#### 3.3、举例

```sql
CREATE TABLE unique_test
(
    id        INT         NOT NULL UNIQUE,
    last_name VARCHAR(20) NOT NULL,
    email     VARCHAR(25) UNIQUE,
    salary    DECIMAL(10, 2)
);
```

#### 3.4、复合唯一约束

```sql
create table 表名称( 
	字段名 数据类型, 
	字段名 数据类型, 
	字段名 数据类型, 
	unique key(字段列表) 
	#字段列表中写的是多个字段名，多个字段名用逗号分隔，表示那么是复合唯一，即多个字段的组合是唯一的
);
```

- 多个条件同时满足唯一

#### 3.5、删除唯一的约束

- 添加唯一性约束的列上也会自动创建唯一索引。 
- 删除唯一约束只能通过删除唯一索引的方式删除。
- 删除时需要指定唯一索引名，唯一索引名就和唯一约束名一样。
- 如果创建唯一约束时未指定名称，如果是单列，就默认和列名相同；如果是组合列，那么默认和() 中排在第一个的列名相同。也可以自定义唯一性约束名。

---

### 4、PRIMARY KEY约束<a id="1.4">💚</a>

#### 4.1、作用

用来唯一标识表中的一行记录。

> <mark>**primary key**</mark>

#### 4.2、特点

- 主键约束相当于**唯一约束+非空约束**的组合，主键约束列不允许重复，也不允许出现空值。
- <mark>**一个表最多只能有一个主键约束**</mark>，建立主键约束可以在列级别创建，也可以在表级别上创建。 
- 主键约束对应着表中的一列或者多列（复合主键）
- 如果是多列组合的复合主键约束，那么这些列都不允许为空值，并且组合的值不允许重复。 
- MySQL的主键名总是`PRIMARY`，就算自己命名了主键约束名也没用。
-  当创建主键约束时，系统默认会在所在的列或列组合上**建立对应的主键索引**（能够根据主键查询 的，就根据主键查询，效率更高）。**如果删除主键约束了，主键约束对应的索引就自动删除了**。
- 需要注意的一点是，不要修改主键字段的值。因为**主键是数据记录的唯一标识**，如果修改了主键的值，就有可能会破坏数据的完整性。

#### 4.3、举例

```sql
CREATE TABLE primary_test
(
    id        INT PRIMARY KEY,
    last_name VARCHAR(20) NOT NULL,
    email     VARCHAR(25),
    salary    DECIMAL(10, 2)
);
```

<!--复合主键举例-->

```sql
create table 表名称( 
	字段名 数据类型,
	字段名 数据类型, 
	字段名 数据类型, 
	primary key(字段名1,字段名2) 
	#表示字段1和字段2的组合是唯一的，也可以有更多个字段
);
```

---

### 5、自增列<a id="1.5">💚</a>

#### 5.1、作用

某个字段的值自增

> **==auto_increment==**

#### 5.2、特点

- **一个表最多只能有一个自增长列** 
- 当需要产生唯一标识符或顺序值时，可设置自增长 
- **自增长列约束的列必须是键列（主键列，唯一键列）** 
- 自增约束的列的**数据类型必须是整数类型**
- 如果自增列指定了 0 和 null，会在当前最大值的基础上自增；**如果自增列手动指定了具体值，直接赋值为具体值。**

#### 5.3、举例

```sql
CREATE TABLE auto_increment
(
    id        INT PRIMARY KEY AUTO_INCREMENT,
    last_name VARCHAR(20) NOT NULL
);

INSERT INTO auto_increment(last_name)
VALUES ('hello');
```

---

### 6、FOREIGN KEY<a id="1.6">💚</a>

#### 6.1、作用

外键约束：限定某个表的某个字段的引用完整性。

> **==FOREIGN KEY==**

<!--举例说明-->

**主表（父表）：被引用的表，被参考的表**

**从表（子表）：引用别人的表，参考别人的表**
例如：员工表的员工所在部门这个字段的值要参考部门表：部门表是主表，员工表是从表。
例如：学生表、课程表、选课表：选课表的学生和课程要分别参考学生表和课程表，学生表和课程表是 主表，选课表是从表。

#### 6.2、特点

- 从表的外键列，必须引用/参考主表的主键或唯一约束的列 

  为什么？因为被依赖/被参考的值必须是唯一的

- 在创建外键约束时，如果不给外键约束命名，默认名不是列名，而是自动产生一个外键名（例如 student_ibfk_1;），也可以指定外键约束名。 

- 创建(CREATE)表时就**指定外键约束的话，先创建主表，再创建从表**

- **删表时，先删从表（或先删除外键约束），再删除主表**

- 当主表的记录被从表参照时，主表的记录将不允许删除，如果要删除数据，需要先删除从表中依赖该记录的数据，然后才可以删除主表的数据 

- 在“从表”中指定外键约束，并且一个表可以建立多个外键约束

- **从表的外键列与主表被参照的列名字可以不相同，但是数据类型必须一样，逻辑意义一致。**

- 当创建外键约束时，系统默认会在所在的列上建立对应的普通索引。但是**索引名是外键的约束名**。（根据外键查询效率很高）。删除外键约束后，必须 手动删除对应的索引

#### 6.3、举例

```sql
CREATE TABLE foreign_dept(
    dept_id INT PRIMARY KEY ,
    dept_name VARCHAR(20)
);
CREATE TABLE foreign_emp(
    emp_id INT PRIMARY KEY AUTO_INCREMENT,
    emp_name VARCHAR(20),
    department_id INT,
    CONSTRAINT fk_emp_dept_id FOREIGN KEY (department_id) REFERENCES foreign_dept(dept_id)
);
```

<!---添加数据-->

> 先往主表添加数据，再往从表添加数据，注意具有外键约束的值的对应相等

```sql
INSERT INTO foreign_dept
VALUES (10, '华电');

INSERT INTO foreign_emp
VALUES (1001, 'hello', 10);
```

#### 6.4、注意

- 添加了外键约束后，主表的修改和删除数据受约束 
- 添加了外键约束后，从表的添加和修改数据受约束 
- 在从表上建立外键，要求主表必须存在
- 删除主表时，要求从表从表先删除，或将从表中外键引用该主表的关系先删除

#### 6.5、约束等级

- `Cascade`方式 ：在父表上update/delete记录时，**同步update/delete掉子表的匹配记录** 
- `Set null`方式 ：在父表上update/delete记录时，**将子表上匹配记录的列设为null**，但是要注意子 表的外键列不能为not null
- `No action`方式 ：如果子表中有匹配的记录，**则不允许对父表对应候选键进行update/delete操作** 
- `Restrict`方式 ：同no action， **都是立即检查外键约束**
- `Set default`方式 ：父表有变更时，子表将外键列设置 成一个默认的值，但Innodb不能识别

![](https://pic.imgdb.cn/item/637e41a816f2c2beb1a7bc7f.png)

**==注意==**

- 如果没有指定等级，就相当于**Restrict**方式。
- 建议：**对于外键约束，最好是采用: ON UPDATE CASCADE ON DELETE RESTRICT 的方式。**

#### 6.6、删除外键约束

##### 1、查看约束名

```sql
SELECT * 
FROM information_schema.table_constraints 
WHERE table_name = '表名称';
#查看某个 表的约束名
```

##### 2、删除外键约束

```sql
ALTER TABLE 从表名 DROP FOREIGN KEY 外键约束名;
```

##### 3、查看索引名

```sql
SHOW INDEX FROM <表名称>; 
#查看某个表的索引名
```

##### 4、删除索引

```sql
ALTER TABLE <从表名> DROP INDEX <索引名>;
```

---

### 7、CHECK 约束<a id="1.7">💚</a>

#### 7.1、作用

检查某个字段的值是否符号xx要求，一般指的是值的范围

> **==CHECK==**

#### 7.2、特点

- **5.7版本不支持**
- 约束一定范围

#### 7.3、举例

```sql
# CHECK 约束
CREATE TABLE check_test
(
    id        INT PRIMARY KEY AUTO_INCREMENT,
    last_name VARCHAR(20),
    salary    DECIMAL(10, 2) CHECK ( salary > 2000 )
);

# Check constraint 'check_test_chk_1' is violated.
# 插入失败
INSERT INTO check_test(last_name, salary)
VALUES ('MaXin',100.2);

INSERT INTO check_test(last_name, salary)
VALUES ('MaXin',2000.20);
```

---

### 8、DEFAULT 约束<a id="1.8">💚</a>

#### 8.1、作用

给某个字段/某列指定默认值，一旦设置默认值，在插入数据时，如果此字段没有显式赋值，则赋值为默认值。

> **==DEFAULT==**

#### 8.2、特点

- 设置默认值，增加数据时不赋值就输入默认值
- 解决NULL问题

#### 8.3、举例

```sql
# DEFAULT 约束
CREATE TABLE default_test
(
    id        INT PRIMARY KEY AUTO_INCREMENT,
    last_name VARCHAR(20),
    salary    DECIMAL(10, 2) DEFAULT 2000
);

DESC default_test;

# 添加数据（无初值）
INSERT INTO default_test(last_name)
VALUES ('hello');

# 建表后添加默认
ALTER TABLE default_test
MODIFY salary DECIMAL(10,2) DEFAULT 2500.56;
```

---

[<!--返回目录-->](#1)

## 二、视图

<a id="2"><!--目录--></a>

- $\textcolor{#2a6e3f}{【1】}$ [视图概述](#2.1)
- $\textcolor{#2a6e3f}{【2】}$ [创建视图](#2.2)
- $\textcolor{#2a6e3f}{【3】}$ [查看视图](#2.3)
- $\textcolor{#2a6e3f}{【4】}$ [更新数据](#2.4)
- $\textcolor{#2a6e3f}{【5】}$ [修改|删除视图](#2.5)
- $\textcolor{#2a6e3f}{【6】}$ [总结](#2.6)

### 1、视图概述<a id="2.1">💛</a>

#### 1.1、常见数据库对象

![](https://pic.imgdb.cn/item/637f586b16f2c2beb1fd424a.png)

#### 1.2、视图概述

- 视图（view）是一种虚拟存在的表，是一个逻辑表，本身并不包含数据。作为一个select语句保存在数据字典中的。
- 通过视图，可以展现基表(用来创建视图的表)的部分数据；视图数据来自定义视图的查询中使用的表，使用视图动态生成。
- 视图（子查询）：是从一个或多个表导出的虚拟的表，其内容由查询定义。具有普通表的结构，但是不实现数据存储。

#### 1.3、视图特点

- 视图是**一种虚拟表 ，本身是不具有数据**的，占用很少的内存空间，它是 SQL 中的一个重要概念。
- 视图建立在已有表的基础上, 视图赖以建立的这些表称为基表。
- **视图的创建和删除只影响视图本身，不影响对应的基表。但是当对视图中的数据进行增加、删除和修改操作时，数据表中的数据会相应地发生变化，反之亦然。**
- 向视图提供数据内容的语句为 SELECT 语句, 可以将视图**理解为存储起来的 SELECT 语句** 
- 在数据库中，视图不会保存数据，数据真正保存在数据表中。当对视图中的数据进行增加、删 除和修改操作时，数据表中的数据会相应地发生变化；反之亦然。
- 视图，是向用户提供基表数据的另一种表现形式。通常情况下，小型项目的数据库可以不使用视图，但是在大型项目中，以及数据表比较复杂的情况下，视图的价值就凸显出来了，它可以帮助我们把经常查询的结果集放到虚拟表中，提升使用效率。理解和使用起来都非常方便。

---

### 2、创建视图<a id="2.2">💛</a>

<!--查询语句-->

```sql
CREATE VIEW <视图名称> 
AS <查询语句>
```

**==创建视图==**

```sql
# 基于单表创建视图
CREATE VIEW vu_emp_s
AS
SELECT employee_id, last_name, salary
FROM emp_s;
# 基于多表查询
CREATE VIEW vu_emp_join_s
AS
SELECT es.employee_id, es.department_id, ds.department_name
FROM emp_s es
         JOIN dept_s ds ON es.department_id = ds.department_id;
```

- 在创建视图时，没有在视图名后面指定字段列表，则视图中字段列表默认和SELECT语句中的字段列表一致。

  ```sql
  # 视图后无指定名称
  CREATE VIEW vu_emp_s_1
  AS
  SELECT employee_id emp_id, last_name lname, salary sal
  FROM emp_s;
  ```

- 如果SELECT语句中给字段取了别名，那么视图中的字段名和别名相同。

  ```sql
  # 视图有指定名称
  CREATE VIEW vu_emp_s_2 (emp_id_s, lname_s, sal_s)
  AS
  SELECT employee_id, last_name, salary
  FROM emp_s;
  ```

---

### 3、查看视图<a id="2.3">💛</a>

##### 3.1、查看表和视图

```sql
SHOW TABLES ;
```

##### 3.2、查看视图结构

```sql
# 查看视图结构
DESCRIBE vu_emp_join_s;
```

##### 3.3、查看视图属性信息

```sql
# 查看视图信息（显示数据表的存储引擎、版本、数据行数和数据大小等）
SHOW TABLE STATUS LIKE 'vu_emp_join_s'\G;
```

> 执行结果显示，注释Comment为VIEW，说明该表为视图，其他的信息为NULL，说明这是一个虚表。

##### 3.4、查看视图的详细定义信息

```sql
# 查看视图的详细定义信息
SHOW CREATE VIEW vu_emp_join_s;
```

---

### 4、更新数据<a id="2.4">💛</a>

#### 4.1、简单更新

```sql
# 更新视图中的数据
UPDATE vu_emp_s
SET salary = 18888
WHERE employee_id = 100;
```

**更新后，视图和创建视图的基础表的相应数据都有改变。**

- 更新视图的数据，基表的数据也会修改
- 更新基表的数据，视图的数据也会修改

#### 4.2、不可更新情况

要使视图可更新，视图中的行和底层基本表中的行之间必须存在 一对一 的关系。另外当视图定义出现如 下情况时，视图不支持更新操作：

- 在定义视图的时候指定了“ALGORITHM = TEMPTABLE”，视图将不支持INSERT和DELETE操作； 
- 视图中不包含基表中所有被定义为非空又未指定默认值的列，视图将不支持INSERT操作；
- 在定义视图的SELECT语句中使用了 JOIN联合查询 ，视图将不支持INSERT和DELETE操作； 
- 在定义视图的SELECT语句后的字段列表中使用了 数学表达式 或 子查询 ，视图将不支持INSERT，也 不支持UPDATE使用了数学表达式、子查询的字段值；
- 在定义视图的SELECT语句后的字段列表中使用 DISTINCT 、 聚合函数 、 GROUP BY 、 HAVING 、 UNION 等，视图将不支持INSERT、UPDATE、DELETE； 
- 在定义视图的SELECT语句中包含了子查询，而子查询中引用了FROM后面的表，视图将不支持 INSERT、UPDATE、DELETE； 
- 视图定义基于一个不可更新视图 ； 
- 常量视图。

---

### 5、修改|删除视图<a id="2.5">💛</a>

#### 5.1、修改视图

##### 1、方式一

> **==OR REPLACE==**

```sql

# 方式一
CREATE OR REPLACE VIEW vu_emp_s_1
AS
SELECT *
FROM emp_s
WHERE salary > 7000;
```

##### 2、方式二

> **==ALTER VIEW==**

```sql
# 方式二
ALTER VIEW vu_emp_s_2
    AS
        SELECT employee_id, last_name
        FROM emp_s
        WHERE salary > 7000;
```

#### 5.2、删除视图

```sql
# 删除视图
DROP VIEW <view_name>;
```

基于视图a、b创建了新的视图c，如果将视图a或者视图b删除，会导致视图c的查询失败。这 样的视图c需要手动删除或修改，否则影响使用。

---

### 6、总结<a id="2.6">💛</a>

#### 6.1、优点

##### 1、操作简单

​	将经常使用的查询操作定义为视图，可以使开发人员不需要关心视图对应的数据表的结构、表与表之间 的关联关系，也不需要关心数据表之间的业务逻辑和查询条件，而只需要简单地操作视图即可，极大简 化了开发人员对数据库的操作。

##### 2、减少数据冗余

​	视图跟实际数据表不一样，它存储的是查询语句。所以，在使用的时候，我们要通过定义视图的查询语 句来获取结果集。而视图本身不存储数据，不占用数据存储的资源，减少了数据冗余。

##### 3、数据安全

- MySQL将用户对数据的 访问限制 在某些数据的结果集上，而这些数据的结果集可以使用视图来实现。用 户不必直接查询或操作数据表。这也可以理解为视图具有 隔离性 。视图相当于在用户和实际的数据表之 间加了一层虚拟表。
- 同时，MySQL可以根据权限将用户对数据的访问限制在某些视图上，用户不需要查询数据表，可以直接 通过视图获取数据表中的信息。这在一定程度上保障了数据表中数据的安全性。

##### 4、适应灵活多变的需求

​	当业务系统的需求发生变化后，如果需要改动数据表的结构，则工作量相对较 大，可以使用视图来减少改动的工作量。这种方式在实际工作中使用得比较多。

#### 6.2、缺点

##### 1、结构变化

​	如果实际数据表的结构变更了，我们就需要及时对 相关的视图进行相应的维护。特别是嵌套的视图（就是在视图的基础上创建视图），维护会变得比较复 杂， 可读性不好 ，容易变成系统的潜在隐患。因为创建视图的 SQL 查询可能会对字段重命名，也可能包 含复杂的逻辑，这些都会增加维护的成本。

##### 2、维护成本高

​	实际项目中，如果视图过多，会导致数据库维护成本的问题。

#### 6.3、建议

​	虽然可以更新视图数据，但总的来说，视图作为虚拟表 ，主要用于方便查询 ，不建议更新视图的数据。对视图数据的更改，都是通过对实际数据表里数据的操作来完成的。

---

[<!--返回目录-->](#2)

[<!--返回总目录-->](#0)

**[返回上一页🥣](typora://app/README.md)**