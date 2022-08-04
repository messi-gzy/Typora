# README

# MinGW

## 一、目录

## 二、GNU

### 1、g++

### 2、gdb

## 三、cmake

### 1、编译

```shell
mkdir build
cd build
cmake -G "MinGW Makefiles" ..  //已MinGW编译器生成makefile
mingw32-make.exe(make)         //编译生成
Windows默认编译器是 MSVC
```

### 2、CMakeLists

#### 1、简介

cmake 是一个跨平台、开源的构建系统。它是一个集软件构建、测试、打包于一身的软件。它使用与平台和==编译器==独立的配置文件来对软件编译过程进行控制。

#### 2、命令

##### 1、指定cmake最小版本

##### 2、设置项目名称

##### 3、设置编译类型

##### 4、指定包含的源文件

###### 4.1、明确包含哪些源文件

###### 4.2、搜索所有的cpp文件

###### 4.3、自定义搜索规则

##### 5、查找指定库文件

##### 6、设置包含的目录

##### 7、设置链接库搜索目录

##### 8、设置target需要的链接的库