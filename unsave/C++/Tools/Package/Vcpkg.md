# Vcpkg

### 一、介绍

- Vcpkg是一个命令行包管理工具，它可以极大地简化三方库的获取、安装、使用和部署流程。简单而又灵活

- Vcpkg是微软团队在GitHub上的一个开源项目，它提供一系列简单的命令，自动下载源码然后编译成三方库，而且并不依赖于Windows注册表或Visual Studio。

### 二、安装

#### 2.1、Windows

> 使用工具：Git
>
> **建议在==PowerShell==下进行**

##### 1、下载

```bash
git clone https://github.com/microsoft/vcpkg.git
```

##### 2、编译

```bash
cd vcpkg
.\bootstrap-vcpkg.bat
```

编译好以后会在同级目录下生成vcpkg.exe文件。



#### 2.2、Linux

### 三、使用