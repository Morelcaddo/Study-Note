

# cmd指令相关

盘符：可以切换盘

dir:查询当前路径下的内容

cd目录:进入单级目录

cd..退回到上一个目录

cd 目录1\目录2进入多级目录

cd \ 回退到盘符目录

cls 清屏

exit 退出命令提示符窗口

# 环境变量

如何想要在任意的目录下打开指定的软件，只需要将该软件的路径配置到环境变量即可

# 字面量

指数据在程序中的书写格式，通常有整数类型，小数类型，字符串类型，字符类型，布尔类型，空类型,需要注意空类型null不能直接打印，必须“null”进行打印

\t  制表符，可以把前面的字符串补齐8或者8的倍数个，用空格补齐

进制相关：二进制0b开头，八进制0开头，十六进制0x开头，通过这个方式会输出该数字对应的十进制数字

# 数据类型

整数：byte(-128~127)(1),short(-32768~32767)(2),

int(-2147483648~-2147483647)(4),

long(-9223372036854775808~9223372036854775808)(8)

需要注意定义long类型的变量，要在数值的最后面加上l（大小写都可）

浮点数：float(-3.401298e-38~3.402823e+38)(4)

同上，数据后面要加上f（大小写都可）

double(-4.9000000e-324~1.797693e+308)(8)

字符：char(0~65535)(2)可以是一个英文字符，也可以是一个汉字

布尔：boolean(true,false)(1)

# 标识符

起名规则：必须有数字，字母，下划线，美元符$组成，不能以数字开头，不能是代码中的关键字，区分大小写

# 输入输出

输出：System.out.println(输出内容);

输入：

导包 import java.util.Scanner;

创建对象：Scanner sc=new Scanner(System.in);

接收整形数据：int x = sc.nextInt();//int可以变成Double等类那些

需要注意next()用于接收字符串类型空格 制表符回车就停止

nextLine()碰到回车才停止

System.out.println()自带换行输入，且可以进行拼接

System.out.print()类似C++的printf()也可以进行拼接





# 运算符

1：在代码中如果有小数进行运算，结果可能不够精确

隐式转换规则：byte<short<int<long<float<double

byte short char 进行运算时都会先转换成int在进行运算

运算中只要出现字符串，+的操作是拼接字符串

例如：123+”abc“=123abc

如果拼接过程出现了变量，则拼接的是变量的值

连续加时，从左到右依此运算

+= -= /=,*=,%=底层逻辑自带强制类型转换

# 条件分支语句

1：语局中只能放boolen类型的变量，而c++可以放整数型

2：对于boolean类型的值判断必须用=而不是==



# switch语句相关

1：表达式的取值可以是byte short int char jdk5以后可以是枚举，jdk7以后可以是String

2:   case 后面要跟的是要和表达式进行比较的值

3：break 用于中断语句

4：defalt 表示所有情况都不匹配时需要执行的语句

5： case后面的值只能是字面量不能是变量（字面量：就是实际的值如1 ，'a')

6： case的值不能重复

```
switch(){
            case 值1:
                语句1;
                break;
            case 值2:
                 语句2;
                 break;
            default:
                语句体n+1;
                break;
        }
```

7:   default语句可以省略，且位置随意

8： case穿透问题，语句开始执行时，会拿着表达式的值去跟case的值进行匹配，匹配上就会开始执行对应的case语句，遇到break就会停止，但倘若该case语句没有break，则会继续执行下面的case语句，直到遇到break语句或者大括号才会停止。

9： 对于对于多个值对应同一个语句的情况我们可以将他们合并，写成case v1,v2语句

10：对于jdk12往后的版本，case->语句体，进行执行，不需要break;

# 循环相关

1：for循环的循环体可以为空

# 随机数获取

1: 导包 import java.util.Random;

2: 创建对象 Random r=new Random();

3:生成 int num=r.nextInt(随机数的范围);右减左+1外面加左端点的值（右端点的值不包括在范围内）

```
r.nextInt(10)//0-9的随机数
```



# 数组

1：静态定义 int[] a={10,20,30};

2： a.length,返回数组的长度

3：动态定义 int[] a=new int[n];

4：二维初始化

```
int[][] a={{},{}};
```



# 方法

1：定义 public static void 方法名()括号内用于放参数

2：定义有返的方法，同上，void换成返回值类型

3：重载：方法名一样，参数类型数量不一样，且在同一个类下的方法构成重载

4： java中的方法返回值可以是数组类型

5： ctrl+alt+m一键提取方法



# 面向对象

获取对象：Student t=new Student()//获取一个Student类的变量t

用于描述一类事物的类叫javabean类，而main类一般称为测试类，在测试类创建javabean类进行测试和调用、

对象中的方法定义格式 public void/返回值类型 名称（参数）

一个代码文件只能有一个类是public修饰的，public修饰的类名必须是代码文件的名称

就近原则：成员变量和局部变量冲突时，依据就近原则，首先使用局部变量，此时如果要进行成员变量的赋值可以使用this.成员变量进行赋值

构造方法：方法名与类名相同，无返回值类型，不能有return,如果不写构造方法，则系统会给一个无参构造，如果自己写了一个构造，则系统不再提供

成员变量与局部变量的区别：

一个类内，方法外，一个方法内，方法声明上

有默认初始化值，无默认初始化值

堆内存 栈内存

一个随类的消失而消失，一个随方法

整个类中有效，整个方法中有效

alt+ins快速生成javabean类的方法

#  javabean

标准的javabean类，成员变量均为私有属性，具有无参构造和带有全部参数的有参构造，每个成员变量都有set,get方法

# 字符串

1：创建后无法被更改，如果改变，相当于重新创建（重新new一个字符串）

2：不需要导包，属于基础包

3：涉及类操作，或者new操作的，变量记录的往往是地址，要注意

4：比较字符串可以使用String类的equals方法，其中equalsIgnoreCase()方法可以忽略大小写进行比较

5：字符串遍历时，用循环从0跑到字符串长度减一的位置，并用charAt(i)去遍历每一个字符

6：涉及字符串替换时使用replace()参数是替换目标字符串，以及替换成的字符串。

7：StringBuilder类是一个可变的字符串容器，可以快速修改，append()方法添加数据返回对象本身，reverse()方法反转字符串，toString()转换为String类型

8：字符串在使用+进行拼接时，本质上也是在使用StringBuilder类进行拼接，效率很低，jdk8以后，拼接操作变成，先预估然后创建一个数组，数组转化成字符串

9：StringJoiner类构造函数里放的是每一次添加的字符串之间的间隔符，开始符号以及终止符号三个变量，注意需要导包

添加时用的是add方法

10：易错案例

```java
public class Main {
    public static void main(String[] args) {
        String s1 = "abc";
        String s2 = "a" + "b" + "c";
        System.out.println(s1 == s2);//true
    }
}//保存的是串池中的地址，串池中有的直接用串池中的地址
```

11：substring方法去截取字符串，参数分别是起始下标和终止下标

```
public boolean startsWith(String prefix)//判断该字符串是否包含特定的前缀
```

12：java的String即使是汉字，跟英文字符串一致，只占一位，如第一个汉字就是s.charAt(0)

# 集合

1：存储引用数据类型，且长度可变，类似与C++STL

2: Arraylist集合需要导包，定义方式Arraylist<引用数据类型> name=new Arraylist<>();集合可以直接被打印

3：对应基本类型的包装类

byte Byte  short Short  char Charcter int Integer long Long float Float  double Double boolean Boolean

# static关键字

1:静态变量是随着类而动的，类没被创建时他就可以被赋值，赋值方法或者访问方法类名.名称

2:静态方法没有this关键字，非静态有但是看不见，this记录的调用方法的调用者的地址值，由虚拟机赋值

3:静态方法不能调用非静态的成员方法或者变量，非静态的可以

# 静态代码块

随着类的加载而加载，且只执行一次

# 继承

```
public class A extends B {

}
//A继承B，且java中默认继承虚拟机中的Object类
```

1：子类不能继承父类的构造方法

2：子类可以继承父类的成员变量，私有的变量不能被直接使用

3：每一个类都会有一个虚方法表，记录的是非private,非static,非final修饰的方法，并传给子类，且能被虚方法表记录的方法才能被继承

4：

```
public class Fu {
    public String name="Father";
}

class Zi extends Fu{
    public String name="son";
    void show(){
        String name="real";
        System.out.println(name);
        System.out.println(this.name);
        System.out.println(super.name);
    }
}//就近原则的运用
```

5: 子类中的构造方法默认先访问父类中的无参构造，且子类的构造方法默认第一句是super(),不写也存在，且在第一行，如果要调用父类的有参构造，则需要手写super(参数)进行调用

6:继承关系只能是单继承不能是多继承

# 多态

1：多态中调用成员变量的方法，编译看左边，运行也看左边，调用方法时，编译看左边，运行看右边（编译就是说左边必须有相应的方法才能够编译成功，运行是说优先运行右边的方法，右边没有则运行左边的,在方法中参数是父类承接子类的操作也属于多态，效果类似上面）

2：继承关系的类之间可以进行强制转换

3：instanceof是Java中的二元运算符，左边是对象，右边是类；当对象是右边类或子类所创建对象时，返回true；否则，返回false。

4：关于多态，子类可以是父类，但父类不能转换为子类，但也分情况

```
Father f = new Father();
Son s = (Son)f;//出错 ClassCastException
```

```
Father f = new Son();
Son s = (Son)f;//可以
```

```
Son s = new Son();
Father f = (Father)s;//可以
```

5： 定义格式：父类类型 变量名=new 子类类型();



# final关键字

1:修饰方法，代表该方法不能被重写

2:修饰类，代表该类不能继续继承出新的子类

3:修饰变量，变量的值在被定义赋值后无法被修改，需要注意引用数据类型不可变的是地址

# 权限修饰符

private:同一个类中使用

空着不写：private基础上多一个同一个包中的其他类可以使用

protected:空着不写的基础上多一个不同包的子类可以使用

public:都可以用

# 代码块

{}里的内容就是一个代码块，代码块里的程序执行完后，会自动释放内存

创建类时，先执行代码块在执行本类的构造方法，作用是把多个构造方法中的重复代码提取出来

static{}静态代码块，随着类的加载而加载，且只执行一次

# 抽象类和抽象方法

抽象方法必须强制重载，相当于只给子类留一个接口，类似C++虚函数，且没有具体的方法体，public abstract 返回值类型 方法名(参数)

抽象类 public abstract class 类名{}，方法抽象后所在类就是抽象类

抽象类不能实例化，抽象类不一定由抽象方法，抽象方法所在的类一定是抽象类，抽象类可以有构造方法，抽象类的子类要么重写抽象类中的所有抽象方法，要么自己也是抽象类

# 接口

public interface 接口名{}进行接口定义，接口能实例化，实例化通过匿名内部类实现，或者new他的子类对象，接口的子类要么实现接口的抽象方法，要么是抽象类

接口和类之间是实现关系，public class implements 接口名1 接口名2{}

接口中的成员变量只能是常量，默认public static final属性，没有构造方法，成员方法是抽象方法，默认修饰符 public abstract

接口和类的关系，可以单实现也可以多实现，还可以继承一个类的同时实现多个接口

接口和接口之间可以单继承也可以多继承

允许在接口中定义默认方法，需要使用关键词default修饰，解决接口升级的问题，public default void show(){}

默认方法不是抽象方法，所以不强制被重写，但是如果被重写，在重写的类里需要去掉default关键词

public可以省略，default不可以省略

如果实现多个接口，且多个接口中存在同名的默认方法，则子类必须对该方法重写

jdk8以后允许在接口定义静态方法，需要用static修饰

静态方法只能由接口名调用，不能通过实现类名或者对象名进行调用

public可以省略，static不能省略

jdk9以后private void show(){}

接口也有多态的操作

适配器设计思想，在接口和实现类之间加一个抽象类,为了避免其他类创建适配器类的对象，中间的适配器类用abstract

# 内部类

内部类可以直接访问外部类的成员，包括私有，外部类要访问内部类的成员，必须要创建对象

获取内部内的对象，在外部类中编写方法，对外提供内部类的对象，或者直接创建Outer.Inter oi=newOuter().newInter(),直接创建需要能被外界访问

当变量重名时this.调用的是该内部类的变量，外部类.this.调用的是外部类的变量

静态内部类只能访问外部类的静态变量和方法，想要访问非静态的需要创建对象，静态方法类的创建 Outer.Inter oi=new Outer.Inter()

内部类的非静态方法通过创建对象去调用，静态方法用外部类.内部类.方法名调用

将内部类定义在方法里叫局部内部类，外界无法使用局部内部类，需要在方法内部创建对象使用

局部内部类可以访问外部类的变量也可以方法方法的局部变量

什么时候需要内部类：当一个类依赖另一个类存在时，而他单独存在没有意义时，就可以创建某个类的内部类

# 匿名内部类

new 类名/接口{重写方法}，继承或者实现，方法重写，创建对象，可以将整个匿名内部类打包放进方法参数里

# GUI图形化界面

java的图形化界面相关的接口分别在AWI包和Swing包下

一个软件可以分成三个部分，JFrame(最外层窗体)，JMenuBar(最上层菜单)，JLabel(管理文字和图片的容器)

导包和创建一个窗口

```
import javax.swing.*;

JFrame gameJframe=new JFrame();

```

设置界面窗口

```
private void initJFrame() {
    //设置界面的宽高
    this.setSize(608, 630);
    //设置界面标题
    this.setTitle("拼图游戏1.0");
    //设置界面置顶
    this.setAlwaysOnTop(true);
    //设置界面居中
    this.setLocationRelativeTo(null);
    //取消默认的居中放置，只有取消了才会按照xy周的形式添加组件
    this.setLayout(null);
    //设置关闭模式
    //"WindowConstants.DO_NOTHING_ON_CLOSE",
    //"WindowConstants.HIDE_ON_CLOSE",
    //"WindowConstants.DISPOSE_ON_CLOSE",多界面存在时，关掉最后一个才会关闭程序
    //"WindowConstants.EXIT_ON_CLOSE"退出当前界面时程序终止
    this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
}
```

设置菜单界面

```
private void initJMenubar() {
        //创建菜单对象
        JMenuBar JmenuBar = new JMenuBar();
        //创建选项对象
        JMenu functionJMenu = new JMenu("功能");
        JMenu aboutJMenu = new JMenu("关于我们");
        //创建下面的条目对象
        JMenuItem replayItem = new JMenuItem("重新游戏");
        JMenuItem reLoginItem = new JMenuItem("重新登录");
        JMenuItem closeItem = new JMenuItem("关闭游戏");
        JMenuItem accountItem = new JMenuItem("公众号");
        //把条目添加到选项中
        functionJMenu.add(replayItem);
        functionJMenu.add(reLoginItem);
        functionJMenu.add(closeItem);
        functionJMenu.add(accountItem);
        //将选项添加到菜单中
        JmenuBar.add(functionJMenu);
        JmenuBar.add(aboutJMenu);
        //给窗口设置这个菜单
        this.setJMenuBar(JmenuBar);
    }
```

创建图像及图像容器并进行添加图片的操作

```
private void initImage() {
        //创建图像
        ImageIcon icon = new ImageIcon("D:\\idea\\project\\study1\\image\\animal\\animal3\\3.jpg");

        //创建一个JLabel图片管理容器
        JLabel jLabel = new JLabel(icon);

        //指定图片位置
        jLabel.setBounds(0, 0, 105, 105);

        //将管理容器添加到界面中,默认放置在中央
        //this.add(jLabel);
        //调用隐藏容器进行添加图片容器
        this.getContentPane().add(jLabel);
    }
```

JLabel既可以管理图片也可以管理文字

事件：当事件源发生了某个事件，则执行某段代码，有以下三种 KeyListener(键盘监听) MouseListener(鼠标监听) ActionLIstener(动作监听)

