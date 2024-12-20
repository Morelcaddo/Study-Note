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

![](assets\api-login.jpg)

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

![](assets\image-20241021224342821.png)

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

![](assets\image-20230926145517782.png)

**字符串类型，布尔类型，数字类型**

![](assets\image-20230926145634149.png)



**字面量类型的使用**

![](assets\image-20230926145813932.png)



**接口类型的使用**

![](assets\image-20230926150816090.png)



**类的使用**

![](assets\image-20230926151839881.png)

**使用class类关键字来定义类，类中可以包含属性，构造方法，普通方法**

**类实现接口**

![](assets\image-20230926152034526.png)

**类继承类**

![](D:\StudyNote\assets\image-20230926152222634.png)





# Spring Boot

## HTTP

**概念：超文本传输协议，规定了浏览器与服务器之间数据传输的规则**

**特点：**

**基于TCP协议：面向连接，安全**

**基于请求-响应模型的：一次请求对应一次响应**

**HTTP协议是无状态的协议，对于事务处理没有记忆能力，每次请求-响应都是独立的**

​	**缺点：多次请求间不能共享数据**

​	**优点：速度快**

### 请求协议

```
GET /hello HTTP/1.1
Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7

Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Host: localhost:8080
```

**以上述数据为例：**

**请求行：请求数据的第一行，分为（请求方式，资源路径，协议）三部分**、

**请求头：从第二行开始，格式（key: value）**

| key             | value                                                        |
| --------------- | ------------------------------------------------------------ |
| Host            | 请求的主机名                                                 |
| User-Agent      | 浏览器版本，例如Chrome浏览器的标识类似Mozilla/5.0 ... Chrome/79，IE浏览器的标识类似Mozilla/5.0 (Windows NT ...) like Gecko |
| Accept          | 表示浏览器能接收的资源类型，如text/*，image/*或者*/*表示所有 |
| Accept-Language | 表示浏览器偏好的语言，服务器可以据此返回不同语言的网页       |
| Accept-Encoding | 表示浏览器可以支持的压缩类型，例如gzip, deflate等。          |
| Content-Type    | 请求主体的数据类型。                                         |
| Content-Length  | 请求主体的大小（单位：字节）                                 |

**请求体：post请求特有的一部分，通过空行与请求头隔开，存放请求参数**

**请求方式-get：请求参数在请求行中，没有请求体，？后面的 部分便是请求参数，相当于请求方式放到url中，因此get安全性较差**

**请求方式-post:请求参数在请求体中，POST请求没有大小限制**

### 响应协议

**响应行：响应数据的第一行，分（协议，状态码，描述）三部分**

**响应头：第二行开始，格式（key:value）**

**响应体：最后一部分，存放响应数据**

| 状态码 | 含义                                                         |
| ------ | ------------------------------------------------------------ |
| 1xx    | 响应中-临时状态码，表示请求已经接受，告诉客户端应该继续请求或者如果它已经完成则忽略它 |
| 2xx    | 成功-表示请求已经被成功接收iu，处理已完成                    |
| 3xx    | 重定向-重定向到其他地方，让客户端在发一次请求已完成整个处理  |
| 4xx    | 客户端错误-处理发生错误，责任在客户端，如：请求了不存在的资源，客户端未被授权，禁止访问等 |
| 5xx    | 服务器错误-处理发生错误，责任在服务器，如：程序抛出异常      |

| key              | value                                                   |
| ---------------- | ------------------------------------------------------- |
| Content-Type     | 表示响应内容的类型，例如text/html                       |
| Content-Length   | 表示响应长度的内容                                      |
| Content-Encoding | 表示该响应压缩算法                                      |
| Cache-Control    | 指示客户端如何缓存，例如max-age=300表示最多可以缓存30秒 |
| Set-Cookie       | 告诉浏览器为当前页面所在的域设置Cookie                  |



**常见的响应状态码**

| 状态码 | 英文描述                               | 解释                                                         |
| ------ | -------------------------------------- | ------------------------------------------------------------ |
| 200    | **`OK`**                               | 客户端请求成功，即**处理成功**，这是我们最想看到的状态码     |
| 302    | **`Found`**                            | 指示所请求的资源已移动到由`Location`响应头给定的 URL，浏览器会自动重新访问到这个页面 |
| 304    | **`Not Modified`**                     | 告诉客户端，你请求的资源至上次取得后，服务端并未更改，你直接用你本地缓存吧。隐式重定向 |
| 400    | **`Bad Request`**                      | 客户端请求有**语法错误**，不能被服务器所理解                 |
| 403    | **`Forbidden`**                        | 服务器收到请求，但是**拒绝提供服务**，比如：没有权限访问相关资源 |
| 404    | **`Not Found`**                        | **请求资源不存在**，一般是URL输入有误，或者网站资源被删除了  |
| 405    | **`Method Not Allowed`**               | 请求方式有误，比如应该用GET请求方式的资源，用了POST          |
| 428    | **`Precondition Required`**            | **服务器要求有条件的请求**，告诉客户端要想访问该资源，必须携带特定的请求头 |
| 429    | **`Too Many Requests`**                | 指示用户在给定时间内发送了**太多请求**（“限速”），配合 Retry-After(多长时间后可以请求)响应头一起使用 |
| 431    | **` Request Header Fields Too Large`** | **请求头太大**，服务器不愿意处理请求，因为它的头部字段太大。请求可以在减少请求头域的大小后重新提交。 |
| 500    | **`Internal Server Error`**            | **服务器发生不可预期的错误**。服务器出异常了，赶紧看日志去吧 |
| 503    | **`Service Unavailable`**              | **服务器尚未准备好处理请求**，服务器刚刚启动，还未初始化好   |

状态码大全：https://cloud.tencent.com/developer/chapter/13553 

## Tomcat

**Tomcat也被称为Web容器，Servlet容器，Servlet程序需要依赖于Tomcat才能运行**

## 请求响应

**请求（HttpServletRequest）:获取请求数据**

**响应（HttpServletResponse）：设置响应数据**

**BS架构：浏览器/服务器架构模式，客户端只需要浏览器，应用程序的逻辑和数据都存储在服务器**

**CS架构：客户端/服务器架构模式**

### 简单参数的传输

**原始的获取请求参数的方法，其中@RequestMapping中的连接代表这个控制器的访问链接**

```

@RestController
public class RequestController {
    @RequestMapping("/simpleParam")
    public String simpleParam(HttpServletRequest request) {
        String name = request.getParameter("name");
        String ageStr = request.getParameter("age");
        
        System.out.println(name + ":" + ageStr);
        return "ok";
    }
}
```

**基于SpringBoot获取请求参数的方法，只需要保证前端的请求参数名与Controller方法的形参的变量名相同即可**

```
@RestController
public class RequestController {
    @RequestMapping("/simpleParam")
    public String simpleParam(String name,String age) {
        System.out.println(name + ":" + age);
        return "ok";
    }
}
```

**当请求参数名与形参的变量名不同时，可以用@RequestParam(name="请求参数名")来指定当前的形参对应的是哪个请求参数名**

```
@RestController
public class RequestController {
    @RequestMapping("/simpleParam")
    public String simpleParam(@RequestParam(name = "name") String username, String age) {
        System.out.println(username + ":" + age);
        return "ok";
    }
}
```

**当请求的参数名不存在，但形参里有对应的参数名时，发出请求会报错，这时需要用到@RequestParam注解中的require,将属性值改为false即可，默认值为true，代表必须传递**

```
@RestController
public class RequestController {
    @RequestMapping("/simpleParam")
    public String simpleParam(@RequestParam(name = "name",required = false) String username, String age) {
        System.out.println(username + ":" + age);
        return "ok";
    }
}
```

**但是同样是缺少请求参数名的情况下，以下方式就不会报错**

```

@RestController
public class RequestController {
    @RequestMapping("/simpleParam")
    public String simpleParam(String name, String age) {
        System.out.println(name + ":" + age);
        return "ok";
    }
}

```

### 实体参数的传输

**简单实体的封装，先定义一个类，包含请求参数的参数名，然后直接将函数参数变量改为这个类即可，注意既是请求的参数与类的参数名对不上也不会报错，只会传入一个null值**

```
package com.example.pojo;

public class User {
    private String name;
    private Integer age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

```
@RestController
public class RequestController {
    @RequestMapping("/simplePojo")
    public String simplePojo(User user){
        System.out.println(user);
        return "ok";
    }
}
```

**如果是复杂参数的情况，按照层次结构对应即可，例如如下案例，请求参数只需要以address.province,address,city的形式进行请求即可**

```
public class User {
    private String name;
    private Integer age;
    private Address address;
}


public class Address {
    private String province;
    private String city;
}


```

### 数组集合参数

**如果请求数据的是一组key值相同但取值不同的数据，则需要用到数组集合参数，此时只需要保持数组名与请求参数的参数名即key值相同即可**

```
@RestController
public class RequestController { 
    @RequestMapping("/arrayParam")
    public String arrayParam(String[] hobby) {
        for (String s : hobby) {
            System.out.println(s);
        }
        return "ok";
    }
}
```

**也可以使用集合的方式进行获取**

```
@RestController
public class RequestController {

    @RequestMapping("/listParam")
    public String listParam(@RequestParam List<String> hobby) {
        System.out.println(hobby);
        return "ok";
    }
}
```

### 日期时间类型的参数

**获取日期类型的参数，如下，只需要将形参的变量改为LocalDateTime,在前面加上@DateTimeFormat(pattern= "yyyy-MM-dd hh-mm-ss")指定格式即可**

```
@RestController
public class RequestController {
    @RequestMapping("/dateParam")
    public String dateParam(@DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss") LocalDateTime updateTime) {
        System.out.println(updateTime);
        return "ok";
    }
}
```

### JSON格式的参数

**JSON数据键名需要与形参对象属性名相同，定义POJO类型形参即可接收参数，但需要用@RequestBody标识**

```
@RestController
public class RequestController {

    @RequestMapping("/jsonParam")
    public String jsonParam(@RequestBody User user) {
        System.out.println(user);
        return "ok";
    }
}

```

### 路径参数

**传递方式：路径参数是通过URL的路径部分来传递的，通常以`/`分隔路径段，下面示例中1便是。**

**示例：`http://localhost:8888/todo/1`**

**使用场景：路径参数常用于标识资源或指定资源的唯一标识符，例如获取用户信息、获取特定文章等。**

**参数不是固定的，所以路径中参数的位置需要用{id}代替，形参前面要加上@PathVariable来代表这个参数是路径参数**

```
@RestController
public class RequestController {
    
    @RequestMapping("/path/{id}")
    public String pathParam(@PathVariable Integer id){
        System.out.println(id);
        return "ok";
    }
}

```

**也可以有多个路径参数，在后面加“/参数”即可**

```
@RestController
public class RequestController {
    @RequestMapping("/path/{id}/{name}")
    public String pathParam(@PathVariable Integer id, @PathVariable String name) {
        System.out.println(id + " " + name);
        return "ok";
    }
}
```

**参数上下需保持一致才可以请求成功**

### 响应数据@ResponseBody

**类型：方法注解，类注解**

**位置：Controller方法上/类上**

**作用：将方法返回值直接响应，如果返回值是实体对象/集合，则会转换为json数据进行响应**

**说明：@RestController=@Controller+@ResponseBody**

**一般情况下我们会统一返回数据，用Result对象进行包装**

```
package com.example.pojo;

/**
 * 统一响应结果封装类
 */
public class Result {
    private Integer code ;//1 成功 , 0 失败
    private String msg; //提示信息
    private Object data; //数据 data

    public Result() {
    }
    public Result(Integer code, String msg, Object data) {
        this.code = code;
        this.msg = msg;
        this.data = data;
    }
    public Integer getCode() {
        return code;
    }
    public void setCode(Integer code) {
        this.code = code;
    }
    public String getMsg() {
        return msg;
    }
    public void setMsg(String msg) {
        this.msg = msg;
    }
    public Object getData() {
        return data;
    }
    public void setData(Object data) {
        this.data = data;
    }

    public static Result success(Object data){
        return new Result(1, "success", data);
    }
    public static Result success(){
        return new Result(1, "success", null);
    }
    public static Result error(String msg){
        return new Result(0, msg, null);
    }

    @Override
    public String toString() {
        return "Result{" +
                "code=" + code +
                ", msg='" + msg + '\'' +
                ", data=" + data +
                '}';
    }
}

```

**注意：Springboot项目的静态前端资源默认存放目录为：classpath:/static,classpath:/public,classpath:resources**

### @RequestMapping

**在使用该注解的时候，会出现需要我们限定请求类型的情况，这个时候我们只需要做如下处理即可，通过mthod属性就可以限制请求类型**

```
@RequestMapping(value = "/depts",method = RequestMethod.GET)
```

**也可以直接使用对应请求类型的注解，如GET**

```
@GetMapping("/depts")
```

**遇到下图的情况，我们还可以把路径中的公共部分抽取出来，放到类上面**

```
@RestController
@Slf4j
public class DeptController {

    @Autowired
    private DeptService deptService;

    @GetMapping("/depts")
    public Result selectAll() {
        List<Dept> deptList = deptService.selectAll();
        return Result.success(deptList);
    }

    @DeleteMapping("/depts/{id}")
    public Result deleteById(@PathVariable Integer id) {
        deptService.deleteById(id);
        return Result.success();
    }

    @PostMapping("/depts")
    public Result insert(@RequestBody Dept dept) {
        deptService.insert(dept);
        return Result.success();
    }
}
```

```
@RestController
@Slf4j
@RequestMapping("/depts")
public class DeptController {

    @Autowired
    private DeptService deptService;

    @GetMapping
    public Result selectAll() {
        List<Dept> deptList = deptService.selectAll();
        return Result.success(deptList);
    }

    @DeleteMapping("/{id}")
    public Result deleteById(@PathVariable Integer id) {
        deptService.deleteById(id);
        return Result.success();
    }

    @PostMapping
    public Result insert(@RequestBody Dept dept) {
        deptService.insert(dept);
        return Result.success();
    }
}
```

### @RequestParam

**通过给形参前面加@RequestParam(defaultValue="值")给形参加上默认值**



## 分层解耦

### 三层架构

**Controller:控制层，接受前端请求，对请求您进行处理，并相应数据**

**service:业务逻辑层，处理具体的业务逻辑**

**dao:数据访问层（持久层），负责数据的访问操作，包括数据的增删改查**

### 分层解耦

**内聚：软件中各个功能模块内部的功能联系**

**耦合：衡量软件中各个层/模块之间的依赖，关联的程度**

**软件设计原则：高内聚，低耦合**

**控制反转：简称IOC，对象的创建控制权由程序自身转移到外部（容器），这种思想称为控制反转**

**依赖注入：简称DI，容器为应用程序提供运行时，所依赖的资源，称之为依赖注入**

**Bean对象：IOC容器中创建，管理的对象，称之为Bean**

### IOC&DI

**Service层及Dao层的实现类，交给IOC管理，只需要在需要管理的实现类上加上@Component注解**

**为Controller层，Service层注入运行时所依赖的对象，只需要在对应的成员变量上加@Autowired注解**

| 注解         | 说明                 | 位置                                                         |
| ------------ | -------------------- | ------------------------------------------------------------ |
| @Component   | 申明bean的基础注解   | 不属于以下三类时用此注解                                     |
| @Controller  | @Component的衍生注解 | 标注在控制器类上                                             |
| @Service     | @Component的衍生注解 | 标注在业务类上                                               |
| @Respository | @Component的衍生注解 | 标注在数据访问类上                                           |
| @Mapper      | Mybatis的注解        | 标注在数据访问类Mapper上                                     |
| @MapperScan  | Spring的注解         | 标注在spring的启动类上，@MapperScan("com.hmall.mapper")，使用该注解扫描对应的mapper包，则可给这个包下的所有mapper进行依赖注入 |

**申明bean的时候，可以通过value属性来指定bean的名字，没有，则默认为类名首字母小写后的名字**

**使用以上四个注解都可以声明bean，但是在springboot集成web开发中，声明控制器bean只能用Controller**

**前面声明bean的四大注解，要想生效，还需要被组件扫描注解@ComponentScan扫描**

**@ComponentScan注解虽然没有显示配置，但是实际上已经包含在启动类声明注解@SpringBootApplication中，默认扫描的范围时启动类所在包及其子包，@ComponentScan({"包名","包名"})去添加扫描的包，建议根据代码规范去放包**

**@Autowired注解，默认是按照类型进行，如果存在多个相同类型的bean，就会报错，可以有以下方式解决**

**@Primary，想让哪个生效，就在哪个上面加**

**@Qualifier("需要的bean的名字")加在需要注入的成员变量上，上述两个解决方案需要在@Autowired的注解上进行**

**@Resource(name="需要的bean的名字")，这个不需要@Autowired**

**@Autowired是Spring框架提供的注解，而@Resource是jdk提供的注解**

**@Autowired默认是按照类型注入，而@Resource默认是按照名称注入**

### 依赖注入的其他方式

**通过set方法进行注入**

```
@Slf4j
@RequestMapping("/users")
@RestController
@Api(tags = "用户管理模块")
public class UserController {
    private IUserService userService;

    public void setUserService(IUserService userService) {
        this.userService = userService;
    }
}
```

**通过构造方法的方式进行注入**

```
@Slf4j
@RequestMapping("/users")
@RestController
@Api(tags = "用户管理模块")
public class UserController {
    private IUserService userService;

    public UserController(IUserService userService) {
        this.userService = userService;
    }
    
}
```

**当然我们也可以用lombok的注解来添加构造函数，常用的@RequiredArgsConstructor注解**

```
@Slf4j
@RequestMapping("/users")
@RestController
@Api(tags = "用户管理模块")
@RequiredArgsConstructor
public class UserController {
    private final IUserService userService;
    
}
```

### 循环依赖

 **在 Spring 应用中，循环依赖指的是两个或多个 Bean 之间相互引用，造成了一个环状的依赖关系。举例来说，如果 Bean A 依赖于 Bean B，同时 Bean B 也依赖于 Bean A，就形成了循环依赖。这种情况下，Spring 容器在创建这些 Bean 时会陷入无限循环，导致应用启动失败或者出现其他不可预测的问题。因此在开发过程中应当尽量避免循环依赖的情况出现**



## 开发规范 Restful

**REST：表述性状态转换，是一种软件结构风格**

**一般开发时遵循以下方式定义url,URL定位资源，HTTP动词描述操作**

**http://localhost:8080/users/1**  **GET查询id为1的用户**

**http://localhost:8080/users**  **POST：新增用户**

**http://localhost:8080/users**  **PUT：修改用户**

**http://localhost:8080/users/1** **DELETE：删除id为1的用户**

**REST是风格，是约定方式，约定不是规定，可以打破。**

**描述模块的功能通常使用复数，也就是加s的格式来描述，表示此类资源，而非单个资源。如：users、emps、books…**

## 日志记录

```
@RestController
@Slf4j
public class DeptController {
    
    @RequestMapping("/depts")
    public Result list() {
        log.info("查询全部的部门数据");
        return Result.success();
    }
}
```

## pagehelper

```
<dependency>
	<groupId>com.github.pagehelper</groupId>
	<artifactId>pagehelper-spring-boot-starter</artifactId>
	<version>1.4.2</version>
</dependency>
```

**pagehelper是一款可以对查询结果自动执行分页操作的插件，只需要在service层使用该插件即可**

```
@override
public PageBean page(Integer page, Integer pageSize){
	PageHelper.startPage(page,pageSize)//这里传的是第几页以及每页显示的条数
	List<Emp> empList = empMapper.list();//这里获取的是数据库的查询结果
	Page<Emp> p = (Page<Emp>) empList;
	return new PageBean(p.getTotal(),p.getResult());//这里p.getTotal()获取查询的总结果数，getResult()获取查询的结果
}
```

## 文件上传

**对于前端而言，文件上传有以下要求，method="post",entrytype="multipart/form-data",且必须有一个input,type="file"**

```
<body>

    <form action="/upload" method="post" enctype="multipart/form-data">
        姓名: <input type="text" name="username"><br>
        年龄: <input type="text" name="age"><br>
        头像: <input type="file" name="image"><br>
        <input type="submit" value="提交">
    </form>

</body>
```

**基于上述前端页面，我们发送请求，服务端获取上述信息，可通过以下方式**

```
@Slf4j
@RestController
public class UploadController {
    @PostMapping("/upload")
    public Result upload(String username, Integer age, MultipartFile image) {
        System.out.println(username + " " + age + " " + image);
        return Result.success();
    }
}
```

**其中MultipartFile image用于接受前端上传的文件**

## 文件存储

```
@Slf4j
@RestController
public class UploadController {
    @PostMapping("/upload")
    public Result upload(String username, Integer age, MultipartFile image) throws IOException {
        System.out.println(username + " " + age + " " + image);
        //获取原始文件名
        String originalFilename=image.getOriginalFilename();

        //将文件存储在指定目录下
        image.transferTo(new File("D:\\web\\image"+originalFilename));//new File()填文件的存储地址
        
        return Result.success();
    }
}

```

**通过以上步骤便可以完成文件的初始获取，但是这样的方式会有文件名重复的文件，我们需要对文件名做处理，可以用UUID作为文件的名字，这个UUID也是这个文件的唯一标识**

```
UUID.randomUUID().toString();//这样便可以获取UUID字符串形式的返回结果
```

**通过配置application.properties来实现更改文件上传以及请求大小**

```
#配置单个文件最大上传大小
spring.servlet.multipart.max-file-size=10MB
#配置单个请求最大上传大小(一次请求可以上传多个文件)
spring.servlet.multipart.max-request-size=100MB

```

**MultipartFile的一些方法**

```
String getOriginalFilename(); //获取原始文件名
void transferTo(File dest); //将接收的文件转存到磁盘文件中
long getSize(); //获取文件的大小，单位：字节
byte[] getBytes(); //获取文件内容的字节数组
InputStream getInputStream(); //获取接收到的文件内容的输入流
```

## 阿里云OSS对象存储

**SDK：软件开发工具包，包括辅助软件开发的依赖，代码示例等**

**Bucket:存储空间是用户用于存储对象的容器，所有的对象都必须隶属于某个存储空间**

**相关依赖**

```
<dependency>
    <groupId>com.aliyun.oss</groupId>
    <artifactId>aliyun-sdk-oss</artifactId>
    <version>3.17.4</version>
</dependency>

<!--java 9 及以上添加下面依赖-->
<dependency>
    <groupId>javax.xml.bind</groupId>
    <artifactId>jaxb-api</artifactId>
    <version>2.3.1</version>
</dependency>
<dependency>
    <groupId>javax.activation</groupId>
    <artifactId>activation</artifactId>
    <version>1.1.1</version>
</dependency>
<!-- no more than 2.3.3-->
<dependency>
    <groupId>org.glassfish.jaxb</groupId>
    <artifactId>jaxb-runtime</artifactId>
    <version>2.3.3</version>
</dependency>
```

**以下是基于阿里云提供的文档集成的一个工具类用于提交文件到阿里云OSS**

```
@Component
public class AliOSSUtils {

    private String endpoint = "";
    private String accessKeyId = "";
    private String accessKeySecret = "";
    private String bucketName = "";

    /**
     * 实现上传图片到OSS
     */
    public String upload(MultipartFile file) throws IOException {
        // 获取上传的文件的输入流
        InputStream inputStream = file.getInputStream();

        // 避免文件覆盖,使用UUID给文件命名
        String originalFilename = file.getOriginalFilename();
        String fileName = UUID.randomUUID().toString() + originalFilename.substring(originalFilename.lastIndexOf("."));

        //上传文件到 OSS
        OSS ossClient = new OSSClientBuilder().build(endpoint, accessKeyId, accessKeySecret);
        ossClient.putObject(bucketName, fileName, inputStream);

        //文件访问路径
        String url = endpoint.split("//")[0] + "//" + bucketName + "." + endpoint.split("//")[1] + "/" + fileName;
        // 关闭ossClient
        ossClient.shutdown();
        return url;// 把上传到oss的路径返回
    }

}
```

