## Django 开发模式与流程



Python web 五大框架: Django, Pylons, Tornado, Bottle,Flask



Django相较于其他WEB框架的**优势**：大而全，框架本身集成了ORM,模型绑定，模板引擎，缓存，Session等。



**一.Django的MTV开发模式**

​    M（Models）负责业务对象和数据库的关系映射

​    T（Template）负责如何把页面展示给用户

​    V（Views）负责业务逻辑 并在适当的时候调用Model 和 Template

​    除了以上外，还需要一个URL分发器，将每个URL的页面请求分发给views处理

​    

​    在一般的MVC模式中：

​        M（Models）应用程序的业务逻辑和业务数据

​        V（Views）封装了应用程序的输出形式，也就是页面

​        C（Controller）协调模型和视图，根据用户请求来选择要调用哪个模型来处理业务

两者对应关系：

​    MTV            MVC 

​    M--------->M    数据库相关

​    T----------->V   页面相关

​    V----------->C   视图控制



**二.Django主要模块及功能**

1.settings: 配置信息

2.urls:路由分发功能

3.views:视图函数处理

4.admin:关于数据库的后台管理工具

5.models:数据库表定义的ORM（对象关系映射）



**三.Django的生命周期**

1.当用户在浏览器中输入url时，浏览器会生成请求头和请求体发送给服务端，请求头和请求体中

会包含浏览器的动作(action),这个动作通常为get或post,体现在url中。

2.url经过Django中的wsgi,再经过Django的中间件，最后url到路由映射表，在路由中进行匹配

一旦匹配成功后，就执行对应的视图函数，后面的路由就不再继续匹配。

3.视图函数根据客户端的请求查询相应的数据，返回给Django，然后Django把客户端想要的数据

作为一个字符串返回给客户端。

4.客户端浏览器接收到返回的数据，经过渲染后显示给用户。