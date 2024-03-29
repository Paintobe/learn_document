========================

##  CSS层叠样式表

========================

##### 什么是css？

层叠样式表

##### 命名规则：

使用字母、数字或下划线和减号构成，不要以数字开头

##### CSS 概述

- CSS 指层叠样式表 (*C*ascading *S*tyle *S*heets)
- 样式定义*如何显示* HTML 元素
- 样式通常存储在*样式表*中
- 把样式添加到 HTML 4.0 中，是为了*解决内容与表现分离的问题*
- *外部样式表*可以极大提高工作效率
- 外部样式表通常存储在 *CSS 文件*中
- 多个样式定义可*层叠*为一

##### 样式解决了一个普遍的问题

HTML 标签原本被设计为用于定义文档内容。通过使用 `<h1>、<p>、<table> `这样的标签，HTML 的初衷是表达“这是标题”、“这是段落”、“这是表格”之类的信息。同时文档布局由浏览器来完成，而不使用任何的格式化标签。

由于两种主要的浏览器（Netscape 和 Internet Explorer）不断地将新的 HTML 标签和属性（比如字体标签和颜色属性）添加到 HTML 规范中，创建文档内容清晰地独立于文档表现层的站点变得越来越困难。

为了解决这个问题，万维网联盟（W3C），这个非营利的标准化联盟，肩负起了 HTML 标准化的使命，并在 HTML 4.0 之外创造出样式（Style）。

所有的主流浏览器均支持层叠样式表。

##### 多重样式将层叠为一个

样式表允许以多种方式规定样式信息。样式可以规定在单个的 HTML 元素中，在 HTML 页的头元素中，或在一个外部的 CSS 文件中。甚至可以在同一个 HTML 文档内部引用多个外部样式表。

##### 层叠次序

**当同一个 HTML 元素被不止一个样式定义时，会使用哪个样式呢？**

一般而言，所有的样式会根据下面的规则层叠于一个新的虚拟样式表中，其中数字 4 拥有最高的优先权。

1. 浏览器缺省设置
2. 外部样式表
3. 内部样式表（位于 <head> 标签内部）
4. 内联样式（在 HTML 元素内部）

因此，内联样式（在 HTML 元素内部）拥有最高的优先权，这意味着它将优先于以下的样式声明：<head> 标签中的样式声明，外部样式表中的样式声明，或者浏览器中的样式声明（缺省值）。

一、css的语法
-----------------------------
##### 格式： 

选择器{属性:值;属性:值;属性:值;....}

##### 其中选择器也叫选择符

##### CSS中注释：


```css
/* ... */
```
## 二、在HTML中如何使用css样式（html中嵌入css的方式）

----------------------------------------------------

1. #### 内联方式（行内样式）

   就是在HTML的标签中使用style属性来设置css样式
    格式： 
    ```
    <html标签 style="属性:值;属性:值;....">被修饰的内容</html标签>  
    <p style="color:blue;font-family:隶书">在HTML中如何使用css样式</p>
    ```

    特点：仅作用于本标签


2. #### 内部方式（内嵌样式）

   就是在head标签中使用`<style type="text/css">....</style>`标签来设置css样式
    格式：

   ```python
    <style type="text/css">
    	....css样式代码
    </style>
   ```

    **特点：**作用于当前整个页面
