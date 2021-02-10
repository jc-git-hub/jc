# Linux Mysql 的安装

## 1、关闭mysql服务`systemctl stop mysqld`

## 2、查看已经安装的mysql组件

```shell
root@172 ~]# rpm -qa | grep -i mysql  #执行这一步


mysql-community-libs-compat-5.7.20-1.el7.x86_64
mysql-community-libs-5.7.20-1.el7.x86_64
mysql57-community-release-el7-11.noarch
mysql-community-client-5.7.20-1.el7.x86_64
mysql-community-server-5.7.20-1.el7.x86_64
mysql-community-common-5.7.20-1.el7.x86_64
```

## 3、卸载已经安装过的组件

```shell
yum -y remove mysql-community-client-5.7.20-1.el7.x86_64
yum -y remove mysql-community-common-5.7.20-1.el7.x86_64

# 卸载comm时，libs-compat会跟随卸载，此步可不操作
yum -y remove mysql-community-libs-compat-5.7.20-1.el7.x86_64
yum -y remove mysql57-community-release-el7-11.noarch

# 卸载client时，server会跟随卸载，此步可不操作
yum -y remove mysql-community-server-5.7.20-1.el7.x86_64
```

## 4、删除mysql目录

```shell
# whereis查找
[root@172 ~]# whereis mysql
mysql: /usr/share/mysql

# 删除残留
rm -rf /usr/share/mysql

# find查找
[root@172 ~]# find / -name mysql
/home/mysql
/etc/selinux/targeted/active/modules/100/mysql
/etc/selinux/targeted/tmp/modules/100/mysql
/var/lib/mysql
/var/lib/mysql/mysql

# 删除残留
rm -rf /home/mysql
rm -rf /etc/selinux/targeted/active/modules/100/mysql
rm -rf /etc/selinux/targeted/tmp/modules/100/mysql
rm -rf /var/lib/mysql
rm -rf /var/lib/mysql/mysql

# 删除配置文件
rm –rf /usr/my.cnf
rm -rf /root/.mysql_sercret  
```

## 5、确认卸载

```shell
rpm -qa | grep -i mysql
```

##  6、下载并安装MySQL官方的 Yum Repository

```shell
wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm

yum -y install mysql57-community-release-el7-10.noarch.rpm

yum -y install mysql-community-server
```

## 7、2 MySQL数据库设置

```shell
 首先启动MySQL
systemctl start  mysqld.service

查看MySQL运行状态
systemctl status mysqld.service

通过如下命令可以在日志文件中找出密码：
grep "password" /var/log/mysqld.log


mysql -u root -p



输入初始密码，此时不能做任何事情，因为MySQL默认必须修改密码之后才能操作数据库


修改密码复杂度协议 set global validate_password_policy=0; 

修改密码长度协议 set global validate_password_length=1; 

set password for root@localhost = password(''); 


### 下面省略
(rootlocalhost:密码)：其中‘new password’替换成你要设置的密码，注意:密码设置必须要大小写字母数字和特殊符号（,/';:等）,不然不能配置成功
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';

如果要修改为root这样的弱密码，需要进行以下配置：
查看密码策略
show variables like '%password%';

退出MySQL
修改密码策略
vi /etc/my.cnf

添加validate_password_policy配置
选择0（LOW），1（MEDIUM），2（STRONG）其中一种，选择2需要提供密码字典文件
#添加validate_password_policy配置
validate_password_policy=0
#关闭密码策略
validate_password = off

重启mysql服务使配置生效
systemctl restart mysqld
```

