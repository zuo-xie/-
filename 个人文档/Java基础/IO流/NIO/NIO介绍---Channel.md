### `Channel`（管道）
Java中的管道，由`java.nio.channels`包中定义，并定义了一些核心功能。<br>
它主要与缓冲区进行交互，本身是不能访问数据的。<br>
本质上类似传统的流，不过`Channel`可以同时进行读写操作。，`Channel`也可以实现异步读写数据。<br>

`Channel`的主要子接口
实现类|说明
--|--
`FileChannel`|从文件中读写数据
`DatagramChannel`|能通过UDP中读写数据
`SocketChannel`|能通过TCP读写网路数据
`ServerSocketChannel`|可以监听新进来的TCP连接，像Web服务器那样，对每一个新进来的连接都会创建一个`SocketChannel`

##### 获取通道的方式
- 对支持通道的类使用`getChannel()`方法。
- 各个通道的静态方法`open()`。
- `Files`工具类的`newByteChannel()`方法。

### `Channel`源码
`Channel`接口
```java
public interface Channel extends Closeable {
    //关闭管道
    public boolean isOpen();
    //告诉管道是否打开
    public void close() throws IOException;
}
```
它本身只提供了两个定义方法。<br>

我们主要是去看它的主要几个实现类。<br>
##### `FileChannel`

我们先来看一下如何获取到相应的管道，之前我们说过获取管道的三个方法。<br>
第一种，使用`getChannel()`
```java
FileChannel channel = new FileInputStream("").getChannel();


public FileChannel getChannel() {
    synchronized (this) {
        if (channel == null) {
            //底层调用FileChannel的open()
            channel = FileChannelImpl.open(fd, path, true, false, this);
        }
        return channel;
    }
}

public static FileChannel open(FileDescriptor var0, String var1, boolean var2, boolean var3, Object var4) {
    //去掉用fileChannelImpl的构造函数
    return new FileChannelImpl(var0, var1, var2, var3, false, var4);
}

private FileChannelImpl(FileDescriptor var1, String var2, boolean var3, boolean var4, boolean var5, Object var6) {
    //传参
    this.fd = var1;
    this.readable = var3;
    this.writable = var4;
    this.append = var5;
    this.parent = var6;
    this.path = var2;
    this.nd = new FileDispatcherImpl(var5);
}
```
> `FileChannelImpl`是`FileChannel`实现类。

第二种，各个通道的`open()`
```java
public static FileChannel open(Path path,
                                   Set<? extends OpenOption> options,
                                   FileAttribute<?>... attrs)
        throws IOException
    {
        FileSystemProvider provider = path.getFileSystem().provider();
        return provider.newFileChannel(path, options, attrs);
    }
```