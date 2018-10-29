# JWT

### 基于session的认证

- 增大服务器的开销
- 扩展性弱
- CSRF攻击

### 基于token的认证

**流程**：

- 用户使用账号密码请求服务器
- 服务器验证用户的信息
- 服务器通过验证发送给用户一个token
- 客户端存储token,并在每次请求时附带上这个token值
- 服务器验证token值，并返回数据

token保存在请求头

### JWT	构成

- 头部（header)
- 载荷（payload）
- 签证（signature）

### header

两部分构成：

- 声明类型
- 声明加密的算法

例如：

{

​	'typ':'JWT',

​	'alg':'HS256'

}

### payload

包含三部分：

- 标准中注册的声明
- 公共的声明
- 私有的声明

例如：

{

​	"sub": "123456789",

​	"name": "John",

​	"admin": true

}

### signature

三部分组成：

- header(base64后的)
- payload(base64后的)
- secret

### 如何应用

一般是在请求头里加入`Authorization`，并加上`Bearer`标注：

```python
fetch('api/user/1', {
  headers: {
    'Authorization': 'Bearer ' + token
  }
})
```



### 总结

- JWT跨语言支持
- 便于传输
- 易于扩展
- 可以在自身存储一些非敏感信息



## Django REST framework JWT

手动签发JWT

修改CreateUserSerializer序列化器，在create方法中增加手动创建token的方法  

将JWT保存在浏览器本地

浏览器提供了sessionStorage和localStorage:

- sessionStorage 浏览器关闭即失效
- localStorage长期有效

前端保存token

