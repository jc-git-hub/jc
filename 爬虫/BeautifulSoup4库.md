# BeautifulSoup4库

Beautiful Soup 是一个HTML/XML的解析器，主要的功能也是如何解析和提取 HTML/XML 数据。
lxml 只会局部遍历，而Beautiful Soup 是基于HTML DOM（Document Object Model）的，会载入整个文档，解析整个DOM树，因此时间和内存开销都会大很多，所以性能要低于lxml。
BeautifulSoup 用来解析 HTML 比较简单，API非常人性化，支持CSS选择器、Python标准库中的HTML解析器，也支持 lxml 的 XML解析器。
Beautiful Soup 3 目前已经停止开发，推荐现在的项目使用Beautiful Soup 4。

## 安装和文档：

1. 安装：`pip install bs4`。
2. 中文文档：<https://www.crummy.com/software/BeautifulSoup/bs4/doc/index.zh.html>

## 几大解析工具对比：

| 解析工具      | 解析速度 | 使用难度 |
| ------------- | -------- | -------- |
| BeautifulSoup | 最慢     | 最简单   |
| lxml          | 快       | 简单     |
| 正则          | 最快     | 最难     |

```
html = """
<table class="tablelist" cellpadding="0" cellspacing="0">
    <tbody>
        <tr class="h">
            <td class="l" width="374">职位名称</td>
            <td>职位类别</td>
            <td>人数</td>
            <td>地点</td>
            <td>发布时间</td>
        </tr>
        <tr class="even">
            <td class="l square"><a target="_blank" href="position_detail.php?id=33824&keywords=python&tid=87&lid=2218">22989-金融云区块链高级研发工程师（深圳）</a></td>
            <td>技术类</td>
            <td>1</td>
            <td>深圳</td>
            <td>2017-11-25</td>
        </tr>
        <tr class="odd">
            <td class="l square"><a target="_blank" href="position_detail.php?id=29938&keywords=python&tid=87&lid=2218">22989-金融云高级后台开发</a></td>
            <td>技术类</td>
            <td>2</td>
            <td>深圳</td>
            <td>2017-11-25</td>
        </tr>
        <tr class="even">
            <td class="l square"><a target="_blank" href="position_detail.php?id=31236&keywords=python&tid=87&lid=2218">SNG16-腾讯音乐运营开发工程师（深圳）</a></td>
            <td>技术类</td>
            <td>2</td>
            <td>深圳</td>
            <td>2017-11-25</td>
        </tr>
        <tr class="odd">
            <td class="l square"><a target="_blank" href="position_detail.php?id=31235&keywords=python&tid=87&lid=2218">SNG16-腾讯音乐业务运维工程师（深圳）</a></td>
            <td>技术类</td>
            <td>1</td>
            <td>深圳</td>
            <td>2017-11-25</td>
        </tr>
        <tr class="even">
            <td class="l square"><a target="_blank" href="position_detail.php?id=34531&keywords=python&tid=87&lid=2218">TEG03-高级研发工程师（深圳）</a></td>
            <td>技术类</td>
            <td>1</td>
            <td>深圳</td>
            <td>2017-11-24</td>
        </tr>
        <tr class="odd">
            <td class="l square"><a target="_blank" href="position_detail.php?id=34532&keywords=python&tid=87&lid=2218">TEG03-高级图像算法研发工程师（深圳）</a></td>
            <td>技术类</td>
            <td>1</td>
            <td>深圳</td>
            <td>2017-11-24</td>
        </tr>
        <tr class="even">
            <td class="l square"><a target="_blank" href="position_detail.php?id=31648&keywords=python&tid=87&lid=2218">TEG11-高级AI开发工程师（深圳）</a></td>
            <td>技术类</td>
            <td>4</td>
            <td>深圳</td>
            <td>2017-11-24</td>
        </tr>
        <tr class="odd">
            <td class="l square"><a target="_blank" href="position_detail.php?id=32218&keywords=python&tid=87&lid=2218">15851-后台开发工程师</a></td>
            <td>技术类</td>
            <td>1</td>
            <td>深圳</td>
            <td>2017-11-24</td>
        </tr>
        <tr class="even">
            <td class="l square"><a target="_blank" href="position_detail.php?id=32217&keywords=python&tid=87&lid=2218">15851-后台开发工程师</a></td>
            <td>技术类</td>
            <td>1</td>
            <td>深圳</td>
            <td>2017-11-24</td>
        </tr>
        <tr class="odd">
            <td class="l square"><a id="test" class="test" target='_blank' href="position_detail.php?id=34511&keywords=python&tid=87&lid=2218">SNG11-高级业务运维工程师（深圳）</a></td>
            <td>技术类</td>
            <td>1</td>
            <td>深圳</td>
            <td>2017-11-24</td>
        </tr>
    </tbody>
</table>
"""
```



