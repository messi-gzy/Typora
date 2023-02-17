# clang-tidy

### 一、介绍

​	`clang-tidy`是一个基于clang的C语言“linter”工具。它的目的是提供一个可扩展的框架，用于诊断和修复典型的编程错误，如样式违反、接口误用或可以通过静态分析推断出的错误。`clang-tidy`是模块化的，为编写新支票提供了方便的界面。

​	`clang-tidy` check可以检测各式各样的问题：

- 检测违反代码规范的代码模式（header guard不满足，include头文件顺序错误)；
- 找出不容易在编译时发现的代码错误（把int赋值给std::string, 变量定义在头文件）；
- 把deprecated的API替换成新的API，modernize模块典型例子，把C++03的代码自动转换成C++11的代码（for-range-loop, auto, nullptr, overriede, default）；

### 二、使用