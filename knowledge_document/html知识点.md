# HTML(HyperText Markup Language)

#### 前言

#### 软件架构

##### B/S

​	Browser/Server   网站

##### C/S

​	Client/Server	       QQ

##### HTML的简介、发展史：

万维网联盟（W3C）维护。包含HTML内容的文件最常用的扩展名是.html，但是像DOS这样的旧操作系统限制扩展名为最多3个字符，所以.htm扩展名也被使用。虽然现在使用的比较少一些了，但是.htm扩展名仍旧普遍被支持。

##### 相关历程：

* 超文本标记语言(第一版) -- 在1993年6月发为互联网工程工作小组(IETF)工作草案发布(并非标准)

* HTML 2.0 -- 1995年11月作为RFC 1866发布,在RFC 2854于2000年6月发布之后被宣布已经过时

* HTML 3.2 -- 1996年1月14日,W3C推荐标准

* HTML 4.0 -- 1997年12月18日,W3C推荐标准

* HTML 4.01(微小改进) -- 1999年12月24日,W3C推荐标准

* ISO/IEC 15445:2000("ISO HTML")--2000年5月15日发布,基于严格的HTML4.01语法,是国际标准化组织和国际电工委员会的标准

* XHTML 1.0 -- 发布于2000年1月26日,是W3C推荐标准,后来经过修订于2002年8月1日重新发布

* XHTML 1.1 -- 于2001年5月31日发布

* XHTML 2.0
  * XHTML 1.0 -- 发布于2000年1月26日,是W3C推荐标准,后来经过修订于2002年8月1日重新发布

* XHTML -- W3C工作草案


**网站：**

把所有的网站资源文件（HTML,CSS,JS,图片,视频等）整合到一起(的一个文件夹)

**编程语言**：解释型和编译型

解释型：HTML、PHP、Javascript，Python

编译型语言：C、C++、Java

**WEB前端**：HTML+CSS+JavaScript

**HTML5:**

HTML5+CSS3+Api+JavaScript

## 一 什么是HTML？

##### 	超文本标记语言

​	(1) 标签 也叫做 标记

​	(2) html是由标签/标记 和内容组成的

​	(3) 标签 是由 标签名称 和属性组成的

**实例：**

> <人 肤色=“黄色” 眼镜="很大"></人>

**扩展：**

使用协议为  http超文本传输协议

普通文本：文字内容

超文本：视频、音频、图片、文字...

## 二 HTML的主体标签

**实例**

```html
<!DOCTYPE html>  #H5的头   声明文档类型 为html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/TDT/xhtml1-strit.dtd">  #之前的头文件 现在不用
<html>
<head>
	<title>标题内容</title>
  	<meta charset="UTF-8"> #设置字符集
</head>
<body>
  	放html的主体标签
</body>
</html>
```

- html:文件是网页，浏览器加载网页，就可以浏览 
- head:头部分，网页总体信息 
  + title:网页标题
  + meta：网页主体信息，会根据name(author/description/keywords)或者httq-equiv(content-type/expires/refresh)属性的不同，而设置网页的不同属性
  + link:引入外部文件和C#中的using异曲同工
  + style：写入CSS
  + script：写入JS
- body:身体部分，网页内容

## 三 HTML的标签

##### 标签分为：单标签/单标记 

如：\<br /> /\<br >

##### 		    双标签/双标记  

如: \<p>\</p>

#### (1) 文本标签

1. `<p></p>   `		段落标签  自成一段  会将上下的文字 和它保持一定的距离

2. `<br />   `     单标记  自闭合  换行

3. `<i></i> /<em></em> `    斜体/强调斜体

4. `<b></b>/<strong></strong> `加粗/强调加粗

5. `<h1>-</h6> `标题标签 字体加粗 自占一行

   **注意：** 建议一个页面h1只能出现一次

6. `<sub></sub>/<sup></sup>` 下标/上标

7. `<hr />`水平分割线

8. `<u></u> `下划线

9. `<del></del> `删除线

10. `<font size="1-7" color="颜色" face="字体"></font>`   设置字得大小 颜色 字体

11. `<span></span>`   无意义得行级标签

    行级：可以和我们的内容在一行来显示 不能设置宽高

    块级：自占一行 可以设置宽高

#### (2) 图片标签

`<img />` 在网页中插入一张图片

**属性：**

+ src： 图片名及url地址 (必须属性)
+ alt: 图片加载失败时的提示信息
+ title：文字提示属性
+ width：图片宽度
+ height：图片高度
+ border：边框线粗细

**实例:**

