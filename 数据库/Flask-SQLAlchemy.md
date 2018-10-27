# Flask-SQLAlchemy

file:///E:/Python%E8%AF%BE%E7%A8%8B/%E9%A1%B9%E7%9B%AE/Flask%E6%A1%86%E6%9E%B6/flasknew/_book/shu-ju-ku/shu-ju-ku-de-ji-ben-cao-zuo.html

**SQLAlchemy:是一个关系数据库框架**

flask-SQLAlchemy:简化了SQLAlchemy操作的flask扩展  



## 安装

pip install flask-sqlalchemy

连接mysql数据库

pip install flask-mysqldb  



## 数据库连接设置

app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://root:mysql@127.0.0.1:3306/test'   # test:数据库名  



## 数据库操作  

插入、修改、删除操作，均由 **数据库会话** 管理

- 会话：**db.session**  , 数据写入数据库前，先将  数据添加到 会话 中，然后调用commit()提交会话  

查询通过query对象操作数据：

- 通过过滤器进行精准查询  



## 在视图函数中定义模型类  

```python
class Role(db.Model):
    # 定义表名
    __tablename__ = 'roles'
    # 定义列对象
    id = db.Column(db.Integer,primary_key=True)
    name = db.Column(db.String(64),unique = True)
    us = db.relationship('User',backref='role')
    # repr() 方法显示一个可读字符串
    def __repr__(self):
        return 'Role:%s'%self.name
    
```

## 模型之前的关联  

### 一对多  

```python
class Role(db.Model):
    #关键代码
    us = db.relationship('User', backref='role',lazy='dynamic')
    ...
     
```

```python
class User(db.Model):
    ...
    role_id = db.Column(db.Integer,db.ForeignKey('roles.id'))
```

- **relationship**： 描述Role和User的关系

- **backref**: 为类User申明新属性的方法  

- **lazy**: 决定什么时候SQLAlchemy从数据库中加载数据 

  -- 设置为子查询方式（subquery） ，在加载完Role对象后，立即加载与其关联的对象。

     --  返回所有数据列表

  -- 设置为动态方式（dynamic），关联对象会在被使用的时候再进行加载，并且在返回前进行过滤。


## 多对多

```python
registrations = db.Table('registrations',  
    db.Column('student_id', db.Integer, db.ForeignKey('students.id')),  
    db.Column('course_id', db.Integer, db.ForeignKey('courses.id'))  
)  
class Course(db.Model):
    ...
class Student(db.Model):
    ...
    courses = db.relationship('Course',secondary=registrations,  
                                    backref='students',  
                                    lazy='dynamic')
```

## 插入数据  

```python
ro1 = Role(name='admin')
db.session.add(role1)
db.session.commit()
```

##  多对多详解

**关键点**：需要添加一张单独的表去记录两张表之间的对应关系 

学生表（Student）

选修课表（Course）

数据关联关系表（Student_Course）

## 数据库迁移

使用数据库迁移框架 ： Flask-Migrate扩展

- 为了导出数据库迁移命令，Flask-Migrate提供了一个MigrateCommand类，可以附加到flask-script的manager对象上。

### 信号机制

**Blinker库**



### 常见关系模板代码

**一对多**

- 示例场景：

  - 用户与其发布的帖子（用户表与帖子表）
  - 角色与所属与该角色的用户（角色表与多用户表）

- 代码：

  ```python
  class Role(db.Model):
      """角色表"""
      __tablename__ = 'roles'
      
      id = db.Column(db.Integer,primary_key = True)
      name = db.Colum(db.String(64),unique=True)
      users = db.relationship('User',backref='role',lazy='dynamic')
      
  class User(db.Model):
      """用户表"""
      __tablename__ = 'users'
      id = db.Column(db.Integer,primary_key = True)
      name = db.Column(db.String(64),unique = True, index = True)
      
  ```


**多对多**

**自关联一对多**

- 评论与该评论的自评论（评论表）

代码：

```python
class Comment(db.Model):
    __tablename__ = "comments"
    id = db.Column(db.Integer,primary_key = True)
    # 评论内容  
    content = db.Column(db.Text,nullable=False)
    # 父评论id
    parent_id = db.Column(db.Integer,db,ForeignKey("comments.id"))
    # 父评论
    parent = db.relationship("Comment",remote_side=[id],
                            backref = db.backref("childs",lazy='dynamic'))
    
```

**自关联多对多**

- 用户关注其他用户（用户表，中间表）

代码：

```python
tb_user_follows = db.Table(
    "tb_user_follows",
    db.Column('follower_id', db.Integer, db.ForeignKey('info_user.id'), primary_key=True),  # 粉丝id
    db.Column('followed_id', db.Integer, db.ForeignKey('info_user.id'), primary_key=True)  # 被关注人的id
)

class User(db.Model):
    """用户表"""
    __tablename__ = "info_user"

    id = db.Column(db.Integer, primary_key=True)  
    name = db.Column(db.String(32), unique=True, nullable=False)

    # 用户所有的粉丝，添加了反向引用followed，代表用户都关注了哪些人
    followers = db.relationship('User',
                                secondary=tb_user_follows,
                                primaryjoin=id == tb_user_follows.c.followed_id,
                                secondaryjoin=id == tb_user_follows.c.follower_id,
                                backref=db.backref('followed', lazy='dynamic'),
                                lazy='dynamic')
```

