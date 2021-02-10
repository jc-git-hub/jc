# Linux操作系统  

## 操作系统分类  

> 本质上是内核   根据内核分为以下三类 

* windows  
* Linux 
* unix 

## Linux发展史  

* Linux = linus + unix  
* 企鹅吉祥物 
* git 
  * 代码版本管理工具
    * svn
    * git 
* 

## Linux 特点  

* 开源免费  
* 资源消耗低   
* 速度快  
* 资源利用率高 
* 安全   
* 应用广 
* 移植性  

### 软件分类  

* GUI  
* 命令行 



# Linux启动流程(了解)

- 加载BIOS(Basic Input Output System)：BIOS是系统启动时加载的第一个软件。
  - 启动上电自检POST(Power-On-Self-Test)，负责完成对CPU、主板、内存、软硬盘子系统、显示子系统（包括显示缓存）、串并行接口、键盘、CD-ROM光驱等的检测，主要检查硬件的好坏。
  - 对外部设备进行初始化，读取BIOS参数，并和实际的硬件进行比较，如果不符合，会影响系统启动。
  - 查找MBR(Master Boot Record,主引导分区)。如果未找到，会提示找不到硬盘。
- 读取主引导分区(MBR):拷贝启动引导代码BootLoader
- 启动引导代码(bootloader):当我们的硬盘上有多个操作系统时，可以用来选择进入到哪个操作系统。
- 加载内核，进入操作系统：运行第一个程序 : /sbin/init
  - sbin/init 会读取相关的配置文件，来确定系统的运行级别。
    - 0： 关机
    - 1 ： 单用户模式
    - 2 ： 无网络支持的多用户模式
    - 3 ： 有网络支持的多用户模式
    - 4 ： 保留，未使用
    - 5 ： 有网络支持，且有图形化界面的多用户模式
    - 6 ： 重启
    - 切换运行级别： init 级别
  - 根据对应的运行级别，查找对应的脚本文件。例如，运行5级别，查找 /etc/rc5.d目录，启动该目录下的相关服务。
    - 这些文件夹下的init脚本都有一些特别的名字，命名都以S（start）、K（kill）或D（disable）开头，后面跟一个数字。当init进入一个运行等级的时候，它会按照数字顺序运行所有以K开头的脚本并传入stop参数，除非对应的init脚本在前一个运行等级中没有启动。然后init按照数字顺序运行所有以S开头的脚本并传入start参数。任何以D开头的init脚本都会被忽略—这让你可以在指定的运行等级禁止一个脚本，或者你也可以仅仅移除全部符号链接。
  - 解析用户自定义的启动脚本：/etc/rc.local（如果存在的话）
  - 进入用户界面。

## Linux 分类 

> GUI 的不同  

* RedHat阵营  
  * RHEL  红帽企业Linux  
  * Centos 
* Debian 阵营  
  * Debian  
  * Ubuntu  
  * fedora  
  * deepin 

## 安装Linux  

* CPU支持  虚拟化技术 virtual technology   
* 一台上  一个操作系统 对cpu的利用率不高  这样的话容易浪费  可以利用虚拟化技术  再安装一个或者多个操作系统  利用剩余的cpu  









# linux操作系统

## 操作系统分类

> 本质上是内核 根据内核分类

* windows
* linux
* unix

## Linux发展史

* Linux= linus + unix
* 企鹅吉祥物
* git
  * 代码管理工具
    * svn
    * git

## linux特点

* 开源免费
* 资源消耗低
* 速度快
* 资源利用率高
* 安全
* 应用广
* 移植性

### 软件分类

* GUI
* 命令行

## linux分类

> GUI不同

* RedHat阵营
  * RHEL 红帽企业linux
  * Centos
* Debian阵营
  * Debain
  * Ubuntu
  * fedora
  * deepin

## 安装Linux

* CPU支持 虚拟化技术  virtual technology
* 一台电脑 一个操作系统对CPU的利用率不高 这样的话容易浪费  利用虚拟化技术 安装多个操作系统 利用剩余的CPU

# yum

# 使用之前请确保已经安装wget，如未安装请执行下面一条命令来安装

```
yum install -y wget
```

# 1.备份当前yum源（可选）

```
cd /etc/yum.repos.d/
cp /CentOS-Base.repo /CentOS-Base-repo.bak
```

# 2.使用wget下载阿里yum源repo文件

```
wget http://mirrors.aliyun.com/repo/Centos-7.repo
```

# 3.清理默认缓存包

```
yum clean all
```

# 4.把下载下来的阿里云repo文件设置成为默认源

```
mv Centos-7.repo CentOS-Base.repo
```

# 5.生成阿里云yum源缓存并更新yum源

```
yum makecache
yum update
```

## 远程连接

```
yum -y install openssh-server
启动服务  开启22端口
service sshd restart   /
systemctl start sshd.service

```

## 























## 常用命令 