```html
<img src="图片地址" title="文字提示" alt="图片加载失败显示得信息" width="宽" height="高" border="边框" />
```

**注意：**

如果宽和高 只给一个 那么为等比缩放  如果俩个都给 那么会按照 你所给的宽和高来显示

#### (3) 路径

1. 相对路径
   + ./	当前
   + ../     上一级
2. 绝对路径
   + 一个固定得链接地址(如域名)
   + 从根磁盘 一直到你的文件得路径

     file协议  打开本地磁盘文件得协议（试一下火狐）

#### (4) 超链接

1. \<a href="链接地址" title="提示信息" target="打开方式">点击显示得内容\</a>

   **属性：**

   href必须，指的是链接跳转地址

   **target:** 

   ​		_blank 新建窗口得形式来打开

   ​	   	 _self      本窗口来打开

   ​           	 _parent  父窗口来打开

   ​           	 _top        顶级窗口来打开

   ​	  	 framename 分帧名来打开

   **title：**文字提示属性（详情）

2. 锚点

   1. 定义锚点  \<a id="锚点名称”>\</a>  现在使用id  以前使用得都是 name
   2. 使用锚点  \<a href="#锚点名">\</a>

#### (5) 列表

1. ##### 无序列表*

   ```html
   <ul>
   	<li></li>  
   </ul>
   <!--
   属性：
   	type 显示得类型
   	square 方形显示
   	disc 默认圆点
   	circle 空心圆
   -->
   ```

2. ##### 有序列表

   ```html
   <ol>
    	<li></li>
   </ol>
   <!--
   属性 
   	type i a A 1 
   	start 起始值

   -->
   ```

3. ##### 自定义列表

   ```html
   <dl>
     	<dt>列表头</dt>
     	<dd>列表内容</dd>
   </dl>
   ```


#### (6) HTML注释

多行注释：<!--注释的内容-->

注释的作用：

1. 代码的调试
2. 解释说明

#### (7) 常用实体化符号标签

##### HTML 中有用的字符实体

注释：实体名称对大小写敏感！

| 显示结果 | 描述            | 实体名称           |
| ---- | ------------- | -------------- |
|      | 空格            | `&nbsp;`       |
| <    | 小于号           | `&lt;`         |
| >    | 大于号           | `&gt;`         |
| &    | 和号            | &amp;          |
| "    | 引号            | &quot;         |
| '    | 撇号            | &apos; (IE不支持) |
| ￠    | 分（cent）       | &cent;         |
| £    | 镑（pound）      | &pound;        |
| ¥    | 元（yen）        | &yen;          |
| €    | 欧元（euro）      | &euro;         |
| §    | 小节            | &sect;         |
| ©    | 版权（copyright） | &copy;         |
| ®    | 注册商标          | &reg;          |
| ™    | 商标            | &trade;        |
| ×    | 乘号            | &times;        |
| ÷    | 除号            | &divide;       |

## 四 分帧

frameset

##### 定义和用法

frameset 元素可定义一个框架集。它被用来组织多个窗口（框架）。每个框架存有独立的文档。在其最简单的应用中，frameset 元素仅仅会规定在框架集中存在多少列或多少行。您必须使用 cols 或 rows 属性。

##### 可选的属性

| 属性          | 值          | 描述            |
| ----------- | ---------- | ------------- |
| cols        | pixels % * | 定义框架集中列的数目和尺寸 |
| rows        | pixels % * | 定义框架集中行的数目和尺寸 |
| frameborder | 1/0        | 是否显示边框        |
| name        |            | 给当前分帧窗口起名称    |
| src         |            | 连接的页面名称       |
| noresize    | noresize   | 页面不会被拖拽       |

**实例**

```html
<frameset rows="20%,*,20%" frameborder="1/0">
  <frame src="" name="分帧名1">
  <frameset cols="20%,*" frameborder="1/0">
    <frame src="" name="分帧名1">
    <frame src="" name="分帧名2">
  </frameset>
  <frame src="" name="分帧名3">
</frameset>
```

**注意：**

不可以和body在一起  需要将body删掉



   ## 五 TABLE表格

**table表格**

**属性：**

+ width 宽
+ height 高
+ border 边框
+ cellpadding/cellspacing  内边距/外边距
+ background 背景图片
+ bgcolor颜色
+ align位置 center/left/right
+ valign规定单元格内容的垂直排列方式。
  + top 对内容进行上对齐。
  + middle  对内容进行居中对齐（默认值）。
  + bottom  对内容进行下对齐。
  + baseline 与基线对齐。
+ rowspan合并行
+ colspan合并列

**标签：**

caption 表格标题

*tr	行标签

