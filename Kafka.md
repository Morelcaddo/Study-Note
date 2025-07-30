# **Kafka**

## **kafka概述**

**消息中间件对比**                              

| **特性**       | **ActiveMQ**                               | **RabbitMQ**                   | **RocketMQ**                 | **Kafka**                                    |
| -------------- | ------------------------------------------ | ------------------------------ | ---------------------------- | -------------------------------------------- |
| **开发语言**   | **java**                                   | **erlang**                     | **java**                     | **scala**                                    |
| **单机吞吐量** | **万级**                                   | **万级**                       | **10万级**                   | **100万级**                                  |
| **时效性**     | **ms**                                     | **us**                         | **ms**                       | **ms级以内**                                 |
| **可用性**     | **高（主从）**                             | **高（主从）**                 | **非常高（分布式）**         | **非常高（分布式）**                         |
| **功能特性**   | **成熟的产品、较全的文档、各种协议支持好** | **并发能力强、性能好、延迟低** | **MQ功能比较完善，扩展性佳** | **只支持主要的MQ功能，主要应用于大数据领域** |

**消息中间件对比-选择建议**

| **消息中间件** | **建议**                                                     |
| -------------- | ------------------------------------------------------------ |
| **Kafka**      | **追求高吞吐量，适合产生大量数据的互联网服务的数据收集业务** |
| **RocketMQ**   | **可靠性要求很高的金融互联网领域,稳定性高，经历了多次阿里双11考验** |
| **RabbitMQ**   | **性能较好，社区活跃度高，数据量没有那么大，优先选择功能比较完备的RabbitMQ** |

**kafka介绍**

**Kafka 是一个分布式流媒体平台,类似于消息队列或企业消息传递系统。kafka官网：http://kafka.apache.org/**  

**![image-20210525181028436](assets\image-20210525181028436.png)**

**kafka介绍-名词解释**

**![image-20210525181100793](assets\image-20210525181100793.png)**

- **producer：发布消息的对象称之为主题生产者（Kafka topic producer）**

- **topic：Kafka将消息分门别类，每一类的消息称之为一个主题（Topic）**

- **consumer：订阅消息并处理发布的消息的对象称之为主题消费者（consumers）**

- **broker：已发布的消息保存在一组服务器中，称之为Kafka集群。集群中的每一个服务器都是一个代理（Broker）。 消费者可以订阅一个或多个主题（topic），并从Broker拉数据，从而消费这些已发布的消息。**

## **kafka安装配置**

**Kafka对于zookeeper是强依赖，保存kafka相关的节点数据，所以安装Kafka之前必须先安装zookeeper**

- **Docker安装zookeeper**

**下载镜像：**

```shell
docker pull zookeeper:3.4.14
```

**创建容器**

```shell
docker run -d --name zookeeper -p 2181:2181 zookeeper:3.4.14
```

- **Docker安装kafka**

**下载镜像：**

```shell
docker pull wurstmeister/kafka:2.12-2.3.1
```

**创建容器**

```shell
docker run -d --name kafka \
--env KAFKA_ADVERTISED_HOST_NAME=192.168.200.130 \
--env KAFKA_ZOOKEEPER_CONNECT=192.168.200.130:2181 \
--env KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://192.168.200.130:9092 \
--env KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 \
--env KAFKA_HEAP_OPTS="-Xmx256M -Xms256M" \
--net=host wurstmeister/kafka:2.12-2.3.1
```

## **kafka入门**

**![image-20210525181412230](assets\image-20210525181412230.png)**

**（1）创建kafka-demo项目，导入依赖**

```xml
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-clients</artifactId>
</dependency>
```

**（2）生产者发送消息**

```java
package com.heima.kafka.sample;

import org.apache.kafka.clients.producer.KafkaProducer;
import org.apache.kafka.clients.producer.ProducerConfig;
import org.apache.kafka.clients.producer.ProducerRecord;

import java.util.Properties;

/**
 * 生产者
 */
public class ProducerQuickStart {

    public static void main(String[] args) {
        //1.kafka的配置信息
        Properties properties = new Properties();
        //kafka的连接地址
        properties.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG,"192.168.200.130:9092");
        //发送失败，失败的重试次数
        properties.put(ProducerConfig.RETRIES_CONFIG,5);
        //消息key的序列化器
        properties.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG,"org.apache.kafka.common.serialization.StringSerializer");
        //消息value的序列化器
        properties.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG,"org.apache.kafka.common.serialization.StringSerializer");

        //2.生产者对象
        KafkaProducer<String,String> producer = new KafkaProducer<String, String>(properties);

        //封装发送的消息
        ProducerRecord<String,String> record = new ProducerRecord<String, String>("itheima-topic","100001","hello kafka");

        //3.发送消息
        producer.send(record);

        //4.关闭消息通道，必须关闭，否则消息发送不成功
        producer.close();
    }

}
```



**（3）消费者接收消息**

```java
package com.heima.kafka.sample;

import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.apache.kafka.clients.consumer.ConsumerRecords;
import org.apache.kafka.clients.consumer.KafkaConsumer;

import java.time.Duration;
import java.util.Collections;
import java.util.Properties;

/**
 * 消费者
 */
public class ConsumerQuickStart {

    public static void main(String[] args) {
        //1.添加kafka的配置信息
        Properties properties = new Properties();
        //kafka的连接地址
        properties.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "192.168.200.130:9092");
        //消费者组
        properties.put(ConsumerConfig.GROUP_ID_CONFIG, "group2");
        //消息的反序列化器
        properties.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");
        properties.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, "org.apache.kafka.common.serialization.StringDeserializer");

        //2.消费者对象
        KafkaConsumer<String, String> consumer = new KafkaConsumer<String, String>(properties);

        //3.订阅主题
        consumer.subscribe(Collections.singletonList("itheima-topic"));

        //当前线程一直处于监听状态
        while (true) {
            //4.获取消息
            ConsumerRecords<String, String> consumerRecords = consumer.poll(Duration.ofMillis(1000));
            for (ConsumerRecord<String, String> consumerRecord : consumerRecords) {
                System.out.println(consumerRecord.key());
                System.out.println(consumerRecord.value());
            }
        }

    }

}
```

**总结**

- **生产者发送消息，多个消费者订阅同一个主题，同一个组下，只能有一个消费者收到消息（一对一）**

**![](assets\1747990351307(1).png)**



- **生产者发送消息，多个消费者订阅同一个主题，不同组的所有消费者都能收到消息（一对多）**

**![](assets/1747990473418(1).png)**

## **kafka分区机制**

**![](assets/1747991389320(1).png)**

**Kafka 中的分区机制指的是将每个主题划分成多个分区（Partition）**

**可以处理更多的消息，不受单台服务器的限制，可以不受限的处理更多的数据**

**topic剖析**

**![](assets/1747991464724(1).png)**

**每一个分区都是一个顺序的、不可变的消息队列， 并且可以持续的添加。分区中的消息都被分了一个序列号，称之为偏移量(offset)，在每个分区中此偏移量都是唯一的。**

**分区策略**

| **分区策略**     | **说明**                                                     |
| ---------------- | ------------------------------------------------------------ |
| **轮询策略**     | **按顺序轮流将每条数据分配到每个分区中**                     |
| **随机策略**     | **每次都随机地将消息分配到每个分区**                         |
| **按键保存策略** | **生产者发送数据的时候，可以指定一个key，计算这个key的hashCode值，按照hashCode的值对不同消息进行存储** |

## **kafka高可用设计**

### **集群**

**![image-20210530223101568](assets\image-20210530223101568.png)**

- **Kafka 的服务器端由被称为 Broker 的服务进程构成，即一个 Kafka 集群由多个 Broker 组成**

- **这样如果集群中某一台机器宕机，其他机器上的 Broker 也依然能够对外提供服务。这其实就是 Kafka 提供高可用的手段之一**

### **备份机制(Replication）**

**![image-20210530223218580](assets\image-20210530223218580.png)**

**Kafka 中消息的备份又叫做 副本（Replica）**

**Kafka 定义了两类副本：**

- **领导者副本（Leader Replica）**

- **追随者副本（Follower Replica）**

**同步方式**

**![image-20210530223316815](assets\image-20210530223316815.png)**

**ISR（in-sync replica）需要同步复制保存的follower**



**如果leader失效后，需要选出新的leader，选举的原则如下：**

**第一：选举时优先从ISR中选定，因为这个列表中follower的数据是与leader同步的**

**第二：如果ISR列表中的follower都不行了，就只能从其他follower中选取**



**极端情况，就是所有副本都失效了，这时有两种方案**

**第一：等待ISR中的一个活过来，选为Leader，数据可靠，但活过来的时间不确定**

**第二：选择第一个活过来的Replication，不一定是ISR中的，选为leader，以最快速度恢复可用性，但数据不一定完整**

## **kafka生产者详解** 

### **发送类型**

- **同步发送**

  **使用send()方法发送，它会返回一个Future对象，调用get()方法进行等待，就可以知道消息是否发送成功**

```java
RecordMetadata recordMetadata = producer.send(kvProducerRecord).get();
System.out.println(recordMetadata.offset());
```

