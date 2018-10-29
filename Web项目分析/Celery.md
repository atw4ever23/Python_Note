# Celery

Celery  是一个基于python开发的分布式异步消息任务队列

Celery 在任务执行时需要通过一个消息中间件来接收和发送任务消息，以及存储结果

Celery 优点：

- 高可用：当任务执行失败或连接中断后，会自动尝试重新执行任务
- 快速：一个单进程的celery每分钟可处理上百万个任务  
- 灵活：几乎celery的各个组件都可以被扩展及自定制  



![image_1chbcgmgc1tcreq11hfdc4h1em29.png-399.1kB](http://static.zybuluo.com/jsutqb/v1gsiz87qdjespxi8cuqjxdm/image_1chbcgmgc1tcreq11hfdc4h1em29.png)





主要构成：

- client  任务的发起方
- worker  任务的执行方
- broker 中间人（client和worker的接头人）
- backend  任务执行结果的存储

