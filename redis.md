# Redis

## 启动服务

**启动Redis服务：`redis-server.exe redis.windows.conf`**

**注意：启动服务后，命令行窗口不要关，关掉就会停止服务**

**打开Redis客户端：`redis-cli.exe`**

**完整命令：`redis-cli.exe -h ip -p port`**

**注意：这里需要另开一个窗口，补充的命令可以省略，ip位置换成目标ip,port换成目标端口**

## docker部署

```shell
docker run -d \
  --name redis \
  --restart=always \
  -p 6379:6379 \
  -v /opt/redis/data:/data \
  redis \
  --requirepass "leadnews" \
  --save 60 1 \
  --appendonly yes \
  --appendfsync everysec \
  --dir /data

```

## 常用数据类型

**Redis存储的是key-value结构的数据，其中key是字符串类型，value有中常用的数据类型，分别是字符串string，哈希hash，列表list，集合set，有序集合sorted set/zset**

![](D:/StudyNote/assets/Redis.png)

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

## redis实现延迟任务

### **实现思路**

![image-20210513150440342](assets\image-20210513150440342.png)

**zset数据类型的去重有序（分数排序）特点进行延迟。例如：时间戳作为score进行排序**

![image-20210513150352211](assets\image-20210513150352211.png)

**问题思路**

**1.为什么任务需要存储在数据库中？**

**延迟任务是一个通用的服务，任何需要延迟得任务都可以调用该服务，需要考虑数据持久化的问题，存储数据库中是一种数据安全的考虑。**

**2.为什么redis中使用两种数据类型，list和zset？**

**效率问题，算法的时间复杂度**

**3.在添加zset数据的时候，为什么不需要预加载？**

**任务模块是一个通用的模块，项目中任何需要延迟队列的地方，都可以调用这个接口，要考虑到数据量的问题，如果数据量特别大，为了防止阻塞，只需要把未来几分钟要执行的数据存入缓存即可。**

### 未来数据定时刷新

#### reids key值匹配

**方案1：keys 模糊匹配**

**keys的模糊匹配功能很方便也很强大，但是在生产环境需要慎用！开发中使用keys的模糊匹配却发现redis的CPU使用率极高，所以公司的redis生产环境将keys命令禁用了！redis是单线程，会被堵塞**

![image-20210515162329679](assets\image-20210515162329679.png)

**方案2：scan** 

**SCAN 命令是一个基于游标的迭代器，SCAN命令每次被调用之后， 都会向用户返回一个新的游标， 用户在下次迭代时需要使用这个新游标作为SCAN命令的游标参数， 以此来延续之前的迭代过程。**

![image-20210515162419548](assets\image-20210515162419548.png)

**代码案例：**

```java
@Test
public void testKeys(){
    Set<String> keys = cacheService.keys("future_*");
    System.out.println(keys);

    Set<String> scan = cacheService.scan("future_*");
    System.out.println(scan);
}
```

#### reids管道

**普通redis客户端和服务器交互模式**

![image-20210515162537224](assets\image-20210515162537224.png)

**Pipeline请求模型**

![image-20210515162604410](assets\image-20210515162604410.png)

**官方测试结果数据对比**

![image-20210515162621928](assets\image-20210515162621928.png)

测试案例对比：

```java
//耗时6151
@Test
public  void testPiple1(){
    long start =System.currentTimeMillis();
    for (int i = 0; i <10000 ; i++) {
        Task task = new Task();
        task.setTaskType(1001);
        task.setPriority(1);
        task.setExecuteTime(new Date().getTime());
        cacheService.lLeftPush("1001_1", JSON.toJSONString(task));
    }
    System.out.println("耗时"+(System.currentTimeMillis()- start));
}


@Test
public void testPiple2(){
    long start  = System.currentTimeMillis();
    //使用管道技术
    List<Object> objectList = cacheService.getstringRedisTemplate().executePipelined(new RedisCallback<Object>() {
        @Nullable
        @Override
        public Object doInRedis(RedisConnection redisConnection) throws DataAccessException {
            for (int i = 0; i <10000 ; i++) {
                Task task = new Task();
                task.setTaskType(1001);
                task.setPriority(1);
                task.setExecuteTime(new Date().getTime());
                redisConnection.lPush("1001_1".getBytes(), JSON.toJSONString(task).getBytes());
            }
            return null;
        }
    });
    System.out.println("使用管道技术执行10000次自增操作共耗时:"+(System.currentTimeMillis()-start)+"毫秒");
}
```

### 分布式锁

**分布式锁：控制分布式系统有序的去对共享资源进行操作，通过互斥来保证数据的一致性。**

**解决方案：**

![image-20210516112457413](assets\image-20210516112457413.png)



### redis分布式锁

**sexnx （SET if Not eXists） 命令在指定的 key 不存在时，为 key 设置指定的值。**

![image-20210516112612399](assets\image-20210516112612399.png)

**这种加锁的思路是，如果 key 不存在则为 key 设置 value，如果 key 已存在则 SETNX 命令不做任何操作**

- **客户端A请求服务器设置key的值，如果设置成功就表示加锁成功**
- **客户端B也去请求服务器设置key的值，如果返回失败，那么就代表加锁失败**
- **客户端A执行代码完成，删除锁**
- **客户端B在等待一段时间后再去请求设置key的值，设置成功**
- **客户端B执行代码完成，删除锁**

**在工具类CacheService中添加方法**

```java
/**
 * 加锁
 *
 * @param name
 * @param expire
 * @return
 */
public String tryLock(String name, long expire) {
    name = name + "_lock";
    String token = UUID.randomUUID().toString();
    RedisConnectionFactory factory = stringRedisTemplate.getConnectionFactory();
    RedisConnection conn = factory.getConnection();
    try {

        //参考redis命令：
        //set key value [EX seconds] [PX milliseconds] [NX|XX]
        Boolean result = conn.set(
                name.getBytes(),
                token.getBytes(),
                Expiration.from(expire, TimeUnit.MILLISECONDS),
                RedisStringCommands.SetOption.SET_IF_ABSENT //NX
        );
        if (result != null && result)
            return token;
    } finally {
        RedisConnectionUtils.releaseConnection(conn, factory,false);
    }
    return null;
}
```

**修改未来数据定时刷新的方法，如下：**

```java
/**
 * 未来数据定时刷新
 */
@Scheduled(cron = "0 */1 * * * ?")
public void refresh(){

    String token = cacheService.tryLock("FUTURE_TASK_SYNC", 1000 * 30);
    if(StringUtils.isNotBlank(token)){
        log.info("未来数据定时刷新---定时任务");

        //获取所有未来数据的集合key
        Set<String> futureKeys = cacheService.scan(ScheduleConstants.FUTURE + "*");
        for (String futureKey : futureKeys) {//future_100_50

            //获取当前数据的key  topic
            String topicKey = ScheduleConstants.TOPIC+futureKey.split(ScheduleConstants.FUTURE)[1];

            //按照key和分值查询符合条件的数据
            Set<String> tasks = cacheService.zRangeByScore(futureKey, 0, System.currentTimeMillis());

            //同步数据
            if(!tasks.isEmpty()){
                cacheService.refreshWithPipeline(futureKey,topicKey,tasks);
                log.info("成功的将"+futureKey+"刷新到了"+topicKey);
            }
        }
    }
}
```





## 主从集群

### 主从集群结构

**下图就是一个简单的Redis主从集群结构：**

![](D:/StudyNote/assets/1741871049119.png)

**如图所示，集群中有一个master节点、两个slave节点（现在叫replica）。当我们通过Redis的Java客户端访问主从集群时，应该做好路由：**

- **如果是写操作，应该访问master节点，master会自动将数据同步给两个slave节点**
- **如果是读操作，建议访问各个slave节点，从而分担并发压力**

### 搭建主从集群

#### 启动多个redis实例

**我们利用课前资料提供的docker-compose文件来构建主从集群：**

文件内容如下：

```YAML
version: "3.2"

services:
  r1:
    image: redis
    container_name: r1
    network_mode: "host"
    entrypoint: ["redis-server", "--port", "7001"]
  r2:
    image: redis
    container_name: r2
    network_mode: "host"
    entrypoint: ["redis-server", "--port", "7002"]
  r3:
    image: redis
    container_name: r3
    network_mode: "host"
    entrypoint: ["redis-server", "--port", "7003"]
```

