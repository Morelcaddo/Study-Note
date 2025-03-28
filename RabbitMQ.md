# RabbitMQ

## 同步调用与异步调用

**微服务一旦拆分，必然涉及到服务之间的相互调用，目前我们服务之间调用采用的都是基于OpenFeign的调用。这种调用中，调用者发起请求后需要等待服务提供者执行业务返回结果后，才能继续执行后面的业务。也就是说调用者在调用过程中处于阻塞状态，因此我们称这种调用方式为同步调用，也可以叫同步通讯。但在很多场景下，我们可能需要采用异步通讯的方式，为什么呢？**

**同步通讯：就如同打视频电话，双方的交互都是实时的。因此同一时刻你只能跟一个人打视频电话。**

**异步通讯：就如同发微信聊天，双方的交互不是实时的，你不需要立刻给对方回应。因此你可以多线操作，同时跟多人聊天。**

**两种方式各有优劣，打电话可以立即得到响应，但是你却不能跟多个人同时通话。发微信可以同时与多个人收发微信，但是往往响应会有延迟。**

**所以，如果我们的业务需要实时得到服务提供方的响应，则应该选择同步通讯（同步调用）。而如果我们追求更高的效率，并且不需要实时响应，则应该选择异步通讯（异步调用）。**



### 同步调用

**之前说过，我们现在基于OpenFeign的调用都属于是同步调用，那么这种方式存在哪些问题呢？**

**举个例子，我们以昨天留给大家作为作业的余额支付功能为例来分析，首先看下整个流程：**

**![](D:/StudyNote/assets/1738912063089.png)**

**目前我们采用的是基于OpenFeign的同步调用，也就是说业务执行流程是这样的：**

- **支付服务需要先调用用户服务完成余额扣减**
- **然后支付服务自己要更新支付流水单的状态**
- **然后支付服务调用交易服务，更新业务订单状态为已支付**

**三个步骤依次执行。**

**这其中就存在3个问题：**

**第一，拓展性差**

**我们目前的业务相对简单，但是随着业务规模扩大，产品的功能也在不断完善。**

**在大多数电商业务中，用户支付成功后都会以短信或者其它方式通知用户，告知支付成功。假如后期产品经理提出这样新的需求，你怎么办？是不是要在上述业务中再加入通知用户的业务？**

**某些电商项目中，还会有积分或金币的概念。假如产品经理提出需求，用户支付成功后，给用户以积分奖励或者返还金币，你怎么办？是不是要在上述业务中再加入积分业务、返还金币业务？**

**最终你的支付业务会越来越臃肿：**

**![](D:/StudyNote/assets/1738912173659.png)**

**也就是说每次有新的需求，现有支付逻辑都要跟着变化，代码经常变动，不符合开闭原则，拓展性不好。**

**第二，性能下降**

**由于我们采用了同步调用，调用者需要等待服务提供者执行完返回结果后，才能继续向下执行，也就是说每次远程调用，调用者都是阻塞等待状态。最终整个业务的响应时长就是每次远程调用的执行时长之和：**

**![](D:/StudyNote/assets/1738912189796.png)**

**假如每个微服务的执行时长都是50ms，则最终整个业务的耗时可能高达300ms，性能太差了。**

**第三，级联失败**

**由于我们是基于OpenFeign调用交易服务、通知服务。当交易服务、通知服务出现故障时，整个事务都会回滚，交易失败。**

**这其实就是同步调用的级联失败问题。**

**但是大家思考一下，我们假设用户余额充足，扣款已经成功，此时我们应该确保支付流水单更新为已支付，确保交易成功。毕竟收到手里的钱没道理再退回去吧。**

**因此，这里不能因为短信通知、更新订单状态失败而回滚整个事务。**

**综上，同步调用的方式存在下列问题：**

- **拓展性差**
- **性能下降**
- **级联失败**

**而要解决这些问题，我们就必须用异步调用的方式来代替同步调用。**

### 异步调用

异步调用方式其实就是基于消息通知的方式，一般包含三个角色：

- 消息发送者：投递消息的人，就是原来的调用方
- 消息Broker：管理、暂存、转发消息，你可以把它理解成微信服务器
- 消息接收者：接收和处理消息的人，就是原来的服务提供方

![](D:/StudyNote/assets/1738920984407.png)

在异步调用中，发送者不再直接同步调用接收者的业务接口，而是发送一条消息投递给消息Broker。然后接收者根据自己的需求从消息Broker那里订阅消息。每当发送方发送消息后，接受者都能获取消息并处理。

这样，发送消息的人和接收消息的人就完全解耦了。

还是以余额支付业务为例：

![](D:/StudyNote/assets/1738921020880.png)

除了扣减余额、更新支付流水单状态以外，其它调用逻辑全部取消。而是改为发送一条消息到Broker。而相关的微服务都可以订阅消息通知，一旦消息到达Broker，则会分发给每一个订阅了的微服务，处理各自的业务。

假如产品经理提出了新的需求，比如要在支付成功后更新用户积分。支付代码完全不用变更，而仅仅是让积分服务也订阅消息即可：

![](D:/StudyNote/assets/1738921036561.png)

不管后期增加了多少消息订阅者，作为支付服务来讲，执行问扣减余额、更新支付流水状态后，发送消息即可。业务耗时仅仅是这三部分业务耗时，仅仅100ms，大大提高了业务性能。

另外，不管是交易服务、通知服务，还是积分服务，他们的业务与支付关联度低。现在采用了异步调用，解除了耦合，他们即便执行过程中出现了故障，也不会影响到支付服务。

综上，异步调用的优势包括：

- 耦合度更低
- 性能更好
- 业务拓展性强
- 故障隔离，避免级联失败

当然，异步通信也并非完美无缺，它存在下列缺点：

- 完全依赖于Broker的可靠性、安全性和性能
- 架构复杂，后期维护和调试麻烦

## 技术选型

**消息Broker，目前常见的实现方案就是消息队列（MessageQueue），简称为MQ.**

**目比较常见的MQ实现：**

- **ActiveMQ**
- **RabbitMQ**
- **RocketMQ**
- **Kafka**

**几种常见MQ的对比：**

|                | **RabbitMQ**                | **ActiveMQ**                       | **RocketMQ**   | **Kafka**      |
| -------------- | --------------------------- | ---------------------------------- | -------------- | -------------- |
| **公司/社区**  | **Rabbit**                  | **Apache**                         | **阿里**       | **Apache**     |
| **开发语言**   | **Erlang**                  | **Java**                           | **Java**       | **Scala&Java** |
| **协议支持**   | **AMQP，XMPP，SMTP，STOMP** | **OpenWire,STOMP，REST,XMPP,AMQP** | **自定义协议** | **自定义协议** |
| **可用性**     | **高**                      | **一般**                           | **高**         | **高**         |
| **单机吞吐量** | **一般**                    | **差**                             | **高**         | **非常高**     |
| **消息延迟**   | **微秒级**                  | **毫秒级**                         | **毫秒级**     | **毫秒以内**   |
| **消息可靠性** | **高**                      | **一般**                           | **高**         | **一般**       |

**追求可用性：Kafka、 RocketMQ 、RabbitMQ**

**追求可靠性：RabbitMQ、RocketMQ**

**追求吞吐能力：RocketMQ、Kafka**

**追求消息低延迟：RabbitMQ、Kafka**

**据统计，目前国内消息队列使用最多的还是RabbitMQ，再加上其各方面都比较均衡，稳定性也好，因此我们课堂上选择RabbitMQ来学习。**

## 安装和部署

**我们同样基于Docker来安装RabbitMQ，使用下面的命令即可：**

```Shell
docker run \
 -e RABBITMQ_DEFAULT_USER=itheima \
 -e RABBITMQ_DEFAULT_PASS=123321 \
 -v mq-plugins:/plugins \
 --name mq \
 --hostname mq \
 -p 15672:15672 \
 -p 5672:5672 \
 --network hm-net\
 -d \
 rabbitmq:3.8-management
```

**可以看到在安装命令中有两个映射的端口：**

- **15672：RabbitMQ提供的管理控制台的端口**
- **5672：RabbitMQ的消息发送处理接口**

**安装完成后，我们访问 http://192.168.150.101:15672即可看到管理控制台。首次访问需要登录，默认的用户名和密码在配置文件中已经指定了。**

**登录后即可看到管理控制台总览页面：**

**RabbitMQ对应的架构如图：**

![](D:/StudyNote/assets/1738925493735.png)

**其中包含几个概念：**

- **`publisher`：生产者，也就是发送消息的一方**
- **`consumer`：消费者，也就是消费消息的一方**
- **`queue`：队列，存储消息。生产者投递的消息会暂存在消息队列中，等待消费者处理**
- **`exchange`：交换机，负责消息路由。生产者发送的消息由交换机决定投递到哪个队列。**
- **`virtual host`：虚拟主机，起到数据隔离的作用。每个虚拟主机相互独立，有各自的exchange、queue.这样当不同项目使用用一个RabbitMQ服务时，就能够通过虚拟主机做到彼此隔离**

## 收发消息

### 交换机

**我们打开Exchanges选项卡，可以看到已经存在很多交换机：**

**![](D:/StudyNote/assets/1738928481192.png)**

