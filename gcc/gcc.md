### 编译过程

https://blog.csdn.net/qq_43515054/article/details/116457813

### 编译踩坑

#### 1.一定要有swap内存

使用free查看内存，如果没有swap内存会报错：

fatal error: ld terminated with signal 9 [Killed

添加swap内存：

https://blog.csdn.net/abrahamchen/article/details/53081361

https://blog.csdn.net/longkg/article/details/12839173