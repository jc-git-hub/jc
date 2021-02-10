# python开发环境配置

## python开发环境配置

 

Python 2和Python 3之间存在着较大的差异，并且，由于各种原因导致了Python 2和Python 3的长期共存。在实际工作过程中，我们可能会同时用到Python 2和Python 3，因此，也需要经常在Python 2和Python 3之间进行来回切换。这就需要对python的版本进行管理，除此之外还需要对不同的软件包进行管理。大部分情况下，对于开源的库我们使用最新版本即可。但是，有时候可能需要对相同的Python版本，在不同的项目中使用不同版本的软件包。

## 安装python3

```
yum -y install  python3  
```

## 安装 psm

```
pip3 install psm   #安装psm  选择国内源 来下载  python工具  
psm ls   #列出国内那些源可以使用  

psm show   #显示当前正在使用哪个源 

pam use douban 
```

## 安装 virtualenv

```
pip3 install virtualenv 
```

## 安装 virtualenvwrapper

```
pip3 install virtualenvwrapper  
```

### 查找命令所在的位置

- which
- whereis

```
which python3    #/usr/bin/python3
```

### 查找脚本所在的位置

```
find / -name virtualenvwrapper.sh #/usr/local/bin/virtualenvwrapper.sh
```

## 编辑配置文件 ~/.bashrc

> 相当于Windows中的 添加环境变量

 

```
vim ~/.bashrc  

export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3  #创建虚拟环境默认的python版本
export WORKON_HOME=~/.envs    #创建好的虚拟环境所在的位置
source /usr/local/bin/virtualenvwrapper.sh  # 管理虚拟环境的脚本  

source  ~/.bashrc 
```

### 创建虚拟环境

 

```
mkvirtualenv 虚拟环境名字   # 创建成功以后自动进入虚拟环境中 
```

 

### 退出虚拟环境

 

```
deactivate  #退出虚拟环境
```

 

### 列出所有的虚拟环境

 

```
lsvirtualenv 
```

 

### 进入指定的虚拟环境

 

```
workon 虚拟环境名称 
```

 

### 查看虚拟环境所在的目录

 

```
workon 虚拟环境名称 
cdvirtualenv  
pwd  
```

 

### 删除虚拟环境

 

```
退出虚拟环境所在的目录  切换到别的目录 
deactivate #退出当前的虚拟环境
lsvirtualenv  
rmvirtualenv 虚拟环境名字  
Copy
```

 

### 创建python2版本的虚拟环境

 

```
which python  # /usr/bin/python  #找到python2所在的位置  
mkvirtualenv  --python=/usr/bin/python   虚拟环境名字  
```

 

#### 切换到不同的虚拟环境

 

```
python  # 查看python版本  


pip list #列出当前虚拟环境安装的软件
```