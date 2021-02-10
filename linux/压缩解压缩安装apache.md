## 压缩解压缩

```shell
windows:
rar 
zip
7z
iso

linux:
gz
bz2
xz

gz格式的压缩  
yum -y install gzip

gzip 文件1 文件2 文件3 文件n  # 压缩 源文件不在变成.gz文件
# 解压缩
gzip -d 文件1.gz 文件2.gz  #源文件不在
gzip不支持压缩目录


bz2格式
bzip2
yum -y install bz2
与gzip相同

xz格式
支持


zip 压缩解压缩
yum -y install zip unzip
zip 自己取的名字.zip  文件1  文件2 文件n  目录1  目录2
unzip 你起的名字.zip  # 解压缩

```

## 打包

```
-c  #打包
-x  #解包
-v  #详细列出过程
-f  #指定文件

-z  #压缩成gz格式
-j  #压缩成bz2格式
-J   #压缩成xz格式

tar -cvf  自己起名字.tar   文件1 文件2 文件n 目录n	# 源文件还在
tar -xvf  #解压缩

打包并压缩：
tar -zcvf 新文件名.tar 需要打包压缩的文件 
tar -zxvf 需要解压缩的文件.tar
```

## 软件安装

- rpm   
  - 先下载 rpm 压缩包
  - 缺点 严格按照顺序安装
- yum   
  - 为了解决rpm 依赖包的问题
  - 自动下载所需要的软件 解决依赖问题
- 编译   
  - 下载
  - 解包并解压缩
  - 配置     
    - ./configure
    - 安装到哪个位置
  - 编译
  - 安装

 

### 编译安装 apache

 

```shell
yum -y install wget 
wget -c https://mirrors.tuna.tsinghua.edu.cn/apache//httpd/httpd-2.4.46.tar.gz
wget -c https://mirrors.bfsu.edu.cn/apache//apr/apr-1.7.0.tar.gz
wget -c https://mirrors.tuna.tsinghua.edu.cn/apache//apr/apr-util-1.6.1.tar.gz
wget -c https://ftp.pcre.org/pub/pcre/pcre-8.44.tar.gz
wget -c https://www.openssl.org/source/openssl-1.1.1i.tar.gz
安装依赖  
yum -y install  gcc  gcc-c++ libtool libtool-ltdl libtool-ltdl-devel expat-devel 

1.安装 apr 
tar -zxvf apr-1.7.0.tar.gz

cd apr-1.7.0
vim configure   
将 RM='$RM'  改成 RM='$RM -f'
./configure  --prefix=/usr/apr  #指定安装的位置 
make && make install 

2.安装 apr-util  
tar -zxvf apr-util-1.6.1.tar.gz
cd apr-util-1.6.1
./configure --prefix=/usr/local/apr-util --with-apr=/usr/apr
make && make install 

3.安装pcre 
tar -zxvf pcre-8.44.tar.gz
cd  pcre-8.44
./configure --prefix=/usr/local/pcre
make && make install 

4.安装openssl  
tar -zxvf openssl-1.1.1i.tar.gz
cd openssl-1.1.1i
./config 
make && make install 
5.httpd 

tar -zxvf httpd-2.4.46.tar.gz

cd httpd-2.4.46/
./configure --prefix=/usr/local/httpd  --sysconfdir=/etc/httpd/ --enable-so --enable-ssl --enable-cgi --enable-rewrite --with-zlib --with-pcre=/usr/local/pcre --with-apr=/usr/apr --with-apr-util=/usr/local/apr-util

make && make install 

--enable 启用模块
--with 依赖于什么包

#启动服务 

cd /usr/local/httpd/bin 

[root@localhost bin]# ./apachectl start 
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using localhost.localdomain. Set the 'ServerName' directive globally to suppress this message

cd /etc/httpd/
 cp httpd.conf httpd.conf.bak
vim httpd.conf

底部命令模式  :set nu  
:199  
ServerName 127.0.0.1:80  


cd /usr/local/httpd/bin/
[root@localhost bin]# ./apachectl restart 
systemctl stop firewalld.service #关闭防火墙  


 cd /usr/local/httpd/htdocs/
vim index.html  改成你想要的内容 

在浏览器 输入该服务器的ip地址  
```