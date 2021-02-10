### 创建数据库

```mysql
mysql 中 以分号为结尾
启动mysql net start mysql

```

```mysql
create database 数据库名;
```



### 查看数据库

  ```mysql
show databases;    # s 不要忘了
  ```



### 选中数据库

```mysql
use 数据库名;
```

### 查看数据库中有多少数据表

```mysql
show tables;  # s 不要忘了
```

### 删除数据库

```mysql
drop database 数据库名字;
```

### 数据表操作

#### 创建数据表

```mysql
create table user(id int(11),name varchar(50),)default charset=utf8;

create table 表名(字段 类型(长度),字段2 类型(长度),)engine=引擎 default charset=utf8;  # mysql中没有utf-8 只有utf8
engine=引擎 设置mysql 引擎
default charset=utf8 设置字符集

复制表
create table 新表名 like 已经存在的表;

```

#### 查看表结构

```mysql
show tables;
desc 表名;

```

#### 删除表

```
drop table 表名;
```

###  数据字段操作

>alter table 表名

#### 修改表字段类型  modify

```mysql
alter table user modify name int(30);
alter table 表名modify 字段  新类型(新长度);

```

#### 添加字段  add

```mysql
alter table user add column age tinyint; 默认加到最后  column 可加可不加
alter table 表名 add column 新字段名 类型(长度);


```

#### 添加字段的时候控制顺序 first 、after

```mysql
alter table user add password varchar(30) first; # 添加第一位
alter table user add sex 类型(长度) after id; # 指定字段的后面

```

#### 删除字段

```mysql
alter table 表名 drop column 字段名  #column 可加可不加

alter table 表名 drop 字段名; # 也是正确的

```

#### 已经存在的表字段 调整顺序   modify first after

```mysql
alter table user modify id int(11) first; # 将id字段调整到第一位

alter table user modify age tinyint after id;#已经存在的字段调整位置

```

#### 修改表名  rename

```mysql
alter table 旧表名 rename 新表名;
# 例子
alter table user rename users;
```

### 类型 引擎 字符集 索引

#### 数据类型

- 数值类型
  - 整型
  - 浮点型
- 字符串类型
- 日期时间类型
- 复合类型
- 空间类型(科学计算人员专用) 

#### 整型

| 类型      | 字节 | 范围             |
| --------- | ---- | ---------------- |
| tinyint   | 1    | -128~127         |
| smallint  | 2    | -32768~32767     |
| mediumint | 3    | -8388608~8388607 |
| int       | 4    |                  |
| bigint    | 8    |                  |
|           |      |                  |

ps: 如果说 某个字段 不能够出现负数 这个时候 需要添加unsigned 无符号 正数

​		年龄我们一般用 tinyint 来表示 0 男 1 女 2未知   加unsigned

​		日期 2019-11-12 12:10:30   一般是存时间戳 因为 时间戳是整型 节约空间

​	

#### 浮点型

| 类型         | 字节 | 范围                                     |
| ------------ | ---- | ---------------------------------------- |
| float（m,d） | 4    | 单精度m表示总个数d表示小数点位数         |
| double(m,d)  | 8    | 双精度m表示总个数d表示小数点后数         |
| decimal      |      | 定点数   存储为字符串的浮点数            |
|              |      | 银行中对于进度要求非常高，建议使用定点数 |

 

#### 字符串

>定长 char(50)  分配50空间 如果超过50截断 只剩50  不足50空格补齐
>
>变长 varchar(50) 分配50空间如果超过50截断 只剩50 不足50不用空格补齐
>
>blob 类型 区分大小  text 类型不区分大小写
>
>

| 类型       | 字节    | 范围                              |
| ---------- | ------- | --------------------------------- |
| char       | 0-255   | 定长                              |
| varchar    | 0-255   | 变长                              |
| tinyblob   | 0-255   | 二进制形式的字符串  不超过255字节 |
| blob       | 0-65535 | 二进制形式的长文本数据            |
| tinytext   | 0-255   | 短文本                            |
| text       | 0-65535 | 长文本字符串                      |
| mediumblob |         | 二进制形式的中等文本数据          |
| logblob    |         | 二进制形式的极大文本              |
| logtext    |         | 极大文本数据                      |

#### 时间类型

| 类型      | 字节 | 举例                   |
| --------- | ---- | ---------------------- |
| date      | 3    | 2019-11-12             |
| time      | 3    | 11:12:13               |
| datetime  | 8    | 2019-11-12 11:12:13    |
| timestamp | 4    | 自动存储记录修改的时间 |
| year      | 1    | 年份                   |
|           |      |                        |
|           |      |                        |

