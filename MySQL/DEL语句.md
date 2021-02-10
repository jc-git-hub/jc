# DEL语句

> 数据库控制语句

* 授权
* 删除权限

### grant

``` mysql
grant 权限 on 库.表 to '用户'@'主机' identified by '密码' with grant option;

权限: select insert update delete *  #*代表所有的权限
库: *所有的库  指定的库名
表: *所有的表 指定的表名
主机: ip地址  % 任何地址

用户不存在  新建用户  存在的话就是授权
注意: 操作之前一定要先 use mysql;
	flush privileges;
```

### revork

```mysql
use mysql;
revoke 权限 on 库.表 from '用户'@'主机';
flush privileges;

mysql> revoke insert on myfirst_database.users from 'shiyang'@'%';
```



### MySQL 忘记密码

```
修改my.ini
复制到别的地方 改完替换
[mysql]
skip-grant-tables
保存 替换

net stop mysql57
net start myswl57

mysql -u root -p
无需输入密码

mysql> update mysql.user set authentication_string=password('你的密码') where user='root';
mysql> flush privileges;
mysql> exit

net stop mysql57
net start myswl57
```



# 更新语句

> update 表1,表2 set 字段1=值1,...,字段n=值n where 条件

```mysql
mysql> update stars set username='小岳岳' where id=3; #修改一个字段
mysql> update stars set username='小岳岳',balance=123.456,province='中原' where id=3;
```

### 两个表同时更新

> update 表1,表2 set 字段1=值1,...,字段n=值n where 条件

```mysql
mysql> update user u,order_goods o set u.tel=u.tel+o.buytime where u.uid=o.uid;
Query OK, 4 rows affected (0.02 sec)
Rows matched: 4  Changed: 4  Warnings: 0

mysql> update user u,order_goods o set u.tel=u.tel-o.buytime,o.buytime=123 where u.uid=o.uid;
Query OK, 8 rows affected (0.00 sec)
Rows matched: 8  Changed: 8  Warnings: 0
```



## 索引

```
# 索引
# 为了提升数据查询的效率 缩小查询的范围 类似书的目录
```

* 普通索引 任何字段都可以添加的索引没有任何限制
* 唯一索引  要求这个字段对应的数据行  每个数据都是唯一的  不能有重复值  年龄性别这样的字段不能创建唯一索引
* 主键索引 特殊的唯一索引  不能有空值 不能有重复值
* 全文索引  需要全局搜素的数据 NLP
* 复合索引   给多个字段同时添加索引

```mysql
? index 

create index   不能创建主键索引   
alter table  

1.普通索引   
alter table 表名 add index 名称(字段);
show index from 表名\G  #列出该表所有的索引   
mysql> alter table 表名 drop index 索引名称;  #删除索引
create index 索引名 on 表名(字段); #创建索引
mysql> drop index in_name on user;  #删除索引
2.唯一索引    unique  
mysql> alter table test66 add unique un_name(tel);
show index from 表名\G  #列出该表所有的索引  
alter table 表名 drop index 索引名称; 

3.主键索引 
创建表的时候 我们一般设置主键 
create table 表名(
	id int(11) unsigned not null primary key auto_increment,
);
删除主键索引 先要把主键自增给他消除
alter table 表名 modify id int(11) unsigned not null;#消除主键自增
alter table 表名 drop primary key; #删除主键索引 
 
alter table 表名 add primary key(id);#添加主键索引 
alter table 表名 modify id int(11) unsigned not null auto_increment; #让主键自增 

4.全文索引  
mysql> ALTER  TABLE stars add fulltext f_name(username);
show index from 表名\G  
alter table 表名 drop index 索引名称; 

https://www.iteye.com/blog/sg552-1560834

5.复合索引  
mysql> alter table stars add index in_name(username,balance); #多个字段同时添加索引 
Query OK, 9 rows affected (0.04 sec)
Records: 9  Duplicates: 0  Warnings: 0


索引是占空间的  并不是越多越好 
```

### 什么时候 添加索引

* where group by、order by 条件常用的字段

# 内置函数

1. 字符串

   1. concat()拼接字符串
   2. lcase()转成小写
   3. ucase()转成大写
   4. length()字符串长度
   5. ltrim() 去除左侧的空格
   6. rtrim() 去除右侧的空格
   7. repeat() 重复
   8. replace()替换
   9. substring(字符串,偏移量,截取的个数) 切片
   10. space() 空格

2. 数学

   1. bin() # 10进制转2进制
   2. ceiling() # 向上取整
   3. floor() #向下取整
   4. max()
   5. min()
   6. sqrt()开平方跟
   7. rand()   产生0-1的随机数

3. 日期

   ```
   now() #当前的日期加时间 
   year(date) # date日期坐在的年份
   month(date) # date日期坐在的月份
   week(date) # date日期坐在的第几周 
   unix_timestamp(date) #日期所在的时间戳
   from_unixtime(时间戳) #时间戳转日期
   mysql> select datediff('1998-10-20','2015-7-23');  #日期差额
   ```
