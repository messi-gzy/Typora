# 基本命令

## 登陆

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

#### 1、显示所有数据库

```sql
show databases;
```

#### 2、显示数据库中的所有表

```sql
use [databaseName];
show tables;
```

#### 3、添加和删除数据库

```sql
create database if not exists [databseName] default character set utf8mb4;
```

```sql
drop database [databseName];
```

#### 4、连接数据库

```sql
use [databaseName];
```

#### 5、查看当前使用数据库

- ```sql
  select database();
  ```

- ```sql
  status;
  ```

#### 6、导入sql文件

```sql
use [databseName];
source [path/xxx.sql];
```

## 表操作

#### 1、显示表的结构

```sql
describe [tableName];
## or
desc [tableName];
```

#### 2、新建和删除表

```sql
create table if not exists [tableName];
drop table [tableName];
```

#### 3、建表语句

```sql
show create table [tableName];
```

#### 4、清空表中记录

```sql
delete from [tableName];
```

