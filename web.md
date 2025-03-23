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

## Pagehelper

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

**指定所有的异常都需要事务回滚：@Transactional（rollbackFor = Exception.class）**

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
public class AliOSSAutoConfiguration {
    @Bean
    public AliOSSUtils aliOSSUtils(AliOSSProperties aliOSSProperties){
        AliOSSUtils aliOSSUtils = new AliOSSUtils();
        aliOSSUtils.setAliOSSProperties(aliOSSProperties);
        return aliOSSUtils;
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

**当然除了使用@Component注解将该properties类注入到spring容器中外，还可以使用@EnableConfigurationProperties,我们只需要在用到该properties类的config类上加上该注解即可**

```java
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

**注意：在老版本中，不使用.imports文件而是使用spring.factories文件去加载自动配置类**

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

### **快速入门**

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

**需要注意，使用openFeign发送Get请求时，不能使用实体参数的方法进行数据的传输，即openFeign的get请求无法解析对象参数，如需使用则需要配合@SpringQueryMap注解**

```java
@GetMapping("/items/page")
PageDTO<ItemDTO> queryItemByPage(@SpringQueryMap PageQuery query);
```







### 连接池

**OpenFeign对http请求做了封装，不过其底层发起http请求，依赖于其他框架，这些框架可以自己选择，包括以下三种：**

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

**以下我们采用方案1进行拆分，当然我个人采用的是**

**这里因为`ItemClient`现在定义到了它所属的服务的包下，而cart-service的启动类定义在`com.hmall.cart`包下，扫描不到`ItemClient`，cart-service无法创建ItemClient的bean,所以会报错。因此我们有以下两种解法**

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

### 微服务间的信息传输

**微服务之间调用是基于OpenFeign来实现的，并不是我们自己发送的请求。我们如何才能让每一个由OpenFeign发起的请求自动携带登录用户信息呢？**

**这里要借助Feign中提供的一个拦截器接口：`feign.RequestInterceptor`**

```Java
public interface RequestInterceptor {

  /**
   * Called for every request. 
   * Add data using methods on the supplied {@link RequestTemplate}.
   */
  void apply(RequestTemplate template);
}
```

**我们只需要实现这个接口，然后实现apply方法，利用`RequestTemplate`类来添加请求头，将用户信息保存到请求头中。这样以来，每次OpenFeign发起请求的时候都会调用该方法，传递用户信息**

**这里我们可以在OpenFeign的配置类里书写**

```
package com.hmall.common.config;

import com.hmall.common.utils.UserContext;
import feign.RequestInterceptor;
import feign.RequestTemplate;
import org.springframework.context.annotation.Bean;
import feign.Logger;
public class DefaultFeignConfig {
    @Bean
    public Logger.Level feignLogLevel(){
        return Logger.Level.FULL;
    }


    @Bean
    public RequestInterceptor userInfoRequestInterceptor(){
        return requestTemplate -> {
            Long userId = UserContext.getUser();
            if(userId != null){
                requestTemplate.header("user-info", userId.toString());
            }

        };
    }

}
```

## 网关

### 基本概念

**网关：就是网络的关口，负责请求的路由，转发，身份校验**

![](assets\1733972209479.png)

**在spring cloud中网关的实现有两种:**

**spring cloud gateway:spring 官方出品，基于webFlux响应式编程，无需调优即可获得优异性能**、

**Netflix zuul:Netflix出品，基于servlet阻塞式编程，需要调优才能获得与springCloudGeteway一样的性能**

### 快速入门

**相关依赖引入**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>hmall</artifactId>
        <groupId>com.heima</groupId>
        <version>1.0.0</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>hm-gateway</artifactId>

    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
    </properties>
    <dependencies>
        <!--common-->
        <dependency>
            <groupId>com.heima</groupId>
            <artifactId>hm-common</artifactId>
            <version>1.0.0</version>
        </dependency>
        <!--网关-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-gateway</artifactId>
        </dependency>
        <!--nacos discovery-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!--负载均衡-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-loadbalancer</artifactId>
        </dependency>
    </dependencies>
    <build>
        <finalName>${project.artifactId}</finalName>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

**编写启动类**

```Java
package com.hmall.gateway;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class GatewayApplication {
    public static void main(String[] args) {
        SpringApplication.run(GatewayApplication.class, args);
    }
}
```

**编写配置文件,以及配置路由**

```yaml
server:
  port: 8080
spring:
  application:
    name: gateway
  cloud:
    nacos:
      server-addr: 192.168.230.130:8848
    gateway:
      routes:
        - id: item # 路由规则id，自定义，唯一
          uri: lb://item-service # 路由的目标服务，lb代表负载均衡，会从注册中心拉取服务列表,除了lb外还有ws(WebSocket)和http
          predicates: # 路由断言，判断当前请求是否符合当前规则，符合则路由到目标服务
            - Path=/items/**,/search/** # 这里是以请求路径作为判断规则
        - id: cart
          uri: lb://cart-service
          predicates:
            - Path=/carts/**
        - id: user
          uri: lb://user-service
          predicates:
            - Path=/users/**,/addresses/**
        - id: trade
          uri: lb://trade-service
          predicates:
            - Path=/orders/**
        - id: pay
          uri: lb://pay-service
          predicates:
            - Path=/pay-orders/**
```

### 路由属性

**网关路由对应的java类型是RouteDefinition，其中常见的属性有：**

**id:路由唯一标识**

**url:路由目标地址**

**predicates:路由断言，判断请求是否符合当前路由**

**filter:路由过滤器，对请求响应作特殊处理**

**这里我们重点关注`predicates`，也就是路由断言。SpringCloudGateway中支持的断言类型有很多：**

| **名称**   | **说明**                       | **示例**                                                     |
| :--------- | :----------------------------- | :----------------------------------------------------------- |
| After      | 是某个时间点后的请求           | - After=2037-01-20T17:42:47.789-07:00[America/Denver]        |
| Before     | 是某个时间点之前的请求         | - Before=2031-04-13T15:14:47.433+08:00[Asia/Shanghai]        |
| Between    | 是某两个时间点之前的请求       | - Between=2037-01-20T17:42:47.789-07:00[America/Denver], 2037-01-21T17:42:47.789-07:00[America/Denver] |
| Cookie     | 请求必须包含某些cookie         | - Cookie=chocolate, ch.p                                     |
| Header     | 请求必须包含某些header         | - Header=X-Request-Id, \d+                                   |
| Host       | 请求必须是访问某个host（域名） | - Host=**.somehost.org,**.anotherhost.org                    |
| Method     | 请求方式必须是指定方式         | - Method=GET,POST                                            |
| Path       | 请求路径必须符合指定规则       | - Path=/red/{segment},/blue/**                               |
| Query      | 请求参数必须包含指定参数       | - Query=name, Jack或者- Query=name                           |
| RemoteAddr | 请求者的ip必须是指定范围       | - RemoteAddr=192.168.1.1/24                                  |
| weight     | 权重处理                       |                                                              |

**路由（Route）过滤器（Filter）允许以某种方式修改传入的 HTTP 请求或传出的 HTTP 响应。路由过滤器的范围是一个特定的路由。Spring Cloud Gateway 包括许多内置的 `GatewayFilter` 工厂。详细见官方文档https://springdoc.cn/spring-cloud-gateway/#gatewayfilter-%E5%B7%A5%E5%8E%82**

### 登录校验

#### 基本概念

**登录校验必须在网关转发请求之前去做，否则就没有了意义，因此我们需要了解一下Gatewat的内部工作原理**

![](assets\1734015962199.png)

**如图所示：**

**1：客户端请求进入网关后由`HandlerMapping`对请求做判断，找到与当前请求匹配的路由规则（`Route`），然后将请求交给`WebHandler`去处理。**

**2：`WebHandler`则会加载当前路由下需要执行的过滤器链（`Filter chain`），然后按照顺序逐一执行过滤器（后面称为`Filter`）。**

**3：图中`Filter`被虚线分为左右两部分，是因为`Filter`内部的逻辑分为`pre`和`post`两部分，分别会在请求路由到微服务之前和之后被执行。**

**4：只有所有`Filter`的`pre`逻辑都依次顺序执行通过后，请求才会被路由到微服务。**

**5：微服务返回结果后，再倒序执行`Filter`的`post`逻辑。**

**6：最终把响应结果返回。**

**如图中所示，最终请求转发是有一个名为`NettyRoutingFilter`的过滤器来执行的，而且这个过滤器是整个过滤器链中顺序最靠后的一个。如果我们能够定义一个过滤器，在其中实现登录校验逻辑，并且将过滤器执行顺序定义到**`NettyRoutingFilter`之前**，这就符合我们的需求了！**

**网关和微服务之间的数据传递如何实现呢，这里可以把数据放到请求头里进行传递**

**各微服务之间的数据传递如何实现，也可以把数据存到请求头里去实现**

#### 自定义GlobalFilte

**网关过滤器链中的过滤器有两种：**

**GatewayFilter：路由过滤器，作用范围比较灵活，可以是任意指定的路由`Route`.** 

**GlobalFilter`：全局过滤器，作用范围是所有路由，不可配置。**

**注意：过滤器链之外还有一种过滤器，HttpHeadersFilter，用来处理传递到下游微服务的请求头。例如org.springframework.cloud.gateway.filter.headers.XForwardedHeadersFilter可以传递代理请求原本的host头到下游微服务**

**其实`GatewayFilter`和`GlobalFilter`这两种过滤器的方法签名完全一致：**

```Java
/**

 * 处理请求并将其传递给下一个过滤器
 * @param exchange 当前请求的上下文，其中包含request、response等各种数据
 * @param chain 过滤器链，基于它向下传递请求
 * @return 根据返回值标记当前请求是否被完成或拦截，chain.filter(exchange)就放行了。
 */
Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain);
```

**入门案例**

```java
package com.hmall.gateway.filters;

import org.springframework.cloud.gateway.filter.GatewayFilterChain;
import org.springframework.cloud.gateway.filter.GlobalFilter;
import org.springframework.core.Ordered;
import org.springframework.http.HttpHeaders;
import org.springframework.http.server.reactive.ServerHttpRequest;
import org.springframework.stereotype.Component;
import org.springframework.web.server.ServerWebExchange;
import reactor.core.publisher.Mono;

@Component
public class MyGlobalFilter implements GlobalFilter, Ordered {

    @Override
    public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        // TODO 模拟登录校验的逻辑
        ServerHttpRequest request = exchange.getRequest();
        HttpHeaders headers = request.getHeaders();
        System.out.println("Headers=" + headers);
        //放行
        return chain.filter(exchange);
    }

