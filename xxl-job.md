# **xxl-job**

## **分布式任务调度**

### **spring task定时任务框架的缺点**

**\- 做集群任务的重复执行问题**

**\- cron表达式定义在代码之中，修改不方便**

**\- 定时任务失败了，无法重试也没有统计**

**\- 如果任务量过大，不能有效的分片执行**

### **什么是分布式任务调度**

**当前软件的架构已经开始向分布式架构转变，将单体结构拆分为若干服务，服务之间通过网络交互来完成业务处理。在分布式架构下，一个服务往往会部署多个实例来运行我们的业务，如果在这种分布式系统环境下运行任务调度，我们称之为分布式任务调度。**

**![image-20210729230059884](assets/image-20210729230059884.png)**

**将任务调度程序分布式构建，这样就可以具有分布式系统的特点，并且提高任务的调度处理能力：**

**1、并行任务调度**

**并行任务调度实现靠多线程，如果有大量任务需要调度，此时光靠多线程就会有瓶颈了，因为一台计算机CPU的处理能力是有限的。**

**如果将任务调度程序分布式部署，每个结点还可以部署为集群，这样就可以让多台计算机共同去完成任务调度，我们可以将任务分割为若干个分片，由不同的实例并行执行，来提高任务调度的处理效率。**

**2、高可用**

**若某一个实例宕机，不影响其他实例来执行任务。**

**3、弹性扩容**

**当集群中增加实例就可以提高并执行任务的处理效率。**

**4、任务管理与监测**

**对系统中存在的所有定时任务进行统一的管理及监测。让开发人员及运维人员能够时刻了解任务执行情况，从而做出快速的应急处理响应。**

**分布式任务调度面临的问题：**

**当任务调度以集群方式部署，同一个任务调度可能会执行多次，例如：电商系统定期发放优惠券，就可能重复发放优惠券，对公司造成损失，信用卡还款提醒就会重复执行多次，给用户造成烦恼，所以我们需要控制相同的任务在多个运行实例上只执行一次。常见解决方案：**

- **分布式锁，多个实例在任务执行前首先需要获取锁，如果获取失败那么就证明有其他服务已经在运行，如果获取成功那么证明没有服务在运行定时任务，那么就可以执行。**
- **ZooKeeper选举，利用ZooKeeper对Leader实例执行定时任务，执行定时任务的时候判断自己是否是Leader，如果不是则不执行，如果是则执行业务逻辑，这样也能达到目的。**

###  **xxl-Job简介**

**针对分布式任务调度的需求，市场上出现了很多的产品：**

**1） TBSchedule：淘宝推出的一款非常优秀的高性能分布式调度框架，目前被应用于阿里、京东、支付宝、国美等很多互联网企业的流程调度系统中。但是已经多年未更新，文档缺失严重，缺少维护。**

**2） XXL-Job：大众点评的分布式任务调度平台，是一个轻量级分布式任务调度平台, 其核心设计目标是开发迅速、学习简单、轻量级、易扩展。现已开放源代码并接入多家公司线上产品线，开箱即用。**

**3）Elastic-job：当当网借鉴TBSchedule并基于quartz 二次开发的弹性分布式任务调度系统，功能丰富强大，采用zookeeper实现分布式协调，具有任务高可用以及分片功能。**

**4）Saturn： 唯品会开源的一个分布式任务调度平台，基于Elastic-job，可以全域统一配置，统一监**
**控，具有任务高可用以及分片功能。** 

**XXL-JOB是一个分布式任务调度平台，其核心设计目标是开发迅速、学习简单、轻量级、易扩展。现已开放源代码并接入多家公司线上产品线，开箱即用。**

**源码地址：https://gitee.com/xuxueli0323/xxl-job**

**文档地址：https://www.xuxueli.com/xxl-job/**

**特性**

- **简单灵活**
  **提供Web页面对任务进行管理，管理系统支持用户管理、权限控制；**
  **支持容器部署；**
  **支持通过通用HTTP提供跨平台任务调度；**
