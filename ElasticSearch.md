# Elasticsearch

## 认识和安装

### 初识ES

**基于传统的数据库的模糊匹配的搜索，会存在效率低下，且功能单一的问题，在分布式系统显然是不够用的，因此我们引入已关闭新的技术Elsticsearch分布式搜索引擎**

**首先我们先了解一下搜索引擎的底层实现，Lucene,这是一个Java语言的搜索引擎类库，是Apache公司的顶级项目，由DougCutting于1999年开发，有着易扩展和高性能（基于倒排索引）这两个优势，而ES是在此基础上继续开发的，具有支持分布式，可水平扩展，并且提供RESTFUL接口，可被任何语言调用等优势**

**ES结合kibana，Logstash，Beats，一整套技术栈，被叫做ELK，被广泛应用在日志数据分析，实时监控等领域**

### 安装ES

**通过下面的Docker命令即可安装单机版本的elasticsearch：**

```Bash
docker run -d \
  --name es \
  -e "ES_JAVA_OPTS=-Xms512m -Xmx512m" \
  -e "discovery.type=single-node" \
  -v es-data:/usr/share/elasticsearch/data \
  -v es-plugins:/usr/share/elasticsearch/plugins \
  --privileged \
  --network hm-net \
  -p 9200:9200 \
  -p 9300:9300 \
  elasticsearch:7.12.1
```

**注意，这里我们采用的是elasticsearch的7.12.1版本，由于8以上版本的JavaAPI变化很大，在企业中应用并不广泛，企业中应用较多的还是8以下的版本。**

**如果拉取镜像困难，可以直接导入课前资料提供的镜像tar包：**

### 安装kibana

**通过下面的Docker命令，即可部署Kibana：**

```Bash
docker run -d \
--name kibana \
-e ELASTICSEARCH_HOSTS=http://es:9200 \
--network=hm-net \
-p 5601:5601  \
kibana:7.12.1
```

## 倒排索引

### 正向索引

**我们先来回顾一下正向索引。**

**例如有一张名为`tb_goods`的表：**

| **id** | **title**      | **price** |
| :----- | :------------- | :-------- |
| 1      | 小米手机       | 3499      |
| 2      | 华为手机       | 4999      |
| 3      | 华为小米充电器 | 49        |
| 4      | 小米手环       | 49        |
| ...    | ...            | ...       |

**其中的`id`字段已经创建了索引，由于索引底层采用了B+树结构，因此我们根据id搜索的速度会非常快。但是其他字段例如`title`，只在叶子节点上存在。**

**因此要根据`title`搜索的时候只能遍历树中的每一个叶子节点，判断title数据是否符合要求。**

**比如用户的SQL语句为：**

```SQL
select * from tb_goods where title like '%手机%';
```

**那搜索的大概流程如图：**

![](D:/StudyNote/assets/1740379274429(1).png)

**说明：**

- **1）检查到搜索条件为`like '%手机%'`，需要找到`title`中包含`手机`的数据**
- **2）逐条遍历每行数据（每个叶子节点），比如第1次拿到`id`为1的数据**
- **3）判断数据中的`title`字段值是否符合条件**
- **4）如果符合则放入结果集，不符合则丢弃**
- **5）回到步骤1**

**综上，根据id精确匹配时，可以走索引，查询效率较高。而当搜索条件为模糊匹配时，由于索引无法生效，导致从索引查询退化为全表扫描，效率很差。**

**因此，正向索引适合于根据索引字段的精确搜索，不适合基于部分词条的模糊匹配。**

**而倒排索引恰好解决的就是根据部分词条模糊匹配的问题。**

### 倒排索引

**倒排索引中有两个非常重要的概念：**

- **文档（`Document`）：用来搜索的数据，其中的每一条数据就是一个文档。例如一个网页、一个商品信息**
- **词条（`Term`）：对文档数据或用户搜索数据，利用某种算法分词，得到的具备含义的词语就是词条。例如：我是中国人，就可以分为：我、是、中国人、中国、国人这样的几个词条**

**创建倒排索引是对正向索引的一种特殊处理和应用，流程如下：**

- **将每一个文档的数据利用分词算法根据语义拆分，得到一个个词条**
- **创建表，每行数据包括词条、词条所在文档id、位置等信息**
- **因为词条唯一性，可以给词条创建正向索引**

**此时形成的这张以词条为索引的表，就是倒排索引表，两者对比如下**：

**正向索引**

| **id（索引）** | **title**      | **price** |
| :------------- | :------------- | :-------- |
| 1              | 小米手机       | 3499      |
| 2              | 华为手机       | 4999      |
| 3              | 华为小米充电器 | 49        |
| 4              | 小米手环       | 49        |
| ...            | ...            | ...       |

**倒排索引**

| **词条（索引）** | **文档id** |
| :--------------- | :--------- |
| 小米             | 1，3，4    |
| 手机             | 1，2       |
| 华为             | 2，3       |
| 充电器           | 3          |
| 手环             | 4          |

**倒排索引的搜索流程如下（以搜索"华为手机"为例），如图**

![](D:/StudyNote/assets/1740379967323.png)

**流程描述：**

**1）用户输入条件`"华为手机"`进行搜索。**

**2）对用户输入条件分词，得到词条：`华为`、`手机`。**

**3）拿着词条在倒排索引中查找（由于词条有索引，查询效率很高），即可得到包含词条的文档id：`1、2、3`。**

**4）拿着文档`id`到正向索引中查找具体文档即可（由于`id`也有索引，查询效率也很高）**

## 基础概念

### 文档和字段

**elasticsearch是面向文档（Document）存储的，可以是数据库中的一条商品数据，一个订单信息。文档数据会被序列化为`json`格式后存储在`elasticsearch`中：**

**因此，原本数据库中的一行数据就是ES中的一个JSON文档；而数据库中每行数据都包含很多列，这些列就转换为JSON文档中的字段（Field）**

### 索引和映射

**随着业务发展，需要在es中存储的文档也会越来越多，比如有商品的文档、用户的文档、订单文档等等：**

**所有文档都散乱存放显然非常混乱，也不方便管理。**

**因此，我们要将类型相同的文档集中在一起管理，称为索引（Index）。例如：**

**商品索引**

```JSON
{
    "id": 1,
    "title": "小米手机",
    "price": 3499
}

{
    "id": 2,
    "title": "华为手机",
    "price": 4999
}

{
    "id": 3,
    "title": "三星手机",
    "price": 3999
}
```

**用户索引**

```JSON
{
    "id": 101,
    "name": "张三",
    "age": 21
}

{
    "id": 102,
    "name": "李四",
    "age": 24
}

{
    "id": 103,
    "name": "麻子",
    "age": 18
}
```

**订单索引**

```JSON
{
    "id": 10,
    "userId": 101,
    "goodsId": 1,
    "totalFee": 294
}

{
    "id": 11,
    "userId": 102,
    "goodsId": 2,
    "totalFee": 328
}
```

- **所有用户文档，就可以组织在一起，称为用户的索引；**
- **所有商品的文档，可以组织在一起，称为商品的索引；**
- **所有订单的文档，可以组织在一起，称为订单的索引；**

**因此，我们可以把索引当做是数据库中的表。**

**数据库的表会有约束信息，用来定义表的结构、字段的名称、类型等信息。因此，索引库中就有映射（mapping），是索引中文档的字段约束信息，类似表的结构约束。**

### mysql与ES对比

**我们统一的把mysql与elasticsearch的概念做一下对比：**

| **MySQL** | **Elasticsearch** | **说明**                                                     |
| :-------- | :---------------- | :----------------------------------------------------------- |
| Table     | Index             | 索引(index)，就是文档的集合，类似数据库的表(table)           |
| Row       | Document          | 文档（Document），就是一条条的数据，类似数据库中的行（Row），文档都是JSON格式 |
| Column    | Field             | 字段（Field），就是JSON文档中的字段，类似数据库中的列（Column） |
| Schema    | Mapping           | Mapping（映射）是索引中文档的约束，例如字段类型约束。类似数据库的表结构（Schema） |
| SQL       | DSL               | DSL是elasticsearch提供的JSON风格的请求语句，用来操作elasticsearch，实现CRUD |

**如图：**

![](D:/StudyNote/assets/1740383859513.png)

**那是不是说，我们学习了elasticsearch就不再需要mysql了呢？**

**并不是如此，两者各自有自己的擅长之处：**

-  **Mysql：擅长事务类型操作，可以确保数据的安全和一致性** 
-  **Elasticsearch：擅长海量数据的搜索、分析、计算** 

**因此在企业中，往往是两者结合使用：**

- **对安全性要求较高的写操作，使用mysql实现**
- **对查询性能要求较高的搜索需求，使用elasticsearch实现**
- **两者再基于某种方式，实现数据的同步，保证一致性**

![](D:/StudyNote/assets/1740383899391.png)

## IK分词器

**中文分词往往需要根据予以分析，比较复杂，这就需要用到中文分词器，例如IK分词器，它的由林良益在2006年开源发布的，其采用的正向迭代最细粒度切分算法一直沿用至今**

### 安装IK分词器

**方案一**：**在线安装**

**运行一个命令即可：**

```Shell
docker exec -it es ./bin/elasticsearch-plugin  install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v7.12.1/elasticsearch-analysis-ik-7.12.1.zip
```

**然后重启es容器：**

```Shell
docker restart es
```

