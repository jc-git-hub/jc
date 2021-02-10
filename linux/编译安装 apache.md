# 编译安装 apache

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
cp -rf /root/apr-1.7.0 /root/httpd-2.4.46/srclib/apr
cp -rf /root/apr-util-1.6.1 /root/httpd-2.4.46/srclib/apr-util
cd /root/httpd-2.4.46/   
./configure --prefix=/usr/local/httpd  --with-included-apr --sysconfdir=/etc/httpd/ --enable-so --enable-ssl --enable-cgi --enable-rewrite --with-zlib --with-pcre=/usr/local/pcre --with-apr=/usr/apr --with-apr-util=/usr/local/apr-util

make && make install 



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