- **丰富的任务管理功能**
  **支持页面对任务CRUD操作；**
  **支持在页面编写脚本任务、命令行任务、Java代码任务并执行；**
  **支持任务级联编排，父任务执行结束后触发子任务执行；**
  **支持设置指定任务执行节点路由策略，包括轮询、随机、广播、故障转移、忙碌转移等；**
  **支持Cron方式、任务依赖、调度中心API接口方式触发任务执行**
- **高性能**
  **任务调度流程全异步化设计实现，如异步调度、异步运行、异步回调等，有效对密集调度进行流量削峰；**
- **高可用**
  **任务调度中心、任务执行节点均 集群部署，支持动态扩展、故障转移**
  **支持任务配置路由故障转移策略，执行器节点不可用是自动转移到其他节点执行**
  **支持任务超时控制、失败重试配置**
  **支持任务处理阻塞策略：调度当任务执行节点忙碌时来不及执行任务的处理策略，包括：串行、抛弃、覆盖策略**
- **易于监控运维**
  **支持设置任务失败邮件告警，预留接口支持短信、钉钉告警；**
  **支持实时查看任务执行运行数据统计图表、任务进度监控数据、任务完整执行日志；**

### **配置部署调度中心-docker安装**

**1.创建mysql容器，初始化xxl-job的SQL脚本**

```shell
docker run -p 3306:3306 --name mysql57 \
-v /opt/mysql/conf:/etc/mysql \
-v /opt/mysql/logs:/var/log/mysql \
-v /opt/mysql/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=root \
-d mysql:5.7
```

**2.拉取镜像**

```shell
docker pull xuxueli/xxl-job-admin:2.3.0
```

**3.创建容器**

```shell
docker run -e PARAMS="--spring.datasource.url=jdbc:mysql://192.168.200.130:3306/xxl_job?Unicode=true&characterEncoding=UTF-8 \
--spring.datasource.username=root \
--spring.datasource.password=123" \
-p 8888:8080 -v /tmp:/data/applogs \
--name xxl-job-admin --restart=always  -d xuxueli/xxl-job-admin:2.3.0
```

### **入门案例编写**

####  **登录调度中心，点击下图所示“新建任务”按钮，新建示例任务**

**![image-20210729232146585](assets\image-20210729232146585.png)**

#### **创建xxljob-demo项目，导入依赖**

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!--xxl-job-->
    <dependency>
        <groupId>com.xuxueli</groupId>
        <artifactId>xxl-job-core</artifactId>
        <version>2.3.0</version>
    </dependency>
</dependencies>
```

#### **application.yml配置**

```yaml
server:
  port: 8881


xxl:
  job:
    admin:
      addresses: http://192.168.200.130:8888/xxl-job-admin
    executor:
      appname: xxl-job-executor-sample
      port: 9999

```

#### **新建配置类**

```java
package com.heima.xxljob.config;

import com.xxl.job.core.executor.impl.XxlJobSpringExecutor;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

/**
 * xxl-job config
 *
 * @author xuxueli 2017-04-28
 */
@Configuration
public class XxlJobConfig {
    private Logger logger = LoggerFactory.getLogger(XxlJobConfig.class);

    @Value("${xxl.job.admin.addresses}")
    private String adminAddresses;

    @Value("${xxl.job.executor.appname}")
    private String appname;

    @Value("${xxl.job.executor.port}")
    private int port;


    @Bean
    public XxlJobSpringExecutor xxlJobExecutor() {
        logger.info(">>>>>>>>>>> xxl-job config init.");
        XxlJobSpringExecutor xxlJobSpringExecutor = new XxlJobSpringExecutor();
        xxlJobSpringExecutor.setAdminAddresses(adminAddresses);
        xxlJobSpringExecutor.setAppname(appname);
        xxlJobSpringExecutor.setPort(port);
        return xxlJobSpringExecutor;
    }


}
```

#### **任务代码，重要注解:@XxlJob(“JobHandler”)**

```java
package com.heima.xxljob.job;

