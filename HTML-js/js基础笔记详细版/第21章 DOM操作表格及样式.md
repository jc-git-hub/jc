**第21章 DOM操作表格及样式**

学习要点：

1.操作表格

2.操作样式

DOM在操作生成HTML上，还是比较简明的。不过，由于浏览器总是存在兼容和陷阱，导致最终的操作就不是那么简单方便了。本章主要了解一下DOM操作表格和样式的一些知识。

一．**操作表格**

<table>标签是HTML中结构最为复杂的一个，我们可以通过DOM来创建生成它，或者HTML DOM来操作它。(PS：HTML DOM提供了更加方便快捷的方式来操作HTML，有手册)。

//需要操作的table

<table border="1" width="300">

​	<caption>人员表</caption>

​	<thead>

​		<tr>

​			<th>姓名</th>

​			<th>性别</th>

​			<th>年龄</th>

​		</tr>

​	</thead>

​	<tbody>

​		<tr>

​			<td>张三</td>

​			<td>男</td>

​			<td>20</td>

​		</tr>

​		<tr>

​			<td>李四</td>

​			<td>女</td>

​			<td>22</td>

​		</tr>

​	</tbody>

​	<tfoot>

​		<tr>

​			<td colspan="3">合计：N</td>

​		</tr>

​	</tfoot>

</table>

//使用DOM来创建这个表格

​	var table = document.createElement('table');

​	table.border = 1;

​	table.width = 300;

​	

​	var caption = document.createElement('caption');

​	table.appendChild(caption);

​	caption.appendChild(document.createTextNode('人员表'));

​	

​	var thead = document.createElement('thead');

​	table.appendChild(thead);

​	var tr = document.createElement('tr');

​	thead.appendChild(tr);

​	

​	var th1 = document.createElement('th');

​	var th2 = document.createElement('th');

​	var th3 = document.createElement('th');

​	

​	tr.appendChild(th1);

​	th1.appendChild(document.createTextNode('姓名'));

​	tr.appendChild(th2);

​	th2.appendChild(document.createTextNode('年龄'));

​	

​	document.body.appendChild(table);

PS：使用DOM来创建表格其实已经没有什么难度，就是有点儿小烦而已。下面我们再使用HTML DOM来获取和创建这个相同的表格。

HTML DOM中，给这些元素标签提供了一些属性和方法

| 属性或方法      | 说明                                  |
| --------------- | ------------------------------------- |
| caption         | 保存着<caption>元素的引用             |
| tBodies         | 保存着<tbody>元素的HTMLCollection集合 |
| tFoot           | 保存着对<tfoot>元素的引用             |
| tHead           | 保存着对<thead>元素的引用             |
| rows            | 保存着对<tr> 元素的HTMLCollection集合 |
| createTHead()   | 创建<thead>元素，并返回引用           |
| createTFoot()   | 创建<tfoot>元素，并返回引用           |
| createCaption() | 创建<caption>元素，并返回引用         |
| deleteTHead()   | 删除<thead>元素                       |
| deleteTFoot()   | 删除<tfoot>元素                       |
| deleteCaption() | 删除<caption>元素                     |
| deleteRow(pos)  | 删除指定的行                          |
| insertRow(pos)  | 向rows集合中的指定位置插入一行        |

<tbody>元素添加的属性和方法

| 属性或方法     | 说明                                       |
| -------------- | ------------------------------------------ |
| rows           | 保存着<tbody>元素中行的HTMLCollection      |
| deleteRow(pos) | 删除指定位置的行                           |
| insertRow(pos) | 向rows集合中的指定位置插入一行，并返回引用 |

<tr>元素添加的属性和方法

| 属性或方法      | 说明                                            |
| --------------- | ----------------------------------------------- |
| cells           | 保存着<tr>元素中单元格的HTMLCollection          |
| deleteCell(pos) | 删除指定位置的单元格                            |
| insertCell(pos) | 向cells集合的指定位置插入一个单元格，并返回引用 |

PS：因为表格较为繁杂，层次也多，在使用之前所学习的DOM只是来获取某个元素会非常难受，所以使用HTML DOM会清晰很多。

//使用HTML DOM来获取表格元素

var table = document.getElementsByTagName('table')[0];	//获取table引用

//按照之前的DOM节点方法获取<caption>

alert(table.children[0].innerHTML);			//获取caption的内容

PS：这里使用了children[0]本身就忽略了空白，如果使用firstChild或者childNodes[0]需要更多的代码。

//按HTML DOM来获取表格的<caption>

alert(table.caption.innerHTML);				//获取caption的内容

//按HTML DOM来获取表头表尾<thead>、<tfoot>