- **异步发送**

  **调用send()方法，并指定一个回调函数，服务器在返回响应时调用函数**

```java
//异步消息发送
producer.send(kvProducerRecord, new Callback() {
    @Override
    public void onCompletion(RecordMetadata recordMetadata, Exception e) {
        if(e != null){
            System.out.println("记录异常信息到日志表中");
        }
        System.out.println(recordMetadata.offset());
    }
});
```

### **参数详解**

#### **ack**

**![image-20210530224302935](D:/BaiduNetdiskDownload/3、黑马程序员Java微服务项目《黑马头条》/Day01/3、黑马程序员Java微服务项目《黑马头条》/day06-kafka及异步通知文章上下架/讲义/kafka及异步通知文章上下架.assets/image-20210530224302935.png)**

**代码的配置方式：**

```java
//ack配置  消息确认机制
prop.put(ProducerConfig.ACKS_CONFIG,"all");
```

**参数的选择说明**

| **确认机制**         | **说明**                                                     |
| -------------------- | ------------------------------------------------------------ |
| **acks=0**           | **生产者在成功写入消息之前不会等待任何来自服务器的响应,消息有丢失的风险，但是速度最快** |
| **acks=1（默认值）** | **只要集群首领节点收到消息，生产者就会收到一个来自服务器的成功响应** |
| **acks=all**         | **只有当所有参与赋值的节点全部收到消息时，生产者才会收到一个来自服务器的成功响应** |

#### **retries**

**![image-20210530224406689](D:\BaiduNetdiskDownload\3、黑马程序员Java微服务项目《黑马头条》\Day01\3、黑马程序员Java微服务项目《黑马头条》\day06-kafka及异步通知文章上下架\讲义\kafka及异步通知文章上下架.assets\image-20210530224406689.png)**

**生产者从服务器收到的错误有可能是临时性错误，在这种情况下，retries参数的值决定了生产者可以重发消息的次数，如果达到这个次数，生产者会放弃重试返回错误，默认情况下，生产者会在每次重试之间等待100ms**

**代码中配置方式：**

```java
//重试次数
prop.put(ProducerConfig.RETRIES_CONFIG,10);
```

#### **消息压缩**

**默认情况下， 消息发送时不会被压缩。**

**代码中配置方式：**

```java
//数据压缩
prop.put(ProducerConfig.COMPRESSION_TYPE_CONFIG,"lz4");
```

| **压缩算法** | **说明**                                                     |
| ------------ | ------------------------------------------------------------ |
| **snappy**   | **占用较少的  CPU，  却能提供较好的性能和相当可观的压缩比， 如果看重性能和网络带宽，建议采用** |
| **lz4**      | **占用较少的 CPU， 压缩和解压缩速度较快，压缩比也很客观**    |
| **gzip**     | **占用较多的  CPU，但会提供更高的压缩比，网络带宽有限，可以使用这种算法** |

**使用压缩可以降低网络传输开销和存储开销，而这往往是向 Kafka 发送消息的瓶颈所在。**

### **生产者配置**

