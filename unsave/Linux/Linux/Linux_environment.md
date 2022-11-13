# Linux环境部署+项目部署

## 一、Linux部署JAVA

##### 1、下载jdk

- 官网：
  
  > https://download.oracle.com/java/18/latest/jdk-18_linux-x64_bin.tar.gz

- 百度网盘：
  
  > 链接：https://pan.baidu.com/s/1p9jmzqHA7Yrx7yaVsK-h0g 
  > 提取码：0s12 
  > --来自百度网盘超级会员V1的分享

##### 2、利用ftp软件将压缩包上传到服务器

​    目录（我这里放到了root目录下）

​    之后再 /usr/local/目录下新建java目录

```
cd /usr/local/
mkdir java
```

##### 3、解压jdk压缩包

```
tar -zxvf /root/jdk-jdk-8U331-Linux-64.tar.gz -C /usr/local/java 
```

##### 4、配置环境

```
vim /etc/profile
```

点击i，在文件末尾输入以下内容

```
JAVA_HOME=/usr/local/java/jdk1.8.0_311
JRE_HOME=/usr/local/java/jdk1.8.0_311/jre
CLASSPATH=$JAVA_HOME/lib/
PATH=$PATH:$JAVA_HOME/bin
export PATH JAVA_HOME JRE_HOME CLASSPATH
```

输入后按Esc，再输入（**：wq**）后回车（保存并退出）

```
source /etc/profile
```

安装完成

检查

```
java -version
javac
```

