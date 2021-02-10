# Redis

 

> http://redis.cn/

 

## redis 持久化

 

- aof
- rdb

 

## 安装

 

```
gcc -v

yum -y install centos-release-scl
yum -y install devtoolset-9-gcc devtoolset-9-gcc-c++ devtoolset-9-binutils
scl enable devtoolset-9 bash
echo "source /opt/rh/devtoolset-9/enable" >>/etc/profile

wget -c  http://download.redis.io/releases/redis-6.0.6.tar.gz

tar -zxvf redis-6.0.6.tar.gz

mv redis-6.0.6  /usr/local/redis


cd /usr/local/redis


make install 
```