​	alert(table.tHead);							//获取表头

​	alert(table.tFoot);							//获取表尾

//按HTML DOM来获取表体<tbody>

alert(table.tBodies);							//获取表体的集合

PS：在一个表格中<thead>和<tfoot>是唯一的，只能有一个。而<tbody>不是唯一的可以有多个，这样导致最后返回的<thead>和<tfoot>是元素引用，而<tbody>返回的是元素集合。

//按HTML DOM来获取表格的行数

alert(table.rows.length);						//获取行数的集合，数量

//按HTML DOM来获取表格主体里的行数

alert(table.tBodies[0].rows.length);			//获取主体的行数的集合，数量

//按HTML DOM来获取表格主体内第一行的单元格数量(tr)

alert(table.tBodies[0].rows[0].cells.length);		//获取第一行单元格的数量

//按HTML DOM来获取表格主体内第一行第一个单元格的内容(td)

alert(table.tBodies[0].rows[0].cells[0].innerHTML);	//获取第一行第一个单元格的内容

//按HTML DOM来删除标题、表头、表尾、行、单元格

​	table.deleteCaption();						//删除标题

​	table.deleteTHead();						//删除<thead>

​	table.tBodies[0].deleteRow(0);				//删除<tr>一行

​	table.tBodies[0].rows[0].deleteCell(0);			//删除<td>一个单元格

//按HTML DOM创建一个表格

​	var table = document.createElement('table');

​	table.border = 1;

​	table.width = 300;

​	

​	table.createCaption().innerHTML = '人员表';

​	

​	//table.createTHead();

​	//table.tHead.insertRow(0);

​	var thead = table.createTHead();

​	var tr = thead.insertRow(0);

​	

​	var td = tr.insertCell(0);

​	td.appendChild(document.createTextNode('数据'));

​	var td2 = tr.insertCell(1);

​	td2.appendChild(document.createTextNode('数据2'));

​	

​	document.body.appendChild(table);

PS：在创建表格的时候<table>、<tbody>、<th>没有特定的方法，需要使用document来创建。也可以模拟已有的方法编写特定的函数即可，例如：insertTH()之类的。

二．**操作样式**

CSS作为(X)HTML的辅助，可以增强页面的显示效果。但不是每个浏览器都能支持最新的CSS能力。CSS的能力和DOM级别密切相关，所以我们有必要检测当前浏览器支持CSS能力的级别。

DOM1级实现了最基本的文档处理，DOM2和DOM3在这个基础上增加了更多的交互能力，这里我们主要探讨CSS，DOM2增加了CSS编程访问方式和改变CSS样式信息。

DOM一致性检测

| 功能           | 版本号        | 说明                                    |
| -------------- | ------------- | --------------------------------------- |
| Core           | 1.0、2.0、3.0 | 基本的DOM,用于表现文档节点树            |
| XML            | 1.0、2.0、3.0 | Core的XML扩展，添加了对CDATA等支持      |
| HTML           | 1.0、2.0      | XML的HTML扩展，添加了对HTML特有元素支持 |
| Views          | 2.0           | 基于某些样式完成文档的格式化            |
| StyleSheets    | 2.0           | 将样式表关联到文档                      |
| CSS            | 2.0           | 对层叠样式表1级的支持                   |
| CSS2           | 2.0           | 对层叠样式表2级的支持                   |
| Events         | 2.0           | 常规的DOM事件                           |
| UIEvents       | 2.0           | 用户界面事件                            |
| MouseEvents    | 2.0           | 由鼠标引发的事件(如：click)             |
| MutationEvents | 2.0           | DOM树变化时引发的事件                   |
| HTMLEvents     | 2.0           | HTML4.01事件                            |
| Range          | 2.0           | 用于操作DOM树中某个范围的对象和方法     |
| Traversal      | 2.0           | 遍历DOM树的方法                         |
| LS             | 3.0           | 文件与DOM树之间的同步加载和保存         |
| LS-Async       | 3.0           | 文件与DOM树之间的异步加载和保存         |
| Valuidation    | 3.0           | 在确保有效的前提下修改DOM树的方法       |

//检测浏览器是否支持DOM1级CSS能力或DOM2级CSS能力

alert('DOM1级CSS能力：' + document.implementation.hasFeature('CSS', '2.0'));

alert('DOM2级CSS能力：' + document.implementation.hasFeature('CSS2', '2.0'));

PS：这种检测方案在IE浏览器上不精确，IE6中，hasFeature()方法只为HTML和版本1.0返回true，其他所有功能均返回false。但IE浏览器还是支持最常用的CSS2模块。

1.访问元素的样式