3. #### 外部导入方式（外部链入）

   ##### 3.1 （推荐）就是在head标签中使用<link/>标签导入一个css文件，在作用于本页面，实现css样式设置

    格式：

   ```Css
   <link href="文件名.css" type="text/css" rel="stylesheet"/>
   ```

   #####  3.2 还可以使用import在style标签中导入css文件。

   格式:

   ```css
   <style type="text/css">
   	@import "文件名.css"
   </style>
   ```

    特点：作用于整个网站

   #####  俩种导入方式的区别:

   1.  link属于html，而@import则属于css

   2. @import 不能写在内嵌样式的上方 否则样式无效

      **格式：**

      ```css
      不生效
       <style type="text/css">
       	div{
       		width:200px;
       	}
       	@import '1.css'
       </style>
       下面的写法生效
       <style type="text/css">
       div{
       	width:200px;
       }
       </style>
       <style type="text/css">
       	@import '1.css'
       </style>
      ```

   3. 加载顺序区别

      加载页面时，link标签引入的 CSS 被同时加载；@import引入的 CSS 将在页面加载完毕后被加载。

   4. 兼容性区别

       @import是 CSS2.1 才有的语法，故只可在 IE5+ 才能识别；link标签作为 HTML 元素，不存在兼容性问题。

   **他们的优先级**：当样式冲突时，就是采用就近原则，是值css属性离被修饰的内容最近的为主。

    若没有样式冲突则采用叠加效果。




三、**css2的选择符：
---------------------------------------------------------------
1. ##### html选择符（标签选择器）

 就是把html标签作为选择符使用
 如 p{....}  网页中所有p标签采用此样式
```css
h2{....}  网页中所有h2标签采用此样式
```
##### 2. class类选择符 (使用点.将自定义名（类名）来定义的选择符)（类选择器）

定义： 		  .类名{样式....}    匿名类

   其他选择符名.类名{样式....}
 使用：`<html标签 class="类名">...</html标签>`

 .mc{color:blue;} /* 凡是class属性值为mc的都采用此样式 */

 p .ps{color:green;}  /\*只有p标签中class属性值为ps的才采用此样式*/

 注意：类选择符可以在网页中重复使用

##### 3.Id选择符(ID选择器)

 定义： #id名{样式.....}
 使用：`<html标签 id="id名">...</html标签>`

 注意：id选择符只在网页中使用一次

选择符的优先级：从大到小 [ID选择符]->[class选择符]->[html选择符]->[html属性]

##### 4.关联选择符（包含选择符）

 格式： 选择符1 选择符2 选择符3 ...{样式....}
 例如： table a{....} /\*table标签里的a标签才采用此样式*/

 	h1 p{color:red} /\*只有h1标签中的p标签才采用此样式*/

##### 5.组合选择符（选择符组）

 格式： 选择符1,选择符2,选择符3 ...{样式....}

 	h3,h4,h5{color:green;} /\*h3、h4和h5都采用此样式*/

##### 6.*通配符（全局选择器）

 说明：

 通配符的写法是“*”，其含义就是所有元素。

 用法：

 常用来重置样式   

 	*{ padding:0; margin:0;}


7. ##### 伪类选(伪元素)择符：

   格式： 标签名:伪类名{样式....}

   ```css
    a:link {color: #FF0000; text-decoration: none} 	    /* 未访问的链接 */

    a:visited {color: #00FF00; text-decoration: none} 	    /* 已访问的链接 */

    a:hover {color: #FF00FF; text-decoration: underline} /* 鼠标在链接上 */

    a:active {color: #0000FF; text-decoration: underline} /* 激活链接 */
   ```

    为了简化代码，可以把伪类选择符中相同的声明提出来放在a选择符中；

   #####  例如：

    a{color:red;}     a:hover{color:green;} 表示超链接的三种状态都相同，只有鼠标划过变颜色。

   伪类（Pseudo classes）是选择符的螺栓，用来指定一个或者与其相关的选择符的状态


8. 属性选择器：
   ...

9. 其他伪类选择器
   ...

##### 优先级:行内->css3选择器->id->class->html->html属性

## 四、  CSS3中的选择器

1. ##### 关系选择器：

 div>p 选择所有作为div元素的子元素p
 div+p 选择紧贴在div元素之后p元素
 div~p 选择div元素后面的所有兄弟元素p
