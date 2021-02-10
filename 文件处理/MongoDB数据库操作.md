# MongoDB数据库操作

`MongoDB`是一个基于分布式文件存储的`NoSQL`数据库。在处理海量数据的时候会比`MySQL`更有优势。爬虫如果上了一个量级，可能就会比较推荐使用`MongoDB`，当然没有上量的数据也完全可以使用`MongoDB`来存储数据。因此学会使用`MongoDB`也是爬虫开发工程师必须掌握的一个技能。

## `Windows`下安装`MongoDB`数据库：

在官网下载`MongoDB`数据库。是一个`msi`文件。官网地址如下：https://www.mongodb.com/download-center?ct=atlasheader#community 然后双击进行安装：

在安装的时候选择安装`Compass`。这个软件是用图形化的界面操作`MongoDB`，使用起来非常方便。

## 运行`MongoDB`：

1. 创建数据目录： 启动`MongoDB`之前，首先要给他指定一个数据存储的路径。比如我在`MongoDB`的安装路径下创建一个`data`文件夹，专门用来存储数据的。`D:\ProgramApp\mongodb\data`。
2. 把`mongodb`的`bin`目录加入到环境变量中。方便后期调用。
3. 执行命令`mongod --dbpath D:\ProgramApp\mongodb\data`启动。

## 连接`MongoDB`：

在环境变量设置好的前提下，使用以下命令`mongo`就可以进入到`mongo`的操作终端了。

## 使用`Compass`软件连接`MongoDB`：

`Compass`是一个图形化的操作`MongoDB`的客户端。使用他来操作会更加方便。

## 将`MongoDB`制作成`windows`服务：

启动`mongodb`后，如果想让`mongodb`一直运行，那么这个终端便不能关闭，而且每次运行的时候还需要指定`data`的路径。因此我们可以将`mongodb`制作成一个服务，以后就通过一行命令就可以运行了。以下将讲解如何制作服务：

1. 创建配置文件：在`mongodb`安装的路径下创建配置文件`mongod.cfg`（路径和名字不是必须和我这的一样），然后在配置文件中添加以下代码：

   ```
   logpath=D:\ProgramApp\mongodb\data\log\mongod.log
   dbpath=D:\ProgramApp\mongodb\data\db
   Copy
   ```

   `logpath`是日志的路径。`dbpath`是`mongodb`数据库的存储路径。

2. 安装`mongodb`服务： 使用以下命令即可将`mongodb`安装成一个服务：

   ```
   mongod --config "cfg配置文件所在路径" --install
   比如：
   mongod --config "D:\ProgramApp\mongodb\mongod.cfg" --install
   Copy
   ```

3. 启动`mongodb`：`net start mongodb`。

4. 关闭`mongodb`： `net stop mongodb`。

5. 移除`mongodb`：`"D:\ProgramApp\mongodb\bin\mongod.exe" --remove`。

## `MongoDB`概念介绍：

| SQL术语/概念 | MongoDB术语/概念 | 解释/说明                           |
| ------------ | ---------------- | ----------------------------------- |
| database     | database         | 数据库                              |
| table        | collection       | 数据库表/集合                       |
| row          | document         | 数据记录行/文档                     |
| column       | field            | 数据字段/域                         |
| index        | index            | 索引                                |
| joins        | joins            | 表连接,MongoDB不支持                |
| primary key  | primary key      | 主键,MongoDB自动将_id字段设置为主键 |

## `MongoDB`三元素：

三元素：数据库、集合、文档。

1. 文档（document）：就是关系型数据库中的一行。文档是一个对象，由键值对构成，是

   ```
   json
   Copy
   ```

   的扩展形式：

   ```json
    {'name':'abc','gender':'1'}
   Copy
   ```

2. 集合（collection）：就是关系型数据库中的表。可以存储多个文档，结构可以不固定。如可以存储如下文档在一个集合中：

   ```json
    {"name":"abc","gender":"1"}
    {"name":"xxx","age":18}
    {"title":'yyy','price':20.9}
   Copy
   ```

## MongoDB基本操作命令：

1. `db`：查看当前的数据库。
2. `show dbs`：查看所有的数据库。
3. `use 数据库名`：切换数据库。如果数据库不存在，则创建一个。（创建完成后需要插入数据库才算创建成功）
4. `db.dropDatabase()`：删除当前指向的数据库。
5. `db.集合名.insert(value)`：添加数据到指定的集合中。
6. `db.集合名.find()`：从指定的集合中查找数据。 更多命令请见：http://www.runoob.com/mongodb/mongodb-tutorial.html

## Python操作`MongoDB`：

### 安装`pymongo`：

要用`python`操作`mongodb`，必须下载一个驱动程序，这个驱动程序就是`pymongo`：

```python
pip install pymongo
Copy
```

### 连接`MongoDB`：

```python
import pymongo
# 获取连接的对象
client = pymongo.MongoClient('127.0.0.1',port=27017)
# 获取数据库
db = client.zhihu
# 获取集合（表）
collection = db.qa
# 插入一条数据到集合中
collection.insert_one({
    "username":"abc",
    "password":'hello'
})
Copy
```

### 数据类型：

| 类型      | 说明                                 |
| --------- | ------------------------------------ |
| Object ID | 文档ID                               |
| String    | 字符串，最常用，必须是有效的UTF-8    |
| Boolean   | 存储一个布尔值，true或false          |
| Integer   | 整数可以是32位或64位，这取决于服务器 |
| Double    | 存储浮点值                           |
| Arrays    | 数组或列表，多个值存储到一个键       |
| Object    | 用于嵌入式的文档，即一个值为一个文档 |
| Null      | 存储Null值                           |
| Timestamp | 时间戳，表示从1970-1-1到现在的总秒数 |
| Date      | 存储当前日期或时间的UNIX时间格式     |

### 操作`MongoDB`：

操作`MongoDB`的主要方法如下：

1. ```
   insert_one
   Copy
   ```

   ：加入一条文档数据到集合中。示例代码如下：

   ```python
    collection.insert_one({
        "username":"abc",
        "password":'hello'
    })
   Copy
   ```

2. ```
   insert_many
   Copy
   ```

   ：加入多条文档数据到集合中。

   ```python
    collection.insert_many([
        {
            "username":'abc',
            'password':'111111'
        },
        {
            "username":'bbb',
            'password':'222222'
        },
    ])
   Copy
   ```

3. ```
   find_one
   Copy
   ```

   ：查找一条文档对象。

   ```python
    result = collection.find_one()
    print(result)
    # 或者是指定条件
    result = collection.find_one({"username":"abc"})
    print(result)
   Copy
   ```

4. ```
   update_one
   Copy
   ```

   ：更新一条文档对象。

   ```python
    collection.update_one({"username":"abc"},{"$set":{"username":"aaa"}})
   Copy
   ```

5. ```
   update_many
   Copy
   ```

   ：更新多条文档对象。

   ```python
    collection.update_many({"username":"abc"},{"$set":{"username":"aaa"}})
   Copy
   ```

6. ```
   delete_one
   Copy
   ```

   ：删除一条文档对象。

   ```python
    collection.delete_one({"username":"abc"})
   Copy
   ```

7. ```
   delete_many
   Copy
   ```

   ：删除多条文档对象。

   ```python
    collection.delete_one({"username":"abc"})
   ```