创建一个按钮对象 JButton

```
private void initJButton() {

        //new一个按钮类，并且起名
        JButton jtb1 = new JButton("点我呀");
        //设置位置及大小
        jtb1.setBounds(0, 0, 100, 50);
        //添加动作监听(无动作限制，任何动作都可触发)
        jtb1.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.out.println("鼠标被点击了");
            }
        });

        //添加该按钮
        this.getContentPane().add(jtb1);
    }
```

MouseListener接口用于承接鼠标所引发的动作

```
mouseClicked()//单击
mousePressed()//按住不松
mouseReleased()//松开
mouseEntered()//划入
mouseExited()//划出
```

KeyListener接口用于承接键盘所引发的动作

```
keyPressed()//按下键时使用,按下不松时，才触发
keyRelesed()//当键被释放时调用
keyTyped()键入键时使用,个别键无法识别
 public void keyReleased(KeyEvent e) {
        char c = e.getKeyChar();//获取键盘上按键的字符
        e.getKeyCode();//获取按键的编码
               
}
```

添加背景图片

```
//先加载的图片在上方后加载的图片在下方
//创建背景图片容器
JLabel background=new JLabel(new ImageIcon("D:\\idea\\project\\study1\\image\\background.png"));
background.setBounds(40,40,508,560);
//添加背景图片
this.getContentPane().add(background);
```

创建一个弹窗对象

```
 //创建一个弹窗对象
JDialog jDialog = new JDialog();
//创建管理图片的容器
JLabel jLabel = new JLabel(new ImageIcon("image/Myself.png"));
//设置位置和宽高
jLabel.setBounds(0, 0,288 , 288);
//添加图片在弹窗中
jDialog.getContentPane().add(jLabel);
//给弹窗设置大小
jDialog.setSize(600, 600);
//让弹框置顶
jDialog.setAlwaysOnTop(true);
//让弹框居中
jDialog.setLocationRelativeTo(null);
//让弹窗不关闭无法操作以下界面
jDialog.setModal(true);
//让弹框显示出来
jDialog.setVisible(true);
```

明文显示的输入框组件JTextField

```
//添加用户名输入框
JTextField username=new JTextField();
username.setBounds(195,134,200,30);
this.getContentPane().add(username);
```

密文显示的输入框组件JPasswordField

关于添加插件图片的处理

```
//5.添加登录按钮
JButton login = new JButton();
login.setBounds(123, 310, 128, 47);
login.setIcon(new ImageIcon("image\\login\\登录按钮.png"));
//去除按钮的默认边框
login.setBorderPainted(false);
//去除按钮的默认背景
login.setContentAreaFilled(false);
this.getContentPane().add(login);
```

界面刷新

```
//刷新一下界面
this.getContentPane().repaint();
```

# 常用API接口

## math

```
Math.random();//返回一个double类型的随机数，范围[0.0,1.0)
Math.absExact(int a);//返回这个数的绝对值，与abs不同，当数值爆int会给出系统报错提示
Math.cbrt(int a);//开立方根
```

## System

```
System.exit();//强制关闭虚拟机，0正常停止，非零异常停止
System.currentTimeMillis();//返回当前系统的时间毫秒值形式，即从时间原点到当前系统时间所过的毫秒，返回值long
//时间原点：1970年1月1日 00:00:00 国内东八区，获取到的是08:00:00
System.arraycopy();//数组拷贝
//参数1，要拷贝的数据从哪个数组来
//参数2：从数据源数组中的第几个索引开始拷贝
//参数3：目的地，把数据拷贝到哪个数组
//参数4：目的地数据的索引
//参数5：拷贝的个数
//细节1：两个数组的数据类型需一致
//细节2：需要考虑到数组的长度
//细节3：如果数据源数组和目的地数组都是引用数据类型，那么子类类型可以赋值给父类类型
```

## Runtime

```
Runtime.getRuntime();//当前系统的运行环境对象
Runtime.getRuntime().exit();//停止虚拟机
Runtime.getRuntime().availableProcessors();//获得CPU的线程数
Runtime.getRuntime().maxMemory();//JVM能从系统中获取的总内存大小
Runtime.getRuntime().totalMmemory();//JVM已经从系统中获取的总内存大小
Runtime.getRuntime().exec();//运行cmd命令
```

## Object相关

```
Object obj=new Object();
System.out.println(obj.toString());
//java.lang.Object@4eec7777(包名+类名+@+地址值),这是对于类来说
System.out.println(obj);//也可以打印出类似的效果
//输出语句的核心逻辑
//当我们打印一个对象时，会调用对象的toString方法，把对象变成字符串
//然后打印到控制台上，打印完毕做换行处理

Student s1=new Student();
Student s2=new Student();
System.out.println(s1.equals(s2));
//object内置的equals方法是用==比较，对于引用型变量,比较的是地址值,如果要比较属性值，需要重写
//字符串调用equals方法时，先判断是否为同一对象，是的话直接返回true，不是的话继续下面的判断
//然后判断参数是否为字符串
//如果是就比较内部属性
//不是直接返回false
//StringBuilder中没有重写equals()方法，使用的是object的，因此比较的是两者的地址值

//受查异常
//受查异常会在编译时被检测。如果一个方法中的代码会抛出受查异常，则该方法必须包含异常处理，即 try-catch 代码块，或在方法签名中用 //throws 关键字声明该方法可能会抛出的受查异常，否则编译无法通过。如果一个方法可能抛出多个受查异常类型，
//，就必须在方法的签名处列出所有的异常类。

Objects.isNull(Object a);//判断对象是否为null,为null返回true
Objects.nonNull(Object a);//跟上面一样，只不过为null返回false
```



## 克隆和拷贝

```
//克隆细节：
//方法在底层会帮我们创建一个对象，并把原对象的数据拷贝过去
//注意：
//1：要在类中重写Object类的clone方法，只需重写，不需要改变函数的内容
//2：javabean类要实现Cloneable这个接口
//3；重写的clone方法返回的是Object类，要进行强转
//4：要添加异常到方法签名中去，否则会报错，关于这段处理上面有进行文字解释
Student s3=new Student("张三");
Student s4=(Student)s3.clone();
//关于拷贝和克隆，引用类型的变量，让两个对象等于相同的地址值，即拷贝地址值，非引用拷贝变量的值，这种叫浅克隆，浅拷贝
//深克隆，是一个新地址，然后把原数据拷贝一份到新的地址中
//Object的克隆在对对象本身进行克隆时是深克隆，是用一个新地址去放新的对象，但是对于克隆的对象里面的引用型变量的克隆是浅克隆

//第三方工具库
//1：导入第三方工具库
//2：编写代码
Gson gson=new Gson();
//把对象变成字符串
String s=gson.toJson(s3);
//再把字符串变回对象就可以了
Student s5=gson.fromJson(s,Student.class);

//在java中null不能调用方法
Objects.equals(Object a,Object b);//先非空判断，然后比较两个对象
//细节
//1：方法的底层会判断s1是否为null，如果为null,返回false
//2：如果s1为null，那么就利用s1再次调用equals方法
//3：此时s1是Student类则调用重写的equal方法
//如果没有重写，则比较地址值，如果重写了，按重写后的来
```

## BigInteger

```
import java.math.BigInteger;//首先导包
//BigInteger的构造方法
public BigInteger(int num,Random rnd)//获取随机大整数，范围[0~2的num次方-1]
public BigInteger(String val)//获取一个指定的大整数，字符串中必须是整数，否则会报错
public BigInteger(String val,int raidx)//获取指定进制的大整数,会显示这个val对应进制转换成十进制的结果

public static BigInteger valueOf(long val)//静态方法获取BigInteger的对象，内部有优化
//细节：能表示的范围只在long的范围，数字后面+L，代表该数字是long
//2：在内部对常用的数字：-16~16进行了优化，提前把-16~16先创建好BigInteger的对象，如果多次重新获取不会创建新的 
BigInteger bd1=BigInteger.valueOf(16);
BigInteger bd2=BigInteger.valueOf(16);
System.out.println(bd1==bd2);//true
//由上述案例可知，这两个对象地址一样，说明没有创建新的对象
//对象一旦创建内部的数据不能发生改变
BigInteger bd1=BigInteger.valueOf(3);
BigInteger bd2=BigInteger.valueOf(5);

public BigInteger add(BigInteger val)//加法
BigInteger ans=bd1.add(bd2);
System.out.println(bd1==ans);//false
System.out.println(bd2==ans);//false;
//此时不会修改BigInteger对象中的值，而是产生了一个新的BigInteger对象记录3,不仅局限于该构造方法
public BigInteger subtract(BigInteger val)//减法
BigInteger bd1=BigInteger.valueOf(3);
BigInteger bd2=BigInteger.valueOf(5);
BigInteger ans=bd1.subtract(bd2);

public BigInteger multiply(BigInteger val)//乘法
BigInteger bd1=BigInteger.valueOf(3);
BigInteger bd2=BigInteger.valueOf(5);
BigInteger ans=bd1.multiply(bd2);

public BigInteger divide(BigInteger val)//除法
BigInteger bd1=BigInteger.valueOf(3);
BigInteger bd2=BigInteger.valueOf(5);
BigInteger ans=bd1.divide(bd2);//结果是商，且是整数

public BigInteger[] divideAndRemainder(BigInteger val)//除法，获取商和余数
BigInteger bd1=BigInteger.valueOf(-10);
BigInteger bd2=BigInteger.valueOf(5);
BigInteger[] ans=bd1.divideAndRemainder(bd2);
System.out.println(ans[0]+" "+ans[1]);//前者是商，后者是余数

public boolean equals(Object x)//比较属性值是否相同
BigInteger bd1=BigInteger.valueOf(-10);
BigInteger bd2=BigInteger.valueOf(5);
System.out.println(bd1.equals(bd2));


public BigInteger pow(int exponent)//幂运算，返回值是BigInteger类型
BigInteger bd1=BigInteger.valueOf(-10);
System.out.println(bd1.pow(10));

public BigInteger max(BigInteger val)//返回较大值
BigInteger bd1=BigInteger.valueOf(-10);
System.out.println(bd1.max(100));

public BigInteger min(BigInteger val)//返回较小值
BigInteger bd1=BigInteger.valueOf(-10);
System.out.println(bd1.min(100));

public int intValue()//转为int类型的整数，超出范围会报错,还有longValue,doubleValue
BigInteger bd1=BigInteger.valueOf(-10);
bd1.intValue()

//BigInteger 最大数据为21亿的21亿次方，范围的数字个数大概是42亿的21亿次方
//底层原理：把待存按二进制32位位一组拆分，放进数组里，数组的大小上限是21亿,数组中每一位表示的数字有42亿
```

## BigDecimal

```
//因为小数计算的不精确问题，我们引用了BigDecimal,用于小数的精算运算，或者存储很大的小数
//BigDecimal是不可变的有符号十进制数
public BigDecimal(double val)//用这个构造任然有可能存在精度上的问题
public BigDecimal(string val)//建议使用这种构造，精确度更高
public static BigDecimal valueOf(double val)//通过静态方法的形式获取对象
public static BigDecimal valueOf(long val)
//细节
//1：如果要表示的数字不大，没有超出double的数值范围，建议使用静态方法
//2：如果表示对额数字较大，超出了double的取值范围，建议使用构造方法
//3：如果我们传递的是0~10之间的整数，包含0，包含10，那么会返回已经创建好的对象，不会重写new

public BigDecimal add(BigDecimal val)//加法
BigDecimal bd1=new BigDecimal("10.3");
BigDecimal bd2=new BigDecimal("10.2");
System.out.println(bd1.add(bd2));

public BigDecimal subtract(BigDecimal val)//减法
BigDecimal bd1=new BigDecimal("10.3");
BigDecimal bd2=new BigDecimal("10.2");
System.out.println(bd1.subtract(bd2));

public BigDecimal multiply(BigDecimal val)//乘法
BigDecimal bd1=new BigDecimal("10.3");
BigDecimal bd2=new BigDecimal("10.2");
System.out.println(bd1.multiply(bd2));

public BigDecimal divide(BigDecimal val)//除法
BigDecimal bd1=new BigDecimal("10");
BigDecimal bd2=new BigDecimal("4");
System.out.println(bd1.divide(bd2));//2.5
//注意：如果结果是除不尽的情况，则按下述情况处理
public BigDecimal divide(BigDecimal divisor, int scale, RoundingMode roundingMode)
//后两个参数表示，精确到几位小数，以及舍入模式，舍入模式详见API开发文档
//BIgDecimal的底层存储
//底层存储的是每一个字符对应的ASIIC

public BigDecimal stripTrailingZeros()//格式处理，去掉多余的零
public String toPlainString()//转化成标准字符串格式输出

```

## 正则表达式

用于校验数据是否合法

```
//String下的方法matches
public boolean matches(String regex)
//regex代表规则，规则书写遵循从左往右的顺序
//案例：6位及20位以内，0不能在开头，必须全部是数字
//regex="[1-9]\\d{5,19}",{}里的数字表示出现的次数，[1-9]代表第一位非0数，\\d代表是必须是数字
```

正则表达式基础用法,字符类（只匹配一个字符）

```
[abc]			只能是a,b,c
[^abc]			除了a，b，c之外的任何字母
[a-zA-Z]		a到z A到Z，包括范围
[a-d[m-p]]		a到d，或m-p
[a-z&&[def]]	a-z和def交集
//注意：这里写成&，这里只表示&符号
[a-z&&[^bc]]	a-z和除bc外的交集
[a-z&&[^m-p]]	a到z和除了m到p的交集
```

预定义字符（只匹配一个字符）

```
.		任何字符
\d		一个数字：[0-9]
\D		非数字：[^0-9]
\s		一个空白字符：[\t\n\x0B\f\r]
\S		非空白字符：[^\s]
\w		[a-zA-Z_0-9]英文，数字，下划线
\W		[^\W]一个非单词字符
//注意：实际写的时候是两个\\,因为\有特殊含义，需要转义
```

数量词

```
X?		X,一次或0次
X*		X,0次或多次
X+		X,一次或多次
X{n}	X,正好n次
X{n,}	X，至少n次
X{n,m}	X,至少n但不超过m
```

api帮助文档查找Pattern即可查找正则表达式相关

```
//电话验证
//分析：
//第一位：1代表第一个数字只能是1
//第二位：[3-9]代表第二位字符的数据范围是字符3-9
//\\d代表数字{9}代表后面的位数里数字出现的次数是9次
Scanner sc=new Scanner(System.in);
String test1=sc.next();
System.out.println(test.matches("1[3-9]]\\d{9}"));
```

## 爬虫

```
import java.util.regex.Pattern;//导包

//Pattern 表示一个正则表达式的对象
//Matcher 文本匹配器，作用按照正则表达式的规则去读取字符串，从头开始读取，再大串中寻找符号匹配规则的子串
//需求：寻找文本中所有的javaXX字样

//获取一个Pattern对象
String str = "java5656";
Pattern p = Pattern.compile("java\\d{0,2}");
//获取文本匹配器的对象
Matcher m = p.matcher(str);
        
//分析：
//1:每一论调用Matcher对象m的find函数，寻找有没有符合条件的子串，有就会返回true，并且停止读取，并且记录下字符串的索引，在调用group方法截取这段，字符串读取完之后，find继续查找 
//索引的字符串，返回字符串
while(m.find()){
    String s=m.group();
    System.out.println(s);
    }  
贪婪爬取和非贪婪爬取：
//案例："abbbbbbbbbccc"，则获取abbbbbbbbb，非贪婪只有ab
String regex="ab+";//贪婪爬取
String regex="ab+?"；//非贪婪爬取
Pattern p=Pattern.compile(regex);
Matcher m=p.matcher(s);
while(m.find()){
	System.out.println(m.group());
}

正则表达式在字符串方法中的使用
public boolean matches(String regex)  判断字符串是否满足正则表达式的规则
public String replaceAll(String regex, String replacement)  按照正则表达式的规则替换满足规则的字符串为replacement
public String[] split(String regex)  按照正则表达式的规则切割字符串，找到符合规则字符串以那个位置为分界进行切割

//正则表达式的分组
//给正则表达式加上()就是一个分组，每个组都有组好，从开始，以左括号为基准，在表达式内部使用可以使用\\1,\\2来表示第几组，在外面，使用$1,$2
```

