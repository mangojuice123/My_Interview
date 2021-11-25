- [一致性哈希算法](#一致性哈希算法)
- [缓存穿透](#缓存穿透)
- [缓存击穿](#缓存击穿)
- [缓存雪崩](#缓存雪崩)
- [缓存预热](#缓存预热)
- [缓存降级](#缓存降级)
- [常见问题](#常见问题)
  - [讲讲 Redis 的过期策略及内存淘汰机制](#讲讲-redis-的过期策略及内存淘汰机制)
  - [讲讲 Redis 和数据库双写一致性](#讲讲-redis-和数据库双写一致性)
  - [Redis 支持哪几种数据类型？](#redis-支持哪几种数据类型)
  - [RDB 和 AOF 的使用场景是什么？](#rdb-和-aof-的使用场景是什么)
- [公司](#公司)


</br></br>


# 一致性哈希算法
- 减轻服务器集群带来的数据迁移代价。
- 虚拟节点技术。


# 缓存穿透
- 缓存穿透是指用户请求的数据在缓存中不存在，即没有命中缓存，同时在数据库中也不存在，导致用户每次请求该数据都要去数据库中查询一遍。
- 解决方案：
  - 使用布隆过滤器。


# 缓存击穿
- 某一个时刻，某个热点的 key 失效。


# 缓存雪崩
- 某一个时刻，出现了**大规模**的 key 失效，导致大量的请求直接打在了数据库上面，导致数据库压力过大而宕机。
- 解决方案：
  - 事前：
    - 均匀过期：设置不同的过期时间，让缓存的时间尽量均匀；
    - 分级缓存：第一级缓存失效的基础上，访问二级缓存，每一级缓存的失效时间都不同；
    - 热点数据缓存永不过期：
      - 物理不过期：针对热点 key 不设置过期时间；
      - 逻辑不过期：把过期时间存在 key 对应的 value 里，如果发现要过期了，通过后台线程进行缓存的构建；
    - `主从 + 哨兵` 构建 Redis 集群避免 Redis 全盘崩溃的情况。
  - 事中：
    - 使用互斥锁或队列限制读写缓存的线程数量。这种方式会阻塞其他线程，造成系统的吞吐量下降。
    - 使用熔断机制，限流降级。
  - 事后：
    - 开启 Redis 持久化机制，尽快恢复缓存数据。


# 缓存预热
- 提前将相关的缓存数据加载到缓存系统中。


# 缓存降级
- 在缓存失效或者服务器挂掉的情况下，不去访问数据库，直接返回默认数据或访问服务的内存数据。


</br></br>


# 常见问题
## 讲讲 Redis 的过期策略及内存淘汰机制
答：
- Redis 采用的是定期删除 + 惰性删除策略。
  - 定期删除 + 惰性删除：默认每隔 100 ms 抽查是否有过期的 key，这样会导致有很多 key 到期但是没有删除。当获取某个 key 时，检查是否过期，过期则删除（惰性删除策略）。
- 内存淘汰机制：LRU。


## 讲讲 Redis 和数据库双写一致性
答：
- 先更新数据库，再更新缓存。


## Redis 支持哪几种数据类型？
答：
- Redis 数据库里面的每个 key-value pair 都是由对象组成的。
- 数据库的键总是一个 String object。
- 数据库的值可以是五种对象中的一种：
  - String：存储 key-value 键值对；
  - List：最新列表功能（`lpush` 往列表里插入新的元素，然后通过 `lrange` 读取最新的列表）；
  - Hash：购物车（`hset [用户] [商品] [数量]`）；
  - Set：利用交集（`sinter`）等功能，计算共同喜好等；
  - Sorted Set：和 List 不同的是可以实现动态的排序，用作排行榜等。


## RDB 和 AOF 的使用场景是什么？
答：
- RDB (Redis Database): The RDB persistence performs point-in-time snapshots of your dataset at specified intervals.
  - RDB is a very compact single-file point-in-time representation of your Redis data.
  - 体积小，内容全，非常适合充当 backup。
- AOF (Append Only File):The AOF persistence logs every write operation received by the server, that will be played again at server startup, reconstructing the original dataset. 
  - Using AOF Redis is much more durable: you can have different fsync policies: no fsync at all, fsync every second, fsync at every query.
  - 最大程度减少数据丢失的可能。


</br></br>


# 公司
- 2021-11 小红书
- 2021-10 字节跳动