```shell
查看帮助

命令  --help 
man 命令   # yum -y install man   空格 分页   q 退出  

关机重启命令  

shutdown -h 12:30 #12:30分关机 
shutdown -h now #立即关机

init 0 #关机

reboot #重启
init 6 #重启 

init5 # 由命令行转为图形界面   ctrl+alt+F2 图形界面到命令行

history #历史命令 
!历史命令行号 #重新执行第 条命令  


#目录操作  Linux 一切从根目录/ 出发  
cd  # 切换到当前用户的家目录 
cd  /home/ #切换到home目录下面  绝对路径  
cd .. #回到上一级目录  
cd ../../  # 回到上上级目录 
cd .  #回到当前目录  

cd - #从哪里切换过来回到哪里去  

pwd #查看当前位于哪个目录   



#快捷键  

tab 键 补全代码
ctrl+c #立即终止  
⬆ #上一条历史命令 
⬇ #下一条历史命令  
ctrl+a #快速移动到命令开头
ctrl+l #清屏  

# 优雅关机  

sync  # 先将内存数据同步到硬盘中  

```



## 终端显示  

```shell
[root@localhost ~]# 
root #当前用户名 
localhost #主机名  
~ #当前用户的家目录    root的家目录在  /root   普通用户的家目录  在 /home/普通用户用户名 
# #管理员用户正在输入 
$ # 普通用户正在输入  

```

## 挂载 

```
u盘内容不能直接看   
我们的电脑可以看硬盘中的内容
把u盘插到电脑上的过程就叫挂载  
拔下来 就是取消挂载  
```



## 文件系统 

* windows 文件系统类型 是NTFS 
* Linux 是ext
* Linux 一切都是文件   不区分后缀名 也就是说  a.txt  a.jpg 在它看来都是一样的文件 



## vim编辑器  

> windows 中 对于文件的操作 都 写 修改 删除 复制  替换 查找  保存  
>
> Linux中对于上述操作 分别在不同的模式下  



### 编辑模式 

> vim test.txt  进入命令模式     a  i   o    进入编辑模式 

| 键   | 说明                              |
| ---- | --------------------------------- |
| i    | 在光标的位置 插入                 |
| a    | 在光标的下一个位置 插入           |
| o    | 在光标的 下一行插入               |
| A    | 在光标所在行尾插人                |
| S    | 先将所在的行 内容删除  然后输入   |
| s    | 先将光标所在位置字符删除 然后输入 |
| I    | 在行首输入                        |
|      |                                   |






### 命令模式  

> vim  test.txt  
>
> 编辑模式 esc 回到命令模式  

| 键             | 说明                                                        |
| -------------- | ----------------------------------------------------------- |
| h              | 光标向左移动                                                |
| j              | 光标向下移动                                                |
| k              | 光标向上移动                                                |
| l              | 光标向右移动                                                |
| dd             | 删除一行                                                    |
| ndd            | 删除n行                                                     |
| u              | 撤回上一次的操作                                            |
| yy             | 复制一行                                                    |
| p              | 粘贴一行                                                    |
| np             | 粘贴n行                                                     |
| nyy            | 复制n行  加入 100yy  如果实际不到100行 有多少行就复制多少行 |
| GG             | 回到结尾                                                    |
| gg             | 回到开头                                                    |
| shift+9        | 块的开头  段落                                              |
| shift+0        | 块的结尾  段落结尾                                          |
| .              | 重复上一次的操作                                            |
| shift+6      ^ | 快速回到行首                                                |
| shift+4    $   | 快速回到行尾                                                |
|                |                                                             |



### 底部命令模式 

> 命令模式-》: 或者 ?  进入底部命令模式  

| 键                                                        | 值                                     |
| --------------------------------------------------------- | -------------------------------------- |
| :w                                                        | 保存                                   |
| :q                                                        | 退出                                   |
| ！                                                        | 强制                                   |
| :wq!                                                      | 强制保存并退出                         |
| :q!                                                       | 强制退出  不保存                       |
| :x！                                                      | 强制保存并退出                         |
| :set nu                                                   | 显示行号                               |
| :set nonu                                                 | 取消显示行号                           |
| :n                                                        | 将光标定位到第n行                      |
| /字符串  回车                                             | n 下一个结果  shift+n 上一个结果       |
| ？字符串 回车                                             | n 上一个结果  shift+n 下一个结果       |
| :s/要查找的字符串/要替换的字符串                          | 替换光标所在行的查到的第一个结果       |
| :s/要查找的字符串/要替换的字符串/g                        | 替换光标所在行的查到的所有结果         |
| :%s/要查找的字符串/要替换的字符串                         | 替换所有行中匹配到的第一个结果         |
| :%s/要查找的字符串/要替换的字符串/g                       | 替换所有行中匹配到的所有结果           |
| :n1,n2s/要查找的字符串/要替换的字符串   :10,20s/张三/李四 | 替换n1到n2之间匹配到每一行的第一个结果 |
| :n1,n2s/要查找的字符串/要替换的字符串/g                   | 替换n1到n2之间匹配到每一行的所有结果   |
| :%s/http:\/\/www.baidu.com/https:\/\/www.qfedu.org/       |                                        |
|                                                           |                                        |



