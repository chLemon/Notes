# 1. HBase简介
## 1.1 HBase定义
HBase是一种分布式【大数据、大集群】、可扩展【动态上下线】、支持海量数据存储的NoSQL数据库。
hbase.apache.org
## 1.2 HBase数据模型
逻辑上，HBase的数据模型和关系型数据库很类似，数据存储在一张表，有行有列。
但从底层上看（K-V），更像一个multi-dimensional map
### 1.2.1 HBase的逻辑结构
列【可以动态增加】，列族【不同列族存放在不同的文件夹中】
Row Key是有序的，字典序，唯一
Region，横向的切片，按照数据量切分
store：存储，存储的内容
### 1.2.2 Hbase的物理存储结构
时间戳TimeStamp：非常重要
不同版本（version）的数据根据timestamp进行区分
整个全部作为一个StoreFile存储
### 1.2.3 数据模型
1. Name Space
自带2个：hbase和default，hbase中存放的是HBase内置的表，default表示默认的命名空间
2. Region
定义表只需要定义列族，具体的列相当于数据，可以动态增加
3. Row
每行都由一个RowKey和多个Column组成，RowKey是字典顺序存储
4. Column
每个列都由Column Family（列族）和Column Qualifier（列限定符，列名）进行限定
5. Time Stamp
用于标识数据的不同版本【除了版本和数据不同，剩下的必须相同，RowKey ColumnFamily ColumnQualifier】
6. Cell
由（RowKey，ColumnFamily，ColumnQualifier，TimeStamp）唯一确定的单元，cell中的数据全是字节码形式存储，没有类型
## 1.3 Hbase基本架构
