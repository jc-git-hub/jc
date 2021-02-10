# Excel文件处理

 

在爬虫开发中，我们主要关注`Excel`文件的读写，不会过多关心`Excel`中的一些样式。如果想要读写`Excel`文件，需要借助到两个库`xlrd`和`xlwt`，其中`xlrd`是用于读的，`xlwt`是用于写的，安装命令如下：

 

```
pip install xlrd
pip install xlwt
```

 

## 读取Excel文件：

 

```python
import xlrd

workbook = xlrd.open_workbook("成绩表.xlsx")
sheet_names = workbook.sheet_names()
print(sheet_names) #打印所有的sheet的名称
```

 

### 获取`Sheet`：

 

一个`Excel`中可能有多个`Sheet`，那么可以通过以下方法来获取想要的`Sheet`信息：

 

1. `sheet_names`：获取所有的`sheet`的名字。
2. `sheet_by_index`：根据索引获取`sheet`对象。
3. `sheet_by_name`：根据名字获取`sheet`对象。
4. `sheets`：获取所有的`sheet`对象。
5. `sheet.nrows`：这个`sheet`中的行数。
6. `sheet.ncols`：这个`sheet`中的列数。

 

示例代码如下：

 

```python
import xlrd

workbook = xlrd.open_workbook("成绩表.xlsx")
sheet_names = workbook.sheet_names()
print(sheet_names) #打印所有的sheet的名称

# 根据索引获取sheet
sheet = workbook.sheet_by_index(0)
print(sheet.name)

# 根据名称获取sheet
sheet = workbook.sheet_by_name("1班成绩")
print(sheet.name)

# 获取所有的sheet对象
sheets = workbook.sheets()
for sheet in sheets:
    print(sheet.name)

# 获取这个sheet中的行数和列数
nrows = sheet.nrows
ncols = sheet.ncols
```

 

### 获取Cell及其属性：

 

每个`Cell`代表的是表格中的一格。以下方法可以方便获取想要的`cell`：

 

1. `sheet.cell(row,col)`：获取指定行和列的`cell`对象。
2. `sheet.row_slice(row,start_col,end_col)`：获取指定行的某几列的cell对象。
3. `sheet.col_slice(col,start_row,end_row)`：获取指定列的某几行的cell对象。
4. `sheet.cell_value(row,col)`：获取指定行和列的值。
5. `sheet.row_values(row,start_col,end_col)`：获取指定行的某几列的值。
6. `sheet.col_values(col,start_row,end_row)`：获取指定列的某几行的值。

 

示例代码如下：

 

```python
sheet = workbook.sheet_by_index(0)

# 使用cell方法获取指定的cell对象
for col in range(sheet.ncols):
    for row in range(sheet.nrows):
        print(sheet.cell(row,col))

# 使用row_slice获取第0行的1-2列的cell对象
cells = sheet.row_slice(0,1,3)
# 使用col_slice获取第0列的1-2行的cell对象
cells = sheet.col_slice(0,1,3)
```

 

另外在`Cell`上面也有一些常用的属性：

 

1. `cell.value`：这个`cell`里面的值。
2. `cell.ctype`：这个`cell`的数据类型。

 

### Cell的数据类型：

 

1. `xlrd.XL_CELL_TEXT（Text）`：文本类型。
2. `xlrd.XL_CELL_NUMBER（Number）`：数值类型。
3. `xlrd.XL_CELL_DATE（Date）`：日期时间类型。
4. `xlrd.XL_CELL_BOOLEAN（Bool）`：布尔类型。
5. `xlrd.XL_CELL_BLANK`：空白数据类型。

 

------

 

## 写入Excel：

 

写入`Excel`步骤如下：

 

1. 导入`xlwt`模块。
2. 创建一个`Workbook`对象。
3. 创建一个`Sheet`对象。
4. 使用`sheet.write(row,col,data)`方法把数据写入到`Sheet`下指定行和列中。如果想要在原来`workbook`对象上添加新的`cell`，那么需要调用`put_cell`来添加。
5. 保存成`Excel`文件。

 

示例代码如下：

 

```python
import xlwt
import random

workbook = xlwt.Workbook(encoding='utf-8')
sheet = workbook.add_sheet("成绩表")
# 添加表头
fields = ['数学','英语','语文']
for index,field in enumerate(fields):
    sheet.write(0,index,field)

# 随机的添加成绩
for row in range(1,10):
    for col in range(3):
        grade = random.randint(0,100)
        sheet.write(row,col,grade)

workbook.save("abc.xls")
```

 

另外，如果想要在原来已经存在的`Excel`文件中添加新的行或者新的列，那么需要采用`put_cell(row,col,type,value,xf_index)`来添加进去，最后再放到`xlwt`创建的`workbook`中，然后再保存进去。示例代码如下：

 

```python
import xlrd
import xlwt

workbook = xlrd.open_workbook("成绩表.xlsx")
rsheet = workbook.sheet_by_index(0)

# 添加总分成绩
rsheet.put_cell(0,4,xlrd.XL_CELL_TEXT,"总分",None)
for row in range(1,rsheet.nrows):
    grade = sum(rsheet.row_values(row,1,4))
    rsheet.put_cell(row,4,xlrd.XL_CELL_NUMBER,grade,None)

# 添加每个科目的平均成绩
total_rows = rsheet.nrows
total_cols = rsheet.ncols
for col in range(1,total_cols):
    grades = rsheet.col_values(col,1,total_rows)
    avg_grade = sum(grades)/len(grades)
    print(type(avg_grade))
    rsheet.put_cell(total_rows,col,xlrd.XL_CELL_NUMBER,avg_grade,None)

# 重新写入一个新的excel文件数据
wwb = xlwt.Workbook(encoding="utf-8")
wsheet = wwb.add_sheet("1班学生成绩")
for row in range(rsheet.nrows):
    for col in range(rsheet.ncols):
        wsheet.write(row,col,rsheet.cell_value(row,col))

wwb.save("abc.xls")
```