## 时间

```
Date时间类
import java.util.Date;
public Date() {this(System.currentTimeMillis());}//空参构造
public Date(long date) {fastTime = date;}//有参构造，构造过时间原点开始过了data毫秒的时间
public void setTime(long time)//修改时间为，离时间原点time毫秒的时间
public long getTime()//获取当前时间的毫秒值

SimpleDateFormat 时间格式化类，并且可以把字符串表示的时间变成Date类
public SimpleDateFormat()//无参构造
public SimpleDateFormat(String pattern)//使用指定格式进行构造,如"yyyy年MM月dd日 HH:mm:ss" E可以代表星期
public final String format(Date date)//格式化(日期对象->字符串)，按照构造时放入的格式进行格式化
public Date parse(String source)//解析(字符串->日期对象)，String待解析的时间字符串，按照构造的格式进行解析

Calendar 代表系统当前时间的日历对象，注意这是一个抽象类
public static Calendar getInsatance();//获取当前时间的日历对象
//会根据系统的不同时区获取不同的日历对象，
//会把时间中的纪元，年，月，日，时，分，秒，星期等等放到同一个数组中
//月份范围0-11，星期里，1代表星期天
public final Date getTime();//获取日期对象vb
public final setTime(Date date);//给日历设置日期对象
public long getTimeInMillis();//拿到时间的毫秒值
public void setTimeInmillis(long millis);//给日历设置时间毫秒值
public int get(int filed);//获取日历中的某个字段的信息，filed代表相应的索引
0代表纪元，1年，2月，3日，4时，5分，6秒
public void set(int filed,int value);//修改日历的某个字段信息
piblic void add(int filed,int amount);//为某个字段增加/减少指定的值

ZoneID时区
public static Set<String> getAvailableZoneIds()；//获取所有时区
public static ZoneId systemDefault();//获取系统默认时区
public static ZoneId of(String zoneId);//获取一个指定时区

Instant时间戳
static Instant now();//获取当前时间的Instant对象
static Instant ofXxxx(long epochMilli);//根据（秒/毫秒/纳秒）获取Instant对象
ZonedDateTime atZone(ZoneId zone);//指定时区
boolean isXxx(Instant otherInstant);//判断系列的方法
Instant minusXxx(long millisToSubtract);//减少时间系列的方法
Instant plusXxx(long millisToSubtract);//增加时间系列的方法

ZoneDateTime 带时区的时间类
static ZoneDateTime now();//获取当前时间的ZoneDateTime对象
static ZoneDateTime ofXxxx();//获取指定时间的ZoneDateTime对象
ZoneDateTime withXxx();//修改时间系列的方法
ZoneDateTime minusXxx();//减少时间系列的方法
ZoneDateTime plusXxx();//增加时间系列的方法
```



## 包装类

```
基本类型对应的包装类，除了char对应的是Character int对应的是Integer,其余的都是对首字母进行大写
//Integer的构造
public Integer(int value)
public Integer(String s)
public static Integer valueOf(int i)
public static Integer valueOf(String s)
public static Integer valueOf(String s,int radix)//根据传入的字符串以及其进制创造Integer对象
//注意，当用静态方法构造对象时。当数据范围在-128~127以内的数字，源码已经创建好对应的对象，使用的都是同一对象

Integer i=10;
//在底层，此时还会去自动调用静态方法valueOf得到一个Integer对象啊

public static String toBinaryString(int i)//转二进制
public static String toOctalString(int i)//转八进制
public static String toHexString(int i)//转16进制
public static int parseInt(String s)//将字符串整数转成int
//细节：
//类型转换的时候，括号中的参数不能是其他，否则会报错
//parseXXX在其他包装类里也有


```

# 算法相关

```
Arrays//操作数组的工具类
public static String toString(数组)//把数组拼接成一个字符串
public static int BinarySearch(数组，查找的元素)//二分查找法查找元素
public static int[] copyOf(原数组，新数组长度)//拷贝数组
public static int[] copyOfRange(原数组，起始索引，结束索引)//拷贝数组(指定范围)
public static void fill(数组，元素)//填充数组
public static void sort(数组)按默认方式进行数组排序
public static void sort(数组，排序规则)//按指定规则对数组进行排序
Arrays.sort(arr, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o1 - o2;//升序
                //return o2 - o1;降序
            }
        });//自定义排序的写法
```



# 集合与数据结构

## Collection(单列集合的顶层集合)

```
public boolean add(E e)//把给定的对象添加到当前集合中
public void clear()//清空集合中的所有元素
public boolean remove(E e)//把给定的对象在当前集合中删除
public boolean contains(Object obj)//判断当前集合中是否有给定的对象
public boolean isEmpty()//判断当前集合是否为空
public int size()//返回集合的长度
//特点：有序，可重复，有索引，但是Collection不具有索引的功能，且只能迭代器遍历
```

## 迭代器

```
Iterator<E> iterator()//返回迭代器对象，默认指向当前集合的零索引,是Collectionn下的数据结构内部的方法
boolean hasNext()//判断当前位置是否有元素，有返回true,没有返回false
E next()//获取当前位置的元素，并将迭代器对象移向下一个位置

Iterator<Integer> i = arr.iterator();

while (i.hasNext()) {
            Integer a = i.next();
            System.out.println(a);
}
//注意，用迭代器操作时，请用迭代器的相关方法进行增加或者删除操作
```

## List(继承Collection)

```
void add(int index,E element)//在指定索引上添加元素
E remove(int index)//根据索引去删除对象，并返回被删除的元素
E set(int index,E element)//修改指定索引处的元素，并返回被修改的元素
Eget(int index)//返回指定索引处的元素
boolean remove(Object o);//根据元素删除，如果重复则删除第一个出现的元素
//支持索引，并且支持for循环遍历

```

## LinkedList

```
public void addFirst(E e)//添加到头
public void addLast(E e)//添加到尾
public E getFirst()//返回列表的第一个元素
public E getLast()//返回列表的最后一个元素
public E removeFirst()//删除并返回第一个元素
public E removeLast()//删除并返回最后一个元素
//关于并发修改异常：
//在使用迭代器或者增强for循环遍历集合时，不要使用集合add或者remove方法进行增加或者删除
```



## 泛型

1：泛型类的写法：修饰符 class 类名<E>{}

2：泛型方法：修饰符<E>返回值类型 方法名（类型 变量）

3：泛型接口：修饰符 interface 接口名<E>{}

​	注意：使用时 实现类给出具体的类型，一旦给出就确定了，或者类延续泛型，创建对象在确定

4：泛型不具备继承性，但是数据具有继承性,例如这个泛型在方法中已经确定其类型了，你传入一个泛型他的类型是前者的泛型确定的类型的子类时，两者并不相通

5：此时可以使用通配符，在<>中加入以下内容

​	?表示不确定的类型

​	? extends E 表示传递E或者E所有的子类类型

​	? super E 表示传递E或者E所有的父类类型

## 红黑树

**红黑规则**

1：每一个结点要么是红色要么是黑色

2：根结点必须是黑色

3：如果一个结点没有子节点或者父节点，则该结点相应的指针属性为nil,这些nil结点视为叶结点，每个nil叶子结点是黑色的

4：如果某一个结点是红色的，那他的子结点必须是黑色（不能出现两个红色结点相连的情况）

5：对每一个结点。从该结点到其所有后代叶结点的简单路径上，均含有相同数目的黑色结点

## Set

无序：存储顺序不一致

不重复：可以去重

无索引

三个实现类：

HashSet:无序，不重复，无索引

LinkedHashSet:有序（与插入顺序一致），不重复，无索引

TreeSet:可排序，不重复，无索引，默认从小到大

Api与Collection一致

## HashSet

关于哈希值，同一对象，在HashCode方法没有重写前，计算出来的Hashcode是不同的，重写后就会相同，可以用idea自行添加到类

## TreeSet

默认排序，只需将类继承Comparable接口，重写CompareTo方法，写法与排序方法的重写规则一致,其中this表示当前待添加的元素

第二种使用Comparator，将它的Compare方法重写，与排序方法的写法类似，其中本方法优先级最高,这个Comparator可以放到对应的Treeset构造方法进行构造，依此来定义Treeset的排序规则



## 双列集合

类似于C++的map，键值对一一对应，一个键值对叫Entry，类似C++的pair,特点键不重复，值可以重复

## map

双列集合的顶层接口

```
V put(K key,V value)//添加元素
V remove(Object key)//根据键删除键值对元素
void clear()//清空所有元素
boolean containsKey(Object key)//判断集合是否包含指定的键
boolean containsValue(Object value)//判断集合中是否包含指定的值
boolean isEmpty()//判断集合是否为空
int size()//返回集合的长度
```

添加对象时，如果键不存在，则将新的键值对添加进去，如果存在，则覆盖原有的值

```
//遍历
通过KeySet方法获取key的set
遍历这个Set，通过get方法，把键传入来获取值
Map<String,String>mp=new HashMap<>();
        mp.put("aaa","bb");
        mp.put("bbb","cc");

        Set<String>se=mp.keySet();
        for (String key : se) {
            String value=mp.get(key);
            System.out.println(key+"+"+value);
        }
       
```

```
Map<String, String> mp = new HashMap<>();
        mp.put("aaa", "bb");
        mp.put("bbb", "cc");

        Set<Map.Entry<String, String>> se = mp.entrySet();
        for (Map.Entry<String, String> en : se) {
            System.out.println(en.getKey() + " " + en.getValue());
        }
```

最后一种foreach遍历，重写接口实现



## TreeMap

按照键值进行排序的map，其余与set的逻辑类似



# 可变参数

```
public static int getSum(int... args) {
	int sum = 0;
    for (int arg : args) {
		sum += arg;
	}
	return sum;
}
//传入的参数数量不确定，外界想传几个就传几个，args作为一个数组来存这些变量，且不能写多个可变参数，如果还有其他参数，可变需要写到末尾，可变参数也可以直接传入一个数组进行使用
```





# 集合工具类Collections

```
public static <T> boolean addAll(collection<T> c,T...elements)//批量添加元素，注意只能添加单列集合
public static void shuffle(List<?> list)//打乱list集合的顺序，注意只能传list
public static <T> void sort(List<T> list)//对list进行排序
public static <T> void sort(List<T> list Comparator<T> c)//根据指定的规则进行排序
public static <T> int binarySearch(List<T> list, T key)//二分查找某个元素
public static <T> void copy(List<T> list, List<T> src)//拷贝集合中的元素
public static <T> fill(List<T> list,T obj)//使用指定的元素填充集合
public static <T> void max/min(Collection<T> coll)//根据默认的自然排序获取最大/最小值
public static <T> void swap(List<T> list,int i,int j)//交换集合中指定位置的元素
```

# 不可变集合

定义：集合中的元素不可变

在List Set Map接口中都存在静态的of方法，获取一个 不可变的集合

```
static<E> List<E> of(E...elements)
static<E> Set<E> of(E...elements)
static<K,V> Map<K,V> of(E...elements)
//注意这个集合不能添加，删除，修改
//当我们要获取一个不可变的Set集合时，要保证里面的元素绝对唯一
//Map里的of方法，参数是有上限的，最多只能传入20个参数，10个键值对
//补充
<T> T[] toArray(T[] a);//Set下的toArray方法，
//toArray方法在底层会比较集合的长度跟数组的长度
//如果集合的长度大于数组的长度，则会创建新的数组，否则不创建直接使用
//解决方法就是使用下列方法进行创建
static <K, V> Map<K, V> copyOf(Map<? extends K, ? extends V> map)
static <K, V> Map<K, V> ofEntries(Entry<? extends K, ? extends V>... entries) 
```

# Stream流

单列集合转换

```
ArrayList<String> list = new ArrayList<>();
Collections.addAll(list, "a", "b", "c");


//Stream<String> stream = list.stream();
//stream.forEach(s -> System.out.println(s));

list.stream().forEach(s-> System.out.println(s));
```

双列集合获取Stream流

```
HashMap<String,String>mp=new HashMap<>();

mp.put("aaa","111");
mp.put("bbb","222");
mp.keySet().stream().forEach(s-> System.out.println(s));

mp.entrySet().stream().forEach(s-> System.out.println(s));

```

数组获取Stream流

```
int[] arr={1,2,3,3,3,3,5,6};
Arrays.stream(arr).forEach(s-> System.out.println(s));
```

零散数据获取Stream流

```
Stream.of(1,2,3).forEach(s-> System.out.println(s));
```

```
Stream<T> filter(Predicate<? super T> predicate);//过滤
Stream<T> limit(long maxSize);//获取前几个元素
Stream<T> skip(long n);跳过前几个元素
Stream<T> distinct();//元素去重
public static <T> Stream<T> concat(Stream<? extends T> a, Stream<? extends T> b)//合并A B两个流
Stream<R> map(Function<? super T, ? extends R> mapper);//转换流中的数据类型

//注意：
//1：中间方法返回新的流，原来的只使用一次，建议只用链式编程
//2：修改Stream流中的数据不会影响原来集合或者数组中的数据
//3：filter方法的参数，用匿名内部类/lamda表达式去写，重写内部的方法，返回值true留下，false去掉
stream.filter(new Predicate<String>() {
    @Override
    public boolean test(String s) {
        return false;
    }
});

//4：map方法一样，Function里面的第一个参数为原本的数据类型，第二个为修改后的，形参s表示每一个数据，返回值表示转换之后的数据
stream.map(new Function<String, Object>() {
     @Override
     public Object apply(String s) {
         return null;
     }
});

```

```
void forEach(Consumer action)//遍历
long count()//统计
Object[] toArray();收集流中的数据并放到数组中
collect(Collector collector)//收集流中的数据并放到集合中，一般使用Collectors.toxxx,来指定集合

//方法中的参数s代表每一个数据，方法里的语句代表对数据的操作
stream.forEach(new Consumer<String>() {
    @Override
    public void accept(String s) {
                
    }
});

//toArray方法会返回Object数组，获取对应的Object数组后，用toString转换后打印

<A> A[] toArray(IntFunction<A[]> generator);//转换为指定类型的数组
 
stream.toArray(new IntFunction<? extends Object[]>() {
            @Override
            public Object[] apply(int value) {
                return new Object[value];
            }
        })
        
//注意：Infuction里面是需要转化的数组类型
//apply形参：流体中的数据个数，要跟数组长度保持一致
//apply返回值：具体类型的数组

//关于collect方法详见这里https://www.bilibili.com/video/BV1yW4y1Y7Ms?p=39&vd_source=2f1dfa0c66ab2a50d7c3ba9e2d6bf5d0

```

# 方法引用

1：引用处必须是函数接口

2：被引用的方法必须已经存在，被引用的方法形参与返回值需要跟抽象方法保持一致

3：被引用方法的功能要满足当前的需求

静态方法引用：类名::方法名

成员方法引用：对象::方法名/this::方法名/super::方法名

构造方法的引用：类名::new

**类名引用成员方法：类名::方法名**

**抽象方法形参的详解：**
**第一个参数：表示引用方法的调用者，决定了可以引用哪些类中的方法，在stream流当中，第一个参数一般表示流里的每一个数据，第二个参数往后的参数与引用方法的形参表示一致，此情况只在类名引用形参的时候需要考虑**

引用数组的构造方法 ：数据类型[]::new