**将其上传至虚拟机的`/root/redis`目录下：**

**注意：以前我们在部署容器时，network_mode使用的时默认的bridge网桥模式，但是redis官方并不建议我们在搭建主从集群时，使用的默认的bridge模式，而是使用host模式，使容器与宿主机使用同一个网络**

**执行命令，运行集群：**

```Bash
docker compose up -d
```

**由于采用的是host模式，我们看不到端口映射。不过能直接在宿主机通过ps命令查看到Redis进程：**

```Shell
ps -ef | grep redis
```

#### 构建主从关系

**虽然我们启动了3个Redis实例，但是它们并没有形成主从关系。我们需要通过命令来配置主从关系：**

```Bash
# Redis5.0以前
slaveof <masterip> <masterport>
# Redis5.0以后
replicaof <masterip> <masterport>
```

**有临时和永久两种模式：**

- **永久生效：在redis.conf文件中利用`slaveof`命令指定`master`节点**
- **临时生效：直接利用redis-cli控制台输入`slaveof`命令，指定`master`节点**

**我们测试临时模式，首先连接`r2`，让其以`r1`为master**

```Bash
# 连接r2
docker exec -it r2 redis-cli -p 7002
# 认r1主，也就是7001
slaveof 192.168.230.130 7001
```

**然后连接`r3`，让其以`r1`为master**

```Bash
# 连接r3
docker exec -it r3 redis-cli -p 7003
# 认r1主，也就是7001
slaveof 192.168.230.130 7001
```

**然后连接`r1`，查看集群状态：**

```Bash
# 连接r1
docker exec -it r1 redis-cli -p 7001
# 查看集群状态
info replication
```

**结果如下：**

```Bash
127.0.0.1:7001> info replication
# Replication
role:master
connected_slaves:2
slave0:ip=192.168.150.101,port=7002,state=online,offset=140,lag=1
slave1:ip=192.168.150.101,port=7003,state=online,offset=140,lag=1
master_failover_state:no-failover
master_replid:16d90568498908b322178ca12078114e6c518b86
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:140
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:140
```

**可以看到，当前节点`r1:7001`的角色是`master`，有两个slave与其连接：**

- **`slave0`：`port`是`7002`，也就是`r2`节点**
- **`slave1`：`port`是`7003`，也就是`r3`节点**

#### 测试

**依次在`r1`、`r2`、`r3`节点上执行下面命令：**

```Bash
set num 123

get num
```

**你会发现，只有在`r1`这个节点上可以执行`set`命令（写操作）也可以执行`get`命令（读操作），其它两个节点只能执行`get`命令（读操作）。也就是说读写操作已经分离了。**

### 主从同步原理

**当主从第一次同步或者断开重连时，从节点都会发送psync请求，尝试数据同步**

![](D:\StudyNote\assets\1741879034726.png)

#### 全量同步

**主从第一次建立连接时，会执行全量同步，将master节点的所有数据都拷贝给slave节点，流程：**

![](D:/StudyNote/assets/1741879815295.png)

**这里有一个问题，`master`如何得知`salve`是否是第一次来同步呢？？**

**有几个概念，可以作为判断依据：**

- **`Replication Id`：简称`replid`，是数据集的标记，replid一致则是同一数据集。每个`master`都有唯一的`replid`，`slave`则会继承`master`节点的`replid`**
- **`offset`：偏移量，随着记录在`repl_baklog`中的数据增多而逐渐增大。`slave`完成同步时也会记录当前同步的`offset`。如果`slave`的`offset`小于`master`的`offset`，说明`slave`数据落后于`master`，需要更新。**

**因此`slave`做数据同步，必须向`master`声明自己的`replication id `和`offset`，`master`才可以判断到底需要同步哪些数据。**

**由于我们在执行`slaveof`命令之前，所有redis节点都是`master`，有自己的`replid`和`offset`。**

**当我们第一次执行`slaveof`命令，与`master`建立主从关系时，发送的`replid`和`offset`是自己的，与`master`肯定不一致。**

**`master`判断发现`slave`发送来的`replid`与自己的不一致，说明这是一个全新的slave，就知道要做全量同步了。**

**`master`会将自己的`replid`和`offset`都发送给这个`slave`，`slave`保存这些信息到本地。自此以后`slave`的`replid`就与`master`一致了。**

**因此，master判断一个节点是否是第一次同步的依据，就是看replid是否一致。流程如图：**

![](D:/StudyNote/assets/1741880147906.png)

**完整流程描述：**

- **`slave`节点请求增量同步**
- **`master`节点判断`replid`，发现不一致，拒绝增量同步**
- **`master`将完整内存数据生成`RDB`，发送`RDB`到`slave`**
- **`slave`清空本地数据，加载`master`的`RDB`**
- **`master`将`RDB`期间的命令记录在`repl_baklog`，并持续将log中的命令发送给`slave`**
- **`slave`执行接收到的命令，保持与`master`之间的同步**

#### 增量同步

**全量同步需要先做RDB，然后将RDB文件通过网络传输个slave，成本太高了。因此除了第一次做全量同步，其它大多数时候slave与master都是做增量同步。**

**什么是增量同步？就是只更新slave与master存在差异的部分数据。如图：**

![img](D:/StudyNote/assets/1741880753627.png)

**那么master怎么知道slave与自己的数据差异在哪里呢?**

#### repl_baklog原理

**master怎么知道slave与自己的数据差异在哪里呢?**

**这就要说到全量同步时的`repl_baklog`文件了。这个文件是一个固定大小的数组，只不过数组是环形，也就是说角标到达数组末尾后，会再次从0开始读写，这样数组头部的数据就会被覆盖。**

**`repl_baklog`中会记录Redis处理过的命令及`offset`，包括master当前的`offset`，和slave已经拷贝到的`offset`：**

![](D:/StudyNote/assets/1741882505478.png)

**slave与master的offset之间的差异，就是salve需要增量拷贝的数据了。**

**随着不断有数据写入，master的offset逐渐变大，slave也不断的拷贝，追赶master的offset：**

![](D:/StudyNote/assets/1741882588532.png)

**直到数组被填满：**

![](D:/StudyNote/assets/1741882638300.png)



**此时，如果有新的数据写入，就会覆盖数组中的旧数据。不过，旧的数据只要是绿色的，说明是已经被同步到slave的数据，即便被覆盖了也没什么影响。因为未同步的仅仅是红色部分：**

![](D:/StudyNote/assets/1741882719972.png)

**但是，如果slave出现网络阻塞，导致master的`offset`远远超过了slave的`offset`：** 

![](D:/StudyNote/assets/1741882767246.png)

**如果master继续写入新数据，master的`offset`就会覆盖`repl_baklog`中旧的数据，直到将slave现在的`offset`也覆盖：**

![](D:/StudyNote/assets/1741882853707.png)

**棕色框中的红色部分，就是尚未同步，但是却已经被覆盖的数据。此时如果slave恢复，需要同步，却发现自己的`offset`都没有了，无法完成增量同步了。只能做全量同步。**

**`repl_baklog`大小有上限，写满后会覆盖最早的数据。如果slave断开时间过久，导致尚未备份的数据被覆盖，则无法基于`repl_baklog`做增量同步，只能再次全量同步。**

### 主从同步优化

**主从同步可以保证主从数据的一致性，非常重要。**

**可以从以下几个方面来优化Redis主从就集群：**

- **在master中配置`repl-diskless-sync  yes`启用无磁盘复制，避免全量同步时的磁盘IO。**
- **Redis单节点上的内存占用不要太大，减少RDB导致的过多磁盘IO**
- **适当提高`repl_baklog`的大小，发现slave宕机时尽快实现故障恢复，尽可能避免全量同步**
- **限制一个master上的slave节点数量，如果实在是太多slave，则可以采用`主-从-从`链式结构，减少master压力**

**`主-从-从`架构图：**

![](D:/StudyNote/assets/1742019506955.png)

**简述全量同步和增量同步区别？**

- **全量同步：master将完整内存数据生成RDB，发送RDB到slave。后续命令则记录在repl_baklog，逐个发送给slave。**
- **增量同步：slave提交自己的offset到master，master获取repl_baklog中从offset之后的命令给slave**

**什么时候执行全量同步？**

- **slave节点第一次连接master节点时**
- **slave节点断开时间太久，repl_baklog中的offset已经被覆盖时**