**方案二**：**离线安装**

**如果网速较差，也可以选择离线安装。**

**首先，查看之前安装的Elasticsearch容器的plugins数据卷目录：**

```Shell
docker volume inspect es-plugins
```

**结果如下：**

```JSON
[
    {
        "CreatedAt": "2024-11-06T10:06:34+08:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/es-plugins/_data",
        "Name": "es-plugins",
        "Options": null,
        "Scope": "local"
    }
]
```

**可以看到elasticsearch的插件挂载到了`/var/lib/docker/volumes/es-plugins/_data`这个目录。我们需要把IK分词器上传至这个目录。**

**然后将准备好的文件夹上传至该目录，并重启es即可**

### 使用IK分词器

**IK分词器包含两种模式：**

-  **`ik_smart`：智能语义切分** 
-  **`ik_max_word`：最细粒度切分** 

**我们在Kibana的DevTools上来测试分词器，首先测试Elasticsearch官方提供的标准分词器：**

```JSON
POST /_analyze
{
  "analyzer": "standard",
  "text": "黑马程序员学习java太棒了"
}
```

**语法说明**

**POST：请求方式**

**/analyze：请求路径，这里省略了ES的路径，有kibana帮我们补充**

**请求参数：json风格：**

​	**analyzer:分词器类型，这里是默认的standard分词器，也可以使用上述我们提到的两种模式**

​	**text:要分词的内容**

### 扩展词典

**随着互联网的发展，“造词运动”也越发的频繁。出现了很多新的词语，在原有的词汇列表中并不存在。比如：“泰裤辣”，“传智播客” 等。**

**所以要想正确分词，IK分词器的词库也需要不断的更新，IK分词器提供了扩展词汇的功能。**

**1）打开IK分词器config目录：**

![](D:/StudyNote/assets/1740382808175.png)

**注意，如果采用在线安装的通过，默认是没有config目录的，需要把课前资料提供的ik下的config上传至对应目录。**

**2）在IKAnalyzer.cfg.xml配置文件内容添加：**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">
<properties>
        <comment>IK Analyzer 扩展配置</comment>
        <!--用户可以在这里配置自己的扩展字典 *** 添加扩展词典-->
        <entry key="ext_dict">ext.dic</entry>
</properties>
```

**3）在IK分词器的config目录新建一个 `ext.dic`，可以参考config目录下复制一个配置文件进行修改**

```Plain
传智播客
泰裤辣
```

**4）重启elasticsearch**

```Shell
docker restart es

