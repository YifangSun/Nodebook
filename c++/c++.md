# c++

## 异常

##### bad_alloc()

bad_alloc( )和 bad_cast() 不能有参数，可以throw	bad_alloc();

其余的异常都可以用字符串初始化。如throw 	runtime_error("aaaa");

##### catch

只能跟在try{ }后面

## 类

##### protect

类外不可见，子类可见。private，类外和子类都不可见。

##### 友元

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

## 库

##### this_thread
C++11提供了一个命名空间this_thread来引用当前线程，该命名空间有4个有用的函数，get_id, yield, sleep_until, sleep_for。
