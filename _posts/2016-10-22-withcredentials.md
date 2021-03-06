
---

layout: post
category: js
title: withCredentials

---

## withCredentials

了解withCredentials之前，需要先了解同源策略和CORS(Cross-Origin Resource Sharing)。

### 1.同源策略

什么是同源策略，哪些情况属于跨站请求？

出于安全考虑，浏览器会拦截跨站请求的返回结果，并报错。

先看下在`http://a.com/a.js`文件中访问以下资源的情况：
 

| URL | 访问是否受限 |  原因 |
| ------------ | ------------- | ------------ |
| http://a.com/b.js | 不受限制  | 同域名不同文件 |
| https://a.com/b.js | 不允许访问  | 同域名不同协议 |
| http://a.com:8080/b.js | 不允许访问  | 同域名不同端口 |
| http://sub.a.com/b.js | 不允许访问  | 子域名不同 |
| http://b.com/b.js | 不允许访问  | 不同域名 |

**只有同一域名，相同端口，相同协议的资源可以互相访问，否则都属于跨域。**

### 2.CORS

不同域名之间要进行数据操作怎么办？

跨域的办法有多种，这里主要介绍CORS。

CORS是W3C的Web应用工作组推荐的一种机制，让Web应用服务器能支持跨站访问。要让`XMLHttpRequest`在浏览器中发起跨域请求，浏览器必须支持CORS带来的新组件，包括请求头和执行策略。

CORS通过新增一些列HTTP头，让服务器能声明哪些来源能通过浏览器访问该服务器的资源。除GET请求以外的HTTP方法，会对服务器数据造成破坏性影响，CORS标准强烈要求浏览器必须先以OPTIONS请求发送一个预请求，确认服务器对跨域请求所支持的HTTP方法，然后再发送真正的请求。服务器也可以通知客户端，是否需要在请求中附带凭证信息（Cookies和HTTP认证相关数据）。


浏览器对于跨站XMLHttpRequest请求不会发送凭证信息，那么问题来了，如果需要在请求中携带cookie怎么办？

这需要浏览器和服务器配合完成。。。

* 1.发送 XMLHttpRequest请求前将`withCredentials`设置为true,使cookie可以随请求发送

`

	var xhr = new XMLHttpRequest();

	xhr.open('POST',url,true);
	
	xhr.withCredentials = true;

`


* 2.服务器相应头中加`Access-Control-Allow-Credentials:true`

* 3.服务器响应头中加`Access-Control-Allow-Origin:http://a.com`



注： 

1.响应带`withCredentials`的请求时，服务器必须指定允许请求的域名，不能使用`*`,否则响应会失败。

2.`withCredentials`需要在`open()`之后设置，否则部分安卓浏览器不能设置成功而且会报错。

zepto的V1版本在`open()`之前设置`withCredentails`，导致报错，成功踩坑。。。

`

	//zepto源码，在xhrFields传withCredentials参数,通过xhr[name] = settings.xhrFields[name]赋值报错
	if (settings.xhrFields) for (name in settings.xhrFields) xhr[name] = settings.xhrFields[name]

	var async = 'async' in settings ? settings.async : true
	
  	xhr.open(settings.type, settings.url, async, settings.username, settings.password)

  `









