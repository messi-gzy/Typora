# Java配置（Windows）

### 一、目录

### 二、Maven

##### 1、下载

- > 官网：
  > 
  > [Maven – Download Apache Maven](https://maven.apache.org/download.cgi)

![](https://pic.imgdb.cn/item/6297024b094754312984ef63.png)

- > 百度网盘：
  > 
  > 链接：https://pan.baidu.com/s/15glszTScDSDVVOfmFVZKrg 
  > 提取码：ed6n 
  > --来自百度网盘超级会员V1的分享

##### 2、配置环境

1. 打开编辑环境变量（控制面板搜索环境变量）

2. 系统变量新建
   
   ![](https://pic.imgdb.cn/item/6297024b094754312984ef3b.png)
   
   ![](https://pic.imgdb.cn/item/6297024b094754312984ef41.png)
   
   > ```
   > MAVEN_HOME
   > ```

3. path变量
   
   ![](https://pic.imgdb.cn/item/6297024b094754312984ef4e.png)
   
   点击编辑（/双击），点击增加
   
   写入
   
   > ```
   > %MAVEN_HOME%\bin
   > ```

4. 环境变量成功，检查
   
   管理员身份运行cmd，输入 **mvn -v**
   
   ![Snipaste_2022-05-15_15-18-39](https://pic.imgdb.cn/item/62970252094754312984f788.png)
   
   出现以上内容，创建成功

##### 3、修改配置文件

1. 打开maven解压目录下的conf中的**settings.xml**（记事本或者编辑器打开）
   
   ![](https://pic.imgdb.cn/item/62970252094754312984f795.png)
   
   找到<mirrors></mirrors>
   
   配置阿里云镜像仓库，国外仓库下载速度慢，体验不好。
   
   > ```xml
   > <!--阿里云仓库-->
   > <mirror>
   >          <id>nexus-aliyun</id>
   >          <mirrorOf>*</mirrorOf>
   >          <name>Nexus aliyun</name>
   >          <url>http://maven.aliyun.com/nexus/content/groups/public</url>
   > </mirror>
   > ```
   
   ==！！！！注意格式和位置不要写进注释里。==

2. 配置本地仓库的地址（所有的包都下载在这里）
   
   > maven默认地址为C盘的 用户目录下/.m2/repository
   > 
   > 建议修改，保护C盘
   
   ![](https://pic.imgdb.cn/item/62970252094754312984f765.png)
   
   再次打开**settings.xml**文件
   
   ![](https://pic.imgdb.cn/item/62970252094754312984f772.png)
   
   找到如图所示的位置,写入下面的内容，注意（**内容里的文件路径是你的本地仓库的路径，自行创建修改**）
   
   ==！！！！注意格式和位置不要写进注释里。==
   
   ```xml
   <localRepository>D:\JAVA\Maven\.m2\repository</localRepository>
   ```

##### 4、idea配置Maven信息

1. File->Settings->Build......->Build Tools->Maven
   
   (File->Settings->搜索Maven）
   
   <img src="https://pic.imgdb.cn/item/6297025a094754312985000a.png" style="zoom:50%;" />

2. ![](https://pic.imgdb.cn/item/6297025a0947543129850003.png)

按照图片所示配置路径

**三个路径都要修改为自已设置的路径**

！！！成功

### 三、Gradle

### 四、Node.js

> 官网：
> 
> http://nodejs.cn/download/
> 
> <img src="https://pic.imgdb.cn/item/62982faf0947543129c0ad59.png" style="zoom: 33%;" />

检查

![](https://pic.imgdb.cn/item/62982f180947543129c0059a.png)

### 五、MinGW

##### 1、下载

> 官网：
> 
> https://sourceforge.net/projects/mingw-w64/files/
> 
> <img src="https://pic.imgdb.cn/item/629ad0d10947543129c04f78.png" style="zoom: 67%;" />

##### 2、安装

解压

![](https://pic.imgdb.cn/item/629ad28c0947543129c2760b.png)

##### 3、环境变量

![](https://pic.imgdb.cn/item/629ad3060947543129c30c3e.png)

**系统变量-->path-->新建-->解压后的bin目录**

##### 4、验证

```shell
gcc --version
g++ --version
```

<img src="https://pic.imgdb.cn/item/629ad6100947543129c6a325.png" style="zoom:50%;" />

![](https://pic.imgdb.cn/item/629ad6100947543129c6a31c.png)
