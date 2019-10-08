# AJAX 和 FETCH 的原理和区别


## AJAX（Asynchronous  JavaScript And XML）
> _AJAX和FETCH不是两个并行的概念，因此应该把::XMLHttpRequest(XHR)::和::Fetch::进行对比。_  
> AJAX是一种开发技术和设计模式，AJAX的含义是使用实时数据更新界面，而无需刷新整个页面，它使用了浏览器提供的::XMLHttpRequest::API。  

## XHR (XMLHttpRequest)
XHR是::事件驱动::的，你需要绑定一些监听器来获取数据。

### 只读属性：
* XHR.readyState: 
0: UNSENT;  代理被创建，但尚未调用 open() 方法。
1: OPENED; open() 方法已经被调用。
2: HEADERS_RECEIVED; send() 方法已经被调用，并且头部和状态已经可获得。
 3: LOADING; 下载中； responseText 属性已经包含部分数据。
4: DONE;下载操作已完成。
https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/readyState
* XHR.response: 相应数据，类型取决于::XHR.responseType::
* XHR.responseText: 纯文本格式的响应数据
* XHR.status: 响应状态，标准的::HTTP状态码::
* XHR.statusText: 服务器返回的状态文本，如”OK”,”Not Found”
* XHR.responseURL:
* XHR.responseXML:

### 修改器属性：
* XHR.responseType:
指定响应数据的类型
	1. “json”: JavaScript 对象
	2. “text”: 纯文本
	3. “” : 等同于”text”
	4. “arraybuffer”: JavaScript ArrayBuffer
	5. “document”: Blob 对象
* XHR.timeout: 表示该请求的::最大请求时间::（毫秒）
* XHR.withCredentials: 
Boolean类型，用来指定跨域 Access-Control 请求是否应带有授权信息，如 cookie、header。
若 withCredentials = false，跨域请求domain2的资源，无法携带domain2的cookie/header。
若 withCredentials = true，跨域请求domain2的资源，可以携带domain2的cookie/header。

### 方法
* XHR.open(method, url, async, user, password): 初始化一个请求
* XHR.send(): 发送请求
* XHR.abort(): 如果请求已被发送，::立刻中止请求:: （readyState置为0）
* XHR.getResponseHeader(name): 返回指定响应头的字符串

### 事件
* XHR.abort / XHR.onabort
* XHR.error / XHR.onerror
* XHR.load / XHR.onload
* XHR.loadstart / XHR.onloadstart
* XHR.loadend / XHR.onloadend
* XHR.progress / XHR.onprogress
* XHR.timeout / XHR.ontimeout

## Fetch
Fetch是最新的API，它::基于Promise::，Promise是现在JavaScript执行异步操作的首选方式。
Fetch提供了单个逻辑位置来定义其他HTTP相关概念，例如CORS和HTTP的扩展。
Fetch接收到一个代表错误的HTTP状态码时，Promise也会被resolve，::仅当网络故障时，才标记为reject::。
- - - -

## XHR 和 Fetch 的相同点
1. 都是浏览器提供的API
2. 作用都是为了异步获取网络资源

## XHR 和 Fetch的不同点
1. XHR是事件驱动的，使用时需要绑定监听器。
2. XHR可以通过timeout设置超时时间，Fetch没有类似方法。
3. XHR可以通过abort()中止请求，Fetch没有类似方法，需要使用AbortController（仍处于实验阶段）。
4. Fetch是基于Promise的，是XHR的较好替代方法。

- - - -
## Fetch实现Timeout
[Fetch实现timeout](http://jsrun.pro/h4bKp/edit)
存在的缺点：在超时后，fetch请求不会被取消。解决方案需要使用AbortController，但是AbortController任然处于实验阶段。