任何HTML元素标签都会有一个通用的属性：style。它会返回CSSStypeDeclaration对象。下面我们看几个最常见的行内style样式的访问方式。

CSS属性及JavaScript调用

| CSS属性   | JavaScript调用       |
| --------- | -------------------- |
| color     | style.color          |
| font-size | style.fontSize       |
| float     | 非IE：style.cssFloat |
| float     | IE：style.styleFloat |

var box = document.getElementById('box');		//获取box

box.style.cssFloat.style;						//CSSStyleDeclaration

box.style.cssFloat.style.color;					//red

box.style.cssFloat.style.fontSize;				//20px

box.style.cssFloat || box.style.styleFloat;		//left，非IE用cssFloat，IE用styleFloat

PS：以上取值方式也可以赋值，最后一种赋值可以如下：

typeof box.style.cssFloat != 'undefined' ? 

box.style.cssFloat = 'right' : box.style.styleFloat = 'right';

DOM2级样式规范为style定义了一些属性和方法

| 属性或方法                | 说明                                           |
| ------------------------- | ---------------------------------------------- |
| cssText                   | 访问或设置style中的CSS代码                     |
| length                    | CSS属性的数量                                  |
| parentRule                | CSS信息的CSSRule对象                           |
| getPropertyCSSValue(name) | 返回包含给定属性值的CSSValue对象               |
| getPropertyPriority(name) | 如果设置了!important，则返回，否则返回空字符串 |
| item(index)               | 返回指定位置CSS属性名称                        |
| removeProperty(name)      | 从样式中删除指定属性                           |
| setProperty(name,v,p)     | 给属性设置为相应的值，并加上优先权             |

box.style.cssText;							//获取CSS代码

//box.style.length;							//3，IE不支持

//box.style.removeProperty('color');			//移除某个CSS属性，IE不支持

//box.style.setProperty('color','blue');			//设置某个CSS属性，IE不支持

PS：Firefox、Safari、Opera9+、Chrome支持这些属性和方法。IE只支持cssText，而getPropertyCSSValue()方法只有Safari3+和Chrome支持。

PS：style属性仅仅只能获取行内的CSS样式，对于另外两种形式内联<style>和链接<link>方式则无法获取到。

虽然可以通过style来获取单一值的CSS样式，但对于复合值的样式信息，就需要通过计算样式来获取。DOM2级样式，window对象下提供了getComputedStyle()方法。接受两个参数，需要计算的样式元素，第二个伪类(:hover)，如果没有没有伪类，就填null。

PS：IE不支持这个DOM2级的方法，但有个类似的属性可以使用currentStyle属性。

​	var box = document.getElementById('box');

var style = window.getComputedStyle ?

 window.getComputedStyle(box, null) : null || box.currentStyle;

​	alert(style .color);							//颜色在不同的浏览器会有rgb()格式

​	alert(style .border);							//不同浏览器不同的结果

​	alert(style .fontFamily);						//计算显示复合的样式值

​	alert(box.style.fontFamily);					//空

PS：border属性是一个综合属性，所以他在Chrome显示了，Firefox为空，IE为undefined。所谓综合性属性，就是XHTML课程里所的简写形式，所以，DOM在获取CSS的时候，最好采用完整写法兼容性最好，比如：border-top-color之类的。

2.操作样式表

使用style属性可以设置行内的CSS样式，而通过id和class调用是最常用的方法。

box.id = 'pox';								//把ID改变会带来灾难性的问题

box.className = 'red';						//通过className关键字来设置样式

在添加className的时候，我们想给一个元素添加多个class是没有办法的，后面一个必将覆盖掉前面一个，所以必须来写个函数：

//判断是否存在这个class

function hasClass(element, className) {  

​	return element.className.match(new RegExp('(\\s|^)'+className+'(\\s|$)'));

}

//添加一个class，如果不存在的话

function addClass(element, className) {

​	if (!hasClass(element, className))   {       

​		element.className += " "+className;  

​	}

}

//删除一个class，如果存在的话

function removeClass(element, className) {   

​	if (hasClass(element, className)) {         

​		element.className = element.className.replace(

new RegExp('(\\s|^)'+className+'(\\s|$)'),' ');   

​	}

}  

之前我们使用style属性，仅仅只能获取和设置行内的样式，如果是通过内联<style>或链接<link>提供的样式规则就无可奈何了，然后我们又学习了getComputedStyle和currentStyle，这只能获取却无法设置。

CSSStyleSheet类型表示通过<link>元素和<style>元素包含的样式表。

document.implementation.hasFeature('StyleSheets', '2.0')	//是否支持DOM2级样式表

​	document.getElementsByTagName('link')[0];	//HTMLLinkElement

