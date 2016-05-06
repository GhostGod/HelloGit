#Redis

常用的数据类型
- String
- Hash
- List
- Set
- Sorted set

- 所用语言：C/C++
- 特点：运行异常快
- 使用许可： BSD
- 协议：类 Telnet
- 有硬盘存储支持的内存数据库，
- 但自2.0版本以后可以将数据交换到硬盘（注意， 2.4以后版本不支持该特性！）
- Master-slave复制（见编注3）
- 虽然采用简单数据或以键值索引的哈希表，但也支持复杂操作，例如 ZREVRANGEBYSCORE。
- INCR & co （适合计算极限值或统计数据）
- 支持 sets（同时也支持 union/diff/inter）
- 支持列表（同时也支持队列；阻塞式 pop操作）
- 支持哈希表（带有多个域的对象）
- 支持排序 sets（高得分表，适用于范围查询）
- Redis支持事务
- 支持将数据设置成过期数据（类似快速缓冲区设计）
- Pub/Sub允许用户实现消息机制
 

最佳应用场景：适用于数据变化快且数据库大小可遇见（适合内存容量）的应用程序。

例如：股票价格、数据分析、实时数据搜集、实时通讯。

（编注3：Master-slave复制：如果同一时刻只有一台服务器处理所有的复制请求，这被称为 Master-slave复制，通常应用在需要提供高可用性的服务器集群


# 8 种 NoSQL 数据库系统对比

http://blog.jobbole.com/1344/

# 其他redis介绍

http://blog.sina.com.cn/s/blog_5a15b7d10101gizu.html