**什么时候执行增量同步？**

- **slave节点断开又恢复，并且在`repl_baklog`中能找到offset时**

## 哨兵集群

### 哨兵工作原理

**Redis提供了`哨兵`（`Sentinel`）机制来监控主从集群监控状态，确保集群的高可用性。**

#### 哨兵的作用

**哨兵集群作用原理图：**

![](D:/StudyNote/assets/1742020865249.png)



**哨兵的作用如下：**

- **状态监控：`Sentinel` 会不断检查您的`master`和`slave`是否按预期工作**
- **故障恢复（failover）：如果`master`故障，`Sentinel`会将一个`slave`提升为`master`。当故障实例恢复后会成为`slave`**
- **状态通知：`Sentinel`充当`Redis`客户端的服务发现来源，当集群发生`failover`时，会将最新集群信息推送给`Redis`的客户端**

**那么问题来了，`Sentinel`怎么知道一个Redis节点是否宕机呢？**

#### 状态监控

**`Sentinel`基于心跳机制监测服务状态，每隔1秒向集群的每个节点发送ping命令，并通过实例的响应结果来做出判断：****

- **主观下线（sdown）：如果某sentinel节点发现某Redis节点未在规定时间响应，则认为该节点主观下线。**
- **客观下线(odown)：若超过指定数量（通过`quorum`设置）的sentinel都认为该节点主观下线，则该节点客观下线。quorum值最好超过Sentinel节点数量的一半，Sentinel节点数量至少3台。**

**如图：**

![](D:/StudyNote/assets/1742020971812.png)

**一旦发现master故障，sentinel需要在salve中选择一个作为新的master，选择依据是这样的：**

- **首先会判断slave节点与master节点断开时间长短，如果超过`down-after-milliseconds * 10`则会排除该slave节点**
- **然后判断slave节点的`slave-priority`值，越小优先级越高，如果是0则永不参与选举（默认都是1）。**
- **如果`slave-prority`一样，则判断slave节点的`offset`值，越大说明数据越新，优先级越高**
- **最后是判断slave节点的`run_id`大小，越小优先级越高（`通过info server可以查看run_id`）。**

**对应的官方文档如下：**

**https://redis.io/docs/management/sentinel/#replica-selection-and-priority**

**问题来了，当选出一个新的master后，该如何实现身份切换呢？**

**大概分为两步：**

- **在多个`sentinel`中选举一个`leader`**
- **由`leader`执行`failover`**

#### 选举leader

**首先，Sentinel集群要选出一个执行`failover`的Sentinel节点，可以成为`leader`。要成为`leader`要满足两个条件：**

- **最先获得超过半数的投票**
- **获得的投票数不小于`quorum`值**

**而sentinel投票的原则有两条：**

- **优先投票给目前得票最多的**
- **如果目前没有任何节点的票，就投给自己**

**比如有3个sentinel节点，`s1`、`s2`、`s3`，假如`s2`先投票：**

- **此时发现没有任何人在投票，那就投给自己。`s2`得1票**
- **接着`s1`和`s3`开始投票，发现目前`s2`票最多，于是也投给`s2`，`s2`得3票**
- **`s2`称为`leader`，开始故障转移**

**不难看出，谁先投票，谁就会称为leader，那什么时候会触发投票呢？**

**答案是第一个确认master客观下线的人会立刻发起投票，一定会成为leader。**

**OK，`sentinel`找到`leader`以后，该如何完成`failover`呢？**

#### failover

**我们举个例子，有一个集群，初始状态下7001为`master`，7002和7003为`slave`：**

![](D:/StudyNote/assets/1742021225785(1).png)

**假如master发生故障，slave1当选。则故障转移的流程如下：**

**1）`sentinel`给备选的`slave1`节点发送`slaveof no one`命令，让该节点成为`master`**

![](D:/StudyNote/assets/1742021294890(1).png)

**2）`sentinel`给所有其它`slave`发送`slaveof 192.168.150.101 7002` 命令，让这些节点成为新`master`，也就是`7002`的`slave`节点，开始从新的`master`上同步数据。**

![](D:/StudyNote/assets/1742021368312.png)

**3）最后，当故障节点恢复后会接收到哨兵信号，执行`slaveof 192.168.150.101 7002`命令，成为`slave`：**

![](D:/StudyNote/assets/1742021427857(1).png)





### 搭建哨兵集群

**首先，我们停掉之前的redis集群：**

```Bash
# 老版本DockerCompose
docker-compose down

# 新版本Docker
docker compose down
```

**然后拿出准备好的sentinel.conf,其内容如下：**

```Bash
sentinel announce-ip "192.168.150.101"
sentinel monitor hmaster 192.168.150.101 7001 2
sentinel down-after-milliseconds hmaster 5000
sentinel failover-timeout hmaster 60000
```

**说明：**

- **`sentinel announce-ip "192.168.150.101"`：声明当前sentinel的ip**
- **`sentinel monitor hmaster 192.168.150.101 7001 2`：指定集群的主节点信息** 
  - **`hmaster`：主节点名称，自定义，任意写**
  - **`192.168.150.101 7001`：主节点的ip和端口**
  - **`2`：认定`master`下线时的`quorum`值**
- **`sentinel down-after-milliseconds hmaster 5000`：声明master节点超时多久后被标记下线**
- **`sentinel failover-timeout hmaster 60000`：在第一次故障转移失败后多久再次重试**

**我们在虚拟机的`/root/redis`目录下新建3个文件夹：`s1`、`s2`、`s3`:**

**将课前资料提供的`sentinel.conf`文件分别拷贝一份到3个文件夹中。**

**接着修改`docker-compose.yaml`文件，内容如下：**

```YAML
version: "3.2"

services:
  r1:
    image: redis
    container_name: r1
    network_mode: "host"
    entrypoint: ["redis-server", "--port", "7001"]
  r2:
    image: redis
    container_name: r2
    network_mode: "host"
    entrypoint: ["redis-server", "--port", "7002", "--slaveof", "192.168.150.101", "7001"]
  r3:
    image: redis
    container_name: r3
    network_mode: "host"
    entrypoint: ["redis-server", "--port", "7003", "--slaveof", "192.168.150.101", "7001"]
  s1:
    image: redis
    container_name: s1
    volumes:
      - /root/redis/s1:/etc/redis
    network_mode: "host"
    entrypoint: ["redis-sentinel", "/etc/redis/sentinel.conf", "--port", "27001"]
  s2:
    image: redis
    container_name: s2
    volumes:
      - /root/redis/s2:/etc/redis
    network_mode: "host"
    entrypoint: ["redis-sentinel", "/etc/redis/sentinel.conf", "--port", "27002"]
  s3:
    image: redis
    container_name: s3
    volumes:
      - /root/redis/s3:/etc/redis
    network_mode: "host"
    entrypoint: ["redis-sentinel", "/etc/redis/sentinel.conf", "--port", "27003"]
```

**直接运行命令，启动集群：**

```Shell
docker-compose up -d
```

**我们以s1节点为例，查看其运行日志：**

```Bash
# Sentinel ID is 8e91bd24ea8e5eb2aee38f1cf796dcb26bb88acf
# +monitor master hmaster 192.168.150.101 7001 quorum 2
* +slave slave 192.168.150.101:7003 192.168.150.101 7003 @ hmaster 192.168.150.101 7001
* +sentinel sentinel 5bafeb97fc16a82b431c339f67b015a51dad5e4f 192.168.150.101 27002 @ hmaster 192.168.150.101 7001
* +sentinel sentinel 56546568a2f7977da36abd3d2d7324c6c3f06b8d 192.168.150.101 27003 @ hmaster 192.168.150.101 7001
* +slave slave 192.168.150.101:7002 192.168.150.101 7002 @ hmaster 192.168.150.101 7001
```

**可以看到`sentinel`已经联系到了`7001`这个节点，并且与其它几个哨兵也建立了链接。哨兵信息如下：**

- **`27001`：`Sentinel ID`是`8e91bd24ea8e5eb2aee38f1cf796dcb26bb88acf`**
- **`27002`：`Sentinel ID`是`5bafeb97fc16a82b431c339f67b015a51dad5e4f`**
- **`27003`：`Sentinel ID`是`56546568a2f7977da36abd3d2d7324c6c3f06b8d`**

### RedisTemplate连接哨兵集群

