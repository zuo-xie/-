### RestTemplate
##### RestTemplate介绍
SpringRestTemplate是Spring用来提供访问Rest服务的，通常情况下我们会利用Apache的HttpClint来制作Http请求工具，但是Apache的使用过于繁琐，Spring提供了一种更简单的方式来进行操作。

##### RestTemplate的使用
我们首先来看Api文档<br>
```
Synchronous client to perform HTTP requests, exposing a simple, template method API over underlying HTTP client libraries such as the JDK HttpURLConnection, Apache HttpComponents, and others.
基于JDK和Apache公开的Http客户端库上开发的简单模板Api，同步客户端执行Http请求

The RestTemplate offers templates for common scenarios by HTTP method, in addition to the generalized exchange and execute methods that support of less frequent cases.
除了支持常见的Http方法和通用方法之外，RestTemplate还提供了Http方法的常用模板
```
文档中简单介绍了RestTemplate
