# MySQL主从复制

## 介绍

MySQL主从复制是一个异步的复制过程，底层是基于Mysql数据库自带的**二进制日志**功能。就是一台或多台MySQL数据库（slave，即**从库**）从另一台MySQL数据库（master，即**主库**）进行日志的复制然后再解析日志并应用到自身，最终实现**从库**的数据和**主库**的数据保持一致。MySQL主从复制是MySQL数据库自带功能，无需借助第三方工具。

MySQL复制过程分成三步：

- master将改变记录到二进制日志（binary log)
- slave将master的binary log拷贝到它的中继日志（relay log)
- slave重做中继日志中的事件，将改变应用到自己的数据库中
  

## 配置-前置条件

提前准备好两台服务器，分别安装Mysql并启动服务成功

- 主库Master 192.168.138.100
- 从库Slave 192.168.138.101

## 配置-主库Master

1. 修改Mysql数据库的配置文件/etc/my.cnf

   ```
   [mysqld]
   log-bin=mysql-bin	#［必须］启用二进制日志
   server-id=100		#［必须］服务器唯一ID
   ```

2. 重启Mysql服务

   ```
   systemctl restart mysqld
   ```

3. 第三步：登录Mysql数据库，执行下面SQL

   ```
   GRANT REPLICATION SLAVE ON *.* to 'xiaoming'@'%' identified by 'Root@123456';
   ```

   注：上面SQL的作用是创建一个用户**xiaoming**，密码为**Root@123456**，并且给xiaoming用户授予**REPLICATION SLAVE** 权限。常用于建立复制时所需要用到的用户权限，也就是slave必须被master授权具有该权限的用户，才能通过该用户复制。

4. 登录Mysql数据库，执行下面SQL，记录下结果中File和Position的值

   ```
   show master status;
   ```

   注：上面SQL的作用是查看Master的状态，执行完此SQL后不要再执行任何操作

## 配置-从库Slave

1. 修改Mysql数据库的配置文件/etc/my.cnf

   ```
   [mysqld]
   server-id=101 #［必须］服务器唯一ID
   ```

2. 重启Mysql服务

   ```
   systemctl restart mysqld
   ```

3. 登录Mysql数据库，执行下面SQL

   ```
   change master to master_host='192.168.138.128',master_user='xiaoming',master_password='Root@123456',master_log_file='mysql-bin.000001',master_log_pos=441;
   
   start slave;
   ```

4. 登录Mysql数据库，执行下面SQL，查看从数据库的状态

   ```
   show slave status;
   ```

## 读写分离案例

### 背景

面对日益增加的系统访问量，数据库的吞吐量面临着巨大瓶颈。对于同一时刻有大量并发读操作和较少写操作类型的应用系统来说，将数据库拆分为主库和从库，主库负责处理事务性的增删改操作，从库负责处理查询操作，能够有效的避免由数据更新导致的行锁，使得整个系统的查询性能得到极大的改善。

### Sharding-JDBC介绍

Sharding-JDBC定位为轻量级Java框架，在Java的JDBC层提供的额外服务。 它使用客户端直连数据库，以jar包形式提供服务，无需额外部署和依赖，可理解为增强版的JDBC驱动，完全兼容JDBC和各种ORM框架。
使用Sharding-JDBC可以在程序中轻松的实现数据库读写分离。

- 适用于任何基于JDBC的ORM框架，如：JPA, Hibernate, Mybatis, Spring JDBC Template或直接使用JDBC。
- 支持任何第三方的数据库连接池，如：DBCP, C3P0, BoneCP, Druid, HikariCP等。
- 支持任意实现JDBC规范的数据库。目前支持MySQL,Oracle,SQLServer,PostgreSQL以及任何遵循SQL92标准的数据库。

```
<dependency>
    <groupId>org. apache. shardingsphere</groupId>
    <artifactId>sharding-jdbc-spring-boot-starter</artifactId>
    <version>4.0.0-RC1</version>
</dependency>
```
