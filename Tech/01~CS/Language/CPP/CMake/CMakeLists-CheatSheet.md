# CMakeLists.txt

```h
//声明要求的 cmake 最低版本,终端输入 cmake -version 可查看cmake的版本
cmake_minimum_required(VERSION 2.8)

//声明 cmake 工程名字
project(slam)

//设置使用g++编译器,这是添加变量的用法set(KEY VALUE)接收两个参数，用来声明变量。在camke语法中使用${KEY}这种写法来取到VALUE
set(CMAKE_CXX_COMPILER "g++")

//设置cmake编译模式有debug和release两种PROJECT_SOURCE_DIR项目根目录也就是是CmakeLists.txt的绝对路径
set(CMAKE_BUILD_TYPE "Release" )

//设定生成的可执行二进制文件存放的存放目录
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

//设定生成的库文件的存放目录
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

//参数CMAKE_CXX_FLAGS含义是： set compiler for c++ language
//添加c++11标准支持，*.CPP文件编译选项,-march=native指定目标程序的cpu架构来进行程序优化
//native就是相当于自检测cpu，-march是gcc优化选项,后面的-O3是用来调节编译时的优化程度的，最高为-O3,最低为-O0即不做优化
//-Ox这个参数只有在CMake -DCMAKE_BUILD_TYPE=release 时有效
//因为debug版的项目生成的可执行文件需要有调试信息并且不需要进行优化,而release版的不需要调试信息但需要优化
set(CMAKE_CXX_FLAGS “-std=c++11 -march=native -O3”)

//调试手段message打印信息，类似于echo/printf，主要用于查cmake文件的语法错误
set(use_test ${SOURCES_DIRECTORY}/user_accounts.cpp)
message("use_test： ${use_test}")

//在CMakeLists.txt中指定安装位置, 在编译终端指定安装位置:cmake -DCMAKE_INSTALL_PREFIX=/usr ..
set(CMAKE_INSTALL_PREFIX < install_path >)

//增加子文件夹，也就是进入源代码文件夹继续构建
add_subdirectory(${PROJECT_SOURCE_DIR}/src)

//添加依赖，去寻找该库的头文件位置、库文件位置以及库文件名称，并将其设为变量，返回提供给CMakeLists.txt其他部分使用。
//cmake_modules.cmake文件是把CMakeLists.txt里用来寻找特定库的内容分离出来,如果提示没有找到第三方依赖库可以尝试安装或者暴力指定路径
// 寻找OpenCV库
find_package(OpenCV REQUIRED)

//在CMakeLists.txt中使用第三方库的三部曲:find_package、include_directories、target_link_libraries
include_directories(${OpenCV_INCLUDE_DIRS})// 去哪里找头文件
link_directories()// 去哪里找库文件(.so/.lib/.ddl等)
target_link_libraries(${OpenCV_LIBRARIES})// 需要链接的库文件
message("OpenCV_INCLUDE_DIRS: \n" ${OpenCV_INCLUDE_DIRS})
message("OpenCV_LIBS: \n" ${OpenCV_LIBS})

// find_package(Eigen3 REQUIRED), 假如找不到Eigen3库，我们就设置变量来指定Eigen3的头文件位置
set(Eigen3_DIR /usr/lib/cmake/eigen3/Eigen3Config.cmake)
include_directories(/usr/local/include/eigen3)
```

# 常用命令说明

- add_executable

`add_executable`命令用于将多个源文件编译成可执行文件。举个例子，假设我们有两个源文件`main.cpp`和`helper.cpp`，它们需要被编译成一个可执行文件`myapp`，我们可以使用下面的代码：

```
add_executable(myapp main.cpp helper.cpp)
```

其中，`myapp`表示生成的可执行文件的名称，`main.cpp`和`helper.cpp`表示源代码文件的名称。如果有多个源代码文件，可以将它们作为参数逐一列出。

- add_library

`add_library`命令用于将多个源文件编译成静态库或动态库。举个例子，假设我们有两个源文件`foo.cpp`和`bar.cpp`，它们需要被编译成一个静态库`libfoobar.a`，我们可以使用下面的代码：