## 目录的操作 

```
ls --help   #查看帮助 
man ls   # 查看帮助

-a  #显示所有文件  包含隐藏文件  
-l # 列出文件或者目录的详细信息 
-h # 用最佳阅读体验  k  m  g
```

### 目录的创建及删除 

```shell
mkdir 目录名 # 创建一个目录  
mkdir -p 递归创建目录 #mkdir -p haha/hahaha/hahahaha/hahahahaha/hahahahahaha 
mkdir -p a/{b,c}/{d,e,f} 
rm -rf 目录名 # r 递归删除  f强制    #删除之前小心  一定做好备份   杜绝 rm -rf /* 的出现  

```



### 列表解读 

```
lrwxrwxrwx.   1 root root    8 1月  12 00:17 sbin -> usr/sbin
drwxr-xr-x.   2 root root    6 4月  11 2018 srv
dr-xr-xr-x.  13 root root    0 1月  12 08:54 sys
-rw-r--r--.   1 root root   14 1月  12 14:33 test.txt

第一部分: l  d  -     l 链接 好比Windows中的快捷方式 d 目录 -  文件 
第二部分:rwxrwxrwx   文件的权限  r 读 w 写 x exec执行   rwx 拥有者   r-x 所在的组   r-x 其他用户  
第三部分: 文件inode 节点  
第四部分: root 目录或者文件的拥有者  
第五部分  root  目录或者文件的所属组  
第六部分  8 文件大小 
第七部分 1月  12 00:17 文件上次大的修改时间  
第八部分 test.txt  目录或者文件的名字  
```

#### 权限 

```
r  read读
w  write写
x  exec 执行 
-  没有权限

rwx 
r 100   4
w 010   2
x 001   1

拥有者  所属组 其它用户  
rwx    rw-    r-x
7      6      5
	  拥有者  所属组 其它用户  
755   rwx      r-x  r-x
700   rwx      ---  ---
600   rw-      ---  ---

```



### ll 

```
ls -al  
ll 是上面命令的别名  
alias c='cd ..' #c 就是 cd ..的别名  这是临时的 重启会失效  

永久生效   
vim ~/.bashrc   
添加 alias c='cd ..'

source ~/.bashrc #让配置文件生效
 
```



## 软链接 

```shell
ln -s 目标文件  快捷方式名称 
```

## 硬链接  

```
ln 源文件名 新文件名 
```



### 往文件中写入内容

```
echo '我不想跟你一起吃晚餐,做最浪漫的事,一起吃早餐' > haha.txt   # > 下一次会把上一次替换掉
echo '我不想跟你一起吃晚餐,做最浪漫的事,一起吃早餐' >> haha.txt  # 追加到后面一行  
```



### 文件的删除  

```shell
rm  -i  #询问是否删除    y 是 n 否  
rm -f  #强制删除   
rm -r  #递归删除   

rm -rf #删除之前检查一下  
rm -rf * #删除当前目录所有   不要在  / 使用  
rm -rf  *.txt  #删除当前目录下  txt结尾的文件  
```



### 文件的拷贝  

```
cp 文件名1  文件名2  # 将文件名1 复制一份命名为 文件名2 

cp test1.txt test1.txt.bak  #复制文件 完成备份
```

### 文件的移动  

```
mv  #同一个目录 下面 重命名  将一个文件 mv 到不同目录 这是剪切  

mv kangbazi.txt.bak  kangbazi.txt #将前面文件重命名  
mv kangbazi.txt  /tmp   #将kangbazi.txt 这个文件剪切到 /tmp目录下 
 mv /tmp/CentOS-Base.repo.qinghua /home/ruirui_haha #将/tmp这个文件剪切到 /home目录下 并改名字  ruirui_haha
 

```

### 文件的查找 

```
find  [路径] [参数] [文件名]

-name 根据文件名查找 
-iname 根据文件名查找  文件名不区分大小写  
-mtime +/-n  -n表示 n天  +n 超过n天的文件   -n n天以内修改的 
-user 根据所属用户 
-size [+/-]n[c/k/m/g]  # -size +3c  大小大于3字节的
-perm 根据权限查找  
-maxdepth #按照深度进行查找  
-ls 查出来的结果按照列表的形式进行展示


[root@localhost ~]# find . -name 'haha.txt' #从当前目录一起查找
./haha.txt
[root@localhost ~]# find  -name 'haha.txt' #从当前目录一起查找 
./haha.txt

find / -mtime -3 #查找3天以内的  
find / -user 'root' #查找所属用户是root的 
find / -maxdepth 1 -size -10k -ls #查找 /目录下 深度是1 大小小于10k 的  并且结果以详细的列表展示 
find /tmp -perm 755   #查找 /tmp 权限是 755的  

```