​	document.getElementsByTagName('style')[0];	//HTMLStyleElement

这两个元素本身返回的是HTMLLinkElement和HTMLStyleElement类型，但CSSStyleSheet类型更加通用一些。得到这个类型非IE使用sheet属性，IE使用styleSheet；

​	var link = document.getElementsByTagName('link')[0];

var sheet = link.sheet || link.styleSheet;			//得到CSSStyleSheet

| 属性或方法              | 说明                                              |
| ----------------------- | ------------------------------------------------- |
| disabled                | 获取和设置样式表是否被禁用                        |
| href                    | 如果是通过<link>包含的，则样式表为URL，否则为null |
| media                   | 样式表支持的所有媒体类型的集合                    |
| ownerNode               | 指向拥有当前样式表节点的指针                      |
| parentStyleSheet        | @import导入的情况下，得到父CSS对象                |
| title                   | ownerNode中title属性的值                          |
| type                    | 样式表类型字符串                                  |
| cssRules                | 样式表包含样式规则的集合，IE不支持                |
| ownerRule               | @import导入的情况下，指向表示导入的规则，IE不支持 |
| deleteRule(index)       | 删除cssRules集合中指定位置的规则，IE不支持        |
| insertRule(rule, index) | 向cssRules集合中指定位置插入rule字符串，IE不支持  |

sheet.disabled;								//false，可设置为true

sheet.href;								//css的URL

sheet.media;								//MediaList，集合

sheet.media[0];							//第一个media的值

sheet.title;								//得到title属性的值

sheet.cssRules								//CSSRuleList，样式表规则集合

sheet.deleteRule(0);						//删除第一个样式规则

sheet.insertRule("body {background-color:red}", 0);	//在第一个位置添加一个样式规则

PS：除了几个不用和IE不支持的我们忽略了，还有三个有IE对应的另一种方式：

sheet.rules;								//代替cssRules的IE版本

sheet.removeRule(0);						//代替deleteRule的IE版本

sheet.addRule("body", "background-color:red", 0);//代替insertRule的IE版本

除了刚才的方法可以得到CSSStyleSheet类型，还有一种方法是通过document的styleSheets属性来获取。

document.styleSheets;						//StyleSheetList，集合

var sheet = document.styleSheets[0];			//CSSStyleSheet，第一个样式表对象

为了添加CSS规则，并且兼容所有浏览器，我们必须写一个函数：

​	var sheet = document.styleSheets[0];

​	insertRule(sheet, "body", "background-color:red;", 0);

function insertRule(sheet, selectorText, cssText, position) {

//如果是非IE

​	if (sheet.insertRule) {

​		sheet.insertRule(selectorText + "{" + cssText + "}", position);

//如果是IE

​	} else if (sheet.addRule) {

​		sheet.addRule(selectorText, cssText, position);

​	}

}

为了删除CSS规则，并且兼容所有浏览器，我们必须写一个函数：

var sheet = document.styleSheets[0];

deleteRule(sheet, 0);

function deleteRule(sheet, index) {

//如果是非IE

​	if (sheet.deleteRule) {

​		sheet.deleteRule(index);

//如果是IE

​	} else if (sheet.removeRule) {

​		sheet.removeRule(index);

​	}

}

通过CSSRules属性(非IE)和rules属性(IE)，我们可以获得样式表的规则集合列表。这样我们就可以对每个样式进行具体的操作了。

​	var sheet = document.styleSheets[0];			//CSSStyleSheet

​	var rules = sheet.cssRules || sheet.rules;			//CSSRuleList，样式表的规则集合列表

​	var rule = rules[0];							//CSSStyleRule，样式表第一个规则

CSSStyleRule可以使用的属性

| 属性             | 说明                                             |
| ---------------- | ------------------------------------------------ |
| cssText          | 获取当前整条规则对应的文本，IE不支持             |
| parentRule       | @import导入的，返回规则或null，IE不支持          |
| parentStyleSheet | 当前规则的样式表，IE不支持                       |
| selectorText     | 获取当前规则的选择符文本                         |
| style            | 返回CSSStyleDeclaration 对象，可以获取和设置样式 |
| type             | 表示规则的常量值，对于样式规则，值为1，IE不支持  |

rule.cssText;								//当前规则的样式文本

rule.selectorText;							//#box，样式的选择符

rule.style.color;							//red，得到具体样式值

PS：Chrome浏览器在本地运行时会出现问题，rules会变成null，只要把它放到服务器上允许即可正常。

总结：三种操作CSS的方法，第一种style行内，可读可写；第二种行内、内联和链接，使用getComputedStyle或currentStyle，可读不可写；第三种cssRules或rules，内联和链接可读可写。