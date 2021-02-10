# 导出mysql语句

## 表字段修改

```mysql

-- 修改表字段类型 ALTER TABLE uses MODIFY pwd BIGINT(10)
-- 增加表字段alter table uses add column money FLOAT(10)

-- 不写modify也可以 alter table uses add tel varchar(11)

-- 删除表字段 alter table uses DROP money;
-- desc uses;

-- show TABLES
-- desc uses;
-- alter table uses change username user_name varchar(255);
-- change add modift 都支持first after;

-- desc uses
-- change 改字段名
-- add 增加表字段
-- 修改字段数据类型;

-- alter table uses change user_name username varchar(200) first;
-- desc uses
-- alter table uses add sex VARCHAR(20) after;
-- alter table uses add COLUMN later varchar(200) FIRST;
-- desc uses;

-- alter table uses drop later;
-- desc uses

-- alter table uses add column later varchar(200) first;

-- desc uses

-- alter table uses add firsts varchar(20) after;


-- alter table 旧表名 新表名
-- alter table uses rename users 
-- show tables

-- desc users
-- alter table users add test1 int(10) default 100 first;
-- 
-- alter table users drop later;
-- alter table users drop firts;
-- desc users

-- CREATE table test1 (
-- id int(11) not null auto_increment,
-- age tinyint(4) default 18,
-- PRIMARY KEY (id)
-- )ENGINE = INNODB DEFAULT CHARSET = utf8mb4

alter table test1 add  laters int(10) ;
```

```mysql

# mysql 引擎
# mysql 从5.5.5开始默认引擎是innoDB
# 以前是MyISAM

# 查看引擎
show ENGINES \G #mysql 以分号结尾  \G分行显示 最佳阅读体验

myisam、innodb区别
1. myisam 不支持事务  表锁  支持全文索引 读取效率高  如果这张表读的多 使用myisam
2. myisam 只缓存索引文件  数据库文件的缓存  由 操作系统完成
3. 

		
```

## 增删改查

```mysql
use myfirst_database;
desc person;

use myfirst_database;
insert into person(id,username) VALUES
('001','wt'),('002','jc'),('003','heih');

select * from person

desc test1

select * from test1

# 修改表字段为主键自增 

alter table test1 modify id int(11) not null primary KEY auto_increment;

# SELECT 类似于python的print
# 打印
SELECT '666';

select '555' as 'haha'

desc person
# 查询
# SELECT 指定字段 FROM 指定表
select id,username from person

# 指定字段 as 别名
select id as 用户编号 ,username as 用户名 from person 

# distinct 单个字段不重复
select username from person ;
SELECT distinct username from person;

# where 限定选择
SELECT *  from person where prsword is NULL;

# 排序 order by esc（默认升序）DESC（降序）
# 对一个字段排序
SELECT * from person where age order by age ASC;
select * from person where id order by age DESC;

# 多个字段排序  如果第一个字段排序完成 
# 在对排序完成相同的字段排序
select * from person where id order by age ,id;


# LIMIT 限制结果集 limit 数据行数
select * from person where age LIMIT 4;
select * from person where age>=18 order by id limit 4;

# 可单独用order BY 排序  不用写where
SELECT * from person ORDER BY age

# is NOT NULL \is NULL
SELECT * from person WHERE prsword is not NULL;

# 区间  between AND
SELECT * from person where age  between 16 and 18;
SELECT * from person where age>=18;


# limit 区间结果集选择
select * from 表名 limit 偏移量，数量
SELECT * from person LIMIT 0,2
# 分页原理
limit （页数-1）*显示量

# 修改引擎
alter table person ENGINE=myisam

desc person 

show CREATE table person

# 修改前
show create table person
CREATE TABLE `person` (
  `id` int(11) NOT NULL,
  `username` varchar(64) DEFAULT NULL,
  `prsword` varchar(10) DEFAULT NULL,
  `age` int(3) NOT NULL DEFAULT '18',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4

# 修改后
CREATE TABLE `person` (
  `id` int(11) NOT NULL,
  `username` varchar(64) DEFAULT NULL,
  `prsword` varchar(10) DEFAULT NULL,
  `age` int(3) NOT NULL DEFAULT '18',
  PRIMARY KEY (`id`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8mb4
```