关于方法引用：因为方法本省需要调用其他方法，于是采用了方法接口+匿名内部类的形式，将两个方法联系起来，后优化成lambda表达式，但本质是为了使用另一个方法的功能。

# 异常

父类：Exception

异常分为两类：编译时异常，运行时异常

编译时异常：没有继承RuntimeException的异常，直接继承于Exception，编译时就会错误提示

运行时异常：RuntimeExcetion本身和子类，编译阶段没有错误显示，运行时出现的

jvm虚拟机遇到异常会自行停止程序的运行

个人处理程序异常可以使用以下方式进行解决,这样处理异常可以保证即使出现程序异常，程序仍然可以正常运行

```java
try{
    //异常代码
}catch(异常类型){
    //处理方式
}

```

如果try catch语句没有遇到异常，则直接跳过这部分的代码，运行下面的代码

如果try catch语句遇到多个问题，建议写多个catch进行捕捉，如果捕获的多个异常中存在父子关系的话，父类一定要写在下面

其中在jdk7以后，我们可以e在一个catch中同时捕获多个异常，不同异常之间用| 隔开

如果try中异常没有被catch捕获，则jvm虚拟机强制停止运行

如果try遇到了问题，try中的其他代码不会执行

## Throwable的成员方法

| 方法名称                      | 说明                            |
| ----------------------------- | ------------------------------- |
| public String getMessage()    | 返回此throwable的详细消息字符串 |
| public String toString()      | 返回此可抛出的简短描述          |
| public void printStackTrace() | 把异常的错误信息输出在控制台    |

## 异常抛出

**throws:写在方法定义处，表示申明一个异常告诉调用者，使用本方法可能会有哪些异常，编译时异常必须要写，运行时异常可以不写**

**throw:写在方法内，结束方法时抛出异常对象，交给调用者方法中，下面的代码不在执行，**

## 自定义异常

**第一步：定义异常类**

**第二步：写继承关系**

**第三步：空参构造**

**第四步：带参构造**

**意义：为了让控制台的报错信息更加见名知意**

```
public class AgeOutOfBoundException extends RuntimeException{

    public AgeOutOfBoundException() {
    }

    public AgeOutOfBoundException(String message) {
        super(message);
    }
}
```

## finally

```
try {

} catch (IOException e) {

} finally {

}
```

**被finally控制的语句一定会执行，除非jvm退出**





# File

**File对象就表示一个路径，可以是文件的路径，也可以是文件夹的路径，这个路径可以存在，也可以不存在**

**构造方法**

| 方法名称                                 | 说明                                               |
| ---------------------------------------- | -------------------------------------------------- |
| public File(String pathname)             | 根据文件路径创建文件对象                           |
| public File(String parent, String child) | 根据父路径名字字符串和子路径名字字符串创建文件对象 |
| public File(File parent, String child)   | 根据父路径文件对象和子路径名字字符串创建文件对象   |

**成员方法**

| 方法名称                                       | 说明                                                         |
| ---------------------------------------------- | ------------------------------------------------------------ |
| public static File listRoots()                 | 列出可用的文件系统根，相当于获取所有的盘符                   |
| public String[] list()                         | 获取当前文件该路径下所有内容，获取的只是文件的名字           |
| public String[] list(FilenameFilter filter)    | 利用文件名过滤器获取当前该路径下所有的内容                   |
| public File[] listFiles()                      | 获取当前该路径所有内容，当调用者File表示的路径不存在或者是一个文件时返回null,当路径表示一个空文件夹时，数组长度为零，需要权限进行访问的文件夹，返回的结果也是null，但是隐藏文件是可以被访问的 |
| public File[] listFile(FileFilter filter)      | 利用文件名过滤器获取当前该路径下所有内容                     |
| public File[] listFiles(FilenameFilter filter) | 利用文件名过滤器获取当前该路径下所有内容                     |

**FilenameFilter是一个文件过滤器，是一个函数接口，里面有一个accept方法，方法的返回值为true，就保留，反之就不保留，其中参数1代表父级路径，参数2代表子级路径**

```java
String[] files = f.list(new FilenameFilter() {
    @Override
    public boolean accept(File dir, String name) {
        return false;
    }
});
```

```
File[] files = f.listFiles(new FileFilter() {
    @Override
    public boolean accept(File pathname) {
        return false;
    }
});
```

**判断获取相关的方法**

| 方法名称                        | 说明                                             |
| ------------------------------- | ------------------------------------------------ |
| public boolean isDirectory()    | 判断此路径名表示的File是否为文件夹               |
| public boolean isFile()         | 判断此路径名表示的File是否为文件                 |
| public boolean exist()          | 判断此路径名表示的File是否存在                   |
| public long length()            | 返回文件的大小（字节）                           |
| public String getAbsolutePath() | 返回文件的绝对路径                               |
| public String getPath()         | 返回定义文件时使用的路径                         |
| public String getName()         | 返回文件的名称，带后缀，如果是文件夹则只有文件名 |
| public String lastModified()    | 返回文件的最后修改时间（毫秒值）                 |

**创建和删除相关的方法**

| 方法名称                       | 说明                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| public boolean createNewFile() | 创建一个新的空的文件，如果当前路径所表示的文件存在，则创建成功，反之失败，如果父级路径不存在则会出现程序异常，并且本方法创建的一定是一个文件，如果路径不含文件名后缀，最后也会生成一个文件 |
| public boolean mkdir()         | 创建单级文件夹，在windows系统中路径是唯一的，如果路径存在则无法创建，并且本方法不能创建多级文件夹，只能创建单级文件夹 |
| public boolean mkdirs()        | 创建多级文件夹，本方法不仅可以创建多级文件夹，还可以创建单级文件夹 |
| public boolean delete()        | 删除文件，空文件夹，不能删除非空文件夹，不走回收站           |

# IO流

## IO流的分类

**按照流的方向：分为输入流（读取），输出流(写出)**

**按照操作文件的类型：分为字节流和字符流，字节流可以操作所有类型的文件，字符流只能操作纯文本文件**

**纯文本文件：用windows自带的记事本能打开并且能读懂的文件**

## 字节流

**字节流分为InputStrean和OutputStream，这两个下面又有FileInputStream和FileOutputStream**

**FileOutputStream：操作本地文件字节输出流，可以把程序中的数据写到本地文件**

**使用步骤：创建对象，写数据，释放资源**

**样例代码**

```
public static void main(String[] args) throws IOException {
    /*关于创建字节输出流对象
        1：参数是字符串表示的路径或者File对象都可以
        2：如果文件不存在会创建一个新的文件，但是要保证父级路径是存在的
        3：如果文件已经存在，则会清空文件
     */
    
    FileOutputStream fos = new FileOutputStream("a.txt");

    /*关于写数据：
        1：write方法的参数整数，但是实际上写的是整数对应的ASCII码对应的字符
     */
    
    fos.write(97);
    
    
    /*释放资源
        解除资源的占用，是必要操作
     */

    fos.close();

}
```

**FileOutputStream写数据的三种方式**

| 方法名称                               | 说明                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| void write(int b)                      | 一次写一个数据                                               |
| void write(byte[] b)                   | 一次写一个字节数组的数据                                     |
| void write(byte[] b, int off, int len) | 一次写一个字节数组的部分数据，off代表起始索引，len代表从起始索引开始写几个数据 |

**注意：对于String类型的字符串，可以通过getBytes()方法获取byte数组，然后进行写入，如果需要换行，可以读取换行符\n,来写入**

**默认创建FileOutputStream是先清空文件，如果不要清空文件，修改构造函数的第二个变量为true即可**

```
FileOutputStream fos = new FileOutputStream("a.txt",true);
```

**FileInputStream:操作本地文件的字节流，可以把本地文件的数据读取到程序中**

**样例代码**

```java
public static void main(String[] args) throws IOException {

    /*创建字节输入流对象
        1：如果文件不存在，直接报错     
     */
     
    FileInputStream fis = new FileInputStream("a.txt");

    /*读取数据
        1：一次读一个字节，读出来的是ASCII上对应的数字
        2：读到文件末尾，read方法返回-1
     */
    int b = fis.read();
    System.out.println((char)b);

    fis.close();
}
```

**循环读取**

```
int b;
while ((b = fis.read()) != -1) {
    System.out.println((char) b);
}
```

**FileInputStream一次读取多个字节**

| 方法名称                       | 说明                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| public int read()              | 一次读取一个数据                                             |
| public int read(byte[] buffer) | 一次读取一个字节数组的数据，将读取结果存入byte数组，返回的是读取的字节数，没有读到东西返回-1 |

**一次读取多个字节进行文件拷贝**

```
public static void main(String[] args) throws IOException {
    FileInputStream fis =new FileInputStream("a.txt");

    FileOutputStream fos = new FileOutputStream("b.txt");

    byte[] bytes = new byte[3];
    int len;

    while((len = fis.read(bytes)) != -1){
        fos.write(bytes);
    }
    
    fos.close();
    fis.close();
}
```

## 字符集

**GBK中，一个英文字母占一个字节，二进制第一位是0，英文上完全兼容ASCII，一个中文汉字占2个字节，二进制第一位是1**

**UTF-16:用2-4个字节保存**

**UTF-32：固定使用4个字节保存**

**UTF-8：用1-4个字节保存，其中英文是一个字节，中午汉字是3个字节**

**以下每种字节保存下，前缀满足的要求**

``` 
0xxxxxxx
110xxxxx 10xxxxxx
1110xxxx 10xxxxxx 10xxxxxx
11110xxx 10xxxxxx 10xxxxxx 10xxxxxx
```

**注意：UTF-8不是字符集是unicode字符集的一种编码**

**java中的编码方法**

| String类中的方法                           | 说明                               |
| ------------------------------------------ | ---------------------------------- |
| public byte[] getBytes()                   | 使用默认方式进行编码,idea默认UTF-8 |
| public byte[] getBytes(String charsetName) | 使用指定方式编码                   |

**java中的解码方法**

| String类中的方法                          | 说明                               |
| ----------------------------------------- | ---------------------------------- |
| String (byte[] bytes)                     | 使用默认方式进行解码,idea默认UTF-8 |
| String (byte[] bytes, String charsetName) | 使用指定方式解码                   |

## 字符流

**字符流 = 字节流 + 字符集**

**特点：一次读一个字节，遇到中文时一次读多个字节**

**字符流分为Reader输入流，writer输出流，下面又分为FileReader,FileWriter**

**FileReader**

| 构造方法                                            | 说明                                                         |
| --------------------------------------------------- | ------------------------------------------------------------ |
| public FileReader(File file)                        | 创建字符输入流关联本地文件                                   |
| public FileReader(String pathname)                  | 创建字符输入流关联本地文件                                   |
| public FileReader(File file, Charset charset)       | 创建字符输入流关联本地文件，根据指定的编码进行创建，Charset可以使用Charset.forName("GBK")进行指定 |
| public FileReader(String fileName, Charset charset) | 创建字符输入流关联本地文件，根据指定的编码进行创建，Charset可以使用Charset.forName("GBK")进行指定 |

**注意：文件不存在会直接报错**

| 成员方法                       | 说明                          |
| ------------------------------ | ----------------------------- |
| public int read()              | 读取数据，读到末尾返回-1      |
| public int read(char[] buffer) | 读取多个数据，读到末尾返回 -1 |
| public int close()             | 释放资源/关流                 |

**样例代码**

```
public class FileDemo3 {
    public static void main(String[] args) throws IOException {
        FileReader fr =new FileReader("a.txt");

        int ch;
        while((ch = fr.read()) != -1){
            System.out.println((char)ch);
        }

        fr.close();
    }
}
```

**FileWriter**

| 构造方法                                                     | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| public FileWriter(File file)                                 | 创建字符输出流关联本地文件                                   |
| public FileWriter(String pathname)                           | 创建字符输出流关联本地文件                                   |
| public FileWriter(File file, boolean append)                 | 创建字符输出流关联本地文件，续写                             |
| public FileWriter(String pathname, boolean append)           | 创建字符输出流关联本地文件，续写                             |
| public FileWriter(File file, Charset charset)                | 创建字符输出流关联本地文件，根据指定的编码进行创建，Charset可以使用Charset.forName("GBK")进行指定 |
| public FileWriter(File file, Charset charset, boolean append) | 创建字符输出流关联本地文件，续写,根据指定的编码进行创建，Charset可以使用Charset.forName("GBK")进行指定 |
| public FileWriter(String fileName, Charset charset)          | 创建字符输出流关联本地文件，根据指定的编码进行创建，Charset可以使用Charset.forName("GBK")进行指定 |
| public FileWriter(String fileName, Charset charset, boolean append) | 创建字符输出流关联本地文件，续写，根据指定的编码进行创建，Charset可以使用Charset.forName("GBK")进行指定 |

**注意：如果文件不存在，则会创建一个文件**

| 成员方法                                  | 说明                   |
| ----------------------------------------- | ---------------------- |
| void write(int c)                         | 写出一个字符           |
| void write(String str)                    | 写出一个字符串         |
| void write(string str, int off, int len)  | 写出一个字符串的一部分 |
| void write(char[] cbuf)                   | 写出一个字符数组       |
| void write(char[] cbuf, int off, int len) | 写出字符数组的一部分   |

**字符流原理解析**

**创建字符输入流对象时，底层关联文件，并创建缓冲区（长度为8192的字节数组）**

**读取数据时：底层会判断缓冲区是否有数据可读，如果缓冲区没有数据，就从文件中获取数据，装到缓冲区，每次尽可能装满，如果文件中也没有数据了，则返回-1，如果缓冲区有数据，就从缓冲区读取**

**在输出流中，执行完write方法后，内容先被存入缓冲区，只有当缓冲区满了之后，或者使用flush方法或者close方法，才会将缓冲区的数据写入到目的地上**

| 成员方法            | 说明                                                         |
| ------------------- | ------------------------------------------------------------ |
| public void flush() | 将缓冲区的数据，刷新到本地的文件上，但是还可以往文件上写数据，只是缓冲区被刷新了 |
| public void close() | 释放资源/关流                                                |

## 缓冲流

**字节缓冲流**

| 构造方法                                     | 说明                               |
| -------------------------------------------- | ---------------------------------- |
| public BufferedInputStream(InputStream is)   | 把基本流包装成高级流，提高读写性能 |
| public BufferedOutputStream(OutputStream os) | 把基本流包装成高级流，提高读写性能 |

**原理：底层自带长度为8192的缓冲区提高性能**

**注意：使用缓冲流同基本流，并且内部会自动关闭基本流，因此只需要调用缓冲流的close方法便可实现流的关闭，读写方法与字节流一致**

**字符缓冲流**

| 构造方法                        | 说明               |
| ------------------------------- | ------------------ |
| piblic BufferedReader(Reader r) | 把基本流变成高级流 |
| public BufferedWriter(Writer w) | 把基本流变成高级流 |

| BufferReader特有方法     | 说明                       |
| ------------------------ | -------------------------- |
| public String readline() | 读取一行数据，遇到换行停止 |

| BufferWriter特有方法    | 说明                                             |
| ----------------------- | ------------------------------------------------ |
| public String newline() | 跨平台换行，使用这个方法可以给文件写一个换行进入 |

**BufferedReader样例代码**

```
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new FileReader("a.txt"));
    String line;
    while((line = br.readLine()) != null){
        System.out.println(line);
    }

    br.close();
}
```

**使用原则，什么时候用，什么时候创建，什么时候不用，什么时候关闭**

## 转换流

**作用：是字符流和字节流之间的桥梁，原始版本是InputStreamReader和OutputStreamReader，他们继承于Reader和Writer**

