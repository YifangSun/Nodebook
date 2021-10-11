## 运算符

### :=

赋值同时初始化，只能在函数内使用。全局变量还是要用var。



## 类型

### channel

类似于通道、消息队列

```go
c := make(chan int)
ch := make(chan int, 100) //指定了缓冲区大小
c <- 3 //传入 send
i := <-c //receive
```

可以阻塞：

- 如果创建时未指定缓冲大小，则没有结果时，接收端会阻塞。
- 如果创建时指定了大小，则会放在缓存中。（缓存满了则阻塞）

### map

ma := make(map[string]int)

ma["a"] = 33

fmt.Println(ma)



## 函数

### 结构函数 - 名字前有参数

https://www.cnblogs.com/sunylat/p/6384721.html

### defer

defer的代码，会在return之后执行，可以用来清理变量

 [golang中defer的使用规则](https://www.cnblogs.com/vikings-blog/p/7099023.html)

### select{}

类似于unix的监控处理IO的select操作。golang中只能用于执行channel相关的操作。

### 函数导出、首字母

模块中要导出的函数，必须首字母大写。

## 编译相关

### go build

生成的文件名是文件夹的名字

go.mod进行包路径的配置

## context库

引用：https://www.jianshu.com/p/755426897746

**有两种context：**

context.Background()

context.TODO()

**四种方法可以返回context：**

context.WithCancel()

context.WithDeadline()

context.WithTimeout()

context.WithTimeout()

**示例：**

```go
context.WithCancel(context.Background())
```



## cli库

### flag

某个flag的shortname不能是h，否则会因为与-help的-h冲突而报错

#### stringSlice

**接收所有：**

str1,str2

"str1","str2"

**只接收第一个：**

[str1,str2] 整体当做一个字符串了

["str1","str2"] 整体当做一个字符串了

str1 str2

"str1" "str2"

[str1 str2] 接收到[str1

["str1" "str2"] 接收到[str1

{str1,str2} 接收到{str1,

{"str1","str2"} 接收到{str1,