|                   **NAME**                   | **DESCRIPTION**                                              | **TYPE**     | **DEFAULT**                                                  | **VALID VALUES**       | **IMPORTANCE** |
| :------------------------------------------: | ------------------------------------------------------------ | ------------ | ------------------------------------------------------------ | ---------------------- | -------------- |
|            **bootstrap.servers**             | **host/port列表，用于初始化建立和Kafka集群的连接。列表格式为host1:port1,host2:port2,....，无需添加所有的集群地址，kafka会根据提供的地址发现其他的地址（你可以多提供几个，以防提供的服务器关闭）** | **list**     |                                                              |                        | **high**       |
|              **key.serializer**              | **实现 org.apache.kafka.common.serialization.Serializer 接口的 key 的 Serializer  类。** | **class**    |                                                              |                        | **high**       |
|             **value.serializer**             | **实现 org.apache.kafka.common.serialization.Serializer 接口的value 的 Serializer  类。** | **class**    |                                                              |                        | **high**       |
|                   **acks**                   | **生产者需要leader确认请求完成之前接收的应答数。此配置控制了发送消息的耐用性，支持以下配置：** | **string**   | **1**                                                        | **[all, -1, 0, 1]**    | **high**       |
|                                              | **acks=0  如果设置为0，那么生产者将不等待任何消息确认。消息将立刻添加到socket缓冲区并考虑发送。在这种情况下不能保障消息被服务器接收到。并且重试机制不会生效（因为客户端不知道故障了没有）。每个消息返回的offset始终设置为-1。** |              |                                                              |                        |                |
|                                              | **acks=1，这意味着leader写入消息到本地日志就立即响应，而不等待所有follower应答。在这种情况下，如果响应消息之后但follower还未复制之前leader立即故障，那么消息将会丢失。** |              |                                                              |                        |                |
|                                              | **acks=all  这意味着leader将等待所有副本同步后应答消息。此配置保障消息不会丢失（只要至少有一个同步的副本或者）。这是最强壮的可用性保障。等价于acks=-1。** |              |                                                              |                        |                |
|              **buffer.memory**               | **生产者用来缓存等待发送到服务器的消息的内存总字节数。如果消息发送比可传递到服务器的快，生产者将阻塞max.block.ms之后，抛出异常。** | **long**     | **33554432**                                                 | **[0,...]**            | **high**       |
|                                              | **此设置应该大致的对应生产者将要使用的总内存，但不是硬约束，因为生产者所使用的所有内存都用于缓冲。一些额外的内存将用于压缩（如果启动压缩），以及用于保持发送中的请求。** |              |                                                              |                        |                |
|             **compression.type**             | **数据压缩的类型。默认为空（就是不压缩）。有效的值有 none，gzip，snappy, 或  lz4。压缩全部的数据批，因此批的效果也将影响压缩的比率（更多的批次意味着更好的压缩）。** | **string**   | **none**                                                     |                        | **high**       |
|                 **retries**                  | **设置一个比零大的值，客户端如果发送失败则会重新发送。注意，这个重试功能和客户端在接到错误之后重新发送没什么不同。如果max.in.flight.requests.per.connection没有设置为1，有可能改变消息发送的顺序，因为如果2个批次发送到一个分区中，并第一个失败了并重试，但是第二个成功了，那么第二个批次将超过第一个。** | **int**      | **0**                                                        | **[0,...,2147483647]** | **high**       |
|             **ssl.key.password**             | **密钥仓库文件中的私钥的密码。**                             | **password** | **null**                                                     |                        | **high**       |
|          **ssl.keystore.location**           | **密钥仓库文件的位置。可用于客户端的双向认证。**             | **string**   | **null**                                                     |                        | **high**       |
|          **ssl.keystore.password**           | **密钥仓库文件的仓库密码。只有配置了ssl.keystore.location时才需要。** | **password** | **null**                                                     |                        | **high**       |
|         **ssl.truststore.location**          | **信任仓库的位置**                                           | **string**   | **null**                                                     |                        | **high**       |
|         **ssl.truststore.password**          | **信任仓库文件的密码**                                       | **password** | **null**                                                     |                        | **high**       |
|                **batch.size**                | **当多个消息要发送到相同分区的时，生产者尝试将消息批量打包在一起，以减少请求交互。这样有助于客户端和服务端的性能提升。该配置的默认批次大小（以字节为单位）：** | **int**      | **16384**                                                    | **[0,...]**            | **medium**     |
|                                              | **不会打包大于此配置大小的消息。**                           |              |                                                              |                        |                |
|                                              | **发送到broker的请求将包含多个批次，每个分区一个，用于发送数据。** |              |                                                              |                        |                |
|                                              | **较小的批次大小有可能降低吞吐量（批次大小为0则完全禁用批处理）。一个非常大的批次大小可能更浪费内存。因为我们会预先分配这个资源。** |              |                                                              |                        |                |
|                **client.id**                 | **当发出请求时传递给服务器的id字符串。这样做的目的是允许服务器请求记录记录这个【逻辑应用名】，这样能够追踪请求的源，而不仅仅只是ip/prot。** | **string**   | **""**                                                       |                        | **medium**     |
|         **connections.max.idle.ms**          | **多少毫秒之后关闭闲置的连接。**                             | **long**     | **540000**                                                   |                        | **medium**     |
|                **linger.ms**                 | **生产者组将发送的消息组合成单个批量请求。正常情况下，只有消息到达的速度比发送速度快的情况下才会出现。但是，在某些情况下，即使在适度的负载下，客户端也可能希望减少请求数量。此设置通过添加少量人为延迟来实现。-  也就是说，不是立即发出一个消息，生产者将等待一个给定的延迟，以便和其他的消息可以组合成一个批次。这类似于Nagle在TCP中的算法。此设置给出批量延迟的上限：一旦我们达到分区的batch.size值的记录，将立即发送，不管这个设置如何，但是，如果比这个小，我们将在指定的“linger”时间内等待更多的消息加入。此设置默认为0（即无延迟）。假设，设置  linger.ms=5，将达到减少发送的请求数量的效果，但对于在没有负载情况，将增加5ms的延迟。** | **long**     | **0**                                                        | **[0,...]**            | **medium**     |
|               **max.block.ms**               | **该配置控制 KafkaProducer.send() 和 KafkaProducer.partitionsFor()  将阻塞多长时间。此外这些方法被阻止，也可能是因为缓冲区已满或元数据不可用。在用户提供的序列化程序或分区器中的锁定不会计入此超时。** | **long**     | **60000**                                                    | **[0,...]**            | **medium**     |
|             **max.request.size**             | **请求的最大大小（以字节为单位）。此设置将限制生产者的单个请求中发送的消息批次数，以避免发送过大的请求。这也是最大消息批量大小的上限。请注意，服务器拥有自己的批量大小，可能与此不同。** | **int**      | **1048576**                                                  | **[0,...]**            | **medium**     |
|            **partitioner.class**             | **实现Partitioner接口的的Partitioner类。**                   | **class**    | **org.apache.kafka.clients.producer.internals.DefaultPartitioner** |                        | **medium**     |
|           **receive.buffer.bytes**           | **读取数据时使用的TCP接收缓冲区(SO_RCVBUF)的大小。如果值为-1，则将使用OS默认值。** | **int**      | **32768**                                                    | **[-1,...]**           | **medium**     |
|            **request.timeout.ms**            | **该配置控制客户端等待请求响应的最长时间。如果在超时之前未收到响应，客户端将在必要时重新发送请求，如果重试耗尽，则该请求将失败。  这应该大于replica.lag.time.max.ms，以减少由于不必要的生产者重试引起的消息重复的可能性。** | **int**      | **30000**                                                    | **[0,...]**            | **medium**     |
|             **sasl.jaas.config**             | **JAAS配置文件使用的格式的SASL连接的JAAS登录上下文参数。这里描述JAAS配置文件格式。该值的格式为：'（=）*;'** | **password** | **null**                                                     |                        | **medium**     |
|        **sasl.kerberos.service.name**        | **Kafka运行的Kerberos主体名称。可以在Kafka的JAAS配置或Kafka的配置中定义。** | **string**   | **null**                                                     |                        | **medium**     |
|              **sasl.mechanism**              | **SASL机制用于客户端连接。这是安全提供者可用与任何机制。GSSAPI是默认机制。** | **string**   | **GSSAPI**                                                   |                        | **medium**     |
|            **security.protocol**             | **用于与broker通讯的协议。 有效值为：PLAINTEXT，SSL，SASL_PLAINTEXT，SASL_SSL。** | **string**   | **PLAINTEXT**                                                |                        | **medium**     |
|            **send.buffer.bytes**             | **发送数据时，用于TCP发送缓存（SO_SNDBUF）的大小。如果值为 -1，将默认使用系统的。** | **int**      | **131072**                                                   | **[-1,...]**           | **medium**     |
|          **ssl.enabled.protocols**           | **启用SSL连接的协议列表。**                                  | **list**     | **TLSv1.2,TLSv1.1,TLSv1**                                    |                        | **medium**     |
|            **ssl.keystore.type**             | **密钥存储文件的文件格式。对于客户端是可选的。**             | **string**   | **JKS**                                                      |                        | **medium**     |
|               **ssl.protocol**               | **最近的JVM中允许的值是TLS，TLSv1.1和TLSv1.2。  较旧的JVM可能支持SSL，SSLv2和SSLv3，但由于已知的安全漏洞，不建议使用SSL。** | **string**   | **TLS**                                                      |                        | **medium**     |
|               **ssl.provider**               | **用于SSL连接的安全提供程序的名称。默认值是JVM的默认安全提供程序。** | **string**   | **null**                                                     |                        | **medium**     |
|           **ssl.truststore.type**            | **信任仓库文件的文件格式。**                                 | **string**   | **JKS**                                                      |                        | **medium**     |
|            **enable.idempotence**            | **当设置为‘true’，生产者将确保每个消息正好一次复制写入到stream。如果‘false’，由于broker故障，生产者重试。即，可以在流中写入重试的消息。此设置默认是‘false’。请注意，启用幂等式需要将max.in.flight.requests.per.connection设置为1，重试次数不能为零。另外acks必须设置为“全部”。如果这些值保持默认值，我们将覆盖默认值。  如果这些值设置为与幂等生成器不兼容的值，则将抛出一个ConfigException异常。如果这些值设置为与幂等生成器不兼容的值，则将抛出一个ConfigException异常。** | **boolean**  | **FALSE**                                                    |                        | **low**        |
|           **interceptor.classes**            | **实现ProducerInterceptor接口，你可以在生产者发布到Kafka群集之前拦截（也可变更）生产者收到的消息。默认情况下没有拦截器。** | **list**     | **null**                                                     |                        | **low**        |
|  **max.in.flight.requests.per.connection**   | **阻塞之前，客户端单个连接上发送的未应答请求的最大数量。注意，如果此设置设置大于1且发送失败，则会由于重试（如果启用了重试）会导致消息重新排序的风险。** | **int**      | **5**                                                        | **[1,...]**            | **low**        |
|           **metadata.max.age.ms**            | **在一段时间段之后（以毫秒为单位），强制更新元数据，即使我们没有看到任何分区leader的变化，也会主动去发现新的broker或分区。** | **long**     | **300000**                                                   | **[0,...]**            | **low**        |
|             **metric.reporters**             | **用作metrics reporters（指标记录员）的类的列表。实现MetricReporter接口，将受到新增加的度量标准创建类插入的通知。  JmxReporter始终包含在注册JMX统计信息中。** | **list**     | **""**                                                       |                        | **low**        |
|           **metrics.num.samples**            | **维护用于计算度量的样例数量。**                             | **int**      | **2**                                                        | **[1,...]**            | **low**        |
|         **metrics.recording.level**          | **指标的最高记录级别。**                                     | **string**   | **INFO**                                                     | **[INFO, DEBUG]**      | **low**        |
|         **metrics.sample.window.ms**         | **度量样例计算上**                                           | **long**     | **30000**                                                    | **[0,...]**            | **low**        |
|         **reconnect.backoff.max.ms**         | **重新连接到重复无法连接的代理程序时等待的最大时间（毫秒）。 如果提供，每个主机的回退将会连续增加，直到达到最大值。  计算后退增加后，增加20％的随机抖动以避免连接风暴。** | **long**     | **1000**                                                     | **[0,...]**            | **low**        |
|           **reconnect.backoff.ms**           | **尝试重新连接到给定主机之前等待的基本时间量。这避免了在循环中高频率的重复连接到主机。这种回退适应于客户端对broker的所有连接尝试。** | **long**     | **50**                                                       | **[0,...]**            | **low**        |
|             **retry.backoff.ms**             | **尝试重试指定topic分区的失败请求之前等待的时间。这样可以避免在某些故障情况下高频次的重复发送请求。** | **long**     | **100**                                                      | **[0,...]**            | **low**        |
|         **sasl.kerberos.kinit.cmd**          | **Kerberos kinit 命令路径。**                                | **string**   | **/usr/bin/kinit**                                           |                        | **low**        |
|  **sasl.kerberos.min.time.before.relogin**   | **Login线程刷新尝试之间的休眠时间。**                        | **long**     | **60000**                                                    |                        | **low**        |
|    **sasl.kerberos.ticket.renew.jitter**     | **添加更新时间的随机抖动百分比。**                           | **double**   | **0.05**                                                     |                        | **low**        |
| **sasl.kerberos.ticket.renew.window.factor** | **登录线程将睡眠，直到从上次刷新ticket到期时间的指定窗口因子为止，此时将尝试续订ticket。** | **double**   | **0.8**                                                      |                        | **low**        |
|            **ssl.cipher.suites**             | **密码套件列表。这是使用TLS或SSL网络协议来协商用于网络连接的安全设置的认证，加密，MAC和密钥交换算法的命名组合。默认情况下，支持所有可用的密码套件。** | **list**     | **null**                                                     |                        | **low**        |
|  **ssl.endpoint.identification.algorithm**   | **使用服务器证书验证服务器主机名的端点识别算法。**           | **string**   | **null**                                                     |                        | **low**        |
|         **ssl.keymanager.algorithm**         | **用于SSL连接的密钥管理因子算法。默认值是为Java虚拟机配置的密钥管理器工厂算法。** | **string**   | **SunX509**                                                  |                        | **low**        |
|     **ssl.secure.random.implementation**     | **用于SSL加密操作的SecureRandom PRNG实现。**                 | **string**   | **null**                                                     |                        | **low**        |
|        **ssl.trustmanager.algorithm**        | **用于SSL连接的信任管理因子算法。默认值是JAVA虚拟机配置的信任管理工厂算法。** | **string**   | **PKIX**                                                     |                        | **low**        |
|          **transaction.timeout.ms**          | **生产者在主动中止正在进行的交易之前，交易协调器等待事务状态更新的最大时间（以ms为单位）。如果此值大于broker中的max.transaction.timeout.ms设置，则请求将失败，并报“InvalidTransactionTimeout”错误。** | **int**      | **60000**                                                    |                        | **low**        |
|             **transactional.id**             | **用于事务传递的TransactionalId。这样可以跨多个生产者会话的可靠性语义，因为它允许客户端保证在开始任何新事务之前使用相同的TransactionalId的事务已经完成。如果没有提供TransactionalId，则生产者被限制为幂等传递。请注意，如果配置了TransactionalId，则必须启用enable.idempotence。  默认值为空，这意味着无法使用事务。** | **string**   | **null**                                                     | **non-empty string**   | **low**        |