## 简单使用：

```python
from bs4 import BeautifulSoup

html = """
<html><head><title>The Dormouse's story</title></head>
<body>
<p class="title" name="dromouse"><b>The Dormouse's story</b></p>
<p class="story">Once upon a time there were three little sisters; and their names were
<a href="http://example.com/elsie" class="sister" id="link1"><!-- Elsie --></a>,
<a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
<a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
and they lived at the bottom of a well.</p>
<p class="story">...</p>
"""

#创建 Beautiful Soup 对象
# 使用lxml来进行解析
soup = BeautifulSoup(html,"lxml")

print(soup.prettify())
```

## 四个常用的对象：

Beautiful Soup将复杂HTML文档转换成一个复杂的树形结构,每个节点都是Python对象,所有对象可以归纳为4种:

1. Tag
2. NavigatableString
3. BeautifulSoup
4. Comment

### 1. Tag：

Tag 通俗点讲就是 HTML 中的一个个标签。示例代码如下：

```python
from bs4 import BeautifulSoup

html = """
<html><head><title>The Dormouse's story</title></head>
<body>
<p class="title" name="dromouse"><b>The Dormouse's story</b></p>
<p class="story">Once upon a time there were three little sisters; and their names were
<a href="http://example.com/elsie" class="sister" id="link1"><!-- Elsie --></a>,
<a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
<a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
and they lived at the bottom of a well.</p>
<p class="story">...</p>
"""

#创建 Beautiful Soup 对象
soup = BeautifulSoup(html,'lxml')


print soup.title
# <title>The Dormouse's story</title>

print soup.head
# <head><title>The Dormouse's story</title></head>

print soup.a
# <a class="sister" href="http://example.com/elsie" id="link1"><!-- Elsie --></a>

print soup.p
# <p class="title" name="dromouse"><b>The Dormouse's story</b></p>

print type(soup.p)
# <class 'bs4.element.Tag'>
```

我们可以利用 soup 加标签名轻松地获取这些标签的内容，这些对象的类型是bs4.element.Tag。但是注意，它查找的是在所有内容中的第一个符合要求的标签。如果要查询所有的标签，后面会进行介绍。
对于Tag，它有两个重要的属性，分别是name和attrs。示例代码如下：

```python
print soup.name
# [document] #soup 对象本身比较特殊，它的 name 即为 [document]

print soup.head.name
# head #对于其他内部标签，输出的值便为标签本身的名称

print soup.p.attrs
# {'class': ['title'], 'name': 'dromouse'}
# 在这里，我们把 p 标签的所有属性打印输出了出来，得到的类型是一个字典。

print soup.p['class'] # soup.p.get('class')
# ['title'] #还可以利用get方法，传入属性的名称，二者是等价的

soup.p['class'] = "newClass"
print soup.p # 可以对这些属性和内容等等进行修改
# <p class="newClass" name="dromouse"><b>The Dormouse's story</b></p>
```

### 2. NavigableString：

如果拿到标签后，还想获取标签中的内容。那么可以通过`tag.string`获取标签中的文字。示例代码如下：

```python
print soup.p.string
# The Dormouse's story

print type(soup.p.string)
# <class 'bs4.element.NavigableString'>thon
```

### 3. BeautifulSoup：

BeautifulSoup 对象表示的是一个文档的全部内容.大部分时候,可以把它当作 Tag 对象,它支持 遍历文档树 和 搜索文档树 中描述的大部分的方法.
因为 BeautifulSoup 对象并不是真正的HTML或XML的tag,所以它没有name和attribute属性.但有时查看它的 .name 属性是很方便的,所以 BeautifulSoup 对象包含了一个值为 “[document]” 的特殊属性 .name