```
add_library(foobar STATIC foo.cpp bar.cpp)
```

其中，`foobar`表示生成的库的名称，`foo.cpp`和`bar.cpp`表示源代码文件的名称。`STATIC`表示生成静态库，`SHARED`表示生成动态库，`MODULE`表示生成插件库。如果不指定库类型，则默认生成静态库。

- target_link_libraries

`target_link_libraries`命令用于将一个或多个库链接到可执行文件或其他库中。举个例子，假设我们需要将`libfoo.a`和`libbar.a`链接到可执行文件`myapp`中，我们可以使用下面的代码：

```
target_link_libraries(myapp foo bar)
```

其中，`myapp`表示可执行文件或其他库的名称，`foo`和`bar`表示需要链接的库的名称。如果有多个库，可以将它们作为参数逐一列出。

- include_directories

`include_directories`命令用于将头文件路径添加到编译器的搜索路径中。举个例子，假设我们需要将`/path/to/include`添加到编译器的头文件搜索路径中，我们可以使用下面的代码：

```
include_directories(/path/to/include)
```

如果有多个路径，可以将它们作为参数逐一列出。另外，`AFTER`和`BEFORE`表示添加的路径在搜索路径中的位置，`SYSTEM`表示添加的路径是系统头文件路径。

- link_directories

`link_directories`命令用于将库文件路径添加到链接器的搜索路径中。举个例子，假设我们需要将`/path/to/lib`添加到链接器的库文件搜索路径中，我们可以使用下面的代码：

```
link_directories(/path/to/lib)
```

如果有多个路径，可以将它们作为参数逐一列出。

- set

`set`命令用于设置变量的值。举个例子，假设我们需要将变量`MY_VARIABLE`的值设置为`hello world`，我们可以使用下面的代码：

```
set(MY_VARIABLE "hello world")
```

其中，`MY_VARIABLE`表示变量的名称，`hello world`表示变量的值。如果变量的值是一个字符串，需要用引号将其括起来。

- if

`if`命令用于判断条件是否成立。举个例子，假设我们需要判断变量`MY_VARIABLE`是否等于`hello world`，如果成立，则执行一些操作，我们可以使用下面的代码：

```
if(MY_VARIABLE STREQUAL "hello world")    # do somethingendif()
```

其中，`MY_VARIABLE`表示判断的条件，`STREQUAL`表示字符串相等。如果条件成立，则执行`do something`部分的代码。

- endif

`endif`命令用于结束`if`语句块。其实，在 CMake 中，所有的控制流语句都需要以`endif`命令结束。举个例子，假设我们需要判断变量`MY_VARIABLE`是否等于`hello world`，如果成立，则打印一条消息，否则打印另一条消息，我们可以使用下面的代码：

```
if(MY_VARIABLE STREQUAL "hello world")    message("MY_VARIABLE is hello world")else()    message("MY_VARIABLE is not hello world")endif()
```

其中，`message`命令用于打印消息。

- foreach

`foreach`命令用于遍历一个列表，并对其中的每个元素执行相同的操作。举个例子，假设我们有一个列表`mylist`，其中包含三个元素`foo`、`bar`和`baz`，我们需要将它们依次打印出来，我们可以使用下面的代码：

```
set(mylist foo bar baz)
foreach(item IN LISTS mylist)    message(${item})endforeach()
```

其中，`item`表示列表中的元素，`mylist`表示需要遍历的列表。`LISTS`表示`mylist`是一个列表。

**1. CMake 语法**

**1.1** **指定 cmake 的最小版本**

```
cmake_minimum_required(version 版本号)
```

例如：

```
cmake_minimum_required(version 2.8)
```

**1.2 定义工程名称**

```
#定义工程名称
project(项目名称)
```

例如：

```
project(MyTest)
```

**1.3 显示定义变量**

```
set(var [value])
```

例如：

```
# 第一种用法，生成代码文件列表
#先直接设置SRC_LIST的值
set(SRC_LIST add.h add.cpp)
#然后再在SRC_LIST中追加main.cpp
set(SRC_LIST ${SRC_LIST} main.cpp)

# 第二种用法，设置库生成目录或者可执行文件生成目录
set( LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib/linux)
set( EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
```