2. ##### 属性选择器：

 [attribute]选择具有attribute属性的元素。
 [attribute=value]选择具有attribute属性且属性值等于value的元素。
 [attribute~=value]选择具有attribute属性且属性值为一用空格分隔的字词列表，其中一个等于value的元素。 
 [attribute|=value]选择具有att属性且属性值为以val开头并用连接符"-"分隔的字符串的E元素。

 ```Css
 div[class|="a"] 	class="a-test"
 ```
 [attibute^=value]匹配具有attribute属性、且值以valule开头的E元素
 [attribute$=value]匹配具有attribute属性、且值以value结尾的E元素
 [attribute*=value]匹配具有attribute属性、且值中含有value的E元素
 浏览器兼容性问题：
 不用担心浏览器兼容问题，也不用考虑IE浏览器版本问题。

CSS 伪类用于向某些选择器添加特殊的效果。
3. ##### 结构性伪类选择器：

 ::first-letter设置对象内的第一个字符的样式。
 ::first-line设置对象内的第一行的样式。
 :before设置在对象前（依据对象树的逻辑结构）发生的内容。

 ​	定义和用法

 ​	:before 选择器在被选元素的内容前面插入内容。

 ​	请使用 content 属性来指定要插入的内容。

 ​	content不能省略

 :after设置在对象后（依据对象树的逻辑结构）发生的内容。

 ​	定义和用法

 ​	:before 选择器在被选元素的内容后面插入内容。

 ​	请使用 content 属性来指定要插入的内容。

 ​	content不能省略

 :first-of-type匹配同类型中的第一个同级兄弟元素
 :last-of-type匹配同类型中的最后一个同级兄弟元素 表示其父元素下的最后一个指定类型的元素。

 :only-of-type匹配同类型中的唯一的一个同级兄弟元素

 :nth-last-of-type(n) 匹配同类型中的倒数第几个同级兄弟元素

 :nth-of-type(n) 匹配同类型中的第几个同级兄弟元素

 :only-child匹配父元素仅有的一个子元素
 :nth-last-child(n)匹配同类型中的倒数第n个同级兄弟元素
 :first-child()匹配父元素的最后一个子元素
 :last-child()匹配父元素的最后一个子元素 其父元素的最后一个子元素，且这个元素是css指定的元素，才可以生效

 :nth-child(n)匹配父元素的第n个子元素

 **实例：**

 ```css
 li:nth-child(2n){color:#f00;} /* 偶数 */
 li:nth-child(2n+1){color:#000;} /* 奇数 */
 ```

 ##### child和type区别:

 child所指定的必须为第一个或者最后一个 否则不生效  但是type可以

 :root匹配元素在文档的根元素。在HTML中，根元素永远是HTML
 :empty匹配没有任何子元素（包括text节点）的元素
 :not(selector)匹配不含有selector选择符的元素
 ```css
 .demo li:not(:last-child) {
 	border-bottom: 1px solid #ddd;
 }
 上述代码的意思是：给该列表中除最后一项外的所有列表项加一条底边线
 ```

4. ##### *状态伪类选择器

 :link 设置超链接a在未被访问前的样式。
 :visited 设置超链接a在其链接地址已被访问过时的样式
 :active	 设置元素在被用户激活（在鼠标点击与释放之间发生的事件）时的样式
  *:hover	设置元素在其鼠标悬停时的样式
  *:focus	设置元素在其获取焦点时的样式
 :target	匹配相关URL指向的E元素 将锚点跳转的代码进行设置

 ```css
 #my_md:target{}
 ```
 :enabled   匹配用户界面上处于可用状态的元素
 :disabled   匹配用户界面上处于禁用状态的元素
 :checked   匹配用户界面上处于选中状态的元素

 **实例：**

 ```css
 input:checked + span {
 	background: #f00;
 }
 input:checked + span:after {
 	content: " 我被选中了";
 }
 <input type="radio" name="colour-group" value="0" /><span></span>
 ```

 ::selection  设置对象被选择时的样式

 **实例：**

 ```css
 p::selection{background:#000;color:#f00;}
 <p>你选中这段文字后，看看它们的文本颜色和背景色，就能明白::selection的作用。</p>
 只能定义被选择时的background-color，color及text-shadow(IE11尚不支持定义该属性)。 
 ```

