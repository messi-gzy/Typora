# 基本命令

## 登陆

<a id="1"><!--登陆--></a>

#### 1、基本登陆

```bash
mysql -u root -p
```

```shell
# -h：MySQL服务器的ip地址或主机名；
# -u：连接MySQL服务器的用户名；
# -e：执行mysql内部命令；
# -p：连接MySQL服务器的密码。
```

#### 2、修改密码

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY '新的密码';
```

#### 3、允许远程连接

```sql
use mysql;
###
update user set user.Host='%' where user.User='root';
###
flush privileges;
```

#### 4、安装

- Windows   ......
- Liunx  [CentOS](../../Linux/Linux/Linux_environment.md)

#### 5、服务启动

- Windows

```powershell
net start mysql
net stop mysql
```

- CentOS

```shell
syatemctl start mysql
systemctl stop mysql
systemctl status mysql
systemctl restart mysql
```

#### 6、新增新用户

##### 6.1、用户授权

```sql
grant 权限 on 数据库.* to 用户名@登录主机 identified by "密码";
flush privileges;
```

`举例`

> ```sql
> grant select,insert,update,delete on . to user@localhost Identified by “password”;
> ```
>
> 如果希望该用户能够在任何机器上登陆mysql，**则将localhost改为\"%\"**。

##### 6.2、新增用户

```sql
create user [username]@[host] identified by [password];
```

`举例`

> ```sql
> create user ubuntu@localhost identified by 'ubuntu';
> ```
>
> 如果希望该用户能够在任何机器上登陆mysql，**则将localhost改为\"%\"**。

#### 7、退出

```sql
exit；
## or
quit;
```

## 数据库操作

<a id="2"><!--数据库操作--></a>

#### 1、显示所有数据库

```sql
show databases;
```

#### 2、显示数据库中的所有表

```sql
use [databaseName]; -- 切换数据库
show tables;
```

#### 3、添加和删除数据库

- ```sql
  create database if not exists [databseName] default character set utf8mb4;
  ```


- ```sql
  drop database [databseName];
  ```


#### 4、连接数据库

```sql
use [databaseName];
```

#### 5、查看当前使用数据库

```sql
select database();
```

#### 6、查看数据库的创建信息

```sql
SHOW CREATE DATABASE [数据库名]; 
-- or 
SHOW CREATE DATABASE [数据库名]\G;
```

#### 7、导入sql文件

```sql
use [databseName];
source [path/xxx.sql];
```

#### 8、修改信息

> 修改数据库的字符集

```sql
ALTER DATABASE [数据库名] CHARACTER SET [字符集]; -- gbk、utf8...
```

## 表操作

<a id="3"><!--表操作--></a>

#### 1、显示表的结构

```sql
describe [tableName];
## or
desc [tableName];
```

#### 2、新建和删除表

```sql
create table [if not exists] [tableName];
drop table [tableName];
```

```sql
CREATE TABLE [IF NOT EXISTS] [表名]( 
        字段1, 数据类型 [约束条件] [默认值], 
        字段2, 数据类型 [约束条件] [默认值], 
        字段3, 数据类型 [约束条件] [默认值], 
        …… [表约束条件]
);
```

#### 3、建表语句

```sql
show create table [tableName];
```

#### 4、清空表

> 只清空数据，不清空表的结构

```sql
TRUNCATE TABLE [tableName];
```

#### 5、修改表

##### 5.1、添加字段

```sql
ALTER TABLE [表名] ADD [COLUMN]<TYPE> [FIRST|AFTER <字段名>];
```

##### 5.2、修改字段

```sql
ALTER TABLE [表名] MODIFY [COLUMN]<TYPE> [DEFAULT 默认值][FIRST|AFTER <字段名 2>];
```

##### 5.3、重命名字段

```sql
ALTER TABLE [表名] CHANGE [column] [新列名] <新数据类型>;
```

##### 5.4、删除字段

```sql
ALTER TABLE [表名] DROP [COLUMN]
```

#### 6、重命名表

- ```sql
  RENAME TABLE [原名] TO [新名];
  ```

- ```sql
  ALTER table [原名] RENAME [TO] [新名]; -- [TO]可以省略
  ```

## [返回🥣](../README.md)
