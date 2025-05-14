#   HTML

## 常见

//<!DOCTYPE html>//设定当前文件为html文件

//<!-- -->//注释,VS快捷键 ctrl+/

//<meta charset="UTF-8">//设置utf-8的字符集

//<meta name="viewport" content="width=device-width, initial-scale=1.0">//设置浏览器兼容性

## 排版

标题标签：<h1>~<h6>//成对出现，字体加粗，且逐渐减小

 段落标签：//<p></p>//

换行标签：//<br>

水平线标签：<hr>

//<b></b>// //<strong></strong>// 加粗

//<u></u>// //<ins><ins>// 下划线

//<i></i>>// //<em></em>// 倾斜

//<s></s>// //<del></del>// 删除线

以上四组标签，后者是突出重要性的强调语境

## 图像

图片标签：//<img src="" alt="">//后面是属性

src:指定图像的url（相对路径/绝对路径,也可以使用绝对网络路径）

alt:替换文本，当图片无法显示时，显示的文字

title:鼠标悬停在图片上时显示的文字

width:图像的宽度（像素px/相对于父元素的百分比%）

height:图像的高度（像素px/相对于父元素的百分比%）

注意：高度和宽度只设置一个时，会等比缩放

./代表同级目录，../上级目录

## 音频和视频

音频标签//<audio></audio>>

//<video src="" controls autoplay muted loop></video>//

src:音频路径

controls:显示播放的控件

autoplay:自动播放(对于视频在谷歌浏览器，在后面加muted实现静音播放)

loop:循环播放

## 链接

标签

```
<a href="..." target="..."></a>展示超链接
```

href:指定资源访问的url,可以是网址，也可以是文件地址，#代表空

target:指定在何处打开资源链接(以下为取值)

​	_self：默认值，在当前页面打开

​	_blank:在空白页面打开

text_decoration 设置文本样式，例如是否含有下划线

## 列表

//<ul></ul>//表示无序列表的整体，用于包裹li标签，也只能包裹li标签

//<li></li>//表示无序列表的每一项，用于包含每一行的内容，可以包含任何内容

//<ol></ol>//表示有序列表的整体，用于包含li标签，也只能包含li标签，每一项前有默认序号标识

//<dl></dl>//表示自定义列表的整体，用于包裹dt/dd标签

//<dt></dt>//表示自定义列表的主题

//<dd></dd>//表示自定义列表的争对主题的每一项内容

## 表格

//<table></table>//表格整体，用于包裹多个tr

属性：

​	border:边框宽度，值为数字

​	width:表格宽度，值为数字

​	height:表格高度，值为数字

//<tr></tr>//表格每行，用于包裹td

//<td></td>//表格单元格，用于包裹内容

属性：

​	rowspan:值为合并的单元格数量，将多行的单元格垂直合并，上下合并只保留最上面的

​	colspan:值为合并的单元格数量，将多列的单元格水平合并，左右合并只保留最左的

//<caption></caption>//表格大标题，默认在表格整体顶部居中位置显示

//<th></th>//表头单元格，表格一小列的标题，通常用于表格第一行，默认加粗居中显示

//<thead></thead>//表格头部，用于包裹tr标签

//<tbody></tbody>//表格主题，用于包裹tr标签

//<tfoot></tfoot>//表格底部，用于包裹tr标签

## 表单标签

//<input>

属性：
	type: text(文本输入)，

​		placeholder(占位符，提示用户的输入内容)

​	password(密码输入)，

​		placeholder(占位符，提示用户的输入内容)

​	radio(单选框)，

​		name,分组，有相同name属性值的单选框为一组，一组同时只能有一个被选中

​		checked 默认选中

​	checkbox(多选框)，

​	file(文件选择)

​		multiple,可以选择多个文件

​	submit(提交按钮)，reset(重置按钮)

​		value:按钮提示文字

​	//<form></form>//需要submit和reset发挥作用，需要将相应的内容放到本标签下

​    button(普通按钮，无功能),

​		value:按钮提示文字

//<button></button>//按钮标签

属性：

​	submit,reset,button，都同上

//<select></select>//下拉菜单整体

​	属性：selected默认选中属性

//<option></option>//下拉菜单的每一项

//<textarea></textarea>//文本域标签，右下角可以拖拽改变大小

​	属性：

​		cols:文本域内可见宽度

​		rows:文本域内可见行数

//<label></label>//用于绑定内容与表单标签的关系，用for 属性去使用，或者删除for属性直接包裹相应的表单

​	属性：

​		for:值为对应表单的id属性的值

## 语义化标签

//<div></div>//自带换行

//<span></span>//不带换行

//<header></header>//网页头部

//<nav></nav>//网页导航

//<footer></footer>//网页底部

//<aside></aside>//网页侧边栏

//<section></section>//网页区块

//<article></article>//网页文章

## 字符实体

#nbsp空格占位符



# CSS

## 写法样式

css一般写在style标签中，模板如下，这是内嵌式写法

```
<style>
	<h1>{
		color: red;
	}
</style>
```

外联样式：<link rel="stylesheet" href="css文件的路径名">，写在head下的title下

行内样式:<h1 style="color: red">文字内容</h1>

## 选择器

### 标签选择器

```
<h1>{
		color: red;
	}
h1标签名
color css属性名
red 属性值
```

### 类选择器

```
<h1 class="cls"></h1>
.cls{
	color:#000000
}
```

注意：不能以数字开头，可以选择多个类，类名之间用空格隔开

### id选择器

```
<h1 id="hid"></h1>
#hid{
	color:red;
}
```

id在页面中是唯一的

### 通配符

```
*{
	color:res;
}
```

可以给整个页面的标签进行设计

## 字体和文本样式

### 字体大小

属性名：front-size

取值：数字+px

### 字体粗细

属性名：front-weight

取值：

​	关键字：normal/bold

​	数值：100-900的整数

### 字体样式（是否倾斜）

属性名：font-style

取值：

​	normal/italic

### 字体系列

属性名：font-family

常见取值：

​	具体字体：Microsoft Yahei

​	字体系列：sans-serif,serif

### 字体font相关属性的连写

属性名：font

值：style weight,size,字体

后面层叠前面的

### 文本缩进

属性名：text-indent

取值：

​	数字+px

​	数字+em

注意：默认字体大小16px

### 文本水平对齐方式

属性名：test-align

取值：

 	left(左对齐)

​	center(居中对齐)

​	right(右对齐)

### 文本修饰

属性名：text-decoration

取值：

​	underline(下划线)

​	line-through(删除线)

​	overline(上划线)

​	none(无装饰线)

### 行高

属性名：line-height(每行文字的高度)

取值：

​	数字+px

​	倍数（当前标签font-size的倍数)

注意：同时设置行高和font的连写 font:style weight size/line-height family

### 颜色表现形式

1：关键字表示 red,blue

2：rgb表示法 rgb(val,val,val)

3：十六进制表示法 #000000 每两位对应一个rgb值

### 标签水平居中

css加这句话 margin:  0 auto;

## 选择器进阶

### 后代选择器

作用：根据 HTML 标签的嵌套关系，选择父元素 后代中(包括子代，孙代) 满足条件的元素

```
<div>
        <p>这是div的儿子</p>   
</div>
<style>
        div p{
            color:red;
        }
</style>
```

语法：父选择器 子选择器{}

### 子代选择器

```
<style>
        div>a{
            color:red;
        }
</style>
<div>
        <a href="#">这是div的a</a>//只有这段代码受选择器影响
        <p>
            <a href="#">这是div里的p里的a</a>
        </p>   
</div>
```

语法：父选择器>子选择器{}

### 并集选择器

```
<p>ppp</p>
<div>div</div>
<span>span</span>
<h1>h1</h1>
<style>
        p,div,span,h1{
            color:red;
        }
</style>
```

### 交集选择器

```
<style>
       p.box{
        color: red;
       }
</style>
<p class="box">这是p标签</p>
<p>ppppppp</p>
<div class="box">这是div标签</div> 
```

### hover伪类选择器

作用：选中鼠标悬停在元素的状态，设置样式

语法：选择器;hover{}

```
<a href="#">这是超链接</a>
<style>
       a:hover{
        color: red;
       }
</style>
```

## 背景相关属性

### 背景颜色

属性名：background-color

属性值：关键字，或者16进制，rgb表示法

```
<div>div</div>
<style>
       div{
        background-color: red;
       }
</style>
```

### 背景图片

属性名：background-image

属性值：url('')

```
<div>div</div>
<style>
       div{
        background-image: url('');
       }
</style>
```

### 背景平铺

属性名：background-repeat

属性值：

​	repeat:(默认值)水平和垂直方向都平铺

​	no-repeat:不平铺

​	repeat-x:沿着水平方向平铺

​	repeat-y:沿着垂直方向平铺

注意：平铺指的是填充方式

### 背景位置

属性名：background-position

属性值：

​	方位名词：

​		水平方向：left,center,right

​		垂直方向：top,center,bottom

​	数字+px(坐标)

​		坐标系：

​			原点：盒子的左上角

​			x轴：水平向右

​			y轴：水平向左

​			判断依据：将图片的左上角与坐标点重合即可

```
div {
            width: 400px;
            height: 400px;
            background-color: pink;
            background-image: url(./images/1.jpg);
            background-repeat: no-repeat;
            /* background-position: right 0; */
            /* background-position: right bottom; */
            /* background-position: center center; */
            /* background-position: center; */
            /* background-position: 50px 0; */
            /* background-position: 50px 100px; */
            background-position: -50px -100px;

            /* 正数: 向右向下移动; 负数:向左向上移动 */
            /* 注意: 背景色和背景图只显示在盒子里面 */
        }
```

### 背景相关属性连写

属性名：background

属性值：单个属性值合写，取值之间以空格隔开

书写顺序：background:color,image,repeat,position

```
<style>
        div {
            width: 400px;
            height: 400px;
            /* 不分先后顺序 背景色  背景图  背景图平铺  背景图位置 */
            /* background: pink url(./images/1.jpg) no-repeat center bottom; */
            /* 背景图位置如果是英文单词可以颠倒顺序 */
            background: pink url(./images/1.jpg) no-repeat bottom center ;

            /* 测试背景图位置如果是数值 不要颠倒顺序 */
            /* 水平50px, 垂直100px */
            /* background: pink url(./images/1.jpg) no-repeat 50px 100px; */
            background: pink url(./images/1.jpg) no-repeat 100px 50px;


        }
</style>
```

## 元素显示模式

### 块级元素

显示特点：

​	1：独占一行

​	2：宽度默认是父元素的宽度，高度默认由内容撑开

​	3：可以设置宽高,设置了宽高，依旧默认独占一行

代表标签

​	div,p,h系列,ul,li,dl,dt,dd,form,header

### 行内元素

显示特点：

​	1：一行可以显示多个

​	2：宽度和高度默认由内容撑开

​	3：不可以设置宽高

代表标签：

​	a,span,b,u,i,s,strong,ins,em,del

