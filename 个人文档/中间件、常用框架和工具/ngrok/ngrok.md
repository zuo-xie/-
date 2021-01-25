### ngrok
#### 内网穿透
在使用ngrok之前，我们应该先去了解内网穿透是什么。
内网穿透即是`NAT`穿透，是指计算机在内网内使用私有IP地址，在连接外网时使用全局IP地址的技术。
#### ngrok是什么
ngrok是应该方向代理，通过公共的端点和本地运行的web服务器之间建立起一个公开的安全通道。ngrok可捕获和分析所有通道上的流量，便于后期分析和重放。
ngrok是由Go语言编写的。
ngrok目前存放在Github上，供开源使用
#### ngrok的作用
ngrok可以方便的在远端进行后端调试，此外ngrok还提供了一个web端程序来监控通信报文信息，另外Ngork也支持TCP端口映射。
#### ngrok的搭建
ngrok的搭建是十分简单的，如果不愿意搭建，国内外也有许多服务提供商提供服务。
搭建ngrok首先需要准备
1. 拥有外网IP的服务器
2. 域名

- 下载Git和下载GO<br/>
搭建ngrok，我们首先需要将服务器配置Git以及Go环境
`yum install git golang`
- 下载ngrok源码，也可以手动上传<br>
ngrok源码已固定，下载最新代码即可。
`git clone https://github.com/inconshreveable/ngrok.git /usr/local/ngrok`
- 切换到ngrok目录并生成对应的证书
```c
cd ngrok

```