5. ##### !important   应用优先权

   ```python
   .test {important
   color: #f00 !important;
   color: #000;
   }
   ```

##### 伪类就是创建了一个假的类名；伪元素就是创建了一个假的元素标签。

同样举例说明伪元素（就是创建了假的元素）：如让<p>啊啦啦啦</p>里面的啊变颜色
我们的一般做法是<p><span>啊</span>啦啦啦</p>然后span{color:red}
但是用伪元素就不用创建新元素span了,直接p::first-letter{color:red}就可以搞定了是不是很爽啊，相当于创建了一个假的元素span然而实际并没有创建

======================================================================================

五、CSS中常用的属性：
---------------------------------------------------------------------------------------
#### (1) color颜色属性：

a. HSL颜色:  通过对色调(H)、饱和度(S)、亮度(L)三个颜色通道的变化以及它们相互之间的叠加来得到各式各样的颜色.

```css
background-color: hsl(240,100%,50%);color:white；
```
b. HSLA颜色: 色调(H)、饱和度(S)、亮度(L)、透明度(A)；
```css
background-color: hsla(0,100%,50%,0.2);
```
*c. RGB颜色: 红(R)、绿(G)、蓝(B)三个颜色通道的变化
```css
background-color: rgba(200,100,0);
```
d. RGBA颜色: 红(R)、绿(G)、蓝(B)、透明度(A)
```css
background-color: rgba(0,0,0,0.5);
```
*e. 图片透明度的设置  img.opacity{ opacity:0.25;}
```css
兼容IE8 filter:alpha(opacity=100);
```

**颜色的使用:**

1. 颜色的英文单词
2. 十六进制
3. rgb

#### (2) 字体属性： font

font
 *font-size: 		字体大小：20px，60%基于父对象的百分比取值
 *font-family：	字体：宋体，Arial
font-style：	normal正常；italic斜体； oblique倾斜的字体
 *font-weight：	字体加粗 ：bold
font-variant:	small-caps 小型的大写字母字体
font-stretch:	[了解]文字的拉伸是相对于浏览器显示的字体的正常宽度（大部分浏览器不支持）。

<' font-style '>： 指定文本字体样式
<' font-variant '>： 指定文本是否为小型的大写字母
<' font-weight '>： 指定文本字体的粗细
<' font-size '>： 指定文本字体尺寸
<' line-height '>： 指定文本字体的行高 tvls
<' font-family '>： 指定文本使用某个字体或字体序列
且font-size和font-family是不可忽略

#### (3) 文本属性：

text-indent:	首行缩进：2em text-indent:30px;
text-overflow：	文本的溢出是否使用省略标记（...）。clip|ellipsis（显示省略标记）
*text-align: 	文本的位置：left center right
text-transform：对象中的文本的大小写：capitalize(首字母)|uppercase大写|lowercase小写
*text-decoration: 字体画线：none无、underline下画线，line-through贯穿线
text-decoration-line：[了解]文本装饰线条的位置（浏览器不兼容）

*text-shadow: 文本的文字是否有阴影及模糊效果
vertical-align: 文本的垂直对齐方式  middle居中
direction：文字流方向。ltr | rtl

white-space:nowrap; /* 强制在同一行内显示所有文本*/

*letter-spacing: 文字或字母的间距
word-spacing：单词间距
*line-height：行高
*color： 字体颜色
word-break:break-all;单词换行

#### (4) *边框：

```css
border:宽度 样式 颜色;
border-color;
border-style; 边框样式：solid实现，dotted点状线，dashed虚线
border-width:
border-left-color;
border-left-style;
border-left-width:
...
CSS3的样式
border-radius：圆角处理
box-shadow:	设置或检索对象阴影
三角
div{
	border: 14px solid #FFF;
	width:0;
	height: 0;
	border-bottom-color:red;
}
```
#### (5) 背景属性：background