## **kafka消费者详解**

### **消费者组**

**![-](assets\image-20210530224706747.png)**

- **消费者组（Consumer Group） ：指的就是由一个或多个消费者组成的群体**

- **一个发布在Topic上消息被分发给此消费者组中的一个消费者**

  - **所有的消费者都在一个组中，那么这就变成了queue模型**

  - **所有的消费者都在不同的组中，那么就完全变成了发布-订阅模型**

### **消息有序性**

**应用场景：**

- **即时消息中的单对单聊天和群聊，保证发送方消息发送顺序与接收方的顺序一致**

- **充值转账两个渠道在同一个时间进行余额变更，短信通知必须要有顺序**

**![image-20210530224903891](assets\image-20210530224903891.png)**

**topic分区中消息只能由消费者组中的唯一一个消费者处理，所以消息肯定是按照先后顺序进行处理的。但是它也仅仅是保证Topic的一个分区顺序处理，不能保证跨分区的消息先后处理顺序。 所以，如果你想要顺序的处理Topic的所有消息，那就只提供一个分区。**

### **提交和偏移量**

**kafka不会像其他JMS队列那样需要得到消费者的确认，消费者可以使用kafka来追踪消息在分区的位置（偏移量）**

**消费者会往一个叫做_consumer_offset的特殊主题发送消息，消息里包含了每个分区的偏移量。如果消费者发生崩溃或有新的消费者加入群组，就会触发再均衡**

**![image-20210530225021266](assets\image-20210530225021266.png)**

**正常的情况**

**![image-20210530224959350](assets\image-20210530224959350.png)**

**如果消费者2挂掉以后，会发生再均衡，消费者2负责的分区会被其他消费者进行消费**

**再均衡后不可避免会出现一些问题**

**问题一：**

**![image-20210530225215337](assets\image-20210530225215337.png)**

**如果提交偏移量小于客户端处理的最后一个消息的偏移量，那么处于两个偏移量之间的消息就会被重复处理。**



**问题二：**

**![image-20210530225239897](assets\image-20210530225239897.png)**

**如果提交的偏移量大于客户端的最后一个消息的偏移量，那么处于两个偏移量之间的消息将会丢失。**



**如果想要解决这些问题，还要知道目前kafka提交偏移量的方式：**

**提交偏移量的方式有两种，分别是自动提交偏移量和手动提交**

- **自动提交偏移量**

**当enable.auto.commit被设置为true，提交方式就是让消费者自动提交偏移量，每隔5秒消费者会自动把从poll()方法接收的最大偏移量提交上去**

- **手动提交 ，当enable.auto.commit被设置为false可以有以下三种提交方式**

  - **提交当前偏移量（同步提交）**

  - **异步提交**

  - **同步和异步组合提交**



**1.提交当前偏移量（同步提交）**

**把`enable.auto.commit`设置为false,让应用程序决定何时提交偏移量。使用commitSync()提交偏移量，commitSync()将会提交poll返回的最新的偏移量，所以在处理完所有记录后要确保调用了commitSync()方法。否则还是会有消息丢失的风险。**

**只要没有发生不可恢复的错误，commitSync()方法会一直尝试直至提交成功，如果提交失败也可以记录到错误日志里。**

```java
while (true){
    ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(1000));
    for (ConsumerRecord<String, String> record : records) {
        System.out.println(record.value());
        System.out.println(record.key());
        try {
            consumer.commitSync();//同步提交当前最新的偏移量
        }catch (CommitFailedException e){
            System.out.println("记录提交失败的异常："+e);
        }

    }
}
```

**2.异步提交**

**手动提交有一个缺点，那就是当发起提交调用时应用会阻塞。当然我们可以减少手动提交的频率，但这个会增加消息重复的概率（和自动提交一样）。另外一个解决办法是，使用异步提交的API。**

```java
while (true){
    ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(1000));
    for (ConsumerRecord<String, String> record : records) {
        System.out.println(record.value());
        System.out.println(record.key());
    }
    consumer.commitAsync(new OffsetCommitCallback() {
        @Override
        public void onComplete(Map<TopicPartition, OffsetAndMetadata> map, Exception e) {
            if(e!=null){
                System.out.println("记录错误的提交偏移量："+ map+",异常信息"+e);
            }
        }
    });
}
```

**3.同步和异步组合提交**

**异步提交也有个缺点，那就是如果服务器返回提交失败，异步提交不会进行重试。相比较起来，同步提交会进行重试直到成功或者最后抛出异常给应用。异步提交没有实现重试是因为，如果同时存在多个异步提交，进行重试可能会导致位移覆盖。**

**举个例子，假如我们发起了一个异步提交commitA，此时的提交位移为2000，随后又发起了一个异步提交commitB且位移为3000；commitA提交失败但commitB提交成功，此时commitA进行重试并成功的话，会将实际上将已经提交的位移从3000回滚到2000，导致消息重复消费。**

```java
try {
    while (true){
        ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(1000));
        for (ConsumerRecord<String, String> record : records) {
            System.out.println(record.value());
            System.out.println(record.key());
        }
        consumer.commitAsync();
    }
}catch (Exception e){+
    e.printStackTrace();
    System.out.println("记录错误信息："+e);
}finally {
    try {
        consumer.commitSync();
    }finally {
        consumer.close();
    }
}
```

### **消费者配置**

