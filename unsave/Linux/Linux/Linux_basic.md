# Linux

`目录`

---

## 1、文件与目录结构

> **Linux 系统中一切皆文件**

![](https://pic.imgdb.cn/item/6310bad216f2c2beb1817df7.png)

---

**目录结构及功能**

![](https://pic.imgdb.cn/item/6310bbdd16f2c2beb182bfad.png)

---

#### 1、/bin

`链接 usr/bin`

> 可执行的二进制文件，如系统自带的 `cd` `ls` `cat` 等。

#### 2、/sbin

`链接 /usr/sbin`

> 放置**系统管理员使用的可执行命令**，如`fdisk`、`shutdown`、`mount` 等。与 <u>/bin 不同的是</u>，这几个目录是系统管理员 ***<u>root</u>***使用的命令，**一般用户只能\"查看\"而不能设置和使用**。

#### 3、/lib

`链接 /usr/lib`

> 系统使用的**<u>函数库的目录</u>**，程序在执行过程中，需要调用一些额外的参数时需要函数库的协助。

---

#### 4、/boot

> 放置linux系统**启动**时用到的一些文件，如***Linux的内核文件***：**<u>/boot/vmlinuz</u>**，系统引导管理器：**<u>/boot/grub</u>**。

#### 5、/dev

> 存放**<u>linux系统下的设备文件</u>**，*访问该目录下某个文件，相当于访问某个设备*，常用的是挂载光驱 mount /dev/cdrom /mnt。

#### 6、/etc

> **<u>系统配置文件存放的目录</u>**，不建议在此目录下存放可执行文件，重要的配置文件有 /etc/inittab、/etc/fstab、/etc/init.d、/etc/X11、/etc/sysconfig、/etc/xinetd.d。

#### 7、/home

> 系统默认的用户家目录，新增用户账号时，用户的家目录都存放在此目录下,表示当前用户的家目录。

---

#### 8、/media  /mnt

> 光盘默认挂载点，通常光盘挂载于 /mnt/cdrom 下，也不一定，可以选择任意位置进行挂载。

#### 9、/proc

> 此目录的**<u>数据都在内存中</u>**，如<u>**系统核心**</u>，<u>**外部设备**</u>，**<u>网络状态</u>**，***由于数据都存放于内存中，所以不占用磁盘空间***，比较重要的目录有 */proc/cpuinfo*、/proc/interrupts、*/proc/dma*、/proc/ioports、*/proc/net/* 等。

#### 10、/root

> **<u>系统管理员的家目录</u>**

#### 11、/run

> 系统运行信息

---

#### 12、/srv

> **系统服务**
> 
> **<u>服务启动之后需要访问的数据目录</u>**，如 www 服务需要访问的网页数据存放在 /srv/www 内。

#### 13、/sys

> **系统硬件信息**

#### 14、/tmp

> **临时存放文件**
> 
> 一般用户或正在执行的程序临时存放文件的目录，任何人都可以访问，重要数据不可放置在此目录下。

#### 15、/var

> 放置系统执行过程中**<u>经常变化的文件</u>**，如随时更改的日志文件 /var/log，/var/log/message：所有的登录文件存放目录，/var/spool/mail：邮件存放的目录，/var/run:程序或服务启动后，其PID存放在该目录下。

---

#### 16、/usr

> **应用程序存放目录**
> 
> <u>**/usr/bin :**</u> 存放应用程序，
> 
> **<u>/usr/share :</u>** 存放共享数据，
> 
> **<u>/usr/lib :</u>** 存放不能直接运行的，却是许多程序运行所必需的一些函数库文件,
> 
> **<u>/usr/local :</u>**: 存放软件升级,
> 
> **<u>/usr/share/doc :</u>** 系统说明文件存放目录,
> 
> **<u>/usr/share/man :</u>**  程序说明文件存放目录。

---

## 2、网络配置

> **查看ip地址**
> 
> ![](https://pic.imgdb.cn/item/6311beaa16f2c2beb1f860eb.png)

---

#### 1、修改静态IP

---

#### 2、配置主机名

---

#### 3、远程登陆

##### 1、登陆

> 通过**ssh**登陆
> 
> ```bash
> ssh 用户名@IP
> ```

![](https://pic.imgdb.cn/item/6311c65816f2c2beb1fd1628.png)

> 退出
> 
> ![](https://pic.imgdb.cn/item/6311c74f16f2c2beb1fe4d76.png)
> 
> ```bash
> exit
> ```

---

##### 2、免密登陆

---

## 3、系统管理

> **进程：一个正在被执行的程序和命令 （process）**
> 
> **服务：启动之后一直存在、常驻内存的进程 （service）**

---

#### 1、Linux 服务管理

##### 1、service

> ~~CentOS 之前版本的使用~~,后续版本使用 ***systemctl***
> 
> **service  服务名 start | stop | restart | status**

查看系统服务

```bash
cd /etc/init.d/

ls
```

![](https://pic.imgdb.cn/item/6313244d16f2c2beb1e738d6.png)

---

##### 2、systemctl

> CentOS 7使用 ***systemctl***
> 
> **systemctl   start | stop | restart | status | disable | enable 服务名**

查看系统服务

```bash
cd /usr/lib/systemd/system、

ll
```

![](https://pic.imgdb.cn/item/6313264616f2c2beb1e9deb8.png)

---

#### 2、系统运行级别

> 系统运行图形化操作界面
> 
> ```bash
> setup
> ```
> 
> ![](https://pic.imgdb.cn/item/6313299716f2c2beb1ed24b0.png)
> 
> 带 `*` 代表开机自启动，`space（空格）` 取消/开启

---

![](https://pic.imgdb.cn/item/63132bd716f2c2beb1ef48af.jpg)

```bash
vim /etc/inittab
```

---

- **CentOS 的运行级别简化**

> `multi-user.target` : 运行级别 3（多用户有网，命令行模式）
> 
> `graphical.target` : 运行级别 5（多用户有网，图形界面模式）

- **查看当前运行级别**

> ```bash
> systemctl get-default
> ```
> 
> `systemctl get-default`

- **修改当前运行级别**

> ```bash
> systemctl set-default xxx.target
> # xxx -->> multi-user | graphical
> ```
> 
> `systemctl set-default xxx.target`
> 
> `# xxx -->> multi-user | graphical`

---

![](https://pic.imgdb.cn/item/6313303516f2c2beb1f3aaad.png)

```cpp
init 3 // 命令行模式
init 5 // 图形界面
```

---

#### 3、配置服务

##### 1、查看服务

![](https://pic.imgdb.cn/item/6313310116f2c2beb1f463b9.png)

> ```bash
> chkconfig --list  #6
> chkconfig --livel 3 network off # 更改 network 服务的3级别为关 
> 
> systemctl list-unit-files #7
> ```

---

##### 2、防火墙

> centos 6 : **iptables**
> 
> centos 7 : **firewalld**
> 
> ```bash
> systemctl stop firewalld
> ```

---

##### 3、关机重启

- **sync**   数据内存同步到硬盘
- **halt** 停机不断电
- **poweroff**  关机断电
- **reboot**  重启
- **shutdown**  [时间]

---

## 4、帮助命令
