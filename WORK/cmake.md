## cmake例子

message 输出语句

cmake_minimum_required 最低版本要求

project，形如

- project(test_KevinCmake VERSION 0.1.0)
- project(SeakyEmoji LANGUAGES CXX)

启用测试功能

```
include(CTest)
enable_testing()
```

include_directories 包含目录

aux_source_directory 设置某个目录所有源文件到指定变量

add_executable 指定某些文件生成exe

set 设置 XXX变量为CCC

target_link_libraries

指定链接给定目标和/或其依赖项时要使用的库。命名的<目标>必须是由add_executable()或add_library()之类的命令创建的，并且不能是ALIAS目标。

add_compile_definitions 增加编译定义

add_library 添加库

remove_definitions 去除定义

## qmake转cmake

Qt之QMake编译转换为CMake编译

https://blog.csdn.net/nchu_zhangyiqing/article/details/122078675

“轻松搞定CMake”系列之CMakeLists文件编写语法规则详解

https://blog.csdn.net/zhanghm1995/article/details/80902807

ubuntu下用cmake编译Qt5（保姆级教程）

https://blog.csdn.net/qq_42823342/article/details/120799577

一文搞懂如何在CMake中使用Qt

https://blog.csdn.net/Copperxcx/article/details/123116433

Qt构建cmake工程方法总结

https://www.cnblogs.com/learnhow/p/15110705.html

CMake教程——QT项目使用CMake

https://www.jianshu.com/p/622d2ec351b5

cmake 添加头文件目录，链接动态、静态库

https://blog.csdn.net/luoganttcc_son/article/details/125934661

cmake小发现

https://zhuanlan.zhihu.com/p/362311688

Qt Cmake添加*.qrc资源文件

https://blog.csdn.net/qq_33835370/article/details/120224455

## cmake关键语句

```
cmake_minimum_required(VERSION 3.5)
project(TwsOnePlatform VERSION 0.1.0)
```

add_subdirectory 添加子目录

```
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
```

find_package target_link_libraries前置操作

include_directories 添加路径，头文件路径

输出目录CMAKE_RUNTIME/ARCHIVE_OUTPUT_DIRECTORY_DEBUG/RELEASE

set(CMAKE_DEBUG_POSTFIX d) 调试后缀d

qt5_add_resources 添加qrc资源文件前置

add_library  创建dll

target_link_libraries 等价add_lib?

add_executable 创建exe

add_dependencies 添加依赖关系（影响编译顺序）

add_compile_definations  添加宏定义

link_directories  包含lib文件路径

## cmake生成exe后面加d

set_target_properties(XXXProject PROPERTIES DEBUG_POSTFIX "d")

## msvc编译器 cmake编译优化级别设置

- /O1 基本优化
- /O2 默认优化
- /Ox 启用所有优化
- /ObN 控制函数内联程度
- /Od 禁用所有优化

例子：`target_compile_options(MyExecutable PRIVATE /O2)`

## cmake未生成lib文件的原因

https://blog.csdn.net/weixin_32155265/article/details/128054373

## AutoUic error

`set(CMAKE_AUTOUIC_SEARCH_PATHS "src/Forms")`

https://www.cnblogs.com/dbai/p/17249494.html

https://blog.csdn.net/qq_51470638/article/details/129101424

## 编译时注意项目内的build是否会有影响，尤其是对于批处理编译的情况

## cmake编译utf-8文件报常量中有换行符的问题

add_compile_options("/utf-8")

## 无法解析的外部符号 static struct QMetaObject问题

cmake未将头文件加入源码