# Ninja

### 一、安装

#### 1.1、Windows

> 环境：VS2022
>
> ​			x64
>
> 工具：Git
>
> ​			Python
>
> **==注意：在具有管理员权限下的cmd中操作==**（[Windows下cmd的cd命令](https://blog.csdn.net/zdy219727/article/details/98605287)）

---

##### 1、编译

###### ①、下载

```bash
git clone https://github.com/ninja-build/ninja.git
```

###### ②、编译

- ```bash
  cd ninja
  ```

- ```bash
  python ./configure.py --bootstrap
  ```

<!--编译成功-->

![](https://pic.imgdb.cn/item/63e5fe664757feff3301d87b.png)

###### ③、查看版本

```bash
ninja.exe --version
```

---

##### 2、配置环境变量

###### ①、打开环境变量

###### ②、修改系统变量

==**path**==：添加自已的`ninja`目录

![](https://pic.imgdb.cn/item/63e602754757feff33089de2.png)

---

#### 1.2、Linux

##### 1.2.1、CentOS



##### 1.2.2、Ubuntu