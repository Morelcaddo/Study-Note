# Apache Commons

**Apache Commons包含了很多开源的工具，用于解决平时编程经常会遇到的问题，减少重复劳动。下面是我这几年做开发过程中自己用过的工具类做简单介绍。**

## **Commons简介**

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

## **Maven依赖 **

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



## **commons-beanutils** 

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



## **commons-betwixt** 

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



## **commons-codec** 

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



## **commons-collections**

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



## **commons-compress** 

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



## commons-configuration

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



## **commons-dbcp**

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



## **commons-dbutils** 

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



## **commons-email** 

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



## **commons-fileupload**

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



## **commons-httpclient**

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



## **commons-io**

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



## **commos-lang** 

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

## **commos-logging**

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

## **Validator** 

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

