### `Netty`基本介绍
> 在学习这个`Netty`时，应该有一些网络编程技巧和线程相关的基础知识

`Neey`是一款异步的事件驱动的网络应用程序框架，支持快速地开发可维护的高性能的面向协议的服务端和客户端。
它是一款基于非阻塞`IO`（`NIO`）开发的网络通信框架，对比阻塞`IO`（`BIO`），它的并发性能得到了极大的提升。

### `Netty`特性总结

分类|特性
--|--
设计|统一的`API`文档，支持多种传输类型。<br>强大的线程模型。<br>真正的无连接数据报套接字支持。<br>连接逻辑支持复用
性能|比`Java`的网络`API`更高吞吐量以及更低的延迟。<br>得益于池化和复用，拥有更低的资源消耗。<br>最少的资源复制
健壮性|不会因慢速、快速或超载的连接而导致`OutOfMemoryError`。<br>消除在高速网络中`NIO`应用程序常见的不公平读/写比例
安全性|完整的`SSL/TLS`以及`StartTLS`支持。<br>可用于受限环境下，如`Applet`和`OSGL`

### `Netty`的线程模型
随着硬件性能的提升，`CPU`核数越来越多。我们可以通过多线程编程来有效的利用`CPU`能力，提升系统的处理效率和并发性能。<br>
而在之后为了提升多线程编程的效率和性能，`Java`提供了线程池、线程安全容器、原子类等。<br>
在之后的网络编程框架中，`Reactor`被大量的使用。`Reactor`模式本身时基于事件驱动，适合处理海量`IO`事件
#### `Reactor`模型
`Netty`、`Redis`就是典型的`Reactor`模型结构。
`《Scalable IO Java》`中介绍的`Reactor`模型的主要由三个角色：
- `Reactor`把`IO`事件分配给对应的`Handler`处理
- `Acceptor`处理客户端连接
- `Handler`处理非阻塞任务
##### 单`Reactor`单线程模式
`Java`的`NIO`模式的`Selector`网络通讯，其实就是一个简单的`Reactor`模型。
![单Reactor单线程流程图](C:\Users\Administrator\Desktop\文档图片文件夹\Netty\Reactor模型\单Reactor单线程流程图.png)
多个客户端连接一个服务端，由`Reactor`去接收客户端连接请求，然后根据对应的事件交给对应的`Handler`处理。
只是利用一个线程来完成，所有的操作，导致他的并发处理能力没有想象的优秀。
##### 单`Reactor`多线程模型
在原来的基础上利用多线程线程池技术，来提高并发效果。
![单Reactor多线程流程图](C:\Users\Administrator\Desktop\文档图片文件夹\Netty\Reactor模型\单Reactor多线程流程图.png)
和单线程`Reactor`模型不同的是，多线程的`Reactor`模型让`Reactor`处理的功能进行分离，`Reactor`只负责客户端的连接事件和读写事件，业务处理交给线程池，充分发挥`CPU`性能。
当然，启用了多线程的技术，也是会导致共享数据和线程安全问题。在更高级别的并发情况下，单`Reactor`还是有些力不从心。

##### 主从`Reactor`多线程模型
主从`Reactor`模型将原来的模型`Reactor`部分进行了拆分。
![主从Reactor模型流程图](C:\Users\Administrator\Desktop\文档图片文件夹\Netty\Reactor模型\主从Reactor模型流程图.png)
`mainReactor`模型只作接收客户端的连接，其他的`Reactor` 模型来作读写操作，业务还是交给线程池处理。

> `Netty`采用的是主从`Reactor`线程模型