|                          **NAME**                          | **DESCRIPTION**                                              | **TYPE**     | **DEFAULT**                 | **VALID VALUES**             | **IMPORTANCE** |
| :--------------------------------------------------------: | ------------------------------------------------------------ | ------------ | --------------------------- | ---------------------------- | -------------- |
|                   **bootstrap.servers**                    | **host/port,用于和kafka集群建立初始化连接。因为这些服务器地址仅用于初始化连接，并通过现有配置的来发现全部的kafka集群成员（集群随时会变化），所以此列表不需要包含完整的集群地址（但尽量多配置几个，以防止配置的服务器宕机）。** | **list**     |                             |                              | **high**       |
|                    **key.deserializer**                    | **key的解析序列化接口实现类（Deserializer）。**              | **class**    |                             |                              | **high**       |
|                   **value.deserializer**                   | **value的解析序列化接口实现类（Deserializer）**              | **class**    |                             |                              | **high**       |
|                    **fetch.min.bytes**                     | **服务器哦拉取请求返回的最小数据量，如果数据不足，请求将等待数据积累。默认设置为1字节，表示只要单个字节的数据可用或者读取等待请求超时，就会应答读取请求。将此值设置的越大将导致服务器等待数据累积的越长，这可能以一些额外延迟为代价提高服务器吞吐量。** | **int**      | **1**                       | **[0,...]**                  | **high**       |
|                        **group.id**                        | **此消费者所属消费者组的唯一标识。如果消费者用于订阅或offset管理策略的组管理功能，则此属性是必须的。** | **string**   | **""**                      |                              | **high**       |
|                 **heartbeat.interval.ms**                  | **当使用Kafka的分组管理功能时，心跳到消费者协调器之间的预计时间。心跳用于确保消费者的会话保持活动状态，并当有新消费者加入或离开组时方便重新平衡。该值必须必比session.timeout.ms小，通常不高于1/3。它可以调整的更低，以控制正常重新平衡的预期时间。** | **int**      | **3000**                    |                              | **high**       |
|               **max.partition.fetch.bytes**                | **服务器将返回每个分区的最大数据量。如果拉取的第一个非空分区中第一个消息大于此限制，则仍然会返回消息，以确保消费者可以正常的工作。broker接受的最大消息大小通过message.max.bytes（broker config）或max.message.bytes (topic  config)定义。参阅fetch.max.bytes以限制消费者请求大小。** | **int**      | **1048576**                 | **[0,...]**                  | **high**       |
|                   **session.timeout.ms**                   | **用于发现消费者故障的超时时间。消费者周期性的发送心跳到broker，表示其还活着。如果会话超时期满之前没有收到心跳，那么broker将从分组中移除消费者，并启动重新平衡。请注意，该值必须在broker配置的group.min.session.timeout.ms和group.max.session.timeout.ms允许的范围内。** | **int**      | **10000**                   |                              | **high**       |
|                    **ssl.key.password**                    | **密钥存储文件中的私钥的密码。  客户端可选**                 | **password** | **null**                    |                              | **high**       |
|                 **ssl.keystore.location**                  | **密钥存储文件的位置，  这对于客户端是可选的，并且可以用于客户端的双向认证。** | **string**   | **null**                    |                              | **high**       |
|                 **ssl.keystore.password**                  | **密钥仓库文件的仓库密码。客户端可选，只有ssl.keystore.location配置了才需要。** | **password** | **null**                    |                              | **high**       |
|                **ssl.truststore.location**                 | **信任仓库文件的位置**                                       | **string**   | **null**                    |                              | **high**       |
|                **ssl.truststore.password**                 | **信任仓库文件的密码**                                       | **password** | **null**                    |                              | **high**       |
|                   **auto.offset.reset**                    | **当Kafka中没有初始offset或如果当前的offset不存在时（例如，该数据被删除了），该怎么办。** | **string**   | **latest**                  | **[latest, earliest, none]** | **medium**     |
|            **最早：自动将偏移重置为最早的偏移**            |                                                              |              |                             |                              |                |
|             **最新：自动将偏移重置为最新偏移**             |                                                              |              |                             |                              |                |
| **none：如果消费者组找到之前的offset，则向消费者抛出异常** |                                                              |              |                             |                              |                |
|                **其他：抛出异常给消费者。**                |                                                              |              |                             |                              |                |
|                **connections.max.idle.ms**                 | **指定在多少毫秒之后关闭闲置的连接**                         | **long**     | **540000**                  |                              | **medium**     |
|                   **enable.auto.commit**                   | **如果为true，消费者的offset将在后台周期性的提交**           | **boolean**  | **TRUE**                    |                              | **medium**     |
|                **exclude.internal.topics**                 | **内部topic的记录（如偏移量）是否应向消费者公开。如果设置为true，则从内部topic接受记录的唯一方法是订阅它。** | **boolean**  | **TRUE**                    |                              | **medium**     |
|                    **fetch.max.bytes**                     | **服务器为拉取请求返回的最大数据值。这不是绝对的最大值，如果在第一次非空分区拉取的第一条消息大于该值，该消息将仍然返回，以确保消费者继续工作。接收的最大消息大小通过message.max.bytes  (broker config) 或 max.message.bytes (topic config)定义。注意，消费者是并行执行多个提取的。** | **int**      | **52428800**                | **[0,...]**                  | **medium**     |
|                  **max.poll.interval.ms**                  | **使用消费者组管理时poll()调用之间的最大延迟。消费者在获取更多记录之前可以空闲的时间量的上限。如果此超时时间期满之前poll()没有调用，则消费者被视为失败，并且分组将重新平衡，以便将分区重新分配给别的成员。** | **int**      | **300000**                  | **[1,...]**                  | **medium**     |
|                    **max.poll.records**                    | **在单次调用poll()中返回的最大记录数。**                     | **int**      | **500**                     | **[1,...]**                  | **medium**     |
|             **partition.assignment.strategy**              | **当使用组管理时，客户端将使用分区分配策略的类名来分配消费者实例之间的分区所有权** | **list**     | **class  org.apache.kafka** |                              | **medium**     |
|                   **.clients.consumer**                    |                                                              |              |                             |                              |                |
|                     **.RangeAssignor**                     |                                                              |              |                             |                              |                |
|                  **receive.buffer.bytes**                  | **读取数据时使用的TCP接收缓冲区（SO_RCVBUF）的大小。  如果值为-1，则将使用OS默认值。** | **int**      | **65536**                   | **[-1,...]**                 | **medium**     |
|                   **request.timeout.ms**                   | **配置控制客户端等待请求响应的最长时间。  如果在超时之前未收到响应，客户端将在必要时重新发送请求，如果重试耗尽则客户端将重新发送请求。** | **int**      | **305000**                  | **[0,...]**                  | **medium**     |
|                    **sasl.jaas.config**                    | **JAAS配置文件中SASL连接登录上下文参数。  这里描述JAAS配置文件格式。 该值的格式为： '(=)*;'** | **password** | **null**                    |                              | **medium**     |
|               **sasl.kerberos.service.name**               | **Kafka运行Kerberos  principal名。可以在Kafka的JAAS配置文件或在Kafka的配置文件中定义。** | **string**   | **null**                    |                              | **medium**     |
|                     **sasl.mechanism**                     | **用于客户端连接的SASL机制。安全提供者可用的机制。GSSAPI是默认机制。** | **string**   | **GSSAPI**                  |                              | **medium**     |
|                   **security.protocol**                    | **用于与broker通讯的协议。  有效值为：PLAINTEXT，SSL，SASL_PLAINTEXT，SASL_SSL。** | **string**   | **PLAINTEXT**               |                              | **medium**     |
|                   **send.buffer.bytes**                    | **发送数据时要使用的TCP发送缓冲区（SO_SNDBUF）的大小。  如果值为-1，则将使用OS默认值。** | **int**      | **131072**                  | **[-1,...]**                 | **medium**     |
|                 **ssl.enabled.protocols**                  | **启用SSL连接的协议列表。**                                  | **list**     | **TLSv1.2,TLSv1.1,TLSv1**   |                              | **medium**     |
|                   **ssl.keystore.type**                    | **key仓库文件的文件格式，客户端可选。**                      | **string**   | **JKS**                     |                              | **medium**     |
|                      **ssl.protocol**                      | **用于生成SSLContext的SSL协议。  默认设置是TLS，这对大多数情况都是适用的。 最新的JVM中的允许值为TLS，TLSv1.1和TLSv1.2。  较旧的JVM可能支持SSL，SSLv2和SSLv3，但由于已知的安全漏洞，不建议使用SSL。** | **string**   | **TLS**                     |                              | **medium**     |
|                      **ssl.provider**                      | **用于SSL连接的安全提供程序的名称。  默认值是JVM的默认安全提供程序。** | **string**   | **null**                    |                              | **medium**     |
|                  **ssl.truststore.type**                   | **信任存储文件的文件格式。**                                 | **string**   | **JKS**                     |                              | **medium**     |
|                **auto.commit.interval.ms**                 | **如果enable.auto.commit设置为true，则消费者偏移量自动提交给Kafka的频率（以毫秒为单位）。** | **int**      | **5000**                    | **[0,...]**                  | **low**        |
|                       **check.crcs**                       | **自动检查CRC32记录的消耗。  这样可以确保消息发生时不会在线或磁盘损坏。 此检查增加了一些开销，因此在寻求极致性能的情况下可能会被禁用。** | **boolean**  | **TRUE**                    |                              | **low**        |
|                       **client.id**                        | **在发出请求时传递给服务器的id字符串。  这样做的目的是通过允许将逻辑应用程序名称包含在服务器端请求日志记录中，来跟踪ip/port的请求源。** | **string**   | **""**                      |                              | **low**        |
|                   **fetch.max.wait.ms**                    | **如果没有足够的数据满足fetch.min.bytes，服务器将在接收到提取请求之前阻止的最大时间。** | **int**      | **500**                     | **[0,...]**                  | **low**        |
|                  **interceptor.classes**                   | **用作拦截器的类的列表。  你可实现ConsumerInterceptor接口以允许拦截（也可能变化）消费者接收的记录。 默认情况下，没有拦截器。** | **list**     | **null**                    |                              | **low**        |
|                  **metadata.max.age.ms**                   | **在一定时间段之后（以毫秒为单位的），强制更新元数据，即使没有任何分区领导变化，任何新的broker或分区。** | **long**     | **300000**                  | **[0,...]**                  | **low**        |
|                    **metric.reporters**                    | **用作度量记录员类的列表。实现MetricReporter接口以允许插入通知新的度量创建的类。JmxReporter始终包含在注册JMX统计信息中。** | **list**     | **""**                      |                              | **low**        |
|                  **metrics.num.samples**                   | **保持的样本数以计算度量。**                                 | **int**      | **2**                       | **[1,...]**                  | **low**        |
|                **metrics.recording.level**                 | **最高的记录级别。**                                         | **string**   | **INFO**                    | **[INFO,  DEBUG]**           | **low**        |
|                **metrics.sample.window.ms**                | **The  window of time a metrics sample is computed over.**   | **long**     | **30000**                   | **[0,...]**                  | **low**        |
|                  **reconnect.backoff.ms**                  | **尝试重新连接指定主机之前等待的时间，避免频繁的连接主机，这种机制适用于消费者向broker发送的所有请求。** | **long**     | **50**                      | **[0,...]**                  | **low**        |
|                    **retry.backoff.ms**                    | **尝试重新发送失败的请求到指定topic分区之前的等待时间。避免在某些故障情况下，频繁的重复发送。** | **long**     | **100**                     | **[0,...]**                  | **low**        |
|            **sasl.kerberos.kinit.cmd Kerberos**            | **kinit命令路径。**                                          | **string**   | **/usr/bin/kinit**          |                              | **low**        |
|         **sasl.kerberos.min.time.before.relogin**          | **尝试/恢复之间的登录线程的休眠时间。**                      | **long**     | **60000**                   |                              | **low**        |
|           **sasl.kerberos.ticket.renew.jitter**            | **添加到更新时间的随机抖动百分比。**                         | **double**   | **0.05**                    |                              | **low**        |
|        **sasl.kerberos.ticket.renew.window.factor**        | **登录线程将休眠，直到从上次刷新到ticket的指定的时间窗口因子到期，此时将尝试续订ticket。** | **double**   | **0.8**                     |                              | **low**        |
|                   **ssl.cipher.suites**                    | **密码套件列表，用于TLS或SSL网络协议的安全设置，认证，加密，MAC和密钥交换算法的明明组合。默认情况下，支持所有可用的密码套件。** | **list**     | **null**                    |                              | **low**        |
|         **ssl.endpoint.identification.algorithm**          | **使用服务器证书验证服务器主机名的端点识别算法。**           | **string**   | **null**                    |                              | **low**        |
|                **ssl.keymanager.algorithm**                | **密钥管理器工厂用于SSL连接的算法。  默认值是为Java虚拟机配置的密钥管理器工厂算法。** | **string**   | **SunX509**                 |                              | **low**        |
|            **ssl.secure.random.implementation**            | **用于SSL加密操作的SecureRandom  PRNG实现。**                | **string**   | **null**                    |                              | **low**        |
|               **ssl.trustmanager.algorithm**               | **信任管理器工厂用于SSL连接的算法。  默认值是为Java虚拟机配置的信任管理器工厂算法。** | **string**   | **PKIX**                    |                              | **low**        |



