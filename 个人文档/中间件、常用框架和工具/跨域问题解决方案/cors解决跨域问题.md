### 什么是跨域问题
在前后端分离的背景下，我想大部分人都有过跨域问题，那我们先来了解一下什么是跨域问题。<br>
当一个资源从与该资源本身所在的服务器不同的域、协议或端口请求一个资源时，资源会发起一个跨域HTTP请求。<br>
例子：当游览器从A域名的网页，去请求B域名的资源时，域名、端口、协议任一不同，都是跨域。<br>
```javascript
    $.ajax({          
           	 url:"http://d.com", //发送请求（提交或读取数据）的地址
             dataType:"预期服务器返回数据的类型",  
             type:"请求方式", 
             async:"true/false",
             data:{发送到/读取后台（服务器）的数据},
             success:function(data){请求成功时执行},      
             error:function(){请求失败时执行}
    });
```
当前端本地去请求url的地址时，就会产生跨域问题。
<br>
![报错图]()

### 解决跨域问题的方法
1. jsonp格式
2. nignx代理
3. cors
4. 其他

### CORS
CORS 是一个W3C标准,全称是"跨域资源共享"（Cross-origin resource sharing），他允许浏览器向跨源服务器发送XMLHttpRequest请求，从而克服啦 AJAX 只能同源使用的限制。<br>
CORS是一种一种机制，它使用额外的HTTP头来告诉游览器。

#### CORS如何解决跨域问题
CORS是Cross Origin Resource Share（跨域资源共享）<br>
CORS需要游览器和服务器同时支持，所有游览器都支持该功能。游览器发现ajax请求跨域，会自动添加头信息。

#### CORS的使用情况
- 客户端向服务端请求资源（前后端分离情况）
- Web字体（CSS中通过`@font-face`使用跨域字体资源）
- 不同域下的前端页面通信而跨域
- `WebGL`贴图
- 使用 `drawImage` 将 Images/video 画面绘制到 canvas
> 后面两个我也不清楚

#### CORS功能概述
CORS会使用一组新的HTTP首部字段来告诉游览器，是否可以跨域请求。<br>
CORS的请求头
请求头|说明
--|--
`Origin`|该请求头在跨域请求或预先请求中，标明发起跨域请求的源域名
`Access-Control-Request-Method`|该请求头用于表明跨域请求使用的实际HTTP方法
`Access-Control-Request-Headers`|该请求头用于在预先请求时，告知服务器要发起的跨域请求中会携带的请求头信息
`with-credentials`|该请求头表明跨域携带cookie

CORS响应头
响应头|说明
--|--
`Access-Control-Allow-Origin`|该响应头中携带了服务端验证后允许的跨域请求域名，可以时一个具体的域名或是一个*（任意域名）
`Access-Control-Expose-Headers`|该响应头用于允许返回给跨域请求的响应头列表，在列表中的响应头内容，才可以被游览器访问
`Access-Control-Max-Age`|该响应头用于告知游览器可以将预先检查请求返回结果缓存的时间，在缓存有效期间内，游览器会使用缓存的预先检查结果判断是否发送跨域请求
`Access-Control-Allow-Methods`|该请求头用于告诉游览器可以支持的请求方法，可以是一个具体的方法列表或是一个*（任意方法）

#### 如何使用CORS
- 客户端需要按规范设置请求头
- 服务端按规范识别并返回响应头。

服务端例子<br>
SpringBoot2.X框架
```java
@Configuration
public class CorsConfig  implements Filter {
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        HttpServletResponse response = (HttpServletResponse) servletResponse;
        response.setHeader("Access-Control-Allow-Origin","http://localhost:8080");
        response.setHeader("Access-Control-Allow-Methods","GET, POST, PUT, DELETE, PATCH, OPTIONS");
        response.setHeader("Access-Control-Max-Age","3600");
        response.setHeader("Access-Control-Allow-Headers","Content-Type");
        response.setHeader("Access-Control-Allow-Credentials","true");
    }
}
```

> [彻底弄懂跨域问题](https://segmentfault.com/a/1190000017867312?utm_source=tag-newest)
>
> [跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)
>
> [HTTP访问控制（CORS）](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS)