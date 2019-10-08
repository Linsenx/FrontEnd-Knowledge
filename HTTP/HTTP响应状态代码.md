# HTTP响应状态代码
> HTTP响应状态代码: HTTP Status Codes  

[HTTP 响应代码 - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status)



## 响应的分类
1. 信息响应（100-199）
2. 成功响应（200-299）
3. 重定向（300-399）
4. 客户端错误（400-499）
5. 服务器错误（500-599）

## 成功响应
### 200 OK
::请求成功::，成功的含义取决于HTTP方法：
* GET：资源已被提取并在消息正文中传输。
* POST：描述动作结果的资源在消息体中传输。
* HEAD：实体标头位于消息正文中。
* TRACE：消息正文包含服务器收到的请求消息
### 201 Created
::请求成功::，并且::创建了一个新的资源::
### 202 Accepted
::请求已经接受::，但尚未处理

## 重定向
### 301 Moved Permanently
被请求资源已经永久性移动到新位置
### 302 Found
请求的资源临时重定向
### 303 See Other
临时性重定向，总是使用GET请求新URI
### 304 Not Modified
自从上次请求后，请求的资源没有修改过

## 客户端错误
### 400 Bad Request
请求格式有误或请求参数有误
### 401 Unauthorized
请求未授权
### 403 Forbidden
禁止访问（不希望客户端获得任何信息）
### 404 Not Found
请求失败，在服务器上找不到任何与URI匹配的资源

## 服务器错误
### 500 Internal Server Error
服务器遇到了错误（最常见的服务器错误）
### 503 Service Unavailable
服务器暂时无法处理请求，可能是因为服务器维护或停机
