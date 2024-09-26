## 参考

[菜鸟教程](https://www.runoob.com/cmake/cmake-tutorial.html)

[Cmake wiki](https://gitlab.kitware.com/cmake/community/-/wikis/home)

## 基础使用

文件:

`CMakeLists.txt`(注意大小写) 

基础构建:

```cmake
# 指定cmake最低版本
cmake_minimum_required(VERSION 3.10)

# 项目名称
project(Tutorial)

# 添加可执行文件
add_executable(Tutorial tutorial.cxx)
```

示例:

```cmake
cmake_minimum_required(VERSION 3.10)   # 指定最低 CMake 版本

project(MyProject VERSION 1.0)          # 定义项目名称和版本

# 设置 C++ 标准为 C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 添加头文件搜索路径
include_directories(${PROJECT_SOURCE_DIR}/include)

# 添加源文件
add_library(MyLib src/mylib.cpp)        # 创建一个库目标 MyLib
add_executable(MyExecutable src/main.cpp)  # 创建一个可执行文件目标 MyExecutable

# 链接库到可执行文件
target_link_libraries(MyExecutable MyLib)
```

## 常规构建命令

### 定义项目名称及语言

```cmake
project(ProjectName CXX) # CXX表示C++语言
```

### 指定源文件

```cmake
add_executable(ProjectName main.cpp other.cpp)
```

### 添加头文件搜索路径

```cmake
include_directories(/usr/local/include)
include_directories(.../your_hpp_path)
```

### 生成库文件

生成名为 `libname` 的库文件:

```cmake
# 创建静态库 .a .lib
add_library(libname STATIC src1.cpp src2.cpp) # 说明：STATIC表示静态库，libname表示生成的库文件名
```

```cmake
# 创建动态库 .so .dll
add_library(libname SHARED src1.cpp src2.cpp)
```

```cmake
# 创建对象库 .o .obj
add_library(libname OBJECT src1.cpp src2.cpp)
```

### 链接目标文件和库文件

链接 `libname1` 和 `libname2` 到 `ProjectName`:

```cmake
target_link_libraries(ProjectName libname1 libname2) # 说明：ProjectName表示目标文件名，libname表示库文件名
```

### 设置/使用变量

设置变量:

```cmake
set(SRC_LIST main.cpp test.cpp) # 设置变量
set(CMAKE_CXX_STANDARD 11) # 设置C++标准
set（CMAKE_CXX_STANDARD_REQUIRED ON） # 设置C++标准是否必须
```

使用变量:

```cmake
add_executable(ProjectName ${SRC_LIST}) # 使用变量
```

### 控制语句

选择语句:

```cmake
if (USE_MYMATH)
  include_directories ("${PROJECT_SOURCE_DIR}/MathFunctions")
  add_subdirectory (MathFunctions)
  set (EXTRA_LIBS ${EXTRA_LIBS} MathFunctions)
endif (USE_MYMATH)
```

循环语句:

```cmake
foreach (loop_var RANGE 10)
  message("loop_var = ${loop_var}")
endforeach(loop_var)
```