>mysql 中日期一般存时间戳 如果数据量不大 那么datetime 也可以 方便查看
>
>select unix_timestamp(now()); # 将当前日期时间转成时间戳

#### 复合类型

| 类型 | 说明     | 举例                 |
| ---- | -------- | -------------------- |
| set  | 集合类型 | set("n1","n2","n3")  |
| enum | 枚举类型 | enum("n1","n2","n3") |

>区别：
>
>enum  只允许从集合中 取出一个值
>
>set 允许从集合中  取出任意多个值





#### 总结

```mysql
create table if not exists numbers(
	id int(11) unsigned not null,
	unsename varchar(50) not null,
	content longtext not null,
	create_time datatime not null,
	sex tinyint unsigend not null default 1,
	age tinyint edfatlt 18
)engine=innodb default charset=utf8;

create table if not exists nums(
	id int(11) unsigned not null,
	unsename varchar(50) not null,
	content longtext not null,
	create_time datatime not null,
	sex tinyint unsigend not null default 1,
	age tinyint zerofill
)engine=innodb default charset=utf8;

zerofill # 表示填充0
unsigned # 不能出现负数
default  # 设置默认值
not null # 表示不为空


```

#### 字符集

- ascii  A 65   a 97
- gbk  简体中文  向下兼容 gb2312
- unicode  兼容世界上所有的语言   跨语言 跨平台
- utf-8 unicode 可变长度的字符串编码 1-6字节

#### 工作过程常用的排序规则

| 规则集           | 说明                 |
| ---------------- | -------------------- |
| gbk_chinese_ci   | 简体中文不区分大小写 |
| utf_8gerneral_ci | 多国语言不区分大小写 |

#### 表字段改名  change

```mysql
1. 修改字段类型  modify
2. 添加字段  add first/after
3. 删除字段  drop
4. 表改名  rename
5. 字段改名  change

alter table users change 旧字段 新字段 类型(长度);
```



### 数据类型 排序

最大到最小   字符串类型 -> 时间类型 ->数值类型

>性别 一般存数值类型 
>
>时间可以存时间戳
>
>如果精度要求高 选择decimal 字符串型的浮点数



### 索引

> 比如 新华字典的目录       比如 书的目录  
>
>目的是 快速找到指定的内容
>
>如果不用索引 那需要从头到尾轮询  效率慢  索引就是 先划定一个范围

#### 类型

- 普通索引
- 唯一索引
- 主键索引
- 全文索引
- 复合索引
- 外键索引   (不建议使用太耗费资源)

##### 普通索引  index

>最基本的索引没有任何限制的

```mysql
alter table 表名 add index(字段名);# 创建索引  这个没有指定索引名称 那么跟字段名相同
alter table 表名 add index 索引名称(字段名);
show index from 表名\G # 查看索引
alter table users drop index 索引名字;# 删除索引

? index 
# 发现创建索引有两种方式
# 1, alter table
# 2, create index
# 区别：creat index  不能创建主键索引

create index 索引名称 on 表名(字段名); # create 创建索引

drop index 索引名称 on users; # 删除索引
show index from users\G; 查看索引
```



##### 唯一索引  unique

>要求这一列不能有重复值   比如 年龄 性别

```mysql
alter table 表名 add unique 索引名称(username);
alter table 表名 drop index 索引名称; # 删除索引
auto_increment # 主键自增
```



##### 主键索引  primary key(字段名) auto_increment 主键自增

>每个表一定有个主键   不能有重复值  不能有空值  一般创建表的时候 我们就创建主键索引
>
>主键索引 是特殊的唯一索引

```mysql
auto_increment # 主键自增
alter table users drop index primary key; # 删除主键索引 如果自动递增这一步报错
alter table users modify id int(11) unsigned not null;# 消除自增
alter table users drop primary key; # 消除之后 在执行则成功

# 添加主键索引
alter table users add primary key(Id); # 创建主键索引
alter table users modify id int(11) unsigned not null auto_increment; # 让主键自动递增
```

##### 全文索引  fulltext 索引名称(字段名)

>对文章中 或者 电商 或者社交网站 对需要全局搜索的内容 进行全文索引

```mysql
alter table users add fulltext 索引名称(字段名);
```

##### 复合索引  index 索引名称(字段,字段);

>对多个字段 同时 添加索引
>
>text 类型不能添加  普通索引、复合索引

```mysql
alter table users add index a_test(username,age); 
```

##### 外键