## 文件配置相关

### 参数配置化

**举例：文件上传中有一个关于文件上传的工具类，其中这个类有四个变量**

```
private String endpoint = "";
private String accessKeyId = "";
private String accessKeySecret = "";
private String bucketName = "";
```

**我们可不可以把这四个变量所对应的值拿去进行统一的管理呢，答案当然是可以的，我们将他们放到application.properties**

```
#阿里云OSS相关参数配置
aliyun.oss.endpoint=地址
aliyun.oss.accessKeyId=""
aliyun.oss.accessKeySecret=""
aliyun.oss.bucketName=""

```

**那么如何将这些变量的值跟类里面的变量联系起来呢，我们可以通过@value("${配置文件中对应的key值}")注解进行配置**

```
@Value("${aliyun.oss.endpoint}")
private String endpoint;
@Value("${aliyun.oss.accessKeyId}")
private String accessKeyId;
@Value("${aliyun.oss.accessKeySecret}")
private String accessKeySecret;
@Value("${aliyun.oss.bucketName}")
private String bucketName;
```

**当然这样还是很麻烦，我们还有更好的方法，使用@ComfigurationProperties,当然使用这个是有前置条件的，需要给类加上@Data,@Component，注解才可以使用，还需要保证类中的变量名与配置文件中的名字一一对应，最后按照如下操作设置@ConfigurationProperties(prefix = "aliyun.oss"),来设置前缀即可，当然使用这个我们还需要引用一个依赖**

```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-configuration-processor</artifactId>
</dependency>
```

```java
@Component
@ConfigurationProperties(prefix = "sky.alioss")
@Data
public class AliOssProperties {

    private String endpoint;
    private String accessKeyId;
    private String accessKeySecret;
    private String bucketName;

}
```



### yml配置文件

**在.properties文件中我们一般这样配置**

```
server.port=8080
server.address=127.0.0.1
```

**而在ymp配置文件中我们是这样配置的,需要按级书写**

```
server:
 port:8080
 address:127.0.0.1
```

**基本语法**

**大小写敏感**

**数值前面必须有空格，作为分隔符**

**使用缩进标识层级关系，缩进时，不允许使用tab键，只能用空格**

**缩进的空格数目不重要，只要相同层级的元素左侧对齐即可**

**#表示注释，从这个字符一直到行尾，都会被解析器忽略**

**定义对象/map集合**

```
user:
 name: Tom
 age: 20
```

**定义数组/List/Set,-后面代表是数组中的值**

```
hobby:
 - java
 - c
 - game
```

## 配置优先级

**三种配置文件优先级排序：命令行属性>java系统属性>properties>yml>yaml**

## 登录校验

### 会话

**会话：用户打开浏览器，访问web服务器的资源，会话建立，直到有一方断开连接，会话结束，再一次会话中可以包含多次请求和响应**

**会话跟踪：一种维护浏览器状态的方法，服务器需要识别多次请求是否来自于同一浏览器，以便在同一次会话的多次请求间共享数据**

**会话跟踪技术：**

​	**客户端会话跟踪技术：Cookie**

​	**服务端会话跟踪技术：Session**

​	**令牌技术**

**Cookie的优点：http协议中支持的技术**

**Cookie的缺点：移动端APP无法使用cookie，不安全，用户可以自己禁用Cookie，Cookie不能跨域**

**Session的优点：存储在服务端，安全**

**Session的缺点：服务器集群环境下无法使用Session,Cookie的缺点**

**令牌技术的优点：支持pc端，移动端，解决集群环境下的认证问题，减轻服务器存储压力**

**令牌技术的缺点：需要自己实现**

### JWT令牌

**定义了一种简洁，自包含的格式，用于在通信双方以json数据格式安全的额传输信息，由于数字签名的存在，这些信息是可靠的**

**组成：**