import com.xxl.job.core.handler.annotation.XxlJob;
import org.springframework.stereotype.Component;

@Component
public class HelloJob {


    @XxlJob("demoJobHandler")
    public void helloJob(){
        System.out.println("简单任务执行了。。。。");

    }
}
```

#### **测试-单节点**

- **启动微服务**

- **在xxl-job的调度中心中启动任务**

### **任务详解-执行器**

- **执行器：任务的绑定的执行器，任务触发调度时将会自动发现注册成功的执行器, 实现任务自动发现功能;** 

- **另一方面也可以方便的进行任务分组。每个任务必须绑定一个执行器**

**![image-20210729232926534](assets\image-20210729232926534.png)**

![image-20210729232825564](assets\image-20210729232825564.png)

 **以下是执行器的属性说明：**

| **属性名称** | **说明**                                                     |
| ------------ | ------------------------------------------------------------ |
| **AppName**  | **是每个执行器集群的唯一标示AppName, 执行器会周期性以AppName为对象进行自动注册。可通过该配置自动发现注册成功的执行器, 供任务调度时使用;** |
| **名称**     | **执行器的名称, 因为AppName限制字母数字等组成,可读性不强, 名称为了提高执行器的可读性;** |
| **排序**     | **执行器的排序, 系统中需要执行器的地方,如任务新增, 将会按照该排序读取可用的执行器列表;** |
| **注册方式** | **调度中心获取执行器地址的方式；**                           |
| **机器地址** | **注册方式为"手动录入"时有效，支持人工维护执行器的地址信息；** |

**自动注册和手动注册的区别和配置**

**![image-20210729233016355](assets\image-20210729233016355.png)**

### **任务详解-基础配置**

**![image-20210729233926457](assets\image-20210729233926457.png)**

**基础配置**

- **执行器：每个任务必须绑定一个执行器, 方便给任务进行分组**

- **任务描述：任务的描述信息，便于任务管理；**

- **负责人：任务的负责人；**

- **报警邮件：任务调度失败时邮件通知的邮箱地址，支持配置多邮箱地址，配置多个邮箱地址时用逗号分隔**

**![image-20210729234009010](assets\image-20210729234009010.png)**

**调度配置**

- **调度类型：**
  - **无：该类型不会主动触发调度；**
  - **CRON：该类型将会通过CRON，触发任务调度；**
  - **固定速度：该类型将会以固定速度，触发任务调度；按照固定的间隔时间，周期性触发；**

**![image-20210729234114283](assets\image-20210729234114283.png)**

**任务配置**

- **运行模式：**

​    **BEAN模式：任务以JobHandler方式维护在执行器端；需要结合 "JobHandler" 属性匹配执行器中任务；**

- **JobHandler：运行模式为 "BEAN模式" 时生效，对应执行器中新开发的JobHandler类“@JobHandler”注解自定义的value值；**

- **执行参数：任务执行所需的参数；**

**![image-20210729234219162](assets\image-20210729234219162.png)**

**阻塞处理策略**

**阻塞处理策略：调度过于密集执行器来不及处理时的处理策略；**

- **单机串行（默认）：调度请求进入单机执行器后，调度请求进入FIFO(First Input First Output)队列并以串行方式运行；**

- **丢弃后续调度：调度请求进入单机执行器后，发现执行器存在运行的调度任务，本次请求将会被丢弃并标记为失败；**

- **覆盖之前调度：调度请求进入单机执行器后，发现执行器存在运行的调度任务，将会终止运行中的调度任务并清空队列，然后运行本地调度任务；**

**![image-20210729234256062](assets\image-20210729234256062.png)**

**路由策略**

**当执行器集群部署时，提供丰富的路由策略，包括；**

- **FIRST（第一个）：固定选择第一个机器；**

- **LAST（最后一个）：固定选择最后一个机器；**

- **ROUND（轮询）**

- **RANDOM（随机）：随机选择在线的机器；**

- **CONSISTENT_HASH（一致性HASH）：每个任务按照Hash算法固定选择某一台机器，且所有任务均匀散列在不同机器上。**

- **LEAST_FREQUENTLY_USED（最不经常使用）：使用频率最低的机器优先被选举；**

- **LEAST_RECENTLY_USED（最近最久未使用）：最久未使用的机器优先被选举；**

- **FAILOVER（故障转移）：按照顺序依次进行心跳检测，第一个心跳检测成功的机器选定为目标执行器并发起调度；**

- **BUSYOVER（忙碌转移）：按照顺序依次进行空闲检测，第一个空闲检测成功的机器选定为目标执行器并发起调度；**

- **SHARDING_BROADCAST(分片广播)：广播触发对应集群中所有机器执行一次任务，同时系统自动传递分片参数；可根据分片参数开发分片任务；**

**![image-20210729234409132](assets\image-20210729234409132.png)**

### **路由策略(轮询)-案例**

**1.修改任务为轮询**

**![image-20210729234513775](assets\image-20210729234513775.png)**

**2.启动多个微服务**

**![image-20210729234536483](assets\image-20210729234536483.png)**

**修改yml配置文件**

```yaml
server:
  port: ${port:8881}


