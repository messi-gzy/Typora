# Java配置（Windows）

### 一、目录

### 二、Maven

##### 1、下载	

- > 官网：
  >
  > [Maven – Download Apache Maven](https://maven.apache.org/download.cgi)

![](E:\图片\snipaste\java配置\Windows\Snipaste_2022-05-15_12-30-40.png)

- > 百度网盘：
  >
  > 链接：https://pan.baidu.com/s/15glszTScDSDVVOfmFVZKrg 
  > 提取码：ed6n 
  > --来自百度网盘超级会员V1的分享

##### 2、配置环境

1. 打开编辑环境变量（控制面板搜索环境变量）

2. 系统变量新建

   ![](E:\图片\snipaste\java配置\Windows\Snipaste_2022-05-15_12-38-19.png)

   ![](E:\图片\snipaste\java配置\Windows\Snipaste_2022-05-15_12-39-36.png)

   > ```
   > MAVEN_HOME
   > ```

   

3. path变量

   ![](E:\图片\snipaste\java配置\Windows\Snipaste_2022-05-15_12-40-19.png)

   点击编辑（/双击），点击增加

   写入

   > ```
   > %MAVEN_HOME%\bin
   > ```

4. 环境变量成功，检查

   管理员身份运行cmd，输入 **mvn -v**

   ![Snipaste_2022-05-15_15-18-39](E:\图片\snipaste\java配置\Windows\Snipaste_2022-05-15_15-18-39.png)

   出现以上内容，创建成功

   

##### 3、修改配置文件

1. 打开maven解压目录下的conf中的**settings.xml**（记事本或者编辑器打开）

   ![](E:\图片\snipaste\java配置\Windows\Snipaste_2022-05-15_15-23-15.png)

   找到<mirrors></mirrors>

   配置阿里云镜像仓库，国外仓库下载速度慢，体验不好。

   > ```xml
   > <!--阿里云仓库-->
   > <mirror>
   > 		 <id>nexus-aliyun</id>
   > 		 <mirrorOf>*</mirrorOf>
   > 		 <name>Nexus aliyun</name>
   > 		 <url>http://maven.aliyun.com/nexus/content/groups/public</url>
   > </mirror>
   > ```

   ==！！！！注意格式和位置不要写进注释里。==

2. 配置本地仓库的地址（所有的包都下载在这里）

   > maven默认地址为C盘的 用户目录下/.m2/repository
   >
   > 建议修改，保护C盘

   ![](E:\图片\snipaste\java配置\Windows\Snipaste_2022-05-15_15-27-31.png)

   再次打开**settings.xml**文件

   ![](E:\图片\snipaste\java配置\Windows\Snipaste_2022-05-15_15-29-42.png)

   找到如图所示的位置,写入下面的内容，注意（**内容里的文件路径是你的本地仓库的路径，自行创建修改**）

   ==！！！！注意格式和位置不要写进注释里。==
   
   ```xml
   <localRepository>D:\JAVA\Maven\.m2\repository</localRepository>
   ```
   

##### 4、idea配置Maven信息

1. File->Settings->Build......->Build Tools->Maven

   (File->Settings->搜索Maven）

2. ![](E:\图片\snipaste\java配置\Windows\Snipaste_2022-05-15_15-50-06.png)

按照图片所示配置路径

**三个路径都要修改为自已设置的路径**

！！！成功

### 三、Gradle