**第一部分：Header(头）， 记录令牌类型、签名算法等。 例如：{"alg":"HS256","type":"JWT"}**

**第二部分：Payload(有效载荷），携带一些自定义信息、默认信息等。 例如：{"id":"1","username":"Tom"}**

**第三部分：Signature(签名），防止Token被篡改、确保安全性。将header、payload，并加入指定秘钥，通过指定签名算法计算而来。**

**场景：登录认证。**

**登录成功后，生成令牌**

**后续每个请求，都要携带JWT令牌，系统在每次请求处理之前，先校验令牌，通过后，再处理**

**使用jwt我们需要先引用相关的依赖**

```
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt</artifactId>
    <version>0.9.1</version>
</dependency>
```

**生成和解析jwt令牌的工具类**

```
public class JwtUtils {

    private static String signKey = "itheima";
    private static Long expire = 43200000L;

    /**
     * 生成JWT令牌
     * @param claims JWT第二部分负载 payload 中存储的内容
     * @return
     */
     
    //map存储自定义信息，通常是键值对的形式,因此用map存储
    public static String generateJwt(Map<String, Object> claims){
        String jwt = Jwts.builder()
                .addClaims(claims)//设置自定义内容，键值对的形式
                .signWith(SignatureAlgorithm.HS256, signKey)//设置加密算法及密钥
                .setExpiration(new Date(System.currentTimeMillis() + expire))//设置过期时间
                .compact();//转成字符串结果
        return jwt;
    }

    /**
     * 解析JWT令牌
     * @param jwt JWT令牌
     * @return JWT第二部分负载 payload 中存储的内容
     */
    public static Claims parseJWT(String jwt){
        Claims claims = Jwts.parser()
                .setSigningKey(signKey)//填写密钥
                .parseClaimsJws(jwt)//添加jwt令牌
                .getBody();//获取结果
        return claims;
    }
}
```

### 过滤器Filter

**概念：Filter 过滤器，是 JavaWeb 三大组件(Servlet、Filter、Listener)之一。**

**过滤器可以把对资源的请求拦截下来，从而实现一些特殊的功能。**

**过滤器一般完成一些通用的操作，比如：登录校验、统一编码处理、敏感字符处理等。**

**快速入门**

**定义Filter：定义一个类，实现 Filter 接口，并重写其所有方法。**

**配置Filter：Filter类上加 @WebFilter 注解，配置拦截资源的路径。引导类上加 @ServletComponentScan 开启Servlet组件**

**要使用Filter必须先在启动类也就是xxxApplication这个类的上面加上@ServletComponentScan**

**定义一个filter类，继承Filter接口，并在上面加上注解@webFilter(),里面的参数代表要拦截的请求，然后doFilter方法中写关于拦截的具体实现	**

```
@WebFilter("/*")
public class DemoFilter implements Filter {

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        filterChain.doFilter(servletRequest,servletResponse);//放行操作
    }

}
```

**执行逻辑：**
**放行后访问对应的web资源，资源访问完成后，还会回到Filter中**

**如果回到filter中不会重头执行，而是执行放行后的逻辑**

| 拦截路径     | urlPatterns | 含义                               |
| ------------ | ----------- | ---------------------------------- |
| 拦截具体路径 | /login      | 只有访问该路径时才会被拦截         |
| 目录拦截     | /emps/*     | 访问目录emps下的所有资源都会被拦截 |
| 拦截所有     | /*          | 访问所有资源都会被拦截             |

**过滤器链：在一个web服务中可以配置多个过滤器，这多个过滤器就会形成一个过滤器链，按照类名的字典序进行执行，执行顺序先按照顺序逐一执行放行前的操作，放行到最后一个后，在从最后一个开始反向执行放行后的操作**

**下面是一个登录校验的基本实现**

```
package com.example.tlias.filter;

import com.alibaba.fastjson.JSONObject;
import com.example.tlias.pojo.Result;
import com.example.tlias.utils.JwtUtils;
import jakarta.servlet.*;
import jakarta.servlet.annotation.WebFilter;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import lombok.extern.slf4j.Slf4j;
import org.springframework.util.StringUtils;

import java.io.IOException;
@Slf4j
@WebFilter("/*")
public class LoginCheckFilter implements Filter {
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {

        //获取请求对象
        HttpServletRequest req = (HttpServletRequest) servletRequest;
        HttpServletResponse resp = (HttpServletResponse) servletResponse;

        //获取请求的url
        String url = req.getRequestURI();

        //如果请求的路径包括login放行
        if(url.contains("login")){
            filterChain.doFilter(servletRequest,servletResponse);
            return;
        }

        //获取jwt令牌
        String jwt = req.getHeader("token");
        if(!StringUtils.hasLength(jwt)){
            //准备错误信息，并包装成json字符串，然后直接返回给前端
            Result result = Result.error("NOT_LOGIN");
            String noLogin = JSONObject.toJSONString(result);
            resp.getWriter().write(noLogin);
            return;
        }

        //这里如果令牌不为空，对令牌进行解析，如果解析成功放行，失败，抓取异常结果，并返回错误信息
        try{
            JwtUtils.parseJWT(jwt);

        } catch (Exception e){
            e.printStackTrace();
            Result result = Result.error("NOT_LOGIN");
            String noLogin = JSONObject.toJSONString(result);
            resp.getWriter().write(noLogin);
            return;
        }

        //放行
        filterChain.doFilter(servletRequest,servletResponse);
    }
}

```

### 拦截器interceptor

**定义一个拦截器对象**

```
@Component
public class LoginCheckInterceptor implements HandlerInterceptor {
    
    //目标资源方法运行前运行，true代表放行
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        return true;
    }

    //目标资源方法运行后运行
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        
    }

    //视图渲染完毕后运行，最后运行
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        
    }
}
```

```
@Configuration
public class WebConfig implements WebMvcConfigurer {
    //给对应的拦截器配置拦截的资源
    private LoginCheckInterceptor loginCheckInterceptor;
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(loginCheckInterceptor).addPathPatterns("/**");
                //配置不要拦截的资源.excludePathPatterns();
    }
}
```

| 拦截路径  | 含义                 | 举例                                     |
| --------- | -------------------- | ---------------------------------------- |
| /*        | 一级路径             | 能匹配/depts,不能匹配/depts/1            |
| /**       | 任意级路径           | 所有路径                                 |
| /depts/*  | /depts下的任意路径   | 能匹配/depts/1,不能匹配/depts/1/2,/depts |
| /depts/** | /depts下的任意级路径 | /depts,/depts/1,/depts/1/2               |

**执行流程：先执行Filter在执行Interceptor**

**接口规范不同：过滤器需要实现Filter接口，而拦截器需要实现HandlerInterceptor接口。**

**拦截范围不同：过滤器Filter会拦截所有的资源，而Interceptor只会拦截Spring环境中的资源。**

### md5加密登录密码

```java
String str = DigestUtils.md5DigestAsHex(password.getBytes());
```

**实际存储到数据库的便是加密后的字符串**



## 异常处理

**定义一个全局异常处理器，处理所有的异常**

**其中@RestControllerAdvice由@ControllerAdvice、@ResponseBody组成，可以用于定义@ExceptionHandler、@InitBinder、@ModelAttribute，并应用到所有@RequestMapping中**

**@ExceptionHandler：用于指定异常处理方法**

```
@RestControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(Exception.class)
    public Result ex(Exception ex){
        ex.printStackTrace();
        return Result.error("对不起，操作失败，请联系管理员");
    }
}
```



## 事务管理

### 事务回顾@Transactional

**事务：是一组操作的集合，它是一个不可分割的工作单位，这些操作，要么同时成功，要么同时失败**

**开启事务（一组操作开始前，开启事务）：start transaction / begin ;**

**提交事务（这组操作全部成功后，提交事务）：commit ;**

**回滚事务（中间任何一个操作出现异常，回滚事务）：rollback ;**

**Spring框架提供事务管理注解，@Transactional**

**注解位置：业务（service）层的方法，类上，接口上**

**作用：将当前方法交给spring进行事务管理，方法执行前，开启事务，成功执行完毕，提交事务，出现异常，自动回滚事务**

```
#开启spring事务管理日志
logging.level.org.springframework.jdbc.support.JdbcTransactionManager=debug
```

### rollbackFor属性

**默认情况下，只有出现 RuntimeException 才回滚异常。rollbackFor属性用于控制出现何种异常类型，回滚事务。**

**指定所有的异常都需要事务回滚：rollbackFor = Exception.class**

### propagation属性

**事务传播行为：指的就是当一个事务方法被另一个事务方法调用时，这个事务方法应该如何进行事务控制。**

**设置属性：@Transaction(propagation = Paopagation.REQUIRED)**

| 属性值        | 含义                                                         |
| ------------- | ------------------------------------------------------------ |
| REQUIRED      | 默认值,需要事务，有则加入，无则创建新事务                    |
| REQUIRES_NEW  | 需要新事务，无论有无，总是创建新事务                         |
| SUPPORTS      | 支持事务，有则加入，无则在无事务状态中运行                   |
| NOT_SUPPORTED | 不支持事务，在无事务状态下运行,如果当前存在已有事务,则挂起当前事务 |
| MANDATORY     | 必须有事务，否则抛异常                                       |
| NEVER         | 必须没事务，否则抛异常                                       |

**REQUIRED ：大部分情况下都是用该传播行为即可。**

**REQUIRES_NEW ：当我们不希望事务之间相互影响时，可以使用该传播行为。比如：下订单前需要记录日志，不论订单保存成功与否，都需要保证日志记录能够记录成功。**

## AOP

### 基本概念和入门程序

**AOP：Aspect Oriented Programming（面向切面编程、面向方面编程），其实就是面向特定方法编程。**

**实现：动态代理是面向切面编程最主流的实现。而SpringAOP是Spring框架的高级技术，旨在管理bean对象的过程中，主要通过底层的动态代理机制，对特定的方法进行编程。**

**首先需要引入AOP的依赖**

```
<dependency>    
	<groupId>org.springframework.boot</groupId>    
	<artifactId>spring-boot-starter-aop</artifactId>
</dependency>

```

**编写AOP程序**

```
@Component
@Aspect
public class TimeAspect {
		@Around("execution(* com.itheima.service.*.*(..))")
		public Object recordTime(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
		long begin = System.currentTimeMillis();
		
		Object object = proceedingJoinPoint.proceed(); //调用原始方法运行，需注意原始方法运行完会有返回值，我们需要接收返回值，并返回回去
		
		long end = System.currentTimeMillis();
		log.info(proceedingJoinPoint.getSignature()+"执行耗时: {}ms", end - begin);
		return object;//此处返回原始方法的返回值
	}
}

```

**解释：首先这个类作为spring框架下的类，需要加上@Component,作为aop程序，需要加上@Aspect注解，@Around来限定这个方法争对的是哪些方法，给哪些方法做了代理**

**连接点：JoinPoint,可以被AOP控制的方法（暗含方法执行时的信息）**

**通知：Advice，指哪些重复的逻辑，也就是共性功能，最终体现为一个方法**

**切入点：PointCut,匹配连接点的条件，通知仅会在切入点方法执行时被应用**

**切面：Aspect，描述通知与切入点的对饮关系（通知+切入点）**

**目标对象：Traget,通知所应用的对象**

**个人理解：AOP可以在不改动原本代码的情况下，给原代码增加功能**

### 通知类型

**@Around：环绕通知，此注解标注的通知方法在目标方法前、后都被执行**

**@Before：前置通知，此注解标注的通知方法在目标方法前被执行**

**@After ：后置通知，此注解标注的通知方法在目标方法后被执行，无论是否有异常都会执行**

**@AfterReturning ： 返回后通知，此注解标注的通知方法在目标方法后被执行，有异常不会执行**

**@AfterThrowing ： 异常后通知，此注解标注的通知方法发生异常后执行**

**注意：**

**@Around环绕通知需要自己调用 ProceedingJoinPoint.proceed() 来让原始方法执行，其他通知不需要考虑目标方法执行**

**@Around环绕通知方法的返回值，必须指定为Object，来接收原始方法的返回值。**

**对于相同的切入点表达式，我们可以将其抽取出来，集中管理**

```
@Pointcut("切入点表达式")
private void pt(){}
```

**提取出来后，我们只需要通过@Around("pt()")的方式使用该切入点表达式即可,当方法的权限为private时只能在当前切面类使用，public则可以在其他切面类使用**

### 通知顺序

**当有多个切面的切入点都匹配到了目标方法，目标方法运行时，多个通知方法都会被执行**

**不同切面类中，默认按照切面类的类名字母排序：**

**目标方法前的通知方法：字母排名靠前的先执行**

**目标方法后的通知方法：字母排名靠前的后执行**

**用 @Order(数字) 加在切面类上来控制顺序**

**目标方法前的通知方法：数字小的先执行**

**目标方法后的通知方法：数字小的后执行**

### 切入点表达式

**切入点表达式：描述切入点方法的一种表达式**

**作用：主要用来决定项目中的哪些方法需要加入通知**

**常见形式：**

**execution(……)：根据方法的签名来匹配**

**@annotation(……) ：根据注解匹配**

#### excution

**语法**

```
execution(访问修饰符?  返回值  包名.类名.?方法名(方法参数) throws 异常?)
```

**其中带 ? 的表示可以省略的部分**

**访问修饰符：可省略（比如: public、protected）**

**包名.类名： 可省略**

**throws 异常：可省略（注意是方法上声明抛出的异常，不是实际抛出的异常）**

**可以使用通配符描述切入点**

**’*‘：单个独立的任意符号，可以通配任意返回值、包名、类名、方法名、任意类型的一个参数，也可以通配包、类、方法名的一部分**

**.. ：多个连续的任意符号，可以通配任意层级的包，或任意类型、任意个数的参数**

**根据业务需要，可以使用 且（&&）、或（||）、非（!） 来组合比较复杂的切入点表达式。l根据业务需要，可以使用 且（&&）、或（||）、非（!） 来组合比较复杂的切入点表达式。**

#### @annotation

**@annotation 切入点表达式，用于匹配标识有特定注解的方法**

**首先，我们需要自定义注解**

```
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface MyLog {
}
```

**@Retention用于描述当前注解什么时候生效，@Target用于定义这个注解在哪里生效，比如在类上还是方法上，然后在需要的方法上加上这个注解即可**

```
@annotation(com.itheima.anno.MyLog)
```

**然后在对应的通知上加上该上述annotaion表达式来操作即可**

### 连接点

**在Spring中用JoinPoint抽象了连接点，用它可以获得方法执行时的相关信息，如目标类名、方法名、方法参数等。**

**对于 @Around 通知，获取连接点信息只能使用 ProceedingJoinPoint**

**对于其他四种通知，获取连接点信息只能使用 JoinPoint ，它是 ProceedingJoinPoint 的父类型**

```
@Around("execution(* com.itheima.service.DeptService.*(..))")
public Object around(ProceedingJoinPoint joinPoint) throws Throwable {
	String className = joinPoint.getTarget().getClass().getName(); //获取目标类名
	Signature signature = joinPoint.getSignature(); //获取目标方法签名
    String methodName = joinPoint.getSignature().getName(); //获取目标方法名
    Object[] args = joinPoint.getArgs(); //获取目标方法运行参数 	
    Object res = joinPoint.proceed(); //执行原始方法,获取返回值（环绕通知）
	return res;
}

```

```
@Before("execution(* com.itheima.service.DeptService.*(..))")
public void before(JoinPoint joinPoint) {
	String className = joinPoint.getTarget().getClass().getName(); //获取目标类名
	Signature signature = joinPoint.getSignature(); //获取目标方法签名
	String methodName = joinPoint.getSignature().getName(); //获取目标方法名
	Object[] args = joinPoint.getArgs(); //获取目标方法运行参数 
}

```

## AspectJ

**AspectJ 是 Java 世界中独立的 AOP 框架，它不依赖于任何框架或容器。因此，除了 Java 应用程序之外，它还可以应用于其他环境，例如 Java EE 应用程序、OSGi环境、Android 环境等。**

### 环境搭建

```xml
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjrt</artifactId>
</dependency>

<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
</dependency>
```

### 技术对比

**1：面向的对象不同**
**Spring AOP**
**Spring AOP 是针对 Spring 框架的 AOP 实现。它依赖于 Spring 框架进行实施和管理，因此它需要使用 Spring 的容器和其他基础设施。**

**AspectJ**
**AspectJ 是 Java 世界中独立的 AOP 框架，它不依赖于任何框架或容器。因此，除了 Java 应用程序之外，它还可以应用于其他环境，例如 Java EE 应用程序、OSGi 环境、Android 环境等。**

**2：AOP 实现方式不同**
**Spring AOP**
**Spring AOP 使用代理的方式实现 AOP。Spring 利用 JDK 动态代理或 CGLIB 代理创建代理对象，代理对象包装目标对象并拦截指定的切点方法，以执行通知。**

**AspectJ**
**AspectJ 支持两种方式实现 AOP。第一种方式是编译时织入，即在编译时将切面代码织入到目标类中。第二种方式是运行时织入，即在目标类加载时通过修改字节码方式织入切面代码。**

**3：支持的切面类型不同**
**Spring AOP**
**Spring AOP 支持比较常见的切面类型，包括方法执行切面、异常拦截切面、前置和后置通知切面等。**

**AspectJ**
**AspectJ 相比 Spring AOP 支持更多的切面类型，包括字段拦截器切面、构造器调用切面、注解切面等。AspectJ 还支持自定义注解和注解处理器，以增强 Java 语言的元素。**

**4：AOP 表达式不同**
**Spring AOP**
**Spring AOP 支持使用 AspectJ 表达式语言（简称为“SpEL”）编写切点表达式。但是，Spring AOP 只支持 AspectJ 表达式的一部分，如 method execution、bean references、args 等。**

**AspectJ**
**AspectJ 使用更为丰富和复杂的切点表达式。在 AspectJ 中，切点表达式可以包含类、方法、参数、返回值、异常等元素，并且可以使用逻辑运算符进行组合。**

**5：性能差异**
**Spring AOP**
**Spring AOP 的实现基于代理，这意味着 Spring 需要在运行时创建代理对象，并在每次方法调用时拦截代理。这可能会导致一定的性能开销。**

**AspectJ**
**AspectJ 提供编译时织入和运行时织入两种方式来实现 AOP。编译时织入可以在编译应用程序时织入切面代码，因此会更加高效，而运行时织入需要在应用程序运行时动态织入切面代码，因此性能开销可能会更大。但是，AspectJ 本身是一个底层的 AOP 框架，因此相对于 Spring AOP 来说，它更精细和高效。**

### 使用

**同springboot Aop一样**

## bean的管理

### bean的获取

**根据name获取bean:**`Object getBean(String name)`

**根据类型获取bean:**`<T> T getBean(Class<T> requiredType)`

**根据name获取bean(带类型转换)：**`<T> T getBean(String name, class<T> requiredType)`

 **获取bean,首先要获取IOC容器对象，这里我们可以采取依赖注入的方法,因为上述方法都是ApplicationContext的方法**

```
@Autowired
private ApplicationContext applicationContext;
```

**通过类似的方法，我们还可以获取请求对象HttpServletRequest**

```
@Autowired
private HttpServletRequest request;
```

### bean的作用域

| 作用域      | 说明                                             |
| ----------- | ------------------------------------------------ |
| singLeton   | 容器内同名称的bean只有一个实例（单例）默认作用域 |
| prototye    | 每次使用该bean时会创建新的实例（非单例）         |
| request     | 每个请求范围内会创建新的实例                     |
| session     | 每个会话范围都会创建新的实例                     |
| application | 每个应用范围都会创建新的实例                     |

**配置作用域可以使用@scope("singLeton"),将该注解加在有依赖注入操作的类上，**

**默认singLeton的bean，在容器启动时被创建，我们也可以使用@Lazy来延迟初始，延迟第一次使用时**

### 第三方bean

**如果我们管理的bean对象来自于第三方（非自定义），是无法使用@Component及其衍生注解使用的，此时需要@Bean注解**

```
@ServletComponentScan
@SpringBootApplication
public class TliasApplication {

    public static void main(String[] args) {
        SpringApplication.run(TliasApplication.class, args);
    }
    @Bean
    public SAXParser saxParser(){
        return new SAXParser();
    }

}
```

### @Configuration

**我们只需要在启动类定义一个方法返回值是需要管理的对象，在这个方法上面加上@Bean注解即可，但是一般我们建议定义一个配置类，在这个类上加上@Configuration,将这个方法放到这个类里**

**通过@Bean注解的name/value属性指定bean名称，如果未指定，则方法名就是**

**如果还需要给这个第三方bean加新的依赖的话，只需要在方法的参数加上对应依赖的形参即可,例如AliOSSUtils这个类还需要依赖AliOSSProperties，但是我们不能通过@Autowired进行注入，就可以用如下方法进行注入**

```
@Configuration
@EnableConfigurationProperties(AliOSSProperties.class)
//当需要依赖的aliOSSProperties对象没有加@Component注解也就是，该对象不是IOC容器被管理的bean时，加此注解
//主要是用来把properties或者yml配置文件转化为bean来使用的，而@EnableConfigurationProperties注解的作用是，
//@ConfigurationProperties注解生效。


@ConfigurationProperties
public class AliOSSAutoConfiguration {
    @Bean
    public AliOSSUtils aliOSSUtils(AliOSSProperties aliOSSProperties){
        AliOSSUtils aliOSSUtils = new AliOSSUtils();
        aliOSSUtils.setAliOSSProperties(aliOSSProperties);
        return aliOSSUtils;
    }
}
```



## 原理

**起步依赖的原理就是依赖传递**

### 自动配置

**SpringBoot的自动配置就是当spring容器启动后，一些配置类、bean对象就自动存入到了IOC容器中，不需要我们手动去声明，从而简化了开发，省去了繁琐的配置操作,这里配置类通常是外部依赖库的类**



**SpringBoot的自动配置就是当Spring容器启动后，一些自动配置类（只是自动配置类，并不是当前的组件配置到IOC容器中，自动配置类通过@Conditional注解来按需配置）就自动装配的IOC容器中，不需要我们手动注入，从而简化了开发，省去繁琐的配置。**



**方案一：通过@ComponentScan({"待扫描的包名"})进行组件扫描**

**方案二：通过@import注解配置**

```
@import({类名.class})
```

**或者创建一个ImportSelector接口的实现类，将其通过上述方法导入，实现类写法如下**

```
public class MyImportSelector implements ImportSelector {
    public String[] selectImports(AnnotationMetadata importingClassMetadata) {
        return new String[]{"com.example.HeaderConfig"};
    }
}
```

**或者也可以使用@Enablexxx注解，分装import注解，然后直接使用这个注解进行配置**

```
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@Import(MyImportSelector.class)
public @interface EnableHeaderConfig {
}
```

**注意上述配置都是配置在springboot启动类上的**

**@SpringBootApplication:该注解标识在SpringBoot工程引导类上，是SpringBoot中最最最重要的注解。该注解由三个部分组成：**

​	**@SpringBootConfiguration：该注解与 @Configuration 注解作用相同，用来声明当前也是一个配置类。**

​	**@ComponentScan：组件扫描，默认扫描当前引导类所在包及其子包。**

​	**@EnableAutoConfiguration：SpringBoot实现自动化配置的核心注解。**



**@Conditional 本身是一个父注解，派生出大量的子注解：**

**@ConditionalOnClass：判断环境中是否有对应字节码文件，才注册bean到IOC容器。**

**@ConditionalOnMissingBean：判断环境中没有对应的bean（类型 或 名称） 指定类型（value）指定名称（name），才注册bean到IOC容器。**

**@ConditionalOnProperty：判断配置文件中有对应属性和值，才注册bean到IOC容器。**

**作用：按照一定的条件进行判断，在满足给定条件后才会注册对应的bean对象到Spring IOC容器中。**

### 自定义starter

**创建 aliyun-oss-spring-boot-starter 模块**

**创建 aliyun-oss-spring-boot-autoconfigure 模块，在starter中引入该模块**

**在 aliyun-oss-spring-boot-autoconfigure 模块中的定义自动配置功能，并定义自动配置文件 META-INF/spring/xxxx.imports**

```
@Configuration
@EnableConfigurationProperties(AliOSSProperties.class)
public class AliOSSAutoConfiguration {
    @Bean
    public AliOSSUtils aliOSSUtils(AliOSSProperties aliOSSProperties){
        AliOSSUtils aliOSSUtils = new AliOSSUtils();
        aliOSSUtils.setAliOSSProperties(aliOSSProperties);
        return aliOSSUtils;
    }
}
```

```
com.aliyun.oss.AliOSSAutoConfiguration
```

## Spring cathe

### 依赖导入

**Spring cathe是一个框架，实现了基于注解的缓存功能，只需要简单的加一个注解，就能实现缓存功能**

**项目中导入maven坐标**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
    <version>2.7.3</version>
</dependency>
```

**在项目中导入Spring-data-redis的相关依赖，spring cathe便可识别要选择哪种缓存实现**

### 常用注解

| 注解           | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| @EnableCathing | 开启缓存注解功能，通常加在启动类上                           |
| @Catheable     | 在方法执行前先查询缓存中是否有数据，如果有数据，则直接返回缓存数据，如果没有缓存数据，调用方法将返回值放到缓存中 |
| @CathePut      | 将方法的缓存值放到缓存中                                     |
| @CatheEvict    | 将一条或多条数据从缓存中删除                                 |
| @CatheConfig   | 该注解加在类上，可以集中设置CatheNames(value)的值,这样类里面的其他注解就不用设置该属性值了 |

### @EnableCathing

```java
@EnableCaching
@SpringBootApplication
@EnableTransactionManagement //开启注解方式的事务管理
@Slf4j
public class SkyApplication {
    public static void main(String[] args) {
        SpringApplication.run(SkyApplication.class, args);
        log.info("server started");
    }
}
```

### @CathePut

```
@Override
@Transactional
@CachePut(key = "#categoryId", cacheNames = "dishCathe")//最后生成的key就是CatheNames::key的形式
public List<DishVO> getByCategoryIdWithFlavor(Long categoryId) {
    List<DishVO> list = new ArrayList<>();
    List<Dish> dishes = dishMapper.getByCategoryId(categoryId);
    for (Dish dish : dishes) {
        DishVO dishVO = new DishVO();
        BeanUtils.copyProperties(dish, dishVO);
        List<DishFlavor> dishFlavorList = dishFlavorMapper.getByDishId(dish.getId());
        dishVO.setFlavors(dishFlavorList);
        list.add(dishVO);
	}
    redisTemplate.opsForValue().set(key, list);
    return list;
}
```

**注意：key属性的值需要用spel表达式，#方法参数名的形式即可获得，如果参数类，例如user,则可以#user.id**

**Spring Cache提供了一些供我们使用的SpEL上下文数据，下表直接摘自Spring官方文档：**

| 名称          | 位置       | 描述                                                         | 示例                   |
| :------------ | :--------- | :----------------------------------------------------------- | :--------------------- |
| methodName    | root对象   | 当前被调用的方法名                                           | `#root.methodname`     |
| method        | root对象   | 当前被调用的方法                                             | `#root.method.name`    |
| target        | root对象   | 当前被调用的目标对象实例                                     | `#root.target`         |
| targetClass   | root对象   | 当前被调用的目标对象的类                                     | `#root.targetClass`    |
| args          | root对象   | 当前被调用的方法的参数列表                                   | `#root.args[0]`        |
| caches        | root对象   | 当前方法调用使用的缓存列表                                   | `#root.caches[0].name` |
| Argument Name | 执行上下文 | 当前被调用的方法的参数，如findArtisan(Artisan artisan),可以通过#artsian.id获得参数 | `#artsian.id`          |
| result        | 执行上下文 | 方法执行后的返回值（仅当方法执行后的判断有效，如 unless cacheEvict的beforeInvocation=false） | `#result`              |

**注意：**

1.当我们要使用root对象的属性作为key时我们也可以将“#root”省略，因为Spring默认使用的就是root对象的属性。 如

```
@Cacheable(key = "targetClass + methodName +#p0")
```

2.使用方法参数时我们可以直接使用“#参数名”或者“#p参数index”。 如：

```
@Cacheable(value="users", key="#id")
@Cacheable(value="users", key="#p0")
```

**关于@CatheEvict和@Catheable的使用跟@CathePut一致，只需要设置好CatheNames还有key这两个属性即可**

`@CachEvict` 的作用 主要针对方法配置，能够根据一定的条件对缓存进行清空 。

| 属性             | 解释                                                         | 示例                                                 |
| :--------------- | :----------------------------------------------------------- | :--------------------------------------------------- |
| allEntries       | 是否清空所有缓存内容，缺省为 false，如果指定为 true，则方法调用后将立即清空所有缓存，如果匹配的是多个数据，则需要设置本属性 | @CachEvict(value=”testcache”,allEntries=true)        |
| beforeInvocation | 是否在方法执行前就清空，缺省为 false，如果指定为 true，则在方法还没有执行的时候就清空缓存，缺省情况下，如果方法执行抛出异常，则不会清空缓存 | @CachEvict(value=”testcache”，beforeInvocation=true) |

## Spring task

**spring task是spring框架提供的任务调度工具，可以按照约定的时间自动执行某个代码逻辑**

**定位：定时任务框架**

**应用场景：**

**信用卡每月还款提醒**

**银行贷款每月还款提醒**

**火车票售票系统处理未支付订单**

**入职纪念日为用户发送通知**

### cron表达式

**定义：cron表达式就是一个字符串用于定义任务触发的时间**

**构成规则：分为6-7个域，由空格分隔开，每个域代表一个含义**

**每个域表达的含义分别是：秒，分钟，小时，日，月，周，年（可选）**

**在线生成网站：https://cron.qqe2.com/**

### 入门案例

**操作步骤：**

**导入maven坐标 spring-context已经存在**

**启动类添加注解@EnableScheduling**

**自定义定时任务类**

**注意：自定义任务类需要加上@Component注解**

```java
@Component
@Slf4j
public class MyTask {
    /*
     * 定时任务，每隔5秒触发一次
     */
    @Scheduled(cron = "0/5 * * * * ?")
    public void executeTask(){
        log.info("定时任务开始执行：{}",new Date());
    }
}
```



## 补充技术点

### ThreadLocal

**ThreadLoacl并不是一个Thread，而是Thread的局部变量，它为每一个线程提供单独一份的存储空间，具有线程隔离的效果，只有在线程内才能获取到对应的值，线程外则不能访问**

| 方法                     | 说明                                 |
| ------------------------ | ------------------------------------ |
| public void set(T value) | 设置当前线程的线程局部变量的值       |
| public T get()           | 返回当前线程所对应的线程局部变量的值 |
| public void remove()     | 移除当前线程的线程局部变量           |

**应用场景：在service层需要获取用户的ID,而用户的ID在jwt令牌里，当我们解析完jwt令牌后，我们就可以把这个id存进ThreadLocal这个存储空间，因为解析jwt令牌和service同属一个线程，因此同时公用一个ThreadLocal内存空间，所以jwt解析阶段所放入的东西，可以被service层访问到**

### Fastjson

**该工具包可以快速把json字符串转换为一个json类，方便数据的获取**

**maven坐标**

```
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
</dependency>
```

**样例代码**

```java
//处理路径规划接口的返回结果
JSONObject routingJSONObject = JSON.parseObject(resultRouting);

if (!routingJSONObject.getString("status").equals("0")) {
    throw new OrderBusinessException("路径规划失败");
}

JSONArray jsonArray = routingJSONObject.getJSONObject("result")
        .getJSONArray("routes");
Integer distance = (Integer) ((JSONObject) jsonArray.get(0)).get("distance");
```



### Lombok

**lombok是一个实用的java类库，能通过注解的形式自动生成构造器，getter/setter,equals,hashcode,toString等方法，并可以自动化生成日志变量**

| 注解                     | 作用                                                         |
| ------------------------ | ------------------------------------------------------------ |
| @Getter/@Setter          | 为所有的属性提供get/set方法                                  |
| @ToString                | 会给类自动生成易阅读的toString方法                           |
| @EqualsAndHashCode       | 根据类所拥有的非静态字段自动重写equals和hashcode方法         |
| @Data                    | 提供了更综合的生成代码功能（@Getter+@Setter+@ToString+@EqualsAndHashCode） |
| @NoArgsConstructor       | 为实体类提供生成无参的构造器方法                             |
| @AllArgsConstructor      | 为实体类生成除了static修饰的字段之外带有各参数的构造器方法   |
| @Builder                 | 注释为你的类生成相对略微复杂的构建器API。比如给Student类加上该注解，效果如下 |
| @RequiredArgsConstructor | 为所有的final字段生成构造函数，一般在spring依赖注入时配合final字段来实现依赖注入 |

```java
Student.builder()
               .sno( "001" )
               .sname( "admin" )
               .sage( 18 )
               .sphone( "110" )
               .build();
```



**maven坐标**

```
<!--lombok-->
<dependency>
	<groupId>org.projectlombok</groupId>
	<artifactId>lombok</artifactId>
</dependency>
```



### Spring boot日期格式化

**应用场景：假设你的前端需要你对日期格式化，但是封装类里的日期是LocalDateTime类型，这时候我们应该如何解决呢**

```
package com.sky.entity;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.io.Serializable;
import java.time.LocalDateTime;

@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class Employee implements Serializable {

    private static final long serialVersionUID = 1L;

    private Long id;

    private String username;

    private String name;

    private String password;

    private String phone;

    private String sex;

    private String idNumber;

    private Integer status;

    //@JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss")
    private LocalDateTime createTime;

    //@JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss")
    private LocalDateTime updateTime;

    private Long createUser;

    private Long updateUser;

}
```

**方案1：在属性上加上注解，对日期进行格式化，@JsonFormat(pattern = yyyy-MM-DD HH:mm:ss"")**

**方案2：在WebConfiguration中扩展Sprinf mvc的消息转换器，统一对日期类型进行格式化处理**

```
@Override
protected void extendMessageConverters(List<HttpMessageConverter<?>> converters) {
    //创建一个消息转换器对象
    MappingJackson2HttpMessageConverter converter = new MappingJackson2HttpMessageConverter();
    //需要为消息转换器设置一个对象转换器，对象转换器可以将java对象序列化成json数据
    converter.setObjectMapper(new JacksonObjectMapper());
    //将自己的消息转换器加入加入容器中
    converters.add(0, converter);


}//将上述方法加入到WebConfiguration类中

```

**JacksonObjectMapper类**

```
package com.sky.json;

import com.fasterxml.jackson.databind.DeserializationFeature;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.module.SimpleModule;
import com.fasterxml.jackson.datatype.jsr310.deser.LocalDateDeserializer;
import com.fasterxml.jackson.datatype.jsr310.deser.LocalDateTimeDeserializer;
import com.fasterxml.jackson.datatype.jsr310.deser.LocalTimeDeserializer;
import com.fasterxml.jackson.datatype.jsr310.ser.LocalDateSerializer;
import com.fasterxml.jackson.datatype.jsr310.ser.LocalDateTimeSerializer;
import com.fasterxml.jackson.datatype.jsr310.ser.LocalTimeSerializer;

import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;

import static com.fasterxml.jackson.databind.DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES;

/**
 * 对象映射器:基于jackson将Java对象转为json，或者将json转为Java对象
 * 将JSON解析为Java对象的过程称为 [从JSON反序列化Java对象]
 * 从Java对象生成JSON的过程称为 [序列化Java对象到JSON]
 */
public class JacksonObjectMapper extends ObjectMapper {

    public static final String DEFAULT_DATE_FORMAT = "yyyy-MM-dd";
    //public static final String DEFAULT_DATE_TIME_FORMAT = "yyyy-MM-dd HH:mm:ss";
    public static final String DEFAULT_DATE_TIME_FORMAT = "yyyy-MM-dd HH:mm";
    public static final String DEFAULT_TIME_FORMAT = "HH:mm:ss";

    public JacksonObjectMapper() {
        super();
        //收到未知属性时不报异常
        this.configure(FAIL_ON_UNKNOWN_PROPERTIES, false);

        //反序列化时，属性不存在的兼容处理
        this.getDeserializationConfig().withoutFeatures(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES);

        SimpleModule simpleModule = new SimpleModule()
                .addDeserializer(LocalDateTime.class, new LocalDateTimeDeserializer(DateTimeFormatter.ofPattern(DEFAULT_DATE_TIME_FORMAT)))
                .addDeserializer(LocalDate.class, new LocalDateDeserializer(DateTimeFormatter.ofPattern(DEFAULT_DATE_FORMAT)))
                .addDeserializer(LocalTime.class, new LocalTimeDeserializer(DateTimeFormatter.ofPattern(DEFAULT_TIME_FORMAT)))
                .addSerializer(LocalDateTime.class, new LocalDateTimeSerializer(DateTimeFormatter.ofPattern(DEFAULT_DATE_TIME_FORMAT)))
                .addSerializer(LocalDate.class, new LocalDateSerializer(DateTimeFormatter.ofPattern(DEFAULT_DATE_FORMAT)))
                .addSerializer(LocalTime.class, new LocalTimeSerializer(DateTimeFormatter.ofPattern(DEFAULT_TIME_FORMAT)));

        //注册功能模块 例如，可以添加自定义序列化器和反序列化器
        this.registerModule(simpleModule);
    }
}
```

#### @JsonFormat

**作用：可以约束时间的接收格式和响应格式 (接收和响应的都是JSON字符串)，将日期类型数据在JSON格式和java.util.Date对象之间转换。**

| 名称     | 作用                                                         |
| -------- | ------------------------------------------------------------ |
| pattern  | 约定时间格式：pattern=“yyyy-MM-dd HH:mm:ss”                  |
| timezone | 指定具体时区： timezone = “GMT+8” or timezone = “Asia/Shanghai” |

#### @DateTimeFormat

**作用：可对java.util.Date、java.uitl.calendar、java.long.Long及Joda时间类型的属性进行标注，主要处理前端时间类型与后端pojo对象中的成员变量进行数据绑定，所约束的时间格式并不会影响后端返回前端的时间类型数据格式**

| 名称    | 作用                                                         |
| ------- | ------------------------------------------------------------ |
| iso     | 类型为DateTimeFormat.ISO，常用值：<br/>DateTimeFormat.ISO.DATE：格式为yyyy-MM-dd<br/>DateTimeFormat.ISO.DATE_TIME：格式为yyyy-MM-dd hh:mm:ss.SSSZ<br/>DateTimeFormat.ISO.TIME：格式为hh:mm:ss.SSSZ<br/>DateTimeFormat.ISO.NONE：表示不使用ISO格式的时间（默认值）<br/> |
| pattern | 类型为String，使用自定义时间格式化字符串，如"yyyy-MM-dd hh:mm:ss" |
| style   | 类型为String，通过样式指定日期时间的格式，由两位字符组成，<br/>第一位表示日期的样式，第二位表示时间的格式，以下是几个常用的可选值：<br/>S：短日期/时间的样式<br/>M：中日期/时间的样式<br/>L：短日期/时间的样式<br/>F：完整日期/时间的样子<br/>-：忽略日期或时间的样式<br/>默认值 style=“SS” |




### 公共字段填充

**基于AOP为所有需要本功能的代码进行功能增强**

**首先需要一个枚举类**

```
public enum OperationType {

    /**
     * 更新操作
     */
    UPDATE,

    /**
     * 插入操作
     */
    INSERT

}
```

**然后需要自定义一个注解，来标记哪些方法需要本功能**

```
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface AutoFill {
    //数据库操作类型：update,insert
    OperationType value();

}
```

**编写aop程序**

```
@Aspect
@Component
@Slf4j
public class AutoFillAspect {
    /**
     * 切入点
     */
    @Pointcut("@annotation(com.sky.annotation.AutoFill)")
    public void autoFillPointCut() {
    }

    /**
     * 前置通知
     */

    @Before("autoFillPointCut()")
    public void autoFill(JoinPoint joinPoint) {
        log.info("开始进行公共字段的自动填充");
        //获取到当前被拦截的方法上的数据库操作类型
        MethodSignature signature = (MethodSignature) joinPoint.getSignature();//获取方法签名对象
        AutoFill autoFill = signature.getMethod().getAnnotation(AutoFill.class);//获取注解对象
        OperationType operationType = autoFill.value();//获取数据库的操作类型


        //获取当前被拦截的方法的参数--实体对象
        Object[] args = joinPoint.getArgs();
        if (args == null || args.length == 0) {
            return;
        }
        Object entity = args[0];

        //准备赋值的数据
        LocalDateTime now = LocalDateTime.now();
        Long currentId = BaseContext.getCurrentId();


        //根据当前不同的操作类型，为对应的属性通过反射来赋值
        if (operationType == OperationType.INSERT) {
            try {
                Method setCreatTime = entity.getClass().getDeclaredMethod(AutoFillConstant.SET_CREATE_TIME, LocalDateTime.class);
                Method setCreateUser = entity.getClass().getDeclaredMethod(AutoFillConstant.SET_CREATE_USER, Long.class);
                Method setUpdateTime = entity.getClass().getDeclaredMethod(AutoFillConstant.SET_UPDATE_TIME, LocalDateTime.class);
                Method setUpdateUser = entity.getClass().getDeclaredMethod(AutoFillConstant.SET_UPDATE_USER, Long.class);
                setCreatTime.invoke(entity, now);
                setCreateUser.invoke(entity,currentId);
                setUpdateTime.invoke(entity,now);
                setUpdateUser.invoke(entity,currentId);

            } catch (NoSuchMethodException | IllegalAccessException | InvocationTargetException e) {
                e.printStackTrace();
            }

        } else {
            Method setUpdateTime = null;
            try {
                setUpdateTime = entity.getClass().getDeclaredMethod(AutoFillConstant.SET_UPDATE_TIME, LocalDateTime.class);
                Method setUpdateUser = entity.getClass().getDeclaredMethod(AutoFillConstant.SET_UPDATE_USER, Long.class);
                setUpdateTime.invoke(entity,now);
                setUpdateUser.invoke(entity,currentId);

            } catch (NoSuchMethodException | InvocationTargetException | IllegalAccessException e) {
                e.printStackTrace();
            }

        }


    }
}
```

### HttpClient

**引入maven依赖**

```
<dependecy>
	<groupId>org.apache.httpcomponents</groupId>
	<artifactId>httpclient</artifactId>
	<version>4.5.13</version>
</dependecy>
```

**发送请求的步骤：**

**1：创建Httpclient对象**

**2：调用Http请求对象**

**3：调用HttpClient的excute方法发送请求**

**基于HttpClient发送一个Get请求**

```java
@SpringBootTest
public class HttpClientTest {
    /*
        发送get方式的请求
     */
    @Test
    public void testGet() throws IOException {
        //创建httpclient对象
        CloseableHttpClient httpClient = HttpClients.createDefault();

        //创建请求对象
        HttpGet httpGet = new HttpGet("http://localhost:8080/user/shop/status");
    
        //发送请求，获取响应结果
        CloseableHttpResponse response = httpClient.execute(httpGet);
    
        //获取反馈回来的状态码
        int statusCode = response.getStatusLine().getStatusCode();
        System.out.println("服务端返回的状态码为：" + statusCode);
    
        //获取反馈回来的数据
        HttpEntity entity = response.getEntity();
        String body = EntityUtils.toString(entity);
        System.out.println("返回的数据体为：" + body);
    
        //关闭资源
        response.close();
        httpClient.close();
    
    }

}


```

**基于HttpClient发送一个Post请求**

```
package com.sky.test;

import com.alibaba.fastjson.JSONObject;
import com.google.gson.JsonObject;
import org.apache.http.HttpEntity;
import org.apache.http.client.HttpClient;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

import java.io.IOException;

@SpringBootTest
public class HttpClientTest {
    /*
        发送post方式的请求
     */
    @Test
    public void testPost() throws IOException {
        //创建httpclient对象
        CloseableHttpClient httpClient = HttpClients.createDefault();

        //创建请求对象
        HttpPost httpPost = new HttpPost("http://localhost:8080/admin/employee/login");
        JSONObject jsonObject = new JSONObject();
        jsonObject.put("username","admin");
        jsonObject.put("password","123456");
        StringEntity stringentity = new StringEntity(jsonObject.toString());
        //指定请求的编码方式
        stringentity.setContentEncoding("utf-8");
        //数据格式
        stringentity.setContentType("application/json");
        httpPost.setEntity(stringentity);

        //发送请求，获取响应结果
        CloseableHttpResponse response = httpClient.execute(httpPost);

        //获取反馈回来的状态码
        int statusCode = response.getStatusLine().getStatusCode();
        System.out.println("服务端返回的状态码为：" + statusCode);

        //获取反馈回来的数据
        HttpEntity entity = response.getEntity();
        String body = EntityUtils.toString(entity);
        System.out.println("返回的数据体为：" + body);

        //关闭资源
        response.close();
        httpClient.close();
    }
}
```

**当然上述方法我们可以封装成一个工具类**

```
package com.sky.utils;

import com.alibaba.fastjson.JSONObject;
import org.apache.http.NameValuePair;
import org.apache.http.client.config.RequestConfig;
import org.apache.http.client.entity.UrlEncodedFormEntity;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.message.BasicNameValuePair;
import org.apache.http.util.EntityUtils;

import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;
import java.util.Map;

/**
 * Http工具类
 */
public class HttpClientUtil {

    static final  int TIMEOUT_MSEC = 5 * 1000;

    /**
     * 发送GET方式请求
     * @param url
     * @param paramMap
     * @return
     */
    public static String doGet(String url,Map<String,String> paramMap){
        // 创建Httpclient对象
        CloseableHttpClient httpClient = HttpClients.createDefault();

        String result = "";
        CloseableHttpResponse response = null;

        try{
            URIBuilder builder = new URIBuilder(url);
            if(paramMap != null){
                for (String key : paramMap.keySet()) {
                    builder.addParameter(key,paramMap.get(key));
                }
            }
            URI uri = builder.build();

            //创建GET请求
            HttpGet httpGet = new HttpGet(uri);

            //发送请求
            response = httpClient.execute(httpGet);

            //判断响应状态
            if(response.getStatusLine().getStatusCode() == 200){
                result = EntityUtils.toString(response.getEntity(),"UTF-8");
            }
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            try {
                response.close();
                httpClient.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

        return result;
    }
    //paramMap代表的就是请求数据，用map的方式进行了封装

    /**
     * 发送POST方式请求
     * @param url
     * @param paramMap
     * @return
     * @throws IOException
     */
    public static String doPost(String url, Map<String, String> paramMap) throws IOException {
        // 创建Httpclient对象
        CloseableHttpClient httpClient = HttpClients.createDefault();
        CloseableHttpResponse response = null;
        String resultString = "";

        try {
            // 创建Http Post请求
            HttpPost httpPost = new HttpPost(url);

            // 创建参数列表
            if (paramMap != null) {
                List<NameValuePair> paramList = new ArrayList();
                for (Map.Entry<String, String> param : paramMap.entrySet()) {
                    paramList.add(new BasicNameValuePair(param.getKey(), param.getValue()));
                }
                // 模拟表单
                UrlEncodedFormEntity entity = new UrlEncodedFormEntity(paramList);
                httpPost.setEntity(entity);
            }

            httpPost.setConfig(builderRequestConfig());

            // 执行http请求
            response = httpClient.execute(httpPost);

            resultString = EntityUtils.toString(response.getEntity(), "UTF-8");
        } catch (Exception e) {
            throw e;
        } finally {
            try {
                response.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

        return resultString;
    }
    //paramMap代表的就是请求数据，用map的方式进行了封装

    /**
     * 发送POST方式请求
     * @param url
     * @param paramMap
     * @return
     * @throws IOException
     */
    public static String doPost4Json(String url, Map<String, String> paramMap) throws IOException {
        // 创建Httpclient对象
        CloseableHttpClient httpClient = HttpClients.createDefault();
        CloseableHttpResponse response = null;
        String resultString = "";

        try {
            // 创建Http Post请求
            HttpPost httpPost = new HttpPost(url);

            if (paramMap != null) {
                //构造json格式数据
                JSONObject jsonObject = new JSONObject();
                for (Map.Entry<String, String> param : paramMap.entrySet()) {
                    jsonObject.put(param.getKey(),param.getValue());
                }
                StringEntity entity = new StringEntity(jsonObject.toString(),"utf-8");
                //设置请求编码
                entity.setContentEncoding("utf-8");
                //设置数据类型
                entity.setContentType("application/json");
                httpPost.setEntity(entity);
            }

            httpPost.setConfig(builderRequestConfig());

            // 执行http请求
            response = httpClient.execute(httpPost);

            resultString = EntityUtils.toString(response.getEntity(), "UTF-8");
        } catch (Exception e) {
            throw e;
        } finally {
            try {
                response.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

        return resultString;
    }
    private static RequestConfig builderRequestConfig() {
        return RequestConfig.custom()
                .setConnectTimeout(TIMEOUT_MSEC)
                .setConnectionRequestTimeout(TIMEOUT_MSEC)
                .setSocketTimeout(TIMEOUT_MSEC).build();
    }

}

```

### WebSocket

#### 基本概念

**webSocket是基于tcp的一种新的网络协议，它实现了浏览器与服务器全双工通信——浏览器和服务器只完成一次握手，两者可以创建持久性的连接，并进行双向数据传输**

**HTTP协议和WebSocket协议对比：**

**Http是短连接，WebSocket是长连接**

**Http通信是单向的，基于请求响应模式，WebSocket支持双向通信**

**二者的底层都是tcp连接**

**应用场景：需要实时更新的数据，例如**

**视频弹幕**

**网页聊天**

**体育实况更新**

**股票基金报价实时更新**

#### **使用步骤**

**1：提供一个页面作为WebSocket客户端**

**2：导入WebSocket的maven坐标**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-websocket</artifactId>
</dependency>
```

**3：导入WebSocket服务端组件WebSocketServer,用于和客户端通信**

```java
/**
 * WebSocket服务
 */
@Component
@ServerEndpoint("/ws/{sid}")
public class WebSocketServer {

    //存放会话对象
    private static Map<String, Session> sessionMap = new HashMap();

    /**
     * 连接建立成功调用的方法
     */
    @OnOpen
    public void onOpen(Session session, @PathParam("sid") String sid) {
        System.out.println("客户端：" + sid + "建立连接");
        sessionMap.put(sid, session);
    }

    /**
     * 收到客户端消息后调用的方法
     *
     * @param message 客户端发送过来的消息
     */
    @OnMessage
    public void onMessage(String message, @PathParam("sid") String sid) {
        System.out.println("收到来自客户端：" + sid + "的信息:" + message);
    }

    /**
     * 连接关闭调用的方法
     *
     * @param sid
     */
    @OnClose
    public void onClose(@PathParam("sid") String sid) {
        System.out.println("连接断开:" + sid);
        sessionMap.remove(sid);
    }

    /**
     * 群发
     *
     * @param message
     */
    public void sendToAllClient(String message) {
        Collection<Session> sessions = sessionMap.values();
        for (Session session : sessions) {
            try {
                //服务器向客户端发送消息
                session.getBasicRemote().sendText(message);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }

}
```

**4：导入配置类WebSocketConfiguration,注册WebSocket的服务端组件**

```java
@Configuration
public class WebSocketConfiguration {

    @Bean
    public ServerEndpointExporter serverEndpointExporter() {
        return new ServerEndpointExporter();
    }

}
```

**5：导入定时任务类WebSocketTask,定时向客户端推送数据**

```Java
@Component
public class WebSocketTask {
    @Autowired
    private WebSocketServer webSocketServer;

    /**
     * 通过WebSocket每隔5秒向客户端发送消息
     */
    @Scheduled(cron = "0/5 * * * * ?")
    public void sendMessageToClient() {
        webSocketServer.sendToAllClient("这是来自服务端的消息：" + DateTimeFormatter.ofPattern("HH:mm:ss").format(LocalDateTime.now()));
    }
}
```

### HuTool

**maven依赖**

```xml
<dependency>
	<groupId>cn.hutool</groupId>
	<artifactId>hutool-all</artifactId>
	<version>5.8.11</version>
</dependency>
```

**类似于Apache Commons的工具包，详细使用请见使用文档**



### Swagger

#### 如何使用

**导入maven项目**

```
<dependency>
    <groupId>com.github.xiaoymin</groupId>
    <artifactId>knife4j-spring-boot-starter</artifactId>
    <version>3.0.2</version>
</dependency>
```

**在配置类中加入knife4j相关配置**

```WebMvcConfiguration
@Bean
 public Docket docket(){
   ApiInfo apiInfo = new ApiInfoBuilder()
       .title(“苍穹外卖项目接口文档”)
       .version(“2.0”)
       .description(“苍穹外卖项目接口文档")
       .build();

   Docket docket = new Docket(DocumentationType.SWAGGER_2)
       .apiInfo(apiInfo)
       .select()
       //指定生成接口需要扫描的包
       .apis(RequestHandlerSelectors.basePackage("com.sky.controller"))
       .paths(PathSelectors.any())
       .build();

   return docket;
 }
```

**设置静态资源映射。否则接口文档页面无法访问**

```WebMvcConfiguration

/**
 * 设置静态资源映射
 * @param registry
 **/
protected void addResourceHandlers(ResourceHandlerRegistry registry) {
   log.info(“开始设置静态资源映射...");
   registry.addResourceHandler("/doc.html").addResourceLocations("classpath:/META-INF/resources/");
   registry.addResourceHandler("/webjars/**").addResourceLocations("classpath:/META-			INF/resources/webjars/");
 }
```

#### 常用注解

| 注解              | 说明                                                 |
| ----------------- | ---------------------------------------------------- |
| @Api              | 用在类上，例如Controller,表示对类的说明              |
| @ApiModel         | 用在类上，例如entity,DTO,VO                          |
| @ApiModelPropetry | 用在属性上，描述属性信息                             |
| @ApiOperation     | 用在方法上，例如Controller的方法，说明方法的用途作用 |
| @ApiParam         | 用在方法的参数上用于说明描述参数                     |



### Apache ECharts

**Apache ECharts是一款基于javascript的数据可视化图表库，提供直观，生动，可交互，可个性化定制的可视化图标**

**使用教程：https://echarts.apache.org/handbook/zh/get-started/**

### Apache POI

**Apache POI是一个处理Microsoft Office各种文件格式的开源项目，就是在java程序中进行Office的各种文件操作**

**应用场景：银行网银系统导出交易明细，各种业务系统导出excel报表，批量导入业务数据**

#### 入门案例

**maven坐标**

```xml
<!-- poi -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi</artifactId>
</dependency>
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
</dependency>
```

**写入文件操作**

```
public class Main {
    public static void main(String[] args) throws IOException {
        //在内存中创建一个excel文件
        XSSFWorkbook excel = new XSSFWorkbook();
        //在excel表中创建一个sheet页
        XSSFSheet sheet = excel.createSheet("info");
        //在Sheet中创建行对象,rowNum编号从0开始
        XSSFRow row = sheet.createRow(0);
        //在行上面创建单元格,注意这里单元格的索引也是从0开始
        XSSFCell cell = row.createCell(0);
        //向单元格里填写内容
        cell.setCellValue("姓名");
        //通过输出流将内存中的Excel文件输出
        FileOutputStream out = new FileOutputStream(new File("D:\\info.xlsx"));
        excel.write(out);
        //关闭资源
        excel.close();
        out.close();

    }
}
```

**读取文件操作**

```java
public class Main {
    public static void main(String[] args) throws IOException {
        //读取磁盘已经存在的excel文件
        XSSFWorkbook excel = new XSSFWorkbook(new FileInputStream(
                new File("D:\\info.xlsx")));
        //读取Excel表中的第一个sheet页,下标从0开始
        XSSFSheet sheet = excel.getSheetAt(0);
        //获取有文字的行里最后一行的行号，注意下标从0开始
        int lastRowNum = sheet.getLastRowNum();
        for (int i = 0; i <= lastRowNum; i++) {
            //获取某一行
            XSSFRow row = sheet.getRow(i);
            //获取有文字的列列里面的最后一列
            int cellNum = row.getLastCellNum();
            for (int j = 0; j < cellNum; j++) {
                //获取当前单元格的值
                String cellValue = row.getCell(j).getStringCellValue();
                System.out.println(cellValue);
            }
        }
    }
}
```



### Apache Commons

**Apache Commons包含了很多开源的工具，用于解决平时编程经常会遇到的问题，减少重复劳动。下面是我这几年做开发过程中自己用过的工具类做简单介绍。**

#### **Commons简介**

| **组件**              | **功能介绍**                                                 |
| --------------------- | ------------------------------------------------------------ |
| commons-beanutils     | 提供了对于JavaBean进行各种操作，克隆对象,属性等等.           |
| commons-betwixt       | XML与Java对象之间相互转换.                                   |
| commons-codec         | 处理常用的编码方法的工具类包 例如DES、SHA1、MD5、Base64等.   |
| commons-collections   | java集合框架操作.                                            |
| commons-compress      | java提供文件打包 压缩类库.                                   |
| commons-configuration | 一个java应用程序的配置管理类库.                              |
| commons-dbcp          | 提供数据库连接池服务.                                        |
| commons-dbutils       | 提供对jdbc 的操作封装来简化数据查询和记录读取操作.           |
| commons-email         | java发送邮件 对javamail的封装.                               |
| commons-fileupload    | 提供文件上传功能.                                            |
| commons-httpclient    | 提供HTTP客户端与服务器的各种通讯操作. 现在已改成HttpComponents |
| commons-io            | io工具的封装.                                                |
| commons-lang          | Java基本对象方法的工具类包 如：StringUtils,ArrayUtils,DateUtils,DateFormatUtils等等. |
| commons-logging       | 提供的是一个Java 的日志接口.                                 |
| commons-validator     | 提供了客户端和服务器端的数据验证框架.                        |

#### **Maven依赖 **

```
<!-- https://mvnrepository.com/artifact/commons-beanutils/commons-beanutils -->
<dependency>
    <groupId>commons-beanutils</groupId>
    <artifactId>commons-beanutils</artifactId>
    <version>1.9.3</version>
</dependency>

<!-- https://mvnrepository.com/artifact/commons-betwixt/commons-betwixt -->
<dependency>
    <groupId>commons-betwixt</groupId>
    <artifactId>commons-betwixt</artifactId>
    <version>0.8</version>
</dependency>

<!-- https://mvnrepository.com/artifact/commons-codec/commons-codec -->
<dependency>
    <groupId>commons-codec</groupId>
    <artifactId>commons-codec</artifactId>
    <version>1.10</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.apache.commons/commons-collections4 -->
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-collections4</artifactId>
    <version>4.1</version>
</dependency>
<!-- https://mvnrepository.com/artifact/commons-collections/commons-collections -->
<dependency>
    <groupId>commons-collections</groupId>
    <artifactId>commons-collections</artifactId>
    <version>3.2.1</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.apache.commons/commons-compress -->
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-compress</artifactId>
    <version>1.18</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.apache.commons/commons-configuration2 -->
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-configuration2</artifactId>
    <version>2.2</version>
</dependency>
<!-- https://mvnrepository.com/artifact/commons-configuration/commons-configuration -->
<dependency>
    <groupId>commons-configuration</groupId>
    <artifactId>commons-configuration</artifactId>
    <version>1.10</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.apache.commons/commons-dbcp2 -->
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-dbcp2</artifactId>
    <version>2.1.1</version>
</dependency>
<!-- https://mvnrepository.com/artifact/commons-dbcp/commons-dbcp -->
<dependency>
    <groupId>commons-dbcp</groupId>
    <artifactId>commons-dbcp</artifactId>
    <version>1.4</version>
</dependency>

<!-- https://mvnrepository.com/artifact/commons-dbutils/commons-dbutils -->
<dependency>
    <groupId>commons-dbutils</groupId>
    <artifactId>commons-dbutils</artifactId>
    <version>1.6</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.apache.commons/commons-email -->
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-email</artifactId>
    <version>1.4</version>
</dependency>
<!-- https://mvnrepository.com/artifact/commons-email/commons-email -->
<dependency>
    <groupId>commons-email</groupId>
    <artifactId>commons-email</artifactId>
    <version>1.0</version>
</dependency>

<!-- https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload -->
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.1</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.apache.httpcomponents/httpclient -->
<dependency>
    <groupId>org.apache.httpcomponents</groupId>
    <artifactId>httpclient</artifactId>
    <version>4.5.12</version>
</dependency>
<!-- https://mvnrepository.com/artifact/commons-httpclient/commons-httpclient -->
<dependency>
    <groupId>commons-httpclient</groupId>
    <artifactId>commons-httpclient</artifactId>
    <version>3.1</version>
</dependency>

<!-- https://mvnrepository.com/artifact/commons-io/commons-io -->
<dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>2.6</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.apache.commons/commons-io -->
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-io</artifactId>
    <version>1.3.2</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.apache.commons/commons-lang3 -->
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.9</version>
</dependency>
<!-- https://mvnrepository.com/artifact/commons-lang/commons-lang -->
<dependency>
    <groupId>commons-lang</groupId>
    <artifactId>commons-lang</artifactId>
    <version>2.6</version>
</dependency>

<!-- https://mvnrepository.com/artifact/commons-logging/commons-logging -->
<dependency>
    <groupId>commons-logging</groupId>
    <artifactId>commons-logging</artifactId>
    <version>1.2</version>
</dependency>

<!-- https://mvnrepository.com/artifact/commons-validator/commons-validator -->
<dependency>
    <groupId>commons-validator</groupId>
    <artifactId>commons-validator</artifactId>
    <version>1.6</version>
</dependency>
```



#### **1、commons-beanutils** 

**提供了对于JavaBean进行各种操作， 比如对象,属性复制等等。**

```
import java.util.HashMap;
import java.util.Map;
import org.apache.commons.beanutils.BeanUtils;
import org.apache.commons.beanutils.PropertyUtils;

public class CommonsBeanUtils {
    public static void main(String[] args) throws Exception {
        // ****************************************************************************
        Person person = new Person();
        person.setName("tom");
        person.setAge(21);
        // 克隆对象
        Person person2 = (Person) BeanUtils.cloneBean(person);
        System.out.println(person2.getName() + ">>" + person2.getAge());
        // ****************************************************************************
        Map<String, String> map = new HashMap<String, String>();
        map.put("name", "tom");
        map.put("email", "tom@");
        map.put("age", "21");
        // 将map转化为一个Person对象
        Person person3 = new Person();
        BeanUtils.populate(person3, map);
        System.out.println(person3.getName() + ">>" + person3.getAge());
        // 通过上面的一行代码，此时person的属性就已经具有了上面所赋的值了。
        // 将一个Bean转化为一个Map对象了，如下：
        Map<String, String> map2 = BeanUtils.describe(person3);
        System.out.println(map2.get("name") + ">>" + map2.get("age"));
        // ****************************************************************************
        Person person4 = new Person();
        person4.setName("andy");
        // 反射调用get方法
        String name = (String) PropertyUtils.getProperty(person4, "name");
        System.out.println(name);
        // 反射调用set方法
        PropertyUtils.setProperty(person4, "age", 25);
        System.out.println(person4.getAge());
    }
}
```



#### **2、commons-betwixt** 

**XML与Java对象之间相互转换。**

```
import java.io.StringReader;
import java.io.StringWriter;
import org.apache.commons.betwixt.io.BeanReader;
import org.apache.commons.betwixt.io.BeanWriter;

public class CommonsBetwixt {
    public static void main(String[] args) throws Exception {
        // ****************************创建一个例子Bean，并将它转化为XML ************************************************
        // 先创建一个StringWriter，我们将把它写入为一个字符串
        StringWriter outputWriter = new StringWriter();
        // Betwixt在这里仅仅是将Bean写入为一个片断
        // 所以如果要想完整的XML内容，我们应该写入头格式
        outputWriter.write("<?xml version=’1.0′ encoding=’UTF-8′ ?>\n");
        // 创建一个BeanWriter，其将写入到我们预备的stream中
        BeanWriter beanWriter = new BeanWriter(outputWriter);
        // 配置betwixt
        // 更多详情请参考java docs 或最新的文档
        beanWriter.getXMLIntrospector().getConfiguration().setAttributesForPrimitives(false);
        beanWriter.getBindingConfiguration().setMapIDs(false);
        beanWriter.enablePrettyPrint();
        // 如果这个地方不传入XML的根节点名，Betwixt将自己猜测是什么
        // 但是让我们将例子Bean名作为根节点吧
        beanWriter.write("person", new Person("John Smith", 21));
        // 输出结果
        System.out.println(outputWriter.toString());
        // Betwixt写的是片断而不是一个文档，所以不要自动的关闭掉writers或者streams，
        // 但这里仅仅是一个例子，不会做更多事情，所以可以关掉
        outputWriter.close();
        // ****************************将XML转化为JavaBean ************************************************
        // 先创建一个XML，由于这里仅是作为例子，所以我们硬编码了一段XML内容
        StringReader xmlReader = new StringReader("<?xml version='1.0' encoding='UTF-8' ?> <person><age>25</age><name>James Smith</name></person>");
        // 创建BeanReader
        BeanReader beanReader = new BeanReader();
        // 配置reader
        beanReader.getXMLIntrospector().getConfiguration().setAttributesForPrimitives(false);
        beanReader.getBindingConfiguration().setMapIDs(false);
        // 注册beans，以便betwixt知道XML将要被转化为一个什么Bean
        beanReader.registerBeanClass("person", Person.class);
        // 现在我们对XML进行解析
        Person person = (Person) beanReader.parse(xmlReader);
        // 输出结果
        System.out.println(person);
    }
}
```



#### **3、commons-codec** 

**公共的编解码实现，比如Base64, Hex, MD5,Phonetic and URLs等等。**



```
import org.apache.commons.codec.binary.Base64;

public class CommonsCodec {
    public static void main(String[] args) throws Exception {
        Base64 base64 = new Base64();
        String encodestr = base64.encodeToString("abcd".getBytes("UTF-8"));
        System.out.println("Base64 编码后：" + encodestr);
        
        String decodestr = new String(Base64.decodeBase64("YWJjZA=="));  
        System.out.println("Base64 解码后："+decodestr);  
    }
}
```



#### **4、commons-collections**

**对java.util的扩展封装，处理数据还是挺灵活的。
**

**org.apache.commons.collections – Commons Collections自定义的一组公用的接口和工具类**

**org.apache.commons.collections.bag – 实现Bag接口的一组类**

**org.apache.commons.collections.bidimap – 实现BidiMap系列接口的一组类**

**org.apache.commons.collections.buffer – 实现Buffer接口的一组类**

**org.apache.commons.collections.collection – 实现java.util.Collection接口的一组类**

**org.apache.commons.collections.comparators – 实现java.util.Comparator接口的一组类**

**org.apache.commons.collections.functors – Commons Collections自定义的一组功能类**

**org.apache.commons.collections.iterators – 实现java.util.Iterator接口的一组类**

**org.apache.commons.collections.keyvalue – 实现集合和键/值映射相关的一组类**

**org.apache.commons.collections.list – 实现java.util.List接口的一组类**

**org.apache.commons.collections.map – 实现Map系列接口的一组类**

**org.apache.commons.collections.set – 实现Set系列接口的一组类**



```
import java.util.ArrayList;
import java.util.Collection;
import java.util.List;

import org.apache.commons.collections.BidiMap;
import org.apache.commons.collections.CollectionUtils;
import org.apache.commons.collections.OrderedMap;
import org.apache.commons.collections.bidimap.TreeBidiMap;
import org.apache.commons.collections.map.LinkedMap;

public class CommonsCollections {
    public static void main(String[] args) {
        //得到集合里按顺序存放的key之后的某一Key
        OrderedMap map = new LinkedMap ();
        map.put("FIVE", "5");
        map.put("SIX", "6");
        map.put("SEVEN", "7");
        map.firstKey(); // returns "FIVE"
        map.nextKey("FIVE"); // returns "SIX"
        map.nextKey("SIX"); // returns "SEVEN"

        //通过key得到value 通过value得到key 将map里的key和value对调
        BidiMap bidi = new TreeBidiMap();
        bidi.put("SIX", "6");
        bidi.get("SIX"); // returns "6"
        bidi.getKey("6"); // returns "SIX"
        // bidi.removeValue("6"); // removes the mapping
        BidiMap inverse = bidi.inverseBidiMap(); // returns a map with keys and values swapped
        System.out.println(inverse);

        //得到两个集合中相同的元素
        List<String> list1 = new ArrayList<String>();
        list1.add("1");
        list1.add("2");
        list1.add("3");
        List<String> list2 = new ArrayList<String>();
        list2.add("2");
        list2.add("3");
        list2.add("5");
        Collection c = CollectionUtils.retainAll(list1, list2);
        System.out.println(c);
    }
}
```



#### **5、commons-compress** 

**commons compress中的打包、压缩类库。** 



```
import java.io.File;
import java.io.FileInputStream;

import org.apache.commons.compress.archivers.zip.ZipArchiveEntry;
import org.apache.commons.compress.archivers.zip.ZipArchiveOutputStream;

public class CommonsCompress {
    public static void main(String[] args) throws Exception {
        // 创建压缩对象
        ZipArchiveEntry entry = new ZipArchiveEntry("CompressTest");
        // 要压缩的文件
        File f = new File("e:\\test.pdf");
        FileInputStream fis = new FileInputStream(f);
        // 输出的对象 压缩的文件
        ZipArchiveOutputStream zipOutput = new ZipArchiveOutputStream(new File("e:\\test.zip"));
        zipOutput.putArchiveEntry(entry);
        int i = 0, j;
        while ((j = fis.read()) != -1) {
            zipOutput.write(j);
            i++;
            System.out.println(i);
        }
        zipOutput.closeArchiveEntry();
        zipOutput.close();
        fis.close();
    }
}
```



#### 6、commons-configuration

**用来帮助处理配置文件的，支持很多种存储方式。**

**1Properties files**

**XML documents**

**Property list files (.plist)**

**JNDI**

**JDBC Datasource**

**System properties**

**Applet parameters**

**Servlet parameters**



```
PropertiesConfiguration config = new PropertiesConfiguration("usergui.properties");  
config.setProperty("colors.background", "#000000);  
config.save();  
  
config.save("usergui.backup.properties);//save a copy  
Integer integer = config.getInteger("window.width");  
```



#### **7、commons-dbcp**

**(Database Connection Pool)是一个依赖Jakarta commons-pool对象池机制的数据库连接池,Tomcat的数据源使用的就是DBCP。**



```
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import javax.sql.DataSource;
import org.apache.commons.dbcp.ConnectionFactory;
import org.apache.commons.dbcp.DriverManagerConnectionFactory;
import org.apache.commons.dbcp.PoolableConnectionFactory;
import org.apache.commons.dbcp.PoolingDataSource;
import org.apache.commons.pool.ObjectPool;
import org.apache.commons.pool.impl.GenericObjectPool;

public class CommonsDbcp {
    public static void main(String[] args) {
        System.out.println("加载jdbc驱动");
        try {
            Class.forName("oracle.jdbc.driver.OracleDriver");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
        System.out.println("Done.");
        //
        System.out.println("设置数据源");
        DataSource dataSource = setupDataSource("jdbc:oracle:thin:@localhost:1521:test");
        System.out.println("Done.");

        //
        Connection conn = null;
        Statement stmt = null;
        ResultSet rset = null;

        try {
            System.out.println("Creating connection.");
            conn = dataSource.getConnection();
            System.out.println("Creating statement.");
            stmt = conn.createStatement();
            System.out.println("Executing statement.");
            rset = stmt.executeQuery("select * from person");
            System.out.println("Results:");
            int numcols = rset.getMetaData().getColumnCount();
            while (rset.next()) {
                for (int i = 0; i <= numcols; i++) {
                    System.out.print("\t" + rset.getString(i));
                }
                System.out.println("");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (rset != null)
                    rset.close();
            } catch (Exception e) {
            }
            try {
                if (stmt != null)
                    stmt.close();
            } catch (Exception e) {
            }
            try {
                if (conn != null)
                    conn.close();
            } catch (Exception e) {
            }
        }
    }

    public static DataSource setupDataSource(String connectURI) {
        // 设置连接地址
        ConnectionFactory connectionFactory = new DriverManagerConnectionFactory(connectURI, null);

        // 创建连接工厂
        PoolableConnectionFactory poolableConnectionFactory = new PoolableConnectionFactory(connectionFactory, null, null, connectURI, false, false);

        // 获取GenericObjectPool 连接的实例
        ObjectPool connectionPool = new GenericObjectPool(poolableConnectionFactory);

        // 创建 PoolingDriver
        PoolingDataSource dataSource = new PoolingDataSource(connectionPool);

        return dataSource;
    }
}
```



#### **8、commons-dbutils** 

**Apache组织提供的一个资源JDBC工具类库，它是对JDBC的简单封装，对传统操作数据库的类进行二次封装，可以把结果集转化成List。，同时也不影响程序的性能。
**

**DbUtils类：启动类**
**ResultSetHandler接口：转换类型接口**
**MapListHandler类：实现类，把记录转化成List**
**BeanListHandler类：实现类，把记录转化成List，使记录为JavaBean类型的对象**
**Qrery Runner类：执行SQL语句的类**



```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.util.List;
import java.util.Map;
import org.apache.commons.dbutils.DbUtils;
import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.BeanListHandler;
import org.apache.commons.dbutils.handlers.MapListHandler;

public class CommonsDbutils {

    public static void main(String[] args) {
        Connection conn = null;
        String url = "jdbc:mysql://localhost:3306/ptest";
        String jdbcDriver = "com.mysql.jdbc.Driver";
        String user = "root";
        String password = "ptest";

        DbUtils.loadDriver(jdbcDriver);
        //****************************转换成list  ************************************
        try {
            conn = DriverManager.getConnection(url, user, password);
            QueryRunner qr = new QueryRunner();
            List results = (List) qr.query(conn, "select id,name from person",new BeanListHandler(Person.class));
            for (int i = 0; i < results.size(); i++) {
                Person p = (Person) results.get(i);
                System.out.println("age:" + p.getAge() + ",name:" + p.getName());
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            DbUtils.closeQuietly(conn);
        }
        //****************************转换成map  ************************************
        try {
            conn = DriverManager.getConnection(url, user, password);
            QueryRunner qr = new QueryRunner();
            List results = (List) qr.query(conn, "select age,name from person",new MapListHandler());
            for (int i = 0; i < results.size(); i++) {
                Map map = (Map) results.get(i);
                System.out.println("age:" + map.get("age") + ",name:"+ map.get("name"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            DbUtils.closeQuietly(conn);
        }
    }
}
```



#### **9、commons-email** 

**提供的一个开源的API，是对javamail的封装。**



```
import org.apache.commons.mail.DefaultAuthenticator;
import org.apache.commons.mail.Email;
import org.apache.commons.mail.EmailException;
import org.apache.commons.mail.SimpleEmail;

public class CommosEmail {
    public static void main(String[] args) throws EmailException {
        Email email = new SimpleEmail();
        email.setHostName("smtp.googlemail.com");
        email.setSmtpPort(465);
        email.setAuthenticator(new DefaultAuthenticator("username", "password"));
        email.setSSLOnConnect(true);
        email.setFrom("user@gmail.com");
        email.setSubject("TestMail");
        email.setMsg("This is a test mail ... :-)");
        email.addTo("foo@bar.com");
        email.send();
    }
}
```



#### **10、commons-fileupload**

**java web文件上传功能。**



```
//检查请求是否含有上传文件  
    boolean isMultipart = ServletFileUpload.isMultipartContent(request);  

    //如果你的应用近于最简单的情况，上面的处理就够了。但我们有时候还是需要更多的控制。  
    //下面提供了几种控制选择
    DiskFileItemFactory factory = new DiskFileItemFactory();  
  
    // Set factory constraints  
    factory.setSizeThreshold(yourMaxMemorySize);  
    factory.setRepository(yourTempDirectory);  
  
    // Create a new file upload handler  
    ServletFileUpload upload = new ServletFileUpload(factory);  
  
    // 设置最大上传大小  
    upload.setSizeMax(yourMaxRequestSize);  
  
    // 解析所有请求  
    List items = upload.parseRequest(request);  
  
    // Create a factory for disk-based file items  
    DiskFileItemFactory factory = new DiskFileItemFactory(  
            yourMaxMemorySize, yourTempDirectory);  
  
    //一旦解析完成，你需要进一步处理item的列表。
    Iterator iter = items.iterator();  
    while (iter.hasNext()) {  
        FileItem item = (FileItem) iter.next();  
  
        if (item.isFormField()) {  
            processFormField(item);  
        } else {  
            processUploadedFile(item);  
        }  
    }  
  
    //区分数据是否为简单的表单数据，如果是简单的数据
    if (item.isFormField()) {  
        String name = item.getFieldName();  
        String value = item.getString();  
        //...省略步骤  
    }  
  
    //如果是提交的文件：  
    if (!item.isFormField()) {  
        String fieldName = item.getFieldName();  
        String fileName = item.getName();  
        String contentType = item.getContentType();  
        boolean isInMemory = item.isInMemory();  
        long sizeInBytes = item.getSize();  
        //...省略步骤  
    }  
  
    //对于这些item，我们通常要把它们写入文件，或转为一个流  
    if (writeToFile) {  
        File uploadedFile = new File(...);  
        item.write(uploadedFile);  
    } else {  
        InputStream uploadedStream = item.getInputStream();  
        //...省略步骤  
        uploadedStream.close();  
    }  
  
    //或转为字节数组保存在内存中
    byte[] data = item.get();  
    //...省略步骤  
    //如果这个文件真的很大，你可能会希望向用户报告到底传了多少到服务端，让用户了解上传的过程
    ProgressListener progressListener = new ProgressListener(){  
       public void update(long pBytesRead, long pContentLength, int pItems) {  
           System.out.println("We are currently reading item " + pItems);  
           if (pContentLength == -1) {  
               System.out.println("So far, " + pBytesRead + " bytes have been read.");  
           } else {  
               System.out.println("So far, " + pBytesRead + " of " + pContentLength  
                                  + " bytes have been read.");  
           }  
       }  
    };  
    upload.setProgressListener(progressListener);  
```



#### **11、commons-httpclient**

 **基于HttpCore实 现的一个HTTP/1.1兼容的HTTP客户端，它提供了一系列可重用的客户端身份验证、HTTP状态保持、HTTP连接管理module。**



```
import java.io.IOException;
import org.apache.commons.httpclient.*;
import org.apache.commons.httpclient.methods.GetMethod;
import org.apache.commons.httpclient.params.HttpMethodParams;

public class CommonsHttpclient {
    public static void main(String[] args) {
        // 构造HttpClient的实例
        HttpClient httpClient = new HttpClient();
        // 创建GET方法的实例
        GetMethod getMethod = new GetMethod("http://www.ibm.com");
        // 使用系统提供的默认的恢复策略
        getMethod.getParams().setParameter(HttpMethodParams.RETRY_HANDLER,
                new DefaultHttpMethodRetryHandler());
        try {
            // 执行getMethod
            int statusCode = httpClient.executeMethod(getMethod);
            if (statusCode != HttpStatus.SC_OK) {
                System.err.println("Method failed: "
                        + getMethod.getStatusLine());
            }
            // 读取内容
            byte[] responseBody = getMethod.getResponseBody();
            // 处理内容
            System.out.println(new String(responseBody));
        } catch (HttpException e) {
            // 发生致命的异常，可能是协议不对或者返回的内容有问题
            System.out.println("Please check your provided http address!");
            e.printStackTrace();
        } catch (IOException e) {
            // 发生网络异常
            e.printStackTrace();
        } finally {
            // 释放连接
            getMethod.releaseConnection();
        }

        // 构造HttpClient的实例
        HttpClient httpClient = new HttpClient();
        // 创建POST方法的实例
        String url = "http://www.oracle.com/";
        PostMethod postMethod = new PostMethod(url);
        // 填入各个表单域的值
        NameValuePair[] data = { new NameValuePair("id", "youUserName"),
                new NameValuePair("passwd", "yourPwd") };
        // 将表单的值放入postMethod中
        postMethod.setRequestBody(data);
        // 执行postMethod
        int statusCode = httpClient.executeMethod(postMethod);
        // HttpClient对于要求接受后继服务的请求，象POST和PUT等不能自动处理转发
        // 301或者302
        if (statusCode == HttpStatus.SC_MOVED_PERMANENTLY
                || statusCode == HttpStatus.SC_MOVED_TEMPORARILY) {
            // 从头中取出转向的地址
            Header locationHeader = postMethod.getResponseHeader("location");
            String location = null;
            if (locationHeader != null) {
                location = locationHeader.getValue();
                System.out.println("The page was redirected to:" + location);
            } else {
                System.err.println("Location field value is null.");
            }
            return;
        }
    }
}
```



#### **12、commons-io**

**对java.io的扩展 操作文件非常方便。**



```
import java.io.BufferedReader;
import java.io.File;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URL;
import java.util.List;

import org.apache.commons.io.FileSystemUtils;
import org.apache.commons.io.FileUtils;
import org.apache.commons.io.IOUtils;

public class CommonsIo {
    public static void main(String[] args) throws Exception {
        // 1．读取Stream
        // 标准代码：
        InputStream in = new URL("http://jakarta.apache.org").openStream();
        InputStreamReader inR = new InputStreamReader(in);
        BufferedReader buf = new BufferedReader(inR);
        String line;
        while ((line = buf.readLine()) != null) {
            System.out.println(line);
        }
        in.close();
        
        // 使用IOUtils
        InputStream in2 = new URL("http://jakarta.apache.org").openStream();
        try {
            System.out.println(IOUtils.toString(in2));
        } finally {
            IOUtils.closeQuietly(in);
        }

        // 2．读取文件
        File file = new File("/commons/io/project.properties");
        List lines = FileUtils.readLines(file, "UTF-8");

        // 3．察看剩余空间
        long freeSpace = FileSystemUtils.freeSpace("C:/");
    }
}
```



#### **13、commos-lang** 

**主要是一些公共的工具集合，比如对字符、数组的操作等等。**

![](D:assets\1582099-20201201203826418-85487697.png)

```
import java.util.Calendar;
import java.util.Date;

import org.apache.commons.lang.ArrayUtils;
import org.apache.commons.lang.ClassUtils;
import org.apache.commons.lang.RandomStringUtils;
import org.apache.commons.lang.StringEscapeUtils;
import org.apache.commons.lang.StringUtils;
import org.apache.commons.lang.time.DateFormatUtils;
import org.apache.commons.lang.time.DateUtils;

public class CommonsLang {
    public static void main(String[] args) throws Exception {
        //********************************ArrayUtils***************************************
        // 将两个数组合并为一个数组
        String[] s1 = new String[] { "1", "2", "3" };
        String[] s2 = new String[] { "a", "b", "c" };
        String[] s = (String[]) ArrayUtils.addAll(s1, s2);
        for (int i = 0; i < s.length; i++) {
            System.out.println(s[i]);
        }
        String str = ArrayUtils.toString(s);
        str = str.substring(1, str.length() - 1);
        System.out.println(str + ">>" + str.length());
        //********************************StringUtils***************************************
        // 截取从from开始字符串
        StringUtils.substringAfter("SELECT * FROM PERSON ", "from");
        // 判断该字符串是不是为数字(0~9)组成，如果是，返回true 但该方法不识别有小数点和请注意
        StringUtils.isNumeric("454534"); // 返回true
        // 取得类名
        System.out.println(ClassUtils.getShortClassName(CommonsLang.class));
        // 取得其包名
        System.out.println(ClassUtils.getPackageName(CommonsLang.class));
        // 五位的随机字母和数字 
        System.out.println(RandomStringUtils.randomAlphanumeric(5));
        // StringEscapeUtils
        System.out.println(StringEscapeUtils.escapeHtml("<html>"));
        // 输出结果为<html>
        System.out.println(StringEscapeUtils.escapeJava("String"));
        // StringUtils,判断是否是空格字符
        System.out.println(StringUtils.isBlank("   "));
        // 将数组中的内容以,分隔
        System.out.println(StringUtils.join(s1, ","));
        // 在右边加下字符,使之总长度为6
        System.out.println(StringUtils.rightPad("abc", 6, 'T'));
        // 首字母大写 
        System.out.println(StringUtils.capitalize("abc"));
        // Deletes all whitespaces from a String 删除所有空格
        System.out.println(StringUtils.deleteWhitespace("   ab  c  "));
        // 判断是否包含这个字符 
        System.out.println(StringUtils.contains("abc", "ba"));
        // 表示左边两个字符 
        System.out.println(StringUtils.left("abc", 2));
        //********************************DateFormatUtils***************************************
        System.out.println(DateFormatUtils.format(new Date(), "yyyy-MM-dd HH:mm:ss"));
        //直接将日期格式化为内置的固定格式
        System.out.println(DateFormatUtils.ISO_DATE_FORMAT.format(new Date()));
        //字符型日期转化为Date
        System.out.println(DateUtils.parseDate("2014-11-11 11:11:11", new String[] { "yyyy-MM-dd HH:mm:ss", "yyyy-MM-dd HH:mm", "yyyy-MM-dd", "yyyy/MM/dd" }));
        //日期舍入与截整
        System.out.println(DateUtils.truncate(new Date(), Calendar.DATE));
        //判断是否是同一天
        System.out.println(DateUtils.isSameDay(new Date(), new Date()));
        //加天数
        System.out.println(DateUtils.addDays(new Date(), 10));
    }
}
```

#### **14、commos-logging**

**提供的是一个Java 的日志接口,同时兼顾轻量级和不依赖于具体的日志实现工具。**

```
import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;

public class CommosLogging {
    private static Log log = LogFactory.getLog(CommosLogging.class);

    public static void main(String[] args) {
        log.error("ERROR");
        log.debug("DEBUG");
        log.warn("WARN");
        log.info("INFO");
        log.trace("TRACE");
        System.out.println(log.getClass());
    }
}
```

#### **15、Validator** 

**通用验证系统，该组件提供了客户端和服务器端的数据验证框架。**

**验证日期**

```
      // 获取日期验证  
      DateValidator validator = DateValidator.getInstance();  
  
      // 验证/转换日期  
      Date fooDate = validator.validate(fooString, "dd/MM/yyyy");  
      if (fooDate == null) {  
          // 错误 不是日期  
          return;  
      }  
```

**表达式验证**

```
      // 设置参数  
      boolean caseSensitive = false;  
      String regex1   = "^([A-Z]*)(?:\\-)([A-Z]*)*$"  
      String regex2   = "^([A-Z]*)$";  
      String[] regexs = new String[] {regex1, regex1};  
  
      // 创建验证  
      RegexValidator validator = new RegexValidator(regexs, caseSensitive);  
  
      // 验证返回boolean  
      boolean valid = validator.isValid("abc-def");  
  
      // 验证返回字符串  
      String result = validator.validate("abc-def");  
  
      // 验证返回数组  
      String[] groups = validator.match("abc-def");  
```



# Spring cloud

**Spring cloud是目前国内使用最广泛的微服务框架，它集成了各种微服务功能组件，并基于spring boot实现了这些组件的自动装配，从而提供良好的用户体验**

## 服务拆分原则

**什么时候拆分**

**创业项目：先采用单体架构，快速开发，快速试错，随着规模扩大，逐渐拆分**

**确定的大型项目：资金充足，目标明确，可以直接选择微服务架构，避免后续拆分的麻烦**

**高内聚：每个服务要尽量做到职责单一，包含的业务相关联高，完整度高**

**低耦合：每个微服务的功能要相对独立，尽量减少对其他服务的依赖**

**纵向拆分：按照业务模块拆分**

**横向拆分：抽取公共服务，提高复用性**

**工程结构：分为两种，一种是独立的project,一种是maven聚合**

## 远程调用

**spring给我们提供了一个RestTemplate工具，可以方便的实现http请求的发送，使用步骤如下：**

**1：注入RestTemplate到spring容器**

```java
@Configuration
public class RestTemplateConfig {

    @Bean
    public RestTemplateConfig restTemplateConfig() {
        return new RestTemplateConfig();
    }
}
```

**2：发起远程调用**

```java
//利用RestTemplate发起http请求，获取http请求
ResponseEntity<List<ItemDTO>> response = restTemplate.exchange(
        "http://localhost:8081/items?ids={ids}", //请求路径
        HttpMethod.GET, //请求方式
        null,           //请求实体
        new ParameterizedTypeReference<List<ItemDTO>>() {
        },  //返回值类型,这里因为返回值的List<ItemDTO>,所以使用这种方式传入
        Map.of("ids", CollUtil.join(itemIds, ","))         //请求参数
);
if(!response.getStatusCode().is2xxSuccessful()){
    //响应失败直接结束
    return;
}
//解析响应
List<ItemDTO> items = response.getBody();
```

## 服务治理

### 服务远程调用时存在的问题

**假如商品微服务被调用较多，为了应对更高的并发，我们进行了多实例部署，如图：**

![](assets\1733225733595.png)

**此时，每个`item-service`的实例其IP或端口不同，问题来了：**

- **item-service这么多实例，cart-service如何知道每一个实例的地址？**
- **http请求要写url地址，`cart-service`服务到底该调用哪个实例呢？**
- **如果在运行过程中，某一个`item-service`实例宕机，`cart-service`依然在调用该怎么办？**
- **如果并发太高，`item-service`临时多部署了N台实例，`cart-service`如何知道新实例的地址？**

**为了解决上述问题，就必须引入注册中心的概念了，接下来我们就一起来分析下注册中心的原理。**

### 注册中心

**在微服务远程调用的过程中，包括两个角色：**

- **服务提供者：提供接口供其它微服务访问，比如`item-service`**
- **服务消费者：调用其它微服务提供的接口，比如`cart-service`**

**在大型微服务项目中，服务提供者的数量会非常多，为了管理这些服务就引入了注册中心的概念。注册中心、服务提供者、服务消费者三者间关系如下**

![](assets\1733226355828.png)



**流程如下：**

- **服务启动时就会注册自己的服务信息（服务名、IP、端口）到注册中心**
- **调用者可以从注册中心订阅想要的服务，获取服务对应的实例列表（1个服务可能多实例部署）**
- **调用者自己对实例列表负载均衡，挑选一个实例**
- **调用者向该实例发起远程调用**

**当服务提供者的实例宕机或者启动新实例时，调用者如何得知呢？**

- **服务提供者会定期向注册中心发送请求，报告自己的健康状态（心跳请求）**
- **当注册中心长时间收不到提供者的心跳时，会认为该实例宕机，将其从服务的实例列表中剔除**
- **当服务有新实例启动时，会发送注册服务请求，其信息会被记录在注册中心的服务实例列表**
- **当注册中心服务列表变更时，会主动通知微服务，更新本地服务列表**

### Nacos

**目前开源的注册中心框架有很多，国内比较常见的有：**

- **Eureka：Netflix公司出品，目前被集成在SpringCloud当中，一般用于Java应用**
- **Nacos：Alibaba公司出品，目前被集成在SpringCloudAlibaba中，一般用于Java应用**
- **Consul：HashiCorp公司出品，目前集成在SpringCloud中，不限制微服务语言**

**我们基于Docker来部署Nacos的注册中心，首先我们要准备MySQL数据库表，用来存储Nacos的数据。由于是Docker部署，所以大家需要将资料中的SQL文件导入到你Docker中的MySQL容器中**

**找到`nacos/custom.env`文件中，有一个MYSQL_SERVICE_HOST也就是mysql地址，需要修改为你自己的虚拟机IP地址：**

![](assets\1733226946038.png)

**然后，将`nacos`目录上传至虚拟机的`/root`目录。**

**进入root目录，然后执行下面的docker命令：**

```PowerShell
docker run -d \
--name nacos \
--env-file ./nacos/custom.env \
-p 8848:8848 \
-p 9848:9848 \
-p 9849:9849 \
--restart=always \
nacos/nacos-server:v2.1.0-slim
```

### 服务注册

**1：引入nacos discovery依赖**

```XML
<!--nacos 服务注册发现-->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```

**2：配置nacos地址**

**在`item-service`的`application.yml`中添加nacos地址配置：**

```yaml
spring:
  application:
    name: item-service # 服务名称
  cloud:
    nacos:
      server-addr: 192.168.150.101:8848 # nacos地址
```

**此时就完成了服务注册**

### 服务发现

**消费者需要连接nacos以取消拉取和订阅服务，因此前两步与服务注册一致，后面加上服务调用即可**

**3：服务发现**

![](assets\1733230912421.png)

## OpenFeign

**OpenFeign是一个声明式的htpp客户端，是spring cloud在Eureka公司开源的Feign基础上改造而来，其作用就是基于spring mvc的常见注解帮我们实现http请求**

**快速入门**

**引入依赖，包括OpenFeign和负载均衡组件spring cloudLoadBalancer**

```XML
  <!--openFeign-->
  <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-openfeign</artifactId>
  </dependency>
  <!--负载均衡器-->
  <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-loadbalancer</artifactId>
  </dependency>
```

**通过@EnableFeignClients注解，启动OpenFeign服务，只需要加到SpringBoot启动类即可**

```
@MapperScan("com.hmall.cart.mapper")
@SpringBootApplication
@EnableFeignClients
public class CartApplication {
    public static void main(String[] args) {
        SpringApplication.run(CartApplication.class, args);
    }
}
```

**编写FeignClient**

```
@FeignClient("item-service")
public interface ItemClient {
    @GetMapping("/items")
    List<ItemDTO> queryItemByIds(@RequestParam("ids") Collection<Long> ids);

}
```

**调用FeignClient接口里的方法**

```java
List<ItemDTO> items = itemClient.queryItemByIds(itemIds);
```

### 连接池

**OpenFeign对http请求做了封装，不过其底层发起http请i去，依赖于其他框架，这些框架可以自己选择，包括以下三种：**

**HttpURLConnection：默认连接，不支持连接池**

**Apache HttpClient:支持连接池**

**OKHttp：支持连接池**

**为了提高性能，建议使用连接池**

**以下以OKHttp为例做演示**

**依赖引入**

```XML
<!--OK http 的依赖 -->
<dependency>
  <groupId>io.github.openfeign</groupId>
  <artifactId>feign-okhttp</artifactId>
</dependency>
```

**开启连接池功能：**

**在`cart-service`的`application.yml`配置文件中开启Feign的连接池功能：**

```YAML
feign:
  okhttp:
    enabled: true # 开启OKHttp功能
```

**重启服务，连接池就生效了。**

### 最佳实践

**如果拆分了交易微服务（`trade-service`），它也需要远程调用`item-service`中的根据id批量查询商品功能。这个需求与`cart-service`中是一样的。**

**因此，我们就需要在`trade-service`中再次定义`ItemClient`接口，这不是重复编码吗？ 有什么办法能加避免重复编码呢？**

**思路1：抽取到微服务之外的公共module**

**思路2：每个微服务自己抽取一个module**

![](assets\1733409117740.png)

**方案1抽取更加简单，工程结构也比较清晰，但缺点是整个项目耦合度偏高。**

**方案2抽取相对麻烦，工程结构相对更复杂，但服务之间耦合度降低。**

**以下我们采用方案1进行拆分**

**在拆分后会存在无法为ItemClient创建bean的问题，这是因为扫描包的问题导致的，有以下两种解决方案可以解决问题**

```
@EnableFeignClients(basePackages = "com.hmall.api.client")
```

```
@EnableFeignClients(clients = {ItemClient.class})
```

### 日志输出

**OpenFeign只会在FeignClient所在包的日志级别为DEBUG时，才会输出日志。而且其日志级别有4级：**

- **NONE：不记录任何日志信息，这是默认值。**
- **BASIC：仅记录请求的方法，URL以及响应状态码和执行时间**
- **HEADERS：在BASIC的基础上，额外记录了请求和响应的头信息**
- **FULL：记录所有请求和响应的明细，包括头信息、请求体、元数据。**

**Feign默认的日志级别就是NONE，所以默认我们看不到请求日志。**

**新建一个配置类，定义Feign的日志级别：**

```java
import org.springframework.context.annotation.Bean;
import feign.Logger;
public class DefaultFeignConfig {
    @Bean
    public Logger.Level feignLogLevel(){
        return Logger.Level.FULL;
    }
}
```

**接下来，要让日志级别生效，还需要配置这个类。有两种方式：**

- **局部生效：在某个`FeignClient`中配置，只对当前`FeignClient`生效**

```Java
@FeignClient(value = "item-service", configuration = DefaultFeignConfig.class)
```

- **全局生效：在`@EnableFeignClients`中配置，针对所有`FeignClient`生效。**

```Java
@EnableFeignClients(defaultConfiguration = DefaultFeignConfig.class)
```



# Mybatis	

## 入门

**在resources下的application.properties文件配置数据库相关信息**

**在mapper文件包下创建与数据库交互的mapper接口，并在上面加上@Mapper注解，在运行时，会自动生成该接口的实现类对象，并交给IOC管理，然后在承接结果的容器上加上对应的操作注解，比如执行查询操作，就加上@Select(),括号里面填对应的语句**

```

@Mapper
public interface UserMapper {
    //查询全部用户信息
    @Select("select * from user")
    public List<User> list();
}
```

**然后在测试类中运行即可，这里UserMapper已经创建对应的实体类，并且交给IOC管理，因此通过依赖注入便可以获得该对象**

```
@SpringBootTest
class MybatieDemoApplicationTests {

    @Autowired
    private UserMapper userMapper;
    @Test
    public void testListUser() {
        List<User> userlist=userMapper.list();
        userlist.stream().forEach(user -> {
            System.out.println(user);
        });
    }

}
```

## JDBC

**概念：Java语言操作关系型数据库的一套api**

## 数据库连接池

**数据库连接池是个容器，负责分配，管理数据库连接，允许应用重复使用一个现有的数据库连接，而不是在重新建立一个，通过释放空闲时间超过最大空闲时间的连接，来避免因为没有释放连接而引起的数据库连接遗漏** 

**druid连接池的依赖**

```
<dependency>
   <groupId>com.alibaba</groupId>
   <artifactId>druid-spring-boot-starter</artifactId>
   <version>1.2.8</version>
</dependency>
```



## Mybatis基础操作

### 删除

```
public interface EmpMapper {
    //根据id删除员工
    @Delete("DELETE FROM emp where id = #{id}")
    public void delete(Integer id);
}
```

**对应接口里的方法上加上注解@Delete,注意这里的id需要动态获取，可以使用#{}的方式获取，通过这个方式获取，使用的就是预编译的sql语句，还可以使用${},但这种方式是直接将参数拼接到sql语句中，存在sql注入的问题，并且这个方法是有返回值的，返回的是操作影响的操作数，需要获取返回值，只需要把返回值改成int**

**预编译sql语句的优点：性能更高，更安全（防止sql注入）**

**sql注入：通过操作输入的数据来修改事先定义好的sql语句，以达到执行代码对服务器进行攻击的方法**

### 新增

```
@Mapper
public interface EmpMapper {

    //新增员工
    @Insert("insert into emp(username, name, gender, image, job, entrydate, dept_id, create_time, update_time)"+
            "VALUE (#{username},#{name},#{gender},#{image},#{job},#{entryDate},#{deptId},#{createTime},#{updateTime}")
    public void insert(Emp emp);

}
```

**这里可以直接传入一个对象，上面#{}里面就可以填对应的对象属性**

**主键返回，默认条件下，基础的插入操作是不会返回主键值的，需要通过如下方式进行获取**

```
@Mapper
public interface EmpMapper {

    //新增员工
    @Options(keyProperty = "id",useGeneratedKeys = true)
    @Insert("insert into emp(username, name, gender, image, job, entrydate, dept_id, create_time, update_time)"+
            "VALUE (#{username},#{name},#{gender},#{image},#{job},#{entryDate},#{deptId},#{createTime},#{updateTime}")
    public void insert(Emp emp);

}
```

### 更新

```
@Mapper
public interface EmpMapper {
    @Update("update emp set username = #{username}, name = #{name},gender = #{gender},image = #{image}," +
            "job = #{job},entrydate = #{entryDate},dept_id = #{deptId},update_time = #{updateTime} where id = #{id}")
    public void update(Emp emp);

}
```

**可以将待更新的数据存储到一个对象中来进行操作**

### 查询

```
@Mapper
public interface EmpMapper {
    @Select("select * from emp where id = #{id}")
    public Emp getById(Integer id);

}
```

**实体类属性名和数据库表查询返回的字段名一样，mybatis会自动封装，不一样则不会封装**

**解决方案如下**

**一：添加别名**

```
@Mapper
public interface EmpMapper {
    @Select("select id, username, password, name, gender, image, job, entrydate entryDate," +
            "dept_id deptId, create_time createTime, update_time updateTime from emp where id = #{id}")
    public Emp getById(Integer id);

}
```

**二：通过@Results和@Result注解来实现映射**

```
@Mapper
public interface EmpMapper {
    @Select("select * from emp where id = #{id}")
    @Results({
            @Result(column = "entrydate", property = "entryDate"),
            @Result(column = "create_time", property = "createTime"),
            @Result(column = "dept_id", property = "deptId"),
            @Result(column = "update_time", property = "updateTime")
    })
    public Emp getById(Integer id);

}
```

**三：开启mybatis的驼峰命名转化开关，打开后会自动将待下划线的名字映射到对应的类属性，a_colume---aColumn**

```
mybatis.configuration.map-underscore-to-camel-case=true
```

**在进行模糊匹配时可能会出现如下情况**

```
@Select("select * from emp where name like '%${name}%' and gender = #{gender} and " +
            "entrydate between #{begin} and #{end} " +
            "order by update_time desc")
```

**此时不能使用#{}，要使用${},因为只有${}有字符串拼接的效果，但这样会有sql注入的问题，于是有了如下解决方案**

```
 @Select("select * from emp where name like concat('%',#{name},'%') and gender = #{gender} and " +
            "entrydate between #{begin} and #{end} " +
            "order by update_time desc")
```

**使用cancat函数进行字符串拼接即可**

### xml映射文件

**xml映射文件的名称与mapper接口名称一致，并且将xml映射文件和mapper接口放置在相同包下，一般配置文件都放在resourecs文件夹下，所以可以在该文件夹下创建一个相同的包来存储相关文件**

**xml映射文件的namespace属性为mapper接口全限定名一致，如：com.example.mapper.EmpMapper**

**xml映射文件中sql语句的id与mapper接口中的方法名一致，并保持返回类型一致**

**以下是配置文件的基本框架**

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper>

    
</mapper>
```

**下面是一个配置样例**

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.example.mapper.EmpMapper">
    <select id="get" resultType="com.example.pojo.Emp">
        select * from emp where name like concat('%',#{name},'%') and gender = #{gender} and
            entrydate between #{begin} and #{end} order by update_time desc
    </select>

</mapper>
```

```

@Mapper
public interface EmpMapper {

    public List<Emp> get(String name, Short gender, LocalDate begin, LocalDate end);

}
```

### 动态sql

**随着用户的输入或外部条件的变化而变化的sql语句**

`<if>`:**用于判定条件是否成立，使用test属性t进行条件语句的判断，其中多个条件之间用and连接**

```
<if test="begin!=null and end!=null">and entrydate between #{begin} and #{end}</if>
```

`<where>`:**只会在子元素有内容的情况下才会插入where语句，并且自动去除字句开头的and or**

```
<where>
	<if test="name!=null">name like concat('%', #{name}, '%')</if>

	<if test="gender!=null">and gender = #{gender}</if>

	<if test="begin!=null and end!=null">and entrydate between #{begin} and #{end}</if>
</where>

```

`<set>`：**动态的在行首添加set关键字，并删掉额外的逗号**

```
<update id="update">
        update emp
        <set>
            <if test = "username != null">username = #{username},</if>
            <if test = "name != null">name = #{name},</if>
            <if test = "gender != null">gender = #{gender},</if>
            <if test = "image != null">image = #{image},</if>
            <if test = "job != null">job = #{job},</if>
            <if test = "entrydate != null">entrydate = #{entrydate},</if>
            <if test = "deptId != null">dept_id = #{deptId},</if>
            <if test = "updateTime != null">update_time = #{updateTime},</if>
        </set>
        where id = #{id}
    </update>
```

`<foreach>`**循环遍历的拼接sql语句**

**collection:遍历的集合的变量名**

**item:集合遍历出来的元素**

**seperator:每一次遍历使用的分隔符**

**open：遍历开始拼接的片段**

**close：遍历结束后拼接的片段**

```
<delete id="delete">
        delete from emp where id in
        <foreach collection = "ids" item = "id" separator = "," open = "(" close = ")">
            #{id}


        </foreach>
</delete>
```

`<sql>`:**用于封装sql语句片段，id属性用于给这个片段加上唯一标识**

`<include>:`**用于引用封装的sql片段，refid属性用于填写引用片段的唯一id**

```
<sql id="commonSelect">
	select id, username, id, username, password, name, gender, image,
		job, entrydate, dept_id, create_time, update_time
		from emp
</sql>
<select id="get" resultType="com.example.pojo.Emp">
	<include refid="commonSelect"/>
	<where>
		<if test="name!=null">name like concat('%', #{name}, '%')</if>

		<if test="gender!=null">and gender = #{gender}</if>

		<if test="begin!=null and end!=null">and entrydate between #{begin} and #{end}</if>
	</where>


	order by update_time desc
</select>
```

**insert标签下的属性**

| 名称             | 解释                     | 取值         |
| ---------------- | ------------------------ | ------------ |
| useGeneratedKeys | 需要获取自动生成的主键值 | true/false   |
| keyProperty      | 将主键值返回给对象的Id   | 对象中的属性 |

**案例**

```sql
<insert id="insert" useGeneratedKeys="true" keyProperty="id">
    insert into dish (name, category_id, price,
        image, description, status, create_time, update_time,
        create_user, update_user) values (#{name}, #{categoryId},
        #{price}, #{image}, #{description}, #{status}, #{creatTime},
        #{updateTime}, #{creatUser}, #{updateUser})
</insert>
```



# Mybatis plus

**个人不推荐使用，原生的Mybatis就已经很好了**

## 入门案例

**依赖引入**

**MybatisPlus官方提供了starter,其中集成了Mybatis和MybatisPlus，并且实现了自动装配的效果，因此我们可以用Mybatis plus的依赖代替Mybatis的依赖**

```
<dependency>
	<groupId>com.baomidou</groupId>
	<artifactId>mybatis-plus-boot-starter</artifacted>
	<version>3.5.3.1</version>
</dependency>
```

**让自定义mapper继承MybatisPlus提供的BaseMapper接口**

**注意这里的泛型一定是你实体类的类型**

```
public interface UserMapper extends BaseMapper<User>{
}
```

**使用事项：**

**1：类名转下划线作为表名**

**2：名为id的字段作为主键**

**3：变量名驼峰转下划线作为表的字段名**

## 常用注解

**当类不满足上述约定俗成时，需要用注解进行配置**

**@TableName:用来指定表名**

**@TableId:用来指定表中的主键字段信息**

**@TableField:用来指定表中的普通字段信息**

**其中@TableId有两个属性，value用于指定对应的表中的字段名，type用于指定id的类型，例如IdType.AUTO就是自增,IdType.INPUT通过set方法自行输入，IdType.ASSIGN_ID,分配ID,接口的identifierGnerator的nextId方法来生成的，默认实现类为DefaultIdtifierGenertor雪花算法,其中最后一个属性是默认属性**

**关于@TableField的使用场景，当成员变量名与数据库的字段名不一致的时候可以使用，还有就是成员变量以is开头，且是布尔值时，还有就是成员变量与数据库关键字冲突时需要用到，用法：**

```
@TableField("`orders`")
```

**成员变量不是数据库字段，也需要使用本注解来说明该变量不是数据库中的字段，用法如下**

```
@TabelField(exist = false)
```

**以下是注解的使用demo**

```java
package com.itheima.mp.domain.po;

import com.baomidou.mybatisplus.annotation.IdType;
import com.baomidou.mybatisplus.annotation.TableField;
import com.baomidou.mybatisplus.annotation.TableId;
import com.baomidou.mybatisplus.annotation.TableName;
import lombok.Data;

import java.time.LocalDateTime;

@Data
@TableName("user")
public class User {

    /**
     * 用户id
     */
    @TableId(value = "id", type = IdType.AUTO)
    private Long id;

    /**
     * 用户名
     */
    @TableField("username")
    private String username;

    /**
     * 密码
     */
    private String password;

    /**
     * 注册手机号
     */
    private String phone;

    /**
     * 详细信息
     */
    private String info;

    /**
     * 使用状态（1正常 2冻结）
     */
    private Integer status;

    /**
     * 账户余额
     */
    private Integer balance;

    /**
     * 创建时间
     */
    private LocalDateTime createTime;

    /**
     * 更新时间
     */
    private LocalDateTime updateTime;
}

```

## 常用配置

![](assets\1732005901781.png)

**注意这里的id-type是全局配置，没有注解配置的优先级高**

## 条件构造器



![](assets\1732006594619.png)

**select语句使用的demo**

```
@Test
void testSelectQueryWrapper() {
    //以下条件构造相当于select id, username, info, balance
    // from user where username like '%o%' and balance >= 1000
    QueryWrapper<User> wrapper = new QueryWrapper<User>()
            .select("id", "username", "info", "balance")
            .like("username", "o")
            .ge("balance", 1000);
    //userMapper.selectList(wrapper);
    log.info(userMapper.selectList(wrapper).toString());
}
```

**update语句使用的demo**

```
@Test
void testUpdateByQueryWrapper() {
    User user = new User();
    user.setBalance(2000);

    //update user set balance = 2000 where username = 'jack'
    QueryWrapper<User> wrapper = new QueryWrapper<User>()
            .eq("username", "jack");

    //参数1：代表要更新的数据，参数2：代表查询条件
    userMapper.update(user, wrapper);
}
```

```
@Test
void testUpdateByUpdateWrapper() {
    //update user set balance -200  where id in (1, 2, 3)
    List<Long> ids = List.of(1L, 2L, 3L);
    UpdateWrapper<User> wrapper = new UpdateWrapper<User>()
            .setSql("balance = balance - 200")
            .in("id", ids);

    userMapper.update(null, wrapper);
}
```

**select 语句使用LambdaQueryWrapper**

```
@Test
void testLambdaQueryWrapper() {
    //select id, username, info, balance
    //from user where username like '%o%' and balance >= 1000
    LambdaQueryWrapper<User> wrapper = new LambdaQueryWrapper<User>()
            .select(User::getId, User::getUsername, User::getInfo, User::getBalance)
            .like(User::getUsername, "o")
            .ge(User::getBalance, 1000);
    log.info(userMapper.selectList(wrapper).toString());
}
```

## 自定义sql

**以update user set balance -200  where id in (1, 2, 3)为例子**

**第一步：构建wrapper条件，并调用对应的mapper**

```java
@Test
void testCustomSqlUpdate() {
    //更新条件
    List<Long> ids = List.of(1L, 2L, 3L);
    int amount = 200;

    //定义条件
    QueryWrapper<User> wrapper = new QueryWrapper<User>()
            .in("id", ids);

    userMapper.updateBalanceByIds(wrapper, amount);
}
```

**第二步：在mapper方法中参数中用Param注解中申明wrapper变量名称必须是ew**

```java
public interface UserMapper extends BaseMapper<User> {


    void updateBalanceByIds(@Param("ew") QueryWrapper<User> wrapper, @Param("amount") int amount);
}
```

**第三步：自定义sql，并使用wrapper条件**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.mp.mapper.UserMapper">
    <update id="updateBalanceByIds">
        update user set balance = balance - #{amount} ${ew.customSqlSegment}
    </update>

</mapper>
```

## Service接口

**继承结构**

![](assets\1732028420493.png)

**解释：IService和ServiceImpl是Mybatis plus中已经提供好的Service接口和对应的接口实现类，而UserService和UserServiceImpl是我们自己写的Service接口和接口实现类，倘若我们要让我们的UserServiceImpl还要拥有Mybatis plus里的Service接口的功能该怎么办呢，并且在拥有这些功能的同时可以不用去实现这些方法？我们只需要让ServiceImpl去继承Mybatis plus中的ServiceImpl,这样UserServiceImpl就会拥有该类的所有功能，因为是继承的实现类，所以还不用去实现这些方法，但是我们在实际开发中使用Service时是通过依赖注入的方式使用的，也就是申明一个UserService类型的变量，将UserServiceImpl注入进入，从而进行使用，这里运用的是多态的思想，但是Mybatis plus中的Service接口所提供的方法只有UserServiceImpl获得了，UserService接口并无法访问到，也就是说现在如果你想使用Mybatis plus中的Service接口的方法，只能通过获取UserServiceimpl类型的变量的方式进行使用，而不能通过依赖注入，依靠多态的属性进行使用，这是因为UserService接口中并没有Mybatis Plus的Service接口中的方法的方法申明，因此我们需要让UserService接口去继承IService接口，从而获得这些方法的申明**

**以下是代码演示**

```java
@Service
public class UseerServiceImpl extends ServiceImpl<UserMapper, User> implements IUserService {


}
```

```java
public interface IUserService extends IService<User>{
}
```



### **使用Service接口进行insert操作还有查询操作**

```
@SpringBootTest
@Slf4j
public class IUserServiceTest {
    @Autowired
    private IUserService userService;

    @Test
    public void testSaveUser() {
        User user = new User();
        user.setUsername("Maker");
        user.setPassword("132");
        user.setPhone("18688990013");
        user.setBalance(250);
        user.setInfo("{\"age\": 24, \"intro\": \"英文老师\", \"gender\": \"female\"}");
        user.setCreateTime(LocalDateTime.now());
        user.setUpdateTime(LocalDateTime.now());

        userService.save(user);

    }


    @Test
    void testQuery() {
        List<User> users = userService.listByIds(List.of(1L, 2L, 3L));
        users.forEach(user -> log.info("用户信息:{}", user));
    }

}
```

### **lambda方法的使用**

**业务场景，假设我们需要一个这样子的sql语句**

![](assets\1732116252636.png)

**如何在不使用动态sql的情况下利用mybatis plus将这个语句实现呢**

```
@Override
public List<User> queryUser(UserQuery userQuery) {
    return lambdaQuery()
            .like(userQuery.getName() != null, User::getUsername, userQuery.getName())
            .eq(userQuery.getStatus() != null, User::getStatus, userQuery.getStatus())
            .ge(userQuery.getMinBalance() != null, User::getBalance, userQuery.getMinBalance())
            .le(userQuery.getMaxBalance() != null, User::getBalance, userQuery.getMaxBalance())
            .list();
}
```

**业务需求，在扣减余额后，如果余额为0，账户冻结**

```
@Override
@Transactional
public void deductBalance(Long id, Integer money) {
    User user = getById(id);
    if (user == null || user.getStatus() == 2) {
        throw new RuntimeException("用户状态异常！");
    }
    if (user.getBalance() < money) {
        throw new RuntimeException("用户余额不足");
    }

    int remainBalance = user.getBalance() - money;
    lambdaUpdate()
            .set(User::getBalance, remainBalance)
            .set(remainBalance == 0, User::getStatus, 2)
            .eq(User::getId, id)
            .eq(User::getBalance, user.getBalance())//乐观锁
            .update();
}
```

**IService接口批处理操作**

**正常情况下使用saveBatch方法进行批处理操作，底层实际上生成了多条sql语句，但实际上，在类似insert这类操作时，多条数据可以用一条sql语句实现，倘若要达到这个效果需要在application.yaml配置文件中加入如下配置*，其中最关键的就是rewriteBatchedStatements=true，这个属于mysql的配置**

```
spring:
  datasource:
    url: jdbc:mysql://127.0.0.1:3306/mp?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&serverTimezone=Asia/Shanghai&rewriteBatchedStatements=true
    driver-class-name: com.mysql.cj.jdbc.Driver
    username: root
    password: 1234
```

## 扩展功能

### 代码生成

**maven依赖**

```xml
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-generator</artifactId>
    <version>3.5.9</version>
</dependency>
```

**但是现在可以用idea插件MybatisPlus使用，可以直接生成基础框架代码**

### 静态工具

**使用：`Db.方法名`**

![](assets\1732198989432.png)

**代码样例**

```java
@Override
public UserVO queryUserAndAddressById(Long id) {
    User user = getById(id);
    if (user == null || user.getStatus() == 2) {
        throw new RuntimeException("用户状态异常");
    }

    List<Address> addresses = Db.lambdaQuery(Address.class)
            .eq(Address::getUserId, id)
            .list();

    UserVO userVO = new UserVO();
    BeanUtil.copyProperties(user, userVO);


    userVO.setAddresses(BeanUtil.copyToList(addresses, AddressVO.class));
    return userVO;
    
}
```

### 逻辑删除

**逻辑删除是基于代码逻辑模拟删除，但并不会真正删除数据，大致操作流程是这样的，在表中添加一个字段用于标记数据是否被删除，但删除时就把把该字段改为1，查询时只查询标记为0的数据**

**然而这样要改变原本代码的条件构造，然而Mybatis plus给我们提供了不改变原代码的基础上，实现逻辑删除的方式，只需要在Application.yaml文件加入如下配置，就可以在使用原本Mybatis plus的方法的情况下，达到逻辑删除的效果，也就是你任然可以使用delete,update等方法，并且不能加任何多余的条件，底层会自动改成逻辑删除的实现方式**

![](assets\1732201785322.png)

**逻辑删除本身也有自己的问题，比如：**

**会导致数据库表垃圾数据越来越多，影响查询效率**

**SQL中全都需要对逻辑删除字段做判断，影响查询效率**

**因此，我不太推荐采用逻辑删除功能，如果数据不能删除，可以采用把数据迁移到其它表的办法**

### 枚举处理器

**场景：比如数据库中有一个字段status表示账户状态，规范编程建议使用枚举类型，但是需要给对应的变量类型上加上@EnumValue**



![](assets\1732203014639.png)

**当然要让这个注解生效需要在application.yaml文件加入以下配置**

![](assets\1732203420333.png)



**当然通过枚举包装数据也有其他的问题，比如你向前端返回数据时，返回就不再是1或者2，而是字段名NORMAL或者FROZEN,如果我们想要返回枚举类中的某个值，只需要在这个值的申明上加上@JsonValue注解即可；**

```java
public enum UserStatus {
    NORMAL(1, "正常"),
    FROZEN(2, "冻结"),
    ;

    @EnumValue
    @JsonValue
    private final int value;
    private final String desc;

    UserStatus(int value, String desc) {
        this.value = value;
        this.desc = desc;
    }
}
```

### json处理器

**场景分析**

**在创建user表时，有一个字段信息代表用户的详细信息，这个字段的数据结构是一个json字符串，在代码用string代替，但是这样显示不太方便，如果可以使用类进行分装，就更好了，但是进行分装后的如何让mp把这个类跟字符串里的信息映射起来，成为了我们需要解决的问题**

```


@Data
@TableName(value = "user", autoResultMap = true)
public class User {

    /**
     * 用户id
     */
    @TableId(value = "id", type = IdType.AUTO)
    private Long id;

    /**
     * 用户名
     */
    @TableField("username")
    private String username;

    /**
     * 密码
     */
    private String password;

    /**
     * 注册手机号
     */
    private String phone;

    /**
     * 详细信息
     */
    @TableField(typeHandler = JacksonTypeHandler.class)
    private UserInfo info;

    /**
     * 使用状态（1正常 2冻结）
     */
    private UserStatus status;

    /**
     * 账户余额
     */
    private Integer balance;

    /**
     * 创建时间
     */
    private LocalDateTime createTime;

    /**
     * 更新时间
     */
    private LocalDateTime updateTime;
}
```

**其中最关键的两个注解。一个是@TableName(value = "user", autoResultMap = true)，一个是@TableField(typeHandler = JacksonTypeHandler.class)用于设置json数据的处理器**

## 插件功能

**Mybatis plus提供很多内置拦截提，如下**

| **序号** | **拦截器**                       | **描述**                           |
| -------- | -------------------------------- | ---------------------------------- |
| 1        | TenantLineInnerInterceptor       | 多租户插件                         |
| 2        | DynamicTableNameInnerInterceptor | 动态表名插件                       |
| 3        | PaginationInnerInterceptor       | 分页插件                           |
| 4        | OptimisticLockerInnerInterceptor | 乐观锁插件                         |
| 5        | IllegalSQLInnerInterceptor       | SQL性能规范插件，检测并拦截垃圾SQL |
| 6        | BlockAttackInnerInterceptor      | 防止全表更新和删除的插件           |

### 分页插件

**首先需要在配置类中配置对应的插件**

![](assets\1732466771120.png)

**代码样例**

```
@Test
void testPageQuery() {
    Page<User> page = Page.of(1, 2);
    //排序条件
    page.addOrder(new OrderItem("balance", true));
    page.addOrder(new OrderItem("id", true));
    Page<User> p = userService.page(page);

    //总条数
    long total = p.getTotal();
    log.info("total = " + total);

    //总页数
    long pages = p.getPages();
    log.info("pages = " + pages);

    //获取查询结果
    List<User> records = p.getRecords();
    records.forEach(user -> log.info("用户信息:{}", user));

}
```



# Redis

## 启动服务

**启动Redis服务：`redis-server.exe redis.windows.conf`**

**注意：启动服务后，命令行窗口不要关，关掉就会停止服务**

**打开Redis客户端：`redis-cli.exe`**

**完整命令：`redis-cli.exe -h ip -p port`**

**注意：这里需要另开一个窗口，补充的命令可以省略，ip位置换成目标ip,port换成目标端口**

## 常用数据类型

**Redis存储的是key-value结构的数据，其中key是字符串类型，value有中常用的数据类型，分别是字符串string，哈希hash，列表list，集合set，有序集合sorted set/zset**

![](assets\Redis.png)

**字符串(string)：普通字符串，Redis中最简单的数据类型**

**哈希(hash)：也叫散列，类似于Java中的HashMap结构**

**列表(list)：按照插入顺序排序，可以有重复元素，类似于Java中的LinkedList**

**集合(set)：无序集合，没有重复元素，类似于Java中的HashSet**

**有序集合(sorted set / zset)：集合中每个元素关联一个分数（score），根据分数升序排序，没有重复元素**

## 常用命令

### 字符串操作命令

**设置指定key的值：`SET key value`**

**删除指定key的值：`DEL key`**

**获取指定key的值：`GET key`**

**设置指定key的值，并将key的过期时间设为second秒：`SETEX key seconds value`**

**只有key不存在的时候设置key的值：`SETNX key value`**

### 哈希操作指令

**将哈希表key中的字段field的值设置为value：`HSET key field value`**

**获取存储在哈希表中指定字段的值：`HGET key field`**

**删除存储在哈希表中的指定字段：`HDEL key field`**

**获取哈希表中所有字段：`HKEYS key`**

**获取哈希表中所有值：`HVALS key`**

### 列表操作指令

**将一个或多个值插入到表头部：`LPUSH key value1 [value2]`**

**将一个或者多个值插入到表尾部：`	RPUSH key value1 [value2] [value3] ...`**

**获取列表指定范围内的元素：`LRANGE key start stop`**

**移除并获取列表内 最后一个元素：`RPOP key`**

**移除并获取列表内第一个元素：`LPOP key`**

**获取列表长度：`LLEN key`**

**获取指定下标索引的元素：`LINDEX key index`**

**在指定元素前后插入值：`LINSERT key BEFORE/AFTER value newValue`**

**注意：`LRANGE key 0 -1`可以获取整个列表的元素**

### 集合操作命令

**向集合添加一个或者多个成员：`SADD key member1 [member2]`**

**返回集合中的所有成员：`SMEMBERS key`**

**获取集合的成员数：`SCARD key`**

**返回给定所有集合的并集：`SUNION key1 [key2]`**

**返回给定所有集合的并集：`SUNION key1 [key2]`**

**删除集合中一个或多个成员：`SREM key member1 [member2]`**

### 有序集合操作命令

**向有序集合添加一个或多个成员：`ZADD key score1 member1 [score2 member2]`**

**通过索引区间返回有序集合中指定区间内的成员：`ZRANGE key start stop [WITHSCORES]`**

**有序集合中对指定成员的分数加上增量increment：`ZINCRBY key increment member`**

**移除有序集合中的一个或者多个成员：`ZREM key member [member...]`**

**注意：跟列表一样区间查找时，stop为0，stop -1则查找所有的元素**

### 通用命令

**查找所有符合给定模式（pattern）的key：`KEYS pattern`**

**检查给定key是否存在：`EXIST key`**

**返回key所存储的值的类型：`TYPE key`**

**用于在key存在时删除key：`DEL key`**

## Java中操作Redis

### 环境配置

**在maven项目中导入Spring-data-redis**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

**配置Redis数据源**

```yaml
spring:
  redis:
    host: ${sky.redis.host}
    port: ${sky.redis.port}
    database: ${sky.redis.database}
```

**编写配置类，创建RedisTemplate对象**

```java
@Slf4j
@Configuration
public class RedisConfiguration {
    @Bean
    public RedisTemplate redisTemplate(RedisConnectionFactory redisConnectionFactory) {
        log.info("开始创建Redis模板类对象....");
        RedisTemplate<Object,Object> redisTemplate = new RedisTemplate<>();
        //设置Redis的连接工厂对象
        redisTemplate.setConnectionFactory(redisConnectionFactory);

        //设置Redis key的序列化器
        redisTemplate.setKeySerializer(new StringRedisSerializer());
        //设置Redis Value的序列化器
        redisTemplate.setValueSerializer(new StringRedisSerializer());
        //设置Redis HashKey的序列化器
        redisTemplate.setHashKeySerializer(new StringRedisSerializer());
        //设置Redis HashValue的序列化器
        redisTemplate.setHashValueSerializer(new StringRedisSerializer());

        return redisTemplate;
    }
}
```

### 操作字符串类型的数据

```java
@SpringBootTest
public class SpringDataRedisTest {
    @Autowired
    private RedisTemplate redisTemplate;

    @Test
    public void testString() {
        //获取字符串操作对象
        ValueOperations valueOperations = redisTemplate.opsForValue();

        //SET key value操作
        valueOperations.set("city", "北京");
        
        //GET key操作
        String city = (String) valueOperations.get("city");
        System.out.println(city);

        //SETEX key seconds value操作
        valueOperations.set("code", 1234, 3, TimeUnit.MINUTES);

        //SETNX key value操作
        valueOperations.setIfAbsent("name", "张三");

    }
}
```

### 操作哈希类型的数据

```java
@SpringBootTest
public class SpringDataRedisTest {
    @Autowired
    private RedisTemplate redisTemplate;

    @Test
    public void testHash() {
        //获取哈希操作对象
        HashOperations hashOperations = redisTemplate.opsForHash();

        //HSET key field value操作
        hashOperations.put("100", "name", "Alice");
        hashOperations.put("100", "age", "20");

        //HGET key field操作
        String name = (String) hashOperations.get("100", "name");
        System.out.println(name);

        //HDEL key field
        hashOperations.delete("100", "age");


        //HKEYS操作
        Set keys = hashOperations.keys("100");


        //HVALS操作
        List values = hashOperations.values("100");
    }
}
```

###  操作List类型的数据

```
@SpringBootTest
public class SpringDataRedisTest {
    @Autowired
    private RedisTemplate redisTemplate;

    @Test
    public void testList() {
        //获取list操作对象
        ListOperations listOperations = redisTemplate.opsForList();

        Collection<String> collection = new ArrayList<>();
        collection.add("apple");
        collection.add("banana");

        //LPUSH key value1 [value2]
        listOperations.leftPush("myList", "d");
        listOperations.leftPushAll("myList", "a", "b", "c");
        listOperations.leftPushAll("myList1", collection);

        //RPUSH key value1 [value2]
        listOperations.rightPush("myList2", "a");
        listOperations.rightPushAll("myList2", "d", "e", "f");
        listOperations.rightPushAll("myList3", collection);


        //LPOP key
        listOperations.leftPop("myList");

        //RPOP key
        listOperations.rightPop("myList");

        //LLEN key
        Long size = listOperations.size("myList");

        //LRANGE key start stop
        List mylist = listOperations.range("myList", 0, -1);
        mylist.forEach(o -> System.out.println(o.toString()));

        //LINDEX key index
        String result = (String)listOperations.index("myList", 0);
        System.out.println(result);
        
    }
}
```

### 操作set类型的数据

```
@SpringBootTest
public class SpringDataRedisTest {
    @Autowired
    private RedisTemplate redisTemplate;

    @Test
    public void testSet() {
        //获取set操作对象
        SetOperations setOperations = redisTemplate.opsForSet();

        //SADD key member1 [member2]
        setOperations.add("set1", "A", "b", "c", "al", "bl");
        setOperations.add("set2", "d", "e", "f", "b", "c");


        //SMEMBERS key
        Set members = setOperations.members("set1");
        System.out.println(members);

        //获取set的size
        Long size = setOperations.size("set1");

        //SUNION key1 [key2]
        Set intersect = setOperations.intersect("set1", "set2");
        System.out.println(intersect);


        //SUNION key1 [key2]
        Set union = setOperations.union("set1", "set2");
        System.out.println(union);

        //SREM key member1 [member2]
        setOperations.remove("set1", "al", "bl");

    }
}
```

### 操作zset类型的数据

```
package com.sky.test;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.data.redis.core.*;

import java.util.ArrayList;
import java.util.Collection;
import java.util.List;
import java.util.Set;
import java.util.concurrent.TimeUnit;
import java.util.function.Consumer;

@SpringBootTest
public class SpringDataRedisTest {
    @Autowired
    private RedisTemplate redisTemplate;

    @Test
    public void testZset() {
        //获取zset操作对象
        ZSetOperations zSetOperations = redisTemplate.opsForZSet();

        //ZADD key score1 member1 [score2 member2]
        zSetOperations.add("zset1", "a", 10);
        zSetOperations.add("zset1", "b", 12);
        zSetOperations.add("zset1", "c", 11);

        //ZRANGE key start stop [WITHSCORES]
        zSetOperations.range("zset1", 0, -1);

        //ZINCRBY key increment member
        zSetOperations.incrementScore("zset1", "c", 10);

        //ZREM key member [member...]
        zSetOperations.remove("zset1", "a", "b");
    }

}
```

### 通用命令操作

```
package com.sky.test;

import io.lettuce.core.ScriptOutputType;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.data.redis.connection.DataType;
import org.springframework.data.redis.core.*;

import java.util.ArrayList;
import java.util.Collection;
import java.util.List;
import java.util.Set;
import java.util.concurrent.TimeUnit;
import java.util.function.Consumer;

@SpringBootTest
public class SpringDataRedisTest {
    @Autowired
    private RedisTemplate redisTemplate;

    @Test
    public void testCommon() {

        //KEYS pattern
        Set keys = redisTemplate.keys("*");
        System.out.println(keys);
        //EXIST key
        boolean name = redisTemplate.hasKey("name");
        boolean set1 = redisTemplate.hasKey("set1");
        System.out.println(name);
        System.out.println(set1);

        //TYPE key
        for (Object key : keys) {
            DataType type = redisTemplate.type(key);
            System.out.println(type.name());
        }

        //DEL key
        redisTemplate.delete("zset1");
    }

}
```





# Maven

## 依赖相关

**在pom.xml文件中添加依赖**

```
<dependencies>
	<dependency>
	<groupId>ch.qos.logback</groupId>
	<artifactId>logback-classic</artifactId>
	<version>1.2.3</version>
	</dependency>
</dependencies>
```

**需注意：依赖具有传递性，如果你不需要某些依赖，可以使用排除依赖,通过以下方式便可以把A项目所依赖的项目B的某个依赖排除**

```
    <dependencies>
        <dependency>
            <groupId>com.itheima</groupId>
            <artifactId>Project-B</artifactId>
            <version>1.2.3</version>
            <!--排除依赖-->
            <exclusions>
                <exclusion>
                    <groupId></groupId>
                    <artifactId></artifactId>
                </exclusion>
            </exclusions>
        </dependency>
    </dependencies>
```

**依赖范围：可以通过<scope></scope>标签进行限制**

| scope值       | 主程序 | 测试程序 | 打包 | 范例         |
| ------------- | ------ | -------- | ---- | ------------ |
| complie(默认) | Y      | Y        | Y    | log4j        |
| test          |        | Y        |      | junit        |
| provided      | Y      | Y        |      | servelet-api |
| runtime       |        | Y        | Y    | jdbc驱动     |

## 继承

**概念：继承描述的是两个工程间的关系，与java中的继承相似，子工程可以继承父工程中的配置信息，常见于依赖关系的继承。**

**作用：简化依赖配置、统一管理依赖**

**实现：<parent> … </parent>**

**jar：普通模块打包，springboot项目基本都是jar包（内嵌tomcat运行）**

**war：普通web程序打包，需要部署在外部的tomcat服务器中运行**

**pom：父工程或聚合工程，该模块不写代码，仅进行依赖管理**



**创建maven模块 tlias-parent ，该工程为父工程，设置打包方式pom(默认jar)。**

```
<packaging>pom</packaging>
```

**在子工程的pom.xml文件中，配置继承关系。**

```
<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>3.3.2</version>
	<relativePath/> <!-- lookup parent from repository -->
</parent>
```

 **relativePath指定父工程的pom文件的相对位置（如果不指定，将从本地仓库/远程仓库查找该工程）。**

**在父工程中配置各个工程共有的依赖（子工程会自动继承父工程的依赖）**

**若父子工程都配置了同一个依赖的不同版本，以子工程的为准**

**需注意：每个工程只能继承一个父工程**

## 版本锁定

**在maven中，可以在父工程的pom文件中通过 <dependencyManagement> 来统一管理依赖版本。**

```
<dependencyManagement>
	<dependencies>        
	<!--JWT令牌-->        
		<dependency>           
			<groupId>io.jsonwebtoken</groupId>          
			<artifactId>jjwt</artifactId>          
			<version>0.9.1</version>      
		</dependency>
	</dependencies>
</dependencyManagement>

```

**子工程引入依赖时，无需指定 <version> 版本号，父工程统一管理。变更依赖版本，只需在父工程中统一变更。**

**自定义属性/引用属性**

```
<properties>
	<lombok.version>1.18.24</lombok.version>
	<jjwt.version>0.9.0</jjwt.version>
</properties>

```

```
<dependencies>
   <dependency>
     <groupId>org.projectlombok</groupId>
     <artifactId>lombok</artifactId>
     <version>${lombok.version}</version>
   </dependency>
 </dependencies>
```

**版本锁定优先级**

**显式声明优先**：在 `pom.xml` 中显式声明的依赖版本优先级最高。如果在你的 `pom.xml` 文件中明确指定了某个依赖的版本号，Maven 将优先使用这个版本。

**依赖管理优先**：`dependencyManagement` 部分中的版本声明优先于传递依赖。如果你在 `pom.xml` 文件的 `dependencyManagement` 部分中声明了某个依赖的版本，这个版本会应用于子模块或直接依赖，而不是传递依赖中提到的版本。

**最短路径优先**：在传递依赖中，Maven 会选择路径最短的版本。如果多个传递依赖之间存在版本冲突，Maven 会选择从根项目到依赖之间路径最短的那个版本。

**声明顺序优先**：如果两个依赖在同一级别上声明并且版本冲突，Maven 会优先选择在 `pom.xml` 文件中先声明的那个版本。

**最近定义优先**：在多模块项目中，如果某个模块对依赖的版本有不同定义，Maven 会优先选择最后定义的版本。这通常发生在多层次继承的情况下。

**综上所述，版本锁定遵循就近原则**

## 聚合

**正常情况下，在多模块开发中，要打包一个项目，首先要把这个项目依赖的模块安装，最后才能对项目主体进行打包**

**聚合：将多个模块组成一个整体，同时进行项目的构建**

**聚合工程：一个不具有业务功能的“空”工程**

**maven中可以通过 <modules> 设置当前聚合工程所包含的子模块名称**

```
<modules>
   <module>../tlias-pojo</module>
   <module>../tlias-utils</module>
   <module>../tlias-web-management</module>
 </modules>
```

**聚合工程中所包含的模块，在构建时，会自动根据模块间的依赖关系设置构建顺序，与聚合工程中模块的配置书写位置无关。**

## 继承与聚合的对比

**作用**

​	**聚合用于快速构建项目**

​	**继承用于简化依赖配置、统一管理依赖**

**相同点：**

​	**聚合与继承的pom.xml文件打包方式均为pom，可以将两种关系制作到同一个pom文件中**

​	**聚合与继承均属于设计型模块，并无实际的模块内容**

**不同点：**

​	**聚合是在聚合工程中配置关系，聚合可以感知到参与聚合的模块有哪些**

​	**继承是在子模块中配置关系，父模块无法感知哪些子模块继承了自己**

## 私服

**私服是一种特殊的远程仓库，它是架设在局域网内的仓库服务，用来代理位于外部的中央仓库，用于解决团队内部的资源共享与资源同步问题。**

**依赖查找顺序：本地仓库-->私服-->中央仓库** 

**项目版本：**

​	**RELEASE（发行版本）：功能趋于稳定、当前更新停止，可以用于发行的版本，存储在私服中的RELEASE仓库中。**

​	**SNAPSHOT（快照版本）：功能不稳定、尚处于开发中的版本，即快照版本，存储在私服的SNAPSHOT仓库中。**

**设置私服的访问用户名/密码（settings.xml中的servers中配置）**

```
<server>     
	<id>maven-releases</id>    
	<username>admin</username>    
	<password>admin</password> 
</server> 

<server>    
	<id>maven-snapshots</id>   
	<username>admin</username>   
	<password>admin</password> 
</server>
```

**IDEA的maven工程的pom文件中配置上传（发布）地址**

```xml
<distributionManagement>
	<repository>         
		<id>maven-releases</id>        
		<url>http://192.168.150.101:8081/repository/maven-releases/</url>    
	</repository>     
	<snapshotRepository>         
		<id>maven-snapshots</id>        
		<url>http://192.168.150.101:8081/repository/maven-snapshots/</url>   
	</snapshotRepository> 
</distributionManagement>

```

**设置私服依赖下载的仓库组地址（settings.xml中的mirrors、profiles中配置）**

```xml
<mirror>
   <id>maven-public</id>
   <mirrorOf>*</mirrorOf>
   <url>http://192.168.150.101:8081/repository/maven-public/</url>
</mirror>
```

**需要在 profiles 中，增加如下配置，来指定snapshot快照版本的依赖，依然允许使用**

```xml
<profile>
    <id>allow-snapshots</id>
        <activation>
         <activeByDefault>true</activeByDefault>
        </activation>
    <repositories>
        <repository>
            <id>maven-public</id>
            <url>http://192.168.150.101:8081/repository/maven-public/</url>
            <releases>
             <enabled>true</enabled>
            </releases>
            <snapshots>
             <enabled>true</enabled>
            </snapshots>
        </repository>
    </repositories>
</profile>
```



如果需要上传自己的项目到私服上，需要在项目的pom.xml文件中，增加如下配置，来配置项目发布的地址(也就是私服的地址)

```xml
<distributionManagement>
    <!-- release版本的发布地址 -->
    <repository>
        <id>maven-releases</id>
        <url>http://192.168.150.101:8081/repository/maven-releases/</url>
    </repository>
    
    <!-- snapshot版本的发布地址 -->
    <snapshotRepository>
        <id>maven-snapshots</id>
        <url>http://192.168.150.101:8081/repository/maven-snapshots/</url>
    </snapshotRepository>
</distributionManagement>
```







# Git

## 常用操作

**定义：分布式版本控制系统**

**工作流程：工作区--->提交代码至暂存区--->本地库（历史版本）--->远程库**

**常用命令**

| 命令名称                             | 作用                              |
| ------------------------------------ | --------------------------------- |
| git config --global user.name 用户名 | 设置用户签名                      |
| git config --global user.email 邮箱  | 设置用户签名                      |
| git init                             | 初始化本地库                      |
| git status                           | 查看本地库状态                    |
| git add 文件名                       | 添加到暂存区                      |
| git commit -m "日志信息" 文件名      | 提交到本地库                      |
| git reflog                           | 查看历史记录,可以查看提交过的版本 |
| git reset --hard 版本号              | 版本                              |

## 分支

**定义：在版本控制过程中，同时推进多个任务，为每个任务，我们就可以创建每个任务的单独分支，使用分支也就意味着程序员可以把自己的工作从开发主线上分离开来，开发自己分支的时候，不会影响主线分支的运行**

**常用命令**

| 命令名称            | 作用                                                        |
| ------------------- | ----------------------------------------------------------- |
| git branch 分支名   | 创建分支,创建分支后会把原分支上的内容复制一份提交到新分支上 |
| git branch -v       | 查看分支                                                    |
| git checkout 分支名 | 切换分支                                                    |
| git merge 分支名    | 把指定的分支合并到当前分支上                                |

![](D:\StudyNote\assets\08f2e6f2dcd2a9cf36a4a21b07b9a3a5.png)

**上述情况就会出现合并冲突的问题**

**遇到合并冲突时的代码提交步骤：**

**1：人为修改合并代码**

**2：添加到暂存区 `git add  文件名`**

**3：执行提交，此时提交不要带文件名，`git commit -m "日志信息"`**

## 远程仓库操作

| 命令                               | 说明                                                     |
| ---------------------------------- | -------------------------------------------------------- |
| git remote -v                      | 查看当前所有远程地址别名                                 |
| git remote add 别名 远程地址       | 起别名                                                   |
| git push 别名 分支                 | 推送本地分支上的内容到远程仓库                           |
| git clone 远程地址                 | 将远程仓库的内容克隆到本地                               |
| git pull 远程库地址别名 远程分支名 | 将远程仓库对于分支最新内容拉下来后与当前本地分支直接合并 |

# Docker

## 基本概念

**快速构建，运行，管理应用的工具**

**镜像和容器**

**当我们利用Docker安装应用时，Docker自动搜索并下载应用镜像，镜像不仅包含应用本身，还包含应用运行所需要的环境，配置，系统函数库，Docker会在运行镜像时创建一个隔离环境，称为容器**

## 部署Mysql

```
docker run -d \
  --name mysql \
  -p 3306:3306 \
  -e TZ=Asia/Shanghai \
  -e MYSQL_ROOT_PASSWORD=123 \
  mysql
```

**命令解读**

- **`docker run -d` ：创建并运行一个容器，`-d`则是让容器以后台进程运行**
- **`--name`` mysql ` : 给容器起个名字叫`mysql`，你可以叫别的**
- **`-p 3306:3306` : 设置端口映射。**
  - **容器是隔离环境，外界不可访问。但是可以将宿主机端口映射容器内到端口，当访问宿主机指定端口时，就是在访问容器内的端口了。**
  - **容器内端口往往是由容器内的进程决定，例如MySQL进程默认端口是3306，因此容器内端口一定是3306；而宿主机端口则可以任意指定，一般与容器内保持一致。**
  - **格式： `-p 宿主机端口:容器内端口`，示例中就是将宿主机的3306映射到容器内的3306端口**
- **`-``e`` TZ=Asia/Shanghai` : 配置容器内进程运行时的一些参数**
  - **格式：`-e KEY=VALUE`，KEY和VALUE都由容器内进程决定**
  - **案例中，`TZ``=Asia/Shanghai`是设置时区；`MYSQL_ROOT_PASSWORD=123`是设置MySQL默认密码**
- **`mysql` : 设置镜像名称，Docker会根据这个名字搜索并下载镜像**
  - **格式：`REPOSITORY:TAG`，例如`mysql:8.0`，其中`REPOSITORY`可以理解为镜像名，`TAG`是版本号**
  - **在未指定`TAG`的情况下，默认是最新版本，也就是`mysql:latest`**

## 常见命令

![](assets\1732636643669.png)

| **命令**       | **说明**                       | **文档地址**                                                 |
| :------------- | :----------------------------- | :----------------------------------------------------------- |
| docker pull    | 拉取镜像                       | [docker pull](https://docs.docker.com/engine/reference/commandline/pull/) |
| docker push    | 推送镜像到DockerRegistry       | [docker push](https://docs.docker.com/engine/reference/commandline/push/) |
| docker images  | 查看本地镜像                   | [docker images](https://docs.docker.com/engine/reference/commandline/images/) |
| docker rmi     | 删除本地镜像                   | [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/) |
| docker run     | 创建并运行容器（不能重复创建） | [docker run](https://docs.docker.com/engine/reference/commandline/run/) |
| docker stop    | 停止指定容器                   | [docker stop](https://docs.docker.com/engine/reference/commandline/stop/) |
| docker start   | 启动指定容器                   | [docker start](https://docs.docker.com/engine/reference/commandline/start/) |
| docker restart | 重新启动容器                   | [docker restart](https://docs.docker.com/engine/reference/commandline/restart/) |
| docker rm      | 删除指定容器                   | [docs.docker.com](https://docs.docker.com/engine/reference/commandline/rm/) |
| docker ps      | 查看容器                       | [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) |
| docker logs    | 查看容器运行日志               | [docker logs](https://docs.docker.com/engine/reference/commandline/logs/) |
| docker exec    | 进入容器                       | [docker exec](https://docs.docker.com/engine/reference/commandline/exec/) |
| docker save    | 保存镜像到本地压缩文件         | [docker save](https://docs.docker.com/engine/reference/commandline/save/) |
| docker load    | 加载本地压缩文件到镜像         | [docker load](https://docs.docker.com/engine/reference/commandline/load/) |
| docker inspect | 查看容器详细信息               | [docker inspect](https://docs.docker.com/engine/reference/commandline/inspect/) |

**补充：**

**默认情况下，每次重启虚拟机我们都需要手动启动Docker和Docker中的容器。通过命令可以实现开机自启：**

```PowerShell
# Docker开机自启
systemctl enable docker

# Docker容器开机自启
docker update --restart=always [容器名/容器id]
```

**样例展示，以nginx为例**

```PowerShell
# 第1步，去DockerHub查看nginx镜像仓库及相关信息

# 第2步，拉取Nginx镜像
docker pull nginx

# 第3步，查看镜像
docker images
# 结果如下：
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
nginx        latest    605c77e624dd   16 months ago   141MB
mysql        latest    3218b38490ce   17 months ago   516MB

# 第4步，创建并允许Nginx容器
docker run -d --name nginx -p 80:80 nginx

# 第5步，查看运行中容器
docker ps
# 也可以加格式化方式访问，格式会更加清爽
docker ps --format "table {{.ID}}\t{{.Image}}\t{{.Ports}}\t{{.Status}}\t{{.Names}}"

# 第6步，访问网页，地址：http://虚拟机地址

# 第7步，停止容器
docker stop nginx

# 第8步，查看所有容器
docker ps -a --format "table {{.ID}}\t{{.Image}}\t{{.Ports}}\t{{.Status}}\t{{.Names}}"

# 第9步，再次启动nginx容器
docker start nginx

# 第10步，再次查看容器
docker ps --format "table {{.ID}}\t{{.Image}}\t{{.Ports}}\t{{.Status}}\t{{.Names}}"

# 第11步，查看容器详细信息
docker inspect nginx

# 第12步，进入容器,查看容器内目录
docker exec -it nginx bash
# 或者，可以进入MySQL
docker exec -it mysql mysql -uroot -p

# 第13步，删除容器
docker rm nginx
# 发现无法删除，因为容器运行中，强制删除容器
docker rm -f nginx
```

## 命令别名

**给常用Docker命令起别名，方便我们访问：**

```PowerShell
# 修改/root/.bashrc文件
vi /root/.bashrc
内容如下：
# .bashrc

# User specific aliases and functions

alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
alias dps='docker ps --format "table {{.ID}}\t{{.Image}}\t{{.Ports}}\t{{.Status}}\t{{.Names}}"'
alias dis='docker images'

# Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi
```

**然后，执行命令使别名生效**

```PowerShell
source /root/.bashrc
```

## 数据卷挂载

**数据卷（Volumes）：是一个虚拟目录，是容器内目录与宿主机目录之间的映射桥梁**

**以Nginx为例，我们知道Nginx中有两个关键的目录：**

- **`html`：放置一些静态资源**
- **`conf`：放置配置文件**

**如果我们要让Nginx代理我们的静态资源，最好是放到`html`目录；如果我们要修改Nginx的配置，最好是找到`conf`下的`nginx.conf`文件。**

**但遗憾的是，容器运行的Nginx所有的文件都在容器内部。所以我们必须利用数据卷将两个目录与宿主机目录关联，方便我们操作。如图：**

![](assets\1732882026490.png)

**在上图中：**

- **我们创建了两个数据卷：`conf`、`html`**
- **Nginx容器内部的`conf`目录和`html`目录分别与两个数据卷关联。**
- **而数据卷conf和html分别指向了宿主机的`/var/lib/docker/volumes/conf/_data`目录和`/var/lib/docker/volumes/html/_data`目录**

**这样以来，容器内的`conf`和`html`目录就 与宿主机的`conf`和`html`目录关联起来，我们称为挂载。此时，我们操作宿主机的`/var/lib/docker/volumes/html/_data`就是在操作容器内的`/usr/share/nginx/html/_data`目录。只要我们将静态资源放入宿主机对应目录，就可以被Nginx代理了。**

** **

| **命令**              | **说明**             | **文档地址**                                                 |
| :-------------------- | :------------------- | :----------------------------------------------------------- |
| docker volume create  | 创建数据卷           | [docker volume create](https://docs.docker.com/engine/reference/commandline/volume_create/) |
| docker volume ls      | 查看所有数据卷       | [docs.docker.com](https://docs.docker.com/engine/reference/commandline/volume_ls/) |
| docker volume rm      | 删除指定数据卷       | [docs.docker.com](https://docs.docker.com/engine/reference/commandline/volume_prune/) |
| docker volume inspect | 查看某个数据卷的详情 | [docs.docker.com](https://docs.docker.com/engine/reference/commandline/volume_inspect/) |
| docker volume prune   | 清除数据卷           | [docker volume prune](https://docs.docker.com/engine/reference/commandline/volume_prune/) |

**注意：**

**当执行docker run命令时，使用-v 数据卷:容器内目录，可以完成数据卷挂载，当创建容器时，如果挂载了数据卷且数据卷不存在，会自动创建数据卷**

## 挂载本地目录或文件

**可以发现，数据卷的目录结构较深，如果我们去操作数据卷目录会不太方便。在很多情况下，我们会直接将容器目录与宿主机指定目录挂载。挂载语法与数据卷类似：**

```Bash
# 挂载本地目录
-v 本地目录:容器内目录
# 挂载本地文件
-v 本地文件:容器内文件
```

**本地目录或文件必须以 `/` 或 `./`开头，如果直接以名字开头，会被识别为数据卷名而非本地目录名。**

 

```
docker run -d \  
	--name mysql \  
	-p 3306:3306 \  
	-e TZ=Asia/Shanghai \  
	-e MYSQL_ROOT_PASSWORD=123 \  
	-v ./mysql/data:/var/lib/mysql \  
	-v ./mysql/conf:/etc/mysql/conf.d \  
	-v ./mysql/init:/docker-entrypoint-initdb.d \  
	mysql
```

## 自定义镜像

**镜像就是包含了应用程序，程序运行的系统函数库，运行配置等文件的文件包，构建镜像的过程就是把上述文件打包的过程**

**镜像结构**

**入口：镜像运行入口，一般是程序启动的额脚本和参数**

**层：添加安装包，依赖，配置等，每次操作都形成新的一层**

**基础镜像：应用依赖的系统函数库，环境，配置等文件**

![](assets\1732889533805.png)

## **DockerFile**

**DockerFile是一个文本文件，其中包含一个个指令，用指令来说明要执行什么操作来构建镜像，将来docker可以根据DockerFile来帮我们构建镜像，常见指令如下**

| **指令**       | **说明**                                     | **示例**                     |
| :------------- | :------------------------------------------- | :--------------------------- |
| **FROM**       | 指定基础镜像                                 | `FROM centos:6`              |
| **ENV**        | 设置环境变量，可在后面指令使用               | `ENV key value`              |
| **COPY**       | 拷贝本地文件到镜像的指定目录                 | `COPY ./xx.jar /tmp/app.jar` |
| **RUN**        | 执行Linux的shell命令，一般是安装过程的命令   | `RUN yum install gcc`        |
| **EXPOSE**     | 指定容器运行时监听的端口，是给镜像使用者看的 | EXPOSE 8080                  |
| **ENTRYPOINT** | 镜像中应用的启动命令，容器运行时调用         | ENTRYPOINT java -jar xx.jar  |

**例如，要基于Ubuntu镜像来构建一个Java应用，其Dockerfile内容如下：**

```Dockerfile
# 指定基础镜像
FROM ubuntu:16.04
# 配置环境变量，JDK的安装目录、容器内时区
ENV JAVA_DIR=/usr/local
ENV TZ=Asia/Shanghai
# 拷贝jdk和java项目的包
COPY ./jdk8.tar.gz $JAVA_DIR/
COPY ./docker-demo.jar /tmp/app.jar
# 设定时区
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# 安装JDK
RUN cd $JAVA_DIR \
 && tar -xf ./jdk8.tar.gz \
 && mv ./jdk1.8.0_144 ./java8
# 配置环境变量
ENV JAVA_HOME=$JAVA_DIR/java8
ENV PATH=$PATH:$JAVA_HOME/bin
# 指定项目监听的端口
EXPOSE 8080
# 入口，java项目的启动命令
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

**所以，就有人提供了基础的系统加JDK环境，我们在此基础上制作java镜像，就可以省去JDK的配置了：**

```Dockerfile
# 基础镜像
FROM openjdk:11.0-jre-buster
# 设定时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# 拷贝jar包
COPY docker-demo.jar /app.jar
# 入口
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

## 镜像构建

然后，执行命令，构建镜像：

```Bash
# 进入镜像目录
cd /root/demo
# 开始构建
docker build -t docker-demo:1.0 .
```

命令说明：

`docker build `: 就是构建一个docker镜像

-t docker-demo:1.0` ：`-t`参数是指定镜像的名称（`repository`和`tag`）

`.` : 最后的点是指构建时Dockerfile所在路径，由于我们进入了demo目录，所以指定的是`.`代表当前目录，也可以直接指定Dockerfile目录：

- ```Bash
  # 直接指定Dockerfile目录
  docker build -t docker-demo:1.0 /root/demo
  ```

## 容器网络互联

**默认情况下，所有容器都是以bridge方式连接到Docker的一个虚拟网桥上**

![](assets\1732892942410.png)



**但是，容器的网络IP其实是一个虚拟的IP，其值并不固定与某一个容器绑定，如果我们在开发时写死某个IP，而在部署时很可能MySQL容器的IP会发生变化，连接会失败。**

**所以，我们必须借助于docker的网络功能来解决这个问题，官方文档：**

**https://docs.docker.com/engine/reference/commandline/network/**

**常见命令有：**

| **命令**                  | **说明**                 | **文档地址**                                                 |
| :------------------------ | :----------------------- | :----------------------------------------------------------- |
| docker network create     | 创建一个网络             | [docker network create](https://docs.docker.com/engine/reference/commandline/network_create/) |
| docker network ls         | 查看所有网络             | [docs.docker.com](https://docs.docker.com/engine/reference/commandline/network_ls/) |
| docker network rm         | 删除指定网络             | [docs.docker.com](https://docs.docker.com/engine/reference/commandline/network_rm/) |
| docker network prune      | 清除未使用的网络         | [docs.docker.com](https://docs.docker.com/engine/reference/commandline/network_prune/) |
| docker network connect    | 使指定容器连接加入某网络 | [docs.docker.com](https://docs.docker.com/engine/reference/commandline/network_connect/) |
| docker network disconnect | 使指定容器连接离开某网络 | [docker network disconnect](https://docs.docker.com/engine/reference/commandline/network_disconnect/) |
| docker network inspect    | 查看网络详细信息         | [docker network inspect](https://docs.docker.com/engine/reference/commandline/network_inspect/) |

**demo：自定义网络**

```Bash
# 1.首先通过命令创建一个网络
docker network create hmall

# 2.然后查看网络
docker network ls
# 结果：
NETWORK ID     NAME      DRIVER    SCOPE
639bc44d0a87   bridge    bridge    local
403f16ec62a2   hmall     bridge    local
0dc0f72a0fbb   host      host      local
cd8d3e8df47b   none      null      local
# 其中，除了hmall以外，其它都是默认的网络

# 3.让dd和mysql都加入该网络，注意，在加入网络时可以通过--alias给容器起别名
# 这样该网络内的其它容器可以用别名互相访问！
# 3.1.mysql容器，指定别名为db，另外每一个容器都有一个别名是容器名
docker network connect hmall mysql --alias db
# 3.2.db容器，也就是我们的java项目
docker network connect hmall dd

# 4.进入dd容器，尝试利用别名访问db
# 4.1.进入容器
docker exec -it dd bash
# 4.2.用db别名访问
ping db
# 结果
PING db (172.18.0.2) 56(84) bytes of data.
64 bytes from mysql.hmall (172.18.0.2): icmp_seq=1 ttl=64 time=0.070 ms
64 bytes from mysql.hmall (172.18.0.2): icmp_seq=2 ttl=64 time=0.056 ms
# 4.3.用容器名访问
ping mysql
# 结果：
PING mysql (172.18.0.2) 56(84) bytes of data.
64 bytes from mysql.hmall (172.18.0.2): icmp_seq=1 ttl=64 time=0.044 ms
64 bytes from mysql.hmall (172.18.0.2): icmp_seq=2 ttl=64 time=0.054 ms
```

## DockerCompose

**大家可以看到，我们部署一个简单的java项目，其中包含3个容器：**

- **MySQL**
- **Nginx**
- **Java项目**

**而稍微复杂的项目，其中还会有各种各样的其它中间件，需要部署的东西远不止3个。如果还像之前那样手动的逐一部署，就太麻烦了。**

**而Docker Compose就可以帮助我们实现多个相互关联的Docker容器的快速部署。它允许用户通过一个单独的 docker-compose.yml 模板文件（YAML 格式）来定义一组相关联的应用容器。**

**docker-compose文件中可以定义多个相互关联的应用容器，每一个应用容器被称为一个服务（service）。由于service就是在定义某个应用的运行时参数，因此与`docker run`参数非常相似。**

**举例来说，用docker run部署MySQL的命令如下：**

```Bash
docker run -d \
  --name mysql \
  -p 3306:3306 \
  -e TZ=Asia/Shanghai \
  -e MYSQL_ROOT_PASSWORD=123 \
  -v ./mysql/data:/var/lib/mysql \
  -v ./mysql/conf:/etc/mysql/conf.d \
  -v ./mysql/init:/docker-entrypoint-initdb.d \
  --network hmall
  mysql
```

**如果用`docker-compose.yml`文件来定义，就是这样：**

```YAML
version: "3.8"

services:
  mysql:
    image: mysql
    container_name: mysql
    ports:
      - "3306:3306"
    environment:
      TZ: Asia/Shanghai
      MYSQL_ROOT_PASSWORD: 123
    volumes:
      - "./mysql/conf:/etc/mysql/conf.d"
      - "./mysql/data:/var/lib/mysql"
    networks:
      - new
networks:
  new:
    name: hmall
```

**对比如下：**

| **docker run 参数** | **docker compose 指令** | **说明**   |
| :------------------ | :---------------------- | :--------- |
| --name              | container_name          | 容器名称   |
| -p                  | ports                   | 端口映射   |
| -e                  | environment             | 环境变量   |
| -v                  | volumes                 | 数据卷配置 |
| --network           | networks                | 网络       |

**以下是一个多文件的部署demo**

**黑马商城部署文件：**

```YAML
version: "3.8"

services:
  mysql:
    image: mysql
    container_name: mysql
    ports:
      - "3306:3306"
    environment:
      TZ: Asia/Shanghai
      MYSQL_ROOT_PASSWORD: 123
    volumes:
      - "./mysql/conf:/etc/mysql/conf.d"
      - "./mysql/data:/var/lib/mysql"
      - "./mysql/init:/docker-entrypoint-initdb.d"
    networks:
      - hm-net
  hmall:
    build: 
      context: .
      dockerfile: Dockerfile
    container_name: hmall
    ports:
      - "8080:8080"
    networks:
      - hm-net
    depends_on:
      - mysql
  nginx:
    image: nginx
    container_name: nginx
    ports:
      - "18080:18080"
      - "18081:18081"
    volumes:
      - "./nginx/nginx.conf:/etc/nginx/nginx.conf"
      - "./nginx/html:/usr/share/nginx/html"
    depends_on:
      - hmall
    networks:
      - hm-net
networks:
  hm-net:
    name: hmall
```

**基础命令**

**基本语法如下：**

```Bash
docker compose [OPTIONS] [COMMAND]
```

**其中，OPTIONS和COMMAND都是可选参数，比较常见的有：**

| **类型** | **参数或指令**                                               | **说明**                    |
| :------- | :----------------------------------------------------------- | :-------------------------- |
| Options  | -f                                                           | 指定compose文件的路径和名称 |
| -p       | 指定project名称。project就是当前compose文件中设置的多个service的集合，是逻辑概念 |                             |
| Commands | up                                                           | 创建并启动所有service容器   |
| down     | 停止并移除所有容器、网络                                     |                             |
| ps       | 列出所有启动的容器                                           |                             |
| logs     | 查看指定容器的日志                                           |                             |
| stop     | 停止容器                                                     |                             |
| start    | 启动容器                                                     |                             |
| restart  | 重启容器                                                     |                             |
| top      | 查看运行的进程                                               |                             |
| exec     | 在指定的运行中容器中执行命令                                 |                             |