```html
https://www.cnblogs.com/wasayezi/p/7412049.html
```



####  总结  建表的同时添加索引

```mysql
creat table if not exists in_test(
    id int(11) unsigned not null primary key auto_increment,
    username varchar(50) not null,
    password varchar(50) not null,
    content text not null,
    index pw(password),
    unique(username),
    fulltext(content)
)engine=myisam default charset=utf8;
```



## 增删改查

#### 增

```mysql
insert into in_text values(有多少字段 写多少); # 主键不能出现重复值，否则报错

# 只是插入指定字段对应的内容即可  主键自增 默认值  可以不用插入 其他字段不能为空
insert into in_text(字段1，字段2，字段3，字段4) values(内容1，内容2，内容3，内容4)# 添加内容是 不要于表中存在的重复，重复则报错



insert into money(username,password,balance,province,age,sex)
values('laowang','123123','1000000','南京',28,0),(),(),(),().....; # 一次性插入多条记录

```

### 查 select 

```mysql
select * from 表名; # * 代表  所有的字段意思
select 字段1，字段2.。。 from 表名;
select 字段1 as 新字段名,字段2 as 新字段名 from 表名; # as 显示结果的别名
```

#### 删

```mysql
delete from 表名; # 清空表
# 如果表中有自增主键 删除全来的表的内容之后，之后的添加则在删除前的 自增主键后面添加

delete from in_test where 字段=值; # 删除指定的内容
```

#### truncate table  清空表

```mysql
truncate table 表名; # 下次插入数据，id下表就从1开始
```

####  改 update

```mysql
update 表名 set 字段="更改内容" where 字段=值; # 更新指定的内容

```

## 数据库查询 扩展

```mysql
create table if not exists money(
	id int(11) unsigned not null primary key auto_increment,
    username varchar(64) not null,
    password varchar(64) not null, 
    province varchar(16) not null,
    balance float not null,
    age tinyint default 19,
    sex tinyint default 0
)engine=myisam default charset=utf8;

insert into money(username,password,balance,province,age,sex)
values('laowang','123123','1000000','南京',28,0),(),(),(),().....; # 一次性插入多条记录
```

#### distinct 查询单个字段不重复记录

```mysql
select distinct age from money; # 查询money 表年龄唯一的结果
select distinct 字段 from 表名;
```

#### where 条件

```mysql
select * from money where age=18;
select * from 表名 where 字段=值;
# 综合条件
select username as '姓名',balance as '余额',province as '省份' from money where id<10 and province='湖北';
```

| 运算符 | 说明 |
| ------ | ---- |
| >      |      |
| <      |      |
| >=     |      |
| <=     |      |
| !=     |      |
| =      |      |
| or     |      |
| and    |      |
|        |      |

##### 结果集排序   order by

- asc 升序
- desc 降序

```mysql
# 按照余额升序排序
select id,username,balance,province from money order by balance asc;
select 字段1，字段2，字段3，...from 表名 order by 字段 关键词;
# 按照余额降序排序
select id,username,balance,province from money order by balance desc;

# 多个字段排序  如果第一个字段已经将结果排序ok 那么第二个字段将被忽略

select id,username,balance,province from money order by balance desc,age asc;

```

##### 结果集限制  limit

```mysql
select * from money limit 5;

```

##### 限制结果集并排序

```mysql
select id,username,balance,province from money order by balance desc,age asc limit 5;
```

##### 结果集区间选择

```mysql
select 字段 from 表名 limit 偏移量(下标开始),数量(取几条数);


```

##### 统计函数

| 函数    | 作用     |
| ------- | -------- |
| count() | 统计函数 |
| sum()   | 求和     |
| avg()   | 平均数   |
| max()   | 最大值   |
| mix()   | 最小值   |

```mysql
select count(*) from  money; # 统计总数
select sum(字段) from money; # 求和
select avg(字段) from money; # 平均数
select max(字段) from money; # 最大值
select mix(字段) from money; # 最小值

```

#### 分组 group by

```mysql
进入 mysql
select @@sql_mode;
会发现有 ONLY_FULL_GROUP_BY 表名这是按照Oracle的分组规则 也就是说 select 所有的列都要在分组中


修改配置文件

sudo vim/etc/mysql/mysqld.conf.d/mysqld.cnf

[mysqld]
sql_mode=
STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION

service mysql restart

重新登陆mysql
select @@sql_mode;
ONLY_FULL_GROUP_BY 取消了

select * from money group by province; # 相同的省份只显示一个

select count(province) as '人数',province form money group by province;
# 统计省份的数量以后再显示

select count(province) as '人数',province from money group by province with rollup;
# 相比较上面结果 多了同一总数的统计

```