**我们点击任意交换机，即可进入交换机详情页面。仍然会利用控制台中的publish message 发送一条消息：**

**![](D:/StudyNote/assets/1738928497697.png)**

**![](D:/StudyNote/assets/1738928514368.png)**

**这里是由控制台模拟了生产者发送的消息。由于没有消费者存在，最终消息丢失了，这样说明交换机没有存储消息的能力。**

### **队列**

**我们打开`Queues`选项卡，新建一个队列：**

**![](D:/StudyNote/assets/1738928627065.png)**

**命名为`hello.queue1`：**

**![](D:/StudyNote/assets/1738928646166.png)**

**再以相同的方式，创建一个队列，密码为`hello.queue2`，最终队列列表如下：**

**![](D:/StudyNote/assets/1738928658630.png)**

**此时，我们再次向`amq.fanout`交换机发送一条消息。会发现消息依然没有到达队列！！**

**怎么回事呢？**

**发送到交换机的消息，只会路由到与其绑定的队列，因此仅仅创建队列是不够的，我们还需要将其与交换机绑定。**

### **绑定关系**

**点击`Exchanges`选项卡，点击`amq.fanout`交换机，进入交换机详情页，然后点击`Bindings`菜单，在表单中填写要绑定的队列名称：**

**![](D:/StudyNote/assets/1738928899023.png)**

**相同的方式，将hello.queue2也绑定到改交换机。**

**最终，绑定结果如下：**

**![](D:/StudyNote/assets/1738928910786.png)**

### **发送消息**

**再次回到exchange页面，找到刚刚绑定的`amq.fanout`，点击进入详情页，再次发送一条消息：**

**![](D:/StudyNote/assets/1738928968167.png)**

**回到`Queues`页面，可以发现`hello.queue`中已经有一条消息了：**

**![](D:/StudyNote/assets/1738928981923.png)**

**点击队列名称，进入详情页，查看队列详情，这次我们点击get message：**

**![](D:/StudyNote/assets/1738928999599.png)**

**可以看到消息到达队列了：**

**![](D:/StudyNote/assets/1738929032723.png)**

**这个时候如果有消费者监听了MQ的`hello.queue1`或`hello.queue2`队列，自然就能接收到消息了。**

## **数据隔离**

### **用户管理**

**点击`Admin`选项卡，首先会看到RabbitMQ控制台的用户管理界面：**

**![](D:/StudyNote/assets/1738930187042.png)**

**这里的用户都是RabbitMQ的管理或运维人员。目前只有安装RabbitMQ时添加的`itheima`这个用户。仔细观察用户表格中的字段，如下：**

- **`Name`：`itheima`，也就是用户名**
- **`Tags`：`administrator`，说明`itheima`用户是超级管理员，拥有所有权限**
- **`Can access virtual host`： `/`，可以访问的`virtual host`，这里的`/`是默认的`virtual host`**

**对于小型企业而言，出于成本考虑，我们通常只会搭建一套MQ集群，公司内的多个不同项目同时使用。这个时候为了避免互相干扰， 我们会利用`virtual host`的隔离特性，将不同项目隔离。一般会做两件事情：**

- **给每个项目创建独立的运维账号，将管理权限分离。**
- **给每个项目创建不同的`virtual host`，将每个项目的数据隔离。**

**比如，我们给黑马商城创建一个新的用户，命名为`hmall`：**

**![](D:/StudyNote/assets/1738930238040.png)**

**你会发现此时hmall用户没有任何`virtual host`的访问权限：**

**![](D:/StudyNote/assets/1738930271324.png)**

**别急，接下来我们就来授权。**

### **virtual host**

**我们先退出登录：**

**![](D:assets\1738930374521.png)**

**切换到刚刚创建的hmall用户登录，然后点击`Virtual Hosts`菜单，进入`virtual host`管理页：**

**![](D:/StudyNote/assets/1738930409078.png)**

**可以看到目前只有一个默认的`virtual host`，名字为 `/`。**

 **我们可以给黑马商城项目创建一个单独的`virtual host`，而不是使用默认的`/`。**

**![](D:/StudyNote/assets/1738930457935.png)**

**创建完成后如图：**

**![](D:/StudyNote/assets/1738930491001.png)**

**由于我们是登录`hmall`账户后创建的`virtual host`，因此回到`users`菜单，你会发现当前用户已经具备了对`/hmall`这个`virtual host`的访问权限了：**

**![](D:\StudyNote\assets\1738930530735.png)**

**此时，点击页面右上角的`virtual host`下拉菜单，切换`virtual host`为 `/hmall`：**

**![](D:/StudyNote/assets/1738930557896.png)**

**然后再次查看queues选项卡，会发现之前的队列已经看不到了：**

**![](D:/StudyNote/assets/1738930592380.png)**

**这就是基于`virtual host `的隔离效果。**

## Spring AMQP

### **快速入门**

**在之前的案例中，我们都是经过交换机发送消息到队列，不过有时候为了测试方便，我们也可以直接向队列发送消息，跳过交换机。**

**在入门案例中，我们就演示这样的简单模型，如图：**

![](D:/StudyNote/assets/1739087991876.png)

**也就是：**

- **publisher直接发送消息到队列**
- **消费者监听并处理队列中的消息**

**注意**：**这种模式一般测试使用，很少在生产中使用。**

**首先我们需要引入相关依赖**

```xml
<!--AMQP依赖，包含RabbitMQ-->
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

**配置RabbitMQ服务端信息**

```YAML
spring:
  rabbitmq:
    host: 192.168.230.130 # 你的虚拟机IP
    port: 5672 # 端口
    virtual-host: /hmall # 虚拟主机
    username: hmall # 用户名
    password: 123 # 密码
```

**然后在`publisher`服务中编写测试类`SpringAmqpTest`，并利用`RabbitTemplate`实现消息发送：**

```Java
package com.itheima.publisher.amqp;

import org.junit.jupiter.api.Test;
import org.springframework.amqp.rabbit.core.RabbitTemplate;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class SpringAmqpTest {

    @Autowired
    private RabbitTemplate rabbitTemplate;

    @Test
    public void testSimpleQueue() {
        // 队列名称
        String queueName = "simple.queue";
        // 消息
        String message = "hello, spring amqp!";
        // 发送消息
        rabbitTemplate.convertAndSend(queueName, message);
    }
}
```

**然后在`consumer`服务的`com.itheima.consumer.listener`包中新建一个类`SpringRabbitListener`，实现接受消息：**

```Java
package com.itheima.consumer.listener;

import org.springframework.amqp.rabbit.annotation.RabbitListener;
import org.springframework.stereotype.Component;

@Component
public class SpringRabbitListener {
    // 利用RabbitListener来声明要监听的队列信息
    // 将来一旦监听的队列中有了消息，就会推送给当前服务，调用当前方法，处理消息。
    // 可以看到方法体中接收的就是消息体的内容
    @RabbitListener(queues = "simple.queue")
    public void listenSimpleQueueMessage(String msg) throws InterruptedException {
        System.out.println("spring 消费者接收到消息：【" + msg + "】");
    }
}
```

### Work Queues

**Work queues，任务模型。简单来说就是让多个消费者绑定到一个队列，共同消费队列中的消息。**

![](D:/StudyNote/assets/1739089596705.png)

**当消息处理比较耗时的时候，可能生产消息的速度会远远大于消息的消费速度。长此以往，消息就会堆积越来越多，无法及时处理。**

**此时就可以使用work 模型，多个消费者共同处理消息处理，消息处理的速度就能大大提高了。**



**这次我们循环发送，模拟大量消息堆积现象。**

**在publisher服务中的SpringAmqpTest类中添加一个测试方法：**

```Java
/**
     * workQueue
     * 向队列中不停发送消息，模拟消息堆积。
     */
@Test
public void testWorkQueue() throws InterruptedException {
    // 队列名称
    String queueName = "work.queue";
    // 消息
    String message = "hello, message_";
    for (int i = 0; i < 50; i++) {
        // 发送消息，每20毫秒发送一次，相当于每秒发送50条消息
        rabbitTemplate.convertAndSend(queueName, message + i);
        Thread.sleep(20);
    }
}
```

**要模拟多个消费者绑定同一个队列，我们在consumer服务的SpringRabbitListener中添加2个新的方法：**

```Java
@RabbitListener(queues = "work.queue")
public void listenWorkQueue1(String msg) throws InterruptedException {
    System.out.println("消费者1接收到消息：【" + msg + "】" + LocalTime.now());
    Thread.sleep(20);
}

@RabbitListener(queues = "work.queue")
public void listenWorkQueue2(String msg) throws InterruptedException {
    System.err.println("消费者2........接收到消息：【" + msg + "】" + LocalTime.now());
    Thread.sleep(200);
}
```

**注意到这两消费者，都设置了`Thead.sleep`，模拟任务耗时：**

- **消费者1 sleep了20毫秒，相当于每秒钟处理50个消息**
- **消费者2 sleep了200毫秒，相当于每秒处理5个消息**

**通过测试，可以看到消费者1和消费者2竟然每人消费了25条消息：**

- **消费者1很快完成了自己的25条消息**
- **消费者2却在缓慢的处理自己的25条消息。**

**也就是说消息是平均分配给每个消费者，并没有考虑到消费者的处理能力。导致1个消费者空闲，另一个消费者忙的不可开交。没有充分利用每一个消费者的能力，最终消息处理的耗时远远超过了1秒。这样显然是有问题的。**

#### 能者多劳

**在spring中有一个简单的配置，可以解决这个问题。我们修改consumer服务的application.yml文件，添加配置：**

```YAML
spring:
  rabbitmq:
    listener:
      simple:
        prefetch: 1 # 每次只能获取一条消息，处理完成才能获取下一个消息
