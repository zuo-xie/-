### Docker简介
Docker是一个开源的应用的容器引擎；是一个轻量级容器技术。
Docker支持将软件编译成一个镜像；然后在镜像中各种软件做好配置，将镜像发布出去，其他使用者可以直接使用这个镜像。
运行中的这个镜像称为容器，容器启动是非常快捷。

### Docker核心概念
- Docker主机（Host）：安装了Docker程序的机器（Docker直接安装在操作系统上）。
- Docker客户端（Client）：连接Docker主机进行操作。
- DOcker仓库（Registry）：用来保存各种打包好的软件镜像。
- Docker守护进程（daemon）：一般在宿主主机后台运行，等待接收来做客户端d的消息。
- Docker镜像（Images）:软件打包好的镜像；放在Docker仓库中。
- Docker容器（Container）：镜像启动后的实例称为一个容器；容器是独立运行的一个或一组应用。

![Docker核心概念图]()

### Docker安装步骤
1. Docker要求CentOS系统的内核版本必须是高于3.10。通过`uname -r`命令来查看当前内核版本。
```
uname -r
```
2. 使用==root==权限登录 CentOS。确保yum包更新到最新。
```
sudo yum update
```
3. 卸载旧版本（如果安装过旧版本的话）。
```
sudo yum remove docker docker-common docker-selinux docker-engine
```
4. 安装需要的软件包，yum-util提供yum-config-manager功能，另外两个是devicemapper驱动依赖的。
```
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```
5. 设置yum源。
```
//这是国外的
sudo yum-config-manager --add-repp https://download.docker.com/linux/centos/docker-ce.repo
//这是阿里的
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.pro
```
6. 查看Docker版本并下载
```
//这是查看
yum list docker-ce --showduplicates | sort -r

//这是下载
sudo yum install docker-ce
```
中途出现Bug
![DockerBug01]()
解决方法：
    1. 将`/etc/yum.repos.d`中关于Docker相关的==repo==全部删除。
    2. 重新添加镜像（步骤5设置yum源）
    
> [附上Bug解决方式链接](https://blog.csdn.net/qq_18948359/article/details/102715729)


7. 检查是否安装成功
```
//检查版本号
docker version
```

8. 启动Docker
```
sudo systemctl start docker
```

9. 后台启动Docker
```
sudo systemctl enable docker
```

10. 退出DOcker
```
sudo systemctl stop docker
```
### Docker命令

命令语句 | 意义 | 语法
---|---|---
`docker search [OPTIONS] TERM`|列出Docker仓库镜像
`docker pull [OPTIONS] NAME[:TAG|@DIGEST]`|从Docker仓库拉取镜像
`docker images [OPTIONS] [REPOSITORY[:TAG]]`|查看本地仓库的docker镜像
`docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`|创建一个容器并启动
`docker ps [OPTIONS]`|列出容器

> 根据后期使用在添加。
> [菜鸟教程的Docker命令](https://www.runoob.com/docker/docker-command-manual.html)