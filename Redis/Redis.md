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
4. 进入／usr/local/redis-4.0.0,进行编译，命令：make
5. 进入redis的src目录，进行安装，命令：make install

### Redis服务启动与停止

## 数据类型

## 常用命令

## 在Java中操作Redis