```

**可以发现，由于消费者1处理速度较快，所以处理了更多的消息；消费者2处理速度较慢，只处理了6条消息。而最终总的执行耗时也在1秒左右，大大提升。**

**正所谓能者多劳，这样充分利用了每一个消费者的处理能力，可以有效避免消息积压问题。**

**Work模型的使用：**

- **多个消费者绑定到一个队列，同一条消息只会被一个消费者处理**
- **通过设置prefetch来控制消费者预取的消息数量**

### 交换机类型

**在之前的两个测试案例中，都没有交换机，生产者直接发送消息到队列。而一旦引入交换机，消息发送的模式会有很大变化：**

![](D:/StudyNote/assets/1739096842340.png)

**可以看到，在订阅模型中，多了一个exchange角色，而且过程略有变化：**

- **Publisher：生产者，不再发送消息到队列中，而是发给交换机**
- **Exchange：交换机，一方面，接收生产者发送的消息。另一方面，知道如何处理消息，例如递交给某个特别队列、递交给所有队列、或是将消息丢弃。到底如何操作，取决于Exchange的类型。**
- **Queue：消息队列也与以前一样，接收消息、缓存消息。不过队列一定要与交换机绑定。**
- **Consumer：消费者，与以前一样，订阅队列，没有变化**

**Exchange（交换机）只负责转发消息，不具备存储消息的能力，因此如果没有任何队列与Exchange绑定，或者没有符合路由规则的队列，那么消息会丢失！**

**交换机的类型有四种：**

- **Fanout：广播，将消息交给所有绑定到交换机的队列。我们最早在控制台使用的正是Fanout交换机**
- **Direct：订阅，基于RoutingKey（路由key）发送给订阅了消息的队列**
- **Topic：通配符订阅，与Direct类似，只不过RoutingKey可以使用通配符**
- **Headers：头匹配，基于MQ的消息头匹配，用的较少。**

### Fanout交换机

**Fanout Exchange会将接收到的消息路由到每一个跟其绑定的queue,所以也叫广播模式**

![](D:/StudyNote/assets/1739097042123.png)

**Fanout交换机有以下特点**

​	**可以有多个队列**

​	**每个队列都要绑定到Exchange（交换机）**

​	**生产者发送的消息，只能发送到交换**

​	**交换机把消息发送给绑定过的所有队列**

​	**订阅队列的消费者都能拿到消息**

**首先我们按照图中的结构创建交换机和队列，先创建两个队列分别命名为fanout.queue1和fanout.queue2**

**接着创建交换机，命名为hmall.fanout**

![](D:/StudyNote/assets/1739101386871.png)

**然后绑定两个队列到交换机：**

**在publisher服务的SpringAmqpTest类中添加测试方法：**

```Java
@Test
public void testFanoutExchange() {
    // 交换机名称
    String exchangeName = "hmall.fanout";
    // 消息
    String message = "hello, everyone!";
    rabbitTemplate.convertAndSend(exchangeName, "", message);//第二个参数是routingKey,目前先不传
}
```

**在consumer服务的SpringRabbitListener中添加两个方法，作为消费者：**

```Java
@RabbitListener(queues = "fanout.queue1")
public void listenFanoutQueue1(String msg) {
    System.out.println("消费者1接收到Fanout消息：【" + msg + "】");
}

@RabbitListener(queues = "fanout.queue2")
public void listenFanoutQueue2(String msg) {
    System.out.println("消费者2接收到Fanout消息：【" + msg + "】");
}
```

**交换机的作用**

- **接收publisher发送的消息**
- **将消息按照规则路由到与之绑定的队列**
- **不能缓存消息，路由失败，消息丢失**
- **FanoutExchange的会将消息路由到每个绑定的队列**

### Direct交换机

**Fanout模式中，一条消息，会被所有订阅的队列都消费。但是，在某些场景下，我们希望不同的消息被不同的队列消费。这时就要用到Direct类型的Exchange。**

![](D:/StudyNote/assets/1739101852544.png)

**在Direct模型下：**

- **队列与交换机的绑定，不能是任意绑定了，而是要指定一个`RoutingKey`（路由key）**
- **消息的发送方在 向 Exchange发送消息时，也必须指定消息的 `RoutingKey`。**
- **Exchange不再把消息交给每一个绑定的队列，而是根据消息的`Routing Key`进行判断，只有队列的`Routingkey`与消息的 `Routing key`完全一致，才会接收到消息**

**操作步骤**

**声明一个名为`hmall.direct`的交换机**

**声明队列`direct.queue1`，绑定`hmall.direct`，`bindingKey`为`blud`和`red`**

**声明队列`direct.queue2`，绑定`hmall.direct`，`bindingKey`为`yellow`和`red`**

**在`consumer`服务中，编写两个消费者方法，分别监听direct.queue1和direct.queue2** 

**在publisher中编写测试方法，向`hmall.direct`发送消息** 

**这里我们以direct.queue1为例展示将red作为key绑定给队列**

![](D:/StudyNote/assets/1739102174566.png)

**在consumer服务的SpringRabbitListener中添加方法：**

```Java
@RabbitListener(queues = "direct.queue1")
public void listenDirectQueue1(String msg) {
    System.out.println("消费者1接收到direct.queue1的消息：【" + msg + "】");
}

@RabbitListener(queues = "direct.queue2")
public void listenDirectQueue2(String msg) {
    System.out.println("消费者2接收到direct.queue2的消息：【" + msg + "】");
}
```



**在publisher服务的SpringAmqpTest类中添加测试方法：**

```Java
@Test
public void testSendDirectExchange() {
    // 交换机名称
    String exchangeName = "hmall.direct";
    // 消息
    String message = "红色警报！日本乱排核废水，导致海洋生物变异，惊现哥斯拉！";
    // 发送消息
    rabbitTemplate.convertAndSend(exchangeName, "red", message);
}
```

**由于使用的red这个key，所以两个消费者都收到了消息：**

![](D:/StudyNote/assets/1739102469564.png)

**我们再切换为blue这个key：**

```Java
@Test
public void testSendDirectExchange() {
    // 交换机名称
    String exchangeName = "hmall.direct";
    // 消息
    String message = "最新报道，哥斯拉是居民自治巨型气球，虚惊一场！";
    // 发送消息
    rabbitTemplate.convertAndSend(exchangeName, "blue", message);
}
```

**你会发现，只有消费者1收到了消息：**

![](D:/StudyNote/assets/1739102515724.png)



**描述下Direct交换机与Fanout交换机的差异**

- **Fanout交换机将消息路由给每一个与之绑定的队列**
- **Direct交换机根据RoutingKey判断路由给哪个队列**
- **如果多个队列具有相同的RoutingKey，则与Fanout功能类似**

### Topic交换机

`**Topic`类型的`Exchange`与`Direct`相比，都是可以根据`RoutingKey`把消息路由到不同的队列。**

**只不过`Topic`类型`Exchange`可以让队列在绑定`BindingKey` 的时候使用通配符！**

```
BindingKey` 一般都是有一个或多个单词组成，多个单词之间以`.`分割，例如： `item.insert
```

**通配符规则：**

- **`#`：匹配一个或多个词**
- **`*`：匹配不多不少恰好1个词**

**举例：**

- **`item.#`：能够匹配`item.spu.insert` 或者 `item.spu`**
- **`item.*`：只能匹配`item.spu`**

![](D:/StudyNote/assets/1739102797291.png)

**假如此时publisher发送的消息使用的`RoutingKey`共有四种：**

- **`china.news `代表有中国的新闻消息；**
- **`china.weather` 代表中国的天气消息；**
- **`japan.news` 则代表日本新闻**
- **`japan.weather` 代表日本的天气消息；**

**解释：**

- **`topic.queue1`：绑定的是`china.#` ，凡是以 `china.`开头的`routing key` 都会被匹配到，包括：**
  - **`china.news`**
  - **`china.weather`**
- **`topic.queue2`：绑定的是`#.news` ，凡是以 `.news`结尾的 `routing key` 都会被匹配。包括:**
  - **`china.news`**
  - **`japan.news`**

**接下来，我们就按照上图所示，来演示一下Topic交换机的用法。**

**首先，在控制台按照图示例子创建队列、交换机，并利用通配符绑定队列和交换机。此处步骤略。**

**在publisher服务的SpringAmqpTest类中添加测试方法：**

```Java
/**
 * topicExchange
 */
@Test
public void testSendTopicExchange() {
    // 交换机名称
    String exchangeName = "hmall.topic";
    // 消息
    String message = "喜报！孙悟空大战哥斯拉，胜!";
    // 发送消息
    rabbitTemplate.convertAndSend(exchangeName, "china.news", message);
}
```

**在consumer服务的SpringRabbitListener中添加方法：**