# 查看 日志
docker logs -f elasticsearch
```

## 索引库操作

### Mapping映射属性

**Mapping是对索引库中文档的约束，常见的Mapping属性包括：**

- **`type`：字段数据类型，常见的简单类型有：** 
  - **字符串：`text`（可分词的文本）、`keyword`（精确值，例如：品牌、国家、ip地址）**
  - **数值：`long`、`integer`、`short`、`byte`、`double`、`float`、**
  - **布尔：`boolean`**
  - **日期：`date`**
  - **对象：`object`**
- **`index`：是否创建索引，默认为`true`，为true就代表es会为该字段创建倒排索引，用于搜索和排序，如果false则不会，该字段也将无法参与搜索和排序**
- **`analyzer`：使用哪种分词器**
- **`properties`：该字段的子字段**

**例如下面的json文档：**

```JSON
{
    "age": 21,
    "weight": 52.1,
    "isMarried": false,
    "info": "黑马程序员Java讲师",
    "email": "zy@itcast.cn",
    "score": [99.1, 99.5, 98.9],
    "name": {
        "firstName": "云",
        "lastName": "赵"
    }
}
```

**对应的每个字段映射（Mapping）：**

![](D:/StudyNote/assets/1740474688721.png)

### 创建索引库和映射

**基本语法**：

- **请求方式：`PUT`**
- **请求路径：`/索引库名`，可以自定义**
- **请求参数：`mapping`映射**

**格式**：

```JSON
PUT /索引库名称
{
  "mappings": {
    "properties": {
      "字段名":{
        "type": "text",
        "analyzer": "ik_smart"
      },
      "字段名2":{
        "type": "keyword",
        "index": "false"
      },
      "字段名3":{
        "properties": {
          "子字段": {
            "type": "keyword"
          }
        }
      },
      // ...略
    }
  }
}
```

**示例**：

```JSON
# PUT /heima
{
  "mappings": {
    "properties": {
      "info":{
        "type": "text",
        "analyzer": "ik_smart"
      },
      "email":{
        "type": "keyword",
        "index": "false"
      },
      "name":{
        "properties": {
          "firstName": {
            "type": "keyword"
          }
        }
      }
    }
  }
}
```

### 查询索引库

**基本语法**：

-  **请求方式：GET** 
-  **请求路径：/索引库名** 
-  **请求参数：无** 

**格式**：

```Plain
GET /索引库名
```

**示例**：

```Plain
GET /heima
```

### 修改索引库

**倒排索引结构虽然不复杂，但是一旦数据结构改变（比如改变了分词器），就需要重新创建倒排索引，这简直是灾难。因此索引库一旦创建，无法修改mapping。**

**虽然无法修改mapping中已有的字段，但是却允许添加新的字段到mapping中，因为不会对倒排索引产生影响。因此修改索引库能做的就是向索引库中添加新字段，或者更新索引库的基础属性。**

**语法说明**：

```JSON
PUT /索引库名/_mapping
{
  "properties": {
    "新字段名":{
      "type": "integer"
    }
  }
}
```

**示例**：

```JSON
PUT /heima/_mapping
{
  "properties": {
    "age":{
      "type": "integer"
    }
  }
}
```

### 删除索引库

**语法：**

-  **请求方式：DELETE** 
-  **请求路径：/索引库名** 
-  **请求参数：无** 

**格式：**

```Plain
DELETE /索引库名
```

示例：

```Plain
DELETE /heima
```

## 文档操作

### 新增文档

**语法：**

```JSON
POST /索引库名/_doc/文档id
{
    "字段1": "值1",
    "字段2": "值2",
    "字段3": {
        "子属性1": "值3",
        "子属性2": "值4"
    },
}
```

**示例：**

```JSON
POST /heima/_doc/1
{
    "info": "黑马程序员Java讲师",
    "email": "zy@itcast.cn",
    "name": {
        "firstName": "云",
        "lastName": "赵"
    }
}
```

**响应：**

![](D:/StudyNote/assets/1740481397329.png)

### 查询文档

根据rest风格，新增是post，查询应该是get，不过查询一般都需要条件，这里我们把文档id带上。

**语法：**

```JSON
GET /{索引库名称}/_doc/{id}
```

**示例：**

```JavaScript
GET /heima/_doc/1
```

![](D:/StudyNote/assets/1740488769912.png)

### 删除文档

**删除使用DELETE请求，同样，需要根据id进行删除：**

**语法：**

```JavaScript
DELETE /{索引库名}/_doc/id值
```

**示例：**

```JSON
DELETE /heima/_doc/1
```

**结果：**

![](D:/StudyNote/assets/1740488852186.png)

### 修改文档

**修改有两种方式：**

- **全量修改：直接覆盖原来的文档**
- **局部修改：修改文档中的部分字段**

#### 全量修改

全量修改是覆盖原来的文档，其本质是两步操作：

- 根据指定的id删除文档
- 新增一个相同id的文档

**注意**：如果根据id删除时，id不存在，第二步的新增也会执行，也就从修改变成了新增操作了。

**语法：**

```JSON
PUT /{索引库名}/_doc/文档id
{
    "字段1": "值1",
    "字段2": "值2",
    // ... 略
}
```

**示例：**

```JSON
PUT /heima/_doc/1
{
    "info": "黑马程序员高级Java讲师",
    "email": "zy@itcast.cn",
    "name": {
        "firstName": "云",
        "lastName": "赵"
    }
}
```

**由于`id`为`1`的文档已经被删除，所以第一次执行时，得到的反馈是`created`：相当于创建文档，当文档已经存在时，在执行反馈就是update**

![](D:/StudyNote/assets/1740489287441.png)

![](D:/StudyNote/assets/1740489304713.png)







#### 局部修改

**局部修改是只修改指定id匹配的文档中的部分字段。**

**语法：**

```JSON
POST /{索引库名}/_update/文档id
{
    "doc": {
         "字段名": "新的值",
    }
}
```

**示例：**

```JSON
POST /heima/_update/1
{
  "doc": {
    "email": "ZhaoYun@itcast.cn"
  }
}
```

**结果**

![](D:/StudyNote/assets/1740489380012.png)

### 批处理

**批处理采用POST请求，基本语法如下：**

```Java
POST _bulk
{ "index" : { "_index" : "test", "_id" : "1" } }
{ "field1" : "value1" }
{ "delete" : { "_index" : "test", "_id" : "2" } }
{ "create" : { "_index" : "test", "_id" : "3" } }
{ "field1" : "value3" }
{ "update" : {"_id" : "1", "_index" : "test"} }
{ "doc" : {"field2" : "value2"} }
```

**其中：**

- **`index`代表新增操作**
  - **`_index`：指定索引库名**
  - **`_id`指定要操作的文档id**
  - **`{ "field1" : "value1" }`：则是要新增的文档内容**
- **`delete`代表删除操作**
  - **`_index`：指定索引库名**
  - **`_id`指定要操作的文档id**
- **`update`代表更新操作**
  - **`_index`：指定索引库名**
  - **`_id`指定要操作的文档id**
  - **`{ "doc" : {"field2" : "value2"} }`：要更新的文档字段**

**示例，批量新增：**

```Java
POST /_bulk
{"index": {"_index":"heima", "_id": "3"}}
{"info": "黑马程序员C++讲师", "email": "ww@itcast.cn", "name":{"firstName": "五", "lastName":"王"}}
{"index": {"_index":"heima", "_id": "4"}}
{"info": "黑马程序员前端讲师", "email": "zhangsan@itcast.cn", "name":{"firstName": "三", "lastName":"张"}}
```

**批量删除：**

```Java
POST /_bulk
{"delete":{"_index":"heima", "_id": "3"}}
{"delete":{"_index":"heima", "_id": "4"}}
```

## DSL查询

**ES提供了DSL查询，就是以JSON格式来定义查询条件**

**Elasticsearch的查询可以分为两大类：**

- **叶子查询（Leaf** **query** **clauses）**：一般是在特定的字段里查询特定值，属于简单查询，很少单独使用。
- **复合查询（Compound** **query** **clauses）**：以逻辑方式组合多个叶子查询或者更改叶子查询的行为方式。

### 快速入门

**我们依然在Kibana的DevTools中学习查询的DSL语法。首先来看查询的语法结构：**

```JSON
GET /{索引库名}/_search
{
  "query": {
    "查询类型": {
      // .. 查询条件
    }
  }
}
```

**说明：**

- **`GET /{索引库名}/_search`：其中的`_search`是固定路径，不能修改**

**例如，我们以最简单的无条件查询为例，无条件查询的类型是：match_all，因此其查询语句如下：**

```JSON
GET /items/_search
{
  "query": {
    "match_all": {
      
    }
  }
}
```

**由于match_all无条件，所以条件位置不写即可。**

**执行结果如下：**

![](D:/StudyNote/assets/1741014468380.png)

**你会发现虽然是match_all，但是响应结果中并不会包含索引库中的所有文档，而是仅有10条。这是因为处于安全考虑，elasticsearch设置了默认的查询页数。**

### 叶子查询

**叶子查询的类型也可以做进一步细分，详情大家可以查看官方文档：**

https://www.elastic.co/guide/en/elasticsearch/reference/7.12/query-dsl.html

**如图：**

![](D:/StudyNote/assets/1741081680120.png)



**这里列举一些常见的，例如：**

- **全文检索查询（Full Text Queries）：利用分词器对用户输入搜索条件先分词，得到词条，然后再利用倒排索引搜索词条。例如：**
  - **`match`：**
  - **`multi_match`**
- **精确查询（Term-level queries）：不对用户输入搜索条件分词，根据字段内容精确值匹配。但只能查找keyword、数值、日期、boolean类型的字段。例如：**
  - **`ids`**
  - **`term`**
  - **`range`**
- **地理坐标查询：用于搜索地理位置，搜索方式很多，例如：**
  - **`geo_bounding_box`：按矩形搜索**
  - **`geo_distance`：按点和半径搜索**

#### 全文检索查询

**全文检索的种类也很多，详情可以参考官方文档：**

**https://www.elastic.co/guide/en/elasticsearch/reference/7.12/full-text-queries.html**

**以全文检索中的`match`为例，语法如下：**

```JSON
GET /{索引库名}/_search
{
  "query": {
    "match": {
      "字段名": "搜索条件"
    }
  }
}
```

**示例：**

![](D:/StudyNote/assets/1741082014321.png)

**与`match`类似的还有`multi_match`，区别在于可以同时对多个字段搜索，而且多个字段都要满足，语法示例：**

```JSON
GET /{索引库名}/_search
{
  "query": {
    "multi_match": {
      "query": "搜索条件",
      "fields": ["字段1", "字段2"]
    }
  }
}
```

**示例：**

![](D:/StudyNote/assets/1741082237637.png)

#### 精确查询

**精确查询，英文是`Term-level query`，顾名思义，词条级别的查询。也就是说不会对用户输入的搜索条件再分词，而是作为一个词条，与搜索的字段内容精确值匹配。因此推荐查找`keyword`、数值、日期、`boolean`类型的字段。例如：**

- **id**
- **price**
- **城市**
- **地名**
- **人名**

**等等，作为一个整体才有含义的字段。**

**详情可以查看官方文档：**

**https://www.elastic.co/guide/en/elasticsearch/reference/7.12/term-level-queries.html**

##### term查询

**以`term`查询为例，其语法如下：**

```JSON
GET /{索引库名}/_search
{
  "query": {
    "term": {
      "字段名": {
        "value": "搜索条件"
      }
    }
  }
}
```

**示例：**

![](D:\StudyNote\assets\1741083003322.png)

**当你输入的搜索条件不是词条，而是短语时，由于不做分词，你反而搜索不到：**

![](D:/StudyNote/assets/1741083185162.png)

**这是因为es把这整个短语当作词条，去词条库中寻找，但显然词条库里并没有华为手机这个词条，因此查找不到**

![](D:/StudyNote/assets/1741083476292.png)

**当我们使用葛兰纳诺查询时，因为词条库没有这个词条，所以查询不到匹配结构**

![](D:/StudyNote/assets/1741083653249.png)

**然而当我们更改字段为brand时，就能查找到了，这是因为当该短语并不是词条库中的词条时，es就会把这个短语与字段对应的值进行匹对，如果能匹对上，则说明这是要查询的结果**

![](D:/StudyNote/assets/1741083832357.png)

**从这张图的结果我们就可以看到，当使用name字段进行精确查找时，我们将华为当作一个整体，去匹配词条库，词条库里有华为这个词，所以能匹配到结果**

**由此，我们便总结出来精确查找的逻辑，首先对查询条件不进行分词，将条件整体当作一个词条，去词条库中匹配，能匹配上，就返回查询结果，不能的话，把这个查询条件整体去与字段的值进行匹配，如果值完全相等，则也会返回查询结果**

##### range查询

**再来看下`range`查询，语法如下：**

```JSON
GET /{索引库名}/_search
{
  "query": {
    "range": {
      "字段名": {
        "gte": {最小值},
        "lte": {最大值}
      }
    }
  }
}
```

**`range`是范围查询，对于范围筛选的关键字有：**

- **`gte`：大于等于**
- **`gt`：大于**
- **`lte`：小于等于**
- **`lt`：小于**

**示例：**

![](D:/StudyNote/assets/1741092187622.png)

### 复合查询

#### bool查询

**bool查询，即布尔查询。就是利用逻辑运算来组合一个或多个查询子句的组合。bool查询支持的逻辑运算有：**

- **must：必须匹配每个子查询，类似“与”**
- **should：选择性匹配子查询，类似“或”**
- **must_not：必须不匹配，不参与算分，类似“非”**
- **filter：必须匹配，不参与算分**

**bool查询的语法如下：**

```JSON
GET /items/_search
{
  "query": {
    "bool": {
      "must": [
        {"match": {"name": "手机"}}
      ],
      "should": [
        {"term": {"brand": { "value": "vivo" }}},
        {"term": {"brand": { "value": "小米" }}}
      ],
      "must_not": [
        {"range": {"price": {"gte": 2500}}}
      ],
      "filter": [
        {"range": {"price": {"lte": 1000}}}
      ]
    }
  }
}
```

**出于性能考虑，与搜索关键字无关的查询尽量采用must_not或filter逻辑运算，避免参与相关性算分。**

**例如黑马商城的搜索页面：**

![](D:/StudyNote/assets/1741093354363.png)

**其中输入框的搜索条件肯定要参与相关性算分，可以采用match。但是价格范围过滤、品牌过滤、分类过滤等尽量采用filter，不要参与相关性算分。**

**比如，我们要搜索`手机`，但品牌必须是`华为`，价格必须是`900~1599`，那么可以这样写：**

```JSON
GET /items/_search
{
  "query": {
    "bool": {
      "must": [
        {"match": {"name": "手机"}}
      ],
      "filter": [
        {"term": {"brand": { "value": "华为" }}},
        {"range": {"price": {"gte": 90000, "lt": 159900}}}
      ]
    }
  }
}
```

#### 算分函数查询

**当我们利用match查询时，文档结果会根据与搜索词条的关联度打分（_score），返回结果时按照分值降序排列。**

**最早的时候，ES采用的是TF(词条频率)算法进行排序**
$$
TF（词条频率）=词条出现次数/文档中词条总数
$$
**后来，经过改进，引入TF-IDF算法**
$$
IDF（逆文档频率）= Log(文档总数/包含该词条的文档总数)
$$

$$
score=\Sigma_i^nTF（词条频率）*IDF（逆文档频率）
$$

**从elasticsearch5.1开始，采用的相关性打分算法是BM25算法，公式如下：**

![](D:/StudyNote/assets/1741098050225.png)

**相较于传统的TF算法，bm25算法收词条出现频率的影响较小**

![](D:/StudyNote/assets/1741098372532.png)



**基于这套公式，就可以判断出某个文档与用户搜索的关键字之间的关联度，还是比较准确的。但是，在实际业务需求中，常常会有竞价排名的功能。不是相关度越高排名越靠前，而是掏的钱多的排名靠前。**

**要想认为控制相关性算分，就需要利用elasticsearch中的function score 查询了。**

**基本语法**：

**function score 查询中包含四部分内容：**

- **原始查询条件：query部分，基于这个条件搜索文档，并且基于BM25算法给文档打分，原始算分（query score)**
- **过滤条件：filter部分，符合该条件的文档才会重新算分**
- **算分函数：符合filter条件的文档要根据这个函数做运算，得到的函数算分（function score），有四种函数** 
  - **weight：函数结果是常量**
  - **field_value_factor：以文档中的某个字段值作为函数结果**
  - **random_score：以随机数作为函数结果**
  - **script_score：自定义算分函数算法**
- **运算模式：算分函数的结果、原始查询的相关性算分，两者之间的运算方式，包括：** 
  - **multiply：相乘**
  - **replace：用function score替换query score**
  - **其它，例如：sum、avg、max、min**

**function score的运行流程如下：**

- **1）根据原始条件查询搜索文档，并且计算相关性算分，称为原始算分（query score）**
- **2）根据过滤条件，过滤文档**
- **3）符合过滤条件的文档，基于算分函数运算，得到函数算分（function score）**
- **4）将原始算分（query score）和函数算分（function score）基于运算模式做运算，得到最终结果，作为相关性算分。**

**因此，其中的关键点是：**

- **过滤条件：决定哪些文档的算分被修改**
- **算分函数：决定函数算分的算法**
- **运算模式：决定最终算分结果**

**示例：给IPhone这个品牌的手机算分提高十倍，分析如下：**

- **过滤条件：品牌必须为IPhone**
- **算分函数：常量weight，值为10**
- **算分模式：相乘multiply**

**对应代码如下：**

```JSON
GET /hotel/_search
{
  "query": {
    "function_score": {
      "query": {  .... }, // 原始查询，可以是任意条件
      "functions": [ // 算分函数
        {
          "filter": { // 满足的条件，品牌必须是Iphone
            "term": {
              "brand": "Iphone"
            }
          },
          "weight": 10 // 算分权重为2
        }
      ],
      "boost_mode": "multipy" // 加权模式，求乘积
    }
  }
}
```

### **排序**

**elasticsearch默认是根据相关度算分（`_score`）来排序，但是也支持自定义方式对搜索结果排序。不过分词字段无法排序，能参与排序字段类型有：`keyword`类型、数值类型、地理坐标类型、日期类型等。**

**详细说明可以参考官方文档：**

**https://www.elastic.co/guide/en/elasticsearch/reference/7.12/sort-search-results.html**

**语法说明：**

```JSON
GET /indexName/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "排序字段": {
        "order": "排序方式asc和desc"
      }
    }
  ]
}
```

**仔细观察，我们就可以发现，sort是一个数据，也就是说我们可以根据多个字段排序**

**示例，我们按照商品价格排序：**

```JSON
GET /items/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "price": {
        "order": "desc"
      }
    }
  ]
}
```

**当然也可以用简化后的写法**

```json
GET /items/_search/
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "sold": "desc"
    },
    {
      "price": "asc"
    }
  ]
}
```

**这个条件代表先按照sold进行降序，当sold相等时，按照price升序**

### 分页

#### 基础分页

**elasticsearch中通过修改`from`、`size`参数来控制要返回的分页结果：**

- **`from`：从第几个文档开始**
- **`size`：总共查询几个文档**

**类似于mysql中的`limit ?, ?`**

**官方文档如下：**

**https://www.elastic.co/guide/en/elasticsearch/reference/7.12/paginate-search-results.html**

**语法如下：**

```JSON
GET /items/_search
{
  "query": {
    "match_all": {}
  },
  "from": 0, // 分页开始的位置，默认为0
  "size": 10,  // 每页文档数量，默认10
  "sort": [
    {
      "price": {
        "order": "desc"
      }
    }
  ]
}
```

#### 深度分页

**elasticsearch的数据一般会采用分片存储，也就是把一个索引中的数据分成N份，存储到不同节点上。这种存储方式比较有利于数据扩展，但给分页带来了一些麻烦。**

**比如一个索引库中有100000条数据，分别存储到4个分片，每个分片25000条数据。现在每页查询10条，查询第99页。那么分页查询的条件如下：**

```JSON
GET /items/_search
{
  "from": 990, // 从第990条开始查询
  "size": 10, // 每页查询10条
  "sort": [
    {
      "price": "asc"
    }
  ]
}
```

**从语句来分析，要查询第990~1000名的数据。**

**从实现思路来分析，肯定是将所有数据排序，找出前1000名，截取其中的990~1000的部分。但问题来了，我们如何才能找到所有数据中的前1000名呢？**

**要知道每一片的数据都不一样，第1片上的第900~1000，在另1个节点上并不一定依然是900~1000名。所以我们只能在每一个分片上都找出排名前1000的数据，然后汇总到一起，重新排序，才能找出整个索引库中真正的前1000名，此时截取990~1000的数据即可。**

**如图：**

![](D:/StudyNote/assets/1741102734581.png)

**试想一下，假如我们现在要查询的是第999页数据呢，是不是要找第9990~10000的数据，那岂不是需要把每个分片中的前10000名数据都查询出来，汇总在一起，在内存中排序？如果查询的分页深度更深呢，需要一次检索的数据岂不是更多？**

**由此可知，当查询分页深度较大时，汇总数据过多，对内存和CPU会产生非常大的压力。**

**因此elasticsearch会禁止`from+ size`` `超过10000的请求。**

**针对深度分页，elasticsearch提供了两种解决方案：**

- **`search after`：分页时需要排序，原理是从上一次查询的值开始，查询下一页数据。官方推荐使用的方式。但是这种方式不支持跳页查询，但是支持实时搜索**
- **`scroll`：Scroll是先做一次初始化搜索把所有符合搜索条件的结果缓存起来生成一个快照，然后持续地、批量地从快照里拉取数据直到没有数据剩下。而这时对索引数据的插入、删除、更新都不会影响遍历结果，因此scroll 并不适合用来做实时搜索。官方已经不推荐使用。**



**详情见文档：**

**https://www.elastic.co/guide/en/elasticsearch/reference/7.12/paginate-search-results.html**

**总结：**

**大多数情况下，我们采用普通分页就可以了。查看百度、京东等网站，会发现其分页都有限制。例如百度最多支持77页，每页不足20条。京东最多100页，每页最多60条。**

**因此，一般我们采用限制分页深度的方式即可，无需实现深度分页。**



### 高亮显示

#### 高亮原理

**什么是高亮显示呢？**

**我们在百度，京东搜索时，关键字会变成红色，比较醒目，这叫高亮显示：**

![](D:/StudyNote/assets/1741187434844.png)

**观察页面源码，你会发现两件事情：**

- **高亮词条都被加了`<em>`标签**
- **`<em>`标签都添加了红色样式**

**css样式肯定是前端实现页面的时候写好的，但是前端编写页面的时候是不知道页面要展示什么数据的，不可能给数据加标签。而服务端实现搜索功能，要是有`elasticsearch`做分词搜索，是知道哪些词条需要高亮的。**

**因此词条的高亮标签肯定是由服务端提供数据的时候已经加上的。**

**因此实现高亮的思路就是：**

- **用户输入搜索关键字搜索数据**
- **服务端根据搜索关键字到elasticsearch搜索，并给搜索结果中的关键字词条添加`html`标签**
- **前端提前给约定好的`html`标签添加`CSS`样式**

#### 实现高亮

**事实上elasticsearch已经提供了给搜索关键字加标签的语法，无需我们自己编码。**

**基本语法如下：**

```JSON
GET /{索引库名}/_search
{
  "query": {
    "match": {
      "搜索字段": "搜索关键字"
    }
  },
  "highlight": {
    "fields": {
      "高亮字段名称": {
        "pre_tags": "<em>",
        "post_tags": "</em>"
      }
    }
  }
}
```

**注意：**

- **搜索必须有查询条件，而且是全文检索类型的查询条件，例如`match`**
- **参与高亮的字段必须是`text`类型的字段**
- **默认情况下参与高亮的字段要与搜索字段一致，除非添加：`required_field_match=false`**

**示例：**

![](D:/StudyNote/assets/1741187566898.png)

### 数据聚合

#### 基本概念

**聚合（`aggregations`）可以让我们极其方便的实现对数据的统计、分析、运算。例如：**

- **什么品牌的手机最受欢迎？**
- **这些手机的平均价格、最高价格、最低价格？**
- **这些手机每月的销售情况如何？**

**实现这些统计功能的比数据库的sql要方便的多，而且查询速度非常快，可以实现近实时搜索效果。**

**官方文档：**

**https://www.elastic.co/guide/en/elasticsearch/reference/7.12/search-aggregations.html**

**聚合常见的有三类：**

-  **桶（**`Bucket`）**聚合：用来对文档做分组** 
   - **`TermAggregation`：按照文档字段值分组，例如按照品牌值分组、按照国家分组**
   - **`Date Histogram`：按照日期阶梯分组，例如一周为一组，或者一月为一组**
-  **度量（**`Metric`）**聚合：用以计算一些值，比如：最大值、最小值、平均值等** 
   - **`Avg`：求平均值**
   - **`Max`：求最大值**
   - **`Min`：求最小值**
   - **`Stats`：同时求`max`、`min`、`avg`、`sum`等**
-  **管道（**`pipeline`）**聚合：其它聚合的结果为基础做进一步运算** 

**注意：参加聚合的字段必须是keyword、日期、数值、布尔类型**

#### bucket聚合

**例如我们要统计所有商品中共有哪些商品分类，其实就是以分类（category）字段对数据分组。category值一样的放在同一组，属于`Bucket`聚合中的`Term`聚合。**

**基本语法如下：**

```JSON
GET /items/_search
{
  "size": 0, 
  "aggs": {
    "category_agg": {
      "terms": {
        "field": "category",
        "size": 20
      }
    }
  }
}
```

**语法说明：**

- **`size`：设置`size`为0，就是每页查0条，则结果中就不包含文档，只包含聚合**
- **`aggs`：定义聚合**
  - **`category_agg`：聚合名称，自定义，但不能重复**
    - **`terms`：聚合的类型，按分类聚合，所以用`term`**
      - **`field`：参与聚合的字段名称**
      - **`size`：希望返回的聚合结果的最大数量**

**来看下查询的结果：**

![](D:/StudyNote/assets/1741686203456.png)

#### 带查询条件的聚合

默认情况下，Bucket聚合是对索引库的所有文档做聚合，例如我们统计商品中所有的品牌，结果如下：

![img](D:/StudyNote/assets/1741686319254.png)

**可以看到统计出的品牌非常多。**

**但真实场景下，用户会输入搜索条件，因此聚合必须是对搜索结果聚合。那么聚合必须添加限定条件。**

**例如，我想知道价格高于3000元的手机品牌有哪些，该怎么统计呢？**

**我们需要从需求中分析出搜索查询的条件和聚合的目标：**

- **搜索查询条件：**
  - **价格高于3000**
  - **必须是手机**
- **聚合目标：统计的是品牌，肯定是对brand字段做term聚合**

**语法如下：**

```JSON
GET /items/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "term": {
            "category": "手机"
          }
        },
        {
          "range": {
            "price": {
              "gte": 300000
            }
          }
        }
      ]
    }
  }, 
  "size": 0, 
  "aggs": {
    "brand_agg": {
      "terms": {
        "field": "brand",
        "size": 20
      }
    }
  }
}
```

**聚合结果如下：**

```JSON
{
  "took" : 2,
  "timed_out" : false,
  "hits" : {
    "total" : {
      "value" : 13,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [ ]
  },
  "aggregations" : {
    "brand_agg" : {
      "doc_count_error_upper_bound" : 0,
      "sum_other_doc_count" : 0,
      "buckets" : [
        {
          "key" : "华为",
          "doc_count" : 7
        },
        {
          "key" : "Apple",
          "doc_count" : 5
        },
        {
          "key" : "小米",
          "doc_count" : 1
        }
      ]
    }
  }
}
```

**可以看到，结果中只剩下3个品牌了。**

#### Metric聚合

**上节课，我们统计了价格高于3000的手机品牌，形成了一个个桶。现在我们需要对桶内的商品做运算，获取每个品牌价格的最小值、最大值、平均值。**

**这就要用到`Metric`聚合了，例如`stat`聚合，就可以同时获取`min`、`max`、`avg`等结果。**

**语法如下：**

```JSON
GET /items/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "term": {
            "category": "手机"
          }
        },
        {
          "range": {
            "price": {
              "gte": 300000
            }
          }
        }
      ]
    }
  }, 
  "size": 0, 
  "aggs": {
    "brand_agg": {
      "terms": {
        "field": "brand",
        "size": 20
      },
      "aggs": {
        "stats_meric": {
          "stats": {
            "field": "price"
          }
        }
      }
    }
  }
}
```

**`query`部分就不说了，我们重点解读聚合部分语法。**

**可以看到我们在`brand_agg`聚合的内部，我们新加了一个`aggs`参数。这个聚合就是`brand_agg`的子聚合，会对`brand_agg`形成的每个桶中的文档分别统计。**

- **`stats_meric`：聚合名称，自定义**
  - **`stats`：聚合类型，stats是`metric`聚合的一种**
    - **`field`：聚合字段，这里选择`price`，统计价格**

**由于stats是对brand_agg形成的每个品牌桶内文档分别做统计，因此每个品牌都会统计出自己的价格最小、最大、平均值。**

**结果如下：**

![img](D:/StudyNote/assets/1741686925021.png)



**另外，我们还可以让聚合按照每个品牌的价格平均值排序：**

![](D:/StudyNote/assets/1741686940173.png)



## JavaRestClient

### 初始化RestClient

**分为三步：**

**1）在`item-service`模块中引入`es`的`RestHighLevelClient`依赖：**

```XML
<dependency>
    <groupId>org.elasticsearch.client</groupId>
    <artifactId>elasticsearch-rest-high-level-client</artifactId>