**分为三步：**

- **1）引入依赖**
- **2）配置哨兵地址**
- **3）配置读写分离**

#### 引入依赖

**就是SpringDataRedis的依赖：**

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

#### 配置哨兵地址

**连接哨兵集群与传统单点模式不同，不再需要设置每一个redis的地址，而是直接指定哨兵地址：**

```YAML
spring:
  redis:
    sentinel:
      master: hmaster # 集群名
      nodes: # 哨兵地址列表
        - 192.168.150.101:27001
        - 192.168.150.101:27002
        - 192.168.150.101:27003
```

#### 配置读写分离

**最后，还要配置读写分离，让java客户端将写请求发送到master节点，读请求发送到slave节点。定义一个bean即可：**

```Java
@Bean
public LettuceClientConfigurationBuilderCustomizer clientConfigurationBuilderCustomizer(){
    return clientConfigurationBuilder -> clientConfigurationBuilder.readFrom(ReadFrom.REPLICA_PREFERRED);
}
```

**这个bean中配置的就是读写策略，包括四种：**

- **`MASTER`：从主节点读取**
- **`MASTER_PREFERRED`：优先从`master`节点读取，`master`不可用才读取`slave`**
- **`REPLICA`：从`slave`节点读取**
- **`REPLICA_PREFERRED`：优先从`slave`节点读取，所有的`slave`都不可用才读取`master`**

### 总结

**Sentinel的三个作用是什么？**

- **集群监控**
- **故障恢复**
- **状态通知**

**Sentinel如何判断一个redis实例是否健康？**

- **每隔1秒发送一次ping命令，如果超过一定时间没有相向则认为是主观下线（`sdown`）**
- **如果大多数sentinel都认为实例主观下线，则判定服务客观下线（`odown`）**

**故障转移步骤有哪些？**

- **首先要在`sentinel`中选出一个`leader`，由leader执行`failover`**
- **选定一个`slave`作为新的`master`，执行`slaveof noone`，切换到master模式**
- **然后让所有节点都执行`slaveof` 新master**
- **修改故障节点配置，添加`slaveof` 新master**

**sentinel选举leader的依据是什么？**

- **票数超过sentinel节点数量1半**
- **票数超过quorum数量**
- **一般情况下最先发起failover的节点会当选**

**sentinel从slave中选取master的依据是什么？**

- **首先会判断slave节点与master节点断开时间长短，如果超过`down-after-milliseconds`` * 10`则会排除该slave节点**
- **然后判断slave节点的`slave-priority`值，越小优先级越高，如果是0则永不参与选举（默认都是1）。**
- **如果`slave-prority`一样，则判断slave节点的`offset`值，越大说明数据越新，优先级越高**
- **最后是判断slave节点的`run_id`大小，越小优先级越高（`通过info server可以查看run_id`）。**

## 分片集群

**主从模式可以解决高可用、高并发读的问题。但依然有两个问题没有解决：**

- **海量数据存储**
- **高并发写**

**要解决这两个问题就需要用到分片集群了。分片的意思，就是把数据拆分存储到不同节点，这样整个集群的存储数据量就更大了。**

**Redis分片集群的结构如图：**

![](D:/StudyNote/assets/1742032046496.png)

**分片集群特征：**

-  **集群中有多个master，每个master保存不同分片数据 ，解决海量数据存储问题**
-  **每个master都可以有多个slave节点 ，确保高可用**
-  **master之间通过ping监测彼此健康状态 ，类似哨兵作用**
-  **客户端请求可以访问集群任意节点，最终都会被转发到数据所在节点** 

### 搭建分片集群

**Redis分片集群最少也需要3个master节点，由于我们的机器性能有限，我们只给每个master配置1个slave，形成最小的分片集群：**

#### 集群配置

**分片集群中的Redis节点必须开启集群模式，一般在配置文件中添加下面参数：**

```Bash
port 7000
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
appendonly yes
```

**其中有3个我们没见过的参数：**

- **`cluster-enabled`：是否开启集群模式**
- **`cluster-config-file`：集群模式的配置文件名称，无需手动创建，由集群自动维护**
- **`cluster-node-timeout`：集群中节点之间心跳超时时间**

**一般搭建部署集群肯定是给每个节点都配置上述参数，不过考虑到我们计划用`docker-compose`部署，因此可以直接在启动命令中指定参数，偷个懒。**

**在虚拟机的`/root`目录下新建一个`redis-cluster`目录，然后在其中新建一个`docker-compose.yaml`文件，内容如下：**

```YAML
version: "3.2"

services:
  r1:
    image: redis
    container_name: r1
    network_mode: "host"
    entrypoint: ["redis-server", "--port", "7001", "--cluster-enabled", "yes", "--cluster-config-file", "node.conf"]
  r2:
    image: redis
    container_name: r2
    network_mode: "host"
    entrypoint: ["redis-server", "--port", "7002", "--cluster-enabled", "yes", "--cluster-config-file", "node.conf"]
  r3:
    image: redis
    container_name: r3
    network_mode: "host"
    entrypoint: ["redis-server", "--port", "7003", "--cluster-enabled", "yes", "--cluster-config-file", "node.conf"]
  r4:
    image: redis
    container_name: r4
    network_mode: "host"
    entrypoint: ["redis-server", "--port", "7004", "--cluster-enabled", "yes", "--cluster-config-file", "node.conf"]
  r5:
    image: redis
    container_name: r5
    network_mode: "host"
    entrypoint: ["redis-server", "--port", "7005", "--cluster-enabled", "yes", "--cluster-config-file", "node.conf"]
  r6:
    image: redis
    container_name: r6
    network_mode: "host"
    entrypoint: ["redis-server", "--port", "7006", "--cluster-enabled", "yes", "--cluster-config-file", "node.conf"]
```

**注意：使用Docker部署Redis集群，network模式必须采用host**

#### 启动集群

**进入`/root/redis-cluster`目录，使用命令启动redis：**

```Bash
docker-compose up -d
```

**启动成功，可以通过命令查看启动进程：**

```Bash
ps -ef | grep redis
# 结果：
root       4822   4743  0 14:29 ?        00:00:02 redis-server *:7002 [cluster]
root       4827   4745  0 14:29 ?        00:00:01 redis-server *:7005 [cluster]
root       4897   4778  0 14:29 ?        00:00:01 redis-server *:7004 [cluster]
root       4903   4759  0 14:29 ?        00:00:01 redis-server *:7006 [cluster]
root       4905   4775  0 14:29 ?        00:00:02 redis-server *:7001 [cluster]
root       4912   4732  0 14:29 ?        00:00:01 redis-server *:7003 [cluster]
```

**可以发现每个redis节点都以cluster模式运行。不过节点与节点之间并未建立连接。**

**接下来，我们使用命令创建集群：**

```Bash
# 进入任意节点容器
docker exec -it r1 bash
# 然后，执行命令
redis-cli --cluster create --cluster-replicas 1 \
192.168.230.130:7001 192.168.230.130:7002 192.168.230.130:7003 \
192.168.230.130:7004 192.168.230.130:7005 192.168.230.130:7006
```

**命令说明：**

- **`redis-cli --cluster`：代表集群操作命令**
- **`create`：代表是创建集群**
- **`--cluster-replicas 1` ：指定集群中每个`master`的副本个数为1**
  - **此时`节点总数 ÷ (replicas + 1)` 得到的就是`master`的数量`n`。因此节点列表中的前`n`个节点就是`master`，其它节点都是`slave`节点，随机分配到不同`master`**

**输入命令后控制台会弹出下面的信息：**

![](D:/StudyNote/assets/1742061515096.png)

**这里展示了集群中`master`与`slave`节点分配情况，并询问你是否同意。节点信息如下：**

- **`7001`是`master`，节点`id`后6位是`da134f`**
- **`7002`是`master`，节点`id`后6位是`862fa0`**
- **`7003`是`master`，节点`id`后6位是`ad5083`**
- **`7004`是`slave`，节点`id`后6位是`391f8b`，认`ad5083`（7003）为`master`**
- **`7005`是`slave`，节点`id`后6位是`e152cd`，认`da134f`（7001）为`master`**
- **`7006`是`slave`，节点`id`后6位是`4a018a`，认`862fa0`（7002）为`master`**

**输入`yes`然后回车。会发现集群开始创建，并输出下列信息：**