*th  列头标签
*td  列标签

**实例：**

   ```html
<table>
  <caption>我是表格的标题</caption>
  <tr>
    <th>我是表头</th>
    <th>我是表头</th>
    <th>我是表头</th>
  </tr>
  <tr>
    <td>我是单元格</td>
    <td>我是单元格</td>
    <td>我是单元格</td>
  </tr>
</table>
   ```

**细线表格实例：**

```html
<table border="0" cellspacing="1" bgcolor="red"  width="80%">
  <tr bgcolor="#ffffff">
    <td>1.1</td>
    <td>1.2</td>
  </tr>
  <tr bgcolor="#ffffff">
    <td>2.1</td>
    <td>2.2</td>
  </tr>
</table>
```



   ## 六 FORM表单

**标签：** `<form></form>`

#### (1) **form属性**

   	action	提交的地址
   	method	提交的方式
   		get
   			(1) 默认不写 为get传参  url地址栏可见
   			(2) 长度受限制 （IE浏览器2k火狐8k）
   			(3) 相对不安全
   		post
   			(1) url地址栏不可见 长度默认不受限制
   			(2) 相对安全
   	enctype 提交的类型
   		enctype属性 在表单有文件上传的时候 需要设置值 值为multipart/form-data

#### (2) input 标签

`<input>` 表单项标签input定义输入字段，用户可在其中输入数据。在 HTML 5 中，type 属性有很多新的值。

具体在下面有详解：

**如：**

`<input type="text" name="username">`

#### (3)  select 标签创建下拉列表。

**属性：**

+ *name属性:定义名称,用于存储下拉值的
+ size：定义菜单中可见项目的数目，html5不支持
+ disabled 当该属性为 true 时，会禁用该菜单。
+ multiple 多选


##### **内嵌标签：**

*`<option>`  下拉选择项标签,用于嵌入到<select>标签中使用的;

##### 属性：

+ *value属性:下拉项的值

+ *selected属性:默认下拉指定项.

#### (4) *textarea 多行的文本输入区域

**属性：**

+ \* name :定义名称,用于存储文本区域中的值。

+ \*cols ：规定文本区内可见的列数。hlc

+ \*rows ：规定文本区内可见的行数。

+ disabled： 是否禁用

+ readonly： 只读

+ placeholder 提示信息

   **注意：**
   默认值是在两个标签之间

#### (5) *button 标签定义按钮。

您可以在 button 元素中放置内容，比如文档或图像。这是该元素与由 input 元素创建的按钮的不同之处。

##### type:

+ submit 默认为submit
+ button 点击
+ reset 重置

#### (6) fieldset html5标签--fieldset 元素可将表单内的相关元素分组。

**disabled属性：**定义 fieldset 是否可见。
**form属性：** 定义该 fieldset 所属的一个或多个表单。

#### (7) legend html5标签

<legend> html5标签--<legend> 标签为 <fieldset>b<figure> 以及 <details> 元素定义标题。

**实例：**

   ```html
<form>     
  <fieldset>
    <legend>健康信息：</legend>
    身高：<input type="text" /><br/>
    体重：<input type="text" /><br/>
  </fieldset>
</form>
   ```

#### (8)  optgroup html5标签

<optgroup> html5标签--<optgroup> 标签定义选项组。此元素允许您组合选项

##### 实例：

 ```html
 <select>
   <optgroup label="Swedish Cars">
 	<option vanlue="volvo">Volvo</option>
 	<option value="saab">Saab</option>
   </optgroup>
   <optgroup label="German Cars">
 	<option value="mercedes">Mercedes</option>
 	<option value="audi">Audi</option>
   </optgroup>
 </select>
 ```

#### (9) datalist html5标签

<datalist> html5标签--<datalist> 标签定义可选数据的列表。与 input 元素配合使用，就可以制作出输入值的下拉列表。
**实例：**

```html
<form action="demo_form.php" method="get">
  <input list="browsers" name="browser">
  <datalist id="browsers">
  <option value="Internet Explorer">
  <option value="Firefox">
  <option value="Chrome">
  <option value="Opera">
  <option value="Safari">
  </datalist>
  <input type="submit">
</form>
```
#### (10) input 标签

**搭配label标签使用**

label 		可以使标签内的区域指向label标签for属性指代的对象的事件。

**实例：**

```html
<label for="male">Male</label>
<input type="radio" name="sex" id="male" />
```

***type属性:表示表单项的类型:**

**值如下:**

+ text:单行文本框

+ password:密码输入框

+ checkbox:多选框 注意要提供value值

+ radio:单选框   注意要提供value值