</dependency>
```

**2）因为SpringBoot默认的ES版本是`7.17.10`，所以我们需要覆盖默认的ES版本：**

```XML
  <properties>
      <maven.compiler.source>11</maven.compiler.source>
      <maven.compiler.target>11</maven.compiler.target>
      <elasticsearch.version>7.12.1</elasticsearch.version>
  </properties>
```

**3）初始化RestHighLevelClient：**

**初始化的代码如下**：

```Java
RestHighLevelClient client = new RestHighLevelClient(RestClient.builder(
        HttpHost.create("http://192.168.150.101:9200")
));
```

**这里为了单元测试方便，我们创建一个测试类`IndexTest`，然后将初始化的代码编写在`@BeforeEach`方法中：**

```Java
package com.hmall.item.es;

import org.apache.http.HttpHost;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

import java.io.IOException;

public class IndexTest {

    private RestHighLevelClient client;

    @BeforeEach
    void setUp() {
        this.client = new RestHighLevelClient(RestClient.builder(
                HttpHost.create("http://192.168.230.130:9200")
        ));
    }

    @Test
    void testConnect() {
        System.out.println(client);
    }

    @AfterEach
    void tearDown() throws IOException {
        this.client.close();
    }
}
```

**@BeforEach注解用于标记每个被@Test标记的方法在测试前执行的方法， @AfterEach方法用于标记每个被@Test标记的方法在测试后执行的方法**

### 索引库操作

#### 创建索引库

##### 商品Mapping映射

**搜索页面的效果如图所示：**

![](D:/StudyNote/assets/1740495654865.png)

**实现搜索功能需要的字段包括三大部分：**

- **搜索过滤字段**
  - **分类**
  - **品牌**
  - **价格**
- **排序字段**
  - **默认：按照更新时间降序排序**
  - **销量**
  - **价格**
- **展示字段**
  - **商品id：用于点击后跳转**
  - **图片地址**
  - **是否是广告推广商品**
  - **名称**
  - **价格**
  - **评价数量**
  - **销量**

**对应的商品表结构如下，索引库无关字段已经划掉：**

![](D:/StudyNote/assets/1740495678900.png)

**结合数据库表结构，以上字段对应的mapping映射属性如下：**

| **字段名**   | **字段类型** | **类型说明**           | **是否参与搜索** | **是否**参与分词 | **分词器** |
| ------------ | ------------ | ---------------------- | ---------------- | ---------------- | ---------- |
| id           | `long`       | 长整数                 | 是               |                  | ——         |
| name         | `text`       | 字符串，参与分词搜索   | 是               | 是               | IK         |
| price        | `integer`    | 以分为单位，所以是整数 | 是               |                  | ——         |
| stock        | `integer`    | 字符串，但需要分词     | 是               |                  | ——         |
| image        | `keyword`    | 字符串，但是不分词     |                  |                  | ——         |
| category     | `keyword`    | 字符串，但是不分词     | 是               |                  | ——         |
| brand        | `keyword`    | 字符串，但是不分词     | 是               |                  | ——         |
| sold         | `integer`    | 销量，整数             | 是               |                  | ——         |
| commentCount | `integer`    | 评价，整数             |                  |                  | ——         |
| isAD         | `boolean`    | 布尔类型               | 是               |                  | ——         |
| updateTime   | `Date`       | 更新时间               | 是               |                  | ——         |

**因此，最终我们的索引库文档结构应该是这样：**

```JSON
PUT /items
{
  "mappings": {
    "properties": {
      "id": {
        "type": "keyword"
      },
      "name":{
        "type": "text",
        "analyzer": "ik_max_word"
      },
      "price":{
        "type": "integer"
      },
      "stock":{
        "type": "integer"
      },
      "image":{
        "type": "keyword",
        "index": false
      },
      "category":{
        "type": "keyword"
      },
      "brand":{
        "type": "keyword"
      },
      "sold":{
        "type": "integer"
      },
      "commentCount":{
        "type": "integer",
        "index": false
      },
      "isAD":{
        "type": "boolean"
      },
      "updateTime":{
        "type": "date"
      }
    }
  }
}
```

##### 创建索引

**创建索引库的API如下：**

![](D:/StudyNote/assets/1740725758740.png)

**代码分为三步：**

- **1）创建Request对象。**
  - **因为是创建索引库的操作，因此Request是`CreateIndexRequest`。**
- **2）添加请求参数**
  - **其实就是Json格式的Mapping映射参数。因为json字符串很长，这里是定义了静态字符串常量`MAPPING_TEMPLATE`，让代码看起来更加优雅。**
- **3）发送请求**
  - **`client.``indices``()`方法的返回值是`IndicesClient`类型，封装了所有与索引库操作有关的方法。例如创建索引、删除索引、判断索引是否存在等**

**在`item-service`中的`IndexTest`测试类中，具体代码如下：**

```Java
@Test
void testCreateIndex() throws IOException {
    // 1.创建Request对象
    CreateIndexRequest request = new CreateIndexRequest("items");
    // 2.准备请求参数
    request.source(MAPPING_TEMPLATE, XContentType.JSON);
    // 3.发送请求
    client.indices().create(request, RequestOptions.DEFAULT);
}

