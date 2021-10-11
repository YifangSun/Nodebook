### 安装

http://download.redis.io/releases/

下载tar包。我下载的是最新的redis-6.2.3.tar.gz

```shell
tar zxvf redis-6.2.3.tar.gz
cd redis-6.2.3
make install
```

如果直接`make`，提示需要安装tcl8.5，因为tests文件夹下测试用例都是tcl脚本。此时需要`make clean`再`make install`。直接`make install`可以避免这种麻烦。

### 连接工具（hiredis）

#### apt安装

`apt-get install libhiredis-dev`

默认安装hiredis-dev及其依赖的hiredis0.13。

apt默认的安装路径为：

头文件：/usr/include/hiredis

库文件：/usr/lib/x86_64-linux-gnu

#### 源码安装

```shell
wget https://github.com/redis/hiredis/archive/refs/tags/v1.0.0.tar.gz
tar zxvf v1.0.0.tar.gz
cd hiredis-1.0.0/
make
sudo make install
sudo ldconfig
```

这里文件默认的安装路径为：

头文件：/usr/local/include/hiredis

库文件：/usr/local/lib

### 例程

#### 例程1

[代码见附录1](#附录1)（摘自https://blog.csdn.net/ggm0928/article/details/83687268）

`g++ test.cpp -o test -lhiredis`

#### 例程2

[官方库中的例子](https://github.com/redis/hiredis)

git clone下载再编译，最基本的例子为example.c。过程中注意两个问题：

1. 官方的例子中头文件为\#include <hiredis.h>，而[例程1](#附录1)中的头文件路径为#include "hiredis/hiredis.h" 。这里需要改一下路径，或者加-I/usr/include/hiredis。

2. 有可能会报错：error: invalid conversion from 'void*' to 'redisReply*'，[例程1](#附录1)中使用强制转换(redisReply\*)避免了这个问题：
   <code>redisReply* r = <font color=red>(redisReply*)</font>redisCommand(c, command1); </code>


### 附录

#### 附录1

```c++
#include <stdio.h>  
#include <stdlib.h>  
#include <stddef.h>  
#include <stdarg.h>  
#include <string.h>  
#include <assert.h>  
#include "hiredis/hiredis.h"  
 
void doTest()  
{  
    //redis默认监听端口为6387 可以再配置文件中修改  
    redisContext* c = redisConnect("127.0.0.1", 6379);  
    if ( c->err)  
    {  
        redisFree(c);  
        printf("Connect to redisServer faile\n");  
        return ;  
    }  
    printf("Connect to redisServer Success\n");  
      
    const char* command1 = "set stest1 value1";  
    redisReply* r = (redisReply*)redisCommand(c, command1);  
      
    if( NULL == r)  
    {  
        printf("Execut command1 failure\n");  
        redisFree(c);  
        return;  
    }  
    if( !(r->type == REDIS_REPLY_STATUS && strcasecmp(r->str,"OK")==0))  
    {  
        printf("Failed to execute command[%s]\n",command1);  
        freeReplyObject(r);  
        redisFree(c);  
        return;  
    }     
    freeReplyObject(r);  
    printf("Succeed to execute command[%s]\n", command1);  
      
    const char* command2 = "strlen stest1";  
    r = (redisReply*)redisCommand(c, command2);  
    if ( r->type != REDIS_REPLY_INTEGER)  
    {  
        printf("Failed to execute command[%s]\n",command2);  
        freeReplyObject(r);  
        redisFree(c);  
        return;  
    }  
    int length =  r->integer;  
    freeReplyObject(r);  
    printf("The length of 'stest1' is %d.\n", length);  
    printf("Succeed to execute command[%s]\n", command2);  
      
      
    const char* command3 = "get stest1";  
    r = (redisReply*)redisCommand(c, command3);  
    if ( r->type != REDIS_REPLY_STRING)  
    {  
        printf("Failed to execute command[%s]\n",command3);  
        freeReplyObject(r);  
        redisFree(c);  
        return;  
    }  
    printf("The value of 'stest1' is %s\n", r->str);  
    freeReplyObject(r);  
    printf("Succeed to execute command[%s]\n", command3);  
      
    const char* command4 = "get stest2";  
    r = (redisReply*)redisCommand(c, command4);  
    if ( r->type != REDIS_REPLY_NIL)  
    {  
        printf("Failed to execute command[%s]\n",command4);  
        freeReplyObject(r);  
        redisFree(c);  
        return;  
    }  
    freeReplyObject(r);  
    printf("Succeed to execute command[%s]\n", command4);     
      
      
    redisFree(c);  
      
}  
 
int main()  
{  
    doTest();  
    return 0;  
} 
```





