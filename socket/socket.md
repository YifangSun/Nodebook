### sockaddr_in 

赋值语句：

```sockaddr_in.sin_family = AF_INET;``` 创建套接字时，用该字段指定地址家族，对于TCP/IP协议的，必须设置为AF_INET。

```sockaddr_in.sin_port = htons( 13 );``` 将监听套接字的端口设置为13，htons表示host to network short，用来进行主机字节序和网络字节序的转换。 

```
struct sockaddr_in { 
　　 short int sin_family; /* 通信类型 */ 
　　 unsigned short int sin_port; /* 端口 */ 
　　 struct in_addr sin_addr; /* Internet 地址 */ 
　　 unsigned char sin_zero[8]; /* 与sockaddr结构的长度相同*/ 
}; 
```

其中：

```
struct in_addr { 
　　 unsigned long s_addr; 
}; 
```
定义完sockaddr_in 后，要转换成sockaddr 格式。
```
struct sockaddr { 
　　 unsigned short sa_family; /* 地址家族, AF_xxx */ 
　　 char sa_data[14]; /*14字节协议地址*/ 
　　 }; 
```
