# MySQL CheatSheet | MySQL 配置与性能优化实践清单

MySQL is a full-featured open-source relational database management system (RDBMS) that was originally built by MySQL AB and currently owned by Oracle Corporation. It stores data in tables that are grouped into a database, uses Structured Query Language (SQL) to access data and such commands as ‘SELECT’, ‘UPDATE’, ‘INSERT’ and ‘DELETE’ to manage it. Related information can be stored in different tables, but the usage of JOIN operation allows you to correlate it, perform queries across various tables and minimize the chance of data duplication.

MySQL is compatible with nearly all operating systems, namely Windows, Linux, Unix, Apple, FreeBSD and many others. It supports various storage engines, like InnoDB (it is the default one), Federated, MyISAM, Memory, CSV, Archive, Blackhole and Merge.

本清单参考了 [MySQL Command Line Cheatsheet](https://gist.github.com/hofmannsven/9164408)、[MySQL 5.7 Reference Manual](https://parg.co/UpB)，更多 MySQL 的学习资料参考 [MySQL 学习与资料索引]()。此外，本文中涉及的 SQL 语句可以前往 [SQLFiddle](http://sqlfiddle.com/#!9/60f53) 查看完整的 SQL 语句，也可以前往 [SQL Teaching](https://www.sqlteaching.com/) 进行交互式基础语法学习。

对于 SQL 方面的知识，请参阅 [SQL CheatSheet](https://parg.co/mtZ)。

```sh
# 启动本地的 MySQL 实例
$ docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag

# 将 MySQL 端口映射出来
$ docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -p 3306:3306 -d mysql:tag

# 允许启动的其他容器中使用 MySQL
$ docker run --name some-app --link some-mysql:mysql -d application-that-uses-mysql

# 启动本地 MySQL 客户端并且连接到目标
$ docker run -it --link some-mysql:mysql --rm mysql sh -c 'exec mysql -h"$MYSQL_PORT_3306_TCP_ADDR" -P"$MYSQL_PORT_3306_TCP_PORT" -uroot -p"$MYSQL_ENV_MYSQL_ROOT_PASSWORD"'

# 将 MySQL 镜像作为客户端使用，连接到远端的数据库
$ docker run -it --rm mysql mysql -hsome.mysql.host -usome-mysql-user -p
```

```sql
--- 老版本中更新 Root 用户信息
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;
 FLUSH PRIVILEGES;

--- 5.7 之后版本
update user set authentication_string=password('YOURSUPERSECRETPASSWORD') where user='root';
```

# 配置与管理

## 权限管理

MySQL 的安装过程不在此赘述，其自带了命令行工具进行管理：

```sh
# Prompt for password / 交互式登录
$ mysql -u [username] -p

$ mysql -u [username] -p [database]
```

登录完毕后可以查看并操作数据库：

```sh
# 展示所有数据库
mysql> show databases;

# 创建新的数据库
mysql> create database [database];

# 选择数据库
mysql> use [database];
```

```sh
# 创建用户并且分配权限
mysql> CREATE USER 'finley'@'%' IDENTIFIED BY 'some_pass';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'finley'@'%'
    ->     WITH GRANT OPTION;

# 修改用户密码
use mysql;
update user set password=PASSWORD("mynewpassword") where User='root';
flush privileges;
```

## 信息检索

```sql
SELECT
  TABLE_NAME, table_rows, data_length, index_length,
  round(((data_length + index_length) / 1024 / 1024),2) 'Size in MB'
FROM information_schema.TABLES
WHERE TABLE_NAME = 'r_case_info' and TABLE_TYPE='BASE TABLE'
ORDER BY data_length DESC;
```

# 数据查询与操作

## 数据类型

![group](https://user-images.githubusercontent.com/5803001/44440908-d6ddc580-a5fc-11e8-9701-096e3b5b7be0.jpg)

## 时间与日期

MySQL 中支持 date 和 datetime、timestamp 等时间类型，其中 date 与 datetime 都是时区无关，timestamp 会跟随设置的时区变化而变化，而 datetime 保存的是绝对值不会变化。占用存储空间不同。timestamp 储存占用 4 个字节，datetime 储存占用 8 个字节。

- 可表示的时间范围不同。timestamp 可表示范围:1970-01-01 00:00:00~2038-01-09 03:14:07，datetime 支持的范围更宽 1000-01-01 00:00:00 ~ 9999-12-31 23:59:59

- 索引速度不同。timestamp 更轻量，索引相对 datetime 更快。

MySQL 仅允许插入无时区的时间格式字符串，当我们插入到 DATETIME 类型时，其会保存字面信息了；如果插入到 TIMESTAMP 类型，MySQL 首先会将其根据当前时区转化为 UTC 时间戳存储，在用户查询的时候则会再从 UTC 时区转化为数据库当前时区。DATETIME 与 TIMESTAMP 在使用上并无太大差异，仅当数据库时区发生变化时，其读取值会发生变化。MySQL 也提供了丰富的[时间与日期函数](http://dev.mysql.com/doc/refman/5.1/en/date-and-time-functions.html#function_month)，sysdate() 和 now() 都可以使用当前时间值，其中 sysdate 表示实时的系统时间，不过其有可能导致主库和从库执行时返回值不一样，导致主从数据库不一致。

```sh
mysql> select now(), curdate(), sysdate(), curtime() \G;
*************************** 1. row ***********************
    now(): 2013-01-17 13:07:53
curdate(): 2013-01-17
sysdate(): 2013-01-17 13:07:53
curtime(): 13:07:53
```

```sql
// 获取事件的年与月
GROUP BY YEAR(record_date), MONTH(record_date)

// 根据固定的时间格式排序
GROUP BY DATE_FORMAT(record_date, '%Y%m')

// 获取 Unix_Stamp
SELECT UNIX_TIMESTAMP('1970-01-01 12:00:00');
```

我们可以使用 TIMESTAMPDIFF 与 DATEDIFF 计算两个日期时间的差：

```sql
--- FRAC_SECOND、SECOND、MINUTE、HOUR、DAY、WEEK、MONTH、QUARTER或 YEAR
SELECT TIMESTAMPDIFF(DAY,'2012-10-01','2013-01-13');

--- 传入两个日期函数，比较的DAY天数
SELECT DATEDIFF('2013-01-13','2012-10-01');
```

# Tuning | 性能调优

MySQL 中常见的性能问题，可能是有如下类型：

- CPU 过载，慢查询，OPTIMZE TABLE
- 内存使用问题，内存相关参数配置不合理
- 磁盘 IO，Buffer pool 命中率；慢查询；redo, undo, data 分开存放
- 网络问题，非专有网络，网络路由
- 表及查询语句问题，主要的查询性能问题：全表扫描 临时表 排序 FileSort

常用定位问题的方法则有：

- 分析状态变量
- MySQL Slow query log
- EXPLAIN 命令查看执行计划
- profiling 查看执行过耗时
- show full processlist
- show engine innodb status
- 查看 innodb 系统表

## 配置

- innodb_buffer_pool_size, 一般设置为机器内存的 50%左右(实践经验)

- innodb_buffer_pool_instances, 5.6 及 5.7，可设置为 8-16 个

- innodb_log_file_size
  一般设置为 25% 的 buffer pool size 大小
- innodb_flush_log_at_trx_commit
  要求高可靠性，设置为 1。不要求高可靠性，可设置为 0 或 2.
- sync_binlog
  Binlog 的可靠性设置，高可靠性设置为 1，但对于性能影响比较大。如果已经配置了 Slave，这个参数可设置为 0
- innodb_flush_method
  Linux 下设置为 O_DIRECT

- innodb_thread_concurrency
  (Cores \* 2) + (# Disks)
- skip_name_resolve
  使用直接 IP 方式，避免 DNS 解析
- innodb_io_capacity，innodb_io_capacity_max
  需要根据你的磁盘的 IOPS 处理能力进行相应设置。
  innodb_io_capacity~= IOPS
- query_cache_type
  是否使用 Query Cache，对于读/写，80%+/20%-的应用可考虑打开。写入请求过多的应用，需要关闭，不然反而影响性能。
- tmp_table_size/ max_heap_table_size
  通过查看状态变量 Created_tmp_disk_tables 及 Created_tmp_tables，决定是否合适

## explain | 分析

在日常工作中，我们会有时会开慢查询去记录一些执行时间比较久的 SQL 语句，找出这些 SQL 语句并不意味着完事了，些时我们常常用到 explain 这个命令来查看一个这些 SQL 语句的执行计划，查看该 SQL 语句有没有使用上了索引，有没有做全表扫描，这都可以通过 explain 命令来查看。

```sh
mysql> explain select * from (select * from ( select * from t1 where id=2602) a) b;
+----+-------------+------------+--------+-------------------+---------+---------+------+------+-------+
| id | select_type | table      | type   | possible_keys     | key     | key_len | ref  | rows | Extra |
+----+-------------+------------+--------+-------------------+---------+---------+------+------+-------+
|  1 | PRIMARY     | <derived2> | system | NULL              | NULL    | NULL    | NULL |    1 |       |
|  2 | DERIVED     | <derived3> | system | NULL              | NULL    | NULL    | NULL |    1 |       |
|  3 | DERIVED     | t1         | const  | PRIMARY,idx_t1_id | PRIMARY | 4       |      |    1 |       |
+----+-------------+------------+--------+-------------------+---------+---------+------+------+-------+
```

当我们的查询语句包含了多个 Select 语句时，explain 会依次返回每个子查询的信息，其中 select_type 就是表示每个 select 子句的类型：

- SIMPLE: 简单 SELECT,不使用 UNION 或子查询等

- PRIMARY: 查询中若包含任何复杂的子部分,最外层的 select 被标记为 PRIMARY

- UNION: UNION 中的第二个或后面的 SELECT 语句

- DEPENDENT UNION: UNION 中的第二个或后面的 SELECT 语句，取决于外面的查询

- UNION RESULT: UNION 的结果

- SUBQUERY: 子查询中的第一个 SELECT

- DEPENDENT SUBQUERY: 子查询中的第一个 SELECT，取决于外面的查询

- DERIVED: 派生表的 SELECT, FROM 子句的子查询

- UNCACHEABLE SUBQUERY: 一个子查询的结果不能被缓存，必须重新评估外链接的第一行

type 表示 MySQL 在表中找到所需行的方式，又称“访问类型”。常用的类型有：ALL, index, range, ref, eq_ref, const, system, NULL（从左到右，性能从差到好）：

- ALL：Full Table Scan，MySQL 将遍历全表以找到匹配的行

- index: Full Index Scan，index 与 ALL 区别为 index 类型只遍历索引树

- range:只检索给定范围的行，使用一个索引来选择行

- ref: 表示上述表的连接匹配条件，即哪些列或常量被用于查找索引列上的值

- eq_ref: 类似 ref，区别就在使用的索引是唯一索引，对于每个索引键值，表中只有一条记录匹配，简单来说，就是多表连接中使用 primary key 或者 unique key 作为关联条件

- const, system: 当 MySQL 对查询某部分进行优化，并转换为一个常量时，使用这些类型访问。如将主键置于 where 列表中，MySQL 就能将该查询转换为一个常量,system 是 const 类型的特例，当查询的表只有一行的情况下，使用 system

- NULL: MySQL 在优化过程中分解语句，执行时甚至不用访问表或索引，例如从一个索引列里选取最小值可以通过单独索引查找完成。

possible_keys, 指出 MySQL 能使用哪个索引在表中找到记录，查询涉及到的字段上若存在索引，则该索引将被列出，但不一定被查询使用。key 列显示 MySQL 实际决定使用的键（索引），如果没有选择索引，键是 NULL。要想强制 MySQL 使用或忽视 possible_keys 列中的索引，在查询中使用 FORCE INDEX、USE INDEX 或者 IGNORE INDEX。key_len 表示索引中使用的字节数，可通过该列计算查询中使用的索引的长度（key_len 显示的值为索引字段的最大可能长度，并非实际使用长度，即 key_len 是根据表定义计算而得，不是通过表内检索出的）；不损失精确性的情况下，长度越短越好。

最后的 Extra 列包含 MySQL 解决查询的详细信息,有以下几种情况：

- Using where: 列数据是从仅仅使用了索引中的信息而没有读取实际的行动的表返回的，这发生在对表的全部的请求列都是同一个索引的部分的时候，表示 mysql 服务器将在存储引擎检索行后再进行过滤

- Using temporary: 表示 MySQL 需要使用临时表来存储结果集，常见于排序和分组查询

- Using filesort: MySQL 中无法利用索引完成的排序操作称为“文件排序”

- Using join buffer：改值强调了在获取连接条件时没有使用索引，并且需要连接缓冲区来存储中间结果。如果出现了这个值，那应该注意，根据查询的具体情况可能需要添加索引来改进性能。

- Impossible where：这个值强调了 where 语句会导致没有符合条件的行。

- Select tables optimized away：这个值意味着仅通过使用索引，优化器可能仅从聚合函数结果中返回一行

## Security | 安全

### SQL Injection

# Links

- [ ] https://www.jianshu.com/p/486a514b0ded
