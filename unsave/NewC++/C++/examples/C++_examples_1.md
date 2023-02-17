## 示例【1】

### 一、获取数组长度

#### 1.1、获取动态数组长度

```cpp
_msize(pointer)/sizeof(type)
    
//  (1) pointer :数组指针
//  (2) type : 数组元素的数据类型
```



## 示例【2】

> Cmake构建的简单项目
>
> 目录结构
>
> ```ABAP
> ├─CMakeLists.txt
> ├─test
> |  ├─CMakeLists.txt
> |  └test.cpp
> ├─src
> |  ├─CMakeLists.txt
> |  └main.cpp
> ├─lib
> |  ├─tool
> |  |  ├─CMakeLists.txt
> |  |  └tools_get_exe_path.cpp
> |  ├─study_1
> |  |    ├─class_study.cpp
> |  |    ├─CMakeLists.txt
> |  |    └hello.cpp
> ├─include
> |    ├─class_study.h
> |    ├─hello.h
> |    └tools_one.h
> ```
>
> - **src**:可执行程序，核心语句
> - **lib**：动态库|静态库生成，可对外提供，可重复调用的
> - **test**：测试程序，生成不同的测试可执行程序
> - **include**：对外提供的头文件

#### 1、总CMakeLists

```cmake
cmake_minimum_required(VERSION 3.10)

set(PROJECT_N study)
project(${PROJECT_N} VERSION 1.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)


add_subdirectory(./test)
add_subdirectory(./src)
add_subdirectory(./lib/study_1)
add_subdirectory(./lib/tool)

IF (WIN32)
    message("windows系统")
    SET(SYSTEM_NAME win)
    SET(
            EXECUTABLE_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
ELSEIF (APPLE)
    message("apple系统")
    SET(SYSTEM_NAME apple)
    SET(
            EXECUTABLE_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out/dll
    )
ELSEIF (UNIX)
    message("unix系统") 
    SET(SYSTEM_NAME unix)
    SET(
            EXECUTABLE_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out/dll
    )
ENDIF()
```

#### 2、src

```cmake
SET(
        EXECUTABLE_OUTPUT_PATH
        ${PROJECT_BINARY_DIR}/out
)
IF (WIN32)
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
ELSEIF (APPLE)
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out/dll
    )
    link_directories(
            ${PROJECT_BINARY_DIR}/out/dll
    )
ELSEIF (UNIX)
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out/dll
    )
    link_directories(
            ${PROJECT_BINARY_DIR}/out/dll
    )
ENDIF ()

include_directories(
        ${PROJECT_SOURCE_DIR}/include
)

add_executable(
        ${PROJECT_NAME}
        main.cpp
)

target_link_libraries(
        ${PROJECT_NAME}
        study_1
        tools
)
```

#### 3、lib

##### 3.1、class_study

```cmake
set(
        SRC_HELLO
        hello.cpp
        class_study.cpp
)
add_library(
        study_1
        SHARED
        ${SRC_HELLO}
)

include_directories(
        ${PROJECT_SOURCE_DIR}/include
)
IF (WIN32)
    SET(
            EXECUTABLE_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
ELSEIF (APPLE)
    SET(
            EXECUTABLE_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out/dll
    )
ELSEIF (UNIX)
    SET(
            EXECUTABLE_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out/dll
    )
ENDIF ()
```

##### 3.2、tools

```cmake
set(
        SRC_HELLO
        tools_get_exe_path.cpp
)
add_library(
        tools
        SHARED
        ${SRC_HELLO}
)

include_directories(
        ${PROJECT_SOURCE_DIR}/include
)
IF (WIN32)
    SET(
            EXECUTABLE_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
ELSEIF (APPLE)
    SET(
            EXECUTABLE_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out/dll
    )
ELSEIF (UNIX)
    SET(
            EXECUTABLE_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out/dll
    )
ENDIF ()

```

#### 4、test

```cmake
IF (WIN32)
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out
    )
    link_directories(
            ${PROJECT_BINARY_DIR}/out
    )
ELSEIF (APPLE)
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out/dll
    )
    link_directories(
            ${PROJECT_BINARY_DIR}/out/dll
    )
ELSEIF (UNIX)
    SET(
            LIBRARY_OUTPUT_PATH
            ${PROJECT_BINARY_DIR}/out/dll
    )
    link_directories(
            ${PROJECT_BINARY_DIR}/out/dll
    )
ENDIF ()

include_directories(
        ${PROJECT_SOURCE_DIR}/include
)

SET(TEST_CLASS test_class)

SET(
        TEST_CLASS_SOURCE
        test.cpp
)

add_executable(
        ${TEST_CLASS}
        ${TEST_CLASS_SOURCE}
)

target_link_libraries(
        ${TEST_CLASS}
        study_1
)

SET(
        EXECUTABLE_OUTPUT_PATH
        ${PROJECT_BINARY_DIR}/out/test
)
```