## **springboot集成kafka**

### **入门**

**1.导入spring-kafka依赖信息**

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <!-- kafkfa -->
    <dependency>
        <groupId>org.springframework.kafka</groupId>
        <artifactId>spring-kafka</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.apache.kafka</groupId>
                <artifactId>kafka-clients</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <groupId>org.apache.kafka</groupId>
        <artifactId>kafka-clients</artifactId>
    </dependency>
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
    </dependency>
</dependencies>
```

**2.在resources下创建文件application.yml**

```yaml
server:
  port: 9991
spring:
  application:
    name: kafka-demo
  kafka:
    bootstrap-servers: 192.168.200.130:9092
    producer:
      retries: 10
      key-serializer: org.apache.kafka.common.serialization.StringSerializer
      value-serializer: org.apache.kafka.common.serialization.StringSerializer
    consumer:
      group-id: ${spring.application.name}-test
      key-deserializer: org.apache.kafka.common.serialization.StringDeserializer
      value-deserializer: org.apache.kafka.common.serialization.StringDeserializer
```

**3.消息生产者**

```java
package com.heima.kafka.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @Autowired
    private KafkaTemplate<String,String> kafkaTemplate;

    @GetMapping("/hello")
    public String hello(){
        kafkaTemplate.send("itcast-topic","黑马程序员");
        return "ok";
    }
}
```

**4.消息消费者**

```java
package com.heima.kafka.listener;

import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.stereotype.Component;
import org.springframework.util.StringUtils;

@Component
public class HelloListener {

    @KafkaListener(topics = "itcast-topic")
    public void onMessage(String message){
        if(!StringUtils.isEmpty(message)){
            System.out.println(message);
        }

    }
}
```

### **传递消息为对象**

**目前springboot整合后的kafka，因为序列化器是StringSerializer，这个时候如果需要传递对象可以有两种方式**

**方式一：可以自定义序列化器，对象类型众多，这种方式通用性不强，本章节不介绍**

**方式二：可以把要传递的对象进行转json字符串，接收消息后再转为对象即可，本项目采用这种方式**

- **发送消息**

```java
@GetMapping("/hello")
public String hello(){
    User user = new User();
    user.setUsername("xiaowang");
    user.setAge(18);

    kafkaTemplate.send("user-topic", JSON.toJSONString(user));

    return "ok";
}
```

- **接收消息**

```java
package com.heima.kafka.listener;

import com.alibaba.fastjson.JSON;
import com.heima.kafka.pojo.User;
import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.stereotype.Component;
import org.springframework.util.StringUtils;

@Component
public class HelloListener {

    @KafkaListener(topics = "user-topic")
    public void onMessage(String message){
        if(!StringUtils.isEmpty(message)){
            User user = JSON.parseObject(message, User.class);
            System.out.println(user);
        }

    }
}
```

## **实时流式计算**

### **概念**

**一般流式计算会与批量计算相比较。在流式计算模型中，输入是持续的，可以认为在时间上是无界的，也就意味着，永远拿不到全量数据去做计算。同时，计算结果是持续输出的，也即计算结果在时间上也是无界的。流式计算一般对实时性要求较高，同时一般是先定义目标计算，然后数据到来之后将计算逻辑应用于数据。同时为了提高计算效率，往往尽可能采用增量计算代替全量计算。**

**![image-20210731090637590](assets\image-20210731090637590.png)**

**流式计算就相当于上图的右侧扶梯，是可以源源不断的产生数据，源源不断的接收数据，没有边界。**

### **应用场景**

- **日志分析**

  **网站的用户访问日志进行实时的分析，计算访问量，用户画像，留存率等等，实时的进行数据分析，帮助企业进行决策**

- **大屏看板统计**

  **可以实时的查看网站注册数量，订单数量，购买数量，金额等。**

- **公交实时数据**

  **可以随时更新公交车方位，计算多久到达站牌等**

- **实时文章分值计算**

  **头条类文章的分值计算，通过用户的行为实时文章的分值，分值越高就越被推荐。**

### **技术方案选型**

- **Hadoop** 

  **![image-20210731090700382](assets\image-20210731090700382.png)**

- **Apche Storm**

  **Storm 是一个分布式实时大数据处理系统，可以帮助我们方便地处理海量数据，具有高可靠、高容错、高扩展的特点。是流式框架，有很高的数据吞吐能力。**

- **Kafka Stream** 

  **可以轻松地将其嵌入任何Java应用程序中，并与用户为其流应用程序所拥有的任何现有打包，部署和操作工具集成。**

## **Kafka Stream** 

### **概述**

**Kafka Stream是Apache Kafka从0.10版本引入的一个新Feature。它是提供了对存储于Kafka内的数据进行流式处理和分析的功能。**

**Kafka Stream的特点如下：**

- **Kafka Stream提供了一个非常简单而轻量的Library，它可以非常方便地嵌入任意Java应用中，也可以任意方式打包和部署**
- **除了Kafka外，无任何外部依赖**
- **充分利用Kafka分区机制实现水平扩展和顺序性保证**
- **通过可容错的state store实现高效的状态操作（如windowed join和aggregation）**
- **支持正好一次处理语义**
- **提供记录级的处理能力，从而实现毫秒级的低延迟**
- **支持基于事件时间的窗口操作，并且可处理晚到的数据（late arrival of records）**
- **同时提供底层的处理原语Processor（类似于Storm的spout和bolt），以及高层抽象的DSL（类似于Spark的map/group/reduce）**



**![image-20210730201706437](assets\image-20210730201706437.png)**



### **Kafka Streams的关键概念**

- **源处理器（Source Processor）：源处理器是一个没有任何上游处理器的特殊类型的流处理器。它从一个或多个kafka主题生成输入流。通过消费这些主题的消息并将它们转发到下游处理器。**
- **Sink处理器：sink处理器是一个没有下游流处理器的特殊类型的流处理器。它接收上游流处理器的消息发送到一个指定的Kafka主题。**

**![image-20210731090727323](assets\image-20210731090727323.png)**



### **KStream**

**（1）数据结构类似于map,如下图，key-value键值对**

**![image-20210731090746415](assets\image-20210731090746415.png)**

**（2）KStream**

**![image-20210730201817959](assets\image-20210730201817959.png)**

**KStream数据流（data stream），即是一段顺序的，可以无限长，不断更新的数据集。**
**数据流中比较常记录的是事件，这些事件可以是一次鼠标点击（click），一次交易，或是传感器记录的位置数据。**

**KStream负责抽象的，就是数据流。与Kafka自身topic中的数据一样，类似日志，每一次操作都是向其中插入（insert）新数据。**

**为了说明这一点，让我们想象一下以下两个数据记录正在发送到流中：**

**（“ alice”，1）->（“” alice“，3）**

**如果您的流处理应用是要总结每个用户的价值，它将返回`4`了`alice`。为什么？因为第二条数据记录将不被视为先前记录的更新。（insert）新数据**

### **Kafka Stream入门案例编写**

**（1）需求分析，求单词个数（word count）**

**![image-20210730201911566](assets\image-20210730201911566.png)**



**（2）引入依赖**

**在之前的kafka-demo工程的pom文件中引入**

```xml
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-streams</artifactId>
    <exclusions>
        <exclusion>
            <artifactId>connect-json</artifactId>
            <groupId>org.apache.kafka</groupId>
        </exclusion>
        <exclusion>
            <groupId>org.apache.kafka</groupId>
            <artifactId>kafka-clients</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

**(3)创建原生的kafka staream入门案例**

