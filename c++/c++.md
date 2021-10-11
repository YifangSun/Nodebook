## 编译

### 编译指令

摘自：https://blog.csdn.net/lin_008/article/details/77600483

#### -I (大写i)

编译程序按照-I指定的路进去搜索头文件。

-I/home/include/表示将-I/home/include/目录作为第一个寻找头文件的目录，寻找的顺序是：

 /home/include/ -->/usr/include-->/usr/local/include

#### -L(大写l)

表示：编译程序按照－L指定的路进去寻找库文件，一般的在-L的后面可以一次用-l指定多个库文件。

-L/lib/表示到/lib/目录下找库文件

#### -l(小写l)

表示：编译程序到系统默认路进搜索，如果找不到，到当前目录，如果当前目录找不到，则到LD_LIBRARY_PATH等环境变量置顶的路进去查找，如果还找不到，那么编译程序提示找不到库。

本例子使用的是gunzip库，库文件名是libz.so，库名是z。很容易看出，把库文件名的头lib和尾.so去掉就是库名了。

**例：**

−L/usr/lib −lprotobuf

#### --shared -fPIC(创建静态库)

<font color=gray>参考：https://blog.csdn.net/derkampf/article/details/69660050</font>

-fPIC 作用于编译阶段，告诉编译器产生与位置无关代码(Position-Independent Code)，则产生的代码中，没有绝对地址，全部使用相对地址，故而代码可以被加载器加载到内存的任意位置，都可以正确的执行。这正是共享库所要求的，共享库被加载时，在内存的位置不是固定的。

```shell
gcc -shared -fPIC -o 1.so 1.c
```

#### *创建动态库

<font color=gray>参考：https://www.cnblogs.com/king-lps/p/7757919.html</font>

Linux创建静态库过程如下：

首先，将代码文件编译成目标文件.o（StaticMath.o）

`g++ -c StaticMath.cpp`

注意带参数-c，否则直接编译为可执行文件

然后，通过ar工具将目标文件打包成.a静态库文件

`ar -crv libstaticmath.a StaticMath.o`

### cmake

.PHONY：https://www.cnblogs.com/idorax/p/9306528.html

## 语法

### lambda

#### 捕获

**值捕获**其实调用了拷贝构造。我删除了默认拷贝构造，值捕获时会报错，error: use of deleted function ……

**引用捕获**什么也不调用。

**move捕获**调用右值拷贝构造。

### 异常

#### bad_alloc()

bad_alloc( )和bad_cast() 不能有参数，可以throw bad_alloc();

其余的异常都可以用字符串初始化。如throw runtime_error("aaaa");

#### catch

只能跟在try{ }后面

### class相关

#### protect

类外不可见，子类可见。private，类外和子类都不可见。

#### 友元

友元函数，类外的函数也可以访问自己类的private。

友元类，这其中的成员函数也都可以访问自己类的private。

友元不能继承

不能传递（A{	friend B}; B{   friend C}）

不能交换(A是B友元，B不一定是A友元)。

```c++
class Point
{
public:
    Point(double xx, double yy)
    {
        x = xx;
        y = yy;
    };
    friend double Distance(Point &a, Point &b);
    friend class B;
    
private:
    double x, y;
};

double Distance(Point &a, Point &b)
{}

class B{
    
}
```

### this_thread
C++11提供了一个命名空间this_thread来引用当前线程，该命名空间有4个有用的函数，get_id, yield, sleep_until, sleep_for。

### std命名空间

#### apply()

apply(func, tuple): 把tuple里的数据，当做参数输入进func，并执行。

#### condition_variable.h

#### decay()

类型退化。移除const、引用、数组等，如左值变右值、数组变指针、函数变指针，一般搭配其他模板使用。如std::is_same。

```c++
// 特别地，c14中有：
template< class T >
using decay_t = typename decay<T>::type;

// 使用：
decat_t<const int&>即为int类型
```

参考：

博客：https://blog.csdn.net/czyt1988/article/details/52812797

cpp官网：https://en.cppreference.com/w/cpp/types/decay

#### forward()

完美转发。可以转发函数、参数

**std::forward_as_tuple:**转发完变成一个tuple

#### move()

#### mem_fn()

把成员函数包装成函数指针。把类当做其第一个参数即可。

#### tuple_cat()

把参数合并成一个tuple

#### visit()

std::visit(func, var);

将var作为func的参数，调用func。func可以是lambda、函数、重载()的类，等等可调用对象。

https://blog.csdn.net/janeqi1987/article/details/100568146



### 形参与实参

| 形参\实参 | 值                                     | 引用                     | 右值                         |
| --------- | -------------------------------------- | ------------------------ | ---------------------------- |
| 值        | 可。调用引用拷贝构造。                 | 同左。实参传引用即传值。 | 可。调用右值拷贝构造。       |
| 引用      | 可。不调用任何，函数中使用参数原地址。 | 同左。实参传引用即传值。 | 不可。右值不能绑定到左值上。 |
| 右值      | 不可。右值不能绑定到左值上。           | 同左。实参传引用即传值。 | 可。不调用任何。             |

**注**：值拷贝构造不合法。即：A(A a)

右值拷贝构造：A(A&& a)

引用拷贝构造：A(A& a)  默认拷贝构造。

## 概念解释

### qualifier

限定词。cv-qualifier，即const和volatile。