static final String MAPPING_TEMPLATE = "{\n" +
            "  \"mappings\": {\n" +
            "    \"properties\": {\n" +
            "      \"id\": {\n" +
            "        \"type\": \"keyword\"\n" +
            "      },\n" +
            "      \"name\":{\n" +
            "        \"type\": \"text\",\n" +
            "        \"analyzer\": \"ik_max_word\"\n" +
            "      },\n" +
            "      \"price\":{\n" +
            "        \"type\": \"integer\"\n" +
            "      },\n" +
            "      \"stock\":{\n" +
            "        \"type\": \"integer\"\n" +
            "      },\n" +
            "      \"image\":{\n" +
            "        \"type\": \"keyword\",\n" +
            "        \"index\": false\n" +
            "      },\n" +
            "      \"category\":{\n" +
            "        \"type\": \"keyword\"\n" +
            "      },\n" +
            "      \"brand\":{\n" +
            "        \"type\": \"keyword\"\n" +
            "      },\n" +
            "      \"sold\":{\n" +
            "        \"type\": \"integer\"\n" +
            "      },\n" +
            "      \"commentCount\":{\n" +
            "        \"type\": \"integer\"\n" +
            "      },\n" +
            "      \"isAD\":{\n" +
            "        \"type\": \"boolean\"\n" +
            "      },\n" +
            "      \"updateTime\":{\n" +
            "        \"type\": \"date\"\n" +
            "      }\n" +
            "    }\n" +
            "  }\n" +
            "}";
