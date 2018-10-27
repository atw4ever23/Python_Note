HTTP（Hyper Text Transfer Protocol） 超文本传输协议

- 基于TCP/IP协议传递数据
- 属于应用层的面向对象的协议
- 工作于客户端-服务器端架构之上

默认端口：80 ，  HTTPS 端口：443

### 特点

- 简单快速：客户向服务器请求服务时，只需传送请求方法和路径
- 灵活：HTTP允许传输任意类型的数据对象
- 无连接： 限制每次连接只处理一个请求，服务器处理完请求，收到应答后，断开连接
- 无状态： 对事物处理没有记忆能力
- 支持B/S  C/S 模式

### URL

HTTP使用URI（Uniform Resource Identifiers）传输数据和建立连接。

URL是一种特殊类型的URI，包含了用于查找某个资源的足够信息

URL（Uniform Resource Locator）组成部分：

- 协议部分
- 域名部分
- 端口部分
- 虚拟目录部分
- 文件名部分
- 锚部分
- 参数部分

### 请求消息Request

客户端发送一个HTTP请求到服务器的请求消息包括以下格式：

- 请求行
- 请求头
- 空行
- 请求数据

**请求行 ：**用来说明请求类型，要访问的资源以及所使用的HTTP版本

**请求头：**说明服务器要使用的附加消息。主要包括：Accept、Age、Cache-Control、Connection、

​		Content-Type、Host、User-Agent

**空行：**请求头后面的空行，必须有

**请求数据：**主体，可以添加任意的其他数据



### 响应消息 Response

服务器接受并处理客户端发送过来的消息后会返回一个HTTP的响应消息

四部分组成：

- 状态行
- 消息报头
- 空行
- 响应正文

### 状态码

- 1xx :指示信息--表示请求已接收，继续处理
- 2xx : 成功-- 表示请求已被成功接收
- 3xx : 重定向
- 4xx : 客户端错误
- 5xx : 服务器端错误

常见状态码：

```
200 OK                        //客户端请求成功
400 Bad Request               //客户端请求有语法错误，不能被服务器所理解
401 Unauthorized              //请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用 
403 Forbidden                 //服务器收到请求，但是拒绝提供服务
404 Not Found                 //请求资源不存在，eg：输入了错误的URL
500 Internal Server Error     //服务器发生不可预期的错误
503 Server Unavailable        //服务器当前不能处理客户端的请求，一段时间后可能恢复正常
```

### HTTP请求方法

- GET
- POST
- HEAD
- PUT
- DELETE
- TRACE
- CONNECT

### HTTP 工作原理

1. 客户端连接到Web服务器
2. 发送HTTP请求
3. 服务器接受请求并返回HTTP响应
4. 释放连接TCP连接
5. 客户端浏览器解析HTML内容