*background-color: 背景颜色
*background-image: 背景图片
*background-repeat：是否重复，如何重复?(平铺) 

+ repeat-x 按照x轴平铺
+ repeat-y 按照y轴平铺
+ no-repeat 不平铺

*background-position：定位

+ center： 背景图像横向和纵向居中。
+ left： 背景图像在横向上填充从左边开始。
+ right： 背景图像在横向上填充从右边开始。
+ top： 背景图像在纵向上填充从顶部开始。
+ bottom： 背景图像在纵向上填充从底部开始。

background-attachment：[əˈtætʃmənt] 是否固定背景，
+ scroll:默认值。背景图像是随对象内容滚动
+ fixed:背景图像固定

#####   css3的属性

*background-size: 背景大小，如 background-size:100px 140px;

**组合写法：**

```python
background: green url("./sc/1.gif") no-repeat center/200px 300px scroll;
```

多层背景：
  background:url(test1.jpg) no-repeat scroll 10px 20px,url(test2.jpg) no-repeat scroll 50px 60px,url(test3.jpg) no-repeat scroll 90px 100px;
  background-origin:content-box,content-box,content-box;
  background-clip:padding-box,padding-box,padding-box;
  background-size:50px 60px,50px 60px,50px 60px;

#### (6) *内补白（内补丁）

padding：		检索或设置对象四边的内部边距,如padding:10px; padding:5px 10px;
padding-top：	检索或设置对象顶边的内部边距
padding-right：	检索或设置对象右边的内部边距
padding-bottom：检索或设置对象下边的内部边距
padding-left：	检索或设置对象左边的内部边距
box-sizing: border-box;

##### 盒子模型

css定义所有的元素都可以拥有像盒子一样的外形和平面空间，即都包含边框（border)、外边距(margin)、内边距(padding)、内容区(content)。
计算公式：
宽 =左右margin+左右border+左右padding+内容width
高 =上下margin+上下border+上下padding+内容height

##### 怪异盒子模型

```css
/* 切换盒子模型计算方式
 *
 * 	从边框左边到边框右边之间的距离  才是width
 * 		计算宽度非常方便
 *
 */
box-sizing: border-box;
```

#### (7) *外补白（外补丁）

margin：		检索或设置对象四边的外延边距,如 margin:10px;  margin:5px auto;
margin-top：	检索或设置对象顶边的外延边距
margin-right：	检索或设置对象右边的外延边距
margin-bottom： 检索或设置对象下b边的外延边距
margin-left：	检索或设置对象左边的外延边距

**注意：**

外边距的上下距离会重叠 左右不会重叠

#### (8) Position定位

*position:	定位方式：absolute(绝对定位)、fixed(固定)（relative定位参考，可对内部相对absolute定位）
*z-index:	层叠顺序，值越大越在上方。
*top:		检索或设置对象与其最近一个定位的父对象顶部相关的位置
right:		检索或设置对象与其最近一个定位的父对象右边相关的位置
bottom:		检索或设置对象与其最近一个定位的父对象下边相关的位置
*left:		检索或设置对象与其最近一个定位的父对象左边相关的位置

**总结：**

1. fixed和absolute绝对定位 不会保留其物理空间 设置当前定位的元素会漂浮在其它元素的上方 
2. 定位会参照外层的定位而定位 如果外层嵌套的标签不存在定位 则会按照body体进行定位
3. fixed和absolute使用除了fixed会随着滚动条的滚动而滚动之外 使用方式一样的



##### 设置div相对于浏览器居中显示

```css
position:absolute;
left:0;
top:0;
bottom:0;
right: 0;
margin: auto;
```
#### (9) Layout布局

*display：	是否及如何显示：