**1.4 设置编译类型**

```
# 编译静态库
add_library(库名称 STATIC 代码文件名称)

# 编译动态库
add_library(库名称 SHARED 代码文件名称)

# 编译可执行程序
add_executable(可执行程序名 代码文件名称)
```

例如：

```
# 编译静态库
add_library(add STATIC add.h add.cpp)
add_library(add STATIC ${ADD_SRC} ${ADD_HDR})

# 编译动态库
add_library(add SHARED add.h add.cpp)
add_library(add SHARED ${ADD_SRC} ${ADD_HDR})

# 编译可执行程序
add_executable(main add.h add.cpp mai.cpp)
add_executable(main ${MAIN_SRC} ${MAIN_HDR})
```

**1.5 指定静态库或者动态库编译输出目录**

例如将当前编译的静态库或者动态库输出到当前项目文件夹 lib 子目录下：

```
set(LIBRARY_OUTPUT_PATH  ${PROJECT_SOURCE_DIR}/lib)
```

**1.6 指定可执行程序编译输出目录**

例如将当前可执行程序输出到当前项目文件夹的 bin 子目录下：

```
#设定可执行二进制文件的目录
set( EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
```

**1.7 设置链接库搜索目录**

例如将链接库搜索目录设置为当前项目文件夹下 lib/linux 文件夹：

```
link_directories( ${PROJECT_SOURCE_DIR}/lib/linux)
```

**1.8 设置包含目录**

例如将包含目录设置为当前项目文件夹下 include 文件夹：

```
include_directories(${PROJECT_SOURCE_DIR}/include)
```

**1.9 设置宏定义**

```
#预定义宏
add_definitions(-D宏名称)
```

例如：

```
add_definitions(-DWINDOWS)
add_definitions(-DLINUX)
```

**1.10 链接静态库**

```
link_libraries(
    静态库1
    静态库2
    静态库3
    ...
)
```

注意，link_libraries 中的静态库为全路径，常与 1.7 link_directories 搭配使用，例如：

lib1.a lib2.a 在目录${PROJECT_SOURCE_DIR}/lib/linux 下，则先设置链接目录，再链接相应的库：

```
#设置链接目录
link_directories( ${PROJECT_SOURCE_DIR}/lib/linux)
link_libraries(
        lib1.a
        lib2.a
)
```

**1.11 链接动态库**

```
target_link_libraries(所需生成的文件名称 所需链接的动态库名称)
```

例如：

```
target_link_libraries(main dl)
```

**1.12 link_libraries 和 target_link_libraries 区别**

在 cmake 语法中，link_libraries 和 target_link_libraries 是很重要的两个链接库的方式，虽然写法上很相似，但是功能上有很大区别：

```
(1) link_libraries用在add_executable之前，target_link_libraries用在add_executable之后
(2) link_libraries用来链接静态库，target_link_libraries用来链接导入库，即按照header file + .lib + .dll方式隐式调用动态库的.lib库
```

**1.13 file 语法**

**1.13.1 将文件夹所有的类型的文件添加到文件列表**

例如将当前文件夹下所有.cpp 文件的文件名加入到 MAIN_SRC 中，将当前文件夹下所有.h 加入到 MAIN_HDR 中。

```
file(GLOB MAIN_SRC ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
file(GLOB MAIN_HDR ${CMAKE_CURRENT_SOURCE_DIR}/*.h)
```

