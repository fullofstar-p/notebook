# Redis基础

## 什么是 Redis？

Redis是一个基于**内存**的key-value结构数据库

- 基于内存存储，读写性能高
- 适合存储热点数据（热点商品、咨询、新闻）
- 企业应用广泛

## Redis入门

### Redis简介

Redis is an open source (BSD licensed), in-memory data structure store, used as a database,cache,and
message broker，翻译为：Redis是一个开源的内存中的数据结构存储系统，它可以用作：数据库、缓存和消息中间件。官网：https://redis.io

Redis是用C语言开发的一个开源的高性能键值对（key-value）数据库，官方提供的数据是可以达到100000＋的QPS（每秒内查询次数）。它存储的value类型比较丰富，也被称为结构化的NoSql数据库。

NoSql (Not Only SQL)，不仅仅是SQL，泛指**非关系型数据库**。NoSql数据库并不是要取代关系型数据库，而是关系型数据库的补充。

- 关系型数据库(RDBMS)
  - Mysql
  - Oracle
  - DB2
  - SQLServer
- 非关系型数据库（NoSql)
  - Redis
  - Mongo db
  - MemCached

**Redis应用场景**

- 缓存
- 任务队列
- 消息队列
- 分布式锁

### Redis下载与安装

Redis安装包分为windos版和Linux版：

- Windows版下载地址：https://github.com/microsoftarchive/redis/releases
- Linux版下载地址：https://download.redis.io/releases/

在Linux系统安装Redis步骤：

1. 将Redis安装包上传到Linux
2. 解压安装包，命令：tar -zxvf redis-4.0.0.tar.gz -C /usr/local
3. 安装Redis的依赖环境gcc，命令：yum install gcc-c++
4. 进入 /usr/local/redis-4.0.0,进行编译，命令：make
5. 进入redis的src目录，进行安装，命令：make install

### Redis服务启动与停止

Linux中redis服务启动，可以使用`redis-server`,默认端口为6379

## 数据类型

**介绍**

Redis存储的是key-value结构的数据,其中key是字符串类型,value有5种常用的数据类型

- 字符串 string
- 哈希 hash
- 列表 list
- 集合 set
- 有序集合 sorted set

**Redis 5种常用数据类型**

![](images/Snipaste_2024-11-03_22-35-04.png)

## 常用命令

### 字符串 string 操作命令

```
SET key value				设置指定key的值
GET key						获取指定key的值
SETEX key seconds value		设置指定key的值，并将key的过期时间设为 seconds 秒
SETNX key value				只有在 key 不存在时设置 key的值
更多命令可以参考Redis中文网：https://www.redis.net.cn
```

### 哈希 hash 操作命令

Redis hash是一个string类型的 field 和 value 的映射表，hash特别适合用于存储对象，常用命令

```
HSET key field value			将哈希表 key 中的字段 field 的值设为 value
HGET key field					获取存储在哈希表中指定字段的值
HDEL key field					删除存储在哈希表中的指定字段
HKEYS key						获取哈希表中所有字段
HVALS key						获取哈希表中所有值
HGETALL key						获取在哈希表中指定key的所有字段和值
```

### 列表 list 操作命令

Redis 列表是简单的字符串列表，按照插入顺序排序，常用命令

```
LPUSH key value1 [value2]		将一个或多个值插入到列表头部
LRANGE key start stop			获取列表指定范围内的元素
RPOP key						移除并获取列表最后一个元素
LLEN key						获取列表长度
BRPOP key1 [key2 ] timeout		移出并获取列表的最后一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止
```

### 集合 set 操作命令

Redis set 是string类型的无序集合。集合成员是唯一的，这就意味着集合中不能出现重复的数据，常用命令

```
SADD key member1 [member2]				向集合添加一个或多个成员
SMEMBERS key							返回集合中的所有成员
SCARD key								获取集合的成员数
SINTER key1[key2]						返回给定所有集合的交集
SUNION key1 [key2]						返回所有给定集合的并集
SDIFF key1 [key2]						返回给定所有集合的差集
SREM key member1 [member2]				移除集合中一个或多个成员
```

### 有序集合 sorted set 操作命令