xxl:
  job:
    admin:
      addresses: http://192.168.200.130:8888/xxl-job-admin
    executor:
      appname: xxl-job-executor-sample
      port: ${executor.port:9999}
```

**3.启动多个微服务**

**每个微服务轮询的去执行任务**

### **路由策略(分片广播)**

#### **分片逻辑**

**执行器集群部署时，任务路由策略选择”分片广播”情况下，一次任务调度将会广播触发对应集群中所有执行器执行一次任务**

**![image-20210729234756221](assets\image-20210729234756221.png)**

**执行器集群部署时，任务路由策略选择”分片广播”情况下，一次任务调度将会广播触发对应集群中所有执行器执行一次任务**

**![image-20210729234822935](assets\image-20210729234822935.png)**

#### **路由策略(分片广播)-案例**

**需求：让两个节点同时执行10000个任务，每个节点分别执行5000个任务**

**①：创建分片执行器**

**![image-20210729234930218](assets\image-20210729234930218.png)**

**②：创建任务，路由策略为分片广播**

**![image-20210729234948571](assets\image-20210729234948571.png)**

**③：分片广播代码**

   **分片参数**

​     **index：当前分片序号(从0开始)，执行器集群列表中当前执行器的序号；**

​     **total：总分片数，执行器集群的总机器数量；**

**修改yml配置**

```yaml
server:
  port: ${port:8881}


xxl:
  job:
    admin:
      addresses: http://192.168.200.130:8888/xxl-job-admin
    executor:
      appname: xxl-job-sharding-executor
      port: ${executor.port:9999}
```

**代码**

```java
package com.heima.xxljob.job;

import com.xxl.job.core.context.XxlJobHelper;
import com.xxl.job.core.handler.annotation.XxlJob;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

import java.util.ArrayList;
import java.util.List;

@Component
public class HelloJob {

    @Value("${server.port}")
    private String port;


    @XxlJob("demoJobHandler")
    public void helloJob(){
        System.out.println("简单任务执行了。。。。"+port);

    }

    @XxlJob("shardingJobHandler")
    public void shardingJobHandler(){
        //分片的参数
        int shardIndex = XxlJobHelper.getShardIndex();
        int shardTotal = XxlJobHelper.getShardTotal();

        //业务逻辑
        List<Integer> list = getList();
        for (Integer integer : list) {
            if(integer % shardTotal == shardIndex){
                System.out.println("当前第"+shardIndex+"分片执行了，任务项为："+integer);
            }
        }
    }

    public List<Integer> getList(){
        List<Integer> list = new ArrayList<>();
        for (int i = 0; i < 10000; i++) {
            list.add(i);
        }
        return list;
    }
}
```

**④：测试**

**启动多个微服务测试，一次执行可以执行多个任务**