```Java
@RabbitListener(queues = "topic.queue1")
public void listenTopicQueue1(String msg){
    System.out.println("消费者1接收到topic.queue1的消息：【" + msg + "】");
}

@RabbitListener(queues = "topic.queue2")
public void listenTopicQueue2(String msg){
    System.out.println("消费者2接收到topic.queue2的消息：【" + msg + "】");
}
```

**描述下Direct交换机与Topic交换机的差异**

- **Topic交换机接收的消息RoutingKey必须是多个单词，以 `.` 分割**
- **Topic交换机与队列绑定时的bindingKey可以指定通配符**
- **`#`：代表0个或多个词**
- **`*`：代表1个词**

### 申明队列和交换机

**SpringAMQP提供了一个Queue类，用来创建队列：**

![](D:/StudyNote/assets/1739108513141.png)

**SpringAMQP还提供了一个Exchange接口，来表示所有不同类型的交换机：**

![](D:/StudyNote/assets/1739108582606.png)

**另外SpringAMQP还提供了ExchangeBuilder来简化这个过程：**

![](D:/StudyNote/assets/1739108669969.png)

**而在绑定队列和交换机时，则需要使用BindingBuilder工厂类来创建Binding对象：**

![](D:/StudyNote/assets/1739108719513.png)

#### fanout示例

**在consumer中创建一个类，声明队列和交换机：**

```Java
package com.itheima.consumer.config;

import org.springframework.amqp.core.Binding;
import org.springframework.amqp.core.BindingBuilder;
import org.springframework.amqp.core.FanoutExchange;
import org.springframework.amqp.core.Queue;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class FanoutConfig {
    /**
     * 声明交换机
     * @return Fanout类型交换机
     */
    @Bean
    public FanoutExchange fanoutExchange(){
        return new FanoutExchange("hmall.fanout");
    }

    /**
     * 第1个队列
     */
    @Bean
    public Queue fanoutQueue1(){
        return new Queue("fanout.queue1");
    }

    /**
     * 绑定队列和交换机
     */
    @Bean
    public Binding bindingQueue1(Queue fanoutQueue1, FanoutExchange fanoutExchange){
        return BindingBuilder.bind(fanoutQueue1).to(fanoutExchange);
    }

    /**
     * 第2个队列
     */
    @Bean
    public Queue fanoutQueue2(){
        return new Queue("fanout.queue2");
    }

    /**
     * 绑定队列和交换机
     */
    @Bean
    public Binding bindingQueue2(Queue fanoutQueue2, FanoutExchange fanoutExchange){
        return BindingBuilder.bind(fanoutQueue2).to(fanoutExchange);
    }
}
```

#### direct示例

**direct模式由于要绑定多个KEY，会非常麻烦，每一个Key都要编写一个binding：**

```Java
package com.itheima.consumer.config;

import org.springframework.amqp.core.*;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class DirectConfig {

    /**
     * 声明交换机
     * @return Direct类型交换机
     */
    @Bean
    public DirectExchange directExchange(){
        return ExchangeBuilder.directExchange("hmall.direct").build();
    }

    /**
     * 第1个队列
     */
    @Bean
    public Queue directQueue1(){
        return new Queue("direct.queue1");
    }

    /**
     * 绑定队列和交换机
     */
    @Bean
    public Binding bindingQueue1WithRed(Queue directQueue1, DirectExchange directExchange){
        return BindingBuilder.bind(directQueue1).to(directExchange).with("red");
    }
    /**
     * 绑定队列和交换机
     */
    @Bean
    public Binding bindingQueue1WithBlue(Queue directQueue1, DirectExchange directExchange){
        return BindingBuilder.bind(directQueue1).to(directExchange).with("blue");
    }

    /**
     * 第2个队列
     */
    @Bean
    public Queue directQueue2(){
        return new Queue("direct.queue2");
    }

    /**
     * 绑定队列和交换机
     */
    @Bean
    public Binding bindingQueue2WithRed(Queue directQueue2, DirectExchange directExchange){
        return BindingBuilder.bind(directQueue2).to(directExchange).with("red");
    }
    /**
     * 绑定队列和交换机
     */
    @Bean
    public Binding bindingQueue2WithYellow(Queue directQueue2, DirectExchange directExchange){
        return BindingBuilder.bind(directQueue2).to(directExchange).with("yellow");
    }
}
```

**通常我们在消费者那一端书写队列和交换机相关的配置类**

#### 基于注解声明

**基于@Bean的方式声明队列和交换机比较麻烦，Spring还提供了基于注解方式来声明。**

**例如，我们同样声明Direct模式的交换机和队列：**

```Java
@RabbitListener(bindings = @QueueBinding(
    value = @Queue(name = "direct.queue1"),
    exchange = @Exchange(name = "hmall.direct", type = ExchangeTypes.DIRECT),
    key = {"red", "blue"}
))
public void listenDirectQueue1(String msg){
    System.out.println("消费者1接收到direct.queue1的消息：【" + msg + "】");
}

@RabbitListener(bindings = @QueueBinding(
    value = @Queue(name = "direct.queue2"),
    exchange = @Exchange(name = "hmall.direct", type = ExchangeTypes.DIRECT),
    key = {"red", "yellow"}
))
public void listenDirectQueue2(String msg){
    System.out.println("消费者2接收到direct.queue2的消息：【" + msg + "】");
}
```

**其中@Queue里的durable属性是可持久化，值为true代表需要持久化**

**是不是简单多了。**

**再试试Topic模式：**

```Java
@RabbitListener(bindings = @QueueBinding(
    value = @Queue(name = "topic.queue1"),
    exchange = @Exchange(name = "hmall.topic", type = ExchangeTypes.TOPIC),
    key = "china.#"
))
public void listenTopicQueue1(String msg){
    System.out.println("消费者1接收到topic.queue1的消息：【" + msg + "】");
}

@RabbitListener(bindings = @QueueBinding(
    value = @Queue(name = "topic.queue2"),
    exchange = @Exchange(name = "hmall.topic", type = ExchangeTypes.TOPIC),
    key = "#.news"
))
public void listenTopicQueue2(String msg){
    System.out.println("消费者2接收到topic.queue2的消息：【" + msg + "】");
}
```

### 消息转换器

**Spring的消息发送代码接收的消息体是一个Object：**

![](D:/StudyNote/assets/1739110092553.png)

**而在数据传输时，它会把你发送的消息序列化为字节发送给MQ，接收消息的时候，还会把字节反序列化为Java对象。**

**只不过，默认情况下Spring采用的序列化方式是JDK序列化。众所周知，JDK序列化存在下列问题：**

- **数据体积过大**
- **有安全漏洞**
- **可读性差**

#### 配置JSON转化器

**显然，JDK序列化方式并不合适。我们希望消息体的体积更小、可读性更高，因此可以使用JSON方式来做序列化和反序列化。**

**在`publisher`和`consumer`两个服务中都引入依赖：**

```XML
<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-xml</artifactId>
    <version>2.9.10</version>
</dependency>
```

**注意，如果项目中引入了`spring-boot-starter-web`依赖，则无需再次引入`Jackson`依赖。**

**配置消息转换器，在`publisher`和`consumer`两个服务的启动类中添加一个Bean即可：**

```Java
@Bean
public MessageConverter messageConverter(){
    // 1.定义消息转换器
    Jackson2JsonMessageConverter jackson2JsonMessageConverter = new Jackson2JsonMessageConverter();
    // 2.配置自动创建消息id，用于识别不同消息，也可以在业务中基于ID判断是否是重复消息
    jackson2JsonMessageConverter.setCreateMessageIds(true);
    return jackson2JsonMessageConverter;
}
```

**消息转换器中添加的messageId可以便于我们将来做幂等性判断。**

## 发送者的可靠性

**消息从生产者到消费者的每一步都可能导致消息丢失：**

- **发送消息时丢失：**
  - **生产者发送消息时连接MQ失败**
  - **生产者发送消息到达MQ后未找到`Exchange`**
  - **生产者发送消息到达MQ的`Exchange`后，未找到合适的`Queue`**
  - **消息到达MQ后，处理消息的进程发生异常**
- **MQ导致消息丢失：**
  - **消息到达MQ，保存到队列后，尚未消费就突然宕机**
- **消费者处理消息时：**
  - **消息接收后尚未处理突然宕机**
  - **消息接收后处理过程中抛出异常**

**综上，我们要解决消息丢失问题，保证MQ的可靠性，就必须从3个方面入手：**

- **确保生产者一定把消息发送到MQ**
- **确保MQ不会将消息弄丢**
- **确保消费者一定要处理消息**

### 发送者重连

**首先第一种情况，就是生产者发送消息时，出现了网络故障，导致与MQ的连接中断。**

**为了解决这个问题，SpringAMQP提供的消息发送时的重试机制。即：当`RabbitTemplate`与MQ连接超时后，多次重试。**

**修改`publisher`模块的`application.yaml`文件，添加下面的内容：**

```YAML
spring:
  rabbitmq:
    connection-timeout: 1s # 设置MQ的连接超时时间
    template:
      retry:
        enabled: true # 开启超时重试机制
        initial-interval: 1000ms # 失败后的初始等待时间
        multiplier: 1 # 失败后下次的等待时长倍数，下次等待时长 = initial-interval * multiplier
        max-attempts: 3 # 最大重试次数
```

