# VMware Pro各版本虚拟机安装配置

## 一、Windows 11安装

##### 1、下载镜像文件

- > 官网（**推荐**/下载速度快，绝对的安全 ）：
  >
  > [https://www.microsoft.com/zh-cn/software-download/windows11](https://www.microsoft.com/zh-cn/software-download/windows11)
  >
  > 按照选项顺序选择家庭版，语言，下载安装（.iso镜像文件）

- > 百度网盘（我自已上传的官网源文件，大家也可以选择）
  >
  > 

##### 2、打开VMware

***(这个自已去找。。。。，官网也有免费版)***

###### 1、新建虚拟机

<img src="https://pic.imgdb.cn/item/629631860947543129cd0d30.png" style="zoom: 50%;" />

选择典型配置就可以了

###### 2、选择镜像文件

<img src="https://pic.imgdb.cn/item/629631860947543129cd0db7.png" style="zoom:50%;" />

==这里选择下载下来的镜像文件，忽略提示无法检测，继续下一步==

###### 3、选择系统版本以及版本

<img src="https://pic.imgdb.cn/item/629631860947543129cd0dc1.png" style="zoom:50%;" />

按照图示选择就可以了

- 输入虚拟机名称（随意），然后选择虚拟机文件存储路径


！！！**建议内存大的盘，最少70G**

- 选择磁盘大小

<img src="https://pic.imgdb.cn/item/629631860947543129cd0d2a.png" style="zoom:50%;" />

磁盘大小就默认的60G就行，都为默认。



###### 4、编辑虚拟机设置

<img src="https://pic.imgdb.cn/item/6296318f0947543129cd1ae4.png" style="zoom:50%;" />

###### 5、加入访问控制密码

<img src="https://pic.imgdb.cn/item/6296318f0947543129cd1af2.png" style="zoom: 50%;" />

###### 6、选择固件类型（UEFI）

<img src="https://pic.imgdb.cn/item/6296318f0947543129cd1b03.png" style="zoom:50%;" />

###### 7、加入TPM安全模块（==**这是最重要的**==）

<img src="https://pic.imgdb.cn/item/6296318f0947543129cd1ac8.png" style="zoom:50%;" />

- 检查自已电脑TPM版本

  > ```
  > Win + R
  > tpm.msc
  > 检查是否启动了，并且版本需要为2.0
  > ```

- 如果版本小于2.0，网上有绕过检查的方法

###### 8、记得修改内存大小，强烈建议选择4G及以上

**（这里太小，很有可能会安装出问题）**

<img src="https://pic.imgdb.cn/item/6296318f0947543129cd1ad2.png" style="zoom:50%;" />

###### 9、然后到这里基本配置就结束了！！！

接下来就是启动虚拟机！！！

###### 10、启动后按步骤依次选择，下一步

（在需要密钥是可以直接跳过，选择没有密钥）

  ***(如果安装时提示未连接网络，也可以选择跳过修改配置)***

此时就可以看见完成了！！！

应该都是可以可以成功的！！！（：

但是你会发现屏幕太小，体验很差，不要担心，只需下载VMware Tools！！！

###### 11、改变屏幕大小

在软件顶部找到虚拟机菜单，选择安装 VMware Tools

<img src="https://pic.imgdb.cn/item/629631960947543129cd24fa.png" style="zoom:50%;" />

**记得在虚拟机运行的时候安装**

很快就可以下载好，在虚拟机中按步骤安装Tools软件就可以了，显示更新Tools 就代表安装成功了。

此时就会自动更改屏幕大小，看起来有那感觉了吧，别忘了打开全屏偶，

这时候看起来是不是完全有那味了！！！哈啊哈哈哈。

*如果没有自动改变大小，也可以再次选择 Tools 菜单，然后选择自适应屏幕*



**！！！安装运行成功**

![](https://pic.imgdb.cn/item/629631960947543129cd24e5.png)

## 二、MacOS 安装配置 

###### 1、下载镜像文件以及工具

- >   第三方网站：https://sysin.org/:
  >
  > 百度网盘链接：https://pan.baidu.com/s/125Wi_SP58_sD6uXm_jtjmw 提取码：gcjh
  > SHA256SUM：16ea61cba4bf5444ef9681466da88df888bf95f6284e5ff2169ee4cbdb222505

- > 我的百度网盘：（包括破解工具）
  >
  > --来自百度网盘超级会员V1的分享
  > hi，这是我用百度网盘分享的内容~复制这段内容打开「百度网盘」APP即可获取 
  > 链接:https://pan.baidu.com/s/1uZLc7088O03-5K4ZdQOIiw 
  > 提取码:2wv7

###### 2、解压破解工具

1. ​	将破解工具解压到VMware 安装路径下

   <img src="https://pic.imgdb.cn/item/62962f6d0947543129c9c510.png" style="zoom:50%;" />

   

2. 检查进程

   - 打开资源管理器

     ![](https://pic.imgdb.cn/item/62962f6d0947543129c9c522.png)

     将有关VMware的进程全部关闭

   - 为了成功，可以先将杀毒软件关闭

3. 右键使用管理员身份运行 **win-install.cmd**

   <img src="https://pic.imgdb.cn/item/62962f6d0947543129c9c517.png" style="zoom:50%;" />

   然后会出现命令行格式，命令行会自已运行，不需要自已去操作，运行完成后会自动关闭

4. 检查

   新建虚拟机，查看是否有MacOS选项

   <img src="https://pic.imgdb.cn/item/62962f6d0947543129c9c533.png" style="zoom:50%;" />

   出现则成功

###### 3、新建虚拟机

1. 向导

   典型->安装程序光盘映像（选择下载下来的镜像文件）->选择操作系统->选则保存位置（尽量要大，避免C盘）->选择磁盘大小（我选的80G，尽量大于等于60G）->完成！！！

   <img src="https://pic.imgdb.cn/item/62962f6d0947543129c9c533.png" style="zoom:50%;" />

2. **此时不要着急运行虚拟机，还没有完成配置哦**

   - 打开刚才自已选择的保存位置

     修改.vmx后缀的文件

     <img src="https://pic.imgdb.cn/item/62962f6d0947543129c9c508.png" style="zoom:50%;" />

     **记事本打开，在文件最后加入以下内容**

     ![](https://pic.imgdb.cn/item/62962f770947543129c9d490.png)

     ==注意自已电脑的处理器==

     > intel：
     >
     > ```
     > smc.version = "0"
     > ```

     > AMD：
     >
     > ```
     > smc.version = "0"
     > cpuid.0.eax = "0000:0000:0000:0000:0000:0000:0000:1011"
     > cpuid.0.ebx = "0111:0101:0110:1110:0110:0101:0100:0111"
     > cpuid.0.ecx = "0110:1100:0110:0101:0111:0100:0110:1110"
     > cpuid.0.edx = "0100:1001:0110:0101:0110:1110:0110:1001"
     > cpuid.1.eax = "0000:0000:0000:0001:0000:0110:0111:0001"
     > cpuid.1.ebx = "0000:0010:0000:0001:0000:1000:0000:0000"
     > cpuid.1.ecx = "1000:0010:1001:1000:0010:0010:0000:0011"
     > cpuid.1.edx = "0000:0111:1000:1011:1111:1011:1111:1111"
     > featureCompat.enable = "TRUE"
     > ```

     ==注意一定要在虚拟机关闭的时候修改文档==

3. ！！！配置完成，这时候就可以开启虚拟机了

4. 按照步骤选择就行

   选择语言，

5. 选择磁盘工具

   <img src="https://pic.imgdb.cn/item/62962f3c0947543129c97b22.png" style="zoom: 50%;" />

6. 抹除磁盘

   <img src="https://pic.imgdb.cn/item/62962f3c0947543129c97b2d.png" style="zoom:50%;" />

   <img src="https://pic.imgdb.cn/item/62962f3c0947543129c97b46.png" alt="macOS 11-2022-05-17-11-41-12" style="zoom:50%;" />

7. 关闭磁盘工具（左上角信号灯红色的）

8. 选择安装MacOS

   <img src="https://pic.imgdb.cn/item/62962f3c0947543129c97b22.png" style="zoom:50%;" />

9. 依次继续就行

10. 然后就是简单的开机选项

11. 如果没有网络，就在关机后在网络配置中选择桥接模式

12. 当然屏幕也是可以放大的 （：！

    在系统完全打开并且配置完成后，在软件菜单中选择虚拟机，安装 VMware Tools

    ==记得不要关机虚拟机==

    下载完成后就会在虚拟机中自动跳出安装界面，输入密码安装成功

    然后应该屏幕就会自动适应哦，记得打开VMware的全屏模式哦！！！

    是不是感觉就来了那

13. 如果没有自动适应，再次在菜单中选择虚拟机，选择Tools 选择自适应屏幕 就好了！！！

    **完成！！！**

![](https://pic.imgdb.cn/item/62962f3c0947543129c97b19.png)

![](https://pic.imgdb.cn/item/62962f3c0947543129c97b0b.png)

[返回上一页](../../README.md)