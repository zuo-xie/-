### 注册中心的作用
注册中心相当于通讯录，他记录了服务和服务地址的映射关系。
当我们在分布式架构中，服务会注册到这里，当服务需要调用其他服务时，会在注册中心去寻找其他服务的地址，进行调用。
### `Dubbo`支持的注册中心
`Dubbo`支持多种注册中心来实现

注册中心|说明
--|--
`zookeeper`|作为`Apache Hadoop`的子项目，是一个树型的目录服务，支持变更推送`Dubbo`推荐使用
`Multicast`|该注册中心不需要启动任何中心节点，只要广播地址是一样的，就可以互相发现
`Nacos`|是`Dubbo`生态系统中重要的注册服务中心实现，其中`dubbo-registry-nacos`则是由`Dubbo`融合`Nacos`注册中心的实现
`Redis`|使用`Redis`的`key/Map`来存储结构<br>     主`Key`为服务名和类型<br>     `Map`中的`Key`用来存储`URL`地址<br>     `Map`中的`Value`用来存储过期时间，用于判断脏数据<br>使用`Redis`的`Publish/Subscribe`事件通知事件的变更<br>     通过事件的值区分事件类型：`register`, `unregister`, `subscribe`, `unsubscribe`<br>     普通消费者直接订阅指定服务提供者的 Key，只会收到指定服务的 `register`, `unregister` 事件<br>      监控中心通过 `psubscribe` 功能订阅 `/dubbo/*`，会收到所有服务的所有变更事件
`Simple`|该注册中心本身就是一个普通的`Dubbo`服务，可以减少第三方依赖，是整体通讯更一致