## 语句


### include

包含cmake文件或模块，用法：

`include(<file|module> [OPTIONAL] [RESULT_VARIABLE <VAR>] [NO_POLICY_SCOPE])`

例：

`include(rpcgen)`

`include(set_cxx_norm.cmake)`

### set

### set_target_properties

设置目标的属性，所有属性如下：

https://cmake.org/cmake/help/latest/manual/cmake-properties.7.html#target-properties

### if

```cmake
if()
else()
endif()
```

### add_library()

将指定的源文件生成链接文件

如：

```cmake
SET(LIBHELLO_SRC hello.c) 
ADD_LIBRARY(hello SHARED ${LIBHELLO_SRC})
```
### add_executable()

### target_link_libraries

目标与其他库进行静态链接。目标是add_library或add_executable生成的。

例如：

```cmake
TARGET_LINK_LIBRARIES(myProject libeng.so)　　#这些库名写法都可以。
TARGET_LINK_LIBRARIES(myProject eng)
```

### function

```cmake
function(函数名)
endfunction()
```
### cmake_parse_argument

https://www.cnblogs.com/gaox97329498/p/10991449.html

## 变量

#### CMAKE_CURRENT_SOURCE_DIR

当前文件夹