```java
package com.heima.kafka.sample;

import org.apache.kafka.common.serialization.Serdes;
import org.apache.kafka.streams.KafkaStreams;
import org.apache.kafka.streams.KeyValue;
import org.apache.kafka.streams.StreamsBuilder;
import org.apache.kafka.streams.StreamsConfig;
import org.apache.kafka.streams.kstream.KStream;
import org.apache.kafka.streams.kstream.TimeWindows;
import org.apache.kafka.streams.kstream.ValueMapper;

import java.time.Duration;
import java.util.Arrays;
import java.util.Properties;

/**
 * 流式处理
 */
public class KafkaStreamQuickStart {

    public static void main(String[] args) {

        //kafka的配置信心
        Properties prop = new Properties();
        prop.put(StreamsConfig.BOOTSTRAP_SERVERS_CONFIG,"192.168.200.130:9092");
        prop.put(StreamsConfig.DEFAULT_KEY_SERDE_CLASS_CONFIG, Serdes.String().getClass());
        prop.put(StreamsConfig.DEFAULT_VALUE_SERDE_CLASS_CONFIG, Serdes.String().getClass());
        prop.put(StreamsConfig.APPLICATION_ID_CONFIG,"streams-quickstart");

        //stream 构建器
        StreamsBuilder streamsBuilder = new StreamsBuilder();

        //流式计算
        streamProcessor(streamsBuilder);


        //创建kafkaStream对象
        KafkaStreams kafkaStreams = new KafkaStreams(streamsBuilder.build(),prop);
        //开启流式计算
        kafkaStreams.start();
    }

    /**
     * 流式计算
     * 消息的内容：hello kafka  hello itcast
     * @param streamsBuilder
     */
    private static void streamProcessor(StreamsBuilder streamsBuilder) {
        //创建kstream对象，同时指定从那个topic中接收消息
        KStream<String, String> stream = streamsBuilder.stream("itcast-topic-input");
        /**
         * 处理消息的value
         */
        stream.flatMapValues(new ValueMapper<String, Iterable<String>>() {
            @Override
            public Iterable<String> apply(String value) {
                return Arrays.asList(value.split(" "));
            }
        })
                //按照value进行聚合处理
                .groupBy((key,value)->value)
                //时间窗口
                .windowedBy(TimeWindows.of(Duration.ofSeconds(10)))
                //统计单词的个数
                .count()
                //转换为kStream
                .toStream()
                .map((key,value)->{
                    System.out.println("key:"+key+",vlaue:"+value);
                    return new KeyValue<>(key.key().toString(),value.toString());
                })
                //发送消息
                .to("itcast-topic-out");
    }
}
```

### **入门案例详解**

#### **原始输入（假设来自 Kafka topic 的句子）**

```
text复制编辑"hello kafka kafka stream"
"hello stream kafka"
```

**Kafka Streams 中我们获取的 `stream` 是：**

```
java


复制编辑
KStream<String, String> stream = builder.stream("itcast-topic-in");
```

#### **步骤 1：`flatMapValues`**

```
java


复制编辑
stream.flatMapValues(value -> Arrays.asList(value.split(" ")))
```

**将句子拆分为单词，每个词作为一个新的记录（flatMap 会“展开”）**

**输入记录：**

```
csharp复制编辑(null, "hello kafka kafka stream")
(null, "hello stream kafka")
```

**输出记录：**

```
csharp复制编辑(null, "hello")
(null, "kafka")
(null, "kafka")
(null, "stream")
(null, "hello")
(null, "stream")
(null, "kafka")
```

------

#### **步骤 2：`.groupBy((key, value) -> value)`**

```
java


复制编辑
.groupBy((key, value) -> value)
```

**按单词内容分组，相同单词归为一组（新 key 是单词）**

**输入：**

```
csharp复制编辑(null, "hello")
(null, "kafka")
(null, "kafka")
(null, "stream")
(null, "hello")
(null, "stream")
(null, "kafka")
```

**分组后的记录（简化为分组结构）：**

```
rust复制编辑"hello" -> ["hello", "hello"]
"kafka" -> ["kafka", "kafka", "kafka"]
"stream" -> ["stream", "stream"]
```

------

#### **步骤 3：`.windowedBy(TimeWindows.of(Duration.ofSeconds(10)))`**

```
java


复制编辑
.windowedBy(TimeWindows.of(Duration.ofSeconds(10)))
```

**为每个单词分组添加一个 10 秒的时间窗口**

**假设上面所有记录都落在时间窗口：[12:00:00 - 12:00:10]**

**窗口后的结构（简化）：**

```
scss复制编辑Windowed("hello", [12:00:00 - 12:00:10]) -> ["hello", "hello"]
Windowed("kafka", [12:00:00 - 12:00:10]) -> ["kafka", "kafka", "kafka"]
Windowed("stream", [12:00:00 - 12:00:10]) -> ["stream", "stream"]
```

------

#### **步骤 4：`.count()`**

```
java


复制编辑
.count()
```

**统计每个单词在每个时间窗口内的出现次数**

**输出（KTable<Windowed<String>, Long>）：**

```
rust复制编辑Windowed("hello", [12:00:00 - 12:00:10]) -> 2
Windowed("kafka", [12:00:00 - 12:00:10]) -> 3
Windowed("stream", [12:00:00 - 12:00:10]) -> 2
```

------

#### **步骤 5：`.toStream().map(...)`**

```
java复制编辑.toStream().map((key, value) -> {
    System.out.println("key:" + key + ",vlaue:" + value);
    return new KeyValue<>(key.key().toString(), value.toString());
})
```

- **`key.key()` 获取窗口中原始 key（单词）**
- **`value` 是计数结果（Long）**
- **打印输出 + 转换为字符串**

**输出记录（KStream<String, String>）：**

```
rust复制编辑"hello" -> "2"
"kafka" -> "3"
"stream" -> "2"
```

**打印内容示例：**

```
graphql复制编辑key:hello@12:00:00/12:00:10,vlaue:2
key:kafka@12:00:00/12:00:10,vlaue:3
key:stream@12:00:00/12:00:10,vlaue:2
```

------

#### **步骤 6：`.to("itcast-topic-out")`**

```
java


复制编辑
.to("itcast-topic-out");
```

**将最终结果发送到 Kafka 的 `itcast-topic-out` 主题中**

**Kafka 中可见的消息（主题内容）：**

```
rust复制编辑"hello" -> "2"
"kafka" -> "3"
"stream" -> "2"
```

------

#### **全流程回顾图示**

```
vbnet复制编辑原始 Kafka 输入（KStream<String, String>）
    ↓
flatMapValues（按空格分词）
    ↓
groupBy（按词分组）
    ↓
windowedBy（加上时间窗口）
    ↓
count（统计每词在窗口中出现次数）
    ↓
toStream + map（提取key + 转字符串）
    ↓
to（写入 Kafka 输出 topic）
```

### **SpringBoot集成Kafka Stream**

**（1）自定配置参数**

```java
package com.heima.kafka.config;

import lombok.Getter;
import lombok.Setter;
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.common.serialization.Serdes;
import org.apache.kafka.streams.StreamsConfig;
import org.apache.kafka.streams.Topology;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.kafka.annotation.EnableKafkaStreams;
import org.springframework.kafka.annotation.KafkaStreamsDefaultConfiguration;
import org.springframework.kafka.config.KafkaStreamsConfiguration;

import java.util.HashMap;
import java.util.Map;

/**
 * 通过重新注册KafkaStreamsConfiguration对象，设置自定配置参数
 */

@Setter
@Getter
@Configuration
@EnableKafkaStreams
@ConfigurationProperties(prefix="kafka")
public class KafkaStreamConfig {
    private static final int MAX_MESSAGE_SIZE = 16* 1024 * 1024;
    private String hosts;
    private String group;
    @Bean(name = KafkaStreamsDefaultConfiguration.DEFAULT_STREAMS_CONFIG_BEAN_NAME)
    public KafkaStreamsConfiguration defaultKafkaStreamsConfig() {
        Map<String, Object> props = new HashMap<>();
        props.put(StreamsConfig.BOOTSTRAP_SERVERS_CONFIG, hosts);
        props.put(StreamsConfig.APPLICATION_ID_CONFIG, this.getGroup()+"_stream_aid");
        props.put(StreamsConfig.CLIENT_ID_CONFIG, this.getGroup()+"_stream_cid");
        props.put(StreamsConfig.RETRIES_CONFIG, 10);
        props.put(StreamsConfig.DEFAULT_KEY_SERDE_CLASS_CONFIG, Serdes.String().getClass());
        props.put(StreamsConfig.DEFAULT_VALUE_SERDE_CLASS_CONFIG, Serdes.String().getClass());
        return new KafkaStreamsConfiguration(props);
    }
}
```

**修改application.yml文件，在最下方添加自定义配置**

```yaml
kafka:
  hosts: 192.168.200.130:9092
  group: ${spring.application.name}
```

**(2)新增配置类，创建KStream对象，进行聚合**

