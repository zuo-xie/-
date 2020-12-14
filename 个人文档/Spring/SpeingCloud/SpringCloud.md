### SpringCloud
#### 概述
微服务架构是一种架构模式，它提倡将单一应用程序划分为一组小的服务，服务之间互相协调、互相配合，为用户提供最终价值。每个服务运行在其独立的进程中，服务与服务采用轻量级的通信机制互相协作。每个服务都围绕着具体业务进行构建，并且能够被独立的部署到生产环境、类生产环境等。

### SpringCloud组件

```
graph LR

服务调用-->Ribbon
服务调用-->LoadBalancer
服务调用-->Feign
服务调用-->OpenFeign
服务降级-->Hystrix
服务降级-->resilience4j
服务降级-->sentienl
服务注册中心-->Eureka
服务注册中心-->Zookeepr
服务注册中心-->Consul
服务注册中心-->Nacos
服务网关-->Zuul
服务网关-->gateway
服务配置-->Nacos
服务配置-->Config
服务总线-->Nacos
服务总线-->Bus
```
