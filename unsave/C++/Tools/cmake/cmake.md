# CMake

> **CMake** 是一个跨平台的工具，根据系统生成配置文件

---

### 1、介绍

1. 开源代码，使用类BSD许可发布。
2. 跨平台，并可以生成native编译配置文件。
   - 在linux/Unix平台，生成makefile。
   - 在苹果平台可以生成Xcode。
   - 在windows平台，可以生成MSVC的工程文件。
3. 能够管理大型项目。
4. 简化编译构建过程和编译过程。
5. cmake的工具链：cmake+make。
6. 高效率，因为cmake在工具链中没有libtool。
7. 可扩展，可以为cmake编写特定功能的模块，扩展cmake功能。

### 2、编译

```shell
mkdir build
cd build
cmake -G "MinGW Makefiles" ..  //已MinGW编译器生成makefile
mingw32-make.exe(make)         //编译生成
Windows默认编译器是 MSVC
```
