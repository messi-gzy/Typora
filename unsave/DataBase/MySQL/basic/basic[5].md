# [基础]5

- $\textcolor{#e18a3b}{【一】}$**[单行函数](#1)**
- $\textcolor{#e18a3b}{【二】}$**[聚合函数](#2)**

## 一、单行函数

<a id="1">**<!--目录-->**</a>

- $\textcolor{#2a6e3f}{【1】}$ [函数的理解](#1.1)
- $\textcolor{#2a6e3f}{【2】}$ [数值函数](#1.2)
- $\textcolor{#2a6e3f}{【3】}$ [字符串函数](#1.3)
- $\textcolor{#2a6e3f}{【4】}$ [日期和时间函数](#1.4)
- $\textcolor{#2a6e3f}{【5】}$ [流程控制函数](#1.5)
- $\textcolor{#2a6e3f}{【6】}$ [加密解密函数](#1.6)
- $\textcolor{#2a6e3f}{【7】}$ [信息函数](#1.7)
- $\textcolor{#2a6e3f}{【8】}$ [其他函数](#1.8)

---

### 1、函数的理解<a id="1.1">💚</a>

#### 1.1、函数

​    函数在计算机语言的使用中贯穿始终，函数的作用是什么呢？它可以把我们经常使用的代码封装起来， 需要的时候直接调用即可。这样既**提高了代码效率** ，**又提高了可维护性** 。在 `SQL`中我们也可以**使用函数对检索出来的数据进行函数操作**。使用这些函数，可以极大地 提高用户对数据库的管理效率 。

#### 1.2、不同DBMS函数的差异

​    `DBMS` 之间的差异性很大，远大于同一个语言不同版本之间的差异。实际上，只有很少的函数是 被 `DBMS` 同时支持的。比如，大多数 `DBMS` 使用（||）或者（+）来做拼接符，而在 `MySQL` 中的字符串拼 接函数为`concat()`。大部分 `DBMS` 会有自己特定的函数，**这就意味着采用 SQL 函数的代码可移植性是很差的**，因此在使用函数的时候需要特别注意。

#### 1.3、MySQL内置函数

​    `MySQL`提供的内置函数从实现的功能角度可以分为==数值函数==、==字符串函数==、==日期和时间函数==、==流程控制函数==、==加密与解密函数==、获取`MySQL`==信息函数==、==聚合函数==等。这里，我将这些丰富的内置函数再分为两 类： ==单行函数== 、 ==聚合函数==（或分组函数） 。

> 单行函数可以嵌套

---

### 2、数值函数<a id="1.2">💚</a>

#### 2.1、基本函数

|        函数         | 作用                                                         |
| :-----------------: | ------------------------------------------------------------ |
|       ABS(x)        | 返回x的绝对值                                                |
|       SIGN(x)       | 返回X的符号。正数返回1，负数返回-1，0返回0                   |
|        PI()         | 返回圆周率的值                                               |
| CEIL(x).CEILING(x)  | 返回大于或等于某个值的最小整数                               |
|      FLOOR(x)       | 返回小于或等于某个值的最大整数                               |
|  LEAST(e1,e2,...)   | 返回列表中的最小值                                           |
| GREATEST(e1,e2,...) | 返回列表中的最大值                                           |
|      MOD(x,y)       | 返回X除以Y后的余数                                           |
|       RAND()        | 返回0~1的随机值                                              |
|       RAND(x)       | 返回0~1的随机值，其中x的值用作种子值，相同的X值会产生相同的随机 数 |
|      ROUND(x)       | 返回一个对x的值进行四舍五入后，最接近于X的整数               |
|     ROUND(x,y)      | 返回一个对x的值进行四舍五入后最接近X的值，并保留到小数点后面Y位 |
|    TRUNCATE(x,y)    | 返回数字x截断为y位小数的结果                                 |
|       SQRT(x)       | 返回x的平方根。当X的值为负数时，返回NULL                     |
|   FORMAT(value,n)   | 返回对数字value进行格式化后的结果数据。n表示 四舍五入 后保留 到小数点后n位 |

#### 2.2、角度与弧度

> **==1弧度：弧长等于半斤的长度，其对应的圆心角的大小==**

| 函数         | 用法                  |
|:----------:| ------------------- |
| RADIANS(x) | 将角度转化为弧度，其中，参数x为角度值 |
| DEGREES(x) | 将弧度转化为角度，其中，参数x为弧度值 |

#### 2.3、三角函数

| 函数         | 作用                                       |
|:----------:| ---------------------------------------- |
| SIN(x)     | 返回x的正弦值，其中，参数x为弧度值                       |
| ASIN(x)    | 返回x的反正弦值，即获取正弦为x的值。如果x的值不在-1到1之间，则返回NULL |
| COS(x)     | 返回x的余弦值，其中，参数x为弧度值                       |
| ACOS(x)    | 返回x的反余弦值，即获取余弦为x的值。如果x的值不在-1到1之间，则返回NULL |
| TAN(x)     | 返回x的正切值，其中，参数x为弧度值                       |
| ATAN(x)    | 返回x的反正切值，即返回正切值为x的值                      |
| ATAN2(m,n) | 返回两个参数的反正切值                              |
| COT(x)     | 返回x的余切值，其中，X为弧度值                         |

#### 2.4、指数与对数

| 函数                  | 作用                                 |
|:-------------------:| ---------------------------------- |
| POW(x,y),POWER(x,y) | 返回x的y次方                            |
| EXP(x)              | 返回e的X次方，其中e是一个常数，2.718281828459045 |
| LN(x),LOG(x)        | 返回以e为底的X的对数，当X <= 0 时，返回的结果为NULL   |
| LOG10(x)            | 返回以10为底的X的对数，当X <= 0 时，返回的结果为NULL  |
| LOG2(x)             | 返回以2为底的X的对数，当X <= 0 时，返回NULL       |

#### 2.5、进制转换

|        函数         | 作用                              |
| :-----------------: | --------------------------------- |
|       BIN(x)        | 返回x的二进制编码                 |
|       HEX(x)        | 返回x的十六进制编码               |
|       OCT(x)        | 返回x的八进制编码                 |
|    CONV(x,f1,f2)    | 返回f1进制数变成f2进制数          |
| CONV(value,from,to) | 将value的值进行不同进制之间的转换 |

---

### 3、字符串函数<a id="1.3">💚</a>

> **==字符串的索引都是从`1`开始的==**

| 函数                             | 作用                                                                                |
|:------------------------------:| --------------------------------------------------------------------------------- |
| ASCII(s)                       | 返回字符串S中的第一个字符的ASCII码值                                                             |
| CHAR_LENGTH(s)                 | 返回字符串s的字符数。作用与CHARACTER_LENGTH(s)相同                                               |
| LENGTH(s)                      | 返回字符串s的字节数，和字符集有关                                                                 |
| CONCAT(s1,s2,....)             | 连接s1,s2,......,sn为一个字符串                                                           |
| CONCAT_WS(x,s1,s2,....)        | 同CONCAT(s1,s2,...)函数，但是每个字符串之间要加上x                                                |
| INSERT(str,idx,len,replacestr) | 将字符串str从第idx位置开始，len个字符长的子串替换为字符串replacestr                                       |
| REPLACE(str,a,b)               | 用字符串b替换字符串str中所有出现的字符串a                                                           |
| UPPER(s) 或 UCASE(s)            | 将字符串s的所有字母转成大写字母                                                                  |
| LOWER(s) 或LCASE(s)             | 将字符串s的所有字母转成小写字母                                                                  |
| LEFT(str,n)                    | 返回字符串str最左边的n个字符                                                                  |
| RIGHT(str,n)                   | 返回字符串str最右边的n个字符                                                                  |
| LPAD(str, len, pad)            | 用字符串pad对str最左边进行填充，直到str的长度为len个字符                                                |
| RPAD(str ,len, pad)            | 用字符串pad对str最右边进行填充，直到str的长度为len个字符                                                |
| LTRIM(s)                       | 去掉字符串s左侧的空格                                                                       |
| RTRIM(s)                       | 去掉字符串s右侧的空格                                                                       |
| TRIM(s)                        | 去掉字符串s开始与结尾的空格                                                                    |
| TRIM(s1 FROM s)                | 去掉字符串s开始与结尾的s1                                                                    |
| TRIM(LEADING s1 FROM s)        | 去掉字符串s开始处的s1                                                                      |
| TRIM(TRAILING s1 FROM s)       | 去掉字符串s结尾处的s1                                                                      |
| REPEAT(str, n)                 | 返回str重复n次的结果                                                                      |
| SPACE(n)                       | 返回n个空格                                                                            |
| STRCMP(s1,s2)                  | 比较字符串s1,s2的ASCII码值的大小                                                             |
| SUBSTR(s,index,len)            | 返回从字符串s的index位置其len个字符，作用与SUBSTRING(s,n,len)、 MID(s,n,len)相同                      |
| LOCATE(substr,str)             | 返回字符串substr在字符串str中首次出现的位置，作用于POSITION(substr IN str)、INSTR(str,substr)相同。未找到，返回0 |
| ELT(m,s1,s2,…,sn)              | 返回指定位置的字符串，如果m=1，则返回s1，如果m=2，则返回s2，如 果m=n，则返回sn                                   |
| FIELD(s,s1,s2,…,sn)            | 返回字符串s在字符串列表中第一次出现的位置                                                             |
| FIND_IN_SET(s1,s2)             | 返回字符串s1在字符串s2中出现的位置。其中，字符串s2是一个以逗号分 隔的字符串                                         |
| REVERSE(s)                     | 返回s反转后的字符串                                                                        |
| NULLIF(value1,value2)          | 比较两个字符串，如果value1与value2相等，则返回NULL，否则返回 value1                                     |

---

### 4、日期和时间函数<a id="1.4">💚</a>

#### 4.1、获取日期、时间

|                             函数                             | 作用                            |
| :----------------------------------------------------------: | :------------------------------ |
|              ==**CURDATE()**==，CURRENT_DATE()               | 返回当前日期，只包含年、 月、日 |
|             ==**CURTIME()**== ， CURRENT_TIME()              | 返回当前时间，只包含时、 分、秒 |
| ==**NOW()**== \| SYSDATE() \| CURRENT_TIMESTAMP() \| LOCALTIME() \|LOCALTIMESTAMP() | 返回当前系统日期和时间          |
|                   UTC_DATE() \| UTC_TIME()                   | 返回UTC（世界标准时间） 日期    |

#### 4.2、时间戳转换

|           函数           | 作用                                   |
| :----------------------: | -------------------------------------- |
|     UNIX_TIMESTAMP()     | 以UNIX时间戳的形式返回当前时间。       |
|   UNIX_TIMESTAMP(date)   | 将时间date以UNIX时间戳的形式返回。     |
| FROM_UNIXTIME(timestamp) | 将UNIX时间戳的时间转换为普通格式的时间 |

> **时间戳：**自 1970 年 1 月 1 日（00:00:00 ）至当前时间的总秒数。

#### 4.3、获取月份等

|                   函数                   | 作用                                   |
| :--------------------------------------: | -------------------------------------- |
|   YEAR(date) / MONTH(date) / DAY(date)   | 返回具体的日期值                       |
| HOUR(time) / MINUTE(time) / SECOND(time) | 返回具体的时间值                       |
|             MONTHNAME(date)              | 返回月份：January，...                 |
|              DAYNAME(date)               | 返回星期几：MONDAY，TUESDAY.....SUNDAY |
|              WEEKDAY(date)               | 返回周几                               |
|              QUARTER(date)               | 返回日期对应的季度，范围为1～4         |
|      WEEK(date) ， WEEKOFYEAR(date)      | 返回一年中的第几周                     |
|             DAYOFYEAR(date)              | 返回日期是一年中的第几天               |
|             DAYOFMONTH(date)             | 返回日期位于所在月份的第几天           |
|             DAYOFWEEK(date)              | 返回周几                               |

#### 4.4、日期操作

|          函数           |                    作用                    |
| :---------------------: | :----------------------------------------: |
| EXTRACT(type FROM date) | 返回指定日期中特定的部分，type指定返回的值 |

![](https://pic1.imgdb.cn/item/6346ce2716f2c2beb11b0341.png)

#### 4.5、时间转换函数

|         函数         | 作用                                                         |
| :------------------: | ------------------------------------------------------------ |
|  TIME_TO_SEC(time)   | 将 time 转化为秒并返回结果值。转化的公式为： ==小时*3600+分钟 *60+秒== |
| SEC_TO_TIME(seconds) | 将 seconds 描述转化为包含小时、分钟和秒的时间                |

#### 4.6、计算函数

##### 1、类型1

|         函数         | 作用                                                         |
| :------------------: | ------------------------------------------------------------ |
|DATE_ADD(datetime, INTERVAL expr type)， ADDDATE(date,INTERVAL expr type)|返回与给定日期时间相差INTERVAL时 间段的日期时间|
|DATE_SUB(date,INTERVAL expr type)， SUBDATE(date,INTERVAL expr type)|返回与date相差INTERVAL时间间隔的 日期|

![](https://pic1.imgdb.cn/item/6346d01b16f2c2beb1219d5e.png)

`举例`

```sql
SELECT DATE_ADD(NOW(), INTERVAL 1 HOUR),NOW()
FROM DUAl;
-- 2022-10-12 23:30:25 --2022-10-12 22:30:25
```

##### 2、类型2

![](https://pic1.imgdb.cn/item/6346d29516f2c2beb1294a7b.png)

#### 4.7、日期格式化

|               函数                | 作用                                       |
| :-------------------------------: | ------------------------------------------ |
|     ==DATE_FORMAT(date,fmt)==     | 按照字符串fmt格式化日期date值              |
|       TIME_FORMAT(time,fmt)       | 按照字符串fmt格式化时间time值              |
|       STR_TO_DATE(str, fmt)       | 按照字符串fmt对str进行解析，解析为一个日期 |
| GET_FORMAT(date_type,format_type) | 返回日期字符串的显示格式                   |

![](https://pic1.imgdb.cn/item/6346d49516f2c2beb12edf7e.png)

`举例`

```sql
SELECT DATE_FORMAT(NOW(), '%H:%i:%s')
FROM DUAL;
-- 22:51:19
```

---

### 5、流程控制函数<a id="1.5">💚</a>

> 流程处理函数可以根据不同的条件，执行不同的处理流程

|                             函数                             | 作用                                             |
| :----------------------------------------------------------: | ------------------------------------------------ |
|                 ==IF(value,value1,value2)==                  | 如果value的值为TRUE，返回value1， 否则返回value2 |
|                    IFNULL(value1, value2)                    | 如果value1不为NULL，返回value1，否 则返回value2  |
| CASE WHEN 条件1 THEN 结果1 WHEN 条件2 THEN 结果2 .... [ELSE resultn] END | 相当于if...else if...else...                     |
| CASE [expr] WHEN 常量值1 THEN 值1 WHEN 常量值1 THEN 值1 .... [ELSE 值n] END | 相当于switch...case...                           |

#### 5.1、IF

```sql
SELECT IF(1>0,'你好','世界')
FROM DUAL;

-- 你好
```

#### 5.2、IFNULL

```sql
SELECT IFNULL(NULL,'世界')
FROM DUAL;

-- 世界
```

#### 5.3、CASE

##### 1、if.....else

```sql
SELECT last_name,
       salary,
       CASE
           WHEN salary >= 10000 THEN '经理'
           WHEN salary BETWEEN 5000 AND 10000 THEN '员工'
           ELSE '海贼' END details,
       department_id
FROM employees;
```

##### 2、switch ....case

```sql
SELECT last_name,
       salary,
       CASE department_id
           WHEN 90 THEN salary * 1.1
           WHEN 60 THEN salary * 1.2
           ELSE salary * 1.3 END details,
       department_id
FROM employees;
```

---

### 6、加密解密函数<a id="1.6">💚</a>

|            函数             | 作用                                                         |
| :-------------------------: | ------------------------------------------------------------ |
|        PASSWORD(str)        | 返回字符串str的加密版本，41位长的字符串。加密结果 不可 逆 ，常用于用户的密码加密，**5.7以上版本不支持** |
|        **MD5(str)**         | 返回字符串str的md5加密后的值，也是一种加密方式。若参数为 NULL，则会返回NULL |
|      ==**SHA(str)**==       | 从原明文密码str计算并返回加密后的密码字符串，当参数为 NULL时，返回NULL。 SHA加密算法比MD5更加安全 。 |
| ENCODE(value,password_seed) | 返回使用password_seed作为加密密码==加密===value,**5.7以上版本不支持** |
| DECODE(value,password_seed) | 返回使用password_seed作为加密密码==解密==value,**5.7以上版本不支持** |

`举例`

```sql
SELECT IF(SHA('world')='7c211433f02071597741e6ff5a8ea34789abbf43','YES','NO')
FROM DUAL;

-- YES
```

### 7、信息函数<a id="1.7">💚</a>

|                          函数                          | 作用                                                      |
| :----------------------------------------------------: | --------------------------------------------------------- |
|                       VERSION()                        | 返回当前MySQL的版本号                                     |
|                    CONNECTION_ID()                     | 返回当前MySQL服务器的连接数                               |
|                  DATABASE()，SCHEMA()                  | 返回MySQL命令行当前所在的数据库                           |
| USER()，CURRENT_USER()、SYSTEM_USER()， SESSION_USER() | 返回当前连接MySQL的用户名，返回结果格式为 “主机名@用户名” |
|                     CHARSET(value)                     | 返回字符串value自变量的字符集                             |
|                    COLLATION(value)                    | 返回字符串value的比较规则                                 |

### 8、其他函数<a id="1.8">💚</a>

|              函数              | 作用                                                         |
| :----------------------------: | ------------------------------------------------------------ |
|       INET_ATON(ipvalue)       | 将以点分隔的IP地址转化为一个数字                             |
|        INET_NTOA(value)        | 将数字形式的IP地址转化为以点分隔的IP地址                     |
|       BENCHMARK(n,expr)        | 将表达式expr重复执行n次。用于测试MySQL处理expr表达式所耗费 的时间 |
| CONVERT(value USING char_code) | 将value所使用的字符编码修改为char_code                       |

**[返回目录](#1)**

## 二、聚合函数

<a id="2">**<!--目录-->**</a>

- $\textcolor{#2a6e3f}{【1】}$ [介绍](#2.1)
- $\textcolor{#2a6e3f}{【2】}$ [聚合函数](#2.2)
- $\textcolor{#2a6e3f}{【3】}$ [GROUP BY](#2.3)
- $\textcolor{#2a6e3f}{【4】}$ [HAVING](#2.4)
- $\textcolor{#2a6e3f}{【5】}$ [SELECT执行过程](#2.5)

### 1、介绍<a id="2.1">💛</a>

​	**聚合（或聚集、分组）函数**，它是对一组数据进行汇总的函数，输入的是一组数据的集合，输出的是单个值。聚合函数**作用于一组数据，并对一组数据返回一个值。**

![](https://pic1.imgdb.cn/item/6347e97516f2c2beb1c36225.png)

> **==聚合函数不能嵌套使用==**

### 2、聚合函数<a id="2.2">💛</a>

**==聚合函数不能嵌套使用==**

#### 2.1、AVG|SUM

|   AVG()   |  求平均值  |
| :-------: | :--------: |
| **SUM()** | **求总合** |

`举例`

```sql
SELECT AVG(salary),SUM(salary),AVG(salary)*107
FROM employees;

-- 6461.682243   691400   691400
```

**==AVG=SUM / COUNT==**

#### 2.2、MIN|MAX

|   MIN()   |   最小值   |
| :-------: | :--------: |
| **MAX()** | **最大值** |

`举例`

```sql
SELECT MIN(salary),MAX(salary)
FROM employees;

-- 2100   24000 
```

#### 2.3、COUNT

> 计算指定字段在查询过程中出现的个数

`举例`

```sql
SELECT COUNT(department_id) num
FROM employees
WHERE department_id<50;
```

- 

- COUNT(*)返回表中记录总数，==**适用于任意数据类型.**==

- **COUNT([expr]) 返回==expr不为空==的记录总数。**

  ==**NULL，为空数据不计算**==

### 3、GROUP BY<a id="2.3">💛</a>

> **可以使用`GROUP BY`子句将表中的数据分成若干组**

#### 3.1、单列

```sql
SELECT AVG(salary) 
FROM employees 
GROUP BY department_id ;
```

#### 3.2、多列

```sql
SELECT department_id, job_id, AVG(salary)
FROM employees
GROUP BY department_id, job_id
ORDER BY department_id DESC ;
```

`结论`

- 在==**SELECT**==列表中**所有未包含在组函数**中的列==**都应该包含在 GROUP BY**==子句中

- **==GROUP BY==中声明的字段可以不出现在==SELECT==**

- **位置**

  ```sql
  SELECT column, group_function(column) 
  FROM table 
  [WHERE condition] 
  [GROUP BY group_by_expression] 
  [ORDER BY column];
  ```

#### 3.3、WITH ROLLUP

​	使用 `WITH ROLLUP` 关键字之后，在所有查询出的分组记录之后**增加一条记录，该记录计算查询出的所 有记录的总和，即统计记录数量。**

`举例`

```sql
SELECT department_id,AVG(salary) 
FROM employees 
WHERE department_id > 80 
GROUP BY department_id WITH ROLLUP;
```

`注意`

​	当使用ROLLUP时，**不能同时使用ORDER BY子句进行结果排序，即ROLLUP和ORDER BY是互相排斥的。**

### 4、HAVING<a id="2.4">💛</a>



### 5、SELECT执行过程<a id="2.5">💛</a>

**[<!--返回目录-->](#2)**

---

## [返回上一页🥣](../../README.md)