```



#### 删除索引库

**删除索引库的请求非常简单：**

```JSON
DELETE /hotel
```

**与创建索引库相比：**

- **请求方式从PUT变为DELTE**
- **请求路径不变**
- **无请求参数**

**所以代码的差异，注意体现在Request对象上。流程如下：**

- **1）创建Request对象。这次是DeleteIndexRequest对象**
- **2）准备参数。这里是无参，因此省略**
- **3）发送请求。改用delete方法**

**在`item-service`中的`IndexTest`测试类中，编写单元测试，实现删除索引：**

```Java
@Test
void testDeleteIndex() throws IOException {
    // 1.创建Request对象
    DeleteIndexRequest request = new DeleteIndexRequest("items");
    // 2.发送请求
    client.indices().delete(request, RequestOptions.DEFAULT);
}
```

#### 判断索引库是否存在

**判断索引库是否存在，本质就是查询，对应的请求语句是：**

```JSON
GET /hotel
```

**因此与删除的Java代码流程是类似的，流程如下：**

- **1）创建Request对象。这次是GetIndexRequest对象**
- **2）准备参数。这里是无参，直接省略**
- **3）发送请求。改用exists方法**

```Java
@Test
void testExistsIndex() throws IOException {
    // 1.创建Request对象
    GetIndexRequest request = new GetIndexRequest("items");
    // 2.发送请求
    boolean exists = client.indices().exists(request, RequestOptions.DEFAULT);
    // 3.输出
    System.err.println(exists ? "索引库已经存在！" : "索引库不存在！");
}
```

**上面的代码里面的exist方法改成get方法即可拿到索引库的所有信息，返回值类型是GetResponse**

**上述所有索引库的操作都是使用以下包org.elasticsearch.client.indices中的类进行操作**

### 文档操作

**以下操作均写在初始化RestClient的那个测试类**

#### 新增文档

我们需要将数据库中的商品信息导入elasticsearch中，而不是造假数据了。

##### 实体类

**索引库结构与数据库结构还存在一些差异，因此我们要定义一个索引库结构对应的实体。**

**在`hm-service`模块的`com.hmall.item.domain.dto`包中定义一个新的DTO：**

```Java
package com.hmall.item.domain.po;

import io.swagger.annotations.ApiModel;
import io.swagger.annotations.ApiModelProperty;
import lombok.Data;

import java.time.LocalDateTime;

@Data
@ApiModel(description = "索引库实体")
public class ItemDoc{

    @ApiModelProperty("商品id")
    private String id;

    @ApiModelProperty("商品名称")
    private String name;

    @ApiModelProperty("价格（分）")
    private Integer price;
    
    @ApiModelProperty("库存数量")
    private Integer stock;

    @ApiModelProperty("商品图片")
    private String image;

    @ApiModelProperty("类目名称")
    private String category;

    @ApiModelProperty("品牌名称")
    private String brand;

    @ApiModelProperty("销量")
    private Integer sold;

    @ApiModelProperty("评论数")
    private Integer commentCount;

    @ApiModelProperty("是否是推广广告，true/false")
    private Boolean isAD;

