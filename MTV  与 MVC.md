# MTV  与 MVC

## MTV

1.用户点击注册按钮，提交信息给服务器

2.View视图接收到注册信息，告诉Model保存信息

3.Model将注册信息保存到数据库

4.数据库返回保存结果给Model

5.Model将保存结果给View

6.View告诉Template产生一个html页面

7.Template将产生的html给View

8.View将html页面给浏览器

9.浏览器显示页面内容

### 

**M：Model , 和数据库进行交互**

**V： View , 接收请求，进行处理，与M和T进行交互，返回应答**

**T： Template , 模板 ， 产生HTML页面**



## MTV           MVC

M                                   M

V                                     C

T                                     V