| 构造方法                                                     | 说明                   |
| ------------------------------------------------------------ | ---------------------- |
| public InputStreamReader(InputStream in)                     | 创建缓冲流             |
| public InputStreamReader(InputStream in, String charsetName) | 创建缓冲流，并指定编码 |
| public OutputStreamWriter(OutputStream out, String charsetName) | 创建缓冲流，并指定编码 |
| public OutputStreamWriter(OutputStream out)                  | 创建缓冲流             |

## 序列化流

**又名：对象操作输出流，可以把java的对象写道本地文件中**

| 构造方法                                    | 说明                 |
| ------------------------------------------- | -------------------- |
| public ObjectOutputStream(OutputStream out) | 把基本流包装成高级流 |

| 成员方法                                  | 说明                     |
| ----------------------------------------- | ------------------------ |
| public final void writeObject(Object obj) | 把对象序列化写到文件中去 |

**样例代码**

```
public static void main(String[] args) throws IOException {

    GirlFriend girlFriend = new GirlFriend("nnn", 18);

    ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("a.txt"));
    
    oos.writeObject(girlFriend);
    
    oos.close();

}
```

**注意：使用对象输出流将对象保存到文件时会出现NotSerializableException异常，此时需要让输出的对象即JavaBean继承一个接口Serializable**

## 反序列化流

| 构造方法                                  | 说明               |
| ----------------------------------------- | ------------------ |
| public ObjectInputStream(InputStream out) | 把基本流变成高级流 |

| 成员方法                 | 说明                                       |
| ------------------------ | ------------------------------------------ |
| public Object readObject | 把序列化到本地文件中的对象，读取到程序中来 |

**样例代码**

```
public static void main(String[] args) throws IOException {

    ObjectInputStream ois = new ObjectInputStream(new FileInputStream(a.txt));
    
    Object o = ois.readObject();
    
    ois.close();


}
```

**在使用反序列化流的时候存在一个问题，就是当你修改JavaBean类的信息后，文件中原来的JavaBean就读取不出来了，这是因为在底层，会根据这个类的信息自动生成一个版本号，一旦类的信息发生变化，版本号就会变，就会无法识别，为了解决这个问题我们可以Serializable接口下的一个变量，来定义它的版本号，当版本号一致，就不会报错，**

```
private static final long serialVersionUID = -119720261244518077L;
```

**当然如果哪个变量你不想序列化到本地，可以用transient关键字表示**

```
private transient Integer age;
```

**关于多个对象的序列化操作，建立先使用list进行保存，在将这个list进行序列化**



## 打印流

**分类：字节打印流PrintStream,字符打印流Printwriter**

**特点：只操作文件目的地，不操作数据，并且可以将数据原样写出**

**字节打印流**

| 构造方法                                                     | 说明                         |
| ------------------------------------------------------------ | ---------------------------- |
| public PrintStream(OutputStream/File/String)                 | 关联字节输出流/文件/文件路径 |
| public PrintStream()String pathName, Charset charset)        | 指定字符编码                 |
| public PrintStream(outputStream out, boolean autoFlush)      | 自动刷新                     |
| public PrintStream(OutputStream out, boolean autoFlush, String encording) | 指定字符编码并自动刷新       |

| 成员方法                                         | 说明                                                  |
| ------------------------------------------------ | ----------------------------------------------------- |
| public void write(int b)                         | 常规方法：规则跟之前一样，将这个ASCII码对应的字节打出 |
| public void println(Xxx xx)                      | 特有方法：打印任意数据，自动刷新，自动换行            |
| public void print(Xxx xx)                        | 特有方法：打印任意数据，不换行                        |
| public void printf(String format, Object.. args) | 特有方法：带着占位符的打印语句，不换行，占位符同C语言 |

**字节打印流，底层没有缓冲区，开不开刷新都一样**

**字符打印流**

| 构造方法                                                     | 说明                         |
| ------------------------------------------------------------ | ---------------------------- |
| public PrintWriter(Write/File/String)                        | 关联字节输出流/文件/文件路径 |
| public PrintWriter(String fileName, Charset charset)         | 指定字符编码                 |
| public PrintWriter(Write w, Boolean autoFlush)               | 自动刷新                     |
| public PrintWriter(OutputStream out, boolean autoFlush, Charset charset) | 指定字符编码并自动刷新       |

| 成员方法                                          | 说明                                        |
| ------------------------------------------------- | ------------------------------------------- |
| public void write(...)                            | 规则跟之前一样，打印对应的字节或者字符串    |
| public void println(Xxx xx)                       | 特有方法：打印任意类型的数据并且换行        |
| public void print(Xxx xx)                         | 特有方法：打印任意类型的数据，不换行        |
| public void printf(String format, Object... args) | 特有方法：带有占位符的打印语句，效果同C语言 |

**字符打印流底层有缓冲区，想要自动刷新需要开启**

## 解压缩流

**解压的本质：把压缩包里数据读取出来，在按照层级拷贝到对应的目录**

```Java
public static void unzip(File src,File dest) throws IOException {
    //解压的本质：把压缩包里面的每一个文件或者文件夹读取出来，按照层级拷贝到目的地当中
    //创建一个解压缩流用来读取压缩包中的数据
    ZipInputStream zip = new ZipInputStream(new FileInputStream(src));
    //要先获取到压缩包里面的每一个zipentry对象
    //表示当前在压缩包中获取到的文件或者文件夹
    ZipEntry entry;
    while((entry = zip.getNextEntry()) != null){
        System.out.println(entry);
        if(entry.isDirectory()){
            //文件夹：需要在目的地dest处创建一个同样的文件夹
            File file = new File(dest,entry.toString());
            file.mkdirs();
        }else{
            //文件：需要读取到压缩包中的文件，并把他存放到目的地dest文件夹中（按照层级目录进行存放）
            FileOutputStream fos = new FileOutputStream(new File(dest,entry.toString()));
            int b;
            while((b = zip.read()) != -1){
                //写到目的地
                fos.write(b);
            }
            fos.close();
            //表示在压缩包中的一个文件处理完毕了。
            zip.closeEntry();
        }
    }

    zip.close();

}
```

## 压缩流

```java
//压缩单个文件
public static void toZip(File src,File dest) throws IOException {
    //1.创建压缩流关联压缩包
    ZipOutputStream zos = new ZipOutputStream(new FileOutputStream(new File(dest,"a.zip")));
    //2.创建ZipEntry对象，表示压缩包里面的每一个文件和文件夹
    //参数：压缩包里面的路径
    ZipEntry entry = new ZipEntry("aaa\\bbb\\a.txt");
    //3.把ZipEntry对象放到压缩包当中
    zos.putNextEntry(entry);
    //4.把src文件中的数据写到压缩包当中
    FileInputStream fis = new FileInputStream(src);
    int b;
    while((b = fis.read()) != -1){
        zos.write(b);
    }
    zos.closeEntry();
    zos.close();
}
```

```java
//压缩整个文件夹
public static void toZip(File src,ZipOutputStream zos,String name) throws IOException {
    //1.进入src文件夹
    File[] files = src.listFiles();
    //2.遍历数组
    for (File file : files) {
        if(file.isFile()){
            //3.判断-文件，变成ZipEntry对象，放入到压缩包当中
            ZipEntry entry = new ZipEntry(name + "\\" + file.getName());//aaa\\no1\\a.txt
            zos.putNextEntry(entry);
            //读取文件中的数据，写到压缩包
            FileInputStream fis = new FileInputStream(file);
            int b;
            while((b = fis.read()) != -1){
                zos.write(b);
            }
            fis.close();
            zos.closeEntry();
        }else{
            //4.判断-文件夹，递归
            toZip(file,zos,name + "\\" + file.getName());
            //     no1            aaa   \\   no1
        }
    }
}
```

## Commons-io

**Commons-io时Apache开源基金组织提供的一组有关IO操作的工具包**

**作用：提高IO的开发效率**

**代码示例：**

```java
public class CommonsIODemo1 {
    public static void main(String[] args) throws IOException {
        /*
          FileUtils类
                static void copyFile(File srcFile, File destFile)                   复制文件
                static void copyDirectory(File srcDir, File destDir)                复制文件夹
                static void copyDirectoryToDirectory(File srcDir, File destDir)     复制文件夹
                static void deleteDirectory(File directory)                         删除文件夹
                static void cleanDirectory(File directory)                          清空文件夹
                static String readFileToString(File file, Charset encoding)         读取文件中的数据变成成字符串
                static void write(File file, CharSequence data, String encoding)    写出数据

            IOUtils类
                public static int copy(InputStream input, OutputStream output)      复制文件
                public static int copyLarge(Reader input, Writer output)            复制大文件
                public static String readLines(Reader input)                        读取数据
                public static void write(String data, OutputStream output)          写出数据
         */


        /* File src = new File("myio\\a.txt");
        File dest = new File("myio\\copy.txt");
        FileUtils.copyFile(src,dest);*/


        /*File src = new File("D:\\aaa");
        File dest = new File("D:\\bbb");
        FileUtils.copyDirectoryToDirectory(src,dest);*/

        /*File src = new File("D:\\bbb");
        FileUtils.cleanDirectory(src);*/



    }
}

```

## Hutool

**代码示例：**

```java
public class Test1 {
    public static void main(String[] args) {
    /*
        FileUtil类:
                file：根据参数创建一个file对象
                touch：根据参数创建文件

                writeLines：把集合中的数据写出到文件中，覆盖模式。
                appendLines：把集合中的数据写出到文件中，续写模式。
                readLines：指定字符编码，把文件中的数据，读到集合中。
                readUtf8Lines：按照UTF-8的形式，把文件中的数据，读到集合中

                copy：拷贝文件或者文件夹
    */


       /* File file1 = FileUtil.file("D:\\", "aaa", "bbb", "a.txt");
        System.out.println(file1);//D:\aaa\bbb\a.txt

        File touch = FileUtil.touch(file1);
        System.out.println(touch);


        ArrayList<String> list = new ArrayList<>();
        list.add("aaa");
        list.add("aaa");
        list.add("aaa");

        File file2 = FileUtil.writeLines(list, "D:\\a.txt", "UTF-8");
        System.out.println(file2);*/

      /*  ArrayList<String> list = new ArrayList<>();
        list.add("aaa");
        list.add("aaa");
        list.add("aaa");
        File file3 = FileUtil.appendLines(list, "D:\\a.txt", "UTF-8");
        System.out.println(file3);*/
        List<String> list = FileUtil.readLines("D:\\a.txt", "UTF-8");
        System.out.println(list);
    }
}
```

## 配置文件

**properties是一个双列集合，拥有map集合的所有特点**

```
Properties prop = new Properties();
```

**基础方法与双列集合保持一致**

**把集合中的数据以键值对的形式写道本地配置文件中去**

```
FileOutputStream fos = new FileOutputStream("path");
prop.store(fos,"xxx");
fos.close();
```

```
public void store(OutputStream out, String comments)//后面的参数表示文件的注释信息
```

**也可以从文件中读取相应的数据，读取到对应的properties集合中去**

```
FileInputStream fis = new FileInputStream("path");
prop.load(fis);
fis.close();
```

```
public synchronized void load(InputStream inStream)
```





# 多线程

## 相关概念

**线程：线程是系统能够进行运算调度的最小单位，他被包含在进程之中，是进程的实际运算单位，也可以理解为软件中相互独立，可以同时运行的功能**

**进程：进程是程序的基本执行实体**
**并发：在同一时刻，有多个指令在单个CPU上交替执行**

**并行：在同一时刻，有多个指令在多个CPU上同时执行**

**实现方式：继承Thread类的方式进行实现，实现Runnable接口的方式实现，利用Callable接口和Future接口的方式实现**

**线程的执行遵循抢占式调度，即在不设置优先级的情况下线程的执行具有随机性**

**三种实现方式的对比**

| 实现             | 优点                                                         | 缺点                                     |
| ---------------- | ------------------------------------------------------------ | ---------------------------------------- |
| 继承Thread类     | 编程比较简单，可以直接使用Thread类的方法                     | 可扩展性较差，不能在继承其他的类         |
| 实现Runnable接口 | 扩展性较强，实现该接口的同时还可以继承其他的类               | 编程较为复杂，不能直接使用Thread类的方法 |
| 实现Callable接口 | 扩展性较强，实现该接口的同时还可以继承其他的类，并且可以获取实现结果 | 编程较为复杂，不能直接使用Thread类的方法 |

## Thread

**样例代码**

```java
public class MyThread extends Thread{
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println(getName() + "Hello world");
        }
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();

        t1.setName("线程1");
        t2.setName("线程2");

        t1.start();
        t2.start();
    }
}
```

**常用方法**

| 方法名称                        | 说明                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| String getName()                | 返回此线程的名称                                             |
| void setName()                  | 设置线程的名字(构造方法也可以设置名字)，没有设置名字，线程有默认名字，格式：Thread-(x序号，从零开始) |
| static Thread currentThread()   | 获取当前线程的对象，当jvm虚拟机启动之后，会自动的启动多条线程，其中有一条就叫main，所用就是调用main方法，并执行里面的代码，，当你在main方法里调用本方法时获取的线程就是main线程 |
| static void sleep(long time)    | 让线程休眠指定的时间，方法的参数就是睡眠时间，单位为毫秒，时间到了，自动醒来 |
| setPriority(int newPriority)    | 设置线程的优先级，这个优先级可以是在1-10的范围内的任何整数，数值越大，优先级越高，默认值是5，而且也不是绝对，优先级越高并不代表一定就能先执行完，只是有更高的概率先执行完代码 |
| final int getPriority()         | 获取线程的优先级                                             |
| final void setDemon(boolean on) | 设置为守护线程，当其他的非守护线程执行完毕，守护线程会陆续结束，这里的结束不是等代码运行完结束，而是运行个几下直接强制结束，非正常结束 |
| public static void yield()      | 出让线程/礼让线程，在线程的run方法里面调用本方法，可以使得线程的执行变得相对均匀 |
| public final void join()        | 插入线程/插队线程，可以把这个线程插队到另一个线程之前，只有这个插入的线程执行完，才会在执行其他的线程 |

## Runnable

**样例代码**

```java
public class MyRunnable implements Runnable{

    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println(Thread.currentThread().getName() + "Hello world");
        }
    }
}
```



```java
public class Main {
    public static void main(String[] args) {
        MyRunnable r1 = new MyRunnable();

        Thread t1 = new Thread(r1);
        Thread t2 = new Thread(r1);

        t1.setName("线程1");
        t2.setName("线程2");

        t1.start();
        t2.start();
    }
}
```



## Callable和Future

**样例代码**

```java
public class MyCallable implements Callable<Integer> {
    @Override
    public Integer call() throws Exception {
        int sum = 0;
        for (int i = 0; i < 100; i++) {
            sum += i;
        }
        return sum;
    }
}
```



```java
public class Main {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        //Callable实现可以获取运行结果
        MyCallable m1 = new MyCallable();

        FutureTask<Integer> f1 = new FutureTask<Integer>(m1);


        Thread t1 = new Thread(f1);

        t1.start();

        //获取运行结果
        int result = f1.get();
        System.out.println(result);

    }
}
```



## 线程的生命周期

**新建：创建线程对象**

**就绪：创建完成后，通过调用start方法，进行就绪状态，此时有执行资格，没有执行权，意思线程可以抢cpu执行权，但是还没抢到，所以没办法执行**

**运行：就绪之后，抢到cpu的执行权，有执行资格，有执行权，如果执行权被抢走，就会回到就绪状态**

**死亡：运行之后，run方法执行完毕，线程死亡，变成垃圾**

**阻塞等待：在运行之后，因为sleep方法获取其他阻塞方法，导致线程进入阻塞状态，此时线程没有执行资格，也没有执行权，阻塞结束后又会进入就绪状态**

## 线程的安全问题

**引例**

```
public class MyThread extends Thread {
    private static int ticket = 0;

    @Override
    public void run() {
        while (true) {
            if (ticket < 100){
                ticket++;
                System.out.println("在卖第" + ticket + "张票");
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }
            } else {
                break;
            }

        }
    }
}
```