    //现在我们要把这个过滤器放入过滤器链，且优先级要在NettyRoutingFilter之前，
    //只需要实现Ordered接口，并实现getOrder方法即可，改方法的返回值越小优先级越高。
    //NettyRoutingFilter优先级最靠后值int的最大值，所以设置为0即可
    @Override
    public int getOrder() {
        return 0;
    }
}
```

#### 自定义GatewayFilter

**自定义`GatewayFilter`不是直接实现`GatewayFilter`，而是实现`AbstractGatewayFilterFactory`。最简单的方式是这样的：**

```Java
@Component
public class PrintAnyGatewayFilterFactory extends AbstractGatewayFilterFactory<Object> {
    @Override
    public GatewayFilter apply(Object config) {
        return new GatewayFilter() {
            @Override
            public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
                // 获取请求
                ServerHttpRequest request = exchange.getRequest();
                // 编写过滤器逻辑
                System.out.println("过滤器执行了");
                // 放行
                return chain.filter(exchange);
            }
        };
    }
}
```

**注意**：**该类的名称一定要以`GatewayFilterFactory`为后缀！**

然后在yaml配置中这样使用：

```YAML
spring:
  cloud:
    gateway:
      default-filters:
            - PrintAny # 此处直接以自定义的GatewayFilterFactory类名称前缀类声明过滤器
```

**入门案例**

```java
package com.hmall.gateway.filters;

import lombok.extern.slf4j.Slf4j;
import org.springframework.cloud.gateway.filter.GatewayFilter;
import org.springframework.cloud.gateway.filter.GatewayFilterChain;
import org.springframework.cloud.gateway.filter.OrderedGatewayFilter;
import org.springframework.cloud.gateway.filter.factory.AbstractGatewayFilterFactory;
import org.springframework.http.HttpHeaders;
import org.springframework.http.server.reactive.ServerHttpRequest;
import org.springframework.stereotype.Component;
import org.springframework.web.server.ServerWebExchange;
import reactor.core.publisher.Mono;

@Component
@Slf4j
public class PrintAnyGatewayFilterFactory extends AbstractGatewayFilterFactory<Object> {

    @Override
    public GatewayFilter apply(Object config) {
        return new OrderedGatewayFilter(new GatewayFilter() {
            @Override
            public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
                // TODO 模拟登录校验的逻辑
                ServerHttpRequest request = exchange.getRequest();
                HttpHeaders headers = request.getHeaders();
                log.info("Headers=" + headers);
                return chain.filter(exchange);
            }
        }, 1);
    }
}
```

**注意：与上面的写法不同，为了给这个filter定义优先级，我们需要return new OrderedGatewayFilter(),这个类的第二个参数就是这个filter的优先级**

**另外，这种过滤器还可以支持动态配置参数，不过实现起来比较复杂，示例：**

```Java
@Component
public class PrintAnyGatewayFilterFactory // 父类泛型是内部类的Config类型
                extends AbstractGatewayFilterFactory<PrintAnyGatewayFilterFactory.Config> {

    @Override
    public GatewayFilter apply(Config config) {
        // OrderedGatewayFilter是GatewayFilter的子类，包含两个参数：
        // - GatewayFilter：过滤器
        // - int order值：值越小，过滤器执行优先级越高
        return new OrderedGatewayFilter(new GatewayFilter() {
            @Override
            public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
                // 获取config值
                String a = config.getA();
                String b = config.getB();
                String c = config.getC();
                // 编写过滤器逻辑
                System.out.println("a = " + a);
                System.out.println("b = " + b);
                System.out.println("c = " + c);
                // 放行
                return chain.filter(exchange);
            }
        }, 100);
    }

    // 自定义配置属性，成员变量名称很重要，下面会用到
    @Data
    static class Config{
        private String a;
        private String b;
        private String c;
    }
    // 将变量名称依次返回，顺序很重要，将来读取参数时需要按顺序获取
    @Override
    public List<String> shortcutFieldOrder() {
        return List.of("a", "b", "c");
    }
        // 返回当前配置类的类型，也就是内部的Config
    @Override
    public Class<Config> getConfigClass() {
        return Config.class;
    }

}
```

**然后在yaml文件中使用：**

```YAML
spring:
  cloud:
    gateway:
      default-filters:
            - PrintAny=1,2,3 # 注意，这里多个参数以","隔开，将来会按照shortcutFieldOrder()方法返回的参数顺序依次复制
```

**上面这种配置方式参数必须严格按照shortcutFieldOrder()方法的返回参数名顺序来赋值。**

**还有一种用法，无需按照这个顺序，就是手动指定参数名：**

```YAML
spring:
  cloud:
    gateway:
      default-filters:
            - name: PrintAny
              args: # 手动指定参数名，无需按照参数顺序
                a: 1
                b: 2
                c: 3
```



### 网关与微服务间传递用户信息

![](assets\1738307351858(1).png)

**如何修改网关发送到下游微服务的请求，把用户信息存储到请求头，这就需要用到ServerWenExchange类提供的api，示例如下**

```
exchange.mutate()
.request(builder -> builder.header("user-info", userInfo))
.build();

```

**接下来，我们只需要编写拦截器，获取用户信息并保存到`UserContext`，然后放行即可。**

**由于每个微服务都有获取登录用户的需求，因此拦截器我们直接写在`hm-common`中，并写好自动装配。这样微服务只需要引入`hm-common`就可以直接具备拦截器功能，无需重复编写。**

**我们在`hm-common`模块下定义一个拦截器：**

```java
package com.hmall.common.interceptors;

import cn.hutool.core.util.StrUtil;
import com.hmall.common.utils.UserContext;
import org.springframework.web.servlet.HandlerInterceptor;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class UserInfoInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        //1：获取用户登录信息
        String userInfo = request.getHeader("user-info");

        //2:判断是否获取了用户，如果有，存入到ThreadLocal
        if(StrUtil.isNotBlank(userInfo)){
            UserContext.setUser(Long.valueOf(userInfo));
        }
        return true;
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        UserContext.removeUser();
    }
}
```



**拦截写好后，我们就需要编写SpringMvc的配置类来配置拦截器**

```java
package com.hmall.common.config;

import com.hmall.common.interceptors.UserInfoInterceptor;
import org.springframework.boot.autoconfigure.condition.ConditionalOnClass;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.DispatcherServlet;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;


@Configuration
@ConditionalOnClass(DispatcherServlet.class)
public class MvcConfig implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new UserInfoInterceptor());
    }
}
```



**当然，即使我们已经编写好了相应的配置类，也还需要在hm-common包下的MATA-INF里spring.factories文件里配置该配置类的路径，具体内容详见spring boot的自动装配相关内容**

```
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
  com.hmall.common.config.MyBatisConfig,\
  com.hmall.common.config.MvcConfig,\
  com.hmall.common.config.JsonConfig
```



**当然，这样写有一个小bug，就是在网关中也依赖了hm-common这个包，但是网关所用到的拦截技术是webFlux，而不是mvc相关的技术，也就是说网关并没有依赖mvc相关的东西，但是又因为依赖了hm-common，导致它间接拥有了我们刚刚配置的拦截器相关的东西，而这些东西又需要mvc相关的依赖，这就导致网关依赖的hm-common的拦截器缺少了mvc依赖，因此报错，也解决这个问题，只需要使用我们在自动装配原理时所学到@ConditionOnClass()注解，这样该配置就有了条件判断生效的效果，当具有这个DispatcherServlet这个类时，这个配置类才会生效，而这个类就是mvc的核心类了**



**当然这里有一个解释有点怪，就是明明网关已经依赖了hm-common,而hm-common又依赖了mvc相关的依赖，根据依赖传递，网关也应当依赖了mvc的相关依赖，关于这个问题，可能是加了特定条件，使得网关屏蔽了该依赖**





### 完整的用户校验功能实现

```
@Component
@RequiredArgsConstructor
public class AuthGlobalFilter implements GlobalFilter, Ordered {
    private final AuthProperties authProperties;
    private final JwtTool jwtTool;
    //用于匹配带通配符的路径
    private final AntPathMatcher antPathMatcher = new AntPathMatcher();
    @Override
    public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        //1:获取request
        ServerHttpRequest request = exchange.getRequest();
        //2:判断是否需要登录拦截
        if(isExclude(request.getPath().toString())){
            return chain.filter((exchange));
        }
        //3：获取token
        String token = null;
        List<String> headers =  request.getHeaders().get("authorization");
        if(headers != null && !headers.isEmpty()){
            token = headers.get(0);
        }

        Long userId = null;
        //4:检验并解析token
        try{
            userId = jwtTool.parseToken(token);
        }catch(UnauthorizedException e){
            //获取相应，并修改响应的状态码
            ServerHttpResponse response = exchange.getResponse();
            response.setStatusCode(HttpStatus.UNAUTHORIZED);
            //可以直接返回响应，实现拦截
            return response.setComplete();
        }



        //5:传递用户信息
        String userInfo = userId.toString();
        ServerWebExchange swe = exchange.mutate()
                .request(builder -> builder.header("user-info",userInfo))
                .build();
        
        //6:放行
        return chain.filter((swe));
    }

    @Override
    public int getOrder() {
        return 0;
    }

    private boolean isExclude(String path){
        for (String excludePath : authProperties.getExcludePaths()) {
            if(antPathMatcher.match(excludePath,path)){
                return true;
            }
        }
        return false;
    }
}
```

## 配置管理

### 配置管理的引入

**不过，现在依然还有几个问题需要解决：**

​	**网关路由在配置文件中写死了，如果变更必须重启微服务**

​	**某些业务配置在配置文件中写死了，每次修改都要重启服务**

​	**每个微服务都有很多重复的配置，维护成本高**

**这些问题都可以通过统一的配置管理器服务解决。而Nacos不仅仅具备注册中心功能，也具备配置管理的功能：**

![](assets\1738336633645.png)

**微服务共享的配置可以统一交给Nacos保存和管理，在Nacos控制台修改配置后，Nacos会将配置变更推送给相关的微服务，并且无需重启即可生效，实现配置热更新。**

**网关的路由同样是配置，因此同样可以基于这个功能实现动态路由功能，无需重启网关即可修改路由配置。**

### **配置共享**

#### 添加共享配置

**我们在nacos控制台分别添加这些配置。**

**首先是jdbc相关配置，在`配置管理`->`配置列表`中点击`+`新建一个配置：**

![](assets\1738503720119.png)

**在弹出的表单中填写信息：**

![](assets\1738504030110.png)

**注意这里的jdbc的相关参数并没有写死，例如：**

- **`数据库ip`：通过`${hm.db.host:192.168.150.101}`配置了默认值为`192.168.150.101`，同时允许通过`${hm.db.host}`来覆盖默认值**
- **`数据库端口`：通过`${hm.db.port:3306}`配置了默认值为`3306`，同时允许通过`${hm.db.port}`来覆盖默认值**
- **`数据库database`：可以通过`${hm.db.database}`来设定，无默认值**

**其中详细的配置如下：**

```YAML
spring:
  datasource:
    url: jdbc:mysql://${hm.db.host:192.168.150.101}:${hm.db.port:3306}/${hm.db.database}?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&serverTimezone=Asia/Shanghai
    driver-class-name: com.mysql.cj.jdbc.Driver
    username: ${hm.db.un:root}
    password: ${hm.db.pw:123}