![](D:/StudyNote/assets/1742061572388.png)

**接着，我们可以通过命令查看集群状态：**

```Bash
redis-cli -p 7001 cluster nodes
```

**结果：**

![](D:/StudyNote/assets/1742061620511.png)

### 散列插槽

**数据要分片存储到不同的Redis节点，肯定需要有分片的依据，这样下次查询的时候才能知道去哪个节点查询。很多数据分片都会采用一致性hash算法。而Redis则是利用散列插槽（`hash slot`）的方式实现数据分片。**

**详见官方文档：**

**https://redis.io/docs/management/scaling/#redis-cluster-101**

**在Redis集群中，共有16384个`hash slots`，集群中的每一个master节点都会分配一定数量的`hash slots`。具体的分配在集群创建时就已经指定了：**

![](D:/StudyNote/assets/1742061961589.png)

**如图中所示：**

- **Master[0]，本例中就是7001节点，分配到的插槽是0~5460**
- **Master[1]，本例中就是7002节点，分配到的插槽是5461~10922**
- **Master[2]，本例中就是7003节点，分配到的插槽是10923~16383**

**当我们读写数据时，Redis基于`CRC16` 算法对`key`做`hash`运算，得到的结果与`16384`取余，就计算出了这个`key`的`slot`值。然后到`slot`所在的Redis节点执行读写操作。**

**不过`hash slot`的计算也分两种情况：**

- **当`key`中包含`{}`时，根据`{}`之间的字符串计算`hash slot`**
- **当`key`中不包含`{}`时，则根据整个`key`字符串计算`hash slot`**

**例如：**

- **key是`user`，则根据`user`来计算hash slot**
- **key是`user:{age}`，则根据`age`来计算hash slot**

**我们来测试一下，先于`7001`建立连接：**

```Bash
# 进入容器
docker exec -it r1 bash
# 进入redis-cli
redis-cli -p 7001
# 测试
set user jack
```

**会发现报错了：**

![](D:/StudyNote/assets/1742062034914(1).png)

**提示我们`MOVED 5474`，其实就是经过计算，得出`user`这个`key`的`hash slot` 是`5474`，而`5474`是在`7002`节点，不能在`7001`上写入！！**

**说好的任意节点都可以读写呢？**

**这是因为我们连接的方式有问题，连接集群时，要加`-c`参数：**

```Bash
# 通过7001连接集群
redis-cli -c -p 7001
# 存入数据
set user jack
```

**结果如下：**

![img](D:/StudyNote/assets/1742062102354(1).png)

**可以看到，客户端自动跳转到了`5474`这个`slot`所在的`7002`节点。**

**现在，我们添加一个新的key，这次加上`{}`：**

```Bash
# 试一下key中带{}
set user:{age} 21

# 再试一下key中不带{}
set age 20
```

**结果如下：**

![](D:/StudyNote/assets/1742062114638.png)

**可以看到`user:{age}`和`age`计算出的`slot`都是`741`。**

### 总结

**Redis分片集群如何判断某个key应该在哪个实例？**

- **将16384个插槽分配到不同的实例**
- **根据key计算哈希值，对16384取余**
- **余数作为插槽，寻找插槽所在实例即可**

**如何将同一类数据固定的保存在同一个Redis实例？**

- **Redis计算key的插槽值时会判断key中是否包含`{}`，如果有则基于`{}`内的字符计算插槽**
- **数据的key中可以加入`{类型}`，例如key都以`{typeId}`为前缀，这样同类型数据计算的插槽一定相同**

### Java客户端连接分片集群

**RedisTemplate底层同样基于lettuce实现了分片集群的支持，而使用的步骤与哨兵模式基本一致**

**1）引入redis的starter依赖**

**2）配置分片集群地址**

**3）配置读写分离**

**与哨兵模式相比，其中只有分片集群的配置方式略有差异，如下：**

```YAML
spring:
  redis:
    cluster:
      nodes:
        - 192.168.150.101:7001
        - 192.168.150.101:7002
        - 192.168.150.101:7003
        - 192.168.150.101:8001
        - 192.168.150.101:8002
        - 192.168.150.101:8003*
```

## Redis数据结构

### RedisObject

**不管是任何一种数据类型，最终都会封装为RedisObject格式，它是一种结构体，C语言中的一种结构，可以理解为Java中的类。**

**结构大概是这样的：**

![](D:/StudyNote/assets/1742134183023.png)

**可以看到整个结构体中并不包含真实的数据，仅仅是对象头信息，内存占用的大小为4+4+24+32+64 = 128bit**

**也就是16字节，然后指针`ptr`指针指向的才是真实数据存储的内存地址。所以RedisObject的内存开销是很大的。**

**属性中的`encoding`就是当前对象底层采用的数据结构或编码方式，可选的有11种之多：**

| **编号** | **编码方式**            | **说明**               |
| :------- | :---------------------- | :--------------------- |
| 0        | OBJ_ENCODING_RAW        | raw编码动态字符串      |
| 1        | OBJ_ENCODING_INT        | long类型的整数的字符串 |
| 2        | OBJ_ENCODING_HT         | hash表（也叫dict）     |
| 3        | OBJ_ENCODING_ZIPMAP     | 已废弃                 |
| 4        | OBJ_ENCODING_LINKEDLIST | 双端链表               |
| 5        | OBJ_ENCODING_ZIPLIST    | 压缩列表               |
| 6        | OBJ_ENCODING_INTSET     | 整数集合               |
| 7        | OBJ_ENCODING_SKIPLIST   | 跳表                   |
| 8        | OBJ_ENCODING_EMBSTR     | embstr编码的动态字符串 |
| 9        | OBJ_ENCODING_QUICKLIST  | 快速列表               |
| 10       | OBJ_ENCODING_STREAM     | Stream流               |
| 11       | OBJ_ENCODING_LISTPACK   | 紧凑列表               |

**Redis中的5种不同的数据类型采用的底层数据结构和编码方式如下：**

| **数据类型** | **编码方式**                                                 |
| :----------- | :----------------------------------------------------------- |
| STRING       | `int`、`embstr`、`raw`                                       |
| LIST         | `LinkedList和ZipList`(3.2以前)、`QuickList`（3.2以后）       |
| SET          | `intset`、`HT`                                               |
| ZSET         | `ZipList`（7.0以前）、`Listpack`（7.0以后）、`HT`、`SkipList` |
| HASH         | `ZipList`（7.0以前）、`Listpack`（7.0以后）、`HT`            |

### SkipList

**SkipList（跳表）首先是链表，但与传统链表相比有几点差异：**

- **元素按照升序排列存储**
- **节点可能包含多个指针，指针跨度不同。**

**传统链表只有指向前后元素的指针，因此只能顺序依次访问。如果查找的元素在链表中间，查询的效率会比较低。而SkipList则不同，它内部包含跨度不同的多级指针，可以让我们跳跃查找链表中间的元素，效率非常高。**

**其结构如图：**

![](D:/StudyNote/assets/1742136356769(1).png)

**我们可以看到1号元素就有指向3、5、10的多个指针，查询时就可以跳跃查找。例如我们要找大小为14的元素，查找的流程是这样的：**

![](D:/StudyNote/assets/1742136402329(1).png)

- **首先找元素1节点最高级指针，也就是4级指针，起始元素大小为1，指针跨度为9，可以判断出目标元素大小为10。由于14比10大，肯定要从10这个元素向下接着找。**
- **找到10这个元素，发现10这个元素的最高级指针跨度为5，判断出目标元素大小为15，大于14，需要判断下级指针**
- **10这个元素的2级指针跨度为3，判断出目标元素为13，小于14，因此要基于元素13接着找**
- **13这个元素最高级级指针跨度为2，判断出目标元素为15，比14大，需要判断下级指针。**
- **13的下级指针跨度为1，因此目标元素是14，刚好于目标一致，找到。**

**这种多级指针的查询方式就避免了传统链表的逐个遍历导致的查询效率下降问题。在对有序数据做随机查询和排序时效率非常高。**

**跳表的结构体如下：**

```C
typedef struct zskiplist {
    // 头尾节点指针
    struct zskiplistNode *header, *tail;
    // 节点数量
    unsigned long length;
    // 最大的索引层级
    int level;
} zskiplist;
```

**可以看到SkipList主要属性是header和tail，也就是头尾指针，因此它是支持双向遍历的。**