```python
soup.name
# '[document]'
```

### 4. Comment：

Tag , NavigableString , BeautifulSoup 几乎覆盖了html和xml中的所有内容,但是还有一些特殊对象.容易让人担心的内容是文档的注释部分:

```python
markup = "<b><!--Hey, buddy. Want to buy a used parser?--></b>"
soup = BeautifulSoup(markup)
comment = soup.b.string
type(comment)
# <class 'bs4.element.Comment'>
```

Comment 对象是一个特殊类型的 NavigableString 对象:

```python
comment
# 'Hey, buddy. Want to buy a used parser'
```

## 遍历文档树：

### 1. contents和children：

```python
html_doc = """
<html><head><title>The Dormouse's story</title></head>

<p class="title"><b>The Dormouse's story</b></p>

<p class="story">Once upon a time there were three little sisters; and their names were
<a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
<a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
<a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
and they lived at the bottom of a well.</p>

<p class="story">...</p>
"""

from bs4 import BeautifulSoup
soup = BeautifulSoup(html_doc,'lxml')

head_tag = soup.head
# 返回所有子节点的列表
print(head_tag.contents)

# 返回所有子节点的迭代器
for child in head_tag.children:
    print(child)
```

### 2. strings 和 stripped_strings

如果tag中包含多个字符串 [2] ,可以使用 .strings 来循环获取：

```python
for string in soup.strings:
    print(repr(string))
    # u"The Dormouse's story"
    # u'\n\n'
    # u"The Dormouse's story"
    # u'\n\n'
    # u'Once upon a time there were three little sisters; and their names were\n'
    # u'Elsie'
    # u',\n'
    # u'Lacie'
    # u' and\n'
    # u'Tillie'
    # u';\nand they lived at the bottom of a well.'
    # u'\n\n'
    # u'...'
    # u'\n'
```

输出的字符串中可能包含了很多空格或空行,使用 .stripped_strings 可以去除多余空白内容：

```python
for string in soup.stripped_strings:
    print(repr(string))
    # u"The Dormouse's story"
    # u"The Dormouse's story"
    # u'Once upon a time there were three little sisters; and their names were'
    # u'Elsie'
    # u','
    # u'Lacie'
    # u'and'
    # u'Tillie'
    # u';\nand they lived at the bottom of a well.'
    # u'...'
```

## 搜索文档树：

### 1. find和find_all方法：

搜索文档树，一般用得比较多的就是两个方法，一个是`find`，一个是`find_all`。`find`方法是找到第一个满足条件的标签后就立即返回，只返回一个元素。`find_all`方法是把所有满足条件的标签都选到，然后返回回去。使用这两个方法，最常用的用法是出入`name`以及`attr`参数找出符合要求的标签。

```python
soup.find_all("a",attrs={"id":"link2"})
```

或者是直接传入属性的的名字作为关键字参数：

```python
soup.find_all("a",id='link2')
```

### 2. select方法：

使用以上方法可以方便的找出元素。但有时候使用`css`选择器的方式可以更加的方便。使用`css`选择器的语法，应该使用`select`方法。以下列出几种常用的`css`选择器方法：

#### （1）通过标签名查找：

```python
print(soup.select('a'))
```

#### （2）通过类名查找：

通过类名，则应该在类的前面加一个`.`。比如要查找`class=sister`的标签。示例代码如下：

```python
print(soup.select('.sister'))
```

#### （3）通过id查找：

通过id查找，应该在id的名字前面加一个＃号。示例代码如下：

```python
print(soup.select("#link1"))
```

#### （4）组合查找：

组合查找即和写 class 文件时，标签名与类名、id名进行的组合原理是一样的，例如查找 p 标签中，id 等于 link1的内容，二者需要用空格分开：

```python
print(soup.select("p #link1"))
```

直接子标签查找，则使用 > 分隔：

```python
print(soup.select("head > title"))
```

#### （5）通过属性查找：

查找时还可以加入属性元素，属性需要用中括号括起来，注意属性和标签属于同一节点，所以中间不能加空格，否则会无法匹配到。示例代码如下：