**注意：当网络不稳定的时候，利用重试机制可以有效提高消息发送的成功率。不过SpringAMQP提供的重试机制是阻塞式的重试，也就是说多次重试等待的过程中，当前线程是被阻塞的。**

**如果对于业务性能有要求，建议禁用重试机制。如果一定要使用，请合理配置等待时长和重试次数，当然也可以考虑使用异步线程来执行发送消息的代码。**

### 发送者确认

**一般情况下，只要生产者与MQ之间的网路连接顺畅，基本不会出现发送消息丢失的情况，因此大多数情况下我们无需考虑这种问题。**

**不过，在少数情况下，也会出现消息发送到MQ之后丢失的现象，比如：**

- **MQ内部处理消息的进程发生了异常**
- **生产者发送消息到达MQ后未找到`Exchange`**
- **生产者发送消息到达MQ的`Exchange`后，未找到合适的`Queue`，因此无法路由**

**针对上述情况，RabbitMQ提供了生产者消息确认机制，包括`Publisher Confirm`和`Publisher Return`两种。在开启确认机制的情况下，当生产者发送消息给MQ后，MQ会根据消息处理的情况返回不同的回执。**

**具体如图所示：**

![](D:/StudyNote/assets/1739173669635.png)

**总结如下：**

- **publisher-confirm，发送者确认**

- - **消息成功投递到交换机，返回ack**
  - **消息未投递到交换机，返回nack**

- **publisher-return，发送者回执**

- - **消息投递到交换机了，但是没有路由到队列。返回ACK，及路由失败原因。**



**其中`ack`和`nack`属于Publisher Confirm机制，`ack`是投递成功；`nack`是投递失败。而`return`则属于Publisher Return机制。**

**默认两种机制都是关闭状态，需要通过配置文件来开启。**

**在publisher模块的`application.yaml`中添加配置：**

```YAML
spring:
  rabbitmq:
    publisher-confirm-type: correlated # 开启publisher confirm机制，并设置confirm类型
    publisher-returns: true # 开启publisher return机制
```

**这里`publisher-confirm-type`有三种模式可选：**

- **`none`：关闭confirm机制**
- **`simple`：同步阻塞等待MQ的回执**
- **`correlated`：MQ异步回调返回回执**

**一般我们推荐使用`correlated`，回调机制。**

#### ReturnCallback

**每个`RabbitTemplate`只能配置一个`ReturnCallback`，因此我们可以在配置类中统一设置。我们在publisher模块定义一个配置类：**

```Java
package com.itheima.publisher.config;

import lombok.AllArgsConstructor;
import lombok.extern.slf4j.Slf4j;
import org.springframework.amqp.core.ReturnedMessage;
import org.springframework.amqp.rabbit.core.RabbitTemplate;
import org.springframework.context.annotation.Configuration;

import javax.annotation.PostConstruct;

@Slf4j
@AllArgsConstructor
@Configuration
public class MqConfig {
    private final RabbitTemplate rabbitTemplate;

    @PostConstruct
    public void init(){
        rabbitTemplate.setReturnsCallback(new RabbitTemplate.ReturnsCallback() {
            @Override
            public void returnedMessage(ReturnedMessage returned) {
                log.error("触发return callback,");
                log.debug("exchange: {}", returned.getExchange());
                log.debug("routingKey: {}", returned.getRoutingKey());
                log.debug("message: {}", returned.getMessage());
                log.debug("replyCode: {}", returned.getReplyCode());
                log.debug("replyText: {}", returned.getReplyText());
            }
        });
    }
}
```

**@PostConstruct注解**

**@PostConstruct该注解被用来修饰一个非静态的void（）方法。被@PostConstruct修饰的方法会在服务器加载Servlet的时候运行，并且只会被服务器执行一次。PostConstruct在构造函数之后执行。**

**通常我们会是在Spring框架中使用到@PostConstruct注解 该注解的方法在整个Bean初始化中的执行顺序：**

**Constructor(构造方法) -> @Autowired(依赖注入) -> @PostConstruct(注释的方法)**

#### ConfirmCallback

**由于每个消息发送时的处理逻辑不一定相同，因此ConfirmCallback需要在每次发消息时定义。具体来说，是在调用RabbitTemplate中的convertAndSend方法时，多传递一个参数, CorrelationData**

**这里的CorrelationData中包含两个核心的东西：**

- **`id`：消息的唯一标示，MQ对不同的消息的回执以此做判断，避免混淆**
- **`SettableListenableFuture`：回执结果的Future对象**

**将来MQ的回执就会通过这个`Future`来返回，我们可以提前给`CorrelationData`中的`Future`添加回调函数来处理消息回执：**

**我们新建一个测试，向系统自带的交换机发送消息，并且添加`ConfirmCallback`：**

```
@Test
public void testConfirmCallback() throws InterruptedException {
    // 1.创建CorrelationData,这里构造函数的参数为消息id，用于标识消息
    CorrelationData cd = new CorrelationData(UUID.randomUUID().toString());
    // 2.给Future添加ConfirmCallback
    cd.getFuture().addCallback(new ListenableFutureCallback<CorrelationData.Confirm>() {
        @Override
        public void onFailure(Throwable ex) {
            // 2.1.Future发生异常时的处理逻辑，基本不会触发
            log.error("send message fail", ex);
        }
        @Override
        public void onSuccess(CorrelationData.Confirm result) {
            // 2.2.Future接收到回执的处理逻辑，参数中的result就是回执内容
            if(result.isAck()){ // result.isAck()，boolean类型，true代表ack回执，false 代表 nack回执
                log.debug("发送消息成功，收到 ack!");
            }else{ // result.getReason()，String类型，返回nack时的异常描述
                log.error("发送消息失败，收到 nack, reason : {}", result.getReason());
            }
        }
    });

    // 交换机名称
    String exchangeName = "hmall.direct";
    // 消息
    String message = "蓝色：通知";
    // 发送消息
    rabbitTemplate.convertAndSend(exchangeName, "blue", message);

    Thread.sleep(2000);
}
```

## MQ的可靠性

**在默认情况下，RabbitMQ会将接收到的信息保存在内存中以降低消息收发的延迟，这样就会引发两个问题：**

​	**一旦MQ宕机，内存中的信息就会丢失**

​	**内存空间有限，当消费者故障或处理过慢时，会导致消息积压，引发MQ阻塞**

### 数据持久化

**RabbitMQ实现数据持久化包括3个方面：**

​	**交换机持久化**

​	**队列持久化**

​	**消息持久化**

#### 交换机持久化

**在控制台的`Exchanges`页面，添加交换机时可以配置交换机的`Durability`参数：**

![](D:/StudyNote/assets/1739183726579.png)

**设置为`Durable`就是持久化模式，`Transient`就是临时模式。**

**基于Spring AMQP生成的交换机默认是持久化的**

#### 队列持久化

**在控制台的Queues页面，添加队列时，同样可以配置队列的`Durability`参数：**

![](D:/StudyNote/assets/1739183746315.png)

**除了持久化以外，你可以看到队列还有很多其它参数，有一些我们会在后期学习。**

**基于Spring AMQP生成的队列默认是持久化的**

#### 消息持久化

**在控制台发送消息的时候，可以添加很多参数，而消息的持久化是要配置一个`properties`：**

![](D:/StudyNote/assets/1739183762075.png)

**说明**：**在开启持久化机制以后，如果同时还开启了生产者确认，那么MQ会在消息持久化以后才发送ACK回执，进一步确保消息的可靠性。**

**不过出于性能考虑，为了减少IO次数，发送到MQ的消息并不是逐条持久化到数据库的，而是每隔一段时间批量持久化。一般间隔在100毫秒左右，这就会导致ACK有一定的延迟，因此建议生产者确认全部采用异步方式。**

**在spring amqp中实现消息的可持久化**

```
@Test
public void testSendMessage() {
    //自定义构建message对象
    Message message = MessageBuilder.withBody("hello".getBytes(StandardCharsets.UTF_8))
            .setDeliveryMode(MessageDeliveryMode.PERSISTENT)
            .build();
    rabbitTemplate.convertAndSend("simple.queue", message);
    
}
```

**代码中的setDeliveryMode函数用于设置消息的持久化操作**

### Lazy Queue

**在默认情况下，RabbitMQ会将接收到的信息保存在内存中以降低消息收发的延迟。但在某些特殊情况下，这会导致消息积压，比如：**

- **消费者宕机或出现网络故障**
- **消息发送量激增，超过了消费者处理速度**
- **消费者处理业务发生阻塞**

**一旦出现消息堆积问题，RabbitMQ的内存占用就会越来越高，直到触发内存预警上限。此时RabbitMQ会将内存消息刷到磁盘上，这个行为成为`PageOut`. `PageOut`会耗费一段时间，并且会阻塞队列进程。因此在这个过程中RabbitMQ不会再处理新的消息，生产者的所有请求都会被阻塞。**

**为了解决这个问题，从RabbitMQ的3.6.0版本开始，就增加了Lazy Queues的模式，也就是惰性队列。惰性队列的特征如下：**

- **接收到消息后直接存入磁盘而非内存**
- **消费者要消费消息时才会从磁盘中读取并加载到内存（也就是懒加载）**
- **支持数百万条的消息存储**

