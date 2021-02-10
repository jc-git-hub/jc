```shell
wget -c https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-4.4.3.tgz #下载
tar -zxvf mongodb-linux-x86_64-rhel70-4.4.3.tgz # 解包并解压缩 
mv mongodb-linux-x86_64-rhel70-4.4.3  /usr/local/mongodb  #将目录移动并改名字 /usr/local/mongodb

mkdir -p /data/db # 创建一个文件夹又来保存数据库的文件   

/usr/local/mongodb/bin  #这里存放的是mongodb执行的命令  
vim ~/.bashrc
	export PATH=/usr/local/mongodb/bin:$PATH
	
source ~/.bashrc  #让配置文件立即生效  


#第一种启动方式  
 mongod --dbpath=/data/db --logpath=/usr/local/mongodb/mongodb.log --logappend &  #启动服务 
 # --dbpath  指定 数据库文件存放的位置  
 # --logpath 指定 日志文件存放的位置  
 
 # --logappend  日志追加的方式  
 # &  后台执行的  
 
 第二种启动方式
 
 
 vim /usr/local/mongodb/mongodb.conf 
 
 
 port=27017 #绑定端口号

dbpath=/data/db #指定数据库存放的位置

logpath=/usr/local/mongodb/mongodb.log #日志的路径

fork=true  #服务后台运行 

logappend=true  # 日志写入方式 

bind_ip=0.0.0.0  # 允许所有的客户端 ip 都可以连接   



mongod --config /usr/local/mongodb/mongodb.conf   #以配置文件的方式启动 



mongo 


exit #退出mongodb   
```

