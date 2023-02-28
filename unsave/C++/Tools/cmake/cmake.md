# CMake

> **CMake** 是一个跨平台的工具，根据系统生成配置文件
>
> **cmake** 是一个跨平台、开源的构建系统。它是一个集软件构建、测试、打包于一身的软件。它使用**与平台和编译器独立的配置文件来对软件编译过程进行控制**。

### 1、介绍

1. 开源代码，使用类BSD许可发布。
2. 跨平台，并可以生成native编译配置文件。
   - 在linux/Unix平台，生成makefile。
   - 在macos平台可以生成Xcode工程。
   - 在windows平台，可以生成MSVC的工程文件。
3. 能够管理大型项目。
4. 简化编译构建过程和编译过程。
5. cmake的工具链：cmake+make。
6. 高效率，因为cmake在工具链中没有libtool。
7. 可扩展，可以为cmake编写特定功能的模块，扩展cmake功能。

### 2、使用

> ```ABAP
> cmake [options] <path-to-source>
> cmake [options] <path-to-existing-build>
> ```

##### 1、Linux

```shell
mkdir build
cd build
cmake ..  #生成makefile
make     #编译生成
```

##### 2、Windows(MinGW)

```powershell
md build
cd build
cmake -G "MinGW Makefiles" ..
mingw32-make | make  
#MinGW默认make工具名称为mingw32-make,为了方便我们可以在同一目录下复制mingw32-make并改名为make,
#注意不要直接修改名称，修改复制后的文件。

#Windows默认编译器是 MSVC
```

### 3、安装

#### 3.1、下载

- [官网](https://cmake.org/download/)【https://cmake.org/download/】
- 任意路径下下载

```bash
wget https://github.com/Kitware/CMake/releases/download/v3.24.2/cmake-3.24.2.tar.gz
```

#### 3.2、解压

```shell
tar -zxvf cmake-3.24.2.tar.gz -C /usr/local/cmake
```

#### 3.3、编译

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

----

[README](../../README.md)