**跳表中节点的结构体如下**：

```C
typedef struct zskiplistNode {
    sds ele; // 节点存储的字符串
    double score;// 节点分数，排序、查找用
    struct zskiplistNode *backward; // 前一个节点指针
    struct zskiplistLevel {
        struct zskiplistNode *forward; // 下一个节点指针
        unsigned long span; // 索引跨度
    } level[]; // 多级索引数组
} zskiplistNode;
```

**每个节点中都包含ele和score两个属性，其中score是得分，也就是节点排序的依据。ele则是节点存储的字符串数据指针。**

**其内存结构如下：**

![](D:/StudyNote/assets/1742136474327(1).png)

### SortedSet

**面试题：Redis的`SortedSet`底层的数据结构是怎样的？**

**答：SortedSet是有序集合，底层的存储的每个数据都包含element和score两个值。score是得分，element则是字符串值。SortedSet会根据每个element的score值排序，形成有序集合。**

**它支持的操作很多，比如：**

- **根据element查询score值**
- **按照score值升序或降序查询element**

**要实现根据element查询对应的score值，就必须实现element与score之间的键值映射。SortedSet底层是基于HashTable来实现的。**

**要实现对score值排序，并且查询效率还高，就需要有一种高效的有序数据结构，SortedSet是基于跳表实现的。**

**加分项：因为SortedSet底层需要用到两种数据结构，对内存占用比较高。因此Redis底层会对SortedSet中的元素大小做判断。如果元素大小**小于128且每个元素都小于64字节，SortedSet底层会采用ZipList，也就是压缩列表来代替HashTable和SkipList****

**不过，`ZipList`存在连锁更新问题，因此而在Redis7.0版本以后，`ZipList`又被替换为Listpack（紧凑列表）。**

**Redis源码中`zset`，也就是`SortedSet`的结构体如下：**

```C
typedef struct zset {
    dict *dict; // dict，底层就是HashTable
    zskiplist *zsl; // 跳表
} zset;
```

**其内存结构如图：**

![](D:/StudyNote/assets/1742139317905.png)

## Redis内存回收机制

**Redis之所以性能强，最主要的原因就是基于内存存储。然而单节点的Redis其内存大小不宜过大，会影响持久化或主从同步性能。**

**我们可以通过修改redis.conf文件，添加下面的配置来配置Redis的最大内存：**

```Properties
maxmemory 1gb
```

**当内存达到上限，就无法存储更多数据了。因此，Redis内部会有两套内存回收的策略：**

- **内存过期策略**
- **内存淘汰策略**

### 内存过期处理

**存入Redis中的数据可以配置过期时间，到期后再次访问会发现这些数据都不存在了，也就是被过期清理了。**

#### 过期命令

**Redis中通过`expire`命令可以给KEY设置`TTL`（过期时间），例如：**

```Bash
# 写入一条数据
set num 123
# 设置20秒过期时间
expire num 20
```

**不过set命令本身也可以支持过期时间的设置：**

```Shell
# 写入一条数据并设置20s过期时间
set num EX 20
```

**当过期时间到了以后，再去查询数据，会发现数据已经不存在。** 

#### 过期策略

**那么问题来了：**

- **Redis如何判断一个KEY是否过期呢？**
- **Redis又是何时删除过期KEY的呢？**

**Redis不管有多少种数据类型，本质是一个`KEY-VALUE`的键值型数据库，而这种键值映射底层正式基于HashTable来实现的，在Redis中叫做Dict.**

**来看下RedisDB的底层源码：**

```C
typedef struct redisDb {
    dict dict;                 / The keyspace for this DB , 也就是存放KEY和VALUE的哈希表*/
    dict *expires;              /* 同样是哈希表，但保存的是设置了TTL的KEY，及其到期时间*/
    dict *blocking_keys;        /* Keys with clients waiting for data (BLPOP)*/
    dict *ready_keys;           /* Blocked keys that received a PUSH */
    dict *watched_keys;         /* WATCHED keys for MULTI/EXEC CAS /
    int id;                     / Database ID, 0 ~ 15 /
    long long avg_ttl;          / Average TTL, just for stats /
    unsigned long expires_cursor; / Cursor of the active expire cycle. */
    list *defrag_later;         /* List of key names to attempt to defrag one by one, gradually. */
} redisDb;
```

**现在回答第一个问题：**

**面试题：Redis如何判断KEY是否过期呢？**

**答：在Redis中会有两个Dict，也就是HashTable，其中一个记录KEY-VALUE键值对，另一个记录KEY和过期时间。要判断一个KEY是否过期，只需要到记录过期时间的Dict中根据KEY查询即可。**

**Redis是何时删除过期KEY的呢？**

**Redis并不会在KEY过期时立刻删除KEY，因为要实现这样的效果就必须给每一个过期的KEY设置时钟，并监控这些KEY的过期状态。无论对CPU还是内存都会带来极大的负担。**

**Redis的过期KEY删除策略有两种：**

- **惰性删除**
- **周期删除**

**惰性删除，顾明思议就是过期后不会立刻删除。那在什么时候删除呢？**

**Redis会在每次访问KEY的时候判断当前KEY有没有设置过期时间，如果有，过期时间是否已经到期。对应的源码如下：**

```C
// db.c
// 寻找要执行写操作的key
robj *lookupKeyWriteWithFlags(redisDb *db, robj *key, int flags) {
    // 检查key是否过期，如果过期则删除
    expireIfNeeded(db,key);
    return lookupKey(db,key,flags);
}

// 寻找要执行读操作的key
robj *lookupKeyReadWithFlags(redisDb *db, robj *key, int flags) {
    robj *val;
    // 检查key是否过期，如果过期则删除
    if (expireIfNeeded(db,key) == 1) {
        // 略 ...
    }
    val = lookupKey(db,key,flags);
    if (val == NULL)
        goto keymiss;
    server.stat_keyspace_hits++;
    return val;
}
```

**周期删除：顾明思议是通过一个定时任务，周期性的抽样部分过期的key，然后执行删除。**

**执行周期有两种：**

- **SLOW模式：Redis会设置一个定时任务`serverCron()`，按照`server.hz`的频率来执行过期key清理**
- **FAST模式：Redis的每个事件循环前执行过期key清理（事件循环就是IO事件处理的循环）。**

**SLOW模式规则：**

- **① 执行频率受`server.hz`影响，默认为10，即每秒执行10次，每个执行周期100ms。**
- **② 执行清理耗时不超过一次执行周期的25%，即25ms.**
- **③ 逐个遍历db，逐个遍历db中的bucket，抽取20个key判断是否过期**
- **④ 如果没达到时间上限（25ms）并且过期key比例大于10%，再进行一次抽样，否则结束**

**FAST模式规则（过期key比例小于10%不执行）：**

- **① 执行频率受`beforeSleep()`调用频率影响，但两次FAST模式间隔不低于2ms**
- **② 执行清理耗时不超过1ms**
- **③ 逐个遍历db，逐个遍历db中的bucket，抽取20个key判断是否过期**
- **④ 如果没达到时间上限（1ms）并且过期key比例大于10%，再进行一次抽样，否则结束**

### 内存淘汰策略

**对于某些特别依赖于Redis的项目而言，仅仅依靠过期KEY清理是不够的，内存可能很快就达到上限。因此Redis允许设置内存告警阈值，当内存使用达到阈值时就会主动挑选部分KEY删除以释放更多内存。这叫做内存淘汰机制。**

#### 内存淘汰时机

**那么问题来了，当内存达到阈值时执行内存淘汰，但问题是Redis什么时候会执去判断内存是否达到预警呢？**

**Redis每次执行任何命令时，都会判断内存是否达到阈值：**

```C
// server.c中处理命令的部分源码
int processCommand(client *c) {
    // ... 略
    if (server.maxmemory && !server.lua_timedout) {
        // 调用performEvictions()方法尝试进行内存淘汰
        int out_of_memory = (performEvictions() == EVICT_FAIL);
        // ... 略
        if (out_of_memory && reject_cmd_on_oom) {
            // 如果内存依然不足，直接拒绝命令
            rejectCommand(c, shared.oomerr);
            return C_OK;
        }
    }
}
```

#### 淘汰策略

**好了，知道什么时候尝试淘汰了，那具体Redis是如何判断该淘汰哪些`Key`的呢？**

**Redis支持8种不同的内存淘汰策略：**