```java
package com.heima.kafka.stream;

import lombok.extern.slf4j.Slf4j;
import org.apache.kafka.streams.KeyValue;
import org.apache.kafka.streams.StreamsBuilder;
import org.apache.kafka.streams.kstream.KStream;
import org.apache.kafka.streams.kstream.TimeWindows;
import org.apache.kafka.streams.kstream.ValueMapper;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import java.time.Duration;
import java.util.Arrays;

@Configuration
@Slf4j
public class KafkaStreamHelloListener {

    @Bean
    public KStream<String,String> kStream(StreamsBuilder streamsBuilder){
        //创建kstream对象，同时指定从那个topic中接收消息
        KStream<String, String> stream = streamsBuilder.stream("itcast-topic-input");
        stream.flatMapValues(new ValueMapper<String, Iterable<String>>() {
            @Override
            public Iterable<String> apply(String value) {
                return Arrays.asList(value.split(" "));
            }
        })
                //根据value进行聚合分组
                .groupBy((key,value)->value)
                //聚合计算时间间隔
                .windowedBy(TimeWindows.of(Duration.ofSeconds(10)))
                //求单词的个数
                .count()
                .toStream()
                //处理后的结果转换为string字符串
                .map((key,value)->{
                    System.out.println("key:"+key+",value:"+value);
                    return new KeyValue<>(key.key().toString(),value.toString());
                })
                //发送消息
                .to("itcast-topic-out");
        return stream;
    }
}
```

**测试：**

​	**启动微服务，正常发送消息，可以正常接收到消息**

### **聚合操作**

**聚合操作就是对key进行的分组操作，比如对key进行出现次数的计数**

#### **聚合操作在 Kafka Streams 中的典型形式**

**Kafka Streams 提供了几种聚合相关的方法：**

| **方法名**           | **说明**                                     |
| -------------------- | -------------------------------------------- |
| **`count()`**        | **统计每个 key 出现的次数**                  |
| **`reduce(...)`**    | **用自定义函数两两合并 value**               |
| **`aggregate(...)`** | **最通用的聚合函数，提供初始化值和聚合函数** |



#### **使用聚合前的准备**

**聚合操作通常在 `KGroupedStream` 或 `KGroupedTable` 上进行，所以你必须先用 `groupBy` 或 `groupByKey` 对流做分组。**

```
java


复制编辑
KGroupedStream<String, String> grouped = stream.groupBy((key, value) -> value);
```

**然后才能：**

```
java复制编辑grouped.count();       // 计数
grouped.reduce(...);   // 自定义合并逻辑
grouped.aggregate(...);// 最强大，初始化 + 合并
```

#### **下面分别讲讲三种聚合操作**

##### **1. `.count()`**

**用途：统计某个 key 出现的次数。**

```
java


复制编辑
KTable<String, Long> wordCount = grouped.count();
```

**输入：**

```
rust复制编辑"a" -> "apple"
"b" -> "banana"
"c" -> "apple"
```

**输出：**

```
rust复制编辑"apple" -> 2
"banana" -> 1
```

**count 是最简单的聚合：每遇到一个 key，就 `+1`。**

##### **2. `.reduce(...)`**

**用途：自定义将多个值合并为一个（比如累加、取最大值等）。**

```
java


复制编辑
KTable<String, String> reduced = grouped.reduce((v1, v2) -> v1 + "," + v2);
```

**输入：**

```
rust复制编辑"a" -> "1"
"a" -> "2"
"a" -> "3"
```

**输出：**

```
rust


复制编辑
"a" -> "1,2,3"
```

**注意：**

- **reduce 不能设置初始化值；**
- **第一次来的是初始值，之后每来一个就和当前值合并。**

##### **3. `.aggregate(...)`**

**用途：功能最强大，可以指定初始值 + 合并函数 + 状态序列化类型。**

```
java复制编辑KTable<String, List<String>> aggregated = grouped.aggregate(
    () -> new ArrayList<>(),                               // 初始化
    (key, value, aggregate) -> {
        aggregate.add(value);
        return aggregate;
    },
    Materialized.with(Serdes.String(), yourListSerde)      // 指定存储格式
);
```

**输入：**

```
rust复制编辑"user1" -> "click"
"user1" -> "view"
"user1" -> "like"
```

**输出：**

```
rust


复制编辑
"user1" -> ["click", "view", "like"]
```

**你可以做任意复杂的聚合逻辑，比如：**

- **累加金额**
- **保存最新的 N 条记录**
- **合并对象字段**
- **自定义数据结构统计**

**详解**

```
.aggregate(new Initializer<Object>() {
    @Override
    public List<String> apply() {
        return new ArrayList<>();
    }
}, new Aggregator<String, String, List<String>>() {
    @Override
    public Object apply(String key, String value, List<String> aggValue) {
        return null;
    }
})
```

**第一个参数用于初始化聚合后的value的值以及类型，这里我们假定类型是List,初始化为一个控制**

**第二个参数主要负责具体的代码逻辑，其中的apply方法的参数分别对应原本的key,value，以及刚刚初始化的新value**

#### **聚合背后的底层机制**

1. **状态存储（State Store）：**
   - **Kafka Streams 会为每个聚合操作自动创建一个本地状态存储（RocksDB）；**
   - **聚合值保存在 state store 中，可以容错和恢复。**
2. **changelog topic：**
   - **状态变更会写入 Kafka topic（changelog），保证 fault-tolerant；**
   - **应用重启时可以从 changelog topic 恢复聚合状态。**
3. **Window 聚合（窗口化聚合）：**
   - **可以结合 `.windowedBy()` 进行时间窗口聚合；**
   - **实现“每10秒内统计一次”、“过去1小时求和”等需求。**

#### **状态存储（State Store）**

##### **定义**

> **状态存储（State Store） 是 Kafka Streams 中用于保存中间计算状态的一种机制，它可以存储：**
>
> - **窗口聚合的结果（如：过去10秒的计数）**
> - **当前某个 key 的最新值（如：某个用户的余额）**
> - **自定义聚合过程的中间变量（如：List、Map、Set）**

**例子 1：统计过去10秒内每个单词出现次数**

```
java复制编辑windowedBy(TimeWindows.of(Duration.ofSeconds(10)))
    .count()
```

**这时候，每个 word 和它对应的 10 秒时间窗口内的计数，需要被保存在某个地方——Kafka Streams 会使用 WindowStore 保存这个状态。**

------

**例子 2：按用户累加金额**

```
java复制编辑.groupByKey()
.aggregate(
    () -> 0L,
    (key, value, agg) -> agg + value
)
```

**这里就用到了一个 KeyValueStore 来保存每个用户的当前累计金额。**

##### **状态存储类型**

| **类型**            | **用途**                                                |
| ------------------- | ------------------------------------------------------- |
| **`KeyValueStore`** | **保存 key 的当前值（无时间维度）**                     |
| **`WindowStore`**   | **保存 key 的每个时间窗口的值，在有windowedBy时会使用** |
| **`SessionStore`**  | **保存 key 的“会话”段，自动合并**                       |

##### **状态是如何恢复的？**

**Kafka Streams 在使用状态存储时，自动将状态变更同步到 Kafka 的 changelog topic 中：**

- **节点崩溃后重启时，会从 changelog 中恢复状态；**
- **这就是所谓的 持久化状态（fault-tolerant state）。**

#### **Materialized.as(...) 方法作用详解**

**基本形式：**

```
java


复制编辑
Materialized.as("my-state-store-name")
```

**作用：**

1. **指定状态存储的名字（用于调试、交互式查询、状态恢复）；**
2. **Kafka Streams 会自动：**
   - **创建本地 RocksDB 状态存储**
   - **创建对应 changelog topic，如：`<app-id>-my-state-store-name-changelog`**
3. **如果不使用 `.as(...)`，Kafka Streams 会默认生成一个随机状态存储名。**

**使用例子：**

```
java复制编辑KTable<Windowed<String>, Long> counts = stream
    .groupByKey()
    .windowedBy(TimeWindows.of(Duration.ofSeconds(10)))
    .count(Materialized.as("word-count-window-store"));
```

**这样就会：**

- **在本地创建一个叫 `"word-count-window-store"` 的 `WindowStore`**

- **自动创建 changelog topic：**

  ```
  arduino
  
  
  复制编辑
  <application-id>-word-count-window-store-changelog
  ```

**总结一下**

| **内容**                    | **作用说明**                                                 |
| --------------------------- | ------------------------------------------------------------ |
| **状态存储（State Store）** | **保存中间计算状态，实现窗口、聚合、去重、会话、交互式查询等核心能力** |
| **`.as("name")`**           | **显式命名状态存储，方便恢复、调试、查询**                   |
| **状态存储位置**            | **本地 RocksDB（或内存），并自动持久化到 Kafka changelog topic** |
| **常用状态存储类型**        | **`KeyValueStore`、`WindowStore`、`SessionStore`**           |

#### **聚合适合解决什么问题？**

- **实时单词统计（WordCount）**
- **实时订单金额总和**
- **实时 UV/活跃用户统计**
- **每类产品销量 TopN（配合 reduce / aggregate）**
- **最近 5 条用户行为记录（aggregate List）**

#### **总结**

| **聚合操作**  | **是否需要初始化** | **能否自定义逻辑** | **是否保留状态** | **常用场景**             |
| ------------- | ------------------ | ------------------ | ---------------- | ------------------------ |
| **count**     | **❌**              | **❌**              | **✅**            | **计数**                 |
| **reduce**    | **❌**              | **✅**              | **✅**            | **累加、最值、拼接等**   |
| **aggregate** | **✅**              | **✅**              | **✅**            | **高级统计、自定义逻辑** |