**在创建多个上述线程，并允许后我们会发现程序出现了一些问题，例如相同的票出现了多次，出现了超出范围的票，（这个问题类似于mysql添加事务后会出现的问题）原因是因为线程的执行具有随机性**



## 锁

**解决方案：利用同步代码块把操作共享的数据锁起来**

```
synchronized (锁) {
	操作共享数据的代码
}
```

**特点1：开始时锁默认打开，有一个线程进入，锁自动关闭**

**特点2：里面的代码执行完毕，线程处理，锁自动打开**

**样例代码**

```
public class MyThread extends Thread {
	//加上static关键字之后就能保证这个变量是唯一的，即便创建了多个该类的对象，用的都是同一个变量
    private static int ticket = 0;

    //锁对象可以是任意的对象，只要是个对象就行，这里使用Object，final可加可不加
    static final Object obj = new Object();
    //这里的锁对象一般使用MyThread.class，这个是当前类的字节码文件，是唯一的

    @Override
    public void run() {
        while (true) {
             synchronized (obj){
                if (ticket < 100) {
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        throw new RuntimeException(e);
                    }
                    ticket++;
                    System.out.println("在卖第" + ticket + "张票");
                } else {
                    break;
                }
            }

        }
    }
}
```

**同步方法**

格式：`修饰符 synchronized 返回值类型 方法名(方法参数){..} `

**特点1：同步方法是锁住方法里面的所有代码**

**特点2：锁对象不能指定，有默认的锁对象，方法非静态就是this,方法静态就是当前类的字节码对象**

**样例代码**

```
public class MyRunnable implements Runnable {

    private int ticket = 0;

    @Override
    public void run() {
        while (true) {
            if (!sell()) break;
        }
    }

    private synchronized boolean sell() {
        if (ticket == 100) {
            return false;
        } else {
            ticket++;
            System.out.println(Thread.currentThread().getName() + "在卖第" + ticket + "张票");
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
            return true;
        }
    }
}
```

**因为MyRunnable对象我只创建一次，所以锁对象是唯一的**

**字符串拼接中，有StringBuilder和StringBuffer,区别在于后者的线程更为安全，有加锁**

## Lock锁

**lock实现提供比使用synchornized方法和语句可以获得更广泛的锁定操作，比如void lock()获得锁，void unlock()释放锁**

**需注意lock是接口不能直接实例化，这里采用它的实现类ReentrantLock来实例化**

```
public class MyThread extends Thread {
    private static int ticket = 0;

    //锁对象可以是任意的对象，只要是个对象就行，这里使用Object
    static final Object obj = new Object();

    static Lock lock = new ReentrantLock();

    @Override
    public void run() {
        while (true) {
            lock.lock();
            try {
                if (ticket < 100) {
                    Thread.sleep(100);
                    ticket++;
                    System.out.println("在卖第" + ticket + "张票");
                } else {
                    break;
                }

            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            } finally {
                lock.unlock();
            }
        }
    }
}
```

## 死锁

**概述**

**线程死锁是指由于两个或者多个线程互相持有对方所需要的资源，导致这些线程处于等待状态，无法前往执行**

**什么情况下会产生死锁**

​	**资源有限**

​	**同步嵌套**



**样例代码**

```
public class Demo {
    public static void main(String[] args) {
        Object objA = new Object();
        Object objB = new Object();

        new Thread(()->{
            while(true){
                synchronized (objA){
                    //线程一
                    synchronized (objB){
                        System.out.println("小康同学正在走路");
                    }
                }
            }
        }).start();

        new Thread(()->{
            while(true){
                synchronized (objB){
                    //线程二
                    synchronized (objA){
                        System.out.println("小薇同学正在走路");
                    }
                }
            }
        }).start();
    }
}
```

## 等待唤醒机制

**概述**

**生产者消费者模式是一个十分经典的多线程协作的模式，弄懂生产者消费者问题能够让我们对多线程编程的理解更加深刻。**

**所谓生产者消费者问题，实际上主要是包含了两类线程：**

​	**一类是生产者线程用于生产数据**

​	**一类是消费者线程用于消费数据**

**为了解耦生产者和消费者的关系，通常会采用共享的数据区域，就像是一个仓库**

**生产者生产数据之后直接放置在共享数据区中，并不需要关心消费者的行为**

**消费者只需要从共享数据区中去获取数据，并不需要关心生产者的行为**

**Object类的等待和唤醒方法**

| 方法名           | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| void wait()      | 导致当前线程等待，直到另一个线程调用该对象的 notify()方法或 notifyAll()方法,哪个线程调用该方法哪个线程跟锁绑定 |
| void notify()    | 唤醒正在等待对象监视器的单个线程                             |
| void notifyAll() | 唤醒正在等待对象监视器的所有线程                             |

**案例需求**

**桌子类(Desk)：定义表示包子数量的变量,定义锁对象变量,定义标记桌子上有无包子的变量**

**生产者类(Cooker)：实现Runnable接口，重写run()方法，设置线程任务**

**1.判断是否有包子,决定当前线程是否执行**

**2.如果有包子,就进入等待状态,如果没有包子,继续执行,生产包子**

**3.生产包子之后,更新桌子上包子状态,唤醒消费者消费包子**

**消费者类(Foodie)：实现Runnable接口，重写run()方法，设置线程任务**

**1.判断是否有包子,决定当前线程是否执行**

**2.如果没有包子,就进入等待状态,如果有包子,就消费包子**

**3.消费包子后,更新桌子上包子状态,唤醒生产者生产包子**

**测试类(Demo)：里面有main方法，main方法中的代码步骤如下**

**创建生产者线程和消费者线程对象**

**分别开启两个线程**

```java
public class Desk {

    //定义一个标记
    //true 就表示桌子上有汉堡包的,此时允许吃货执行
    //false 就表示桌子上没有汉堡包的,此时允许厨师执行
    public static boolean flag = false;
    
    //汉堡包的总数量
    public static int count = 10;
    
    //锁对象
    public static final Object lock = new Object();

}

public class Cooker extends Thread {
//    生产者步骤：
//            1，判断桌子上是否有汉堡包
//    如果有就等待，如果没有才生产。
//            2，把汉堡包放在桌子上。
//            3，叫醒等待的消费者开吃。
    @Override
    public void run() {
        while(true){
            synchronized (Desk.lock){
                if(Desk.count == 0){
                    break;
                }else{
                    if(!Desk.flag){
                        //生产
                        System.out.println("厨师正在生产汉堡包");
                        Desk.flag = true;
                        Desk.lock.notifyAll();
                    }else{
                        try {
                            Desk.lock.wait();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                }
            }
        }
    }
}

public class Foodie extends Thread {
    @Override
    public void run() {
//        1，判断桌子上是否有汉堡包。
//        2，如果没有就等待。
//        3，如果有就开吃
//        4，吃完之后，桌子上的汉堡包就没有了
//                叫醒等待的生产者继续生产
//        汉堡包的总数量减一

        //套路:
            //1. while(true)死循环
            //2. synchronized 锁,锁对象要唯一
            //3. 判断,共享数据是否结束. 结束
            //4. 判断,共享数据是否结束. 没有结束
        while(true){
            synchronized (Desk.lock){
                if(Desk.count == 0){
                    break;
                }else{
                    if(Desk.flag){
                        //有
                        System.out.println("吃货在吃汉堡包");
                        Desk.flag = false;
                        Desk.lock.notifyAll();
                        Desk.count--;
                    }else{
                        //没有就等待
                        //使用什么对象当做锁,那么就必须用这个对象去调用等待和唤醒的方法.
                        try {
                            Desk.lock.wait();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                }
            }
        }
    
    }

}

public class Demo {
    public static void main(String[] args) {
        /*消费者步骤：
        1，判断桌子上是否有汉堡包。
        2，如果没有就等待。
        3，如果有就开吃
        4，吃完之后，桌子上的汉堡包就没有了
                叫醒等待的生产者继续生产
        汉堡包的总数量减一*/

        /*生产者步骤：
        1，判断桌子上是否有汉堡包
        如果有就等待，如果没有才生产。
        2，把汉堡包放在桌子上。
        3，叫醒等待的消费者开吃。*/
    
        Foodie f = new Foodie();
        Cooker c = new Cooker();
    
        f.start();
        c.start();
    
    }

}
```

## 阻塞队列

**阻塞队列继承结构**

**iterable-->Collection-->Queue-->BlockingQueue-->(ArrayBlockingQueue.LinkedBlockingQueue)**

**常见BlockingQueue:**

**ArrayBlockingQueue: 底层是数组,有界,需注意在构造该阻塞队列时，构造函数需要传入队列的长度**

**LinkedBlockingQueue: 底层是链表,无界.但不是真正的无界,最大为int的最大值**

**BlockingQueue的核心方法:**

| 成员方法                                           | 说明                              |
| -------------------------------------------------- | --------------------------------- |
| void put(E e) throws InterruptedException//E是泛型 | 将参数放入队列,如果放不进去会阻塞 |
| E take() throws InterruptedException;//E是泛型     | 取出第一个数据,取不到会阻塞       |

**注意：阻塞队列在底层实现的时候自带锁**

**代码实现**

```

public class Foodie extends Thread {
    ArrayBlockingQueue<String> queue;

    public Foodie(ArrayBlockingQueue<String> queue) {
        this.queue = queue;
    }

    @Override
    public void run() {
        while(true){
            try {
                String food = queue.take();
                System.out.println("吃货吃了面条");
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
        }
    }
}


public class Cooker extends Thread {

    ArrayBlockingQueue<String> queue;

    public Cooker(ArrayBlockingQueue<String> queue) {
        this.queue = queue;
    }


    @Override
    public void run() {
        while (true) {
            try {
                //厨师要做的就是不断把面条放进阻塞队列中
                queue.put("面条");
                System.out.println("厨师放了一碗面条");
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
        }
    }
}



public class Main {
    public static void main(String[] args) {
        ArrayBlockingQueue<String> queue = new ArrayBlockingQueue<>(5);

        Cooker c =new Cooker(queue);
        Foodie f = new Foodie(queue);

        c.start();
        f.start();
    }
}
```

## 线程的状态

**新建状态（NEW）:创建线程状态**

**就绪状态（RUNNABLE）:start方法**

**阻塞状态（BLOCKED）:无法获得锁对象**

**等待状态（WAITED）:wait方法**

**计时等待（SLEEPTIMED WAITED）:sleep方法**

**结束状态（TERMINATED）:全部代码运行完毕**



## 线程池

**步骤：创建线程池，提交任务，所有的任务执行完毕，关闭线程池**

**线程池工具类：Excutors**

| 方法名称                                                     | 说明                     |
| ------------------------------------------------------------ | ------------------------ |
| public static ExcutorService newCachedThreadPool()           | 创建一个没有上线的线程池 |
| public static ExcutorService new FicedThreadPool(int nThread) | 创建有上限的线程池       |

**样例代码**

```
public class Main {
    public static void main(String[] args) throws InterruptedException {
        //获取线程池的对象
        ExecutorService pool = Executors.newCachedThreadPool();

        //提交任务,此处的MyRunnable是Runnable的实现类
        pool.submit(new MyRunnable());
        pool.submit(new MyRunnable());

        //销毁线程池
        //pool.shutdown();

    }
}
```

**此处使用有上限的线程池，即使你提交了多个任务，里面依旧只有三个线程在执行**

```
public class Main {
    public static void main(String[] args) throws InterruptedException {
        //获取线程池的对象
        ExecutorService pool = Executors.newFixedThreadPool(3);

        //提交任务,此处的MyRunnable是Runnable的实现类
        pool.submit(new MyRunnable());
        pool.submit(new MyRunnable());
        pool.submit(new MyRunnable());
        pool.submit(new MyRunnable());

        //销毁线程池
        //pool.shutdown();

    }
}
```

**核心原理**

**1：创建一个线程池，池子是空的**

**2：提交任务时，池子会创建新的线程对象，任务执行完毕时，线程还给池子，下回再次提交任务时，不需要创建的新的线程，直接复用已有的线程即可**

**3：但是如果提交任务时，池子中没有空闲线程，也无法创建新的线程，任务就会排队等待**

## 自定义线程池--ThreadPoolExecutor

**ThreadPoolExecutor threadPoolExecutor = new ThreadPoolExecutor(核心线程数量,最大线程数量,空闲线程最大存活时间,时间单位,任务队列,创建线程工厂,任务的拒绝策略);**

**需注意当任务数两超过队列长度还有线程的最大数量时，多余的任务就会被拒绝**

**任务拒绝策略**

| 任务拒绝策略                          | 说明                                                   |
| ------------------------------------- | ------------------------------------------------------ |
| ThreadPoolExcutor.AbortPolicy         | 默认策略：丢弃任务并抛出RejectedExecutionException异常 |
| ThreadPoolExcutor.DiscardPolicy       | 丢弃任务，但是不抛出异常                               |
| ThreadPoolExcutor.DiscardOldestPolicy | 抛弃队列中等待最久的任务，然后把当前任务加入队列中     |
| ThreadPoolExcutor.CallerRunsPolicy    | 调用任务的run()方法绕过线程池直接执行                  |

**样例代码**

```
public class Main {
    public static void main(String[] args) throws InterruptedException {
        //    参数一：核心线程数量
        //    参数二：最大线程数
        //    参数三：空闲线程最大存活时间
        //    参数四：时间单位
        //    参数五：任务队列
        //    参数六：创建线程工厂
        //    参数七：任务的拒绝策略

        ThreadPoolExecutor pool = new ThreadPoolExecutor(3, 6, 60,
                TimeUnit.SECONDS, new ArrayBlockingQueue<>(3), Executors.defaultThreadFactory(),
                new ThreadPoolExecutor.AbortPolicy()
        );

        pool.submit(new MyRunnable());
    }
}
```

**注意：当核心线程满时，在提交任务就会进入阻塞队列**

**注意：当核心线程满，阻塞队列也满时，会创建临时线程**

**注意：当核心线程满时，队伍满时，临时线程满时，会触发任务拒绝策略**

**关于线程池的大小：**

**CPU密集型运算：最大并行数+ 1**

**I/O密集型运算：最大并行*****期望CPU利用率*（总时间（CPU计算时间 + 等待时间）/CPU计算时间）**

**最大并行数：基于intel的超线程技术，可以把核变成更多的线程，线程就是最大并行数**

**CPU密集型运算指的时计算操作，I/O指文件读取操作**

# 网络编程

## 基本概念

**定义：在网络通信协议下，不同计算机上运行的程序，进行的程序传输**

**CS架构：客户端服务器架构，优点：画面精美，用户体验好，但是需要开发客户端，也需要开发服务端，用户需要下载和更新很麻烦**

**BS架构：浏览器服务器架构，优点不需要开发客户端，是需要页面+服务端，且用户不需要下载，打开浏览器就能使用，但是如果应用过大，就会受影响**

**网络编程三要素：确定对方电脑在互联网上的地址即IP，确定接受数据的软件即端口号，确定网络传输的规则即协议**

**端口号：应用程序在设备中的唯一标识**

**协议：数据在网络中传输的规则，常见的协议有UDP,TCP,HTTP,HTTPS,FTP**

## IP地址

**IP：设备在网络中的地址，即互联网协议地址，是分配给上网设备的数字标签，是唯一的标识**

**IP地址分为两大类**

**IPv4：是给每个连接在网络上的主机分配一个32bit地址。按照TCP/IP规定，IP地址用二进制来表示，每个IP地址长32bit，也就是4个字节。例如一个采用二进制形式的IP地址是“11000000 10101000 00000001 01000010”，这么长的地址，处理起来也太费劲了。为了方便使用，IP地址经常被写成十进制的形式，中间使用符号“.”分隔不同的字节。于是，上面的IP地址可以表示为“192.168.1.66”。IP地址的这种表示法叫做“点分十进制表示法”，这显然比1和0容易记忆得多**

