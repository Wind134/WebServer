# WebServer

基于C++ 11实现的高性能服务器，webbench压测可达15000以上的QPS(Queries Per Second)；

但需要注意的是，QPS并不是衡量服务器的唯一指标，响应时间和并发连接数也是很重要的参考，该项目主要以QPS结果为参考；

## 改进及功能

### 改进

- 重写了线程池，整个服务器性能有一定提升，重写的线程池主要包括以下几个部分：
  - 在创建线程池的循环中，将线程对象加入vector数组，线程的创建过程更加直观和易于理解；
  - 重写了任务的提交函数，通过bind处理了含参数任务的提交；
  - 简化了类的成员表达形式，使整个工程更加直观；
- 在HTTP请求报文的处理环节中，精简了一些变量的处理；

### 功能

- 高效健全的异步日志处理系统；
- 实现了超时任务的自动处理；
- 设计了一个数据库连接池，减少频繁建立与关闭数据库的开销；
- 基于正则表达式以及枚举状态机实现了对HTTP请求报文与相应报文的解析和发送；
- 实现了一个动态增长的缓冲区；
- 具有一定的高并发处理能力；

## 框架结构

待补充！

## 运行环境
```
系统：Arch Linux
CPU：intel i5 1135G7
编程工具：C++14，MySQL
```
## 启动方式

先编译，makefile文件会在项目地址处新建文件夹，进入项目文件夹根目录，`make`编译；

在**项目**文件夹下运行：`./bin/server`，为什么要在项目文件夹下运行请看[注意事项](#注意事项)；


## 压力测试

通过webbench进行压力测试，该工具的获取既可以基于源码安装，同时可以根据你自身的发行版安装！

### 获取方式
- **Arch Linux**

直接从万能的AUR中搜索下载即可：`yay -S webbench`

- **其他**

源码编译安装即可，[源码地址](http://ibiblio.org/pub/Linux/apps/www/servers/webbench-1.5.tar.gz)；

**编译事项:** make记得加参数，因为wenbench中包含的诸多头文件在现代发行版已经转移位置；

`CPPFLAGS=-I/usr/include/tirpc make`

## 性能表现



## 注意事项
通过makefile编译程序之后，要在WebServer-Self的文件夹目录下运行服务器程序，否则无法获取到resources路径信息，导致浏览器访问失败；

这是因为源码中getcwd函数只能获取终端所在文件夹的路径，这部分还有优化空间，后续考虑更改路径获取策略；

## 遗留问题

webbench压测过后，再次压测性能表现异常，监测硬件资源时表现在CPU基本没有占用；

## 致谢

TCP/IP网络编程 [韩] 尹圣雨 著	金国哲 译。

Linux高性能服务器编程，游双著。

@[markparticle](https://github.com/markparticle/WebServer)

@[qinguoyi](https://github.com/qinguoyi/TinyWebServer)