    @ApiModelProperty("更新时间")
    private LocalDateTime updateTime;
}
```

##### API语法

**新增文档的请求语法如下：**

```JSON
POST /{索引库名}/_doc/1
{
    "name": "Jack",
    "age": 21
}
```

**对应的JavaAPI如下：**

```java
@Test
void testIndexDocument() throws IOException {
    //1:创建request对象
    IndexRequest request = new IndexRequest("indexName").id("1");
    //2:准备json文档
    request.source("", XContentType.JSON);
    //3:发送请求
    client.index(request, RequestOptions.DEFAULT);
}
```

**可以看到与索引库操作的API非常类似，同样是三步走：**

- **1）创建Request对象，这里是`IndexRequest`，因为添加文档就是创建倒排索引的过程**
- **2）准备请求参数，本例中就是Json文档**
- **3）发送请求**

**变化的地方在于，这里直接使用`client.xxx()`的API，不再需要`client.indices()`了。**

##### 完整代码

**我们导入商品数据，除了参考API模板“三步走”以外，还需要做几点准备工作：**

- **商品数据来自于数据库，我们需要先查询出来，得到`Item`对象**
- **`Item`对象需要转为`ItemDoc`对象**
- **`ItemDTO`需要序列化为`json`格式**

**因此，代码整体步骤如下：**

- **1）根据id查询商品数据`Item`**
- **2）将`Item`封装为`ItemDoc`**
- **3）将`ItemDoc`序列化为JSON**
- **4）创建IndexRequest，指定索引库名和id**
- **5）准备请求参数，也就是JSON文档**
- **6）发送请求**

**在`item-service`的`DocumentTest`测试类中，编写单元测试：**

```Java
@Test
void testAddDocument() throws IOException {
    // 1.根据id查询商品数据
    Item item = itemService.getById(100002644680L);
    // 2.转换为文档类型
    ItemDoc itemDoc = BeanUtil.copyProperties(item, ItemDoc.class);
    // 3.将ItemDTO转json
    String doc = JSONUtil.toJsonStr(itemDoc);

    // 1.准备Request对象
    IndexRequest request = new IndexRequest("items").id(itemDoc.getId());
    // 2.准备Json文档
    request.source(doc, XContentType.JSON);
    // 3.发送请求
    client.index(request, RequestOptions.DEFAULT);
}
```

#### 查询文档

**我们以根据id查询文档为例**

**查询的请求语句如下：**

```JSON
GET /{索引库名}/_doc/{id}
```

**与之前的流程类似，代码大概分2步：**

- **创建Request对象**
- **准备请求参数，这里是无参，直接省略**
- **发送请求**

**不过查询的目的是得到结果，解析为ItemDTO，还要再加一步对结果的解析。示例代码如下：**

![](D:/StudyNote/assets/1740733182455.png)

**可以看到，响应结果是一个JSON，其中文档放在一个`_source`属性中，因此解析就是拿到`_source`，反序列化为Java对象即可。**

**其它代码与之前类似，流程如下：**

- **1）准备Request对象。这次是查询，所以是`GetRequest`**
- **2）发送请求，得到结果。因为是查询，这里调用`client.get()`方法**
- **3）解析结果，就是对JSON做反序列化**



**在`item-service`的`DocumentTest`测试类中，编写单元测试：**

```Java
@Test
void testGetDocumentById() throws IOException {
    // 1.准备Request对象
    GetRequest request = new GetRequest("items").id("100002644680");
    // 2.发送请求
    GetResponse response = client.get(request, RequestOptions.DEFAULT);
    // 3.获取响应结果中的source
    String json = response.getSourceAsString();
    
    ItemDoc itemDoc = JSONUtil.toBean(json, ItemDoc.class);
    System.out.println("itemDoc= " + ItemDoc);
}
```



#### 删除文档

**删除的请求语句如下：**

```JSON
DELETE /hotel/_doc/{id}
```

**与查询相比，仅仅是请求方式从`DELETE`变成`GET`，可以想象Java代码应该依然是2步走：**

- **1）准备Request对象，因为是删除，这次是`DeleteRequest`对象。要指定索引库名和id**
- **2）准备参数，无参，直接省略**
- **3）发送请求。因为是删除，所以是`client.delete()`方法**

**在`item-service`的`DocumentTest`测试类中，编写单元测试：**

```Java
@Test
void testDeleteDocument() throws IOException {
    // 1.准备Request，两个参数，第一个是索引库名，第二个是文档id
    DeleteRequest request = new DeleteRequest("item", "100002644680");
    // 2.发送请求
    client.delete(request, RequestOptions.DEFAULT);
}
```

#### 修改文档

**修改我们讲过两种方式：**

- **全量修改：本质是先根据id删除，再新增**
- **局部修改：修改文档中的指定字段值**

**在RestClient的API中，全量修改与新增的API完全一致，判断依据是ID：**

- **如果新增时，ID已经存在，则修改**
- **如果新增时，ID不存在，则新增**

**这里不再赘述，我们主要关注局部修改的API即可。**



**局部修改的请求语法如下：**

```JSON
POST /{索引库名}/_update/{id}
{
  "doc": {
    "字段名": "字段值",
    "字段名": "字段值"
  }
}
```

**代码示例如图：**

![](D:/StudyNote/assets/1740733825477.png)

**与之前类似，也是三步走：**

- **1）准备`Request`对象。这次是修改，所以是`UpdateRequest`**
- **2）准备参数。也就是JSON文档，里面包含要修改的字段**
- **3）更新文档。这里调用`client.update()`方法**



**在`item-service`的`DocumentTest`测试类中，编写单元测试：**

```Java
@Test
void testUpdateDocument() throws IOException {
    // 1.准备Request
    UpdateRequest request = new UpdateRequest("items", "100002644680");
    // 2.准备请求参数
    request.doc(
            "price", 58800,
            "commentCount", 1
    );
    // 3.发送请求
    client.update(request, RequestOptions.DEFAULT);
}
```

#### 文档批处理

**批处理与前面讲的文档的CRUD步骤基本一致：**

- **创建Request，但这次用的是`BulkRequest`**
- **准备请求参数**
- **发送请求，这次要用到`client.bulk()`方法**

**`BulkRequest`本身其实并没有请求参数，其本质就是将多个普通的CRUD请求组合在一起发送。例如：**

- **批量新增文档，就是给每个文档创建一个`IndexRequest`请求，然后封装到`BulkRequest`中，一起发出。**
- **批量删除，就是创建N个`DeleteRequest`请求，然后封装到`BulkRequest`，一起发出**

**因此`BulkRequest`中提供了`add`方法，用以添加其它CRUD的请求：**

![](D:/StudyNote/assets/1740734544879.png)

**可以看到，能添加的请求有：**

- **`IndexRequest`，也就是新增**
- **`UpdateRequest`，也就是修改**
- **`DeleteRequest`，也就是删除**

**因此Bulk中添加了多个`IndexRequest`，就是批量新增功能了。示例：**

```Java
@Test
void testBulk() throws IOException {
    // 1.创建Request
    BulkRequest request = new BulkRequest();
    // 2.准备请求参数
    request.add(new IndexRequest("items").id("1").source("json doc1", XContentType.JSON));
    request.add(new IndexRequest("items").id("2").source("json doc2", XContentType.JSON));
    // 3.发送请求
    client.bulk(request, RequestOptions.DEFAULT);
}
```



**当我们要导入商品数据时，由于商品数量达到数十万，因此不可能一次性全部导入。建议采用循环遍历方式，每次导入1000条左右的数据。**

**`item-service`的`DocumentTest`测试类中，编写单元测试：**

```Java
@Test
void testLoadItemDocs() throws IOException {
    // 分页查询商品数据
    int pageNo = 1;
    int size = 1000;
    while (true) {
        Page<Item> page = itemService.lambdaQuery().eq(Item::getStatus, 1).page(new Page<Item>(pageNo, size));
        // 非空校验
        List<Item> items = page.getRecords();
        if (CollUtils.isEmpty(items)) {
            return;
        }
        log.info("加载第{}页数据，共{}条", pageNo, items.size());
        // 1.创建Request
        BulkRequest request = new BulkRequest("items");
        // 2.准备参数，添加多个新增的Request
        for (Item item : items) {
            // 2.1.转换为文档类型ItemDTO
            ItemDoc itemDoc = BeanUtil.copyProperties(item, ItemDoc.class);
            // 2.2.创建新增文档的Request对象
            request.add(new IndexRequest()
                            .id(itemDoc.getId())
                            .source(JSONUtil.toJsonStr(itemDoc), XContentType.JSON));
        }
        // 3.发送请求
        client.bulk(request, RequestOptions.DEFAULT);

        // 翻页
        pageNo++;
    }
}
```

### DSL查询

#### 快速入门

##### 发送请求

**首先以`match_all`查询为例，其DSL和JavaAPI的对比如图：**

![](D:/StudyNote/assets/1741613342763(1).png)

**代码解读：**

-  **第一步，创建`SearchRequest`对象，指定索引库名** 
-  **第二步，利用`request.source()`构建DSL，DSL中可以包含查询、分页、排序、高亮等** 
   - **`query()`：代表查询条件，利用`QueryBuilders.matchAllQuery()`构建一个`match_all`查询的DSL**
-  **第三步，利用`client.search()`发送请求，得到响应** 

**这里关键的API有两个，一个是`request.source()`，它构建的就是DSL中的完整JSON参数。其中包含了`query`、`sort`、`from`、`size`、`highlight`等所有功能：**

![](D:/StudyNote/assets/1741613482109.png)

**另一个是`QueryBuilders`，其中包含了我们学习过的各种叶子查询、复合查询等：**

![](D:/StudyNote/assets/1741613541842.png)

##### 解析响应结果

**在发送请求以后，得到了响应结果`SearchResponse`，这个类的结构与我们在kibana中看到的响应结果JSON结构完全一致：**

```JSON
{
    "took" : 0,
    "timed_out" : false,
    "hits" : {
        "total" : {
            "value" : 2,
            "relation" : "eq"
        },
        "max_score" : 1.0,
        "hits" : [
            {
                "_index" : "heima",
                "_type" : "_doc",
                "_id" : "1",
                "_score" : 1.0,
                "_source" : {
                "info" : "Java讲师",
                "name" : "赵云"
                }
            }
        ]
    }
}
```

**因此，我们解析`SearchResponse`的代码就是在解析这个JSON结果，对比如下：**

![](D:/StudyNote/assets/1741613628387.png)

**代码解读**：

**elasticsearch返回的结果是一个JSON字符串，结构包含：**

- **`hits`：命中的结果** 
  - **`total`：总条数，其中的value是具体的总条数值**
  - **`max_score`：所有结果中得分最高的文档的相关性算分**
  - **`hits`：搜索结果的文档数组，其中的每个文档都是一个json对象** 
    - **`_source`：文档中的原始数据，也是json对象**

**因此，我们解析响应结果，就是逐层解析JSON字符串，流程如下：**

- **`SearchHits`：通过`response.getHits()`获取，就是JSON中的最外层的`hits`，代表命中的结果** 
  - **`SearchHits#getTotalHits().value`：获取总条数信息**
  - **`SearchHits#getHits()`：获取`SearchHit`数组，也就是文档数组** 
    - **`SearchHit#getSourceAsString()`：获取文档结果中的`_source`，也就是原始的`json`文档数据**

##### 总结

**文档搜索的基本步骤是：**

1. **创建`SearchRequest`对象**
2. **准备`request.source()`，也就是DSL。**
   1. **`QueryBuilders`来构建查询条件**
   2. **传入`request.source()` 的` query() `方法**
3. **发送请求，得到结果**
4. **解析结果（参考JSON结果，从外到内，逐层解析）**

**完整代码如下：**

```Java
@Test
void testMatchAll() throws IOException {
    // 1.创建Request
    SearchRequest request = new SearchRequest("items");
    // 2.组织请求参数
    request.source().query(QueryBuilders.matchAllQuery());
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);
}

private void handleResponse(SearchResponse response) {
    SearchHits searchHits = response.getHits();
    // 1.获取总条数
    long total = searchHits.getTotalHits().value;
    System.out.println("共搜索到" + total + "条数据");
    // 2.遍历结果数组
    SearchHit[] hits = searchHits.getHits();
    for (SearchHit hit : hits) {
        // 3.得到_source，也就是原始json文档
        String source = hit.getSourceAsString();
        // 4.反序列化并打印
        ItemDoc item = JSONUtil.toBean(source, ItemDoc.class);
        System.out.println(item);
  
```

#### 叶子查询

**所有的查询条件都是由QueryBuilders来构建的，叶子查询也不例外。因此整套代码中变化的部分仅仅是query条件构造的方式，其它不动。**

**例如`match`查询：**

```Java
@Test
void testMatch() throws IOException {
    // 1.创建Request
    SearchRequest request = new SearchRequest("items");
    // 2.组织请求参数
    request.source().query(QueryBuilders.matchQuery("name", "脱脂牛奶"));
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);
}
```

**对应的json语句**

```json
GET /items/_search
{
  "query": {
    "match": {
      "name": "脱脂牛奶"
    }
  }
}
```

**再比如`multi_match`查询：**

```Java
@Test
void testMultiMatch() throws IOException {
    // 1.创建Request
    SearchRequest request = new SearchRequest("items");
    // 2.组织请求参数
    request.source().query(QueryBuilders.multiMatchQuery("脱脂牛奶", "name", "category"));
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);
}
```

**对应的json语句**

```json
GET /items/_search
{
  "query": {
    "multi_match": {
      "query": "脱脂牛奶",
      "fields": ["name", "category"]
    }
  }
}
```

**还有`range`查询：**