##### 分组的结果过滤一下 having

```mysql
select count(province) as result,province from money group by province having result>1;
# 选择大于1的输出
```

### 总结

```mysql
select 你选择的列 [as '显示的别名']
from 表
where 条件
group by 分组 [having 分组过滤的条件]
order by 字段
limit  偏移量，数量

```

## 多表联合查询

- 内连接  inner join on
- 外连接  
  - 左连接   left join on
  - 右连接   right join on
- 子查询

### 表

```mysql
# 用户表
creat table if not exists users(
    uid int(11) unsingned not null primary key auto_increment,
    username varchar(64) not null,
    password varchar(64) not null,
)engine=innodb  default charset=utf8;

# 订单表
creat table if not exists order_goods(
	oid int(11) unsigned not null primary key auto_increment,
    uid int(11) not null,
    name varchar(64) not null,
    buytime int(11) not null
)engine=innodb default charset=utf8;
```



### 内连接

```mysql
# 第一版写法
select users.uid,users.username as '用户名',order_goods.name as '商品名',order_goods.buytime from users,order_goods where users.uid=order_goods.uid;

# select 表1.字段1,表2.字段2 as '别名',表2.字段1 as '别名',表2.字段2 from 表1,表2 where 表1.字段=表2.字段;
# 给表起别名 在表名后面 空格  # 给字段起别名用as


# 第二版写法
select 表1.字段1 [as 别名],表n.字段 from 表1 inner join 表n on 条件;
# 范例
select users.uid as ID,users.username as '姓名',order_goods.name as '商品名',order_goods.buytime from users inner join order_goods on users.uid=order_goods.uid;
```

### 外连接

```mysql
1. 左连接  select 表1.字段1 [as 别名],表n.字段n from 表1 left join 表n on 条件;
# 注：以左边的表为准
select users.uid as ID,users.username as '姓名',order_goods.name as '商品名',order_goods.buytime from users left join order_goods on users.uid=order_goods.uid;


2. 右连接  select 表1.字段1 [as 别名],表n.字段n from 表1 right join 表n on 条件;

select users.uid as ID,users.username as '姓名',order_goods.name as '商品名',order_goods.buytime from users right join order_goods on users.uid=order_goods.uid;

3. 如果上面左连接为例子 null 可以显示默认值
(case when 表.字段 is null then 默认值 else 表.字段 end) as '别名'

select users.uid,users.username as 用户名,(case when order_goods.name is null then '没买东西' else order_goods.name end) as 商品名 from users left join order_goods on users.uid=order_goods.uid;

4. 如果上面左连接为例子 unll 可以显示默认值
ifnull(表.字段, '默认值')
select users.uid,users.username as 用户名, ifnull(order_goods.name,'默认值') as 商品名 from users left join order_goods on users.uid=order_goods.uid;

```

### 子查询

```mysql
1. 查询购买用户的详细信息

selcet * from users where uid in(2,3,4,5); # 查询购买用户的详细信息 括号中的值是写死的

2. select * from users where uid in(select uid from order_goods);
# 先从一个表中查出记录再 将结果作为条件 从另外表中查询


```

#### union  union all 

```mysql
select uid from users union all select uid from order_goods; # 两表的uid字段所有记录

select uid form users union select uid from order_goods;# 去除重复记录
```

## 视图 *需要常用自带优化*

```mysql
视图是关系型数据库中将⼀一组查询指令构成的结果集组合成可查询的数据表的对
象。简单的说，视图就是虚拟的表，但与数据表不不同的是，数据表是⼀一种实体结
构，⽽而视图是⼀一种虚拟结构，你也可以将视图理理解为保存在数据库中被赋予名字的

SQL语句句。
使⽤用视图可以获得以下好处：
1. 可以将实体数据表隐藏起来，让外部程序⽆无法得知实际的数据结构，让访问者
可以使⽤用表的组成部分⽽而不不是整个表，降低数据库被攻击的⻛风险。
2. 在⼤大多数的情况下视图是只读的（更更新视图的操作通常都有诸多的限制），外
部程序⽆无法直接透过视图修改数据。
3. 重⽤用SQL语句句，将⾼高度复杂的查询包装在视图表中，直接访问该视图即可取出
需要的数据；也可以将视图视为数据表进⾏行行连接查询。
4. 视图可以返回与实体数据表不不同格式的数据

# 需要注意的
既然视图是⼀一张虚拟的表，那么视图的中的数据可以更更新吗？视图的可更更新性要视
具体情况⽽而定，以下类型的视图是不不能更更新的：
1. 使⽤用了了聚合函数（SUM、MIN、MAX、AVG、COUNT等）、DISTINCT、
GROUP BY、HAVING、UNION或者UNION ALL的视图。
2. SELECT中包含了了⼦子查询的视图。
3. FROM⼦子句句中包含了了⼀一个不不能更更新的视图的视图。
4. WHERE⼦子句句的⼦子查询引⽤用了了FROM⼦子句句中的表的视图。
```

