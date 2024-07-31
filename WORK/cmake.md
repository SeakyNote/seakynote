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

## cmake编译一个文件一个文件加上还是遍历加上

遍历添加的问题

- 可能有些文件放在那但不需要编译的场景
- 可能会遍历到不想编译的文件
  - 比如build目录
- 据说华为也是逐个添加的

## 在cmake中，对于target_link_libraries函数，public和private有什么区别？

在CMake中，`target_link_libraries`函数用于将库链接到目标上，并指定该链接的属性。这个函数有三个关键字：`PUBLIC`、`PRIVATE`和`INTERFACE`。它们定义了链接库的使用范围和传播方式。

### 关键字解释

1. **PRIVATE**
   - 当你使用`PRIVATE`关键字时，链接库只对当前目标可见。这意味着其他链接到该目标的目标不会继承这些链接库。
   - 用法示例：
     ```cmake
     target_link_libraries(my_target PRIVATE some_library)
     ```
     在这个例子中，`some_library`只对`my_target`可见，不会传递给任何链接到`my_target`的其他目标。

2. **PUBLIC**
   - 当你使用`PUBLIC`关键字时，链接库对当前目标和所有链接到该目标的目标可见。这意味着它们会传播到依赖于当前目标的所有其他目标。
   - 用法示例：
     ```cmake
     target_link_libraries(my_target PUBLIC some_library)
     ```
     在这个例子中，`some_library`对`my_target`可见，并且任何链接到`my_target`的目标也会看到并链接`some_library`。

3. **INTERFACE**
   - 当你使用`INTERFACE`关键字时，链接库只对链接到当前目标的目标可见，而当前目标本身不会链接这些库。通常用于接口库。
   - 用法示例：
     ```cmake
     target_link_libraries(my_target INTERFACE some_library)
     ```
     在这个例子中，`some_library`不会链接到`my_target`，但是任何链接到`my_target`的目标都会看到并链接`some_library`。

### 应用场景举例

假设你有三个目标：`libA`、`libB` 和 `app`，且依赖关系如下：

- `libA` 依赖于 `some_library`
- `libB` 依赖于 `libA`
- `app` 依赖于 `libB`

1. **使用 `PRIVATE`**：
   ```cmake
   target_link_libraries(libA PRIVATE some_library)
   ```
   这种情况下，`libB` 和 `app` 都不会看到 `some_library`，只有 `libA` 会链接 `some_library`。

2. **使用 `PUBLIC`**：
   ```cmake
   target_link_libraries(libA PUBLIC some_library)
   ```
   这种情况下，`libB` 会看到并链接 `some_library`，而 `app` 也会通过 `libB` 继承到 `some_library`。

3. **使用 `INTERFACE`**：
   ```cmake
   target_link_libraries(libA INTERFACE some_library)
   ```
   这种情况下，`libA` 本身不会链接 `some_library`，但 `libB` 和 `app` 都会看到并链接 `some_library`。

### 总结

- **PRIVATE**：链接库仅对当前目标可见，不会传播。
- **PUBLIC**：链接库对当前目标和依赖当前目标的所有目标可见，并传播。
- **INTERFACE**：链接库对依赖当前目标的所有目标可见，但不链接到当前目标。

选择适当的关键字有助于控制库的可见性和依赖性，确保项目构建的正确性和效率。

## ctest

catch2

https://blog.csdn.net/Tosonw/article/details/89449029

https://gitee.com/bigearrabbit/kevin_ctest

https://www.jetbrains.com/lp/devecosystem-2022/cpp/#Which-unit-testing-frameworks-do-you-regularly-use

## cmake install
https://gitee.com/bigearrabbit/KevinCmake/tree/master/cmake_install

https://www.bilibili.com/video/BV1Ep421Q7Rt