```Java
@Test
void testRange() throws IOException {
    // 1.创建Request
    SearchRequest request = new SearchRequest("items");
    // 2.组织请求参数
    request.source().query(QueryBuilders.rangeQuery("price").gte(10000).lte(30000));
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);
}
```

**对应的json语句**

```
GET /{索引库名}/_search
{
  "query": {
    "range": {
      "price": {
        "gte": {10000},
        "lte": {30000}
      }
    }
  }
}
```



**还有`term`查询：**

```Java
@Test
void testTerm() throws IOException {
    // 1.创建Request
    SearchRequest request = new SearchRequest("items");
    // 2.组织请求参数
    request.source().query(QueryBuilders.termQuery("brand", "华为"));
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);
}
```

**对应的json语句**

```json
GET /{索引库名}/_search
{
  "query": {
    "term": {
      "brand": {
        "value": "华为"
      }
    }
  }
}
```

#### 复合查询

**复合查询也是由`QueryBuilders`来构建，我们以`bool`查询为例，DSL和JavaAPI的对比如图：**

![](D:/StudyNote/assets/1741616583882(1).png)

**完整代码如下：**

```Java
@Test
void testBool() throws IOException {
    // 1.创建Request
    SearchRequest request = new SearchRequest("items");
    // 2.组织请求参数
    // 2.1.准备bool查询
    BoolQueryBuilder bool = QueryBuilders.boolQuery();
    // 2.2.关键字搜索
    bool.must(QueryBuilders.matchQuery("name", "脱脂牛奶"));
    // 2.3.品牌过滤
    bool.filter(QueryBuilders.termQuery("brand", "德亚"));
    // 2.4.价格过滤
    bool.filter(QueryBuilders.rangeQuery("price").lte(30000));
    request.source().query(bool);
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);
}
```

#### 排序和分页

**之前说过，`requeset.source()`就是整个请求JSON参数，所以排序、分页都是基于这个来设置，其DSL和JavaAPI的对比如下：**

![](D:/StudyNote/assets/1741617288414(1).png)

**完整示例代码：**

```Java
@Test
void testPageAndSort() throws IOException {
    int pageNo = 1, pageSize = 5;

    // 1.创建Request
    SearchRequest request = new SearchRequest("items");
    // 2.组织请求参数
    // 2.1.搜索条件参数
    request.source().query(QueryBuilders.matchQuery("name", "脱脂牛奶"));
    // 2.2.排序参数
    request.source().sort("price", SortOrder.ASC);
    // 2.3.分页参数
    request.source().from((pageNo - 1) * pageSize).size(pageSize);
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);
}
```

**这里的sort可以调用多次，以添加多个字段**



#### 高亮

**高亮查询与前面的查询有两点不同：**

- **条件同样是在`request.source()`中指定，只不过高亮条件要基于`HighlightBuilder`来构造**
- **高亮响应结果与搜索的文档结果不在一起，需要单独解析**

**首先来看高亮条件构造，其DSL和JavaAPI的对比如图：**

![](D:/StudyNote/assets/1741618069877.png)

**示例代码如下：**

```Java
@Test
void testHighlight() throws IOException {
    // 1.创建Request
    SearchRequest request = new SearchRequest("items");
    // 2.组织请求参数
    // 2.1.query条件
    request.source().query(QueryBuilders.matchQuery("name", "脱脂牛奶"));
    // 2.2.高亮条件
    request.source().highlighter(
            SearchSourceBuilder.highlight()
                    .field("name")
                    .preTags("<em>")
                    .postTags("</em>")
    );
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);
}
```

**这里的field,preTags,postTags,可以调用多次，设置多个值**

**再来看结果解析，文档解析的部分不变，主要是高亮内容需要单独解析出来，其DSL和JavaAPI的对比如图**

![](D:/StudyNote/assets/1741618311524.png)

**代码解读：**

- **第`3、4`步：从结果中获取`_source`。`hit.getSourceAsString()`，这部分是非高亮结果，json字符串。还需要反序列为`ItemDoc`对象**
- **第`5`步：获取高亮结果。`hit.getHighlightFields()`，返回值是一个`Map`，key是高亮字段名称，值是`HighlightField`对象，代表高亮值**
- **第`5.1`步：从`Map`中根据高亮字段名称，获取高亮字段值对象`HighlightField`**
- **第`5.2`步：从`HighlightField`中获取`Fragments`，并且转为字符串。这部分就是真正的高亮字符串了**
- **最后：用高亮的结果替换`ItemDoc`中的非高亮结果**

完整代码如下：

```Java
private void handleResponse(SearchResponse response) {
    SearchHits searchHits = response.getHits();
    // 1.获取总条数
    long total = searchHits.getTotalHits().value;
    System.out.println("共搜索到" + total + "条数据");
    // 2.遍历结果数组
    SearchHit[] hits = searchHits.getHits();
    for (SearchHit hit : hits) {
        // 3.得到_source，也就是原始json文档
        String source = hit.getSourceAsString();
        // 4.反序列化
        ItemDoc item = JSONUtil.toBean(source, ItemDoc.class);
        // 5.获取高亮结果
        Map<String, HighlightField> hfs = hit.getHighlightFields();
        if (CollUtils.isNotEmpty(hfs)) {
            // 5.1.有高亮结果，获取name的高亮结果
            HighlightField hf = hfs.get("name");
            if (hf != null) {
                // 5.2.获取第一个高亮结果片段，就是商品名称的高亮值
                String hfName = hf.getFragments()[0].string();
                item.setName(hfName);
            }
        }
        System.out.println(item);
    }
}
```

#### 数据聚合

##### bucket聚合

**可以看到在DSL中，`aggs`聚合条件与`query`条件是同一级别，都属于查询JSON参数。因此依然是利用`request.source()`方法来设置。**

**不过聚合条件的要利用`AggregationBuilders`这个工具类来构造。DSL与JavaAPI的语法对比如下：**

![](D:/StudyNote/assets/1741687906208(1).png)

**聚合结果与搜索文档同一级别，因此需要单独获取和解析。具体解析语法如下：**

![](D:/StudyNote/assets/1741687974596(1).png)

**完整代码如下：**

```Java
@Test
void testAgg() throws IOException {
    // 1.创建Request
    SearchRequest request = new SearchRequest("items");
    // 2.准备请求参数
    BoolQueryBuilder bool = QueryBuilders.boolQuery()
            .filter(QueryBuilders.termQuery("category", "手机"))
            .filter(QueryBuilders.rangeQuery("price").gte(300000));
    request.source().query(bool).size(0);
    // 3.聚合参数
    request.source().aggregation(
            AggregationBuilders.terms("brand_agg").field("brand").size(5)
    );
    // 4.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 5.解析聚合结果
    Aggregations aggregations = response.getAggregations();
    // 5.1.获取品牌聚合,如果是stats聚合这里的类就是stats
    Terms brandTerms = aggregations.get("brand_agg");
    // 5.2.获取聚合中的桶
    List<? extends Terms.Bucket> buckets = brandTerms.getBuckets();
    // 5.3.遍历桶内数据
    for (Terms.Bucket bucket : buckets) {
        // 5.4.获取桶内key
        String brand = bucket.getKeyAsString();
        System.out.print("brand = " + brand);
        long count = bucket.getDocCount();
        System.out.println("; count = " + count);
    }
}
```

##### metric聚合

**使用metric聚合也跟bucket一样，只需要使用AggretionBuilders的subAggretion方法去设置即可**

```java
@Test
void testAgg() throws IOException {
    //1：创建request对象
    SearchRequest request = new SearchRequest("items");
    //2：配置request参数
    request.source()
            .query(QueryBuilders.matchAllQuery());
    request.source().size(0);
    request.source()
            .aggregation(AggregationBuilders
                    .terms("brand_agg")
                    .field("brand")
                    .size(20)
                    .subAggregation(AggregationBuilders
                            .stats("stats_meric")
                            .field("price")));

    //3：发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);

}
```

**对应的json文件**

```json
GET /items/_search
{
  "query": {
    "match_all": {
    }
  }, 
  "size": 0, 
  "aggs": {
    "brand_agg": {
      "terms": {
        "field": "brand",
        "size": 20
      },
      "aggs": {
        "stats_meric": {
          "stats": {
            "field": "price"
          }
        }
      }
    }
  }
}
```

#### 算分函数

**java中使用算分函数如下**

```java
@Test
void testFunctionScore() throws IOException {
    //1：创建request对象
    SearchRequest request = new SearchRequest("items");
    FunctionScoreQueryBuilder.FilterFunctionBuilder[] filterFunctions
            = {new FunctionScoreQueryBuilder.FilterFunctionBuilder(
            QueryBuilders.termQuery("isAD", true),
            ScoreFunctionBuilders.weightFactorFunction(1000))
    };


    FunctionScoreQueryBuilder functionScoreQuery =
            QueryBuilders.functionScoreQuery(QueryBuilders.matchAllQuery(),
                    filterFunctions).boostMode(
                    CombineFunction.REPLACE);

    request.source().query(functionScoreQuery);

    //3：发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);

}
```

**对应的json文件**

```json
GET /items/_search
{
  "query": {
    "function_score": {
      "query": {
        "match_all": {}
      },
      "functions": [ 
        {
          "filter": { 
            "term": {
              "isAD": "true"
            }
          },
          "weight": 1000 
        }
      ],
      "boost_mode": "replace" 
    }
  }
}
```