###### 举个例子

```mysql
 create view v_student(no,name,sex,age) as select sno,sname,ssex,sage from student;
 show tables; # 发现多了一个v_student
 # 一切基本表现都像基本表,只要不在视图中增删改其他的都不用管,只要基本表的字段不变,基本表字段变了,只需把SQL语句重新写就行了,是虚拟表不保存数据
 # 多个表视图
 create view v_student(sno,sname,sage,sclass,cno,cname,score) as select s.sno,sname,sgae,sclass,c.cno,cname,score from student s join grade g on g.sno=s.sno join coure c on g.cno=c.cno;
```



## DCL 数据库控制语句

>首先选中mysql
>
>每个数据库服务器都有一个mysql数据库
>
>mysql 数据库存放着 权限用户等 重要信息  每个数据库都是不同的

```mysql
# 添加权限
grant all on *.* to root@'%' identified by '123456' with grant option
# grant 权限 on 数据库.数据表 to '用户名'@'主机' indentified by '密码' 

权限：all 所有权限
	select
	insert
	update
	delete
	
数据库：
	  * 所有的数据库
数据表：
	  * 所有的数据表
用户名：
	 用户名如果不是存在的 那么就会新建
主机：
	 % 任意主机
flush privileges; 刷新权限

revoke 权限 on 数据库.数据表 from '用户名'@'主机'; # 移除权限

flush privileges; 刷新权限
```

## 数据库的备份及恢复 

#### 备份 mysql dump

```mysql
# Linux 
mysqldump -u root -p test > /tmp/test.sql

# Windows
mysqldump -u root -p test > d:\test.sql

```

#### 恢复mysql

```mysql
# Linux
mysql -u root -p test < /tmp/test.sql
# Windows
mysql -u root -p test < d:\test.sql
```

## Python 操作Mysql

>Python 不能直接操作Mysql 需要借助第三方工具
>
>Pymysql(开源)

### 安装 Pymysql

```shell
1. pip install pymysql

2. sudu apt-get install git
	git clone https://github.com/PyMySQL/PyMySQL.git
	cd PyMySQL
	Python setup.py install
	
```

### 	Python 操作 Mysql 

- 连接数据库
- 创建游标
- 执行sql 语句
- 获取结果集
- 关闭连接

```python
import pymysql

# 连接数据库
# 主机地址
# 用户名
# 密码
# 数据库名字

#encoding:utf-8
import pymysql

#连接数据库
#主机地址 
#用户名
#密码
#数据库名字


#enconding:utf-8
import pymysql
#第一步
db = pymysql.connect("127.0.0.1",'root','123456','test')

#第二步  
cursor =db.cursor()


#准备sql语句 
sql = 'select * from money order by balance limit 3'

#执行sql语句
cursor.execute(sql)

#获取结果集  
data = cursor.fetchone()
print(data)

#释放句柄对象  
cursor.close()

#关闭mysql 连接 
db.close()
```

#### 创建数据

```python
#enconding:utf-8
import pymysql
#第一步 
db = pymysql.connect("127.0.0.1",'root','123456','test')

#第二步  
cursor =db.cursor()


#准备sql语句 
sql = 'create table if not exists kangbazi(id int(11) unsigned not null primary key auto_increment,username varchar(64) not null)engine=innodb default charset=utf8'

#执行sql语句
cursor.execute(sql)

#释放句柄对象  
cursor.close()

#关闭mysql 连接 
db.close()
```

#### 插入数据

````python
#enconding:utf-8
import pymysql
#第一步 
db = pymysql.connect("127.0.0.1",'root','123456','test')

#第二步  
cursor =db.cursor()


#准备sql语句 
sql = 'insert into xiaoxixi(username) values("xiaoxixi1"),("xiaoxixi2")'
try:
	#执行sql语句
	cursor.execute(sql)
    db.commit()
except:
    db.rollback() # 只有innodb引擎才支持事务
#释放句柄对象  
cursor.close()

#关闭mysql 连接 
db.close()
````





