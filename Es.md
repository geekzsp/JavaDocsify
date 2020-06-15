# Elasticsearch

## What 什么是Es

Es是一个全文搜索引擎，它可以快速地储存、搜索和分析海量数据。

## Why  为什么要用Es，能解决什么问题，和其他相比有什么好处

!> 全文搜索引擎胜在快速和高效的查询大批量**非结构化**的文本

**Es优点**

1. Es是分布式的。不需要其他组件。
2. Es支持Lucence的接近实时搜索
3. Es采用了GateWay的概念，备份更加简单

**Solr优点**

1. 老牌全文搜索引擎，社区强大and活跃
2. 支持多种格式如 HTML、PDF、DOC、JSON、CSV

**总结**

1. Solr是传统架构、Es是分布式架构 实时搜索效率高
2. 当单纯的对已有数据进行搜索时，Solr更快。
3. 随着数据量的增加，Solr的搜索效率会变得更低，而Elasticsearch却没有明显的变化。

## How Es是如何工作的。如何使用Es

### Es基本概念

* Node 与 Cluster

天然的分布式。一个Es实例为一个Node。一组Node构成一个集群Cluster

* 结合传统数据库对比记忆

| MySQL               | ElasticSearch                                  |
| ------------------- | ---------------------------------------------- |
| Database(数据库)    | Index(索引)                                    |
| Table(表)           | Type(类型)                                     |
| Row(行)             | Document(文档)                                 |
| Column(列)          | Field(字段)                                    |
| Schema(方案)        | Mapping(映射)                                  |
| Index(索引)         | Everthing Indexed by default(所有字段都被索引) |
| SQL(结构化查询语言) | Query DSL(查询专用语言)                        |

Index里面的单条记录成为Document(文档)。许多Document构成一个Index。 Document可以根据Type进行分组
它是虚拟的逻辑分组，用来过滤 Document。

### 基本命令

```shell
# 新建一个名叫weather的 Index。
curl -X PUT 'localhost:9200/weather'
# 删除Index
curl -X DELETE 'localhost:9200/weather'
# 新增记录 index：accounts  type:person id:1
curl -X PUT 'localhost:9200/accounts/person/1' -d 
'{
  "user": "张三",
  "title": "工程师",
  "desc": "数据库管理"
}' 
# 更新记录 （就是重新发送一次数据）
curl -X PUT 'localhost:9200/accounts/person/1' -d 
'{
    "user" : "张三",
    "title" : "工程师",
    "desc" : "数据库管理，软件开发"
}' 
# 查看记录   pretty=true表示易读的格式
curl 'localhost:9200/accounts/person/1?pretty=true'
# 删除记录 
curl -X DELETE 'localhost:9200/accounts/person/1'
# 查询所有记录  GET  /Index/Type/_search
curl 'localhost:9200/accounts/person/_search'

# 搜索  Match 查询语法  (指定的匹配条件是desc字段里面包含"软件"这个词) form 从什么开始(默认0) size指定条数 （默认10条 ）
curl 'localhost:9200/accounts/person/_search'  -d 
'{
  "query" : { "match" : { "desc" : "软件" }},
  "from": 1,
  "size": 1
}'
# or 多个搜索关键字， Elastic 认为它们是or关系。
curl 'localhost:9200/accounts/person/_search'  -d 
'{
  "query" : { "match" : { "desc" : "软件 系统" }}
}'
# and 
curl 'localhost:9200/accounts/person/_search'  -d 
'{
  "query": {
    "bool": {
      "must": [
        { "match": { "desc": "软件" } },
        { "match": { "desc": "系统" } }
      ]
    }
  }
}'
```

## Java 客户端

ES支持的客户端连接方式

1. REST API ，端口 9200   Java High Level REST Client API  推荐！

```java
<dependency>
    <groupId>org.elasticsearch.client</groupId>
    <artifactId>elasticsearch-rest-high-level-client</artifactId>
    <version>6.7.1</version>
</dependency>
```

2. Transport  tcp连接 端口 9300   官方会逐步抛弃

```java
 <dependency>
        <groupId>org.elasticsearch.client</groupId>
        <artifactId>transport</artifactId>
        <version>6.2.4</version>
 </dependency>
```

JavaApi和ElasticSearch通信的两种方式： 

1. 节点客户端（Node Client）集群中的节点（但不保存数据，不能成为主节点） 知道整个集群状态 这意味着它可以执行 APIs 但少了一个网络跃点。 如果你只需要有少数的、长期持久的对象连接到集群，客户端节点可以更高效
2. 传输客户端（Transport Client）  应用程序和ES集群之前的通讯层。进行节点轮询和集群嗅探 。是外部的 解耦的 适合 大规模集群 推荐！

```java
client = TransportClient.builder().build()
   .addTransportAddress(new InetSocketTransportAddress(InetAddress.getByName("localhost"), 9300));
//搜索
SearchResponse searchResponse = 
    client.prepareSearch("music").setTypes("lyrics").execute().actionGet();
SearchHit[] hits = searchResponse.getHits().getHits();
//插入文档
 StringBuilder json = new StringBuilder("{");
      json.append("\"name\":\""+request.raw().getParameter("name")+"\",");
      json.append("\"artist\":\""+request.raw().getParameter("artist")+"\",");
      json.append("\"year\":"+request.raw().getParameter("year")+",");
      json.append("\"album\":\""+request.raw().getParameter("album")+"\",");
      json.append("\"lyrics\":\""+request.raw().getParameter("lyrics")+"\"}");
 
      IndexRequest indexRequest = new IndexRequest("music", "lyrics",
          UUID.randomUUID().toString());
      indexRequest.source(json.toString());
      IndexResponse esResponse = client.index(indexRequest).actionGet()
```







es存储索引信息，hbase才是真的存储数据



你说的方案正是我想要表达的方案,es里可以只存需要查询的字段和hbase的rowkey，hbase存所有数据。文章中的demo的确将全部转了一份到es中，只是一个案例而已，具体的肯定是需要根据自己的业务来! 通过es查询出来id再去hbase中查找详细信息。本文只是把文章的list列出来，所以是没有进hbase查，当点击案例中的文章详情的时候再通过构建Get去hbase中查。这边是缺少了后续步骤而已!





一般情况下，公司达到一定规模，有类似全文检索的需求或者高频 key:value 的时候，大家会推荐 ES+HBase 的架构体系去完成搜索和详情的需求，而现实中，绝大多数情况下生产环境不会将数据直接写入到 ES 或者 Hbase，大家都会优先写入数据库，不进行双写的操作是因为增加链路影响业务。当然 Hbase 可能还好一点，ES 本身就是非实时查询系统（为什么是非实时，有兴趣的可以去看看 ES 读写流程），这种情况下也造就了 ES 和 HBase 的一个准实时系统。针对业务来说，准实时是可以满足相关需求的，比如商家搜索订单并不要求实时。



使用ElasticSearch赋能HBase二级索引

