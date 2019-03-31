### shell 查以_data结尾的文件

```python
find ./  -type -f -name "*._data" 
```

### 执行shell脚本

```python
1.
cd demo
chmod +x ./test.sh
./test.sh

2.
source test.sh

```

### shell 按时间和文件大小排序

```python
ll -rt # 时间
ll -Sl  #大小
```



### python的垃圾回收机制

```python
# 引用计数机制为主，标记清除和分代收集机制为辅

1.引用计数机制
优点：
	- 简单
	- 实时性： 一旦没有引用， 内存就直接释放了
缺点：
	- 维护引用计数消耗资源
	- 循环引用


```

### python中参数是引用传递，还是值传递

```python
Python 中一切皆为对象，数字是对象，列表是对象，函数也是对象，任何东西都是对象。而变量是对象的一个引用（又称为名字或者标签），对象的操作都是通过引用来完成的。
Python 函数中，参数的传递本质上是一种赋值操作，而赋值操作是一种名字到对象的绑定过程
```

### python 字符串去空格

```python
1.strip()  # 取出字符串开头或结尾的空格
2.replace() # 字符串的替换
	a.replace(" ","")
3.join()+split()
	a = "a b c"
	"".join(a.split())

```

### 装饰器

```python
def deco(func):
    def wrapper(*args, **kw):
        print("%s is running" % __func__.name)
        return func(*args)
    return wrapper
```

### 二分查找

```python
def bin_search(array, target):
    low = 0
    high = len(array-1)
    while low <= high:
        mid = (low + high)//2
        if array[mid] == target:
            return mid
        elif array[mid] > target:
            high = mid -1
        else:
            low = mid +1
     return -1

```

### yield

```python
带yield的函数在Python中被称之为generator（生成器）

# 斐波那契数列
def fib(max):
    n, a, b = 0,0,1
    while n<max:
        yield b
        a,b = b, a+b
        n = n+1
一个带有 yield 的函数就是一个 generator，它和普通函数不同，生成一个 generator 看起来像函数调用，但不会执行任何函数代码，直到对其调用 next()（在 for 循环中会自动调用 next()）才开始执行。虽然执行流程仍按函数的流程执行，但每执行到一个 yield 语句就会中断，并返回一个迭代值，下次执行时从 yield 的下一个语句继续执行。看起来就好像一个函数在正常执行的过程中被 yield 中断了数次，每次中断都会通过 yield 返回当前的迭代值。
# 文件读取
def read_file(fpath): 
   BLOCK_SIZE = 1024 
   with open(fpath, 'rb') as f: 
       while True: 
           block = f.read(BLOCK_SIZE) 
           if block: 
               yield block 
           else: 
               return
```

### Django生命周期

```python
1.用户在浏览器中输入URL，浏览器会生成请求头和请求体发送给服务器，
请求头或请求体中包含请求的动作。
2.url经过Django中的wsgi——中间件——路由映射表，在路由中进行匹配，
匹配成功后，执行对应的视图函数
3.视图函数根据客户端的请求查询相应的数据，返回给Django,然后Django把客户端想要的数据作为一个字符串返回给客户端
4.客户端接收到数据，经过模板 渲染后显示给用户
```

### 消息对列

```python
1.为什么要使用消息队列？
	解耦 异步 高并发
    
2.消息队列的选用
	- RabbitMQ 
    基于erlang开发，所以并发能力很强，性能极其好，延时很低;管理界面较丰富；	
    - ActiveMQ  版本更新慢
    -Kafka  大型互联网公司
    
3.RabbitMQ防止消息丢失
	- 消息确认机制：当消息处理完成后，给服务端发送一个确认消息，来告诉服务端可以删除该消息了。如果连接断开的时候，Server端没有收到消费者发出的确认信息，则会把消息转发给其他保持在线的消费者
    
4.消息的持久化
	声明队列时设置一个参数即可
    boolean durable = True
    
    

```

### http Header 包含哪些字段

```python
General   
Response Headers   
Request Headers

- Host  请求的web服务器域名地址
- User-Agent HTTP客户端运行的浏览器的详细信息
- Accept 指定客户端能够接收的内容类型
- Accept-Language 指定HTTP客户端浏览器用来展示返回信息所优先选择的语言
- Content-Type 显示HTTP请求提交的内容类型
- keep-alive 长连接
- cookie
- status code
```

### 元类