- **`noeviction`： 不淘汰任何key，但是内存满时不允许写入新数据，默认就是这种策略。**
- **`volatile``-ttl`： 对设置了TTL的key，比较key的剩余TTL值，TTL越小越先被淘汰**
- **`allkeys``-random`：对全体key ，随机进行淘汰。也就是直接从db->dict中随机挑选**
- **`volatile-random`：对设置了TTL的key ，随机进行淘汰。也就是从db->expires中随机挑选。**
- **`allkeys-lru`： 对全体key，基于LRU算法进行淘汰**
- **`volatile-lru`： 对设置了TTL的key，基于LRU算法进行淘汰**
- **`allkeys-lfu`： 对全体key，基于LFU算法进行淘汰**
- **`volatile-lfu`： 对设置了TTL的key，基于LFI算法进行淘汰**

**比较容易混淆的有两个算法：**

- **LRU（`L``east ``R``ecently ``U``sed`），最近最久未使用。用当前时间减去最后一次访问时间，这个值越大则淘汰优先级越高。**
- **LFU（`L``east ``F``requently ``U``sed`），最少频率使用。会统计每个key的访问频率，值越小淘汰优先级越高。**

**Redis怎么知道某个KEY的`最近一次访问时间`或者是`访问频率`呢？**

**还记不记得之前讲过的RedisObject的结构？**

**回忆一下：**

![](D:/StudyNote/assets/1742146328342.png)

**其中的`lru`就是记录最近一次访问时间和访问频率的。当然，你选择`LRU`和`LFU`时的记录方式不同：**

- **LRU：以秒为单位记录最近一次访问时间，长度24bit**
- **LFU：高16位以分钟为单位记录最近一次访问时间，低8位记录逻辑访问次数**

**时间就不说了，那么逻辑访问次数又是怎么回事呢？8位无符号数字最大才255，访问次数超过255怎么办？**

**这就要聊起Redis的逻辑访问次数算法了，LFU的访问次数之所以叫做逻辑访问次数，是因为并不是每次key被访问都计数，而是通过运算：**

- **① 生成`[0,1)`之间的随机数`R`**
- **② 计算 ：1/(旧次数 *  lfu_log_factor + 1)，记录为P， `lfu_log_factor`默认为10**
- **③ 如果 `R` < `P `，则计数器 `+1`，且最大不超过255**
- **④ 访问次数会随时间衰减，距离上一次访问时间每隔 `lfu_decay_time` 分钟(默认1) ，计数器`-1`**

**显然LFU的基于访问频率的统计更符合我们的淘汰目标，因此官方推荐使用LFU算法。**

**算法我们弄明白了，不过这里大家要注意一下：Redis中的`KEY`可能有数百万甚至更多，每个KEY都有自己访问时间或者逻辑访问次数。我们要找出时间最早的或者访问次数最小的，难道要把Redis中所有数据排序？**

**要知道Redis的内存淘汰是在每次执行命令时处理的。如果每次执行命令都先对全量数据做内存排序，那命令的执行时长肯定会非常长，这是不现实的。**

**所以Redis采取的是抽样法，即每次抽样一定数量（`maxmemory_smples`）的key，然后基于内存策略做排序，找出淘汰优先级最高的，删除这个key。这就导致Redis的算法并不是真正的LRU，而是一种基于抽样的近似LRU算法。**

**不过，在Redis3.0以后改进了这个算法，引入了一个淘汰候选池，抽样的key要与候选池中的key比较淘汰优先级，优先级更高的才会被放入候选池。然后在候选池中找出优先级最高的淘汰掉，这就使算法的结果更接近与真正的LRU算法了。特别是在抽样值较高的情况下（例如10），可以达到与真正的LRU接近的效果。**

### 总结

**面试题：Redis如何判断KEY是否过期呢？**

**答：在Redis中会有两个Dict，也就是HashTable，其中一个记录KEY-VALUE键值对，另一个记录KEY和过期时间。要判断一个KEY是否过期，只需要到记录过期时间的Dict中根据KEY查询即可。**

**面试题：Redis何时删除过期KEY？如何删除？**

**答：Redis的过期KEY处理有两种策略，分别是惰性删除和周期删除。**

**惰性删除是指在每次用户访问某个KEY时，判断KEY的过期时间：如果过期则删除；如果未过期则忽略。**

**周期删除有两种模式：**

- **SLOW模式：通过一个定时任务，定期的抽样部分带有TTL的KEY，判断其是否过期。默认情况下定时任务的执行频率是每秒10次，但每次执行不能超过25毫秒。如果执行抽样后发现时间还有剩余，并且过期KEY的比例较高，则会多次抽样。**
- **FAST模式：在Redis每次处理NIO事件之前，都会抽样部分带有TTL的KEY，判断是否过期，因此执行频率较高。但是每次执行时长不能超过1ms，如果时间充足并且过期KEY比例过高，也会多次抽样**

**面试题：当Redis内存不足时会怎么做？**

**答：这取决于配置的内存淘汰策略，Redis支持很多种内存淘汰策略，例如LRU、LFU、Random. 但默认的策略是直接拒绝新的写入请求。而如果设置了其它策略，则会在每次执行命令后判断占用内存是否达到阈值。如果达到阈值则会基于配置的淘汰策略尝试进行内存淘汰，直到占用内存小于阈值为止。**

**面试题：那你能聊聊LRU和LFU吗？**

**答：`LRU`是最近最久未使用。Redis的Key都是RedisObject，当启用LRU算法后，Redis会在Key的头信息中使用24个bit记录每个key的最近一次使用的时间`lru`。每次需要内存淘汰时，就会抽样一部分KEY，找出其中空闲时间最长的，也就是`now - lru`结果最大的，然后将其删除。如果内存依然不足，就重复这个过程。**

**由于采用了抽样来计算，这种算法只能说是一种近似LRU算法。因此在Redis4.0以后又引入了`LFU`算法，这种算法是统计最近最少使用，也就是按key的访问频率来统计。当启用LFU算法后，Redis会在key的头信息中使用24bit记录最近一次使用时间和逻辑访问频率。其中高16位是以分钟为单位的最近访问时间，后8位是逻辑访问次数。与LFU类似，每次需要内存淘汰时，就会抽样一部分KEY，找出其中逻辑访问次数最小的，将其淘汰。**

**面试题：逻辑访问次数是如何计算的？**

**答：由于记录访问次数的只有`8bit`，即便是无符号数，最大值只有255，不可能记录真实的访问次数。因此Redis统计的其实是逻辑访问次数。这其中有一个计算公式，会根据当前的访问次数做计算，结果要么是次数`+1`，要么是次数不变。但随着当前访问次数越大，`+1`的概率也会越低，并且最大值不超过255.**

**除此以外，逻辑访问次数还有一个衰减周期，默认为1分钟，即每隔1分钟逻辑访问次数会`-1`。这样逻辑访问次数就能基本反映出一个`key`的访问热度了。**

## 缓存问题

**Redis经常被用作缓存，而缓存在使用的过程中存在很多问题需要解决。例如：**

- **缓存的数据一致性问题**
- **缓存击穿**
- **缓存穿透**
- **缓存雪崩**

### 缓存一致性

**我们先看下目前企业用的最多的缓存模型。缓存的通用模型有三种：**

- **`Cache Aside`：有缓存调用者自己维护数据库与缓存的一致性。即：**
  - **查询时：命中则直接返回，未命中则查询数据库并写入缓存**
  - **更新时：更新数据库并删除缓存，查询时自然会更新缓存**
- **`Read/Write Through`：数据库自己维护一份缓存，底层实现对调用者透明。底层实现：**
  - **查询时：命中则直接返回，未命中则查询数据库并写入缓存**
  - **更新时：判断缓存是否存在，不存在直接更新数据库。存在则更新缓存，同步更新数据库**
- **`Write Behind Cahing`：读写操作都直接操作缓存，由线程异步的将缓存数据同步到数据库**

![](D:/StudyNote/assets/1742291776562.png)

**目前企业中使用最多的就是`Cache Aside`模式，因为实现起来非常简单。但缺点也很明显，就是无法保证数据库与缓存的强一致性。为什么呢？我们一起来分析一下。**

**`Cache Aside`的写操作是要在更新数据库的同时删除缓存，那为什么不选择更新数据库的同时更新缓存，而是删除呢？**