例如将当前文件[夹子](https://m.hqchip.com/app/1601)目录 src 文件夹下所有.cpp 文件的文件名加入到 MAIN_SRC 中，将当前文件夹子目录 src 文件夹下所有.h 加入到 MAIN_HDR 中。

```
file(GLOB MAIN_SRC ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp)
file(GLOB MAIN_HDR ${CMAKE_CURRENT_SOURCE_DIR}/src/*.h)
```

**1.13.2 递归搜索该文件夹，将文件夹下（包含子目录）符合类型的文件添加到文件列表**

例如将当前文件夹下（包括子目录下）所有.cpp 文件的文件名加入到 MAIN_SRC 中，所有.h 加入到 MAIN_HDR 中：

```
file(GLOB_RECURSE MAIN_SRC ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
file(GLOB_RECURSE MAIN_HDR ${CMAKE_CURRENT_SOURCE_DIR}/*.h)
```

**1.14 List 操作**

常见的 List 操作包括：

```
list(LENGTH  )
list(GET   [ ...]
   )
list(APPEND  [ ...])
list(FIND   )
list(INSERT    [ ...])
list(REMOVE_ITEM   [ ...])
list(REMOVE_AT   [ ...])
list(REMOVE_DUPLICATES )
list(REVERSE )
list(SORT )
```

**1.14.1 List 移除指定项**

例如从 MAIN_SRC 移除指定项：

```
list(REMOVE_ITEM MAIN_SRC ${CMAKE_CURRENT_SOURCE_DIR}/add.cpp)
```

**1.14.2 将两个 List 链接起来**

```
# 搜索当前目录
file(GLOB  MAIN_SRC ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
file(GLOB  MAIN_HDR ${CMAKE_CURRENT_SOURCE_DIR}/*.h)

# 递归搜索当前目录下src子目录
file(GLOB_RECURSE MAIN_SRC_ELSE  ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp)
file(GLOB_RECURSE MAIN_HDR_ELSE  ${CMAKE_CURRENT_SOURCE_DIR}/src/*.h)

# 将MAIN_SRC_ELSE中的值添加到MAIN_SRC
# 将MAIN_HDR_ELSE中的值添加到MAIN_HDR
list(APPEND MAIN_SRC ${MAIN_SRC_ELSE})
list(APPEND MAIN_HDR ${MAIN_HDR_ELSE})
```

**1.15 添加子文件夹**

例如：

```
add_subdirectory(src)
```

该语句会在执行完当前文件夹 CMakeLists.txt 之后执行 src 子目录下的 CMakeLists.txt

**1.16 message 输出消息机制**

输出正常：

```
message(STATUS "Enter cmake ${CMAKE_CURRENT_LIST_DIR}")
```

输出警告：

```
message(WARNING "Enter cmake ${CMAKE_CURRENT_LIST_DIR}")
```

输出错误：

```
message(FATAL_ERROR "Enter cmake ${CMAKE_CURRENT_LIST_DIR}")
```

**1.17 安装**

install 指令用于定义安装规则，安装的内容包括二进制可执行文件、动态库、静态库以及文件、目录、脚本等。

**1.17.1 目标文件安装** 例如：

```
install(TARGETS util
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib)
```

ARCHIVE 指静态库，LIBRARY 指动态库，RUNTIME 指可执行目标二进制，上述示例的意思是：

如果目标 util 是可执行二进制目标，则安装到 `${CMAKE_INSTALL_PREFIX}/bin` 目录 如果目标 util 是静态库，则安装到安装到 `${CMAKE_INSTALL_PREFIX}/lib` 目录 如果目标 util 是动态库，则安装到安装到 `${CMAKE_INSTALL_PREFIX}/lib` 目录。

**1.17.2 文件夹安装**

```
install(DIRECTORY include/ DESTINATION include/util)
```

这个语句的意思是将 include/目录安装到 include/util 目录。

**1.18 设置编译选项**

设置编译选项可以通过 add_com[pi](https://www.elecfans.com/tags/pi/)le_options 命令，也可以通过 set 命令修改 CMAKE_CXX_FLAGS 或 CMAKE_C_FLAGS。方式 1：

```
set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -march=native -O3 -frtti -fpermissive -fexceptions -pthread")
```

方式 2：

```
add_compile_options(-march=native -O3 -fexceptions -pthread -fPIC)
```

这两种方式的区别在于：

```
add_compile_options命令添加的编译选项是针对所有编译器的(包括c和c++编译器)，而set命令设置CMAKE_C_FLAGS或CMAKE_CXX_FLAGS变量则是分别只针对c和c++编译器的。
```

**1.19 预定义变量**

### **1.19.1 基本变量**

- **PROJECT_SOURCE_DIR**

- 我们使用 cmake 命令后紧跟的目录，一般是工程的根目录；

- **PROJECT_BINARY_DIR**

  执行 cmake 命令的目录,通常是${PROJECT_SOURCE_DIR}/build；

- **CMAKE_INCLUDE_PATH**

  系统环境变量,非 cmake 变量；

- **CMAKE_LIBRARY_PATH**

  系统环境变量,非 cmake 变量；

- **CMAKE_CURRENT_SOURCE_DIR**

  当前处理的 CMakeLists.txt 所在的路径；

- **CMAKE_CURRENT_BINARY_DIR**

  target 编译目录（使用 ADD_SURDIRECTORY(src bin)可以更改此变量的值 ，SET(EXECUTABLE_OUTPUT_PATH <新路径>)并不会对此变量有影响,只是改变了最终目标文件的存储路径）；

- **CMAKE_CURRENT_LIST_FILE**

  输出调用这个变量的 CMakeLists.txt 的完整路径；

- **CMAKE_CURRENT_LIST_LINE**

  输出这个变量所在的行；

- **CMAKE_MODULE_PATH**

  定义自己的 cmake 模块所在的路径（这个变量用于定义自己的 cmake 模块所在的路径，如果你的工程比较复杂，有可能自己编写一些 cmake 模块，比如 SET(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake),然后可以用 INCLUDE 命令来调用自己的模块）；

- **EXECUTABLE_OUTPUT_PATH**

  重新定义目标二进制可执行文件的存放位置；

- **LIBRARY_OUTPUT_PATH**

  重新定义目标链接库文件的存放位置；

- **PROJECT_NAME**

  返回通过 PROJECT 指令定义的项目名称；

- **CMAKE_ALLOW_LOOSE_LOOP_CONSTRUCTS**

  用来控制 IF ELSE 语句的书写方式；

### **1.19.2 [操作系统](https://www.elecfans.com/v/tag/527/)变量**

- **CMAKE_MAJOR_VERSION**

  cmake 主版本号,如 3.4.1 中的 3；

- **CMAKE_MINOR_VERSION**

  cmake 次版本号,如 3.4.1 中的 4；

- **CMAKE_PATCH_VERSION**

  cmake 补丁等级,如 3.4.1 中的 1；

- **CMAKE_SYSTEM**

  操作系统名称，包括版本名，如 Linux-2.6.22；

- **CAMKE_SYSTEM_NAME**

  操作系统名称，不包括版本名，如 Linux；

- **CMAKE_SYSTEM_VERSION**

  操作系统版本号,如 2.6.22；

- **CMAKE_SYSTEM_PROCESSOR**

  电脑

  处理器

  名称，如

  i686；

- **UNIX**

  在所有的类 UNIX 平台为 TRUE,包括 OS X 和 cygwin，Linux/Unix 操作系统；

- **WIN32**

  在所有的 win32 平台为 TRUE,包括 cygwin，Windows 操作系统；

- **APPLE**

  苹果操作系统；

例如操作系统判断方式一：

```
if(WIN32)
    message(STATUS “This operating system is Windows.”)
elseif(UNIX)
    message(STATUS “This operating system is Linux.”)
elseif(APPLE)
    message(STATUS “This operating system is APPLE.”)
endif(WIN32)
```

操作系统判断方式二：

```
if (CMAKE_SYSTEM_NAME MATCHES "Linux")
    message(STATUS "current platform: Linux ")
elseif (CMAKE_SYSTEM_NAME MATCHES "Windows")
    message(STATUS "current platform: Windows")
elseif (CMAKE_SYSTEM_NAME MATCHES "FreeBSD")
    message(STATUS "current platform: FreeBSD")
else ()
    message(STATUS "other platform: ${CMAKE_SYSTEM_NAME}")
endif (CMAKE_SYSTEM_NAME MATCHES "Linux")
```

### **1.19.3 开关选项**

- BUILD_SHARED_LIBS

  控制默认的库编译方式。如果未进行设置,使用 ADD_LIBRARY 时又没有指定库类型,默认编译生成的库都是静态库；

- **CMAKE_C_FLAGS**

  设置 C 编译选项，也可以通过指令 ADD_DEFINITIONS()添加；

- **CMAKE_CXX_FLAGS**

  设置 C++编译选项，也可以通过指令 ADD_DEFINITIONS()添加；

- **CMAKE_C_COMPILER**

  指定 C 编译器；

- **CMAKE_CXX_COMPILER**

  指定 C++编译器；

- CMAKE_BUILD_TYPE==::build 类型(Debug, Release, …)

  CMAKE_BUILD_TYPE=Debug

### **1.19.4 环境变量**

设置环境变量：

```
set(env{name} value)
```

调用环境变量：

```
$env{name}
```

例如：

```
message(STATUS "$env{name}")
```

### 1.19.5 CMAKE_INCLUDE_CURRENT_DIR

自动添加 CMAKE_CURRENT_BINARY_DIR 和 CMAKE_CURRENT_SOURCE_DIR 到当前处理 的 CMakeLists.txt。相当于在每个 CMakeLists.txt 加入：

```
include_directories(${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR})
```

### **1.20 条件判断**

### **1.20.1 逻辑判断和比较**

- **if (expression)**：expression 不为空时为真，false 的值包括（0,N,NO,OFF,FALSE,NO[TF](https://www.hqchip.com/app/1522)OUND）；
- **if (not exp)**：与上面相反；
- **if (var1 AND var2)**：如果两个变量都为真时为真；
- **if (var1 OR var2)**：如果两个变量有一个为真时为真；
- **if (COMMAND cmd)**：如果 cmd 确实是命令并可调用为真；
- **if (EXISTS dir) if (EXISTS file)**：如果目录或文件存在为真；
- **if (file1 IS_NEWER_THAN file2)**：当 file1 比 file2 新，或 file1/file2 中有一个不存在时为真，文件名需使用全路径；
- **if (IS_DIRECTORY dir)**：当 dir 是目录时为真；
- **if (DEFINED var)**：如果变量被定义为真；
- **if (var MATCHES regex)**：给定的变量或者字符串能够匹配正则表达式 regex 时为真，此处 var 可以用 var 名，也可以用 ${var}；
- **if (string MATCHES regex)**：给定的字符串能够匹配正则表达式 regex 时为真。

### 1.20.2 数字比较

- **if (variable LESS number)**：

  如果 variable 小于 number 时为真；

- **if (string LESS number)**：

  如果 string 小于 number 时为真；

- **if (variable GREATER number)**：

  如果 variable 大于 number 时为真；

- **if (string GREATER number)**：

  如果 string 大于 number 时为真；

- **if (variable EQUAL number)**：

  如果 variable 等于 number 时为真；

- **if (string EQUAL number)**：

  如果 string 等于 number 时为真。

### **1.20.3** **\*\*字母表\*\*\*\***顺序比较\*\*

- **if (variable STRLESS string)**
- **if (string STRLESS string)**
- **if (variable STRGREATER string)**
- **if (string STRGREATER string)**
- **if (variable STREQUAL string)**
- **if (string STREQUAL string)**

### **1.21 循环**

### 1.21.1 fore[ac](https://m.hqchip.com/app/1703)h

start 表示起始数，stop 表示终止数，step 表示步长

```
foreach(loop_var RANGE start stop [step])
    ...
endforeach(loop_var)
```

### **1.21.2 while**

```
while(condition)
    ...
endwhile()
```

### 1.22 自动检测编译器是否支持 C++11

```
include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
else()
    message(STATUS "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()
```

### 1.23 CMake 生成 VS 解决方案将项目放置在设定文件夹下

例如，我们在工程中引用了许多的第三方开源库，这些库的源码与自己所写的代码需要进行区分和隔离，通常情况下会单独开一个 third 筛选器存储这些第三方库的项目，怎么做？

- 第一步：

在第三方库的 CMakeLists.txt 中 cmake_minimum_required(VERSION 2.6)中加上 set_property(GLOBAL PROPERTY USE_FOLDERS On)

- 第二步：在生成编译目标的语法之后，如：

```
add_executable(demo demo.cpp) # 生成可执行文件
add_library(common STATIC util.cpp) # 生成静态库
add_library(common SHARED util.cpp) # 生成动态库或共享库
```

加入一句：

```
set_target_properties(${第三方库项目名称} PROPERTIES FOLDER “目标文件夹名称”)
```
