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

新建html页面，引入vue文件

```
<script src="js/vue.js"></script>
```

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

## 插值表达式

**形式：{{}}**

**内容：变量，三元运算符，函数调用，算数运算**

## Vue常见指令

**指令：带有v-前缀的通常都是Vue指令**

| 指令      | 作用                                                |
| --------- | --------------------------------------------------- |
| v-bind    | 为html标签绑定属性值，如设置href,css样式等          |
| v-model   | 为表单元素上创建双向数据绑定                        |
| v-on      | 为html标签绑定事件                                  |
| v-if      |                                                     |
| v-else-if | 条件性的渲染某元素，判定为true时渲染，否则不渲染    |
| v-else    |                                                     |
| v-show    | 根据条件展示某元素，区别在于切换的是display属性的值 |
| v-for     | 列表渲染，遍历容器的元素或者对象的属性              |

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

**引用Axios文件**

```
<script src="js/axios-0.18.0.js"></script>
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

**get和post的区别：Get是向服务器发索取数据的一种请求，而Post是向服务器提交数据的一种请求**

## vue组件开发

**概念：vue组件文件以.vue结尾，每个组件由三部分组成： <template> <script> <style>**

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
npm install element-ui@2.15.3 
```

**在Main.js引入Element组件库**

```
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
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

**前端路由：URL中的hash(#号)与组件之间的对应关系**

**组成：**

**VueRouter：路由器类，根据路由请求在路由视图中动态渲染选中的组件**

**<router-link>：请求链接组件，浏览器会解析成<a>**

**<router-view>：动态视图组件，用来渲染展示与路由路径对应的组件**

```
Vue.use(VueRouter)

const routes = [
  {
    path: '/emp', //连接路径
    name: 'emp',  //路由名称
    component: () => import('../views/tlias/EmpView.vue')//连接的板块
  },
  {
    path: '/dept',
    name: 'dept',
    component: () => import('../views/tlias/DeptView.vue')
  }
]

const router = new VueRouter({
  routes
})
```

```
<router-link to="/">[text]</router-link>
```

**to：导航路径，要填写的是你在router/index.js文件里配置的path值，如果要导航到默认首页，只需要写成 to="/" ，**

**[text] ：就是我们要显示给用户的导航名称。**

```
<emp-view></emp-view>//在app.vue中使用这个标签进行访问
```

**[vue-router（路由）详细教程_vue 路由-CSDN博客](https://blog.csdn.net/wulala_hei/article/details/80488727)**

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

```
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

```
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

| 注解         | 说明                 | 位置                     |
| ------------ | -------------------- | ------------------------ |
| @Component   | 申明bean的基础注解   | 不属于以下三类时用此注解 |
| @Controller  | @Component的衍生注解 | 标注在控制器类上         |
| @Service     | @Component的衍生注解 | 标注在业务类上           |
| @Respository | @Component的衍生注解 | 标注在数据访问类上       |

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

**我们只需要在启动类定义一个方法返回值是需要管理的对象，在这个方法上面加上@Bean注解即可，但是一般我们建议定义一个配置类，在这个类上加上@Configuration,将这个方法放到这个类里**

**通过@Bean注解的name/value属性指定bean名称，如果未指定，则方法名就是**

**如果还需要给这个第三方bean加新的依赖的话，只需要在方法的参数加上对应依赖的形参即可,例如AliOSSUtils这个类还需要依赖AliOSSProperties，但是我们不能通过@Autowired进行注入，就可以用如下方法进行注入**



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

## 补充技术点

### ThreadLocal

**ThreadLoacl并不是一个Thread，而是Thread的局部变量，它为每一个线程提供单独一份的存储空间，具有线程隔离的效果，只有在线程内才能获取到对应的值，线程外则不能访问**

| 方法                     | 说明                                 |
| ------------------------ | ------------------------------------ |
| public void set(T value) | 设置当前线程的线程局部变量的值       |
| public T get()           | 返回当前线程所对应的线程局部变量的值 |
| public void remove()     | 移除当前线程的线程局部变量           |

**应用场景：在sjervice层需要获取用户的ID,而用户的ID在jwt令牌里，当我们解析完jwt令牌后，我们就可以把这个id存进ThreadLocal这个存储空间，因为解析jwt令牌和service同属一个线程，因此同时公用一个ThreadLocal内存空间，所以jwt解析阶段所放入的东西，可以被service层访问到**

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

## lombok

**lombok是一个实用的java类库，能通过注解的形式自动生成构造器，getter/setter,equals,hashcode,toString等方法，并可以自动化生成日志变量**

| 注解                | 作用                                                         |
| ------------------- | ------------------------------------------------------------ |
| @Getter/@Setter     | 为所有的属性提供get/set方法                                  |
| @ToString           | 会给类自动生成易阅读的toString方法                           |
| @EqualsAndHashCode  | 根据类所拥有的非静态字段自动重写equals和hashcode方法         |
| @Data               | 提供了更综合的生成代码功能（@Getter+@Setter+@ToString+@EqualsAndHashCode） |
| @NoArgsConstructor  | 为实体类提供生成无参的构造器方法                             |
| @AllArgsConstructor | 为实体类生成除了static修饰的字段之外带有各参数的构造器方法   |

```
<!--lombok-->
<dependency>
	<groupId>org.projectlombok</groupId>
	<artifactId>lombok</artifactId>
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

# Swagger

## 如何使用

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

## 常用注解

| 注解              | 说明                                                 |
| ----------------- | ---------------------------------------------------- |
| @Api              | 用在类上，例如Controller,表示对类的说明              |
| @ApiModel         | 用在类上，例如entity,DTO,VO                          |
| @ApiModelPropetry | 用在属性上，描述属性信息                             |
| @ApiOperation     | 用在方法上，例如Controller的方法，说明方法的用途作用 |



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