mybatis-plus:
  configuration:
    default-enum-type-handler: com.baomidou.mybatisplus.core.handlers.MybatisEnumTypeHandler
  global-config:
    db-config:
      update-strategy: not_null
      id-type: auto
```



**然后是统一的日志配置，命名为`shared-log.``yaml`，配置内容如下：**

```YAML
logging:
  level:
    com.hmall: debug
  pattern:
    dateformat: HH:mm:ss:SSS
  file:
    path: "logs/${spring.application.name}"
```

**然后是统一的swagger配置，命名为`shared-swagger.yaml`，配置内容如下：**

```YAML
knife4j:
  enable: true
  openapi:
    title: ${hm.swagger.title:黑马商城接口文档}
    description: ${hm.swagger.description:黑马商城接口文档}
    email: ${hm.swagger.email:zhanghuyi@itcast.cn}
    concat: ${hm.swagger.concat:虎哥}
    url: https://www.itcast.cn
    version: v1.0.0
    group:
      default:
        group-name: default
        api-rule: package
        api-rule-resources:
          - ${hm.swagger.package}
```

**注意，这里的swagger相关配置我们没有写死，例如：**

- **`title`：接口文档标题，我们用了`${hm.swagger.title}`来代替，将来可以有用户手动指定**
- **`email`：联系人邮箱，我们用了`${hm.swagger.email:``zhanghuyi@itcast.cn``}`，默认值是`zhanghuyi@itcast.cn`，同时允许用户利用`${hm.swagger.email}`来覆盖。**



#### 拉取共享配置

**接下来，我们要在微服务拉取共享配置。将拉取到的共享配置与本地的`application.yaml`配置合并，完成项目上下文的初始化。**

**不过，需要注意的是，读取Nacos配置是SpringCloud上下文（`ApplicationContext`）初始化时处理的，发生在项目的引导阶段。然后才会初始化SpringBoot上下文，去读取`application.yaml`。**

**也就是说引导阶段，`application.yaml`文件尚未读取，根本不知道nacos 地址，该如何去加载nacos中的配置文件呢？**

**SpringCloud在初始化上下文的时候会先读取一个名为`bootstrap.yaml`(或者`bootstrap.properties`)的文件，如果我们将nacos地址配置到`bootstrap.yaml`中，那么在项目引导阶段就可以读取nacos中的配置了。**

![](assets\1738504781655.png)

**因此，微服务整合Nacos配置管理的步骤如下：**

**1）引入依赖：**

**在cart-service模块引入依赖：**

```XML
  <!--nacos配置管理-->
  <dependency>
      <groupId>com.alibaba.cloud</groupId>
      <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
  </dependency>
  <!--读取bootstrap文件-->
  <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-bootstrap</artifactId>
  </dependency>
```

**2）新建bootstrap.yaml**

**在cart-service中的resources目录新建一个bootstrap.yaml文件：**

内容如下：

```YAML
spring:
  application:
    name: cart-service # 服务名称
  profiles:
    active: dev
  cloud:
    nacos:
      server-addr: 192.168.150.101 # nacos地址
      config:
        file-extension: yaml # 文件后缀名
        shared-configs: # 共享配置
          - dataId: shared-jdbc.yaml # 共享mybatis配置
          - dataId: shared-log.yaml # 共享日志配置
          - dataId: shared-swagger.yaml # 共享日志配置
```

**3）修改application.yaml**

**由于一些配置挪到了bootstrap.yaml，因此application.yaml需要修改为：**

```YAML
server:
  port: 8082
feign:
  okhttp:
    enabled: true # 开启OKHttp连接池支持
hm:
  swagger:
    title: 购物车服务接口文档
    package: com.hmall.cart.controller
  db:
    database: hm-cart
```

### 配置热更新

**配置热更新：当修改配置文件中的配置时，微服务无需重启即可使配置生效**

**这里我们 以购物车数量的上限为例，进行配置热更新的展示**

**首先，我们在nacos中添加一个配置文件，将购物车的上限数量添加到配置中：**

![](assets\1738507039613.png)

**注意文件的dataId格式：**

```Plain
[服务名]-[spring.active.profile].[后缀名]
```

**文件名称由三部分组成：**

- **`服务名`：我们是购物车服务，所以是`cart-service`**
- **`spring.active.profile`：就是spring boot中的`spring.active.profile`，可以省略，则所有profile共享该配置**
- **`后缀名`：例如yaml**

**这里我们直接使用`cart-service.yaml`这个名称，则不管是dev还是local环境都可以共享该配置。**

**配置内容如下：**

```YAML
hm:
  cart:
    maxAmount: 1 # 购物车商品数量上限
```

**接下来只需要在代码中编写对应的配置类即可**

### 动态路由

**网关的路由配置全部是在项目启动时由`org.springframework.cloud.gateway.route.CompositeRouteDefinitionLocator`在项目启动的时候加载，并且一经加载就会缓存到内存中的路由表内（一个Map），不会改变。也不会监听路由变更，所以，我们无法利用配置热更新来实现路由更新。**

**完成这个需求，我们就需要实现一下两件事情**

**1：监听nacos配置变更的消息**

**2：当配置变更时，将最新的路由信息更新到网关路由表**

#### 监听配置变更

**在Nacos官网中给出了手动监听Nacos配置变更的SDK：**

https://nacos.io/zh-cn/docs/sdk.html

**如果希望 Nacos 推送配置变更，可以使用 Nacos 动态监听配置接口来实现。**

```Java
public void addListener(String dataId, String group, Listener listener)
```

请求参数说明：

| **参数名** | **参数类型** | **描述**                                                     |
| :--------- | :----------- | :----------------------------------------------------------- |
| dataId     | string       | 配置 ID，保证全局唯一性，只允许英文字符和 4 种特殊字符（"."、":"、"-"、"_"）。不超过 256 字节。 |
| group      | string       | 配置分组，一般是默认的DEFAULT_GROUP。                        |
| listener   | Listener     | 监听器，配置变更进入监听器的回调函数。                       |

**示例代码：**

```Java
String serverAddr = "{serverAddr}";
String dataId = "{dataId}";
String group = "{group}";
// 1.创建ConfigService，连接Nacos
Properties properties = new Properties();
properties.put("serverAddr", serverAddr);
ConfigService configService = NacosFactory.createConfigService(properties);
// 2.读取配置
String content = configService.getConfig(dataId, group, 5000);
// 3.添加配置监听器
configService.addListener(dataId, group, new Listener() {
        @Override
        public void receiveConfigInfo(String configInfo) {
        // 配置变更的通知处理
                System.out.println("recieve1:" + configInfo);
        }
        @Override
        public Executor getExecutor() {
                return null;
        }
});
```

**这里核心的步骤有2步：**

- **创建ConfigService，目的是连接到Nacos**
- **添加配置监听器，编写配置变更的通知处理逻辑**

**由于我们采用了`spring-cloud-starter-alibaba-nacos-config`自动装配，因此`ConfigService`已经在`com.alibaba.cloud.nacos.NacosConfigAutoConfiguration`中自动创建好了：**

![](assets\1738576334403.png)

**NacosConfigManager中是负责管理Nacos的ConfigService的，具体代码如下：**

![](assets\1738576467939.png)

**因此，只要我们拿到`NacosConfigManager`就等于拿到了`ConfigService`，第一步就实现了。**

**第二步，编写监听器。虽然官方提供的SDK是ConfigService中的addListener，不过项目第一次启动时不仅仅需要添加监听器，也需要读取配置，因此我们建议使用ConfigService下的这个接口：**

```
String getConfigAndSignListener(String var1, String var2, long var3, Listener var5) throws NacosException;
```

#### 更新路由配置

**更新路由要用到`org.springframework.cloud.gateway.route.RouteDefinitionWriter`这个接口：**

```Java
package org.springframework.cloud.gateway.route;

import reactor.core.publisher.Mono;

/**
 * @author Spencer Gibb
 */