Redis sorted set 有序集合是string 类型元素的集合，且不允许重复的成员。每个元素都会关联一个double类型的分数(score)。redis正是通过分数来为集合中的成员进行从小到大排序。有序集合的成员是唯一的，但分数却可以重复。常用命令

```
ZADD key score1 member1 [score2 member2]		向有序集合添加一个或多个成员，或者更新已存在成员的分数
ZRANGE key start stop [WITHSCORES]				通过索引区间返回有序集合中指定区间内的成员
ZINCRBY key increment member					有序集合中对指定成员的分数加上增量increment  
ZREM key member [member..…]						移除有序集合中的一个或多个成员
```

### 通用命令

```
KEYS pattern		查找所有符合给定模式（pattern）的 key
EXISTS key			检查给定 key 是否存在
TYPE key			返回key 所储存的值的类型
TTL key				返回给定 key的剩余生存时间（TTL, time to live)，以秒为单位
DEL key				该命令用于在 key存在是删除 key
```

## 在Java中操作Redis

**介绍**

Redis 的Java客户端很多，官方推荐的有三种：

- Jedis
- Lettuce
- Redisson

Spring 对 Redis客户端进行了整合，提供了 Spring Data Redis，在Spring Boot项目中还提供了对应的Starter，即spring-boot-starter-data-redis

**Jedis**

Jedis的maven坐标：
```
<dependency>
    <groupld>redis.clients</groupld>
    <artifactld>jedis</artifactld>
    <version>2.8.0</version>
</dependency>
```

使用Jedis操作Redis的步骤：

1. 获取连接
2. 执行操作
3. 关闭连接

**Spring Data Redis**

在Spring Boot项目中，可以使用Spring Data Redis来简化Redis操作，maven坐标：

```
<dependency>
	<groupld>org.springframework.boot</groupld>
	<artifactld>spring-boot-starter-data-redis</artifactld>
</dependency>
```

Spring Data Redis中提供了一个高度封装的类：RedisTemplate，针对jedis客户端中大量api进行了归类封装，将同一类型操作封装为operation接口，具体分类如下：

- ValueOperations：简单K-V操作
- SetOperations: set类型数据操作
- ZSetOperations: zset类型数据操作
- HashOperations：针对map类型的数据操作
- ListOperations：针对list类型的数据操作

## Spring Cache

### Spring Cache介绍

**Spring Cache**是一个框架，实现了基于注解的缓存功能，只需要简单地加一个注解，就能实现缓存功能。
Spring Cache提供了一层抽象，底层可以切换不同的cache实现。具体就是通过**CacheManager**接口来统一不同的缓存技术。
CacheManager是Spring提供的各种缓存技术抽象接口。

**针对不同的缓存技术需要实现不同的CacheManager:**

| CacheManager        | 描述                               |
| ------------------- | ---------------------------------- |
| EhCacheCacheManager | 使用EhCache作为缓存技术            |
| GuavaCacheManager   | 使用Google的GuavaCache作为缓存技术 |
| RedisCacheManager   | 使用Redis作为缓存技术              |

### Spring Cache常用注解

| 注解           | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| @EnableCaching | 开启缓存注解功能                                             |
| @Cacheable     | 在方法执行前spring查看缓存中是否有数据，如果有数据，则直接返回缓存数据；<br/>若没有数据，调用方法并将方法返回值放到缓存中 |
| @CachePut      | 将方法的返回值放到缓存中                                     |
| @CacheEvict    | 将一条或多条数据从缓存中删除                                 |

在spring boot项目中，使用缓存技术只需在项目中导入相关缓存技术的依赖包，并在启动类上使用
@EnableCaching开启缓存支持即可。
例如，使用Redis作为缓存技术，只需要导入Spring data Redis的maven坐标即可。

### Spring Cache使用方式

**在Spring Boot项目中使用Spring Cache的操作步骤（使用redis缓存技术）**:

1. 导入maven坐标
   spring-boot-starter-data-redis、 

2. 配置application.yml

    ```
   spring:
   	cache:
   		redis:
   			time-to-live:1800000 ＃设置缓存有效期
   ```

3. 在启动类上加入＠EnableCaching注解，开启缓存注解功能

4. 在Controller的方法上加入＠Cacheable、@CacheEvict等注解，进行缓存操作

  