```python
print(soup.select('a[href="http://example.com/elsie"]'))
```

#### （6）获取内容

以上的 select 方法返回的结果都是列表形式，可以遍历形式输出，然后用 get_text() 方法来获取它的内容。

```python
soup = BeautifulSoup(html, 'lxml')
print type(soup.select('title'))
print soup.select('title')[0].get_text()

for title in soup.select('title'):
    print title.get_text()
```

# BeautifulSoup笔记：

## find_all的使用：

1. 在提取标签的时候，第一个参数是标签的名字。然后如果在提取标签的时候想要使用标签属性进行过滤，那么可以在这个方法中通过关键字参数的形式，将属性的名字以及对应的值传进去。或者是使用`attrs`属性，将所有的属性以及对应的值放在一个字典中传给`attrs`属性。
2. 有些时候，在提取标签的时候，不想提取那么多，那么可以使用`limit`参数。限制提取多少个。

## find与find_all的区别：

1. find：找到第一个满足条件的标签就返回。说白了，就是只会返回一个元素。
2. find_all:将所有满足条件的标签都返回。说白了，会返回很多标签（以列表的形式）。

## 使用find和find_all的过滤条件：

1. 关键字参数：将属性的名字作为关键字参数的名字，以及属性的值作为关键字参数的值进行过滤。
2. attrs参数：将属性条件放到一个字典中，传给attrs参数。

## 获取标签的属性：

1. 通过下标获取：通过标签的下标的方式。

   ```python
   href = a['href']
   ```

2. 通过attrs属性获取：示例代码：

   ```python
   href = a.attrs['href']
   ```

## string和strings、stripped_strings属性以及get_text方法：

1. string：获取某个标签下的非标签字符串。返回来的是个字符串。如果这个标签下有多行字符，那么就不能获取到了。
2. strings：获取某个标签下的子孙非标签字符串。返回来的是个生成器。
3. stripped_strings：获取某个标签下的子孙非标签字符串，会去掉空白字符。返回来的是个生成器。
4. get_text：获取某个标签下的子孙非标签字符串。不是以列表的形式返回，是以普通字符串返回。


## CSS选择器：

1. 根据标签的名字选择，示例代码如下：

   ```css
   p{
       background-color: pink;
   }
   ```

2. 根据类名选择，那么要在类的前面加一个点。示例代码如下：

   ```css
   .line{
       background-color: pink;
   }
   ```

3. 根据id名字选择，那么要在id的前面加一个#号。示例代码如下：

   ```css
   #box{
       background-color: pink;
   }
   ```

4. 查找子孙元素。那么要在子孙元素中间有一个空格。示例代码如下：

   ```css
   #box p{
       background-color: pink;
   }
   ```

5. 查找直接子元素。那么要在父子元素中间有一个>。示例代码如下：

   ```css
   #box > p{
       background-color: pink;
   }
   ```

6. 根据属性的名字进行查找。那么应该先写标签名字，然后再在中括号中写属性的值。示例代码如下：

   ```css
   input[name='username']{
       background-color: pink;
   }
   ```

7. 在根据类名或者id进行查找的时候，如果还要根据标签名进行过滤。那么可以在类的前面或者id的前面加上标签名字。示例代码如下：

   ```css
   div#line{
       background-color: pink;
   }
   div.line{
       background-color: pink;
   }
   ```

## BeautifulSop中使用css选择器：

在`BeautifulSoup`中，要使用css选择器，那么应该使用`soup.select()`方法。应该传递一个css选择器的字符串给select方法。


## 常见的四种对象：

1. Tag：BeautifulSoup中所有的标签都是Tag类型，并且BeautifulSoup的对象其实本质上也是一个Tag类型。所以其实一些方法比如find、find_all并不是BeautifulSoup的，而是Tag的。
2. NavigableString：继承自python中的str，用起来就跟使用python的str是一样的。
3. BeautifulSoup：继承自Tag。用来生成BeaufifulSoup树的。对于一些查找方法，比如find、select这些，其实还是Tag的。
4. Comment：这个也没什么好说，就是继承自NavigableString。

## contents和children：

返回某个标签下的直接子元素，其中也包括字符串。他们两的区别是：contents返回来的是一个列表，children返回的是一个迭代器。