**IPv6：由于互联网的蓬勃发展，IP地址的需求量愈来愈大，但是网络地址资源有限，使得IP的分配越发紧张。为了扩大地址空间，通过IPv6重新定义地址空间，采用128位地址长度，每16个字节一组，分成8组十六进制数，这样就解决了网络地址资源数量不够的问题**

**分类形式：**

​	**公网地址（万维网使用）和私有地址（局域网使用）**

​	**192.68.开头的就是私有地址，范围即192.168.0.0-192.168.255.255，专门为组织结构内部使用，依次节省IP**

**其中127.0.0.1，也可以是localhost:是回送地址，也称本地IP，永远只会寻找当前所在本机**

**DOS常用命令：**

​	**ipconfig：查看本机IP地址**

​	**ping IP地址：检查网络是否连通**

## InetAddress类

**相关方法**

| 方法名                                    | 说明                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| static InetAddress getByName(String host) | 确定主机名称的IP地址。主机名称可以是机器名称，也可以是IP地址 |
| String getHostName()                      | 获取此IP地址的主机名                                         |
| String getHostAddress()                   | 返回文本显示中的IP地址字符串                                 |

**样例代码**

```
public class Main {
    public static void main(String[] args) throws UnknownHostException {
        //InetAddress address = InetAddress.getByName("itheima");
        InetAddress address = InetAddress.getByName("192.168.1.66");

        //public String getHostName()：获取此IP地址的主机名
        String name = address.getHostName();
        //public String getHostAddress()：返回文本显示中的IP地址字符串
        String ip = address.getHostAddress();

        System.out.println("主机名：" + name);
        System.out.println("IP地址：" + ip);
    }
}
```

## 端口和协议

**端口**

​	**设备上应用程序的唯一标识**

**端口号**

​	**用两个字节表示的整数，它的取值范围是0~65535。其中，0~1023之间的端口号用于一些知名的网络服务和应用，普通的应用程序需	要使用1024以上的端口号。如果端口号被另外一个服务或应用所占用，会导致当前程序启动失败**

**协议**

​	**计算机网络中，连接和通信的规则被称为网络通信协议**

**OSI参考模型：世界互联网协议标准，全球通信规范，单模型过于理想化，未能在因特网上进行广泛推广**

**TCP/IP参考模型：事实上的国际标准**

| OSI参考模型 | TCP/IP参考模型  | TCP/IOP参考模型各层对应协议 | 面向哪些                                                     |
| ----------- | --------------- | --------------------------- | ------------------------------------------------------------ |
| 应用层      | 应用层          | HTTP,FTP,Telent,DNS         | 一般是应用程序需要关注的，如浏览器，邮箱，程序员一般在这一层开发 |
| 表示层      | 应用层          | HTTP,FTP,Telent,DNS         | 一般是应用程序需要关注的，如浏览器，邮箱，程序员一般在这一层开发 |
| 会话层      | 应用层          | HTTP,FTP,Telent,DNS         | 一般是应用程序需要关注的，如浏览器，邮箱，程序员一般在这一层开发 |
| 传输层      | 传输层          | TCP,UDP                     | 选择传输使用TCP,UDP协议                                      |
| 网络层      | 网络层          | IP,ICMP,ARP                 | 封装自己的IP，对方的IP等信息                                 |
| 数据链路层  | 物理+数据链路层 | 硬件设备。010100101010100   | 转换成二进制利用物理设备进行传输                             |
| 物理层      | 物理+数据链路层 | 硬件设备。010100101010100   | 转换成二进制利用物理设备进行传输                             |

**UDP协议**

​	**用户数据报协议(User Datagram Protocol)**

​	**UDP是无连接通信协议，即在数据传输时，数据的发送端和接收端不建立逻辑连接。简单来说，当一台计算机向另外一台计算机发送数	据时，发送端不会确认接收端是否存在，就会发出数据，同样接收端在收到数据时，也不会向发送端反馈是否收到数据。**

​	**由于使用UDP协议消耗系统资源小，通信效率高，所以通常都会用于音频、视频和普通数据的传输**

​	**例如视频会议通常采用UDP协议，因为这种情况即使偶尔丢失一两个数据包，也不会对接收结果产生太大影响。但是在使用UDP协议传	送数据时，由于UDP的面向无连接性，不能保证数据的完整性，因此在传输重要数据时不建议使用UDP协议**

**TCP协议**

​	**传输控制协议 (Transmission Control Protocol)**

**TCP协议是面向连接的通信协议，即传输数据之前，在发送端和接收端建立逻辑连接，然后再传输数据，它提供了两台计算机之间可靠无差错的数据传输。在TCP连接中必须要明确客户端与服务器端，由客户端向服务端发出连接请求，每次连接的创建都需要经过“三次握手”**

​	**三次握手：TCP协议中，在发送数据的准备阶段，客户端与服务器之间的三次交互，以保证连接的可靠**

​	**第一次握手，客户端向服务器端发出连接请求，等待服务器确认**

​	**第二次握手，服务器端向客户端回送一个响应，通知客户端收到了连接请求**

​	**第三次握手，客户端再次向服务器端发送确认信息，确认连接**

​	**完成三次握手，连接建立后，客户端和服务器就可以开始进行数据传输了。由于这种面向连接的特性，TCP协议可以保证传输数据的安	全，所以应用十分广泛。例如上传文件、下载文件、浏览网页等**

## UDP通信程序

**发送数据**

**步骤：**

**1：创建发送端的DatagramSocket对象，类似于找个快递公司**

**2：数据打包（DatagramPacket）,类似于快递打包包裹**

**3：发送数据，类似于快递公司发货**

**4：释放资源，类似于付钱走人**

**样例代码**

```
public class Main {
    public static void main(String[] args) throws IOException {

        /*
            创建对象
            无参：随机选一个端口
            有参：指定端口号进行绑定，表明是从这个端口号往外发送的
        */
        DatagramSocket ds = new DatagramSocket();

        /*
            打包数据

        */
        String str = "Hello";
        byte[] bytes = str.getBytes();
        InetAddress address = InetAddress.getByName("127.0.0.1");
        int port = 10086;
        DatagramPacket dp = new DatagramPacket(bytes,bytes.length,address,port);

        //发送数据
        ds.send(dp);

        //释放资源
        ds.close();

    }
}
```

**Java中的UDP通信**

​	**UDP协议是一种不可靠的网络协议，它在通信的两端各建立一个Socket对象，但是这两个Socket只是发送，接收数据的对象，因此**

​	**对于基于UDP协议的通信双方而言，没有所谓的客户端和服务器的概念**

​	**Java提供了DatagramSocket类作为基于UDP协议的Socket**

**构造方法**

| 方法名                                                      | 说明                                                 |
| ----------------------------------------------------------- | ---------------------------------------------------- |
| DatagramSocket()                                            | 创建数据报套接字并将其绑定到本机地址上的任何可用端口 |
| DatagramPacket(byte[] buf,int len,InetAddress add,int port) | 创建数据包,发送长度为len的数据包到指定主机的指定端口 |

**相关方法**

| 方法名                         | 说明                   |
| ------------------------------ | ---------------------- |
| void send(DatagramPacket p)    | 发送数据报包           |
| void close()                   | 关闭数据报套接字       |
| void receive(DatagramPacket p) | 从此套接字接受数据报包 |

**接受数据**

**步骤：**

**1：创建接收端的DatagramSocket对象，类似于找个快递公司**

**2：接受打包好的数据，类似于接受快递**

**3：解析数据包，类似拆快递**

**4：释放资源，类似于付钱走人**

**样例代码**

```
package com.example.Test6;


import java.io.IOException;
import java.net.*;

public class Receive {
    public static void main(String[] args) throws IOException {

        /*
            创建接收端的DatagramSocket对象
            注意：在接受的时候必须要绑定端口，而且绑定的端口要跟发送端定义的接收端口一致
        */
        DatagramSocket ds = new DatagramSocket(10086);


        //接收数据包
        byte[] bytes = new byte[1024];
        DatagramPacket dp = new DatagramPacket(bytes, bytes.length);

        //这里的receive方法是阻塞的，如果没接收到数据它会在这里死等
        ds.receive(dp);

        //解析数据包
        byte[] data = dp.getData();
        int len = dp.getLength();
        InetAddress address = dp.getAddress();
        int port = dp.getPort();

        System.out.println("接收到数据" + new String(data, 0, len));
        System.out.println("该数据是从" + address + "这个电脑的" + port + "端口发出");

        //释放资源
        ds.close();

    }
}
```

**接收数据的步骤**

​	**创建接收端的Socket对象(DatagramSocket)**

​	**创建一个数据包，用于接收数据**

​	**调用DatagramSocket对象的方法接收数据**

​	**解析数据包，并把数据在控制台显示**

​	**关闭接收端**

**构造方法**

| 方法名                              | 说明                                            |
| ----------------------------------- | ----------------------------------------------- |
| DatagramPacket(byte[] buf, int len) | 创建一个DatagramPacket用于接收长度为len的数据包 |

**相关方法**

| 方法名            | 说明                                     |
| ----------------- | ---------------------------------------- |
| byte[]  getData() | 返回数据缓冲区                           |
| int  getLength()  | 返回要发送的数据的长度或接收的数据的长度 |

**UDP三种通讯方式**

**单播**

​	**单播用于两个主机之间的端对端通信**

**组播**

​	**组播用于对一组特定的主机进行通信**

​	**地址：224.0.0.0---239.255.255.255,其中224.0.0.0---224.0.0.255为预留的组播地址，是可以用的组播地址**

**广播**

​	**广播用于一个主机对整个局域网上所有主机上的数据通信**

​	**地址：255.255.255.255 **

**组播实现步骤**

**发送端**

1. **创建发送端的Socket对象(DatagramSocket)**
2. **创建数据，并把数据打包(DatagramPacket)**
3. **调用DatagramSocket对象的方法发送数据(在单播中,这里是发给指定IP的电脑但是在组播当中,这里是发给组播地址)**
4. **释放资源**

**接收端**

1. **创建接收端Socket对象(MulticastSocket)**
2. **创建一个箱子,用于接收数据**
3. **把当前计算机绑定一个组播地址**
4. **将数据接收到箱子中**
5. **解析数据包,并打印数据**
6. **释放资源**

**代码实现**

```java
// 发送端
public class ClinetDemo {
    public static void main(String[] args) throws IOException {
        // 1. 创建发送端的Socket对象(DatagramSocket)
        DatagramSocket ds = new DatagramSocket();
        String s = "hello 组播";
        byte[] bytes = s.getBytes();
        InetAddress address = InetAddress.getByName("224.0.1.0");
        int port = 10000;
        // 2. 创建数据，并把数据打包(DatagramPacket)
        DatagramPacket dp = new DatagramPacket(bytes,bytes.length,address,port);
        // 3. 调用DatagramSocket对象的方法发送数据(在单播中,这里是发给指定IP的电脑但是在组播当中,这里是发给组播地址)
        ds.send(dp);
        // 4. 释放资源
        ds.close();
    }
}
// 接收端
public class ServerDemo {
    public static void main(String[] args) throws IOException {
        // 1. 创建接收端Socket对象(MulticastSocket)
        MulticastSocket ms = new MulticastSocket(10000);
        // 2. 创建一个箱子,用于接收数据
        DatagramPacket dp = new DatagramPacket(new byte[1024],1024);
        // 3. 把当前计算机绑定一个组播地址,表示添加到这一组中.
        ms.joinGroup(InetAddress.getByName("224.0.1.0"));
        // 4. 将数据接收到箱子中
        ms.receive(dp);
        // 5. 解析数据包,并打印数据
        byte[] data = dp.getData();
        int length = dp.getLength();
        System.out.println(new String(data,0,length));
        // 6. 释放资源
        ms.close();
    }
}
```

## TCP通信程序

**TCP通信是一种可靠的网络协议，它在通信的两端各建立一个Socket对象，通信之间必须保证连接已经建立，通过Socket产生IO流来进行网络通信**

**客户端发数据步骤：**

**1：创建客户端的Socket对象与指定服务端连接，Socket(String host, int port)**

**2：获取输入流，写数据,OutputStream getOutputStream()**

**3：释放资源,void close()**

**服务端接收数据步骤：**

**1：创建服务器端的Socket对象（ServerSocket）,ServerSocket(int port)，这里的端口要跟客户端的定义的端口保持一致**

**2：监听客户端连接，返回一个Socket对象，Socket accept()**

**3：获取输入流，读数据，并把数据显示到控制台 InputStream getInputStream()**

**4:释放资源，void close()**

**发送数据构造方法**

| 方法名                               | 说明                                                         |
| ------------------------------------ | ------------------------------------------------------------ |
| Socket(InetAddress address,int port) | 创建流套接字并将其连接到指定IP指定端口号                     |
| Socket(String host, int port)        | 创建流套接字并将其连接到指定主机上的指定端口，这里的host是指定IP地址的字符串形式 |

**发送数据相关方法**

| 方法名                         | 说明                 |
| ------------------------------ | -------------------- |
| InputStream  getInputStream()  | 返回此套接字的输入流 |
| OutputStream getOutputStream() | 返回此套接字的输出流 |

**样例代码**

```java
public class Client {
    public static void main(String[] args) throws IOException {
        //TCP协议，发送数据

        //1.创建Socket对象
        //细节：在创建对象的同时会连接服务端
        //      如果连接不上，代码会报错
        Socket socket = new Socket("127.0.0.1",10000);
    
        //2.可以从连接通道中获取输出流
        OutputStream os = socket.getOutputStream();
        //写出数据
        os.write("aaa".getBytes());
    
        //3.释放资源
        os.close();
        socket.close();
    }

}
```

**接受数据构造方法**

| 方法名                  | 说明                             |
| ----------------------- | -------------------------------- |
| ServletSocket(int port) | 创建绑定到指定端口的服务器套接字 |

**接收数据相关方法**

| 方法名          | 说明                           |
| --------------- | ------------------------------ |
| Socket accept() | 监听要连接到此的套接字并接受它 |



**接收数据构造方法**

| 方法名                  | 说明                             |
| ----------------------- | -------------------------------- |
| ServletSocket(int port) | 创建绑定到指定端口的服务器套接字 |

**接收数据相关方法**

| 方法名          | 说明                           |
| --------------- | ------------------------------ |
| Socket accept() | 监听要连接到此的套接字并接受它 |

**注意事项**

1. **accept方法是阻塞的,作用就是等待客户端连接**
2. **客户端创建对象并连接服务器,此时是通过三次握手协议,保证跟服务器之间的连接**
3. **针对客户端来讲,是往外写的,所以是输出流**
   **针对服务器来讲,是往里读的,所以是输入流**
4. **read方法也是阻塞的**
5. **客户端在关流的时候,还多了一个往服务器写结束标记的动作**
6. **最后一步断开连接,通过四次挥手协议保证连接终止**

​	**四次挥手步骤：**

**1：客户端向服务端发出取消连接的请求**

**2：服务器返回一个响应，表示收到客户端的取消连接请求，等到服务器发送完数据**

**3：服务器向客户端发出确认取消的信息**

**4：客户端再次发出确认取消的信息，连接取消**





```
public class Server {
    public static void main(String[] args) throws IOException {
        //TCP协议，接收数据

        //1.创建对象ServerSocker
        ServerSocket ss = new ServerSocket(10000);
    
        //2.监听客户端的链接
        Socket socket = ss.accept();
    
        //3.从连接通道中获取输入流读取数据
        InputStream is = socket.getInputStream();
        int b;
        while ((b = is.read()) != -1){
            System.out.println((char) b);
        }
    
        //4.释放资源
        socket.close();
        ss.close();
    }

}
```