![](https://pic.imgdb.cn/item/629635460947543129d2a036.png)

<img src="https://pic.imgdb.cn/item/629635460947543129d2a052.png" style="zoom: 50%;" />

成功！！！

## 二、tomcat部署配置

##### 1、下载压缩包

- 官网：
  
  > https://dlcdn.apache.org/tomcat/tomcat-10/v10.0.20/bin/apache-tomcat-10.0.20.tar.gz

- 百度网盘：
  
  > 链接：https://pan.baidu.com/s/1iIi9Ac_SPkkgGSOab2rlzw 
  > 提取码：tkvt 
  > --来自百度网盘超级会员V1的分享

##### 2、利用ftp软件将压缩包上传到服务器

​    目录（我这里放到了root目录下）

​    之后再 /usr/local/目录下新建tomcat目录

```
cd /usr/local/
mkdir tomcat
```

##### 3、解压apache-tomcat压缩包

```
tar -zxvf apache-tomcat-10.0.20.tar.gz(/*按tab键自动补全*/) -C /usr/local/tomcat
```

##### 4、防火墙设置

```
firewall-cmd --state //查看防火墙设置
        {
        running:已启动
        not running:已关闭
        }
systemctl start firewalld //启动防火墙
systemctl enable firwalld.service//设置开机自启防火墙
firewall-cmd --reload//重启防火墙

firewall-cmd --zone=public --add-port=8080/tcp --permanent //开放端口

netstat -tnlp
```

- 查看tomcat默认端口（若需要修改默认端口选择此方法）
  
  > ```
  > vim /usr/local/tomcat/apache-tomcat-10.0.20/conf/server.xml
  > ```
  
  查看<Connector post=“8080”，修改post，
  
  按Esc，输入（**：wq**）保存并退出

- 查看防火墙信息，若关闭状态则开启防火墙

- 开放端口

- 重启防火墙

- 再服务器控制台网页开启端口 TCP 8080 端口
  
  （可以同时开启TCP 23端口）

- 重启防火墙

##### 5、开启tomcat

> ```
> cd /usr/local/tomcat/apache-tomcat-10.0.20/bin/
> ./startup.sh
> ```

##### 6、查看监听端口

```
netstat -tnlp
```

显示8080

##### 7、在浏览器中输入自已服务器的IP地址：8080/

显示tomcat启动页则部署成功

![](https://pic.imgdb.cn/item/6296357f0947543129d2e4c3.png)

##### 8、关闭tomcat

```
cd /usr/local/tomcat/apache-tomcat-10.0.20/bin/
./shutdown.sh
```

##### 9、配置快捷键并开机自启动

- ⾸先进⼊/etc/rc.d/init.d ⽬录，创建⼀个名为tomcat 的⽂件，并赋予执⾏权限
  
  > ```
  > cd /etc/rc.d/init.d/
  > touch tomcat
  > chmod +x tomcat
  > ```

- 编辑tomcat
  
  > ```sh
  > vim tomcat
  > 
  > 写入
  > #!/bin/bash
  > # description: Tomcat Start Stop Restart
  > # processname: tomcat
  > # chkconfig: 2345 20 80
  > #idea - tomcat config start 
  > #!/bin/bash
  > # description: Tomcat Start Stop Restart
  > # processname: tomcat
  > # chkconfig: 2345 20 80
  > JAVA_HOME=/usr/local/java/jdk1.8.0_311
  > export JAVA_HOME
  > PATH=$JAVA_HOME/bin:$PATH
  > export PATH
  > CATALINA_HOME=/usr/local/tomcat/apache-tomcat-10.0.20
  > case $1 in
  > start)
  > sh $CATALINA_HOME/bin/startup.sh
  > ;;
  > stop)
  > sh $CATALINA_HOME/bin/shutdown.sh
  > ;;
  > restart)
  > sh $CATALINA_HOME/bin/shutdown.sh
  > sh $CATALINA_HOME/bin/startup.sh
  > ;;
  > esac
  > exit 0
  > #chmod 755 tomcat
  > #chkconfig --add tomcat
  > #chkconfig --level 2345 tomcat on
  > 
  > ：wq  保存并退出
  > ```

- 快捷键启动
  
  > ```
  > service tomcat start
  > service tomcat stop
  > ```

- 开机自启动
  
  > ```
  > chkconfig --add tomcat
  > chkconfig tomcat on
  > ```

##### 10、拓展

如果想要生成其他文件的直链链接

在**tomcat**的**webapps**文件下

webapps/test/test.png

浏览器访问 **ip+：8080/test/test.png**

## 三、MySQL

### 1、5.7

##### 1、检查

卸载系统⾃带的MARIADB（如果有）

```
rpm -qa|grep mariadb
```

<img src="https://pic.imgdb.cn/item/629636920947543129d45275.png" style="zoom:50%;" />

如果有，就

```
yum -y remove mariadb-server-5.5.56-2.el7.x86_64
yum -y remove mariadb-5.5.56-2.el7.x86_64
yum -y remove mariadb-devel-5.5.56-2.el7.x86_64
yum -y remove mariadb-libs-5.5.56-2.el7.x86_64
.......
```

##### 2、下载并上传

> 官网：[MySQL :: Download MySQL Community Server](https://dev.mysql.com/downloads/mysql/5.7.html#download)
> 
> <img src="https://pic.imgdb.cn/item/629636920947543129d45285.png" style="zoom: 67%;" />

上传并创建文件夹

```
/*上传目录*/
/usr/local/file 
/*创建*/
cd /usr/local
mkdir mysql
```

##### 3、解压

```
cd /usr/local/file
tar -zxvf mysql-5.7.38-linux-glibc2.12-x86_64.tar.gz -C /usr/local/mysql
```

##### 4、创建mysql用户组和用户

```
groupadd mysql
useradd -r -g mysql mysql
```

##### 5、创建数据存储目录

```
cd /usr/local/mysql
mkdir data
/*赋予访问权限*/
chown mysql:mysql -R /usr/local/mysql/data/
```

##### 6、创建配置文件

```
vim /etc/my.cnf
```

写入->

```properties
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8mb4
socket=/var/lib/mysql/mysql.sock

[mysqld]
skip-name-resolve
#设置3306端⼝
port = 3306
socket=/var/lib/mysql/mysql.sock
# 设置mysql的安装⽬录
basedir=/usr/local/mysql/mysql-5.7.38-linux-glibc2.12-x86_64
# 设置mysql数据库的数据的存放目录
datadir=/usr/local/mysql/data
# 允许最⼤连接数
max_connections=200
# 服务端使⽤的字符集默认为8⽐特编码的latin1字符集
character-set-server=utf8mb4
# 创建新表时将使⽤的默认存储引擎
default-storage-engine=INNODB
log-error=/usr/local/mysql/data/mysql.err
pid-file=/usr/local/mysql/data/mysql.pid

lower_case_table_names=1
max_allowed_packet=16M
```

同时创建文件夹

```
mkdir /var/lib/mysql
chmod 777 /var/lib/mysql
```

##### 7、安装MySQL

###### 1、进入文件

```
cd /usr/local/mysql/mysql-5.7.38-linux-glibc2.12-x86_64/bin/
```

###### 2、初始化

```
./mysqld --initialize --user=mysql --basedir=/usr/local/mysql/mysql-5.7.38-linux-glibc2.12-x86_64/ --datadir=/usr/local/mysql/data
```

- 如果此时提醒 error while loading....libaio.so.1 .....
  
  <img src="https://pic.imgdb.cn/item/629636a10947543129d466b7.png" style="zoom:150%;" />

- 原因缺少libaio包
  
  下载即可
  
  但是yum下载默认为32位的，还是会出错

- 安装64位
  
  ![](https://pic.imgdb.cn/item/629636a10947543129d466c1.png)
  
  ```
  yum search libaio
  yum install libaio-devel.x86_64 -y
  ```

###### 3、检查密码

```
cat /usr/local/mysql/data/mysql.err
```

<img src="https://pic.imgdb.cn/item/629636920947543129d45290.png"  />

==**一定记住这个密码哦！！！**==

==**一定记住这个密码哦！！！**==

==**一定记住这个密码哦！！！**==

###### 4、复制文件

```
cp /usr/local/mysql/mysql-5.7.38-linux-glibc2.12-x86_64/support-files/mysql.server /etc/init.d/mysql
```

###### 5、修改文件

```
vim /etc/init.d/mysql
```

修改其***basedir*** 和***datadir*** 为实际对应⽬录

<img src="https://pic.imgdb.cn/item/629636920947543129d45299.png" style="zoom: 67%;" />

##### 8、设置MYSQL系统服务

###### 1、⾸先增加mysql 服务控制脚本执⾏权限

```
chmod +x /etc/init.d/mysql
```

###### 2、同时将mysqld 服务加⼊到系统服务

```
chkconfig --add mysql
```

###### 3、最后检查mysqld 服务是否已经⽣效即可

```
chkconfig --list mysql
```

![](https://pic.imgdb.cn/item/629636920947543129d4526e.png)

服务注册完成

##### 9、启动MySQL

```
service mysql start
```

![](https://pic.imgdb.cn/item/6296369a0947543129d45d87.png)

**==启动成功==**

##### 10、添加环境变量

> （方便全局使用mysql命令行）

```
vim ~/.bash_profile
```

末尾添加

```
export PATH=$PATH:/usr/local/mysql/mysql-5.7.38-linux-glibc2.12-x86_64/bin
```

![](https://pic.imgdb.cn/item/6296369a0947543129d45d8d.png)

生效环境变量

```
source ~/.bash_profile
```

##### 11、登录MySQL

​    1、登录

```
mysql -u root -p
```

![](https://pic.imgdb.cn/item/6296369a0947543129d45d96.png)

密码是之前保存的随机密码

显示如上表示成功

###### 2、修改root密码

继续在命令行执行

```
alter user user() identified by "666666";
flush privileges;
```

![](https://pic.imgdb.cn/item/6296369a0947543129d45dae.png)

###### 3、设置远程连接

继续在命令行操作

```
use mysql
update user set user.Host='%' where user.User='root';
flush privileges;
```

![](https://pic.imgdb.cn/item/6296369a0947543129d45d7b.png)

==**Ctrl+D**退出命令行==

###### 4、远程测试

工具连接

DataGrip：

![](https://pic.imgdb.cn/item/629636a10947543129d466a1.png)

连接成功！！！

<img src="https://pic.imgdb.cn/item/629636a10947543129d466ad.png" style="zoom:150%;" />

**安装完成！！！！**

----

### 2、8.0+

> **如果安装过请先卸载，卸载看下一个标题**

##### 2.1、卸载

卸载系统⾃带的MARIADB（如果有）

```
rpm -qa|grep mariadb
```

<img src="https://pic.imgdb.cn/item/629636920947543129d45275.png" style="zoom:50%;" />

如果有，就

```
yum -y remove mariadb-server-5.5.56-2.el7.x86_64
yum -y remove mariadb-5.5.56-2.el7.x86_64
yum -y remove mariadb-devel-5.5.56-2.el7.x86_64
yum -y remove mariadb-libs-5.5.56-2.el7.x86_64
.......
```

##### 2.2、下载并上传

###### 1、下载

[官网](https://downloads.mysql.com/archives/community/)

<img src="https://pic1.imgdb.cn/item/633e652b16f2c2beb1758ae0.png" style="zoom: 100%;" />

###### 2、上传

通过ftp工具上传到**`/usr/loacl/mysql`**目录下

###### 3、解压

```shell
cd /usr/local/mysql
#解压
tar -xvf mysql-8.0.28-1.el7.x86_64.rpm-bundle.tar -C /usr/local/mysql
```

##### 2.3、安装

###### 1、授予权限

由于mysql安装过程中，会通过mysql用户在/tmp目录下新建tmp_db文件，所以请给/tmp较大的权限。执 行 ：

```
chmod -R 777 /tmp
```

###### 2、安装依赖

- ```shell
  yum install libaio-devel.x86_64 -y
  ```

- ```shell
  yum install net-tools -y
  ```

- ```shell
  yum install -y perl-Module-Install.noarch
  ```

- ```shell
  yum remove mysql-libs
  ```

###### 3、rpm安装

```shell
cd /usr/local/mysql
#安装
```

**==这里安装必须按下面的顺序依次安装，不要打乱==**

```shell
rpm -ivh mysql-community-common-8.0.28-1.el7.x86_64.rpm 
rpm -ivh mysql-community-client-plugins-8.0.28-1.el7.x86_64.rpm 
rpm -ivh mysql-community-libs-8.0.28-1.el7.x86_64.rpm 
rpm -ivh mysql-community-client-8.0.28-1.el7.x86_64.rpm 
rpm -ivh mysql-community-icu-data-files-8.0.28-1.el7.x86_64.rpm
rpm -ivh mysql-community-server-8.0.28-1.el7.x86_64.rpm
```

###### 4、查看信息

```shell
mysql --version
##or
mysqladmin --version
```

如果显示版本信息，代表安装成功

![](https://pic1.imgdb.cn/item/633e69a816f2c2beb17d0477.png)

##### 2.4、初始化

###### 1、初始化

```shell
mysqld --initialize --user=mysql
```

###### 2、查看密码

```shell
cat /var/log/mysqld.log
```

![](https://pic1.imgdb.cn/item/633e7fcd16f2c2beb1a4e0b9.png)

**==记录这个密码==**

###### 3、启动服务

```shell
systemctl start mysqld
```

> 查看服务状态
> 
> ```
> systemctl status mysqld
> ```
> 
> ![](https://pic1.imgdb.cn/item/633e804516f2c2beb1a5c5bf.png)

> 查看是否为自启动
> 
> ```bash
> systemctl list-unit-files|grep mysqld.service
> ```
> 
> ![](https://pic1.imgdb.cn/item/633e809d16f2c2beb1a667bc.png)
> 
> - 如不是enabled可以运行如下命令设置自启动
>   
>   ```
>   systemctl enable mysqld.service
>   ```

##### 2.5、登陆

###### 1、登陆

```
mysql -u root -p
```

输入之前记录下的密码

###### 2、修改密码

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY '新的密码';
```

> 密码太简单可能会报错

###### 3、允许远程连接

依次执行三条语句

```sql
use mysql;
###
update user set user.Host='%' where user.User='root';
###
flush privileges;
```

**==记得开放3306端口==**

```
firewall-cmd --zone=public --add-port=3306/tcp --permanent
firewall-cmd --reload  //重启防火墙
```

---

### 3、卸载

##### 1、卸载系统⾃带的MARIADB（如果有）

```
rpm -qa|grep mariadb
```

<img src="https://pic.imgdb.cn/item/629636920947543129d45275.png" style="zoom:50%;" />

如果有，就

```
yum -y remove mariadb-server-5.5.56-2.el7.x86_64
yum -y remove mariadb-5.5.56-2.el7.x86_64
yum -y remove mariadb-devel-5.5.56-2.el7.x86_64
yum -y remove mariadb-libs-5.5.56-2.el7.x86_64
.......
```

##### 2、关闭mysql服务

```shell
systemctl stop mysqld.service
```

> ```shell
> #查看服务状态
> systemctl status mysqld.service
> ```

##### 3、卸载其他版本的MySQL

> ###### 通过rpm安装的卸载
> 
> ```
> rpm -qa | grep - i mysql
> ```
> 
> ![](https://pic1.imgdb.cn/item/633e5f3616f2c2beb16b0f13.png)
> 
> 全部删除：
> 
> ```
> yum remove mysql-community-libs-8.0.25-1.e17.x86_64
> ......
> ```

##### 4、删除mysql相关文件

- 查找文件

```shell
find / -name mysql
```

- 删除文件

删除所有查找出来的文件

```
rm -rf [...]
```

##### 5、删除配置文件

```shell
rm -rf /etc/my.cnf
```

## 四、Nginx

##### 1、下载并上传到服务器

> 官网：
> 
> https://nginx.org/en/download.html

位置：/root

##### 2、解压

```
cd /usr/local
mkdir nginx
```

```
cd /root
tar -zxvf nginx-1.21.6.tar.gz -C /usr/local/nginx/
```

##### 3、配置编译幻境

###### 1、安装 gcc

```
yum install gcc-c++
```

<img src="https://pic.imgdb.cn/item/629635f60947543129d39773.png" style="zoom: 67%;" />

###### 2、安装 pcre-devel

```
yum install -y pcre pcre-devel
```

###### 3、安装 zlib

```
yum install -y zlib zlib-devel
```

###### 4、安装 Open SSL

```
yum install -y openssl openssl-devel
```

##### 4、编译安装

```
 cd /usr/local/nginx/nginx-1.21.6/
 ./configure
 make
 make install
```

==如果https支持==
 ==在输入 ./configure   应该为 ./configure --with-http_ssl_module==

编译结束后可执行文件在

```
/usr/local/nginx/sbin/nginx
```

##### 5、启动Nginx

###### 1、启动

```
/usr/local/nginx/sbin/nginx
```

###### 2、停止

```
/usr/local/nginx/sbin/nginx -s stop
```

###### 3、重启

```
/usr/local/nginx/sbin/nginx -s reload
```

###### 4、查看进程

```
ps aux|grep nginx
```

配置文件路径

```
/usr/local/nginx/conf/nginx.conf
```

###### 5、设置开机自启

```
vim /etc/rc.local

###底部写入

/usr/local/nginx/sbin/nginx
```

![](https://pic.imgdb.cn/item/629635f60947543129d3974f.png)

###### 6、记得开放端口

开往网络安全组和端口

```
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --reload  //重启防火墙
```

![](https://pic.imgdb.cn/item/629635f60947543129d39755.png)

访问成功

**安装完成！！！**

## 五、Go环境配置

##### 1、下载Go安装包

> 官网：[Downloads - The Go Programming Language (google.cn)](https://golang.google.cn/dl/)
> 
> 下载包：https://golang.google.cn/dl/go1.18.2.linux-amd64.tar.gz

上传到服务器

##### 2、解压

- 在/usr/local 下新建 go文件架
  
  ```
  mkdir go
  ```

- 切换到Go安装包路径

- 解压
  
  ```
  tar -zxvf go1.18.2.linux-amd64.tar.gz -C /usr/local/go
  ```

##### 3、建立工作目录

> 官方建议放在 /home/go 下，创建三个目录：bin（编译后可的执行文件的存放路径）、pkg（编译包时，生成的.a文件的存放路径）、src（源码路径，一般我们的工程就创建在src下面）
> 
> ![](https://pic.imgdb.cn/item/629633c70947543129d071c5.png)

```
mkdir -p /home/go/bin /home/go/pkg /home/go/src
```

##### 4、配置环境变量

```
vim /etc/profile
```

```shell
export GOROOT=/usr/local/go/go
export GOPATH=/home/go
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```

![](https://pic.imgdb.cn/item/629633c70947543129d071c9.png)

```
source /etc/profile
```

##### 5、检查

- 版本信息

```
go version
```

![](https://pic.imgdb.cn/item/629633c70947543129d071db.png)

- 配置信息

```
go env
```

<img src="https://pic.imgdb.cn/item/629633c70947543129d071e8.png" style="zoom: 50%;" />

**安装完成！！！**

## 六、Python环境配置

CentOS 7.4 默认⾃带了⼀个Python2.7 环境，再装⼀个Python3 ，打造⼀个共存的环境。

![](https://pic.imgdb.cn/item/628f7287094754312959648c.png)

##### 1、下载

> 官网：[Python Release Python 3.10.4 | Python.org](https://www.python.org/downloads/release/python-3104/)
> 
> ![](https://pic.imgdb.cn/item/628f72870947543129596493.png)

##### 2、解压

```
cd /usr/local
mkdir python
```

```
cd /root
tar -zxvf Python-3.10.4.tgz -C /usr/local/python/
```

##### 3、安装相关预备环境

```
yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-develgcc make
```

##### 4、编译

- 安装目录

```
cd /usr/local/python
mkdir python3
```

- 编译安装

```
cd /usr/local/python/Python-3.10.4
```

```
./configure --prefix=/usr/local/python/python3
```

![](https://pic.imgdb.cn/item/628f7287094754312959649d.png)

- 安装

```
make && make install
```

编译完成！！！

##### 5、验证安装

```
/usr/local/python/python3/bin/python3
```

![](https://pic.imgdb.cn/item/628f72870947543129596488.png)

***ctrl+D*** 退出

##### 6、建立软连接

```
ln -s /usr/local/python/python3/bin/python3 /usr/bin/python3
ln -s /usr/local/python/python3/bin/pip3 /usr/bin/pip3
```

##### 7、检查

```
python3
```

![](https://pic.imgdb.cn/item/628f72870947543129596484.png)

安装完成！！！！

## 七、Node.js 配置

##### 1、下载

> 官网：
> 
> http://nodejs.cn/download/
> 
> ![](https://pic.imgdb.cn/item/629771ca0947543129136f64.png)

##### 2、解压

```
mkdir /usr/local/node
tar -xvf node-v16.15.0-linux-x64.tar.xz -C /usr/local/node
mv /usr/local/node/node-v16.15.0-linux-x64 /usr/local/node/node
```

##### 3、配置环境变量

```
vim /etc/profile
```

```
export PATH=/usr/local/node/node/bin:$PATH
```

![](https://pic.imgdb.cn/item/629773a509475431291635d3.png)

##### 4、检查

```
node -v
npm version
npx -v
```

![](https://pic.imgdb.cn/item/62977405094754312916e5dc.png)

## 八、CMake

#### 1、下载

- [官网](https://cmake.org/download/)【https://cmake.org/download/】
- 任意路径下下载

```bash
wget https://github.com/Kitware/CMake/releases/download/v3.24.2/cmake-3.24.2.tar.gz
```

#### 2、解压

```shell
tar -zxvf cmake-3.24.2.tar.gz -C /usr/local/cmake
```

#### 3、编译

- 【1】

```bash
cd /usr/local/cmake/cmake-3.24.2
```

- 【2】

```shell
yum install -y gcc gcc-c++ make automake
# 这步一定要做，不然后续./bootstrap会报错
yum install -y openssl openssl-devel 
```

- 【3】

```
./bootstrap
```

- 【4】

```
gmake
```

```
gmake install
```

## 九、GCC

#### 1、直接安装

- GCC

```bash
sudo yum install gcc
```

- G++

```bash
sudo yum install gcc-cc++
```

- 

```bash
sudo yum install autoconf make
```

#### 2、更高版本

- ```bash
  sudo yum install centos-release-scl
  ```

- ```bash
  sudo yum install devtoolset-9-gcc devtoolset-9-gcc-c++ devtoolset-9-binutils
  ```

  > `注意`：其中的数字可以更改为指定大版本

- 激活**devtoolset**

  ```bash
  scl enable devtoolset-9 bash
  ```

  > `注意`：可以激活指定版本的gcc

- 写入环境

  > `注意`：scl命令只是临时，关闭终端后会恢复原版本，可写入环境，解决

  ```shell
  echo "source /opt/rh/devtoolset-9/enable" >>/etc/profile
  ```

==**注意在所有语句中自已安装的对应版本号 **==