public interface RouteDefinitionWriter {
        /**
     * 更新路由到路由表，如果路由id重复，则会覆盖旧的路由
     */
        Mono<Void> save(Mono<RouteDefinition> route);
        /**
     * 根据路由id删除某个路由
     */
        Mono<Void> delete(Mono<String> routeId);

}
```

**这里更新的路由，也就是RouteDefinition，之前我们见过，包含下列常见字段：**

- **id：路由id**
- **predicates：路由匹配规则**
- **filters：路由过滤器**
- **uri：路由目的地**

**将来我们保存到Nacos的配置也要符合这个对象结构，将来我们以JSON来保存，格式如下：**

```JSON
{
  "id": "item",
  "predicates": [{
    "name": "Path",
    "args": {"_genkey_0":"/items/**", "_genkey_1":"/search/**"}
  }],
  "filters": [],
  "uri": "lb://item-service"
}
```

**以上JSON配置就等同于：**

```YAML
spring:
  cloud:
    gateway:
      routes:
        - id: item
          uri: lb://item-service
          predicates:
            - Path=/items/**,/search/**
```

**OK，我们所需要用到的SDK已经齐全了。**

#### 最终实现

```java
package com.hmall.gateway.routers;

import cn.hutool.json.JSONUtil;
import com.alibaba.cloud.nacos.NacosConfigManager;
import com.alibaba.nacos.api.config.listener.Listener;
import com.alibaba.nacos.api.exception.NacosException;
import lombok.RequiredArgsConstructor;
import lombok.extern.slf4j.Slf4j;
import org.springframework.cloud.gateway.route.RouteDefinition;
import org.springframework.cloud.gateway.route.RouteDefinitionWriter;
import org.springframework.stereotype.Component;
import reactor.core.publisher.Mono;

import javax.annotation.PostConstruct;
import java.util.HashSet;
import java.util.List;
import java.util.Set;
import java.util.concurrent.Executor;

@Component
@Slf4j
@RequiredArgsConstructor
public class DynamicRouterLoader {
    private final NacosConfigManager nacosConfigManager;
    private final RouteDefinitionWriter writer;
    private final String dataId = "gateway-routes.json";
    private final String group = "DEFAULT_GROUP";
    private final Set<String> routeIds = new HashSet<>();

    @PostConstruct
    public void initRouteConfigListener() throws NacosException {
        //1：项目启动时，先拉取一次配置，并添加配置监听器
        String configInfo = nacosConfigManager.getConfigService()
                .getConfigAndSignListener(dataId, group, 5000, new Listener() {
                    //获取一个线程池
                    @Override
                    public Executor getExecutor() {
                        return null;
                    }

                    @Override
                    public void receiveConfigInfo(String configInfo) {
                        //2：监听到配置变更，需要去更新路由表
                        updateConfigInfo(configInfo);
                    }
                });
        //3：第一次读取到配置，也需要更新到路由表
        updateConfigInfo(configInfo);
    }

    public void updateConfigInfo(String configInfo) {
        log.info("监听到路由配置信息：{}", configInfo);
        //1:解析配置文件，转为RouteDefinition对象
        List<RouteDefinition> routeDefinitions = JSONUtil.toList(configInfo, RouteDefinition.class);
        //删除旧的路由
        for (String routeId : routeIds) {
            writer.delete(Mono.just(routeId)).subscribe();
        }
        routeIds.clear();
        for (RouteDefinition routeDefinition : routeDefinitions) {
            //更新路由表
            writer.save(Mono.just(routeDefinition)).subscribe();
            //记录路由Id，便于下一次更新时删除
            routeIds.add(routeDefinition.getId());
        }
    }
}
```

**然后在nacos中配置gateway-routes.json文件**

```json
[
    {
        "id": "item",
        "predicates": [{
            "name": "Path",
            "args": {"_genkey_0":"/items/**", "_genkey_1":"/search/**"}
        }],
        "filters": [],
        "uri": "lb://item-service"
    },
    {
        "id": "cart",
        "predicates": [{
            "name": "Path",
            "args": {"_genkey_0":"/carts/**"}
        }],
        "filters": [],
        "uri": "lb://cart-service"
    },
    {
        "id": "user",
        "predicates": [{
            "name": "Path",
            "args": {"_genkey_0":"/users/**", "_genkey_1":"/addresses/**"}
        }],
        "filters": [],
        "uri": "lb://user-service"
    },
    {
        "id": "trade",
        "predicates": [{
            "name": "Path",
            "args": {"_genkey_0":"/orders/**"}
        }],
        "filters": [],
        "uri": "lb://trade-service"
    },
    {
        "id": "pay",
        "predicates": [{
            "name": "Path",
            "args": {"_genkey_0":"/pay-orders/**"}
        }],
        "filters": [],
        "uri": "lb://pay-service"
    }
]
```

**代码解释**

**首先是代码中的获取的配置信息configInfo,通过getConfigAndSignListener文件设置dataId,groupId则可以拿到对应的存储在nacos中的配置文件，并且添加监听事件，当监听事件监听到配置文件发生变化时，就会触发updateConfigInfo函数去更新配置文件**

**关于获取配置信息，为什么要先拉取配置信息，在设置监听，是项目启动后，第一次拉取配置信息，设置完监听对象，此时刚设置完的监听事件并不会监听到刚刚的配置信息，也就不会触发设置在监听事件内的updateConfigInfo方法，因此为了确保第一次拉取的配置信息也能够配置成功，我们需要在监听方法的外面，再执行一下updateConfigInfo方法，确保第一次拉取配置信息也可以被配置成功。**

**然后关于updateConfigInfo方法，我们使用RouteDefinitionWriter进行修改**



## 服务保护和分布式事务

### 雪崩问题

**微服务调用链路中的某个服务故障，引起整个链路中的所有微服务都不可用，这就是雪崩**

**产生原因：**

**1：微服务相互调用，服务提供者出现故障或阻塞**

**2：服务调用者没有做好异常处理，导致自身故障**

**3：调用链中的所有服务级联失败，导致整个集群故障**

**解决思路：**

**1：尽可能避免出现故障或阻塞，保证代码的健壮性，保证网络畅通，能应对较高的并发请求**

**2：服务调用者做好远程调用异常的备用方案 ，避免故障扩散**

### 服务保护方案

#### 请求限流

**请求限流：限制访问微服务的请求的并发量，避免服务因流量激增出现故障**

**服务故障最重要原因，就是并发太高！解决了这个问题，就能避免大部分故障。当然，接口的并发不是一直很高，而是突发的。因此请求限流，就是限制或控制接口访问的并发流量，避免服务因流量激增而出现故障。**

**请求限流往往会有一个限流器，数量高低起伏的并发请求曲线，经过限流器就变的非常平稳。这就像是水电站的大坝，起到蓄水的作用，可以通过开关控制水流出的大小，让下游水流始终维持在一个平稳的量。**

![](assets\1738658475627.png)

#### 线程隔离

**当一个业务接口响应时间长，而且并发高时，就可能耗尽服务器的线程资源，导致服务内的其它接口受到影响。所以我们必须把这种影响降低，或者缩减影响的范围。线程隔离正是解决这个问题的好办法。**

**线程隔离：也叫做舱壁模式，模拟船舱隔板的防水原理，通过限定每个业务能使用的线程数量而将故障业务隔离，避免故障扩散**

**线程隔离的思想来自轮船的舱壁模式：**

![](assets\1738659804793.png)

**轮船的船舱会被隔板分割为N个相互隔离的密闭舱，假如轮船触礁进水，只有损坏的部分密闭舱会进水，而其他舱由于相互隔离，并不会进水。这样就把进水控制在部分船体，避免了整个船舱进水而沉没。**

**为了避免某个接口故障或压力过大导致整个服务不可用，我们可以限定每个接口可以使用的资源范围，也就是将其“隔离”起来。**

![](assets\1738659927791(1).png)

**如图所示，我们给查询购物车业务限定可用线程数量上限为20，这样即便查询购物车的请求因为查询商品服务而出现故障，也不会导致服务器的线程资源被耗尽，不会影响到其它接口。**

#### 服务熔断

**线程隔离虽然避免了雪崩问题，但故障服务（商品服务）依然会拖慢购物车服务（服务调用方）的接口响应速度。而且商品查询的故障依然会导致查询购物车功能出现故障，购物车业务也变的不可用了。**

**服务熔断：由断路器统计请求的异常比例或慢调用比例，如果超出阈值则会熔断该业务，拦截该接口的请求，熔断期间，所有请求快速失败，全部走fallback逻辑**

**所以，我们要做两件事情：**

- **编写服务降级逻辑：就是服务调用失败后的处理逻辑，根据业务场景，可以抛出异常，也可以返回友好提示或默认数据。**
- **异常统计和熔断：统计服务提供方的异常比例，当比例过高表明该接口会影响到其它服务，应该拒绝调用该接口，而是直接走降级逻辑。**

![](assets\1738659927791(1).png)

#### 服务保护技术

|          | Sentinel                                       | Hystrix                      |
| -------- | ---------------------------------------------- | ---------------------------- |
| 线程隔离 | 信号量隔离                                     | 线程池隔离/信号量隔离        |
| 熔断策略 | 基于慢调用比例或异常比例                       | 基于异常比率                 |
| 限流     | 基于QFS，支持流量整形                          | 有限的支持                   |
| Fallback | 支持                                           | 支持                         |
| 控制台   | 开箱即用，可配置规则，查看秒级监控，机器发现等 | 不完善                       |
| 配置方式 | 基于控制台，重启后失败                         | 基于注解或配置文件，永久生效 |
| 出平方   | alibaba                                        | Netflex                      |

### Sentinel

#### 快速入门

**Sentinel是阿里巴巴开源的一款服务保护框架，目前已经加入SpringCloudAlibaba中。官方网站：**

**https://sentinelguard.io/zh-cn/**

**Sentinel 的使用可以分为两个部分:**

- **核心库（Jar包）：不依赖任何框架/库，能够运行于 Java 8 及以上的版本的运行时环境，同时对 Dubbo / Spring Cloud 等框架也有较好的支持。在项目中引入依赖即可实现服务限流、隔离、熔断等功能。**
- **控制台（Dashboard）：Dashboard 主要负责管理推送规则、监控、管理机器信息等。**

**为了方便监控微服务，我们先把Sentinel的控制台搭建出来。**

**1）下载jar包**

**下载地址：**

**https://github.com/alibaba/Sentinel/releases**

**2）运行**

**将jar包放在任意非中文、不包含特殊字符的目录下，重命名为`sentinel-dashboard.jar`：**

**然后运行如下命令启动控制台：**

```Shell
java -Dserver.port=8090 -Dcsp.sentinel.dashboard.server=localhost:8090 -Dproject.name=sentinel-dashboard -jar sentinel-dashboard.jar
```

**其它启动时可配置参数可参考官方文档：**

**https://github.com/alibaba/Sentinel/wiki/%E5%90%AF%E5%8A%A8%E9%85%8D%E7%BD%AE%E9%A1%B9**

**3）访问**

**访问[http://localhost:8090](http://localhost:8080)页面，就可以看到sentinel的控制台了：**

**需要输入账号和密码，默认都是：sentinel**

**登录后，即可看到控制台，默认会监控sentinel-dashboard服务本身：**

#### 微服务整合

**我们在`cart-service`模块中整合sentinel，连接`sentinel-dashboard`控制台，步骤如下：**

**1）引入sentinel依赖**

```XML
<!--sentinel-->
<dependency>
    <groupId>com.alibaba.cloud</groupId> 
    <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
</dependency>
```

**2）配置控制台**

**修改application.yaml文件，添加下面内容：**

```YAML
spring:
  cloud: 
    sentinel:
      transport:
        dashboard: localhost:8090
```

**3）访问`cart-service`的任意端点**

**重启`cart-service`，然后访问查询购物车接口，sentinel的客户端就会将服务访问的信息提交到`sentinel-dashboard`控制台。并展示出统计信息：**

![](assets\1738667614023.png)

**点击簇点链路菜单，会看到下面的页面：**

![](assets\1738667768404.png)

**所谓簇点链路，就是单机调用链路，是一次请求进入服务后经过的每一个被`Sentinel`监控的资源。默认情况下，`Sentinel`会监控`SpringMVC`的每一个`Endpoint`（接口）。**

**因此，我们看到`/carts`这个接口路径就是其中一个簇点，我们可以对其进行限流、熔断、隔离等保护措施。**

**不过，需要注意的是，我们的SpringMVC接口是按照Restful风格设计，因此购物车的查询、删除、修改等接口全部都是`/carts`路径：**

![](assets\1738668131942.png)

**默认情况下Sentinel会把路径作为簇点资源的名称，无法区分路径相同但请求方式不同的接口，查询、删除、修改等都被识别为一个簇点资源，这显然是不合适的。**

**所以我们可以选择打开Sentinel的请求方式前缀，把`请求方式 + 请求路径`作为簇点资源名：**

首先，在`cart-service`的`application.yml`中添加下面的配置：

```YAML
spring:
  cloud:
    sentinel:
      transport:
        dashboard: localhost:8090
      http-method-specify: true # 开启请求方式前缀
```

**然后，重启服务，通过页面访问购物车的相关接口，可以看到sentinel控制台的簇点链路发生了变化：**

![](assets\1738668233436.png)

#### 请求限流实现

**在簇点链路后面点击流控按钮，即可对其做限流配置：**

![](D:\StudyNote\assets\1738670083215.png)

**在弹出的菜单中这样填写：**

![](assets\1738670207003.png)

**这样就把查询购物车列表这个簇点资源的流量限制在了每秒6个，也就是最大QPS为6.**

#### 线程隔离实现

**首先，我们需要开启OpenFeign对Sentinel的支持**

```YAML
feign:
  sentinel:
    enabled: true # 开启feign对sentinel的支持
```

**需要注意的是，默认情况下SpringBoot项目的tomcat最大线程数是200，允许的最大连接是8492，单机测试很难打满。**

**所以我们需要配置一下cart-service模块的application.yml文件，修改tomcat连接：**

```YAML
server:
  port: 8082
  tomcat:
    threads:
      max: 50 # 允许的最大线程数
    accept-count: 50 # 最大排队等待数量
    max-connections: 100 # 允许的最大连接
```

**然后重启cart-service服务，可以看到查询商品的FeignClient自动变成了一个簇点资源：**

![](assets\1738683564376.png)

**接着我们去配置线程隔离，点击查询商品的FeignClient对应的簇点资源后面的流控按钮：**

![](assets\1738683793582.png)

**在弹出的表单中填写下面内容**

![](assets\1738683809731.png)

**注意，这里勾选的是并发线程数限制，也就是说这个查询功能最多使用5个线程，而不是5QPS。如果查询商品的接口每秒处理2个请求，则5个线程的实际QPS在10左右，而超出的请求自然会被拒绝。**

#### Fallback（降级逻辑）

**触发限流或熔断后的请求不一定要直接报错，也可以返回一些默认数据或者友好提示，用户体验会更好。**

**给FeignClient编写失败后的降级逻辑有两种方式：**

- **方式一：FallbackClass，无法对远程调用的异常做处理**
- **方式二：FallbackFactory，可以对远程调用的异常做处理，我们一般选择这种方式。**

**这里我们演示方式二的失败降级处理。**

**首先在item-service包下的api包下定义一个fallback类**

```
package com.hmall.item.api.fallback;

import com.hmall.common.domain.OrderDetailDTO;
import com.hmall.common.exception.BizIllegalException;
import com.hmall.common.utils.CollUtils;
import com.hmall.item.api.client.ItemClient;
import com.hmall.item.domain.dto.ItemDTO;
import lombok.extern.slf4j.Slf4j;
import org.springframework.cloud.openfeign.FallbackFactory;

import java.util.Collection;
import java.util.List;
@Slf4j
public class ItemClientFallback implements FallbackFactory<ItemClient> {
    @Override
    public ItemClient create(Throwable cause) {
        return new ItemClient() {
            @Override
            public List<ItemDTO> queryItemsByIds(Collection<Long> ids) {
                log.error("远程调用ItemClient#queryItemByIds方法出现异常，参数：{}", ids, cause);
                // 查询购物车允许失败，查询失败，返回空集合
                return CollUtils.emptyList();
            }

            @Override
            public void deductStock(List<OrderDetailDTO> items) {
                // 库存扣减业务需要触发事务回滚，查询失败，抛出异常
                throw new BizIllegalException(cause);
            }
        };
    }
}
```

**这个类继承于FallbackFactory，内部有一个方法可以创建对应泛型的client,这里改方法就是创建一个Itemclient去代替原有的Itemclient进行反馈，里面的方法都是原有的Itemclient接口里的接口，当然我们在这里要重写这些方法**



**然后我们需要将ItemClientFallback注册为一个bean,这里我们需要一个配置类对其进行注册**

```
@Slf4j
public class ItemFeignConfig {
    @Bean
    public ItemClientFallback itemClientFallback() {
        log.info("正在定义ItemClientFallback");
        return new ItemClientFallback();
    }
}
```

**最后在ItemClient上的@FeignClient使用fallbackFactory指定一下即可**

```
package com.hmall.item.api.client;


import com.hmall.common.config.DefaultFeignConfig;
import com.hmall.common.domain.OrderDetailDTO;
import com.hmall.item.api.config.ItemFeignConfig;
import com.hmall.item.api.fallback.ItemClientFallback;
import com.hmall.item.domain.dto.ItemDTO;
import org.springframework.cloud.openfeign.FeignClient;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestParam;

import java.util.Collection;
import java.util.List;

@FeignClient(value = "item-service", fallbackFactory = ItemClientFallback.class, configuration = {DefaultFeignConfig.class, ItemFeignConfig.class})
public interface ItemClient {
    @GetMapping("/items")
    List<ItemDTO> queryItemsByIds(@RequestParam("ids") Collection<Long> ids);

    @PutMapping("/items/stock/deduct")
    void deductStock(@RequestBody List<OrderDetailDTO> items);
}
```

**当然我们需要注意，我们给ItemClient新添加了一个配置类，也需要在注解里把这个类添加进去**

#### 服务熔断实现

**Sentinel中的断路器不仅可以统计某个接口的慢请求比例，还可以统计异常请求比例。当这些比例超出阈值时，就会熔断该接口，即拦截访问该接口的一切请求，降级处理；当该接口恢复正常时，再放行对于该接口的请求。**

**断路器的工作状态切换有一个状态机来控制：**

![](assets\1738756091941.png)

**状态机包括三个状态：**

- **closed：关闭状态，断路器放行所有请求，并开始统计异常比例、慢请求比例。超过阈值则切换到open状态**
- **open：打开状态，服务调用被熔断，访问被熔断服务的请求会被拒绝，快速失败，直接走降级逻辑。Open状态持续一段时间后会进入half-open状态**
- **half-open：半开状态，放行一次请求，根据执行结果来判断接下来的操作。** 
  - **请求成功：则切换到closed状态**
  - **请求失败：则切换到open状态**

**我们可以在控制台通过点击簇点后的`熔断`按钮来配置熔断策略：**

![](assets\1738756573333.png)

**在弹出的表格中这样填写：**

![](assets\1738756590045.png)

**这种是按照慢调用比例来做熔断，上述配置的含义是：**

- **RT超过200毫秒的请求调用就是慢调用**
- **统计最近1000ms内的最少5次请求，如果慢调用比例不低于0.5，则触发熔断**
- **熔断持续时长20s**

**配置完成后，再次利用Jemeter测试，可以发现：**

![](assets\1738757165429.png)

**在一开始一段时间是允许访问的，后来触发熔断后，查询商品服务的接口通过QPS直接为0，所有请求都被熔断了。而查询购物车的本身并没有受到影响。**

**此时整个购物车查询服务的平均RT影响不大：**

![](assets\1738757181029.png)



### 分布式事务

**首先我们看看项目中的下单业务整体流程：**         

 ![](assets\1738841397681.png)                                                                                                                             

**由于订单、购物车、商品分别在三个不同的微服务，而每个微服务都有自己独立的数据库，因此下单过程中就会跨多个数据库完成业务。而每个微服务都会执行自己的本地事务：**

- **交易服务：下单事务**
- **购物车服务：清理购物车事务**
- **库存服务：扣减库存事务**

**整个业务中，各个本地事务是有关联的。因此每个微服务的本地事务，也可以称为分支事务。多个有关联的分支事务一起就组成了全局事务。我们必须保证整个全局事务同时成功或失败。**

**我们知道每一个分支事务就是传统的单体事务，都可以满足ACID特性，但全局事务跨越多个服务、多个数据库，就很难满足了**

**事务并未遵循ACID的原则，归其原因就是参与事务的多个子业务在不同的微服务，跨越了不同的数据库。虽然每个单独的业务都能在本地遵循ACID，但是它们互相之间没有感知，不知道有人失败了，无法保证最终结果的统一，也就无法遵循ACID的事务特性了。**

**这就是分布式事务问题，出现以下情况之一就可能产生分布式事务问题：**

- **业务跨多个服务实现**
- **业务跨多个数据源实现**

### Seata

#### 基本概念

**解决分布式事务的方案有很多，但实现起来都比较复杂，因此我们一般会使用开源的框架来解决分布式事务问题。在众多的开源分布式事务框架中，功能最完善、使用最多的就是阿里巴巴在2019年开源的Seata了。**

**https://seata.io/zh-cn/docs/overview/what-is-seata.html**

**其实分布式事务产生的一个重要原因，就是参与事务的多个分支事务互相无感知，不知道彼此的执行状态。因此解决分布式事务的思想非常简单：**

**就是找一个统一的事务协调者，与多个分支事务通信，检测每个分支事务的执行状态，保证全局事务下的每一个分支事务同时成功或失败即可。大多数的分布式事务框架都是基于这个理论来实现的。**

**Seata也不例外，在Seata的事务管理中有三个重要的角色：**

-  **TC (Transaction Coordinator) - 事务协调者：维护全局和分支事务的状态，协调全局事务提交或回滚。**
-  **TM (Transaction Manager) - 事务管理器：定义全局事务的范围、开始全局事务、提交或回滚全局事务。比如下单操作对应的方法就是全局事务的范围** 
-  **RM (Resource Manager) - 资源管理器：管理分支事务，与TC交谈以注册分支事务和报告分支事务的状态，并驱动分支事务提交或回滚。** 

**Seata的工作架构如图所示：**

![](assets\1738846048177.png)

**其中，TM和RM可以理解为Seata的客户端部分，引入到参与事务的微服务依赖中即可。将来TM和RM就会协助微服务，实现本地分支事务与TC之间交互，实现事务的提交或回滚。**

**而TC服务则是事务协调中心，是一个独立的微服务，需要单独部署。**

#### 部署TC服务

**Seata支持多种存储模式，但考虑到持久化的需要，我们一般选择基于数据库存储。执行课前资料提供的`《seata-tc.sql》`，导入数据库表：**

**课前资料准备了一个seata目录，其中包含了seata运行时所需要的配置文件：其中包含中文注释，大家可以自行阅读。我们将整个seata文件夹拷贝到虚拟机的`/root`目录：**

**需要注意，要确保nacos、mysql都在hm-net网络中。如果某个容器不再hm-net网络，可以参考下面的命令将某容器加入指定网络：**

```Shell
docker network connect [网络名] [容器名]
```

**在虚拟机的`/root`目录执行下面的命令：**

```Shell
docker run --name seata \
-p 8099:8099 \
-p 7099:7099 \
-e SEATA_IP=192.168.230.130 \
-v ./seata:/seata-server/resources \
--privileged=true \
--network hm-net \
-d \
seataio/seata-server:1.5.2
```

#### 微服务集成seata

**为了方便各个微服务集成seata，我们需要把seata配置共享到nacos，因此`trade-service`模块不仅仅要引入seata依赖，还要引入nacos依赖:**

```XML
<!--统一配置管理-->
  <dependency>
      <groupId>com.alibaba.cloud</groupId>
      <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
  </dependency>
  <!--读取bootstrap文件-->
  <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-bootstrap</artifactId>
  </dependency>
  <!--seata-->
  <dependency>
      <groupId>com.alibaba.cloud</groupId>
      <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
  </dependency>
```

**首先在nacos上添加一个共享的seata配置，命名为`shared-seata.yaml`：**

**内容如下：**

```YAML
seata:
  registry: # TC服务注册中心的配置，微服务根据这些信息去注册中心获取tc服务地址
    type: nacos # 注册中心类型 nacos
    nacos:
      server-addr: 192.168.150.101:8848 # nacos地址
      namespace: "" # namespace，默认为空
      group: DEFAULT_GROUP # 分组，默认是DEFAULT_GROUP
      application: seata-server # seata服务名称
      username: nacos
      password: nacos
  tx-service-group: hmall # 事务组名称
  service:
    vgroup-mapping: # 事务组与tc集群的映射关系
      hmall: "default"
```

**然后，改造`trade-service`模块，添加`bootstrap.yaml`：**

**内容如下:**

```YAML
spring:
  application:
    name: trade-service # 服务名称
  profiles:
    active: dev
  cloud:
    nacos:
      server-addr: 192.168.150.101 # nacos地址
      config:
        file-extension: yaml # 文件后缀名
        shared-configs: # 共享配置
          - dataId: shared-jdbc.yaml # 共享mybatis配置
          - dataId: shared-log.yaml # 共享日志配置
          - dataId: shared-swagger.yaml # 共享日志配置
          - dataId: shared-seata.yaml # 共享seata配置
```

**可以看到这里加载了共享的seata配置。**

**然后改造application.yaml文件，内容如下：**

```YAML
server:
  port: 8085
feign:
  okhttp:
    enabled: true # 开启OKHttp连接池支持
  sentinel:
    enabled: true # 开启Feign对Sentinel的整合
hm:
  swagger:
    title: 交易服务接口文档
    package: com.hmall.trade.controller
  db:
    database: hm-trade
```

#### XA模式

##### 基本介绍

**Seata支持四种不同的分布式事务解决方案：**

- **XA**
- **TCC**
- **AT**
- **SAGA**

**这里我们以`XA`模式和`AT`模式来给大家讲解其实现原理。**

**`XA` 规范 是` X/Open` 组织定义的分布式事务处理（DTP，Distributed Transaction Processing）标准，XA 规范 描述了全局的`TM`与局部的`RM`之间的接口，几乎所有主流的数据库都对 XA 规范 提供了支持。**

**A是规范，目前主流数据库都实现了这种规范，实现的原理都是基于两阶段提交。**

**正常情况：**

![](assets\1738860695622(1).png)

**异常情况：**

![](assets\1738860731598.png)

**一阶段：**

- **事务协调者通知每个事务参与者执行本地事务**
- **本地事务执行完成后报告事务执行状态给事务协调者，此时事务不提交，继续持有数据库锁**

**二阶段：**

- **事务协调者基于一阶段的报告来判断下一步操作**
- **如果一阶段都成功，则通知所有事务参与者，提交事务**
- **如果一阶段任意一个参与者失败，则通知所有事务参与者回滚事务**

**Seata对原始的XA模式做了简单的封装和改造，以适应自己的事务模型，基本架构如图：**

![](assets\1738860843078.png)

**`RM`一阶段的工作：**

1. **注册分支事务到`TC`**
2. **执行分支业务sql但不提交**
3. **报告执行状态到`TC`**

**`TC`二阶段的工作：**

1.  **`TC`检测各分支事务执行状态**
   1. **如果都成功，通知所有RM提交事务**
   2. **如果有失败，通知所有RM回滚事务** 

**`RM`二阶段的工作：**

- **接收`TC`指令，提交或回滚事务**

##### 优缺点

**`XA`模式的优点是什么？**

- **事务的强一致性，满足ACID原则**
- **常用数据库都支持，实现简单，并且没有代码侵入**

**`XA`模式的缺点是什么？**

- **因为一阶段需要锁定数据库资源，等待二阶段结束才释放，性能较差**
- **依赖关系型数据库实现事务**

##### 实现步骤

**首先，我们要在配置文件中指定要采用的分布式事务模式。我们可以在Nacos中的共享shared-seata.yaml配置文件中设置：**

```YAML
seata:
  data-source-proxy-mode: XA
```

**其次，我们要利用`@GlobalTransactional`标记分布式事务的入口方法：**

![](assets\1738861052740.png)

#### AT模式

##### 基本原理

**`AT`模式同样是分阶段提交的事务模型，不过缺弥补了`XA`模型中资源锁定周期过长的缺陷。**

**基本流程图：**

![](assets\1738861939570.png)

**阶段一`RM`的工作：**

- **注册分支事务**
- **记录undo-log（数据快照）**
- **执行业务sql并提交**
- **报告事务状态**

**阶段二提交时`RM`的工作：**

- **删除undo-log即可**

**阶段二回滚时`RM`的工作：**

- **根据undo-log恢复数据到更新前**



**我们用一个真实的业务来梳理下AT模式的原理。**

**比如，现在有一个数据库表，记录用户余额：**

| **id** | **money** |
| :----- | :-------- |
| 1      | 100       |

**其中一个分支业务要执行的SQL为：**

```SQL
 update tb_account set money = money - 10 where id = 1
```

**AT模式下，当前分支事务执行流程如下：**

**一阶段：**

1. **`TM`发起并注册全局事务到`TC`**
2. **`TM`调用分支事务**
3. **分支事务准备执行业务SQL**
4. **`RM`拦截业务SQL，根据where条件查询原始数据，形成快照。**

```JSON
{
  "id": 1, "money": 100
}
```

1. **`RM`执行业务SQL，提交本地事务，释放数据库锁。此时 money = 90**
2. **`RM`报告本地事务状态给`TC`**

**二阶段：**

**`TM`通知`TC`事务结束**

**`TC`检查分支事务状态**

​	**如果都成功，则立即删除快照**

​	**如果有分支事务失败，需要回滚。读取快照数据（{"id": 1, "money": 100}），将快照恢复到数据库。此时数据库再次恢复为100**

**流程图：**

![](assets\1739520573723.png)

##### 实现步骤

**首先快照的存储需要一个数据表，并且每一个快照对应一个数据库，这里以hm-cart数据库为例**

![](D:\StudyNote\assets\1738862703935.png)

**然后修改配置，注意，默认配置就是AT模式**

```yaml
seata:
  data-source-proxy-mode: XA
```

**最后给对应的方法加上注解即可**

![](assets\1738861052740.png)

##### AT与XA的区别

**简述`AT`模式与`XA`模式最大的区别是什么？**

- **`XA`模式一阶段不提交事务，锁定资源；`AT`模式一阶段直接提交，不锁定资源。**
- **`XA`模式依赖数据库机制实现回滚；`AT`模式利用数据快照实现数据回滚。**
- **`XA`模式强一致；`AT`模式最终一致**

**可见，AT模式使用起来更加简单，无业务侵入，性能更好。因此企业90%的分布式事务都可以用AT模式来解决。**

## 面试相关

### 分布式事务

**分布式事务，就是指不是在单个服务或单个数据库架构下，产生的事务，例如：**

- **跨数据源的分布式事务**
- **跨服务的分布式事务**
- **综合情况**

**我们之前解决分布式事务问题是直接使用Seata框架的AT模式，但是解决分布式事务问题的方案远不止这一种。**

#### CAP定理

**解决分布式事务问题，需要一些分布式系统的基础知识作为理论指导，首先就是CAP定理。**

**1998年，加州大学的计算机科学家 Eric Brewer 提出，分布式系统有三个指标：**

- **Consistency（一致性）**
- **Availability（可用性）**
- **Partition tolerance （分区容错性）**

**它们的第一个字母分别是 `C`、`A`、`P`。Eric Brewer认为任何分布式系统架构方案都不可能同时满足这3个目标，这个结论就叫做 CAP 定理。**

##### 一致性

**`Consistency`（一致性）：用户访问分布式系统中的任意节点，得到的数据必须一致。**

**比如现在包含两个节点，其中的初始数据是一致的：**

![](assets\1742573649224.png)

**当我们修改其中一个节点的数据时，两者的数据产生了差异：**

![](assets\1742573710194.png)

**要想保住一致性，就必须实现node01 到 node02的数据 同步：**

![](assets\1742573756042.png)

##### 可用性

**Availability （可用性）：用户访问分布式系统时，读或写操作总能成功。**

**只能读不能写，或者只能写不能读，或者两者都不能执行，就说明系统弱可用或不可用。**

##### 分区容错

**`Partition`，就是分区，就是当分布式系统节点之间出现网络故障导致节点之间无法通信的情况：**

![](assets\1742575415836.png)

**如上图，node01和node02之间网关畅通，但是与node03之间网络断开。于是node03成为一个独立的网络分区；node01和node02在一个网络分区。**

**`Tolerance`，就是容错，即便是系统出现网络分区，整个系统也要持续对外提供服务。**

##### 矛盾

**在分布式系统中，网络不能100%保证畅通，也就是说网络分区的情况一定会存在。而我们的系统必须要持续运行，对外提供服务。所以分区容错性（`P`）是硬性指标，所有分布式系统都要满足。而在设计分布式系统时要取舍的就是一致性（`C`）和可用性（`A`）了。**

**假如现在出现了网络分区，如图：**

![](assets\1742575504837.png)

**由于网络故障，当我们把数据写入node01时，可以与node02完成数据同步，但是无法同步给node03。现在有两种选择：**

- **允许用户任意读写，保证可用性。但由于node03无法完成同步，就会出现数据不一致的情况。满足AP**
- **不允许用户写，可以读，直到网络恢复，分区消失。这样就确保了一致性，但牺牲了可用性。满足CP**

**可见，在分布式系统中，`A`和`C`之间只能满足一个。**

#### BASE理论

**既然分布式系统要遵循CAP定理，那么问题来了，我到底是该牺牲一致性还是可用性呢？如果牺牲了一致性，出现数据不一致该怎么处理？**

**人们在总结系统设计经验时，最终得到了一些心得：**

- **Basically Available （基本可用）：分布式系统在出现故障时，允许损失部分可用性，即保证核心可用。**
- **Soft State（软状态）：在一定时间内，允许出现中间状态，比如临时的不一致状态。**
- **Eventually Consistent（最终一致性）：虽然无法保证强一致性，但是在软状态结束后，最终达到数据一致。**

**以上就是BASE理论。**

**简单来说，BASE理论就是一种取舍的方案，不再追求完美，而是最终达成目标。因此解决分布式事务的思想也是这样，有两个方向：**

- **AP思想：各个子事务分别执行和提交，无需锁定数据。允许出现结果不一致，然后采用弥补措施恢复，实现最终一致即可。例如`AT`模式就是如此**
- **CP思想：各个子事务执行后不要提交，而是等待彼此结果，然后同时提交或回滚。在这个过程中锁定资源，不允许其它人访问，数据处于不可用状态，但能保证一致性。例如`XA`模式**

#### AT模式下脏写问题

**我们先回顾一下AT模式的流程，AT模式也分为两个阶段：**

**第一阶段是记录数据快照，执行并提交事务：**

![](assets\1742634452774.png)

**第二阶段根据阶段一的结果来判断：**

- **如果每一个分支事务都成功，则事务已经结束（因为阶段一已经提交），因此删除阶段一的快照即可**
- **如果有任意分支事务失败，则需要根据快照恢复到更新前数据。然后删除快照**

![](assets\1742634514788.png)

**这种模式在大多数情况下（99%）并不会有什么问题，不过在极端情况下，特别是多线程并发访问AT模式的分布式事务时，有可能出现脏写问题，如图：**

![](assets\1742634591189.png)

**解决思路就是引入了全局锁的概念。在释放DB锁之前，先拿到全局锁。避免同一时刻有另外一个事务来操作当前数据。需要注意这里的全局锁是逻辑锁，由seata中的tc维护，而非数据库的锁，因此不受seata管理的事务也不受此锁的影响**

![](assets\1742634728882.png)

**当然，如果在这之中出现了一个不受seata管理的事务，去修改数据库，也会出现脏写的问题，这种情况下，seata也提供了一个机制，用于告知开发人员，但出现这种情况时，需要人工介入**

![](assets\1742635742101.png)

#### TCC模式

**TCC模式与AT模式非常相似，每阶段都是独立事务，不同的是TCC通过人工编码来实现数据恢复。需要实现三个方法：**

-  **`try`：资源的检测和预留；** 
-  **`confirm`：完成资源操作业务；要求 `try` 成功 `confirm` 一定要能成功。** 
-  **`cancel`：预留资源释放，可以理解为try的反向操作。** 

##### 流程分析

**举例，一个扣减用户余额的业务。假设账户A原来余额是100，需要余额扣减30元。**

**阶段一（ Try ）：检查余额是否充足，如果充足则冻结金额增加30元，可用余额扣除30**

**初始余额：**

![](assets\1742651496030(1).png)

**余额充足，可以冻结：**

![](assets\1742651544107(1).png)

**此时，总金额 = 冻结金额 + 可用金额，数量依然是100不变。事务直接提交无需等待其它事务。**

**阶段二（Confirm)：假如要提交（Confirm），之前可用金额已经扣减，并转移到冻结金额。因此可用金额不变，直接冻结金额扣减30即可：**

![](assets\1742651590345(1).png)

**此时，总金额 = 冻结金额 + 可用金额 = 0 + 70  = 70元**

**阶段二(Canncel)：如果要回滚（Cancel），则释放之前冻结的金额，也就是冻结金额扣减30，可用余额增加30**

![](assets\1742651636871(1).png)

**这里的冻结操作，。可以在数据库添加一个字段冻结余额，用于记录冻结的资源，在进行扣减的操作的时候，可以同时修改这行数据的冻结余额字段和余额字段即可**

**TCC工作模型**

![](assets\1742652661525.png)

##### 事务悬挂和空回滚

**假如一个分布式事务中包含两个分支事务，try阶段，一个分支成功执行，另一个分支事务阻塞：**

![](assets\1742652280203.png)

**如果阻塞时间太长，可能导致全局事务超时而触发二阶段的`cancel`操作。两个分支事务都会执行cancel操作：**

![](assets\1742652344417.png)

**要知道，其中一个分支是未执行`try`操作的，直接执行了`cancel`操作，反而会导致数据错误。因此，这种情况下，尽管`cancel`方法要执行，但其中不能做任何回滚操作，这就是空回滚。**

**对于整个空回滚的分支事务，将来try方法阻塞结束依然会执行。但是整个全局事务其实已经结束了，因此永远不会再有confirm或cancel，也就是说这个事务执行了一半，处于悬挂状态，这就是业务悬挂问题。**

**以上问题都需要我们在编写try、cancel方法时处理。**

##### 总结

**TCC模式的每个阶段是做什么的？**

- **Try：资源检查和预留**
- **Confirm：业务执行和提交**
- **Cancel：预留资源的释放**

**TCC的优点是什么？**

- **一阶段完成直接提交事务，释放数据库资源，性能好**
- **相比AT模型，无需生成快照，无需使用全局锁，性能最强**
- **不依赖数据库事务，而是依赖补偿操作，可以用于非事务型数据库**

**TCC的缺点是什么？**

- **有代码侵入，需要人为编写try、Confirm和Cancel接口，太麻烦**
- **软状态，事务是最终一致**
- **需要考虑Confirm和Cancel的失败情况，做好幂等处理、事务悬挂和空回滚处理**

#### 最大努力通知

**最大努力通知是一种最终一致性的分布式事务解决方案。顾明思议，就是通过消息通知的方式来通知事务参与者完成业务执行，如果执行失败会多次通知。无需任何分布式事务组件介入。**

![](D:\StudyNote\assets\1742653000205(1).png)

**在这个过程中，服务1会尽可能的通知服务二，一直失败重试，知道超过规定时间，当然该过程还需要依赖消息中间件的可靠性，如果想尽可能保证其稳定，可以直接去掉消息中间件，而采用服务调用的方式，只不过这个服务调用出现失败时，需要一直的尝试**

### 注册中心

#### 环境隔离

**企业实际开发中，往往会搭建多个运行环境，例如：**

- **开发环境**
- **测试环境**
- **预发布环境**
- **生产环境**

**这些不同环境之间的服务和数据之间需要隔离。**

**还有的企业中，会开发多个项目，共享nacos集群。此时，这些项目之间也需要把服务和数据隔离。**

**因此，Nacos提供了基于`namespace`的环境隔离功能。具体的隔离层次如图所示：**

![](assets\1742653974809(1).png)

**说明：**

- **Nacos中可以配置多个`namespace`，相互之间完全隔离。默认的`namespace`名为`public`**
- **`namespace`下还可以继续分组，也就是group ，相互隔离。 默认的group是`DEFAULT_GROUP`**
- **`group`之下就是服务和配置了**

##### 创建namespace

**nacos提供了一个默认的`namespace`，叫做`public`：**

![](assets\1742654321680(1).png)

**默认所有的服务和配置都属于这个`namespace`，当然我们也可以自己创建新的`namespace`：**

![](assets\1742654555467(1).png)

**然后填写表单：**

![](assets\1742654617056.png)

**添加完成后，可以在页面看到我们新建的`namespace`，并且Nacos为我们自动生成了一个命名空间id：**

![](assets\1742654662960.png)

**我们切换到配置列表页，你会发现`dev`这个命名空间下没有任何配置：**

![](assets\1742654721523.png)

##### 微服务配置namespace

**默认情况下，所有的微服务注册发现、配置管理都是走`public`这个命名空间。如果要指定命名空间则需要修改`application.yml`文件。**

**比如，我们修改`item-service`服务的bootstrap.yml文件，添加服务发现配置，指定其`namespace`当然我们也可以给共享配置文件指定namespace：**

```YAML
spring:
  application:
    name: item-service # 服务名称
  profiles:
    active: dev
  cloud:
    nacos:
      server-addr: 192.168.150.101 # nacos地址
      discovery: # 服务发现配置
        namespace: 8c468c63-b650-48da-a632-311c75e6d235 # 设置namespace，必须用id
      config:
        file-extension: yaml # 文件后缀名
          namespace: 8c468c63-b650-48da-a632-311c75e6d235 # 设置namespace，必须用id
      # 。。。略
```

**此时启动对应的服务就会发现它已经出现对应的命名空间下了**

#### 分级模型

**在一些大型应用中，同一个服务可以部署很多实例。而这些实例可能分布在全国各地的不同机房。由于存在地域差异，网络传输的速度会有很大不同，因此在做服务治理时需要区分不同机房的实例。**

**例如item-service，我们可以部署3个实例：**

- **127.0.0.1:8081**
- **127.0.0.1:8082**
- **127.0.0.1:8083**

**假如这些实例分布在不同机房，例如：**

- **127.0.0.1:8081，在上海机房**
- **127.0.0.1:8082，在上海机房**
- **127.0.0.1:8083，在杭州机房**

**Nacos中提供了集群（`cluster`）的概念，来对应不同机房。也就是说，一个服务（`service`）下可以有很多集群（`cluster`），而一个集群（`cluster`）中下又可以包含很多实例（`instance`）。**

**如图：**

![](assets\1742656080164.png)

**因此，结合我们上一节学习的`namespace`命名空间的知识，任何一个微服务的实例在注册到Nacos时，都会生成以下几个信息，用来确认当前实例的身份，从外到内依次是：**

- **namespace：命名空间**
- **group：分组**
- **service：服务名**
- **cluster：集群**
- **instance：实例，包含ip和端口**

**这就是nacos中的服务分级模型。**

**在Nacos内部会有一个服务实例的注册表，是基于Map实现的，其结构与分级模型的对应关系如下：**

![](assets\1742656128902.png)

**查看nacos控制台，会发现默认情况下所有服务的集群都是default：**

![](assets\1742656226159(1).png)

**如果我们要修改服务所在集群，只需要修改`bootstrap.yml`即可：**

```YAML
spring:
  cloud:
    nacos:
      discovery:
        cluster-name: BJ # 集群名称，自定义
```

**我们修改`item-service`的`bootstrap.yml`，然后重新创建一个实例：**

**再次查看nacos：**

![](assets\1742656324579.png)

**发现8084这个新的实例确实属于`BJ`这个集群了。**

#### Eureka 

**Eureka是Netflix公司开源的一个服务注册中心组件，早期版本的SpringCloud都是使用Eureka作为注册中心。由于Eureka和Nacos的starter中提供的功能都是基于SpringCloudCommon规范，因此两者使用起来差别不大。**

**这里我们使用一个简单的项目来演示一下**

![](assets\1742657079833.png)

**结构说明：**

- **`eureka-server`：Eureka的服务端，也就是注册中心。没错，Eureka服务端要自己创建项目**
- **`order-service`：订单服务，是一个服务调用者，查询订单的时候要查询用户**
- **`user-service`：用户服务，是一个服务提供者，对外暴露查询用户的接口**

**这里我们看一下eureka-server项目**

![](assets\1742657161108.png)

**可以看到它只有一个启动类和一个配置文件**

```java
package cn.itcast.eureka;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@EnableEurekaServer
@SpringBootApplication
public class EurekaApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaApplication.class, args);
    }
}
```

**可以看到，只需要在application类加@EnableEurekaServer即可**

```yml
server:
  port: 10086
spring:
  application:
    name: eurekaserver
eureka:
  client:
    service-url:
      defaultZone: http://127.0.0.1:10086/eureka
```

**配置文件里只需要配置服务端口号，服务名称，以及Eureka自己的地址**

**当然除了上面的东西之外，还需要引入依赖**

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

**启动以后，访问`localhost:10086`即可查看到Eureka的控制台，相对于Nacos来说简陋了很多：**

![](assets\1742657443173.png)

**微服务引入Eureka的方式也极其简单，分两步：**

- **引入`eureka-client`依赖**
- **配置`eureka`地址**

```xml
<!--eureka-client-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

```yml
eureka:
  client:
    service-url:
      defaultZone: http://127.0.0.1:10086/eureka
```

#### Eureka和Nacos对比

**Eureka和Nacos都能起到注册中心的作用，用法基本类似。但还是有一些区别的，例如：**

- **Nacos支持配置管理，而Eureka则不支持。**

**而且服务注册发现上也有区别，我们来做一个实验：**

**我们停止`user-service`服务，然后观察Eureka控制台，你会发现很长一段时间过去后，Eureka服务依然没有察觉`user-service`的异常状态。**

**这与Eureka的健康检测机制有关。在Eureka中，健康检测的原理如下：**

- **微服务启动时注册信息到Eureka，这点与Nacos一致。**
- **微服务每隔30秒向Eureka发送心跳请求，报告自己的健康状态。Nacos中默认是5秒一次。**
- **Eureka如果90秒未收到心跳，则认为服务疑似故障，可能被剔除。Nacos中则是15秒超时，30秒剔除。**
- **Eureka如果发现超过85%比例的服务都心跳异常，会认为是自己的网络异常，暂停剔除服务的功能。**
- **Eureka每隔60秒执行一次服务检测和清理任务；Nacos是每隔5秒执行一次。**

**综上，你会发现Eureka是尽量不剔除服务，避免“误杀”，宁可放过一千，也不错杀一个。这就导致当服务真的出现故障时，迟迟不会被剔除，给服务的调用者带来困扰。**

**不仅如此，当Eureka发现服务宕机并从服务列表中剔除以后，并不会将服务列表的变更消息推送给所有微服务。而是等待微服务自己来拉取时发现服务列表的变化。而微服务每隔30秒才会去Eureka更新一次服务列表，进一步推迟了服务宕机时被发现的时间。**

**而Nacos中微服务除了自己定时去Nacos中拉取服务列表以外，Nacos还会在服务列表变更时主动推送最新的服务列表给所有的订阅者。**

**综上，Eureka和Nacos的相似点有：**

- **都支持服务注册发现功能**
- **都有基于心跳的健康监测功能**
- **都支持集群，集群间数据同步默认是AP模式，即最全高可用性**

**Eureka和Nacos的区别有：**

- **Eureka的心跳是30秒一次，Nacos则是5秒一次**
- **Eureka如果90秒未收到心跳，则认为服务疑似故障，可能被剔除。Nacos中则是15秒超时，30秒剔除。**
- **Eureka每隔60秒执行一次服务检测和清理任务；Nacos是每隔5秒执行一次。**
- **Eureka只能等微服务自己每隔30秒更新一次服务列表；Nacos即有定时更新，也有在服务变更时的广播推送**
- **Eureka仅有注册中心功能，而Nacos同时支持注册中心、配置管理**
- **Eureka和Nacos都支持集群，而且默认都是AP模式，不过这里nacos支持CP模式**
- **Nacos支持服务端主动检测提供者状态，临时实例采用心跳模式，永久实例采用主动检测，不过默认都是临时实例的模式**

**这里我们放一张对比图**

![](assets\1742658397879(1).png)

### 远程调用

#### 负载均衡原理

**在SpringCloud的早期版本中，负载均衡都是有Netflix公司开源的Ribbon组件来实现的，甚至Ribbon被直接集成到了Eureka-client和Nacos-Discovery中。**

**但是自SpringCloud2020版本开始，已经弃用Ribbon，改用Spring自己开源的Spring Cloud LoadBalancer了，我们使用的OpenFeign的也已经与其整合。**

**接下来我们就通过源码分析，来看看OpenFeign底层是如何实现负载均衡功能的。**

##### 源码跟踪

**要弄清楚OpenFeign的负载均衡原理，最佳的办法肯定是从FeignClient的请求流程入手。**

**首先，我们在`com.hmall.cart.service.impl.CartServiceImpl`中的`queryMyCarts`方法中打一个断点。然后在swagger页面请求购物车列表接口。**

**进入断点后，观察`ItemClient`这个接口：**

![](assets\1742743512817.png)

**你会发现ItemClient是一个代理对象，而代理的处理器则是`SentinelInvocationHandler`。这是因为我们项目中引入了`Sentinel`导致。**

**我们进入`SentinelInvocationHandler`类中的`invoke`方法看看：**

![](assets\1742743570624.png)

**可以看到这里是先获取被代理的方法的处理器`MethodHandler`，接着，Sentinel就会开启对簇点资源的监控：**

![](assets\1742743640414.png)

**开启Sentinel的簇点资源监控后，就可以调用处理器了，我们尝试跟入，会发现有两种实现：**

![](assets\1742743689696.png)

**这其实就是OpenFeign远程调用的处理器了。继续跟入会进入`SynchronousMethodHandler`这个实现类：**

![](assets\1742743755618.png)

**在上述方法中，会循环尝试调用`executeAndDecode()`方法，直到成功或者是重试次数达到Retryer中配置的上限。**

**我们继续跟入`executeAndDecode()`方法：**

![](assets\1742743803265.png)

**`executeAndDecode()`方法最终会利用`client`去调用`execute()`方法，发起远程调用。**

**这里的client的类型是`feign.Client`接口，其下有很多实现类：**

![](assets\1742743890513.png)

**由于我们项目中整合了seata，所以这里client对象的类型是`SeataFeignBlockingLoadBalancerClient`，内部实现如下：**

![](assets\1742744051079.png)

**这里直接调用了其父类，也就是`FeignBlockingLoadBalancerClient`的`execute`方法，来看一下：**

![](assets\1742744127261.png)

**整段代码中核心的有4步：**

- **从请求的`URI`中找出`serviceId`**
- **利用`loadBalancerClient`，根据`serviceId`做负载均衡，选出一个实例`ServiceInstance`**
- **用选中的`ServiceInstance`的`ip`和`port`替代`serviceId`，重构`URI`**
- **向真正的URI发送请求**

**所以负载均衡的关键就是这里的loadBalancerClient，类型是`org.springframework.cloud.client.loadbalancer.LoadBalancerClient`，这是`Spring-Cloud-Common`模块中定义的接口，只有一个实现类：**

![](assets\1742744221076.png)

**而这里的`org.springframework.cloud.client.loadbalancer.BlockingLoadBalancerClient`正是`Spring-Cloud-LoadBalancer`模块下的一个类：**

![](assets\1742744356985.png)

**我们继续跟入其`BlockingLoadBalancerClient#choose()`方法：**

![](assets\1742744433082.png)

**图中代码的核心逻辑如下：**

- **根据serviceId找到这个服务采用的负载均衡器（`ReactiveLoadBalancer`），也就是说我们可以给每个服务配不同的负载均衡算法。**
- **利用负载均衡器（`ReactiveLoadBalancer`）中的负载均衡算法，选出一个服务实例**

**`ReactiveLoadBalancer`是`Spring-Cloud-Common`组件中定义的负载均衡器接口规范，而`Spring-Cloud-Loadbalancer`组件给出了两个实现：**

![](assets\1742744477829.png)

**默认的实现是`RoundRobinLoadBalancer`，即轮询负载均衡器。负载均衡器的核心逻辑如下：**

![](assets\1742744525210.png)

**核心流程就是两步：**

- **利用`ServiceInstanceListSupplier#get()`方法拉取服务的实例列表，这一步是采用响应式编程**
- **利用本类，也就是`RoundRobinLoadBalancer`的`getInstanceResponse()`方法挑选一个实例，这里采用了轮询算法来挑选。**

**这里的ServiceInstanceListSupplier有很多实现：**

![](assets\1742744570376.png)

**其中CachingServiceInstanceListSupplier采用了装饰模式，加了服务实例列表缓存，避免每次都要去注册中心拉取服务实例列表。而其内部是基于`DiscoveryClientServiceInstanceListSupplier`来实现的。**

**在这个类的构造函数中，就会异步的基于DiscoveryClient去拉取服务的实例列表：**

![](assets\1742744614405.png)

##### 流程梳理

**根据之前的分析，我们会发现Spring在整合OpenFeign的时候，实现了`org.springframework.cloud.openfeign.loadbalancer.FeignBlockingLoadBalancerClient`类，其中定义了OpenFeign发起远程调用的核心流程。也就是四步：**

- **获取请求中的`serviceId`**
- **根据`serviceId`负载均衡，找出一个可用的服务实例**
- **利用服务实例的`ip`和`port`信息重构url**
- **向真正的url发起请求**

**而具体的负载均衡则是不是由`OpenFeign`组件负责。而是分成了负载均衡的接口规范，以及负载均衡的具体实现两部分。**

**负载均衡的接口规范是定义在`Spring-Cloud-Common`模块中，包含下面的接口：**

- **`LoadBalancerClient`：负载均衡客户端，职责是根据serviceId最终负载均衡，选出一个服务实例**
- **`ReactiveLoadBalancer`：负载均衡器，负责具体的负载均衡算法**

**OpenFeign的负载均衡是基于`Spring-Cloud-Common`模块中的负载均衡规则接口，并没有写死具体实现。这就意味着以后还可以拓展其它各种负载均衡的实现。**

**不过目前`SpringCloud`中只有`Spring-Cloud-Loadbalancer`这一种实现。**

**`Spring-Cloud-Loadbalancer`模块中，实现了`Spring-Cloud-Common`模块的相关接口，具体如下：**

- **`BlockingLoadBalancerClient`：实现了`LoadBalancerClient`，会根据serviceId选出负载均衡器并调用其算法实现负载均衡。**
- **`RoundRobinLoadBalancer`：基于轮询算法实现了`ReactiveLoadBalancer`**
- **`RandomLoadBalancer`：基于随机算法实现了`ReactiveLoadBalancer`，**

**这样一来，整体思路就非常清楚了，流程图如下：**

![](assets\1742744677373.png)



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

### **IService接口批处理操作**

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



# Maven

## 依赖相关

**在pom.xml文件中添加依赖**

```xml
<dependencies>
	<dependency>
	<groupId>ch.qos.logback</groupId>
	<artifactId>logback-classic</artifactId>
	<version>1.2.3</version>
	</dependency>
</dependencies>
```

**需注意：依赖具有传递性，如果你不需要某些依赖，可以使用排除依赖,通过以下方式便可以把A项目所依赖的项目B的某个依赖排除**

```xml
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