+ none隐藏
+ block块状显示
+ inline 行级
+ inline-block 行级的块级标签

   *float:指出了对象是否及如何浮动:值none | left | right
    *clear：清除浮动：none | left | right | both两侧
    visibility：设置或检索是否显示对象。visible|hidden|collapse。

    ​与display属性不同，此属性为隐藏的对象保留其占据的物理空间

    clip:检索或设置对象的可视区域。区域外的部分是透d明的。 rect(上-右-下-左)

    ​如：clip:rect(auto 50px 20px auto);上和左不裁剪，右50，下20.

 *overflow:超出隐藏：hidden，visible：不剪切内容
 overflow-x：内容超过其指定宽度时如何管理内容: visible | hidden | scroll | auto
 overflow-y：内容超过其指定高度时如何管理内容

图片格式（了解）
*    png    常用的网络传输格式，开发中用的最多的格式 HTML常用，
   * 			移动开发（Android，IOS，WP）,这个格式文件失真率低
      * 		支持透明像素，相对来说占用空间比较多
* jpg    比较常用的图片格式，压缩性能比较高，不支持透明像素 失真率比较高

* gif    动态图片，不透明的，占用空间比较高

* psd    Photoshop的原图，PS超级大，但是可以保留图片原始所有资料

* webp   Google定义的，它集合了png和jpg的优点

     支持透明像素，空间占用低

##### 新增CSS3选择器及属性只需在选择器或属性前加上相对应的浏览器前缀即可

-webkit- 		Chrome
 -moz-     		FF
 -ms-			IE
 -o-			Opera

#### (10) 用户界面 User Interface

*cursor	鼠标指针采用何种系统预定义的光标形状。pointer小手，url自定义

zoom	设置或检索对象的缩放比例： normal|5倍|200%百分比
box-sizing	设置或检索对象的盒模型组成模式。content-box | border-box

content-box： padding和border不被包含在定义的width和height之内。
border-box： padding和border被包含在定义的width和height之内。

resize	设置或检索对象的区域是否允许用户缩放，调节元素尺寸大小。
+ none： 不允许用户调整元素大小。

+ both： 用户可以调节元素的宽度和高度。

+ horizontal： 用户可以调节元素的宽度

+ vertical： 用户可以调节元素的高度。

outline 复合属性：设置或检索对象外的线条轮廓

outline-width设置或检索对象外的线条轮廓的宽度
outline-style设置或检索对象外的线条轮廓的样式
outline-color设置或检索对象外的线条轮廓的颜色
 outline-offset设置或检索对象外的线条轮廓偏移位置的数值

#### (11) 表格相关属性：

border-collapse	设置或检索表格的行和单元格的边是合并在一起还是按照标准的HTML样式分开	separate | collapse
border-spacing	设置或检索当表格边框独立时，行和单元格的边框在横向和纵向上的间距
caption-side	设置或检索表格的caption对象是在表格的那一边	top | bottom 
empty-cells	设置或检索当表格的单元格无内容时，是否显示该单元格的边框	hide | show

#### (12) 过渡 Transition:

transition 	检索或设置对象变换时的过渡效果
transition-property	检索或设置对象中的参与过渡的属性
transition-duration	检索或设置对象过渡的持续时间
transition-timing-function	检索或设置对象中过渡的类型
transition-delay	检索或设置对象延迟过渡的时间

#### (13) 动画 Animation

animation 	检索或设置对象所应用的动画特效
animation-name	检索或设置对象所应用的动画名称
animation-duration	检索或设置对象动画的持续时间
animation-timing-function	检索或设置对象动画的过渡类型
animation-delay	检索或设置对象动画延迟的时间
animation-iteration-count	检索或设置对象动画的循环次数
animation-direction	检索或设置对象动画在循环中是否反向运动 alternate
animation-play-state	检索或设置对象动画的状态
animation-fill-mode	检索或设置对象动画时间之外的状态

#### (14) 2D变换 2D Transform:

transform 	检索或设置对象的变换
transform-origin	检索或设置对象中的变换所参照的原点