+ file:文件上传选择框

+ button:普通按钮

+ submit:提交按钮

+ image:图片提交按钮

  `<input type=“image” width=“100” height=“100”border=“2”src=“上传图片”/>`

+ reset:重置按钮, 还原到开始(第一次打开时)的效果

+ hidden:表单隐藏域,是要和表单一块提交的信息,但是不需要用户修改

***name属性: ** 表单项名,用于存储内容值的
***value属性: **  输入的值(默认指定值)
**size属性: ** 输入框的宽度值
**maxlength属性**:  输入框的输入内容的最大长度

**minlength属性：** 输入框的输入内容的最小长度

**readonly属性: ** 对输入框只读属性
***disabled属性:  **禁用属性

readonly 数据还是会提交给服务器端 disabled 将数据作废掉 不会再传递给服务器端

***checked属性: ** 对选择框指定默认选项
**placeholder**   提示信息

***required** 必填属性

src和alt是为图片按钮设置的

注意：reset重置按钮是将表单数据恢复到第一次打开时的状态，并不是清空

image图片按钮，默认具有提交表单功能。

#### (11) 作为了解的input h5的新属性

**type属性：**

+ time   时间
+ date  日期
+ range  区间
+ email  邮箱
+ url  url地址
+ color  颜色
+ number  数值
+ search  搜索



## 七、HTML中HEAD头部设置

设置网页编码：

> `<meta charset="utf-8"/>`

自动刷新：

> `<meta http-equiv="refresh" content="时间;url=网址" />`

关键字：

> `<meta name="Keywords" content="关键字" />`

描述：  

> `<meta name="Description" content="简介、描述" />`

站点作者:

> `<meta name="author" content="root,root@xxxx.com">`告诉搜索引擎你的站点的制作的作者；

网页标题：

> `<title>本网页标题</title>`

导入CSS文件：

> `<link type="text/css" rel="stylesheet" href="**.css"/>`

CSS代码：

> `<style type="text/css">嵌入css样式代码</style>`

JS文件或代码： 

> `<script >。。。</script>`

设置网页小图标:

> `<link rel="icon" href="/favicon.ico" type="image/x-icon" />`

**注意：**

头标签中的内容不会显示在浏览器中



八、 HTML5多媒体标签（熟悉）
------------------------------------

#### (1) audio 音频

HTML5 中的新属性。

| 属性       | 值        | 描述                                       |
| -------- | -------- | ---------------------------------------- |
| autoplay | autoplay | 如果出现该属性，则音频在就绪后马上播放。                     |
| controls | controls | 如果出现该属性，则向用户显示控件，比如播放按钮。                 |
| loop     | loop     | 如果出现该属性，则每当音频结束时重新开始播放。                  |
| muted    | muted    | 规定视频输出应该被静音。                             |
| preload  | preload  | 如果出现该属性，则音频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| src      | *url*    | 要播放的音频的 URL。                             |

方式一

**实例：**

```html
<audio src="./images/beidahuang.mp3" controls="controls">
		你的浏览器不支持播放
</audio>
```

方式二

##### 实例:

```html
<audio controls="controls">
  <source src="./images/beidahuang.mp3" type="audio/mpeg" />
  你的浏览器不支持播放
</audio>
```

#### (2) video 视频

 HTML5 中的新属性。

| 属性       | 值        | 描述                                       |
| -------- | -------- | ---------------------------------------- |
| autoplay | autoplay | 如果出现该属性，则视频在就绪后马上播放。                     |
| controls | controls | 如果出现该属性，则向用户显示控件，比如播放按钮。                 |
| height   | *pixels* | 设置视频播放器的高度。                              |
| loop     | loop     | 如果出现该属性，则当媒介文件完成播放后再次开始播放。               |
| muted    | muted    | 规定视频的音频输出应该被静音。                          |
| poster   | *URL*    | 规定视频下载时显示的图像，或者在用户点击播放按钮前显示的图像。          |
| preload  | preload  | 如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| src      | *url*    | 要播放的视频的 URL。                             |
| width    | *pixels* | 设置视频播放器的宽度。                              |

方式一

##### 实例：

```html
<video src="res/happy.mp4" controls poster="res/glnz.jpeg" width="200" height="300" loop>
    您的浏览器不支持播放 请更换浏览器在此播放
</video>
```
方式二

##### 实例:

```html
<video  controls loop poster="tiao.jpg">
	<source src="movie.webm" type="video/webm">
	<source src="movie.ogg" type="video/ogg">
	<source src="movie.mp4" type="video/mp4">
	您的破浏览器该扔了，不支持视频标签
</video>
```