**而在3.12版本之后，LazyQueue已经成为所有队列的默认格式。因此官方推荐升级MQ为3.12版本或者所有队列都设置为LazyQueue模式。**

#### 控制台配置Lazy模式

**在添加队列的时候，添加`x-queue-mod=lazy`参数即可设置队列为Lazy模式：**

![](D:/StudyNote/assets/1739186360214(1).png)

#### 代码配置Lazy模式

**在利用SpringAMQP声明队列的时候，添加`x-queue-mod=lazy`参数也可设置队列为Lazy模式：**

```Java
@Bean
public Queue lazyQueue(){
    return QueueBuilder
            .durable("lazy.queue")
            .lazy() // 开启Lazy模式
            .build();
}
```

**当然，我们也可以基于注解来声明队列并设置为Lazy模式：**

```Java
@RabbitListener(queuesToDeclare = @Queue(
        name = "lazy.queue",
        durable = "true",
        arguments = @Argument(name = "x-queue-mode", value = "lazy")
))
public void listenLazyQueue(String msg){
    log.info("接收到 lazy.queue的消息：{}", msg);
}
```

#### 更新已有队列为lazy模式

**对于已经存在的队列，也可以配置为lazy模式，但是要通过设置policy实现。**

**可以基于命令行设置policy：**

```Shell
rabbitmqctl set_policy Lazy "^lazy-queue$" '{"queue-mode":"lazy"}' --apply-to queues  
```

**命令解读：**

- **`rabbitmqctl` ：RabbitMQ的命令行工具**
- **`set_policy` ：添加一个策略**
- **`Lazy` ：策略名称，可以自定义**
- **`"^lazy-queue$"` ：用正则表达式匹配队列的名字**
- **`'{"queue-mode":"lazy"}'` ：设置队列模式为lazy模式**
- **`--apply-to queues`：策略的作用对象，是所有的队列**

**当然，也可以在控制台配置policy，进入在控制台的`Admin`页面，点击`Policies`，即可添加配置：**

![](D:/StudyNote/assets/1739186663288(1).png)

## 消费者可靠性

### 消费者确认机制

**为了确认消费者是否成功处理消息，RabbitMQ提供了消费者确认机制（Consumer Acknowledgement）。即：当消费者处理消息结束后，应该向RabbitMQ发送一个回执，告知RabbitMQ自己消息处理状态。回执有三种可选值：**

- **ack：成功处理消息，RabbitMQ从队列中删除该消息**
- **nack：消息处理失败，RabbitMQ需要再次投递消息**
- **reject：消息处理失败并拒绝该消息，RabbitMQ从队列中删除该消息**

**一般reject方式用的较少，除非是消息格式有问题，那就是开发问题了。因此大多数情况下我们需要将消息处理的代码通过`try catch`机制捕获，消息处理成功时返回ack，处理失败时返回nack.**



**由于消息回执的处理代码比较统一，因此SpringAMQP帮我们实现了消息确认。并允许我们通过配置文件设置ACK处理方式，有三种模式：**

- **`none`：不处理。即消息投递给消费者后立刻ack，消息会立刻从MQ删除。非常不安全，不建议使用**
- **`manual`：手动模式。需要自己在业务代码中调用api，发送`ack`或`reject`，存在业务入侵，但更灵活**
- **`auto`：自动模式。SpringAMQP利用AOP对我们的消息处理逻辑做了环绕增强，当业务正常执行时则自动返回`ack`.  当业务出现异常时，根据异常判断返回不同结果：**
  - **如果是业务异常，会自动返回`nack`；**
  - **如果是消息处理或校验异常，自动返回`reject`;**

**返回Reject的常见异常有：**

> Starting with version 1.3.2, the default ErrorHandler is now a ConditionalRejectingErrorHandler that rejects (and does not requeue) messages that fail with an irrecoverable error. Specifically, it rejects messages that fail with the following errors:
>
> - o.s.amqp…MessageConversionException: Can be thrown when converting the incoming message payload using a MessageConverter.
> - o.s.messaging…MessageConversionException: Can be thrown by the conversion service if additional conversion is required when mapping to a @RabbitListener method.
> - o.s.messaging…MethodArgumentNotValidException: Can be thrown if validation (for example, @Valid) is used in the listener and the validation fails.
> - o.s.messaging…MethodArgumentTypeMismatchException: Can be thrown if the inbound message was converted to a type that is not correct for the target method. For example, the parameter is declared as Message<Foo> but Message<Bar> is received.
> - java.lang.NoSuchMethodException: Added in version 1.6.3.
> - java.lang.ClassCastException: Added in version 1.6.3.

通过下面的配置可以修改SpringAMQP的ACK处理方式：

```YAML
spring:
  rabbitmq:
    listener:
      simple:
        acknowledge-mode: none # 不做处理  
```



### 失败重试机制

**当消费者出现异常后，消息会不断requeue（重入队）到队列，再重新发送给消费者。如果消费者再次执行依然出错，消息会再次requeue到队列，再次投递，直到消息处理成功为止。**

**极端情况就是消费者一直无法执行成功，那么消息requeue就会无限循环，导致mq的消息处理飙升，带来不必要的压力：**

**当然，上述极端情况发生的概率还是非常低的，不过不怕一万就怕万一。为了应对上述情况Spring又提供了消费者失败重试机制：在消费者出现异常时利用本地重试，而不是无限制的requeue到mq队列。**

**修改consumer服务的application.yml文件，添加内容：**

```YAML
spring:
  rabbitmq:
    listener:
      simple:
        retry:
          enabled: true # 开启消费者失败重试
          initial-interval: 1000ms # 初识的失败等待时长为1秒
          multiplier: 1 # 失败的等待时长倍数，下次等待时长 = multiplier * last-interval
          max-attempts: 3 # 最大重试次数
          stateless: true # true无状态；false有状态。如果业务中包含事务，这里改为false
```

**重启consumer服务，重复之前的测试。可以发现：**

- **消费者在失败后消息没有重新回到MQ无限重新投递，而是在本地重试了3次**
- **本地重试3次以后，抛出了`AmqpRejectAndDontRequeueException`异常。查看RabbitMQ控制台，发现消息被删除了，说明最后SpringAMQP返回的是`reject`**

**结论：**

- **开启本地重试时，消息处理过程中抛出异常，不会requeue到队列，而是在消费者本地重试**
- **重试达到最大次数后，Spring会返回reject，消息会被丢弃**

### 失败处理策略

**在之前的测试中，本地测试达到最大重试次数后，消息会被丢弃。这在某些对于消息可靠性要求较高的业务场景下，显然不太合适了。**

**因此Spring允许我们自定义重试次数耗尽后的消息处理策略，这个策略是由`MessageRecovery`接口来定义的，它有3个不同实现：**

-  **`RejectAndDontRequeueRecoverer`：重试耗尽后，直接`reject`，丢弃消息。默认就是这种方式** 
-  **`ImmediateRequeueMessageRecoverer`：重试耗尽后，返回`nack`，消息重新入队** 
-  **`RepublishMessageRecoverer`：重试耗尽后，将失败消息投递到指定的交换机** 

**比较优雅的一种处理方案是`RepublishMessageRecoverer`，失败后将消息投递到一个指定的，专门存放异常消息的队列，后续由人工集中处理。**

**1）在consumer服务中定义处理失败消息的交换机和队列**

```Java
@Bean
public DirectExchange errorMessageExchange(){
    return new DirectExchange("error.direct");
}
@Bean
public Queue errorQueue(){
    return new Queue("error.queue", true);
}
@Bean
public Binding errorBinding(Queue errorQueue, DirectExchange errorMessageExchange){
    return BindingBuilder.bind(errorQueue).to(errorMessageExchange).with("error");
}
```

**2）定义一个RepublishMessageRecoverer，关联队列和交换机**

```Java
@Bean
public MessageRecoverer republishMessageRecoverer(RabbitTemplate rabbitTemplate){
    return new RepublishMessageRecoverer(rabbitTemplate, "error.direct", "error");
}
```

### 业务幂等性

**何为幂等性？**

**幂等是一个数学概念，用函数表达式来描述是这样的：`f(x) = f(f(x))`，例如求绝对值函数。**

**在程序开发中，则是指同一个业务，执行一次或多次对业务状态的影响是一致的。例如：**

- **根据id删除数据**
- **查询数据**
- **新增数据**

**但数据的更新往往不是幂等的，如果重复执行可能造成不一样的后果。比如：**

- **取消订单，恢复库存的业务。如果多次恢复就会出现库存重复增加的情况**
- **退款业务。重复退款对商家而言会有经济损失。**

**所以，我们要尽可能避免业务被重复执行。**

**然而在实际业务场景中，由于意外经常会出现业务被重复执行的情况，例如：**

- **页面卡顿时频繁刷新导致表单重复提交**
- **服务间调用的重试**
- **MQ消息的重复投递**

**我们在用户支付成功后会发送MQ消息到交易服务，修改订单状态为已支付，就可能出现消息重复投递的情况。如果消费者不做判断，很有可能导致消息被消费多次，出现业务故障。**

**举例：**

