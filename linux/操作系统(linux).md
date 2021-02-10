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