### 行内块元素

显示特点：
	1：一行可以显示多个

​	2：可以设置宽高

代表标签：

​	input,textarea,button,select

​	特殊情况：img有行内块标签的特点

### 元素显示模式转换

语法：

display:block (转块级)

display:inline-block(转行内块)

display:inline(转行内)

### 标签嵌套

1；块级元素一般作为大容器，可以嵌套：文本，块级元素，行内元素，行内块元素

​	但是p标签不要嵌套div,ph等块级元素

2：a标签可以嵌套任意元素，除了a标签本身

## CSS特性

### 继承性

特性：子元素有默认继承父元素样式的特点

可以继承的常见属性：

​	color,font-style font-weight......

注意： 自己本身固有的属性不会继承父类，如需更改属性，需单独进行编写

### 层叠性

特性：
	1：给同一个标签设置不同样式--->此时样式会层层叠加-->会共同作用在标签上

​	2：给同一个标签设置相同的样式-->此时样式会层叠覆盖-->写在最后的样式会生效

注意：

​	当样式冲突时，只有当选择器优先级相同时，才会通过层叠性判断结果

### 优先级

继承<通配符选择器<标签选择器<类选择器<id选择器<行内样式<!important

注意：

​	1：!important写在属性值后面，分号的前面

​	2：!important不能提升继承的优先级，只要是继承优先级最低

​	3：实际开发中不建议使用

### 权重叠加计算

场景：如果是复合选择器，此时需要权重叠加计算方法，判断最终哪个选择器优先级最高会生效

（行内，id，类，标签）

比较规则：

1. 先比较第一级数字，如果比较出来了，之后的统统不看 
2. 如果第一级数字相同，此时再去比较第二级数字，如果比较出来了，之后的统统不看 
3. 如果最终所有数字都相同，表示优先级相同，则比较层叠性（谁写在下面，谁说了算!）
4. 都是继承，遵循就近原则

注意点：!important如果不是继承，则权重最高，天下第一！  

## 盒子模型

### 内容区域的宽度和高度

属性：width,height

取值：数字+px

### border边框

属性名：border

属性值：单个取值连写，中间空格连写（粗细（数值+px） 线条种类（solid,关键字）颜色）

```
<style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
            /* border: 粗细  线条样式   颜色 -- 不分先后顺序 */
            /* solid : 实线 */
            /* border: 1px solid #000; */

            /* dashed: 虚线 */
            /* border: 5px dashed #000; */

            /* dotted : 点线 */
            /* border: 5px dotted #000; */

            border-left: 5px dotted #000;
            border-right: 5px dotted #000;
            border-top: 1px solid red;
            border-bottom: 1px solid red;
        }
</style>
```

### border 单方向设置

场景：只给盒子的某个方向单独设置边框

属性名：border-方位名词

属性值：连写的取值

### 盒子实际大小初级计算公式

盒子本身宽高加边框的宽度

### 内边距（padding）

属性名：padding

属性值：数字+px

```
<style>
        div {
            width: 300px;
            height: 300px;
            background-color: pink;
            /* 添加了4个方向的内边距 */
            /* padding: 50px; */

            /* padding 属性可以当做复合属性使用, 表示单独设置某个方向的内边距 */
            /* padding 最多取4个值 */

            /* 四值: 上  右   下  左 */
            /* padding: 10px 20px 40px 80px; */

            /* 三值 : 上   左右   下*/
            /* padding: 10px 40px 80px; */

            /* 两值 : 上下  左右*/
            /* padding: 10px 80px; */

            padding-left: 10px;
            padding-bottom: 50px;
        }

        /* 多值写法, 永远都是从上开始顺时针转一圈, 如果数不够, 看对面 */
</style>
```

注意：算盒子实际大小时跟border一样，要加上本省的宽度

### 内减模式(box-sizing)

属性名：box-sizing

属性值：（关键字）border-box

备注：此属性加上之后设置的宽高是盒子的整体宽高

```
<style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
            border: 10px solid #000;
            padding: 20px;

            /* 內减模式 */
            /* 变成CSS3的盒子模型, 好处: 加了border和padding不需要手动减法 */
            box-sizing: border-box;
        }
</style>
```

### 外边距（margin）

不计算在盒子实际大小里

margin取负值时出现如下情况：

1：元素本身没有宽度，会增加元素宽度(left/right)

2：元素本身有宽度，会产生位移(left/right)

3：margin-top为负值，不管是否有高度，都不会增加高度，而是产生向上的唯一

4：margin-bottom为负值的时候不会位移，而是减少自身供css读取的高度

```
<style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
            margin: 50px;
            margin-left: 100px;
        }
</style>
```

### 默认内外边距清除

```
<style>
        * {
            margin: 0;
            padding: 0;
        }
</style>
```

### 版心居中

```
<style>
        div {
            width: 1000px;
            height: 300px;
            background-color: pink;
            margin: 0 auto;
        }
</style>
```

### 列表风格(去掉默认圆点)

```
ul {
            list-style: none;
        }
```

### 内外边距常见问题

#### 合并

场景：垂直布局的块级元素，上下的margin会合

结果：最终两者距离为margin的最大值

```
<div class="one">11</div>
<div class="two">22</div>
<style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }

        .one {
            /* margin-bottom: 50px; */
            margin-bottom: 60px;
        }

        .two {
            margin-top: 50px;
        }
</style>
```

#### 塌陷

互相嵌套的块级元素，子元素的margin-top会作用在父元素上，导致父元素也有了外边距

解决方案：

1：给父元素设置border-top或padding-top(分割父子元素的margin-top)

2：给父元素设置overflow:hidden

3：转换成行内块元素

4：设置浮动

```
	<style>
        .father {
            width: 300px;
            height: 300px;
            background-color: pink;
            /* padding-top: 50px; */
            /* 如果设计稿没有border, 不能使用这个解决办法 */
            /* border: 1px solid #000; */

            /* overflow: hidden; */
        }

        .son {
            width: 100px;
            height: 100px;
            background-color: skyblue;

            margin-top: 50px;

            display: inline-block;
        }
    </style>
    <div class="father">
        <div class="son">son</div>
    </div>
```

#### 行内元素的margin和padding无效情况

场景：给行内元素设置margin和padding时

结果： 1. 水平方向的margin和padding布局中有效！ 2. 垂直方向的margin和padding布局中无效！

```
 	<style>
        span {
            /* margin: 100px; */
            /* padding: 100px; */
            line-height: 100px;
        }
    </style>
    <span>span</span>
    <span>span</span>
```

## 浮动

### 结构伪类选择器

作用与优势：

作用：根据元素在HTML中的结构关系查找元素 

优势：减少对于HTML中类的依赖，有利于保持代码整洁 

场景：常用于查找某父级选择器中的子元素

```
E:first-child{} 匹配父元素中的第一个元素，并且是E元素
E:last-child{}  匹配父元素中的最后一个元素，并且是E元素
E:nth-child(n){}匹配父元素中第N个元素，并且是E元素
E:nth-last-child(n) 匹配父元素中倒数第N个元素，并且是E元素
```

```
	<style>
        /* 选中第一个 */
        /* li:first-child {
            background-color: green;
        } */

        /* 最后一个 */
        /* li:last-child {
            background-color: green;
        } */

        /* 任意一个 */
        /* li:nth-child(5) {
            background-color: green;
        } */

        /* 倒数第xx个 */
        li:nth-last-child(1) {
            background-color: blue;
        }
    </style>
```

也可以通过n组成以下公式

偶数：2n/even

奇数：2n+1,2n-1,odd

找到前5个：-n+5

找到从第五个往后：n+5

### 伪元素

伪元素：一般页面中的非主体内容可以使用伪元素

区别： 

元素：HTML 设置的标签 

伪元素：由 CSS 模拟出的标签效果

::before 在父元素内容的最前添加一个伪元素

::after     在父元素内容的最后添加一个伪元素

注意点： 

1. 必须设置content属性才能生效 
2. 伪元素默认是行内元素

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .father {
            width: 300px;
            height: 300px;
            background-color: pink;
        }

        .father::before {
            /* 内容 */
            /* content属性必须添加, 否则伪元素不生效 */
            content: '';
            color: green;
            width: 100px;
            height: 100px;
            background-color: blue;

            /* 默认是行内元素, 宽高不生效 */
            display: block;
        }

        .father::after {
            content: '大米';
        }
    </style>
</head>
<body>
    <!-- 伪元素 通过css创建标签, 装饰性的不重要的小图 -->

    <!-- 找父级, 在这个父级里面创建子级标签 -->

    <div class="father">爱</div>

    <!-- 老鼠爱大米 -->
</body>
</html>
```

### 标准流

标准流：又称文档流，是浏览器在渲染显示网页内容时默认采用的一套排版规则，规定了应该以何种方式排列元素

常见标准流排版规则： 

块级元素：从上往下，垂直布局，独占一行 

行内元素 或 行内块元素：从左往右，水平布局，空间不够自动折行

引入：浏览器解析行内块或行内标签的时候，如果标签换行书写会产生一个空格的距离，不换行代码可读性差，换行会有间距

### 浮动的作用

早期用于图文环绕，现在用于网页布局，比如一个在左，一个在右

### 浮动的属性和取值

属性名：float

属性值：left/right(左浮动/右浮动)

### 浮动的特点

浮动元素会脱离标准流（简称：脱标），在标准流中不占位置 • 相当于从地面飘到了空中 

浮动元素比标准流高半个级别，可以**覆盖**标准流中的元素 

浮动找浮动，下一个浮动元素会在上一个浮动元素后面左右浮动 

浮动元素有特殊的显示效果 • 一行可以显示多个 • 可以设置宽高

注意点： 浮动的元素不能通过text-align:center或者margin:0 auto

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /* 浮动的标签  顶对齐 */
        /* 浮动: 在一行排列, 宽高生效 -- 浮动后的标签具备行内块特点 */
        .one {
            width: 100px;
            height: 100px;
            background-color: pink;

            float: left;

            margin-top: 50px;
        }

        .two {
            width: 200px;
            height: 200px;
            background-color: skyblue;

            float: left;

            /* 因为有浮动, 不能生效 - 盒子无法水平居中 */
            margin: 0 auto;
        }

        .three {
            width: 300px;
            height: 300px;
            background-color: orange;
        }
    </style>
</head>
<body>
    <div class="one">one</div>
    <div class="two">two</div>
    <div class="three">three</div>
</body>
</html>
```

### CSS属性书写顺序

1：浮动，display

2：盒子模型：margin border padding 宽度 高度 背景色

3：文字样式

### 清除浮动

含义：清除浮动带来的影响 

影响：如果子元素浮动了，此时子元素不能撑开标准流的块级父元素

原因：子元素浮动后脱标 → 不占位置