**原因很简单，假如一段时间内无人查询，但是有多次更新，那这些更新都属于无效更新。采用删除方案也就是延迟更新，什么时候有人查询了，什么时候更新。**

**那到底是先更新数据库再删除缓存，还是先删除缓存再更新数据库呢？**

**现在假设有两个线程，一个来更新数据，一个来查询数据。我们分别分析两种策略的表现。**

**我们先分析策略1，先更新数据库再删除缓存：**

**正常情况**

![](D:\StudyNote\assets\1742290706916.png)

**异常情况**

![](D:/StudyNote/assets/1742290791874.png)

**常情况说明：**

- **线程1删除缓存后，还没来得及更新数据库，**
- **此时线程2来查询，发现缓存未命中，于是查询数据库，写入缓存。由于此时数据库尚未更新，查询的是旧数据。也就是说刚才的删除白删了，缓存又变成旧数据了。**
- **然后线程1更新数据库，此时数据库是新数据，缓存是旧数据**

**由于更新数据库的操作本身比较耗时，在期间有线程来查询数据库并更新缓存的概率非常高。因此不推荐这种方案。**

**再来看策略2，先更新数据库再删除缓存：**

**正常情况**

![](D:/StudyNote/assets/1742290895110.png)

**异常情况**

![](D:/StudyNote/assets/1742291019137.png)

**异常情况说明：**

- **线程1查询缓存未命中，于是去查询数据库，查询到旧数据**
- **线程1将数据写入缓存之前，线程2来了，更新数据库，删除缓存**
- **线程1执行写入缓存的操作，写入旧数据**

**可以发现，异常状态发生的概率极为苛刻，线程1必须是查询数据库已经完成，但是缓存尚未写入之前。线程2要完成更新数据库同时删除缓存的两个操作。要知道线程1执行写缓存的速度在毫秒之间，速度非常快，在这么短的时间要完成数据库和缓存的操作，概率非常之低。**

**综上，添加缓存的目的是为了提高系统性能，而你要付出的代价就是缓存与数据库的强一致性。如果你要求数据库与缓存的强一致，那就需要加锁避免并行读写。但这就降低了性能，与缓存的目标背道而驰。**

**因此不管任何缓存同步方案最终的目的都是尽可能保证最终一致性，降低发生不一致的概率。我们采用先更新数据库再删除缓存的方案，已经将这种概率降到足够低，目的已经达到了。**

**同时我们还要给缓存加上过期时间，一旦发生缓存不一致，当缓存过期后会重新加载，数据最终还是能保证一致。这就可以作为一个兜底方案。**

### 缓存穿透

**什么是缓存穿透呢？**

**我们知道，当请求查询缓存未命中时，需要查询数据库以加载缓存。但是大家思考一下这样的场景：**

> **如果我访问一个数据库中也不存在的数据。会出现什么现象？**

**由于数据库中不存在该数据，那么缓存中肯定也不存在。因此不管请求该数据多少次，缓存永远不可能建立，请求永远会直达数据库。**

**假如有不怀好意的人，开启很多线程频繁的访问一个数据库中也不存在的数据。由于缓存不可能生效，那么所有的请求都访问数据库，可能就会导致数据库因过高的压力而宕机。**

**解决这个问题有两种思路：**

- **缓存空值**
- **布隆过滤器**

#### 缓存空值

**简单来说，就是当我们发现请求的数据即不存在与缓存，也不存在与数据库时，将空值缓存到Redis，避免频繁查询数据库。实现思路如下：**

![](D:/StudyNote/assets/1742295165966.png)

**优点：**

- **实现简单，维护方便**

**缺点：**

- **额外的内存消耗**

#### 布隆过滤器

**布隆过滤是一种数据统计的算法，用于检索一个元素是否存在一个集合中。**

**一般我们判断集合中是否存在元素，都会先把元素保存到类似于树、哈希表等数据结构中，然后利用这些结构查询效率高的特点来快速匹配判断。但是随着元素数量越来越多，这种模式对内存的占用也越来越大，检索的速度也会越来越慢。而布隆过滤的内存占用小，查询效率却很高。**

**布隆过滤首先需要一个很长的bit数组，默认数组中每一位都是0.** 

![](D:/StudyNote/assets/1742295267237.png)

**然后还需要`K`个`hash`函数，将元素基于这些hash函数做运算的结果映射到bit数组的不同位置，并将这些位置置为1，例如现在k=3：**

- **`hello`经过运算得到3个角标：1、5、12**
- **`world`经过运算得到3个角标：8、17、21**
- **`java`经过运算得到3个角标：17、25、28**

**则需要将每个元素对应角标位置置为1：**

![](D:/StudyNote/assets/1742295351833.png)

**此时，我们要判断元素是否存在，只需要再次基于`K`个`hash`函数做运算， 得到`K`个角标，判断每个角标的位置是不是1：**

- **只要全是1，就证明元素存在**
- **任意位置为0，就证明元素一定不存在**

**假如某个元素本身并不存在，也没添加到布隆过滤器过。但是由于存在hash碰撞的可能性，这就会出现这个元素计算出的角标已经被其它元素置为1的情况。那么这个元素也会被误判为已经存在。**

**因此，布隆过滤器的判断存在误差：**

- **当布隆过滤器认为元素不存在时，它肯定不存在**
- **当布隆过滤器认为元素存在时，它可能存在，也可能不存在**

**当`bit`数组越大、`Hash`函数`K`越复杂，`K`越大时，这个误判的概率也就越低。由于采用`bit`数组来标示数据，即便`4,294,967,296`个`bit`位，也只占`512mb`的空间**

**我们可以把数据库中的数据利用布隆过滤器标记出来，当用户请求缓存未命中时，先基于布隆过滤器判断。如果不存在则直接拒绝请求，存在则去查询数据库。尽管布隆过滤存在误差，但一般都在0.01%左右，可以大大减少数据库压力。**

**使用布隆过滤后的流程如下：**

![](D:/StudyNote/assets/1742295446134.png)

### 缓存雪崩

**缓存雪崩是指在同一时段大量的缓存key同时失效或者Redis服务宕机，导致大量请求到达数据库，带来巨大压力。**

![](D:/StudyNote/assets/1742296375096.png)

**常见的解决方案有：**

- **给不同的Key的TTL添加随机值，这样KEY的过期时间不同，不会大量KEY同时过期**
- **利用Redis集群提高服务的可用性，避免缓存服务宕机**
- **给缓存业务添加降级限流策略**
- **给业务添加多级缓存，比如先查询本地缓存，本地缓存未命中再查询Redis，Redis未命中再查询数据库。即便Redis宕机，也还有本地缓存可以抗压力**

### 缓存击穿

**缓存击穿问题也叫热点Key问题，就是一个被高并发访问并且缓存重建业务较复杂的key突然失效了，无数的请求访问会在瞬间给数据库带来巨大的冲击。**

**由于我们采用的是`Cache Aside`模式，当缓存失效时需要下次查询时才会更新缓存。当某个key缓存失效时，如果这个key是热点key，并发访问量比较高。就会在一瞬间涌入大量请求，都发现缓存未命中，于是都会去查询数据库，尝试重建缓存。可能一瞬间就把数据库压垮了。**

![](D:/StudyNote/assets/1742297215047.png)

**如上图所示：**

- **线程1发现缓存未命中，准备查询数据库，重建缓存，但是因为数据比较复杂，导致查询数据库耗时较久**
- **在这个过程中，一下次来了3个新的线程，就都会发现缓存未命中，都去查询数据库**
- **数据库压力激增**

**常见的解决方案有两种：**

- **互斥锁：给重建缓存逻辑加锁，避免多线程同时指向**
- **逻辑过期：热点key不要设置过期时间，在活动结束后手动删除。**

**基于互斥锁的方案如图：**

![](D:/StudyNote/assets/1742297285257.png)

**逻辑过期的思路如图：**

![](D:/StudyNote/assets/1742297285257.png)

**两者对比**

| 解决方案 | 优点                                     | 缺点                                       |
| -------- | ---------------------------------------- | ------------------------------------------ |
| 互斥锁   | 没有额外的内存消耗，保证一致性。实现简单 | 线程需要等待，性能受到影响，可能有死锁风险 |
| 逻辑过期 | 线程无需等待，性能较好                   | 不保证一致性，有额外的内存消耗，实现复杂   |

