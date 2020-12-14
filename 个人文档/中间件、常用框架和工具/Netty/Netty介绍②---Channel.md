### `Channel`
`Channel`是`Netty`的传输`API`的核心，它被用作所有的`IO`操作。
`io.netty.channel.channel`是Netty网络操作抽象类，它聚合了一组功能，包括但不限于网络的读、写、客户端发起的连接等功能。
`Channel`是连接了网络套接字或能够进行`I/O`操作（`read()`、`write()`、`connect()`、`bind()`）的组件。

![](C:\Users\Administrator\Desktop\文档图片文件夹\Netty\继承图\Channel\NettyChannelUML.png)

> 这张图稍微看一下就可以了
从`UML` 图中我们知道该接口的基本为`Channel`族的顶层，不过它存在一个更为顶级的抽象接口
我们首先从该类开始分析。
方法|说明
--|--
`ByteBufAllocator alloc()`|返回分配的`ByteBufAllocator`，它将用于分配ByteBufs。
`long bytesBeforeUnwritable()`|获取直到`isWritable()`返回`false`为止可以写入的字节数。
`long bytesBeforeWritable()`|获取必须从基础缓冲区中耗尽多少字节，直到`isWritable()`返回`true`。
`ChannelFuture closeFuture()`|返回`ChannelFuture`，当`channel`通道关闭时，改通道关闭
`ChannelConfig config()`|返回该`channel`管道的配置类
`EventLoop eventLoop()`|返回该`channel`注册的`EventLoop`
`ChannelId id()`|返回该`Channel`的唯一标识
`boolean isActive()`|如果此通道处于活动并已连接，则返回`true`
`boolean isOpen()`|如果该通道处于打开状态，返回`true`
`boolean isRegistered()`|如果该`Channel`已向`EventLoop注册`，返回`true`
`boolean isWritable()`|当且仅当 `I/O`线程立即被执行请求的写操作时，才回返回`true`
`ChannelPipeline pipeline()`|返回该`Channel`分配的`ChannelPipeline`
> 方法的说明是`Netty API`文档中的