目的：需要父元素有高度，从而不影响其他网页元素的布局

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .top {
            margin: 0 auto;
            width: 1000px;
            /* height: 300px; */
            background-color: pink;
        }

        .bottom {
            height: 100px;
            background-color: green;
        }

        .left {
            float: left;
            width: 200px;
            height: 300px;
            background-color: #ccc;
        }

        .right {
            float: right;
            width: 790px;
            height: 300px;
            background-color: skyblue;
        }
    </style>
</head>
<body>
    <!-- 父子级标签, 子级浮动, 父级没有高度, 后面的标准流盒子会受影响, 显示到上面的位置 -->
    <div class="top">
        <div class="left"></div>
        <div class="right"></div>
    </div>
    <div class="bottom"></div>
</body>
</html>
```

#### 清除方法

##### 1：直接设置父元素高度

##### 2：额外标签

​	在父元素内容的最后添加一个块级元素

​	给添加的块级元素设置clear:both

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .top {
            margin: 0 auto;
            width: 1000px;
            /* height: 300px; */
            background-color: pink;
        }

        .bottom {
            height: 100px;
            background-color: green;
        }

        .left {
            float: left;
            width: 200px;
            height: 300px;
            background-color: #ccc;
        }

        .right {
            float: right;
            width: 790px;
            height: 300px;
            background-color: skyblue;
        }

        .clearfix {
            /* 清除左右两侧浮动的影响 */
            clear: both;
        }
    </style>
</head>
<body>
    <!-- 父子级标签, 子级浮动, 父级没有高度, 后面的标准流盒子会受影响, 显示到上面的位置 -->
    <div class="top">
        <div class="left"></div>
        <div class="right"></div>
        <div class="clearfix"></div>
    </div>
    <div class="bottom"></div>
</body>
</html>
```

##### 3：单伪元素法

```
	.clearfix::after {
            content: '';

            /* 伪元素添加的标签是行内, 要求块 */
            display: block;
            clear: both;

            /* 为了兼容性 */
            height: 0;
            visibility: hidden;
        }
        <div class="top clearfix">
        <div class="left"></div>
        <div class="right"></div>
        <!-- 通过css 添加标签 -->
    </div>
    <div class="bottom"></div>
```

在需要清除的标签后面加上这个元素clearfix

##### 4：双伪元素清除法

```
        /* 清除浮动 */
        .clearfix::before,
        .clearfix::after {
            content: '';
            display: table;
        }

        /* 真正清除浮动的标签 */
        .clearfix::after {
            /* content: '';
            display: table; */
            clear: both;
        }
        </div>
    <div class="bottom"></div>
```

##### 5：给父元素设置overflow:hiden

## 定位装饰

### 设置定位方式

属性名：position

属性值：

​	静态定位（static）

​	相对定位（relative）

​	绝对定位（absolute）

​	固定定位（fixed）

### 设置偏移值

偏移值分为两个方向，水平和垂直各选一个即可

选取原则为就近原则

属性名：

​	水平 left right

​	垂直 top bottom

属性值：

​	数字+px

### 静态定位

介绍：静态定位是默认值，就是之前认识的标准流。 

代码：position: static;

注意点： 1. 静态定位就是之前标准流，不能通过方位属性进行移动 

​				2. 之后说的定位不包括静态定位，一般特指后几种：相对、绝对、固定

### 相对定位

代码：position: relative;

注意：

占有原来的位置

仍然具体标签原有的显示模式特点

改变位置参照自己原来的位置

### 绝对定位

介绍：拼爹型定位，相对于非静态定位的父元素进行定位移动，先找已经定位的父级, 如果有这样的父级就以这个父级为参照物进行定位;

​        有父级, 但父级没有定位, 以浏览器窗口为参照为进行定位

代码：position: absolute;

注意：

1. 脱标, 不占位

2. 改变标签的显示模式特点: 具体行内块特点(在一行共存, 宽高生效)

特点：  需要配合方位属性实现移动 

​			 默认相对于浏览器可视区域进行移动

​			 在页面中不占位置 → 已经脱标

绝对定位相对于谁移动？ 

1. 祖先元素中没有定位 → 默认相对于浏览器进行移动 
2. 祖先元素中有定位 → 相对于 **最近的** **有定位** 的祖先元素进行移动

建议定位模式：子绝父相

### 绝对定位盒子的居中设置

注意:绝对定位的盒子不能用margin: 0 auto;进行居中定位

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box {
            /* 1. 绝对定位的盒子不能使用左右margin auto居中 */
            position: absolute;
            /* margin: 0 auto; */
            /* left: 50%, 整个盒子移动到浏览器中间偏右的位置 */
            left: 50%;
            /* 把盒子向左侧移动: 自己宽度的一半 */
            /* margin-left: -150px; */

            top: 50%;
            /* margin-top: -150px; */

            /* 位移: 自己宽度高度的一半 */
            transform: translate(-50%, -50%);

            width: 400px;
            height: 300px;
            background-color: pink;
        }
    </style>
</head>
<body>
    
    <div class="box"></div>
