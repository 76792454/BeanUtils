# Mysql存储引擎

InnoDB和MyISAM和NDB三个引擎的区别	

https://blog.csdn.net/paullinjie/article/details/80290386

InnoDB引擎（默认存储引擎）支持事务安全 数据和索引保存在磁盘和内存中，其中的数据主要是按照页的方式管理，由于磁盘和CPU之间读写速度有很大限制，所以采用缓冲池技术（内存）来提高读写速度

https://blog.csdn.net/m0_37962600/article/details/81005191

InnoDB支持行级锁。行级锁可以最大程度的支持并发，行级锁是由存储引擎层实现的。

锁：锁的主要作用是管理共享资源的并发访问，用于实现事务的隔离性

​    类型：共享锁（读锁）、独占锁（写锁)     

​    MySQL锁的力度：表级锁（开销小、并发性低），通常在服务器层实现

​                  行级锁（开销大、并发性高），只会在存储引擎层面进行实现

innodb存储引擎：适合做修改、删除

MyISAM引擎 

MyISAM存储引擎的特点是：表级锁、不支持事务，支持全文索引，适合一些CMS内容管理系统作为后台数据库使用，但是使用大并发、重负荷生产系统上，表锁结构的特性就显得力不从心；内存只存索引

Myisam存储引擎：适合做查询、写入

NDB引擎

是一个集群存储引擎，支持事务数据保存在内存中

Memory引擎

使用表级锁 数据保存在内存中，不支持BLOB和TEXT等大字段 如果数据库重启，memory表会重建，如果有对应的从数据库表，数据也会掉失。适合存储临时数据的临时表Mermory使用hash索引，只支持表锁，并发性太差

Archive引擎

只支持INSERT和SELECT操作适合存储归档信息Archive引擎使用行锁来实现高并发的插入操作，不是事务安全的存储引擎，设计的目的是提供高速的插入和压缩

Mysql索引

如复合索引、前缀索引、唯一索引，都是属于非聚簇索引，其数据结构为B+树。

这个聚簇索引，在Mysql中是没有语句来另外生成的。在Innodb中，Mysql中的数据是按照主键的顺序来存放的。那么聚簇索引就是按照每张表的主键来构造一颗B+树，叶子节点存放的就是整张表的行数据。由于表里的数据只能按照一颗B+树排序，因此一张表只能有一个聚簇索引。

在Innodb中，聚簇索引默认就是主键索引。

InnoDB中10个线程，一个负责把缓冲区中的数据刷新到磁盘中，一个负责日志，四个负责读，四个负责写 



