```python
#创建一个数据表
create table students(
	id int unsigned primary key auto_increment not null,
	name varchar(20) default '',
	age tinyint unsigned default 0,
	height decimal (5,2),
	gender enum('男','女','中性') default '保密',
	cls_id int unsigned default 0,
	is_delete bit default 0
	);


	create table classes(
			id int unsigned auto_increment primary key not null,
			name varchar(30) not null
			);


insert into students (name,age) values("XXX",9);
insert into students set name = "YYY", age=10;


#查询
select * from students;
select * from classes;
select id, name from classes;


select name, age from students;

select name as n,age as a from students;

select s.name,c.name from students as s, classes as c;

#增删改查(curd)  创建(create)  更新(update) 读取(retrive) 删除(delete)

#增加

#全列插入
insert into students values(0,"郭靖",1,"蒙古","2016-1-2");

#部分列插入
insert into students(name,hometown,birthday) values('黄蓉','桃花岛','2016-1-1');

#全列多行插入
insert into students(name) values('杨康'),('杨过');

#修改
update students set gender=0,hometown='北京' where id = 5;

#删除
delete from students where id = 5;




#消除重复行
select distinct gender from students;

#条件查询

select * from students where age >18;
select * from students where age>18 and gender="女";

select * from students where age >18 or height>=180;

select * from students where not age>18 and gender=2;
select * from students where not (age>18 and gender=2);
select * from students where (not age<=18) and gender=2;


#模糊查询

select name from students where name="小";
select name from students where name like "小%";

select name from students where name like "%小%";
select name from students where name like "__";
select name from students where name like "___";
select name from students where name like "__%";

select name from students where name rlike "^周.*";

select name from students where name rlike "^周.*伦$";


#范围查询

select name, age from students where age=18 or age=34;
select name, age from students where age in (12,18,34);

select name,age from students where age not in (12,18,34);

select name, age from students where age between 18 and 34;

select * from students where age not between 18 and 34;

select * from students where height is null;
select * from students where height is not null;

select * from students where (age between 18 and 34) and gender=1 order by age;
select * from students where (age between 18 and 34) and gender=2 order by height desc;
select * from students where (age between 18 and 34) and gender=2 order by height desc,id desc;


#聚合函数

select count(*) from students where gender=1;
select count(*) as MaleSum from students where gender=1;

select max(height) from students where gender=2;

select sum(age) from students;

select avg(age) from students;

select sum(age)/count(*) from students;

select round(sum(age)/count(*), 2) from students;

#分组

select gender from students group by gender;

select gender count(*) from students group by gender;

select gender, count(*) from students where gender=1 group by gender;

select gender,group_concat(name) from students where gender=1 group by gender;

select gender,group_concat(name),avg(age) from students group by gender having avg(age)>30;

# 分页
select * from students limit 0,5;

#连接查询

select * from students inner join classes on students.cls_id=classes.id;
select * from students as s left join classes as c on s.cls_id=c.id;
select...from xxx as s left join xxx as c on ... where...
select...from xxx as s left join xxx as c on having...

#自关联
select city.* from areas as city
inner join areas as province on city.pid=province.aid
where province.atitle='山西省';

#子查询
select * from students where height = (select max(height) from students);


#数据备份
mysqldump -uroot -p 数据库名 > python.sql;

#恢复
mysql -uroot -p 新数据库名 < python.sql;


#python 操作Mysql
from pymysql import *


def main():
	conn = connect(host='localhost',port=3306,database='jing_dong',user = 'root',
	password = 'mysql',charset='utf8'
	cs1 = conn.cursor()
	
	count = cs1.execute('insert into goods_cates(name) values("硬盘")')
	print(count)
	
	count = cs1.execute('insert into goods_cates(name) values("光盘")')
	
	conn.commit()
	
	cs1.close()
	conn.close()
	
if __name__ == '__main__':
	main()
	
	
	
#参数化
#sql语句的参数化，防止sql注入
#注意：此处不同于python的字符串格式化，全部使用%s 占位

from pymysql import *


def main():
	find_name = input("请输入物品名称:")
	conn = connect(host='localhost',port = 3306,user='root',password='mysql',
	database = 'jing_dong',charset='utf8')
	cs1 = conn.cursor()
	
	params = [find_name]
	count = cs1.execute('select * from goods where name=%s',params)
	
	print(count)
	result = cs1.fetchall()
	print(result)
	cs1.close()
	conn.close()
	
if __name__ == " __main__":
	main()
	
	
#视图

#定义视图
create view 视图名称 as select语句；
#查看视图
show tables;
#使用视图
select * from v_stu_score;
#删除视图
drop view 视图名称；
#视图的作用
1.提高了重用性，就像一个函数
2.对数据库重构，却不影响程序的运行
3.提高了安全性能，可以对不同的用户
4.让数据更加清晰


#事务

#事务四大特性
原子性 一致性 隔离性 持久性
#开启事务
begin; 或者 start transaction;
#提交事务
commit;
#回滚事务
rollback;

#索引

#查看索引
show index from 表名；
#创建索引
create index 索引名称 on 表名(字段名称(长度))
#删除索引
drop index 索引名称 on 表名；

#账户管理

#创建账户
grant 权限列表 on 数据库 to '用户名'@'访问主机' identified by '密码';

#查看用户权限
show grants for laowang@localhost;

#修改密码
update user set authentication_string=password('新密码') where user=
'用户名';

修改完成后需要刷新权限
flush privileges

#删除账户
drop user 'laowang'@'localhost';

flush privileges;






























```