1. **假如用户刚刚支付完成，并且投递消息到交易服务，交易服务更改订单为已支付状态。**
2. **由于某种原因，例如网络故障导致生产者没有得到确认，隔了一段时间后重新投递给交易服务。**
3. **但是，在新投递的消息被消费之前，用户选择了退款，将订单状态改为了已退款状态。**
4. **退款完成后，新投递的消息才被消费，那么订单状态会被再次改为已支付。业务异常。**

**因此，我们必须想办法保证消息处理的幂等性。这里给出两种方案：**

- **唯一消息ID**
- **业务状态判断**

#### 唯一消息ID

**这个思路非常简单：**

1. **每一条消息都生成一个唯一的id，与消息一起投递给消费者。**
2. **消费者接收到消息后处理自己的业务，业务处理成功后将消息ID保存到数据库**
3. **如果下次又收到相同消息，去数据库查询判断是否存在，存在则为重复消息放弃处理。**

**我们该如何给消息添加唯一ID呢？**

**其实很简单，SpringAMQP的MessageConverter自带了MessageID的功能，我们只要开启这个功能即可。**

**以Jackson的消息转换器为例：**

```Java
@Bean
public MessageConverter messageConverter(){
    // 1.定义消息转换器
    Jackson2JsonMessageConverter jjmc = new Jackson2JsonMessageConverter();
    // 2.配置自动创建消息id，用于识别不同消息，也可以在业务中基于ID判断是否是重复消息
    jjmc.setCreateMessageIds(true);
    return jjmc;
}
```

**当然使用唯一消息id需要涉及到数据库操作会影响mq性能，一般建议建议在业务上操作，或者我们可以把id存储在Redis提高读写效率**

#### 业务判断

**业务判断就是基于业务本身的逻辑或状态来判断是否是重复的请求或消息，不同的业务场景判断的思路也不一样。**

**例如我们当前案例中，处理消息的业务逻辑是把订单状态从未支付修改为已支付。因此我们就可以在执行业务时判断订单状态是否是未支付，如果不是则证明订单已经被处理过，无需重复处理。**

**相比较而言，消息ID的方案需要改造原有的数据库，所以我更推荐使用业务判断的方案。**

**以支付修改订单的业务为例，我们需要修改`OrderServiceImpl`中的`markOrderPaySuccess`方法：**

```Java
    @Override
    public void markOrderPaySuccess(Long orderId) {
        // 1.查询订单
        Order old = getById(orderId);
        // 2.判断订单状态
        if (old == null || old.getStatus() != 1) {
            // 订单不存在或者订单状态不是1，放弃处理
            return;
        }
        // 3.尝试更新订单
        Order order = new Order();
        order.setId(orderId);
        order.setStatus(2);
        order.setPayTime(LocalDateTime.now());
        updateById(order);
    }
```

**上述代码逻辑上符合了幂等判断的需求，但是由于判断和更新是两步动作，因此在极小概率下可能存在线程安全问题。**

**我们可以合并上述操作为这样：**

```Java
@Override
public void markOrderPaySuccess(Long orderId) {
    // UPDATE `order` SET status = ? , pay_time = ? WHERE id = ? AND status = 1
    lambdaUpdate()
            .set(Order::getStatus, 2)
            .set(Order::getPayTime, LocalDateTime.now())
            .eq(Order::getId, orderId)
            .eq(Order::getStatus, 1)
            .update();
}
```

**注意看，上述代码等同于这样的SQL语句：**

```SQL
UPDATE `order` SET status = ? , pay_time = ? WHERE id = ? AND status = 1
```

**我们在where条件中除了判断id以外，还加上了status必须为1的条件。如果条件不符（说明订单已支付），则SQL匹配不到数据，根本不会执行。**

### 兜底方案

**虽然我们利用各种机制尽可能增加了消息的可靠性，但也不好说能保证消息100%的可靠。万一真的MQ通知失败该怎么办呢？**

**有没有其它兜底方案，能够确保订单的支付状态一致呢？**

**其实思想很简单：既然MQ通知不一定发送到交易服务，那么交易服务就必须自己主动去查询支付状态。这样即便支付服务的MQ通知失败，我们依然能通过主动查询来保证订单状态的一致。**

**流程如下：**

![](D:/StudyNote/assets/1739438076125.png)

**图中黄色线圈起来的部分就是MQ通知失败后的兜底处理方案，由交易服务自己主动去查询支付状态。**

**不过需要注意的是，交易服务并不知道用户会在什么时候支付，如果查询的时机不正确（比如查询的时候用户正在支付中），可能查询到的支付状态也不正确。**

**那么问题来了，我们到底该在什么时间主动查询支付状态呢？**

**这个时间是无法确定的，因此，通常我们采取的措施就是利用定时任务定期查询，例如每隔20秒就查询一次，并判断支付状态。如果发现订单已经支付，则立刻更新订单状态为已支付即可。**

**定时任务大家之前学习过，具体的实现这里就不再赘述了。**

**至此，消息可靠性的问题已经解决了。**

**综上，支付服务与交易服务之间的订单状态一致性是如何保证的？**

- **首先，支付服务会正在用户支付成功以后利用MQ消息通知交易服务，完成订单状态同步。**
- **其次，为了保证MQ消息的可靠性，我们采用了生产者确认机制、消费者确认、消费者失败重试等策略，确保消息投递的可靠性**
- **最后，我们还在交易服务设置了定时任务，定期查询订单支付状态。这样即便MQ通知失败，还可以利用定时任务作为兜底方案，确保订单支付状态的最终一致性。**

## 延迟消息

**在电商的支付业务中，对于一些库存有限的商品，为了更好的用户体验，通常都会在用户下单时立刻扣减商品库存。例如电影院购票、高铁购票，下单后就会锁定座位资源，其他人无法重复购买。**

**但是这样就存在一个问题，假如用户下单后一直不付款，就会一直占有库存资源，导致其他客户无法正常交易，最终导致商户利益受损！**

**因此，电商中通常的做法就是：对于超过一定时间未支付的订单，应该立刻取消订单并释放占用的库存。**

**例如，订单支付超时时间为30分钟，则我们应该在用户下单后的第30分钟检查订单支付状态，如果发现未支付，应该立刻取消订单，释放库存。**

**但问题来了：如何才能准确的实现在下单后第30分钟去检查支付状态呢？**

**像这种在一段时间以后才执行的任务，我们称之为延迟任务，而要实现延迟任务，最简单的方案就是利用MQ的延迟消息了。**

**在RabbitMQ中实现延迟消息也有两种方案：**

- **死信交换机+TTL**
- **延迟消息插件**

### 死信交换机

**什么是死信？**

**当一个队列中的消息满足下列情况之一时，可以成为死信（dead letter）：**

- **消费者使用`basic.reject`或 `basic.nack`声明消费失败，并且消息的`requeue`参数设置为false**
- **消息是一个过期消息，超时无人消费**
- **要投递的队列消息满了，无法投递**

**如果一个队列中的消息已经成为死信，并且这个队列通过`dead-letter-exchange`属性指定了一个交换机，那么队列中的死信就会投递到这个交换机中，而这个交换机就称为死信交换机（Dead Letter Exchange）。而此时加入有队列与死信交换机绑定，则最终死信就会被投递到这个队列中。**

**死信交换机有什么作用呢？**

​	**收集那些因处理失败而被拒绝的消息**

​	**收集那些因队列满了而被拒绝的消息**

​	**收集因TTL（有效期）到期的消息**

**前面两种作用场景可以看做是把死信交换机当做一种消息处理的最终兜底方案，与消费者重试时讲的`RepublishMessageRecoverer`作用类似。**

**而最后一种场景，大家设想一下这样的场景：**

**如图，有一组绑定的交换机（`ttl.fanout`）和队列（`ttl.queue`）。但是`ttl.queue`没有消费者监听，而是设定了死信交换机`hmall.direct`，而队列`direct.queue1`则与死信交换机绑定，RoutingKey是blue：**

![](D:/StudyNote/assets/1739441181213.png)

**假如我们现在发送一条消息到`ttl.fanout`，RoutingKey为blue，并设置消息的有效期为5000毫秒：**

![](D:/StudyNote/assets/1739441212712.png)

**注意：尽管这里的`ttl.fanout`不需要RoutingKey，但是当消息变为死信并投递到死信交换机时，会沿用之前的RoutingKey，这样`hmall.direct`才能正确路由消息。**

**消息肯定会被投递到`ttl.queue`之后，由于没有消费者，因此消息无人消费。5秒之后，消息的有效期到期，成为死信：**

![](D:/StudyNote/assets/1739441248965.png)

**死信被投递到死信交换机`hmall.direct`，并沿用之前的RoutingKey，也就是`blue`：**

![](D:/StudyNote/assets/1739441287173(1).png)

**由于`direct.queue1`与`hmall.direct`绑定的key是blue，因此最终消息被成功路由到`direct.queue1`，如果此时有消费者与`direct.queue1`绑定， 也就能成功消费消息了。但此时已经是5秒钟以后了：**

![](D:/StudyNote/assets/1739441325314(1).png)

**也就是说，publisher发送了一条消息，但最终consumer在5秒后才收到消息。我们成功实现了延迟消息。**

**注意：**

**RabbitMQ的消息过期是基于追溯方式来实现的，也就是说当一个消息的TTL到期以后不一定会被移除或投递到死信交换机，而是在消息恰好处于队首时才会被处理。**

