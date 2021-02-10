# 读写分离   

> 读写分离是解决方案
>
> 具体实施 是主从复制

​     

| ip            | 角色   | 说明                            |
| ------------- | ------ | ------------------------------- |
| 192.168.54.55 | master | 拥有写的权限 从库来这边同步数据 |
| 192.168.54.50 | slave  | 拥有只读的权限                  |

1. 保证主库和从库 能够正常通信 一般在内网下面
2. 关闭防火墙 systemctl stop firewalld.service
3. 配置 master

```
   vim /etc/my.cnf 
   [mysqld]
   log-bin=mysql-bin
   server-id=55
   binlog-do-db=demo
   binlog-ignore-db=mysql
       
       
   systemctl restart mysqld.service 
```

​     

1. 配置slave

 

```
   [mysqld]
   server-id=55
   replicate_do_db=demo
   replicate_ignore_db=mysql
       
   systemctl restart mysqld.service 
```

​     

1. 创建 一模一样的表结构

   ```shell
   mysql> create database demo;
   Query OK, 1 row affected (0.02 sec)
          
   mysql> use demo;
   Database changed
   mysql> create table user(id int(11) unsigned not null primary key auto_increment,username varchar(64) not null)engine=innodb default charset=utf8;
   Query OK, 0 rows affected (0.01 sec)
   ```

2. 主库上创建一个专门用来同步权限的账户

   ```shell
   # 创建同步权限的用户   
   mysql> create user 'user'@'X.X.X.X' identified by 'password';
   Query OK, 0 rows affected (0.01 sec)
   # 对用户授权       
   mysql> grant replication slave on *.* to 'mysync'@'%' identified by '123456';
   Query OK, 0 rows affected, 1 warning (0.00 sec)
   # 刷新权限       
   mysql> flush privileges;
          
   mysql> show master status;
   +------------------+----------+--------------+------------------+-------------------+
   | File             | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
   +------------------+----------+--------------+------------------+-------------------+
   | mysql-bin.000002 |      154 | demo         | mysql            |                   |
   +------------------+----------+--------------+------------------+-------------------+
   1 row in set (0.00 sec)
   ```

3. 从库上进行 跟随主库的设置

   ```shell
   # 查看帮助信息
   help contents
          
   help Transactions
          
   ? change master to  
          
          
   mysql> change master to 
       -> MASTER_HOST='192.168.54.55',
       -> MASTER_USER='mysync',
       -> MASTER_PASSWORD='123456',
       -> MASTER_PORT=3306,
       -> MASTER_LOG_FILE='mysql-bin.000002',
       -> MASTER_LOG_POS=607,
       -> MASTER_CONNECT_RETRY=10;
          
          
   start slave\G   开启从服务器 
          
   mysql> show slave status \G
          
          
    Slave_IO_Running: Connecting
    Slave_SQL_Running: Yes
   ```