</body>
</html>
```

绝对定位的盒子属于行内块元素，需设置宽高

### 固定定位

➢ 介绍：死心眼型定位，相对于浏览器进行定位移动 

➢ 代码： position: fixed;

➢ 特点：

 需要配合方位属性实现移动 

相对于浏览器可视区域进行移动 

在页面中不占位置 → 已经脱标 

具备行内块的特点



➢ 应用场景： 1. 让盒子固定在屏幕中的某个位置

```
<style>
        /* css书写: 1. 定位 / 浮动 / display ; 2. 盒子模型; 3. 文字属性 */
        .box {
            position: fixed;
            left: 0;
            top: 0;

            /* 
                1. 脱标-不占位置
                2. 改变位置参考浏览器窗口
                3. 具备行内块特点
            */


            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
    
    
```

### 显示层级的关系

➢ 不同布局方式元素的层级关系： • 标准流 < 浮动 < 定位 

➢ 不同定位之间的层级关系：

 • 相对、绝对、固定默认层级相同 

• 此时HTML中写在下面的元素层级更高，会覆盖上面的元素

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            
            width: 200px;
            height: 200px;
        }

        .one {
            position: absolute;
            left: 20px;
            top: 50px;

            z-index: 1;

            background-color: pink;
        }

        .two {
            position: absolute;
            left: 50px;
            top: 100px;
            
            background-color: skyblue;
        }

        /* 
            默认情况下, 定位的盒子  后来者居上 ,
            z-index:整数; 取值越大, 显示顺序越靠上, z-index的默认值是0
            注意: z-index必须配合定位才生效
        */
    </style>
</head>
<body>
    <div class="one">one</div>
    <div class="two">two</div>
</body>
</html>
```

### 垂直对齐

基线：浏览器文字类型元素排版中存在用于对齐的基线（baseline）

问题：当图片和文字在一行中显示的时候，底部是不对齐的

#### 垂直对齐方式

属性名：vertical-align

属性值：baseline(默认，基线对齐)

​				top(顶部对齐)

​				middle(中部对齐)

​				bottom(底部对齐)

注意： 浏览器把行内和行内块标签当做文字处理,默认基线对齐 

### 光标类型

➢ 场景：设置鼠标光标在元素上时显示的样式 

➢ 属性名：cursor 

➢ 常见属性值：

​			default(默认值，通常是箭头)

​			pointer(小手效果，提示用户可以点击)

​			text(工字形，提示用户可以选择文字)

​			move(十字光标，提示用户可以移动)

```
<style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;

            /* 手型 */
            /* cursor: pointer; */

            /* 工字型, 表示可以复制 */
            /* cursor: text; */

            /* 十字型, 表示可以移动 */
            cursor: move;

        }
    </style>
```

### 边框圆角

➢ 场景：让盒子四个角变得圆润，增加页面细节，提升用户体验 

➢ 属性名：border-radius 

➢ 常见取值：数字+px 、百分比

```
<style>
        .box {
            margin: 50px auto;
            width: 200px;
            height: 200px;
            background-color: pink;

            /* 一个值: 表示4个角是相同的 */
            border-radius: 10px;

            /* 4值: 左上  右上   右下   左下 -- 从左上顺时针转一圈 */
            /* border-radius: 10px 20px 40px 80px; */

            /* border-radius: 10px 40px 80px; */

            /* border-radius: 10px 80px; */
        }
    </style>
```

#### 边框圆角常见应用

➢ 画一个正圆： 

1. 盒子必须是正方形 

2. 设置边框圆角为盒子宽高的一半 → border-radius:50% 

➢ 胶囊按钮： 

盒子要求是长方形 

设置 → border-radius：盒子高度的一半

```
<style>
        .one {
            width: 200px;
            height: 200px;
            background-color: pink;

            /* border-radius: 100px; */
            /* 50% : 取盒子尺寸的一半 */
            border-radius: 50%;
        }

        /* 胶囊状: 长方形, border-radius取值是高度的一半 */
        .two {
            width: 400px;
            height: 200px;
            background-color: skyblue;

            border-radius: 100px;
        }
    </style>
```



### 溢出部分显示效果

 ➢ 溢出部分：指的是盒子 内容部分 所超出盒子范围的区域 

➢ 场景：控制内容溢出部分的显示效果，如：显示、隐藏、滚动条…… 

➢ 属性名：overflow 

➢ 常见属性值：

​		visible(溢出部分可见)

​		hidden(溢出部分隐藏)

​		scroll(无论是否溢出，都显示滚动条)

​		auto(根据是否溢出，来选择是否显示滚动条)

```
<style>
        .box {
            width: 300px;
            height: 300px;
            background-color: pink;

            /* 溢出隐藏 */
            overflow: hidden;

            /* 滚动: 无论内容是否超出都显示滚动条的位置 */
            /* overflow: scroll; */

            /* auto: 根据内容是否超出, 判断是否显示滚动条 */
            /* overflow: auto; */
        }
    </style>
```

### 元素本身隐藏

➢ 场景：让某元素本身在屏幕中不可见。如：鼠标:hover之后元素隐藏 

➢ 常见属性： 

1. visibility：hidden 2. display：none 

➢ 区别： 

visibility：hidden 隐藏元素本身，并且在网页中 占位置 

display：none 隐藏元素本身，并且在网页中 不占位置

 ➢ 注意点： 

• 开发中经常会通过 display属性完成元素的显示隐藏切换 

• display：none；（隐藏）、 display：block；（显示）

```
<style>
        div {
            width: 200px;
            height: 200px;
        }

        .one {
            /* 占位隐藏 */
            /* visibility: hidden; */

            /* **** 不占位隐藏 */
            display: none;

            background-color: pink;
        }

        .two {
            background-color: green;
        }
    </style>
```

### 元素整体透明度

➢ 场景：让某元素整体（包括内容）一起变透明 

➢ 属性名：opacity

 ➢ 属性值：0~1之间的数字 • 1：表示完全不透明 • 0：表示完全透明 

➢ 注意点： • opacity会让元素整体透明，包括里面的内容，如：文字、子元素等……

```
<style>
        div {
            width: 400px;
            height: 400px;
            background-color: green;

            opacity: 0.5;
        }
    </style>
```

# Javascript

## 书写位置

### 内部写法

直接写在html文件里，用script标签包裹

规范：script写在body标签里面，通常放在底部

### 外部写法

代码写在.js的文件里，通过script标签引入，script也写在body内部，src放文件地址

```
<script src=""></script>
```

### 内联

写在标签内部

## 注释和结束符

单行注释：//

块注释：/**/

以;为结束，可写可不写

## 输入输出

```
//文档输出内容
document.write('要输出的内容')
//也可以向代码中输出标签，输出一个h1标签，浏览器会显示一个h1标签
//控制台打印
console.log('')
//警告框
alert('要输出的内容')
//输入
prompt('')//显示一个提示框，对话中包含一个文字信息，用来提示用户输入文字  
```

注意：打印标签时，可以分开打印标签的头和尾，在头和尾中间打印的内容就是标签的内容，标签里面有变量时，可以用模板字符串进行拼接



## 变量

### 变量声明

```
let 变量名
```

注意：let不允许多次申明一个变量

### 输入数据保存进变量

```
let uname=promote('请输入姓名')
```

### 命名规则

1：不能使用关键字

2：只能使用下划线，字母，数字，$组成，且不能以数字开头

3：严格区分大小写

## 数组

### 数组申明

```
let 数组名 = [数据1，数据2，...]
```

### 取值

```
数组名[下标]
```

### 数组长度

```
数组名.length//获取数组长度
```

## 常量

```
const 常量名 = 常量值//不可改变
```

## 数据类型

### 基本数据类型

#### number数字型 

可以是整数，小数，负数........

#### string字符串型

用'    ',"   ",反引号括起来的都是字符串型，推荐使用单引号，+可以实现字符串拼接

##### 模板字符串

使用场景：拼接字符串和变量

语法：反引号，内容拼接变量时用${变量名}包住变量

#### boolean布尔型

取值true/false

注意：0,undefined,null,false,NaN转换为布尔型变量都是false，其余都是true

#### undefined未定义型

申明一个变量但未赋值

#### null空型

```
let ogj=null//本质是一个对象
```

**注意：null+1为1，undefined+1会报错（Nan）获取**

#### 类型转换

 使用表单,promote过来的数据默认是字符串类型，此时不能直接相加

##### 隐式转换

1：+号两边只要有一个是字符串，都会把另一个转成字符串

2：除了+号以外的算数运算符，* /等都会把数据转成数字类型

3：+作为正号解析可以转为数字型

4：任何数字和字符串相加都是字符串

5：有字符串的加法""+1结果为"1"

6：减法-只能用于数学，他会使空字符串变为0,比如""-2=-2

7：null经过数字转换后会变为0

8：undefined经过数字转换之后变为NaN

##### 显式转换

###### 转为数字类型

Number(数据)

转成数字类型

如果字符串里有非数字，则结果为Nan,Nan也是Number类型的数据

parseInt(数据)

只保留整数

parseFloat(数据)

可以保留小数

### 引用数据类型

object对象

## 循环相关

同其他语言

## 运算符

### 赋值运算符

同C++

### 比较运算符

===比较是否值和类型都相等

!== 左右两边是否不全等

其余的同C++

### 逻辑运算符

同C++

### 运算符优先级

1：小括号

2：一元运算符：++，--，！

3：算数运算符：先* /后 + -

4：关系运算符：> >= < <=

5：相等运算符：==  != === !==

6：逻辑运算符：先&&后||

7：赋值运算符=

8：逗号运算符，

### 三元运算符

条件？满足条件语句1：不满足条件的语句2

### 逻辑中断

| 符号 | 短路条件          |
| ---- | ----------------- |
| &&   | 左边为false就短路 |
| \|\| | 左边为true就短路  |



## 数组

### 数组声明

```
let 数组名=[数据1,数据2,数据3,....数据n]
let 数组名=new Array(数据1,数据2,数据3,....数据n)
```

注意：数据的类型不用统一

​			定义了一个空数组，没给具体的值，查找数组的值，控制台打			印显示的结果是undefined

### 数组取值

```
数组名[下标]
```

### 数组长度

```
数组名.length
```

### 遍历数组

略

### 数组值的修改

```
数组[下标]=新值
```

### 数组添加

#### 尾插

```
数组.push(元素1,元素2,...元素n)//返回新数组的长度
```

#### 头插

```
数组.unshift(元素1,元素2,...元素n)//返回数组的长度
```

### 数组的删除

#### 尾删

```
数组.pop()//删除数组的最后一个元素，并返回它的值
```

#### 头删

```
数组.shift()//删除数组的第一个元素，并返回它的值
```

#### 下标删除

```
数组.splice(起始位置,删除几个元素)//第二个参数不写，默认删到最后
```

### 数组的排序

```
arr.sort(function(a.b){
	return a - b;
})//升序排序

arr.sort(function(a.b){
	return b - a;
})//降序排序

arr.sort()//默认升序
```

## 函数

### 函数申明

```
function 函数名(参数列表){}
```

### 函数调用

```
函数名(参数列表)
```

### 函数的参数

1：函数体的参数是形参，直接写参数名即可，调用函数时括号里的参数是实参。

2：参数可以设置默认值,写法如下

```
function example(x = 1,y = 1){}
//当用户不传入实参时，就会使用默认参数
```

### 函数的返回值

```
return 数据
//函数体里加上这条语句即可
```

注意：

1：return后面的代码不会执行

2：return函数可以没有return,这种情况默认返回值为undefined

### 函数细节的补充

1：两个相同的函数后面的会覆盖前面的 (所以尽可能不要重复命名)

2：在js中，形参的个数和实参可以不一致，如果形参过多，默认用undefined填，实参过多，自动忽略

### 作用域

1：通常来说，一段代码中所用到的名字并不总是有效和可用的，而这个名字的可用性就是作用域

2：函数和循环定义的变量就是局部变量

3：如果在函数内部，有一个未申明的变量，此时外部也可以访问

4：函数的形参是函数的局部变量

5：不同作用域下的同名变量遵循就近原则，能够访问的情况下先局部，局部没有找全局

### 匿名函数

#### 申明

```
function(){}
```

#### 使用方式

##### 函数表达式

将函数名赋值给一个变量，并通过变量名称进行调用

```
let fn=function(){}
//赋值后这个变量的名字就是函数的名字，调用方法同普通函数一样
let fn=()=>{}
```

注意：先写表达式，在使用

##### 立即执行函数

场景介绍：避免全局变量之间的污染

```
(function(形参){函数体})(实参);
(function(形参){函数体}(实参));//两种方式必须加;
```

### 回调函数

**回调函数是一种在编程中常用的概念，它允许将一个函数作为参数传递给另一个函数，并在后者执行完毕后执行。这种机制让程序具有更大的灵活性和解耦能力。**

**回调函数的工作原理**

**在编程中，回调函数通常用于异步操作，例如网络请求或文件处理。当主函数需要执行一个可能耗时的操作时，它不会直接执行这个操作，而是将其作为回调函数传递给另一个处理函数。这样，主函数可以继续执行其他任务，而不必等待耗时操作完成。一旦耗时操作完成，回调函数就会被调用。**

**例如，假设有一个函数*A*，它接受另一个函数*B*作为参数。当*A*执行完毕后，它会调用*B*。这里的*B*就是一个回调函数。在JavaScript中，这个过程可能看起来像这样：**

```javascript
// 定义主函数，回调函数作为参数
function A(callback) {
callback();
console.log('我是主函数');
}

// 定义回调函数
function B(){
setTimeout("console.log('我是回调函数')", 3000); // 模仿耗时操作
}

// 调用主函数，将函数B传进去
A(B);

// 输出结果
// 我是主函数
// 我是回调函数
```

**在这个例子中，即使*B*函数模拟了一个耗时的操作（通过*setTimeout*），*A*函数也不会等待它完成就继续执行。这就是回调函数的一个关键特性：它允许程序继续运行，而不会被阻塞。**

**回调函数的优势**

**使用回调函数的主要优势是解耦。它允许将具体的操作从执行环境中分离出来，使得代码更加灵活和可重用。例如，在一个下载任务中，下载进度的更新可能需要通过回调函数来实现，因为下载模块不应该知道显示模块的具体实现细节。**

**此外，回调函数还可以帮助处理异步操作，使得程序可以在等待某个操作完成时继续执行其他任务。这在处理网络请求或大型文件时尤其有用。**

**回调函数的使用场景**

**回调函数通常用于以下场景：**

**异步操作，如网络请求或文件读写。事件处理，如用户界面中的按钮点击。定时器函数，如定时更新数据。**

## 对象（object）

### 对象使用

```
let 对象名 = {}
let 对象名 = new Object()
```

```
let 对象名 = {
	属性名:属性值,
	方法名:函数
}
```

#### 查询对象

```
对象名.属性
对象名['属性名']//当属性名带有字符串时
```

#### 修改对象

```
对象名.属性=新值
```

#### 增加属性

```
对象名.新属性名=新值
```

#### 删除属性

```
delete 对象名.属性
```

### 对象的方法

```
let 对象名 = {
	name:'andy',
	属性名:function(){}
	//属性名(){}
}
对象名.方法名(参数)
```

### 遍历对象

```
let obj={
	uname:'andy',
	age=18,
	sex='男'
}
for(let k in obj){
	console.log(k)//打印属性名
	console.log(obj[k])//打印属性值
}//for in也可以遍历数组,k代表下标，是字符串类型的0 1 2
```

### JSON

定义：通过javascript对象标记法书写的文本,经常作为数据载体在网络中进行传输，本质是字符串

```
{
	"name":"Tom",
	"age":20
}
```

数据类型：数字直接直接定义，字符串在双引号中定义，逻辑值true,false,数组在方括号中，对象花括号，null

JSON字符串转换为js对象

```
var jsObject=JSON.parse(userStr)
```

js对象转化为JSON字符串

```
var jsonStr=JSON.stringify(jsObject)
```



### 内置对象

#### Math

详见mdn文档

| 函数            | 功能                                |
| --------------- | ----------------------------------- |
| random          | 生成0-1之间的随机数（包含0不包含1） |
| ceil            | 向下取整                            |
| floor           | 向上取整                            |
| max（多个参数） | 最大值                              |
| min（多个参数） | 最小值                              |
| pow             | 幂运算                              |
| abs             | 绝对值                              |
| round           | 四舍五入                            |

**注：生成n-m之间的随机整数**

```
Math.flour(Math.random()*(m-n+1)+n)
```

## 变量声明

**建议优先const,然后let**

**注意：**

```
const arr=['res','blue']
arr.push('white')//不报错，本质是一个指针，存储的是地址，地址没变，所以不会报错，对象同理

const name=[]
name=[1,2]//此时会报错，地址改变
const obj={}
obj={
	UNAME='PINK'
}//此时也会报错，地址改变
```

## WebApi

### 作用和分类

作用：就是使用js去操作html和浏览器

分类：DOM（文档对象模型），BOM（浏览器对象模型）

### BOM

#### Window对象

```
//获取
Window.属性
Window.方法()
```

属性：

​	 history:对History对象的只读引用

​	location:用于窗口或框架的Location对象

​	navigator:对于Navigator对象的只读引用

方法：
	alert():显示一段消息和一个确认按钮的警告框

​	confirm():显示带有一段消息以及确认按钮的和取消按钮的对话框

​	setnterval(函数名，数字):按照指定的周期（以毫秒计算）来调用	函数或计算达式

​	setTimeout(函数名，数字):在指定的毫秒数后调用函数或计算表	达式

#### Location对象

```
//获取
window.location.属性
location.属性
```

属性：

​	href:设置或返回完整的URL

### DOM

#### 基本概念

将标记语言的各个组成部分分装成对应的对象

Document:整个文档对象

Element:元素对象

Attribute:属性对象

Text:文本对象

Comment:注释对象

#### 获取DOM元素

##### 根据CSS选择器获取DOM元素

```
document.querySelector('css选择器')
```

注意：
CSS怎么查找对应标签的，这里怎么写，优先返回匹配的第一个，可以直接修改

```
document.querySelectorAll('css选择器')//选取匹配到的所有标签，返回的是一个伪数组，不能单个修改
```

伪数组：
有长度，有索引号，但是没有push(),pop()方法，想要得到每一个元素，则需要for遍历获得

##### 其它获取方式

```
document.getElementById('id')//根据id获取，返回单个对象
document.getElementsByTagName('div')//根据标签获取，返回一个对象数组
document.getElementsByClassName('w')//根据类名获取元素，返回一个对象数组
document.getElementByName("hobby")//根据name属性值获取，返回一个对象数组
```

##### 修改元素内容

获取文字内容：元素.innerText（显示纯文本，不解析标签）

​							元素.innerHTML（会解析标签）



##### 操作元素常用属性

对象（元素）.属性=值



##### 操作元素样式属性

**通过style属性操作CSS:**对象.style.样式属性=值（别忘了跟单位）

**通过类名修改样式：**元素.className=值（可以将这个标签的属性直接修改成这个类的属性值，相当于加这个类在这个标签上，会覆盖原先的类名，如果要保留，可以用写两个类的写法，类名+" "+类名）

**通过classList操作类控制CSS**：

```
元素.classList.add('类名')//添加一个类
元素.classList.remove('类名')//删除一个类
元素.classList.toggle('类名')//切换一个类，有就删除，没有就加上
```

##### 操作表单元素属性

表单.属性名=值

获取表单里的值用的是value

表单里的有些属性，添加就有效果，移除就没有效果，如果为true代表添加了该属性，false代表移除了，比如：disabled,checked,selected

##### 自定义属性

定义方式：data-自定义属性，在标签上以data-开头

在DOM对象上一律以 元素.database 方式获取自定义对象集合，元素.databse.属性名（不带data-）

### 定时器-间歇函数

开启定时器

```
setINterval(函数,间隔时间)
```

作用：每隔多长时间调用这个函数

单位：毫秒

注意：写的是函数名，不要加（）,函数执行不是立即开始，是经过指定间隔时间后开始执行，或者写一个匿名函数放在里面

返回值：返回的是id数值

关闭定时器

```
let 变量名 = setInterval(函数名，间隔时间)
clearInterval(变量名)
```

### 事件绑定

```
//方法一：通过Html标签的事件属性进行绑定
<input type="button" onclick="on()" value="按钮1">

<script>
	function on(){
		alert("我点击了")
	}
</script>
```

```
//方法2：通过Dom元素进行绑定
//方法一：通过Html标签的事件属性进行绑定
<input type="button" onclick="on()" value="按钮1" id='btn'>

<script>
	document.getElementById("btn").onclick = function on(){
		alert("我点击了")
	}
</script>
```

| 事件名      | 说明                                           |
| ----------- | ---------------------------------------------- |
| onclick     | 鼠标单击事件                                   |
| omblur      | 元素失去焦点（输入框中的光标闪动就是获得焦点） |
| onfocus     | 元素获得焦点                                   |
| onload      | 某个页面或图像被完成加载                       |
| onsubmit    | 当表单提交时触发该事件                         |
| onkeydown   | 某个键盘的键被按下时                           |
| onmouseover | 鼠标移到某个元素之上                           |
| onmouseout  | 鼠标从某元素移开                               |



### 事件监听

**语法**

```
元素对象.addEventListener('事件类型',要执行的函数)
```

**事件监听三要素**

**事件源：**哪个dom元素被事件触发了，要获取dom元素

**事件类型**：鼠标点击click,鼠标经过mouseover,鼠标进入mouseenter,鼠标离开mouseleave

**事件调用的函数**：要做什么事，写法同间歇函数

补充：传统调用

```
元素.onclick=function(){}//设置监听行为
元素.onclick()//行为触发
```

**焦点事件**：focus获得焦点 blur失去焦点

**键盘事件**：keydown 键盘按下触发 keyup键盘抬起触发 

**文本事件** ：input用户输入事件                                                               



### 事件对象

存储对象里有事件触发时的相关信息，绑定的回调函数的第一个参数就是事件对象

属性：type:获取当前事件的类型

clientX/clientY:获取光标相对于浏览器可见窗口左上角的位置

offsetX/offsetY:获取光标相对于当前dom元素左上角的位置

key:用户按下的键盘键的值

### 环境对象

指的是函数内部特殊的变量this,它代表着函数运行的环境

### 回调函数

当一个函数当参数来传递给另外一个函数的时候，这个函数就是回调函数

### 事件流

定义：是事件完整执行的过程中的流动路径

捕获阶段从大到小，冒泡阶段从小到大

**事件捕获**:DOM.addEventListener(事件类型，事件处理函数，是否使用捕获机制),true捕获阶段触发，false冒泡阶段触发,默认值是false

**事件冒泡**：当一个元素触发事件后，会依次向上调用所有父级元素的同名事件

**阻止冒泡和捕获：**

```
事件对象.stopPropagation()
```

****

**解绑事件**

on事件方式=null覆盖即可

传统on只有冒泡没有捕获

removeEventListener(事件类型，事件处理函数)

匿名函数无法解绑

### 事件委托

优点：减少注册次数，可以提高程序性能

原理：利用事件冒泡的特点，给父元素注册事件，当我们触发子元素时，会冒泡到父元素触发父元素的事件

补充：事件对象.target，在事件委托中，可以获取在父元素被冒泡触发时，触发的子元素的对象

### 阻止默认行为

事件对象.preventDefault()

### 其他事件

#### 页面加载事件

##### 加载外部资源结束触发的事件

事件名：load

给所有页面加页面加载事件：window.addEventListener('load',function(){})

##### 当初始HTML文档加载完触发的事件

事件名：DOMContentLoaded

#### 元素滚动事件

事件名：scroll

相关属性：scrollLeft和scrollTop(卷轴左边或者上边隐藏的部分)

整个html标签对象:document.documentElement

#### 页面尺寸事件

**窗口尺寸改变**：resize

**元素宽高的获取属性**：clientWidth,clientHeight,注意宽高不包含border和滚动条

包含padding,border：offsetWidth,offsetHeight

获取位置：offsetLeft,offsetTop,只读属性（获取距离自己最近的定位父级元素顶上/左边的位置）

### 日期对象

#### 实例化

```
const date=new Date()//创建一个当前时间
const date=new Date('2000-5-5 08:20:20')//获取一个指定的时间
```

**注意：以下方法全部基于Date类**

#### 日期对象方法

| 方法          | 作用               | 说明                 |
| ------------- | ------------------ | -------------------- |
| getFullYear() | 获得年份           | 获取四位年份         |
| getMonth()    | 获得月份           | 取值为0-11           |
| getDate()     | 获取月份中的每一天 | 不同月份的取值也不同 |
| getDay()      | 获取星期           | 取值0-6              |
| getHours()    | 获取小时           | 取值0-23             |
| getMinutes()  | 获取分钟           | 取值0-59             |
| getSeconds()  | 获取秒             | 取值0-59             |

```
toLocaleString()//获取格式如下2022/4/1 08:01:01
toLocalDateString()//获取格式如下2022/04/01
```

#### 时间戳

定义：自1970年01月01日00时00分010秒起的毫秒数，1s=1000ms

获取时间戳的方法

```
getTime()//调用
+new Date()//此方法不用在前面加类名，实例化
Date.now()//静态方法
```

### 节点操作

#### 节点分类

元素节点：所有标签

属性节点：所有属性

文本节点，所有文本

其他...

#### 查找节点

**父节点查找**

```
子元素.parentNode//返回最近一级的父节点，没有返回null
```

**子节点的查找**

```
父元素.children//仅获得所有元素节点，返回的是一个伪数组
```

**兄弟关系查找**

```
元素.nextElementSibling//下一个兄弟节点
元素.previousElementSibling//上一个兄弟节点
```

#### 增加节点

```
document.createElement('标签名')//创建节点
父元素.appendChild(待插入的元素)//插入父元素的最后面
父元素.insertBefore(要插入的元素，在哪个元素的前面)//插入到某个子元素的前面
```

#### 克隆节点

```
元素.cloneNode(布尔值)
```

true:包含后代节点一起克隆

false，则代表克隆时不包含后代节点，默认值为false

#### 删除节点

```
父元素.removeChild(要删除的元素)
```

注：不存在父子关系则删除不成功

删除和隐藏有区别

### m端事件（移动端事件）

| 触屏touch事件 | 说明                       |
| ------------- | -------------------------- |
| touchstart    | 触摸dom元素触发            |
| touchmove     | 在dom元素上滑动时触发      |
| touchend      | 从dom 元素上移开时才会触发 |

#### swiper插件的使用

官网下载，然后在项目中引用文件路径

### Window对象

**Bom**：浏览器对象模型

window对象是一个全局对象，也是js中的顶级对象

document,alert这些都是window属性，基本bom的属性和方法都是window

所有var定义在全局作用域的变量，函数都会变成window对象的属性和方法

window对象的属性和方法调用的时候可以省略window

#### 延迟函数

代码延迟执行的函数

```
setTimeout(回调函数，等待的毫秒数)//仅执行一次，这是与间歇函数的不同
```

#### js执行机制

js语言一大特点就是单线程，也就是同一个事件只能做一件事，同一时间只能做一件事

**同步任务**：在主线程上执行，形成一个执行栈

**异步任务**：有以下三种类型

普通事件：如Click，resize,

资源加载，如load,error

定时器：如setInterval,setTimeout

异步任务添加到任务队列

执行顺序：先执行栈中的同步任务，然后异步任务放入任务队列，一旦栈中的所有同步任务执行完毕，系统就会依次读取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入栈，开始执行

#### location对象

location的数据类型是对象，它拆分并保存了url地址的各个部分

**常用属性和方法**

href属性获取完整的url地址，对其赋值时用于地址的跳转

```
location.href='网址'//实现页面自动跳转
```

# Vue

## Vue快速入门

在js代码区域，创建Vue核心对象，定义数据模型

**Vue2中定义**

```
<script>
	new Vue({
		el:"#app",//Vue接管的区域
		data:{
			message:"Hello Vue"
		}
	})
</script>
```

**Vue3中定义**

```
<script>
    const app = Vue.createApp({
        data(){
            return {
                message:'Hello Vue!'
            }
        }
    })
    app.mount('#app')
</script>
```

编写视图

```
<div id="app">
	<input type="text" v-model="message">
	{{message}}
</div>
```

**注意：Vue是双向数据绑定，视图层的数据变化会影响数据模型，数据模型的变化又会影响视图层的数据变化**

## 前端工程创建

### **环境要求**

**node.js(前端项目的运行环境) npm(JavaScript包管理工具) Vue CLI(基于VUE进行快速开发的完整系统，实现交互式的项目脚手架)**

### **创建工程**

**在项目所在的文件夹下打开cmd,输入如下指令**

```  
vue create 项目名称
```

**也可以使用如下指令打开网页进行工程的创建**

```
vue ui
```

### **项目结构**

**node_modules:当前项目依赖的js包**

**assets:静态资源存放目录**

**components:公共组件存放目录**

**App.vue:项目的主组件，页面的入口文件**

**main.js:整个项目的入口文件**

**package.json:项目的配置信息，依赖包管理**

**vue.config,js:vue-cli的配置文件**

### 项目启动

```
npm run serve
```

### 修改端口号

**在vue.config.js文件中进行如下调整**

**原配置文件**

```json
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true
})
```

**修改后的文件**

```json
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  devServer: {
    port: 7070
  }
})
```



## 插值表达式

**形式：{{}}**

**内容：变量，三元运算符，函数调用，算数运算**

**作用：用于绑定data方法返回的对象属性**

## Vue常见指令

**指令：带有v-前缀的通常都是Vue指令**

| 指令      | 作用                                                         |
| --------- | ------------------------------------------------------------ |
| v-bind    | 为html标签绑定属性值，如设置href,css样式等，用法v-bind:xxx = ""或者:xxx = "",xxx指属性 |
| v-model   | 为表单输入项和data方法中的属性创建双向数据绑定，用法v-model = ""，双向绑定指任意一方改变都会同步给另一方 |
| v-on      | 为html标签绑定事件,用法v-on:xxx = ""或者@xxx = ""，xxx指属性 |
| v-if      |                                                              |
| v-else-if | 条件性的渲染某元素，判定为true时渲染，否则不渲染，用法v-if="" v-lese-if = "" v-else |
| v-else    |                                                              |
| v-show    | 根据条件展示某元素，区别在于切换的是display属性的值,v-show = "" |
| v-for     | 列表渲染，遍历容器的元素或者对象的属性,用法v-for=""          |

```
<a v-bind:href="url"></a>
<a :href="url"></a>
<script>
    //定义Vue对象
    new Vue({
        el: "#app", //vue接管区域
        data:{
           url=""
        }
    })
</script>

```



```
<input type="button" value="按钮" v-on:click="handle()">
<input type="button" value="按钮" @click="handle()">

<script>
    //定义Vue对象
    new Vue({
        el: "#app", //vue接管区域
        data:{
           
        },
        methods: {
            handle:function(){
            	alert("我被点击了")
            }
            //也可以简写成以下形式
            handle(){
            	alert("我被点击了")
            }
        }
    })
</script>
```



```
<span v-if="age <= 35">年轻人(35及以下)</span>
<span v-else-if="age > 35 && age < 60">中年人(35-60)</span>
<span v-else>老年人(60及以上)</span>

<script>
    //定义Vue对象
    new Vue({
        el: "#app", //vue接管区域
        data:{
           age: 20
        },
        methods: {
            
        }
    })
</script>


<span v-show="age <= 35">老年人(60及以上)</span>
```



```
<div id="app">
	<div v-for="addr in addrs">{{addr}}</div>
	<div v-for="(addr,index) in addrs" >{{index+1}}:{{addr}}</div>
</div>

    
</body>
<script>
    //定义Vue对象
    new Vue({
        el: "#app", //vue接管区域
        data:{
           addrs:["北京", "上海", "西安", "成都", "深圳"]
        },
        methods: {
            
        }
    })
</script>
```



## Vue的生命周期

**生命周期：指一个对象从创建到销毁的整个过程，生命周期一共分为8个阶段，没触发一个生命周期事件埃，会自动执行一个生命周期方法，称为钩子方法，方法名就是生命周期的名字**

| 状态          | 阶段周期 |
| ------------- | -------- |
| brforeCreate  | 创建前   |
| created       | 创建后   |
| beforeMount   | 挂载前   |
| mounted       | 挂载后   |
| beforeUpdate  | 更新前   |
| updated       | 更新后   |
| beforeDestroy | 销毁前   |
| destroyed     | 销毁后   |

```
<script>
    //定义Vue对象
    new Vue({
        el: "#app", //vue接管区域
        data:{
           
        },
        methods: {
            
        },
        mounted () {
            alert("vue挂载完成,发送请求到服务端")
        }
    })
</script>
```

## Ajax

**概念：Asynchronous Javascript And XML,异步的JavaScript和XML**

**作用：**

​	**数据交换：通过Ajax可以给服务器发送请求，并获取服务器响应的数据**

​	**异步交互：可以在不重新加载整个页面的情况下，与服务器交换数据并更新部分网页的技术**

**原生的Ajax请求：**

```
<script>
    function getData(){
        //1. 创建XMLHttpRequest 
        var xmlHttpRequest  = new XMLHttpRequest();
        
        //2. 发送异步请求
        xmlHttpRequest.open('GET','http://yapi.smart-xwork.cn/mock/169327/emp/list');
        xmlHttpRequest.send();//发送请求
        
        //3. 获取服务响应数据
        xmlHttpRequest.onreadystatechange = function(){
            if(xmlHttpRequest.readyState == 4 && xmlHttpRequest.status == 200){
                document.getElementById('div1').innerHTML = xmlHttpRequest.responseText;
            }
        }
    }
</script>
```

## Axios

**安装环境**

```
npm install axios
```

**导入**

```
import axios from 'axios'
```

**使用Axios发送请求，并获取响应结果**

```
<script>
    function get(){
        //通过axios发送异步请求-get
        // axios({
        //     method: "get",
        //     url: "http://yapi.smart-xwork.cn/mock/169327/emp/list"
        // }).then(result => {
        //     console.log(result.data);
        // })


        axios.get("http://yapi.smart-xwork.cn/mock/169327/emp/list").then(result => {
            console.log(result.data);
        })
    }

    function post(){
        //通过axios发送异步请求-post
        // axios({
        //     method: "post",
        //     url: "http://yapi.smart-xwork.cn/mock/169327/emp/deleteById",
        //     data: "id=1"
        // }).then(result => {
        //     console.log(result.data);
        // })

        axios.post("http://yapi.smart-xwork.cn/mock/169327/emp/deleteById","id=1").then(result => {
            console.log(result.data);
        })
    }
</script>

```

**或者也可以这样写**

```
  methods: {
    handleSend() {
      axios
        .post("/api/admin/employee/login", {
          username: "admin",
          password: "123456",
        })
        .then((res) => {
          console.log(res);
        })
        .catch((err) => {
          console.log(err.response);
        });
    },
  },
};
```



```
handleSendGet() {
      axios
        .get("/api/admin/shop/status", {
          headers: {
            token:
      "eyJhbGciOiJIUzI1NiJ9.eyJlbXBJZCI6MSwiZXhwIjoxNzMxMDAxMzAzfQ.fmdvv3ODQ3xxaRGjTAgwex9iqfpUXQiKPMCdeaRkG-M",
          },
        })
        .then((res) => {
          console.log(res);
        });
    },
```

**以下是axios的请求时的所有可配置属性**

```
axios({
  // `url` 是用于请求的服务器 URL
  url: '/user',

  // `method` 是创建请求时使用的方法
  method: 'get', // 默认值

  // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
  // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
  baseURL: 'https://some-domain.com/api/',

  // `transformRequest` 允许在向服务器发送前，修改请求数据
  // 它只能用于 'PUT', 'POST' 和 'PATCH' 这几个请求方法
  // 数组中最后一个函数必须返回一个字符串， 一个Buffer实例，ArrayBuffer，FormData，或 Stream
  // 你可以修改请求头。
  transformRequest: [function (data, headers) {
    // 对发送的 data 进行任意转换处理

    return data;
  }],

  // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
  transformResponse: [function (data) {
    // 对接收的 data 进行任意转换处理

    return data;
  }],

  // 自定义请求头
  headers: {'X-Requested-With': 'XMLHttpRequest'},

  // `params` 是与请求一起发送的 URL 参数
  // 必须是一个简单对象或 URLSearchParams 对象
  params: {
    ID: 12345
  },

  // `paramsSerializer`是可选方法，主要用于序列化`params`
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function (params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },

  // `data` 是作为请求体被发送的数据
  // 仅适用 'PUT', 'POST', 'DELETE 和 'PATCH' 请求方法
  // 在没有设置 `transformRequest` 时，则必须是以下类型之一:
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - 浏览器专属: FormData, File, Blob
  // - Node 专属: Stream, Buffer
  data: {
    firstName: 'Fred'
  },
  
  // 发送请求体数据的可选语法
  // 请求方式 post
  // 只有 value 会被发送，key 则不会
  data: 'Country=Brasil&City=Belo Horizonte',

  // `timeout` 指定请求超时的毫秒数。
  // 如果请求时间超过 `timeout` 的值，则请求会被中断
  timeout: 1000, // 默认值是 `0` (永不超时)

  // `withCredentials` 表示跨域请求时是否需要使用凭证
  withCredentials: false, // default

  // `adapter` 允许自定义处理请求，这使测试更加容易。
  // 返回一个 promise 并提供一个有效的响应 （参见 lib/adapters/README.md）。
  adapter: function (config) {
    /* ... */
  },

  // `auth` HTTP Basic Auth
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },

  // `responseType` 表示浏览器将要响应的数据类型
  // 选项包括: 'arraybuffer', 'document', 'json', 'text', 'stream'
  // 浏览器专属：'blob'
  responseType: 'json', // 默认值

  // `responseEncoding` 表示用于解码响应的编码 (Node.js 专属)
  // 注意：忽略 `responseType` 的值为 'stream'，或者是客户端请求
  // Note: Ignored for `responseType` of 'stream' or client-side requests
  responseEncoding: 'utf8', // 默认值

  // `xsrfCookieName` 是 xsrf token 的值，被用作 cookie 的名称
  xsrfCookieName: 'XSRF-TOKEN', // 默认值

  // `xsrfHeaderName` 是带有 xsrf token 值的http 请求头名称
  xsrfHeaderName: 'X-XSRF-TOKEN', // 默认值

  // `onUploadProgress` 允许为上传处理进度事件
  // 浏览器专属
  onUploadProgress: function (progressEvent) {
    // 处理原生进度事件
  },

  // `onDownloadProgress` 允许为下载处理进度事件
  // 浏览器专属
  onDownloadProgress: function (progressEvent) {
    // 处理原生进度事件
  },

  // `maxContentLength` 定义了node.js中允许的HTTP响应内容的最大字节数
  maxContentLength: 2000,

  // `maxBodyLength`（仅Node）定义允许的http请求内容的最大字节数
  maxBodyLength: 2000,

  // `validateStatus` 定义了对于给定的 HTTP状态码是 resolve 还是 reject promise。
  // 如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，
  // 则promise 将会 resolved，否则是 rejected。
  validateStatus: function (status) {
    return status >= 200 && status < 300; // 默认值
  },

  // `maxRedirects` 定义了在node.js中要遵循的最大重定向数。
  // 如果设置为0，则不会进行重定向
  maxRedirects: 5, // 默认值

  // `socketPath` 定义了在node.js中使用的UNIX套接字。
  // e.g. '/var/run/docker.sock' 发送请求到 docker 守护进程。
  // 只能指定 `socketPath` 或 `proxy` 。
  // 若都指定，这使用 `socketPath` 。
  socketPath: null, // default

  // `httpAgent` and `httpsAgent` define a custom agent to be used when performing http
  // and https requests, respectively, in node.js. This allows options to be added like
  // `keepAlive` that are not enabled by default.
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // `proxy` 定义了代理服务器的主机名，端口和协议。
  // 您可以使用常规的`http_proxy` 和 `https_proxy` 环境变量。
  // 使用 `false` 可以禁用代理功能，同时环境变量也会被忽略。
  // `auth`表示应使用HTTP Basic auth连接到代理，并且提供凭据。
  // 这将设置一个 `Proxy-Authorization` 请求头，它会覆盖 `headers` 中已存在的自定义 `Proxy-Authorization` 请求头。
  // 如果代理服务器使用 HTTPS，则必须设置 protocol 为`https`
  proxy: {
    protocol: 'https',
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },

  // see https://axios-http.com/zh/docs/cancellation
  cancelToken: new CancelToken(function (cancel) {
  }),

  // `decompress` indicates whether or not the response body should be decompressed 
  // automatically. If set to `true` will also remove the 'content-encoding' header 
  // from the responses objects of all decompressed responses
  // - Node only (XHR cannot turn off decompression)
  decompress: true // 默认值

})
```





**get和post的区别：Get是向服务器发索取数据的一种请求，而Post是向服务器提交数据的一种请求**

| 请求                             |
| -------------------------------- |
| axios.get(url[,config])          |
| axios.delete(url[,config])       |
| axios.head(url[,config])         |
| axios.options(url[,config])      |
| axios.post(url[,data[,config]])  |
| axios.put(url[,data[,config]])   |
| axios.patch(url[,data[,config]]) |

**[]里面的参数代表可选参数，调用的时候可以传也可以不传**

**参数列表**

**url:请求路径**

**data:请求体数据，最常见的JSON格式数据**

**config:配置对象，可以查询参数，请求头信息**

**跨域问题：当一个请求url的协议、域名、端口三者之间任意一个与当前页面url不同即为跨域**

**为了解决跨域问题我们在vue.config.js文件中可以进行如下配置，进行代理操作**

```javascript
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  devServer: {
    port: 7070,
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        pathRewrite: {
          '^/api': ''
        }
      }
    }
  }
})

```

**注：'/api'代表匹配的请求前缀，代码里只有带该前缀的请求才会被进行，但是最终的请求路径里如果不需要这段前缀，则使用pathRewriter去掉，target属性代表代理之后url前面要加的前缀**

**举例"/api/admin/emplyee.login"的实际请求路径是"http://localhost:8080/admin/employee/login"**





## vue组件开发

**概念：vue组件文件以.vue结尾，每个组件由三部分组成： <template>(结构) <script>（逻辑） <style>（样式）**

**数据模型的定义**

```
<script>
  export default{
    data: function{
      return {
        message: "Hello world"
      }
    }
  }
</script>
```

```
<script>
  export default{
    data() {
      return {
        message: "Hello world"
      }
    }
  }
</script>
```

**数据模型的使用**

```
<template>
  <div>
    <h1>{{message}}</h1>
    
  </div>
</template>
```

## Element

**给当前项目安装**

```
npm i element -ui -s
```

**在Main.js引入Element组件库**

```
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
//全局使用element ui
Vue.use(ElementUI);
```

**新建ElementView.vue组件**

```
<template>
    <div>
        <el-row>
            <!--button按钮-->
            <el-button>默认按钮</el-button>
            <el-button type="primary">主要按钮</el-button>
            <el-button type="success">成功按钮</el-button>
            <el-button type="info">信息按钮</el-button>
            <el-button type="warning">警告按钮</el-button>
            <el-button type="danger">危险按钮</el-button>
        </el-row>
    </div>
</template>

<script>
    export default{
        
    }

</script>

<style>

</style>
```

**在App.vue中进行组件引用，只需要使用ElementView标签即可**

```
<template>
  <div>
    <element-view>

    </element-view>
    
  </div>
</template>

<script>
  import ElementView from './views/element/ElementView.vue'
  export default{
  components: { ElementView },
    data() {
      return {
        
      }
    }
  }

</script>

<style>

</style>

```

## Vue路由

**安装：`npm install vue-router`**

**前端路由：URL中的hash(#号)与组件之间的对应关系**

**组成：**

**VueRouter：路由器类，根据路由请求在路由视图中动态渲染选中的组件**

**<router-link>：请求链接组件，浏览器会解析成<a>**

**<router-view>：动态视图组件，用来渲染展示与路由路径对应的组件**

**router文件夹下index.js文件的内容**

```
import Vue from 'vue'
import VueRouter from 'vue-router'
import HomeView from '../views/HomeView.vue'

Vue.use(VueRouter)

const routes = [
  {
    path: '/',
    name: 'home',
    component: HomeView
  },
  {
    path: '/about',
    name: 'about',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import(/* webpackChunkName: "about" */ '../views/AboutView.vue')
  }
]

const router = new VueRouter({
  routes
})

export default router

```

**在App.vue中使用<router-link></router-link>组件实现页面跳转**

```
<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>

```



**也可以在App.vue中实现编程式路由跳转**

```
<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <input type="button" value="编程式路由跳转" @click="jump" />
    </nav>
    <router-view />
  </div>
</template>

<script>
export default {
  methods: {
    jump() {
      this.$router.push({ path: "/about" });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>

```

**重定向属性的使用**

**场景需求：假设我们需要对所有不存在的请求资源做处理，则可以用一下的方法去实现**

```
import Vue from 'vue'
import VueRouter from 'vue-router'
import HomeView from '../views/HomeView.vue'

Vue.use(VueRouter)

const routes = [
  {
    path: '/',
    name: 'home',
    component: HomeView
  },
  {
    path: '/about',
    name: 'about',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import(/* webpackChunkName: "about" */ '../views/AboutView.vue')
  },
  {
    path: '/404',
    component: () => import('../views/404View.vue')
  },
  {
    path: '*',
    redirect: '/404'
  }
  
]

const router = new VueRouter({
  routes
})

export default router
```

**代码解释：这里当访问路径没有匹配到时，就会自动匹配到'*'路径，此时对该路径请求进行重定向，重定向到/404请求即可**

**通过children属性实现嵌套路由**

```
const routes = [
  {
    path: '/c',
    component: () => import('../views/container/ContainerView.vue'),
    children: [
      {
        path: '/c/p1',
        component: () => import('../views/container/P1View.vue')
      },
      {
        path: '/c/p2',
        component: () => import('../views/container/P2View.vue')
      },
      {
        path: '/c/p3',
        component: () => import('../views/container/P3View.vue')
      }
    ]
  },  
]
```



**[vue-router（路由）详细教程_vue 路由-CSDN博客](https://blog.csdn.net/wulala_hei/article/details/80488727)**

## Vue x

**Vue x是一个专门为Vue.js应用程序开发的状态管理库**

**Vue x可以在多个组件之间共享数据，并且共享的数据是响应式，即数据的变更能及时渲染到模板**

**Vue x采用集中式存储管理所有组件的状态**

### 核心概念

**state:状态对象，集中定义各个组件共享的数据**

**mutations:类似于一个事件，用于修改共享数据，要求必须是同步函数**

**actions:类似于mutation,可以包含异步操作，通过调用mutation来改变共享数据**

### 使用

**在store文件夹下的index.js**

```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    name: '未登录游客'
  },
  getters: {
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  }
})

```

**如果要在App.vue文件下使用则可以用以下方式**

```
<template>
  <div id="app">
    <nav>
      <div>{{$store.state.name}}</div>
    </nav>
    <router-view />
  </div>
</template>
```

**mutations属性的使用，首先在mutations中设置一个函数用于修改数据**

```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    name: '未登录游客'
  },
  getters: {
  },
  mutations: {
    setName(state, newName) {
      state.name = newName
    }
  },
  actions: {
  },
  modules: {
  }
})

```

**在App.vue中调用mutations中的方法进行数据的修改**

```
<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <input type="button" value="通过mutations修改数据" @click="handleUpdate" />
      <div>{{$store.state.name}}</div>
    </nav>
  </div>
</template>

<script>
export default {
  methods: {
    handleUpdate() {
      this.$store.commit('setName','Joker')
      //commit函数的参数含义，第一个参数代表要调用的函数名字，第二个代表调用的函数的第二个参数，待调用的函数的第一个参数是state,会自动传入
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>

```

**使用mutations进行异步后端请求修改数据的操作**

**在store文件夹下的index.js文件中进行如下修改**

```
import axios from 'axios'
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    name: '未登录游客'
  },
  getters: {
  },
  mutations: {
    setName(state, newName) {
      state.name = newName
    }
  },
  actions: {
    setNameByAxios() {
      axios({
        url: '/api/admin/employee/login',
        method: 'post',
        data: {
          username: 'admin',
          password: '123456'
        }
      }).then(res => {
        if(res.data.code == 1){
          this.commit('setName', res.data.data.name)
        }
      })
    }
  },
  modules: {
  }
})

```

**在App.vue中调用mutations中的函数**

```
<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <input type="button" value="通过mutations修改数据" @click="handleUpdate" />
      <input type="button" value="通过actions修改数据" @click="handleUpdate2" />
      <div>{{$store.state.name}}</div>
    </nav>
  </div>
</template>

<script>
export default {
  methods: {
    handleUpdate() {
      this.$store.commit('setName','Joker')
    },
    handleUpdate2() {
      this.$store.dispatch('setNameByAxios')//调用mutations中的函数，参数含义跟上面action一致
    }
  },
};
</script>
```



## nginx

**运行npm脚本build，然后将dist文件夹下的文件复制到nginx下的html文件即可**

**nginx反向代理的好处：提高访问速度，进行负载均衡，保证后端服务的安全**

**反向代理和负载均衡的配置**

```nginx.conf
server{
	listen 80;
	server_name localhost;
	location/api/{
		proxy_pass http://localhost:8080/admin/;
	}
}
```



```nginx.conf
upstream webserver{
	server 192.168.100.128:8080;
	server 192.168.100.129:8080;
}


server{
	listen 80;
	server_name localhost;
	location/api/{
		proxy_pass http://webserver/admin/;
	}
}
```

**nginx负载均衡策略**

| 名称       | 说明                                                   |
| ---------- | ------------------------------------------------------ |
| 轮询       | 默认方式                                               |
| weight     | 权重方式，默认为1，权重越高，被分配的客户端请求越多    |
| ip_hash    | 依据ip分配方式，这样每个访客可以固定访问一个后端服务   |
| least_conn | 依据最少连接方式，把请求优先分配给连接数少的后端服务   |
| url_hash   | 依据url分配方式，这样相同的url会被分配到同一个后端服务 |
| fair       | 依据响应时间方式，响应时间短的服务将会被优先分配       |

# 微信小程序开发

## 入门案例

**主体部分**

| 文件     | 必需 | 作用             |
| -------- | ---- | ---------------- |
| app.js   | 是   | 小程序逻辑       |
| app.json | 是   | 小程序公共配置   |
| app.wxss | 否   | 小程序公共样式表 |

**文件类型**

| 文件类型 | 必需 | 作用       |
| -------- | ---- | ---------- |
| js       | 是   | 页面逻辑   |
| wxml     | 是   | 页面结构   |
| json     | 否   | 页面配置   |
| wxss     | 否   | 页面样式表 |

## 展示文字数据

```javascript
// index.js
Page({
  data:{
    msg:'hello world'
  }
})
```

```xml
<!--index.wxml-->
<navigation-bar title="Weixin" back="{{false}}" color="black" background="#FFF"></navigation-bar>
<scroll-view class="scrollarea" scroll-y type="list">
  <view class="container">
    {{msg}}
  </view>
</scroll-view>
```

## 点击按钮获取用户信息

```javascript
// index.js
Page({
  data:{
    msg:'hello world'
  },
  //获取威信用户的头像和名称
  getUserInfo(){
    wx.getUserProfile({
      desc: '获取用户信息',
      success: (res)=>{
        console.log(res.userInfo);
      }
    })
  }
})

```

```xml
<!--index.wxml-->
<navigation-bar title="Weixin" back="{{false}}" color="black" background="#FFF"></navigation-bar>
<scroll-view class="scrollarea" scroll-y type="list">
  <view class="container">
    <view>{{msg}}</view>
    <view>
    <button bindtap="getUserInfo" type="primary">获取用户信息</button>
    </view>
  </view>
</scroll-view>

```

## 将获取的数据传给data

```javascript
// index.js
Page({
  data:{
    msg:'hello world',
    nickName:''
  },
  //获取威信用户的头像和名称
  getUserInfo(){
    wx.getUserProfile({
      desc: '获取用户信息',
      success: (res)=>{
        console.log(res.userInfo);
        //为数据赋值
        this.setData({
          nickName: res.userInfo.nickName
        })
      }
    })
  }
})

```

```xml
<!--index.wxml-->
<navigation-bar title="Weixin" back="{{false}}" color="black" background="#FFF"></navigation-bar>
<scroll-view class="scrollarea" scroll-y type="list">
  <view class="container">
    <view>{{msg}}</view>
    <view>
      <button bindtap="getUserInfo" type="primary">获取用户信息</button>
      昵称:{{nickName}}
    </view>
  </view>
</scroll-view>

```

## 获取微信用户的授权码

```xml
<!--index.wxml-->
<navigation-bar title="Weixin" back="{{false}}" color="black" background="#FFF"></navigation-bar>
<scroll-view class="scrollarea" scroll-y type="list">
  <view class="container">
    <view>{{msg}}</view>
    <view>
      <button bindtap="getUserInfo" type="primary">获取用户信息</button>
      昵称:{{nickName}}
    </view>
    <view>
      <button type="warn" bindtap="wxLogin">微信登录</button>
      授权码：{{code}}
    </view>
  </view>
</scroll-view>

```

```javascript
// index.js
Page({
  data:{
    msg:'hello world',
    nickName:'',
    code:''
  },
  //获取威信用户的头像和名称
  getUserInfo(){
    wx.getUserProfile({
      desc: '获取用户信息',
      success: (res)=>{
        console.log(res.userInfo);
        //为数据赋值
        this.setData({
          nickName: res.userInfo.nickName
        })
      }
    })
  },

  //微信登录，获取微信用户的授权码
  wxLogin(){
    wx.login({
      success: (res) => {
        console.log(res.code)
        this.setData({
          code: res.code
        })
      }
    })
  }
})

```

## 给后端发送请求

```javascript
// index.js
Page({
  data:{
    msg:'hello world',
    nickName:'',
    code:''
  },
  //获取威信用户的头像和名称
  getUserInfo(){
    wx.getUserProfile({
      desc: '获取用户信息',
      success: (res)=>{
        console.log(res.userInfo);
        //为数据赋值
        this.setData({
          nickName: res.userInfo.nickName
        })
      }
    })
  },

  //微信登录，获取微信用户的授权码
  wxLogin(){
    wx.login({
      success: (res) => {
        console.log(res.code)
        this.setData({
          code: res.code
        })
      }
    })
  },

  sendRequest(){
    wx.request({
      url: 'http://localhost:8080/user/shop/status',
      method:'GET',
      success:(res)=>{
        console.log(res.data)
      }
    })
  }
})

```

```xml
<!--index.wxml-->
<navigation-bar title="Weixin" back="{{false}}" color="black" background="#FFF"></navigation-bar>
<scroll-view class="scrollarea" scroll-y type="list">
  <view class="container">
    <view>{{msg}}</view>
    <view>
      <button bindtap="getUserInfo" type="primary">获取用户信息</button>
      昵称:{{nickName}}
    </view>
    <view>
      <button type="warn" bindtap="wxLogin">微信登录</button>
      授权码：{{code}}
    </view>
    <view>
      <button type = "default" bindtap="sendRequest">发送请求</button>
    </view>
  </view>
</scroll-view>

```

## 登录流程时序

![](D:/StudyNote/assets/api-login.jpg)

**说明**

1. 调用 [wx.login()](https://developers.weixin.qq.com/miniprogram/dev/api/open-api/login/wx.login.html) 获取 **临时登录凭证code** ，并回传到开发者服务器。
2. 调用 [auth.code2Session](https://developers.weixin.qq.com/miniprogram/dev/OpenApiDoc/user-login/code2Session.html) 接口，换取 **用户唯一标识 OpenID** 、 用户在微信开放平台账号下的**唯一标识UnionID**（若当前小程序已绑定到微信开放平台账号） 和 **会话密钥 session_key**。

之后开发者服务器可以根据用户标识来生成自定义登录态，用于后续业务逻辑中前后端交互时识别用户身份。

**注意事项**

1. 会话密钥 `session_key` 是对用户数据进行 [加密签名](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/signature.html) 的密钥。为了应用自身的数据安全，开发者服务器**不应该把会话密钥下发到小程序，也不应该对外提供这个密钥**。
2. 临时登录凭证 code 只能使用一次

**访问code2Session**

**请求方式：get**

**请求路径：https://api.weixin.qq.com/sns/jscode2session**

**请求参数**

| 属性       | 类型   | 必填 | 说明                                                         |
| :--------- | :----- | :--- | :----------------------------------------------------------- |
| appid      | string | 是   | 小程序 appId                                                 |
| secret     | string | 是   | 小程序 appSecret                                             |
| js_code    | string | 是   | 登录时获取的 code，可通过[wx.login](https://developers.weixin.qq.com/miniprogram/dev/api/open-api/login/wx.login.html)获取 |
| grant_type | string | 是   | 授权类型，此处只需填写 authorization_code                    |

**返回参数**

| 属性        | 类型   | 说明                                                         |
| :---------- | :----- | :----------------------------------------------------------- |
| session_key | string | 会话密钥                                                     |
| unionid     | string | 用户在开放平台的唯一标识符，若当前小程序已绑定到微信开放平台账号下会返回，详见 [UnionID 机制说明](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/union-id.html)。 |
| errmsg      | string | 错误信息                                                     |
| openid      | string | 用户唯一标识                                                 |
| errcode     | int32  | 错误码                                                       |

## 微信支付

![](D:/StudyNote/assets/image-20241021224342821.png)

**详细接口文档：https://pay.weixin.qq.com/doc/v3/merchant/4012525110**

**相关maven坐标**

```xml
<!--微信支付-->
<dependency>
    <groupId>com.github.wechatpay-apiv3</groupId>
    <artifactId>wechatpay-apache-httpclient</artifactId>
    <version>0.4.8</version>
</dependency>
```



# Typescript

## 基础介绍

**是javascript的超集，可编译成标准的javascript,并在编译时进行类型检查**

**安装typescript**

```
npm install -g typescript
```

**查看TS版本**

```
tsc -v
```

**编译ts文件**

```
tsc fileName
```

**样例代码**

```typescript
function hello (msg:string) {
	console.log(msg)
}

hello("123")
```

**可以看到唯一的区别就是在变量后面限制了类型，如果类型不匹配，就会报错**

## 常用数据类型

| 类型       | 例                                   | 备注                         |
| ---------- | ------------------------------------ | ---------------------------- |
| 字符串类型 | string                               |                              |
| 数字类型   | number                               |                              |
| 布尔类型   | boolean                              |                              |
| 数组类型   | number[],string[],boolean[],依次类推 |                              |
| 任意类型   | any                                  | 相当于又回到了没有类型的时代 |
| 复杂类型   | type与interface                      |                              |
| 函数类型   | () => void                           | 对函数的参数和返回值进行说明 |
| 字面量类型 | "a"\|"b"\|"c"                        | 限制变量或参数的取值         |
| class类    | class Animal                         |                              |

**标注位置：标注变量，参数，返回值**

**使用方式 ：变量名:类型**

**变量标注，参数标注，返回值标注的使用**

![](D:/StudyNote/assets/image-20230926145517782.png)

**字符串类型，布尔类型，数字类型**

![](D:/StudyNote/assets/image-20230926145634149.png)



**字面量类型的使用**

![](D:/StudyNote/assets/image-20230926145813932.png)



**接口类型的使用**

![](D:/StudyNote/assets/image-20230926150816090.png)



**类的使用**

![](D:/StudyNote/assets/image-20230926151839881.png)

**使用class类关键字来定义类，类中可以包含属性，构造方法，普通方法**

**类实现接口**

![](D:/StudyNote/assets/image-20230926152034526.png)

**类继承类**

![](D:\StudyNote\assets\image-20230926152222634.png)