# 反射

**定义：允许对封装类的字段，方法和构造方法的信息进行编程访问**

## 获取Class对象的三种方式

```
Class.forName("全类名")//源代码阶段获取，最为常用的一种
类名.class//加载阶段获取，当作参数使用
对象.getClass()//运行阶段获取，已经有这个类的对象的时候使用
```

**全类名：包名+类名**

**样例代码**

```
public class MyReflectDemo1 {
    public static void main(String[] args) throws ClassNotFoundException {

        /*
        * 获取class对象的三种方式：
        *   1. Class.forName("全类名");
        *   2. 类名.class
        *   3. 对象.getClass();
        *
        * */


        //1. 第一种方式
        //全类名 ： 包名 + 类名
        //最为常用的
        Class clazz1 = Class.forName("com.itheima.myreflect1.Student");

        //2. 第二种方式
        //一般更多的是当做参数进行传递
        Class clazz2 = Student.class;


       //3.第三种方式
        //当我们已经有了这个类的对象时，才可以使用。
        Student s = new Student();
        Class clazz3 = s.getClass();

        System.out.println(clazz1 == clazz2);
        System.out.println(clazz2 == clazz3);


    }
}
```



## 获取构造方法（Constructor对象）

**注意以下方法需要先获取Class对象**

**Class类中的获取方法**

| 成员方法                                                     | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Constructor<?>[] getConstructors()                           | 返回公共构造方法对象的数组(public属性的构造方法)             |
| Constructor<?>[] getDeclaredConstructors()                   | 返回所有构造方法对象的数组                                   |
| Constructor<T> getConstructor(Class<?>...parmeterTypes)      | 返回单个公共构造方法对象(public属性的构造方法)，这里的参数，指的是构造方法的参数的Class对象 |
| Constructor<T> getDeclaredConstructor(Class<?>...parmeterTypes) | 返回单个构造方法对象构造方法，这里的参数，指的是构造方法的参数的Class对象 |

**创建对象的方法**

| 方法                             | 说明                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| T newInstance(Object...initargs) | 根据指定的构造方法创造对象，比如你获取了Student类的Constructor对象，然后你通过Constructor对象调用本方法就可以创建Student对象，里面的参数对应的是构造方法的参数 |
| setAccessible(boolean flag)      | 设置为true,表示取消访问检查，比如使用上面的方法进行创建对象时，私有的是无法通过上面的方法进行使用的，取消检查，就可以暴力反射进行使用了 |

```
package com.itheima.myreflect2;


import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Parameter;

public class MyReflectDemo {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException {
    /*
        Class类中用于获取构造方法的方法
            Constructor<?>[] getConstructors()                                返回所有公共构造方法对象的数组
            Constructor<?>[] getDeclaredConstructors()                        返回所有构造方法对象的数组
            Constructor<T> getConstructor(Class<?>... parameterTypes)         返回单个公共构造方法对象
            Constructor<T> getDeclaredConstructor(Class<?>... parameterTypes) 返回单个构造方法对象


        Constructor类中用于创建对象的方法
            T newInstance(Object... initargs)                                 根据指定的构造方法创建对象
            setAccessible(boolean flag)                                       设置为true,表示取消访问检查
    */

        //1.获取class字节码文件对象
        Class clazz = Class.forName("com.itheima.myreflect2.Student");

        //2.获取构造方法
       /* Constructor[] cons1 = clazz.getConstructors();
        for (Constructor con : cons1) {
            System.out.println(con);
        }
        Constructor[] cons2 = clazz.getDeclaredConstructors();
        for (Constructor con : cons2) {
            System.out.println(con);
        }*/


       /* Constructor con1 = clazz.getDeclaredConstructor();
        System.out.println(con1);

        Constructor con2 = clazz.getDeclaredConstructor(String.class);
        System.out.println(con2);

        Constructor con3 = clazz.getDeclaredConstructor(int.class);
        System.out.println(con3);*/

        Constructor con4 = clazz.getDeclaredConstructor(String.class,int.class);

        //获取权限修饰符
        int modifiers = con4.getModifiers();
        System.out.println(modifiers);
        
        
        //获取构造方法的参数数组，即Parameter
        Parameter[] parameters = con4.getParameters();
        for (Parameter parameter : parameters) {
            System.out.println(parameter);
        }

        //暴力反射：表示临时取消权限校验
        con4.setAccessible(true);
        Student stu = (Student) con4.newInstance("张三", 23);

        System.out.println(stu);


    }
}
```





## 获取成员变量对象（Field对象）

**Class类中获取方法**

| 成员方法                            | 说明                                                       |
| ----------------------------------- | ---------------------------------------------------------- |
| Field[] getFields()                 | 返回所有公共成员变量对象的数组                             |
| Field[] getDeclaredFields()         | 返回所有成员变量对象的数组，任意属性                       |
| Field getField(String name)         | 返回单个公共成员变量对象，根据成员变量的名字进行获取       |
| Field getDeclaredField(String name) | 返回单个成员变量对象，根据成员变量的名字进行获取，任意属性 |

**Field类的方法**

| 成员方法                           | 说明                                                     |
| ---------------------------------- | -------------------------------------------------------- |
| void set(Object obj, Object value) | 给对应的成员变量赋值，第一个参数指定对象，第二参数指定值 |
| Object get(Object obj)             | 获取对应的成员变量的值，参数指定对象                     |

**样例代码**

```
package com.itheima.myreflect3;

import java.lang.reflect.Field;

public class MyReflectDemo {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException, IllegalAccessException {
    /*
       Class类中用于获取成员变量的方法
            Field[] getFields()：                返回所有公共成员变量对象的数组
            Field[] getDeclaredFields()：        返回所有成员变量对象的数组
            Field getField(String name)：        返回单个公共成员变量对象
            Field getDeclaredField(String name)：返回单个成员变量对象

       Field类中用于创建对象的方法
            void set(Object obj, Object value)：赋值
            Object get(Object obj)              获取值

    */


        //1.获取class字节码文件的对象
        Class clazz = Class.forName("com.itheima.myreflect3.Student");

        //2.获取所有的成员变量
       /* Field[] fields = clazz.getDeclaredFields();
        for (Field field : fields) {
            System.out.println(field);
        }*/

        //获取单个的成员变量
        Field name = clazz.getDeclaredField("name");
        System.out.println(name);

        //获取权限修饰符
        int modifiers = name.getModifiers();
        System.out.println(modifiers);

        //获取成员变量的名字
        String n = name.getName();
        System.out.println(n);

        //获取成员变量的数据类型
        Class<?> type = name.getType();
        System.out.println(type);

        //获取成员变量记录的值
        Student s = new Student("zhangsan",23,"男");
        name.setAccessible(true);
        String value = (String) name.get(s);
        System.out.println(value);

        //修改对象里面记录的值
        name.set(s,"lisi");

        System.out.println(s);

    }
}
```

## 获取成员方法的对象（Method对象）

**Class类中用于获取成员方法的方法**

| 方法                          | 说明                                       |
| ----------------------------- | ------------------------------------------ |
| Method[] getMethods()         | 返回所有公共成员方法对象的数组，包括继承的 |
| Method[] getDeclaredMethods() | 返回所有成员方法对象的数组，不包括继承的   |
| Method getMethod()            | 返回单个公共成员方法对象                   |
| Method getDeclaredMethod()    | 返回单个成员方法对象                       |

**Method类的成员方法**

| 方法                                    | 说明                                                         |
| --------------------------------------- | ------------------------------------------------------------ |
| Object invoke(Object obj,Object...args) | 运行对应方法，参数一：表示调用方法的对象，参数二：调用方法的传递参数，返回值就是方法的返回值 |

**样例代码**

```
package com.itheima.myreflect4;


import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.lang.reflect.Parameter;

public class MyReflectDemo {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, IllegalAccessException {
    /*
       Class类中用于获取成员方法的方法
            Method[] getMethods()：返回所有公共成员方法对象的数组，包括继承的
            Method[] getDeclaredMethods()：返回所有成员方法对象的数组，不包括继承的
            Method getMethod(String name, Class<?>... parameterTypes) ：返回单个公共成员方法对象
            Method getDeclaredMethod(String name, Class<?>... parameterTypes)：返回单个成员方法对象


       Method类中用于创建对象的方法
            Object invoke(Object obj, Object... args)：运行方法
            参数一：用obj对象调用该方法
            参数二：调用方法的传递的参数（如果没有就不写）
            返回值：方法的返回值（如果没有就不写）

        获取方法的修饰符
        获取方法的名字
        获取方法的形参
        获取方法的返回值
        获取方法的抛出的异常

    */



        //1. 获取class字节码文件对象
        Class clazz = Class.forName("com.itheima.myreflect4.Student");

        //2. 获取里面所有的方法对象(包含父类中所有的公共方法)
       /* Method[] methods = clazz.getMethods();
        for (Method method : methods) {
            System.out.println(method);
        }*/

        // 获取里面所有的方法对象(不能获取父类的，但是可以获取本类中私有的方法)
        /*Method[] methods = clazz.getDeclaredMethods();
        for (Method method : methods) {
            System.out.println(method);
        }*/

        // 获取指定的单一方法
        Method m = clazz.getDeclaredMethod("eat", String.class);
        System.out.println(m);

        // 获取方法的修饰符
        int modifiers = m.getModifiers();
        System.out.println(modifiers);

        // 获取方法的名字
        String name = m.getName();
        System.out.println(name);

        // 获取方法的形参
        Parameter[] parameters = m.getParameters();
        for (Parameter parameter : parameters) {
            System.out.println(parameter);
        }

        //获取方法的抛出的异常
        Class[] exceptionTypes = m.getExceptionTypes();
        for (Class exceptionType : exceptionTypes) {
            System.out.println(exceptionType);
        }

        //方法运行
        /*Method类中用于创建对象的方法
        Object invoke(Object obj, Object... args)：运行方法
        参数一：用obj对象调用该方法
        参数二：调用方法的传递的参数（如果没有就不写）
        返回值：方法的返回值（如果没有就不写）*/


        Student s = new Student();
        m.setAccessible(true);
        //参数一s：表示方法的调用者
        //参数二"汉堡包"：表示在调用方法的时候传递的实际参数
        String result = (String) m.invoke(s, "汉堡包");
        System.out.println(result);


    }
}
```

# 动态代理

```
package com.itheima.mydynamicproxy1;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

/*
*
* 类的作用：
*       创建一个代理
*
* */
public class ProxyUtil {


    /*
    *
    * 方法的作用：
    *       给一个明星的对象，创建一个代理
    *
    *  形参：
    *       被代理的明星对象
    *
    *  返回值：
    *       给明星创建的代理
    *
    *
    *
    * 需求：
    *   外面的人想要大明星唱一首歌
    *   1. 获取代理的对象
    *      代理对象 = ProxyUtil.createProxy(大明星的对象);
    *   2. 再调用代理的唱歌方法
    *      代理对象.唱歌的方法("只因你太美");
    * */
    public static Star createProxy(BigStar bigStar){
       /* java.lang.reflect.Proxy类：提供了为对象产生代理对象的方法：

        public static Object newProxyInstance(ClassLoader loader, Class<?>[] interfaces, InvocationHandler h)
        参数一：用于指定用哪个类加载器，去加载生成的代理类
        参数二：指定接口，这些接口用于指定生成的代理长什么，也就是有哪些方法
        参数三：用来指定生成的代理对象要干什么事情*/
        Star star = (Star) Proxy.newProxyInstance(
                ProxyUtil.class.getClassLoader(),//参数一：用于指定用哪个类加载器，去加载生成的代理类
                new Class[]{Star.class},//参数二：指定接口，这些接口用于指定生成的代理长什么，也就是有哪些方法
                //参数三：用来指定生成的代理对象要干什么事情
                new InvocationHandler() {
                    @Override
                    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                        /*
                        * 参数一：代理的对象
                        * 参数二：要运行的方法 sing
                        * 参数三：调用sing方法时，传递的实参
                        * */
                        if("sing".equals(method.getName())){
                            System.out.println("准备话筒，收钱");
                        }else if("dance".equals(method.getName())){
                            System.out.println("准备场地，收钱");
                        }
                        //去找大明星开始唱歌或者跳舞
                        //代码的表现形式：调用大明星里面唱歌或者跳舞的方法
                        return method.invoke(bigStar,args);
                    }
                }
        );
        return star;

    }
}
```



```
public class Test {
    public static void main(String[] args) {



    /*
        需求：
            外面的人想要大明星唱一首歌
             1. 获取代理的对象
                代理对象 = ProxyUtil.createProxy(大明星的对象);
             2. 再调用代理的唱歌方法
                代理对象.唱歌的方法("只因你太美");
     */


        //1. 获取代理的对象
        BigStar bigStar = new BigStar("鸡哥");
        Star proxy = ProxyUtil.createProxy(bigStar);

        //2. 调用唱歌的方法
        String result = proxy.sing("只因你太美");
        System.out.println(result);




    }
}
```

# 注解

**定义：就是java代码里的特殊标记，让其他程序根据注解信息来决定怎么执行程序**

**自定义注解**

```
public @interface 注解名称 {
	public 属性类型 属性名() default 默认值;
}
```

**特殊属性名：value**

**如果注解中只有一个value属性，使用注解时，value名称可以不写，即下面的写法**

```
@Test("aaa")
@Test(value = "aaa")
```

**样例**

```
public @interface MyTest {
    String aaa();
    boolean bbb();
    String[] ccc();
}
```

**扩展，上述代码的实际模样**

```
public interface MyTest extends Annotation {
	public abstract Stringh aaa();
	public abstract boolean bbb();
	public abstract String[] ccc();
}
```

**元注解**

**定义：修饰注解的注解**

**@Target: 被申明的注解可以在哪些位置使用**

| 值                         | 含义     |
| -------------------------- | -------- |
| ElementType.TYPE           | 类，接口 |
| ElementType.FIELD          | 成员变量 |
| ElementType.METHOD         | 成员方法 |
| ElementType.PARAMETER      | 方法参数 |
| ElementType.CONSTRUCTOR    | 构造器   |
| ElementType.LOCAL_VARIABLE | 局部变量 |

**@Retention:申明注解的保留周期**

| 值                       | 含义                                     |
| ------------------------ | ---------------------------------------- |
| Retention.SOURCE         | 注解只作用在源码阶段，字节码文件中不存在 |
| Retention.CLASS          | 保留到字节码文件阶段，运行阶段不存在     |
| Retention.SOURCE.RUNTIME | 一直保留到运行阶段                       |

**很多注解的应用就是结合反射原理来触发方法的执行的，比如junit**

# junit测试单元

**对于需要运行测试的方法我们只需要在这个方法的上面加上@Test注解**

**断言机制**

```
Assert.assertEquals(String message, long expected, long actual)
```

**第一个参数：代表如果跟预期结果不一致输出什么信息**

**第二个参数：预测值**

**第三个参数：实际值**

**常用注解**

| 注解                    | 含义                                                         |
| ----------------------- | ------------------------------------------------------------ |
| @Test                   | 测试类的方法必须用它修饰才能成为测试方法，才能启动执行       |
| @Before/@BeforeEach     | 用来修饰一个实例方法，该方法会在每一个测试方法执行之前执行一次 |
| @After/AfterEach        | 用来修饰一个实例方法，该方法会在每一个测试方法执行之后执行一次 |
| @BeforeClass/@BeforeAll | 用来修饰一个静态方法，该方法会在所有测试方法之前执行一次     |
| @AfterClass/@AfterAll   | 用来修饰一个静态方法，该方法会在所有测试方法之后执行一次     |

**在测试方法执行前执行的方法：常用于初始化资源**

**在测试方法执行后执行的方法：常用于释放资源**

**住：/之前的是junit4版本的注解,后面是junit5版本**

