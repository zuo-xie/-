### `ByteBuf`
`ByteBUf`是一个`Byte`数组的缓冲区，他的基本功能与`JDK`原生的`ByteBuf`一致。
`ByteBuf`的优点
- 可扩展（用户自定义缓冲区扩展）
- 零拷贝（通过内置地缓冲区类型实现）
- 读写模式切换便捷
- 支持池化

从逻辑上分，`ByteBuf`可分为4个部分
![](C:\Users\Administrator\Desktop\文档图片文件夹\Netty\继承图\ByteBuf\ByteBuf逻辑分层.png)
第一部分是已经丢弃的字节，数据是无效的。
第二部分是可读字节，这部分数据是 `ByteBuf `的主体数据， 从` ByteBuf` 里面读取的数据都来自这一部分。
第三部分的数据是可写字节，所有写到 `ByteBuf` 的数据都会写到这一段。
第四部分的字节，表示的是该 `ByteBuf` 最多还能扩容的大小。

`ByteBuf`通过3个整数指针，来有效的区分可读事件和可写事件，使他们没有冲突。
- `readerIndex`
	读指针 指向可读的起始位置，每读取一次字节，加1，一旦与`writerIndex`相等，则不可读。
- `writerIndex`
	写指针 指向写入的起始位置，每写一个字节，加1，一旦`maxCapacity`相等，则不可写。
- `maxCapacity`
	最大容量 指向最大容量 超过最大容量报错。