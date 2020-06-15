# HBase 

## What  

我们主要用来存储一些 运营商数据  数据量很大。且  非规则
HBase是Apache的Hadoop项目的子项目，是Hadoop Database的简称。

HBase是一个高可靠性、高性能、面向列、可伸缩的分布式存储系统，利用HBase技术可在廉价PC Server上搭建起大规模结构化存储集群。

HBase不同于一般的关系数据库，它是一个适合于**非结构化数据存储**的数据库，HBase**基于列**的而不是基于行的模式。

## Why

hbase表的特性

1、大

hbase表可以存储海量的数据。
2、无模式

mysql表中每一行列的字段是相同，而hbase表中每一行数据可以有截然不同的列。
3、面向列

hbase表中的数据可以有很多个列，后期它就是按照不同的列去存储数据，写入到不同的文件中。
面向列族进行存储数据。
4、稀疏

在hbase表中为null的列并不占用实际的存储空间。
5、数据的多版本

对于hbase表中的数据在进行数据更新的时候，它并没有把之前的结果数据直接删除掉，而是保留数据的多个版本，每一个数据都给一个版本号，这个版本号就是按照我们插入数据的时间戳去确定。
6、数据类型单一

无论是什么类型的数据，最后都被转换成了字节数组存储在hbase表中



## How

### 数据模型

![](assets/640-20200615180135919.png)

稀疏矩阵、 黑块就是key value

#### RowKey

用来表示唯一一行记录的主键，HBase的数据是按照RowKey的字典顺序进行全局排序的，所有的查询都只能依赖于这一个排序维度。

>通过下面一个例子来说明一下"字典排序"的原理：
>RowKey列表{"abc", "a", "bdf", "cdf", "def"}按字典排序后的结果为{"a", "abc", "bdf", "cdf", "defg"}
>也就是说，当两个RowKey进行排序时，先对比两个RowKey的第一个字节，如果相同，则对比第二个字节，依次类推...如果在对比到第M个字节时，已经超出了其中一个RowKey的字节长度，那么，短的RowKey要被排在另外一个RowKey的前面。

#### 稀疏矩阵

![](assets/640-2215295.)

**每一行中，列的组成都是灵活的，行与行之间并不需要遵循相同的列定义**

#### Region

**横向切割**成一个个"子表"，这一个个"子表"就是Region
![](assets/640-20200615180135898.jpeg)

**Region**是HBase中负载均衡的基本单元，当一个Region增长到一定大小以后，会自动分裂成两个。

#### Column Family

**纵向切割**
![](assets/640-20200615180135900.jpeg)

### KeyValue


KeyValue的设计不是源自Bigtable，而是要追溯至论文"The log-structured merge-tree(LSM-Tree)"。每一行中的每一列数据，都被包装成独立的拥有特定结构的KeyValue，KeyValue中包含了丰富的自我描述信息:
![](assets/640-20200615180135983.png)
看的出来，KeyValue是支撑"稀疏矩阵"设计的一个关键点：一些Key相同的任意数量的独立KeyValue就可以构成一行数据。但这种设计带来的一个显而易见的缺点：**每一个KeyValue所携带的自我描述信息，会带来显著的数据膨胀。**