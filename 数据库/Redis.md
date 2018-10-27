# Redis

## NoSQL

- 非关系型数据库
- 存储方式 K-V
- 没有通用语言 ，每种nosql都有自己的API和语法



## Redis特性

- 支持数据持久化
- 不仅支持k-v类型的数据，提供多种数据结构的存储
- 支持数据的备份，master-slave模式的数据备份

## Redis优势

- 读写速度快
- 丰富的数据类型
- 原子性
- 支持 publish/subscribe，通知，过期等特性

## 数据操作

- redis：key-value的数据结构，每条数据都是一个键值对
- 键不能重复

键的类型：字符串

值的类型：

- 字符串 string
- 哈希 hash
- 列表 list
- 集合 set
- 有序集合 zset  

## 与python交互

```python
from redis import *
if __name__ == "__main__":
	try:
        # 创建StrictRedis对象，与redis服务器建立连接
        sr = StrictRedis()
    except Exception as e:
        print(e)
```