**当队列中消息堆积很多的时候，过期消息可能不会被按时处理，因此你设置的TTL时间不一定准确。**

### DelayExchange插件

**基于死信队列虽然可以实现延迟消息，但是太麻烦了。因此RabbitMQ社区提供了一个延迟消息插件来实现相同的效果。**

**官方文档说明：**

https://blog.rabbitmq.com/posts/2015/04/scheduling-messages-with-rabbitmq

#### 下载

**插件下载地址：**

**https://github.com/rabbitmq/rabbitmq-delayed-message-exchange**

**由于我们安装的MQ是`3.8`版本，因此这里下载`3.8.17`版本：**

#### 安装

**因为我们是基于Docker安装，所以需要先查看RabbitMQ的插件目录对应的数据卷。**

```Shell
docker volume inspect mq-plugins
```

**结果如下：**

```JSON
[
    {
        "CreatedAt": "2024-06-19T09:22:59+08:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/mq-plugins/_data",
        "Name": "mq-plugins",
        "Options": null,
        "Scope": "local"
    }
]
```

**插件目录被挂载到了`/var/lib/docker/volumes/mq-plugins/_data`这个目录，我们上传插件到该目录下。**

**接下来执行命令，安装插件：**

```Shell
docker exec -it mq rabbitmq-plugins enable rabbitmq_delayed_message_exchange
```



#### 声明延迟交换机

**基于注解方式：**

```Java
@RabbitListener(bindings = @QueueBinding(
        value = @Queue(name = "delay.queue", durable = "true"),
        exchange = @Exchange(name = "delay.direct", delayed = "true"),
        key = "delay"
))
public void listenDelayMessage(String msg){
    log.info("接收到delay.queue的延迟消息：{}", msg);
}
```



**基于`@Bean`的方式：**

```Java
package com.itheima.consumer.config;

import lombok.extern.slf4j.Slf4j;
import org.springframework.amqp.core.*;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Slf4j
@Configuration
public class DelayExchangeConfig {

    @Bean
    public DirectExchange delayExchange(){
        return ExchangeBuilder
                .directExchange("delay.direct") // 指定交换机类型和名称
                .delayed() // 设置delay的属性为true
                .durable(true) // 持久化
                .build();
    }

    @Bean
    public Queue delayedQueue(){
        return new Queue("delay.queue");
    }
    
    @Bean
    public Binding delayQueueBinding(){
        return BindingBuilder.bind(delayedQueue()).to(delayExchange()).with("delay");
    }
}
```

#### 发送延迟消息

**发送消息时，必须通过x-delay属性设定延迟时间：**

```Java
@Test
void testPublisherDelayMessage() {
    // 1.创建消息
    String message = "hello, delayed message";
    // 2.发送消息，利用消息后置处理器添加消息头
    rabbitTemplate.convertAndSend("delay.direct", "delay", message, new MessagePostProcessor() {
        @Override
        public Message postProcessMessage(Message message) throws AmqpException {
            // 添加延迟消息属性
            message.getMessageProperties().setDelay(5000);
            return message;
        }
    });
}
```

**注意：**

**延迟消息插件内部会维护一个本地数据库表，同时使用Elang Timers功能实现计时。如果消息的延迟时间设置较长，可能会导致堆积的延迟消息非常多，会带来较大的CPU开销，同时延迟消息的时间会存在误差。**

**因此，不建议设置延迟时间过长的延迟消息。**

## 基于mq通信的两个服务传递用户信息

**某些业务中，需要根据登录用户信息处理业务，而基于MQ的异步调用并不会传递登录用户信息。前面我们的做法比较麻烦，至少要做两件事：**

- **消息发送者在消息体中传递登录用户**
- **消费者获取消息体中的登录用户，处理业务**

**这样做不仅麻烦，而且编程体验也不统一，毕竟我们之前都是使用UserContext来获取用户。**

### 方案一：在发送消息和接受消息时进行处理

**发送者**

```java
rabbitTemplate.convertAndSend("trade.topic", "order.create", itemIds, message -> {
    message.getMessageProperties().setHeader("user-info", UserContext.getUser());
    return message;
});
```

**使用MessagePostProcessor对消息添加处理操作，首先获取Message对象，然后给消息添加一个请求头“user-info”，用于存储用户信息**

**消费者**

```java
@RabbitListener(bindings = @QueueBinding(
        value = @Queue(name = "cart.clear.queue", durable = "true"),
        exchange = @Exchange(name = "trade.topic"),
        key = {"order.create"}

))
public void listenCartClear(Collection<Long> ids, Message message) {
    log.info("收到订单创建消息，准备清除购物车数据");
    UserContext.setUser(message.getMessageProperties().getHeader("user-info"));
    cartService.removeByItemIds(ids);
}
```



**在消费者的接收消息的方法里添加Message类型的参数，然后在方法拿到消息的请求头，获取里面的user-info数据，并存入ThreadLocaL**

### **方案二：通过修改mq的配置来实现上述操作**

```java
package com.hmall.common.config;

import com.hmall.common.utils.UserContext;
import lombok.AllArgsConstructor;
import lombok.extern.slf4j.Slf4j;
import org.aopalliance.intercept.MethodInterceptor;
import org.springframework.amqp.core.Message;
import org.springframework.amqp.core.MessagePostProcessor;
import org.springframework.amqp.rabbit.config.SimpleRabbitListenerContainerFactory;
import org.springframework.amqp.rabbit.connection.ConnectionFactory;
import org.springframework.amqp.rabbit.core.RabbitTemplate;
import org.springframework.amqp.support.converter.Jackson2JsonMessageConverter;
import org.springframework.amqp.support.converter.MessageConverter;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import javax.annotation.PostConstruct;

@Configuration
@Slf4j
@AllArgsConstructor
public class MqConfig {
    @Bean
    public MessageConverter messageConverter(){
        log.info("初始化消息转换器.......");
        // 1.定义消息转换器
        Jackson2JsonMessageConverter jjmc = new Jackson2JsonMessageConverter();
        // 2.配置自动创建消息id，用于识别不同消息，也可以在业务中基于ID判断是否是重复消息
        jjmc.setCreateMessageIds(true);
        return jjmc;
    }


    @Bean
    public MessagePostProcessor messagePostProcessor(){
        log.info("初始化消息头信息.......");
        return message -> {
            message.getMessageProperties().setHeader("user-info", UserContext.getUser());
            return message;
        };
    }

    @Bean
    public MethodInterceptor userContextMessageAdvice(){
        log.info("初始化消息拦截器.....");
        return invocation -> {
            for(Object arg : invocation.getArguments()){
                if(arg instanceof Message){
                    Message message = (Message) arg;
                    UserContext.setUser(message.getMessageProperties().getHeader("user-info"));
                    break;
                }
            }
            return invocation.proceed();
        };
    }


    @Bean
    public RabbitTemplate rabbitTemplate(ConnectionFactory connectionFactory){
        RabbitTemplate rabbitTemplate = new RabbitTemplate(connectionFactory);
        rabbitTemplate.setMessageConverter(messageConverter());
        rabbitTemplate.setBeforePublishPostProcessors(messagePostProcessor());
        return rabbitTemplate;
    }

    @Bean
    public SimpleRabbitListenerContainerFactory rabbitListenerContainerFactory(ConnectionFactory connectionFactory){
        SimpleRabbitListenerContainerFactory factory = new SimpleRabbitListenerContainerFactory();
        factory.setConnectionFactory(connectionFactory);
        factory.setMessageConverter(messageConverter());
        factory.setAdviceChain(userContextMessageAdvice());
        return factory;
    }

}
```

**MessagePostProcessor 的作用**

**MessagePostProcessor 允许你在消息的生命周期中插入自定义逻辑，通常用于以下场景：**

**消息发送前的处理：在消息发送到 RabbitMQ 之前，修改消息的属性（例如设置消息头、过期时间、优先级等）。**

**消息消费后的处理：在消息从 RabbitMQ 消费之后，对消息进行额外的处理（例如记录日志、修改消息内容等）。**



**SimpleRabbitListenerContainerFactory 的作用**

**SimpleRabbitListenerContainerFactory 是 Spring AMQP 提供的一个工厂类，用于创建和管理 RabbitMQ 消息监听器的容器（SimpleMessageListenerContainer）。它的主要作用包括：**

**配置消息监听器的连接工厂（ConnectionFactory）。**

**设置消息转换器（MessageConverter），用于将 RabbitMQ 的消息体转换为 Java 对象。**

**添加拦截器链（AdviceChain），用于在消息处理前后执行自定义逻辑。**



**首先要在配置端实现消息传递的效果，我们需要重新自定义一个RabbitListener，因为是我们自定义的我们需要为他设置ConnectionFactory，ConnectionFactory系统已经有默认的创建好的，我们直接用参数的形式进行依赖注入，拿到这个ConnectionFactory，此外我们还需要消息转换器，直接将相关的方法导入就行，最后就是在发送消息添加一个MessagePostProcessor，对所有的消息，在消息发送前进行添加请求头的操作**

**消费者监听到消息时，我们还需要把消息头中的信息拿出来存入ThreadLocal，这时候就需要一个类SimpleRabbitListener去添加一个拦截器链，用于把消息的请求头中的数据存入ThreadLocal,这里我们使用的是MethodInterceptor**

