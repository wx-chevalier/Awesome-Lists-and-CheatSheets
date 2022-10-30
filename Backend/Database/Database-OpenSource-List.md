# Database OpenSource List | 数据库相关开源工具索引

# Showcase

## RDB

- [MiniDataBase #Project# #Scratch#](https://github.com/msdeep14/MiniDataBase): A simple Relational Database using B+ Tree Index.

- [2016-chidb #Project#](https://people.cs.uchicago.edu/~adamshaw/papers/sigcse2016-chidb.pdf): Building a Simple Relational Database System from Scratch.

- [2017-SimpleDB #Project# #Scratch#](https://github.com/iamxpy/SimpleDB): UC Berkeley's Database class CS186: Implement A Simple Database Management System.

- [Database basics: writing a SQL database from scratch in Go #Series# #Scratch#](https://notes.eatonphil.com/database-basics.html): In this series we'll write a rudimentary database from scratch in Go.

- [2018-手写 SQL 编译器 #Scratch#](https://parg.co/oXJ): 因为工作关系，需要开发支持众多方言的 SQL 编辑器，所以复习了一下编译原理相关知识。相比编译原理专家，我们只需要了解部分编译原理即可实现 SQL 编辑器，所以这是一篇写给前端的编译原理文章。

- [2020-Let's Build a Simple Database #Series#](https://cstack.github.io/db_tutorial/): Writing a sqlite clone from scratch in C.

- [miniob #Project#](https://github.com/oceanbase/miniob): miniob 是 OceanBase 与华中科技大学联合开发的、面向"零"基础同学的数据库入门实践工具。 miniob 设计的目标是让同学们快速了解数据库并深入学习数据库内核，期望通过相关训练之后，能够对数据库内核各个模块的功能及其关联有所了解，并能够在 使用数据库时，设计出高效的 SQL 。miniob 面向的对象主要是在校学生，并且诸多模块都做了简化，比如不考虑并发操作。

## Distributed DB

- [LBADD #Project# #Scratch#](https://github.com/tomarrell/lbadd): An experimental, distributed SQL database.

- [CockroachDB #Project#](https://github.com/cockroachdb/cockroach): CockroachDB is a cloud-native distributed SQL database designed to build, scale, and manage modern, data-intensive applications.

- [Toydb #Project#](https://github.com/erikgrinaker/toydb): Distributed SQL database in Rust, written as a learning project. Most components are built from scratch.

- [rqlite #Project#](https://github.com/rqlite/rqlite): The lightweight, distributed relational database built on SQLite.

## Timeseries

- [2017-Writing a Time Series Database from Scratch](https://fabxc.org/tsdb/): While the current storage has served us well, I propose a newly designed storage subsystem that corrects for shortcomings of the existing solution and is equipped to handle the next order of scale.

- [2021-mandodb #Project#](https://github.com/chenjiandongx/mandodb): 🤔 A minimize Time Series Database, written from scratch as a learning project. 从零开始实现一个 TSDB

# Universal SQL Tools

## Client

### GUI

- [SQL Fiddle #Project#](http://sqlfiddle.com/): A tool for easy online testing and sharing of database problems and their solutions.

- [Dbeaver #Project#](https://dbeaver.io): Free multi-platform database tool for developers, SQL programmers, database administrators and analysts.

- [HeidiSQL #Project#](https://www.heidisql.com/): HeidiSQL is free software, and has the aim to be easy to learn. "Heidi" lets you see and edit data and structures from computers running one of the database systems MariaDB, MySQL, Microsoft SQL or PostgreSQL.

- [2020-Beekeeper Studio #Project#](https://github.com/beekeeper-studio/beekeeper-studio): Cross platform SQL editor and database management app for Windows, Linux, and Mac.

- [2020-Hue Editor #Project#](https://github.com/cloudera/hue): Open source SQL Query Assistant for Databases/Warehouses.

- [DataStation #Project#](https://github.com/multiprocessio/datastation): App to easily query, script, and visualize data from every database, file, and API.

### CMD

- [2018-q #Project#](https://github.com/harelba/q): q is a command line tool that allows direct execution of SQL-like queries on CSVs/TSVs (and any other tabular text files).

- [usql #Project#](https://github.com/knq/usql): usql is a universal command-line interface for working with SQL databases.

### Editor

- [2014-sqlpad #Project#](https://github.com/rickbergfalk/sqlpad): Web-based SQL editor run in your own private cloud. Supports MySQL, Postgres, SQL Server, Vertica, Crate, Presto, SAP HANA, and Cassandra.

- [2016-Falcon #Project#](https://github.com/plotly/falcon): Free, open-source SQL client for Windows and Mac 🦅

- [2022-SQL Father #Project#](https://github.com/liyupi/sql-father-backend-public): 快速生成 SQL 和模拟数据的网站（Java 后端），大幅提高开发测试效率！by 程序员鱼皮

## Analysis & Execution & Driver

- [queryparser #Project#](https://github.com/uber/queryparser): Parsing and analysis of Vertica, Hive, and Presto SQL. [Queryparser, an Open Source Tool for Parsing and Analyzing SQL](https://eng.uber.com/queryparser/)

- [sql-parser #Project#](https://github.com/dt-fe/sql-parser): Light and fast sql parser on browser.

- [2013-Druid #Project#](https://druid.apache.org/): 阿里巴巴数据库事业部出品，为监控而生的数据库连接池。

- [Apache Calcite #Project#](https://calcite.apache.org/): Industry-standard SQL parser,validator and JDBC driver.

- [2018-sqler #Project#](https://github.com/alash3al/sqler): write APIs using direct SQL queries with no hassle, let's rethink about SQL.

- [Zetasql #Project#](https://github.com/google/zetasql): ZetaSQL defines a language (grammar, types, data model, and semantics) as well as a parser and analyzer.

### Audit（审核平台）

- [2017-SQLAdvisor #Project#](https://github.com/Meituan-Dianping/SQLAdvisor): SQLAdvisor 是由美团点评公司技术工程部 DBA 团队(北京)开发维护的一个分析 SQL 给出索引优化建议的工具。它基于 MySQL 原生态词法解析，结合分析 SQL 中的 where 条件、聚合条件、多表 Join 关系 给出索引优化建议。目前 SQLAdvisor 在美团点评内部广泛应用，公司内部对 SQLAdvisor 的开发全面转到 github 上，开源和内部使用保持一致。

- [2019-Yearning #Project#](https://github.com/cookieY/Yearning): MYSQL 开源 SQL 语句审核平台。

## Migration & Backup & Transfer

- [FlyWay #Project#](https://github.com/flyway/flyway): Evolve your database schema easily and reliably across all your instances.

- [PingCAP-Loader #Project#](https://github.com/pingcap/docs-cn/blob/master/tools/loader.md)

- [2019-Refinery #Project#](https://github.com/rust-db/refinery): refinery makes running migrations for different databases as easy as possible.

- [Xtrabackup #Project#](https://github.com/percona/percona-xtrabackup): Open source hot backup tool for InnoDB and XtraDB databases.

## Benchmark

- [DBT2 #Project#](http://osdldbt.sourceforge.net/)

- [SysBench #Project#](http://sysbench.sourceforge.net/)

- [supersmack #Project#](http://vegan.net/tony/supersmack/)

- [mybench](http://jeremy.zawodny.com/mysql/mybench/)

# Relational Database

- [2019-MySQL #Project#](https://www.mysql.com/): The world's most popular open source database.

## StoreEngine

- [2021-Extensible-Storage-Engine #Project#](https://github.com/microsoft/Extensible-Storage-Engine): ESE is an embedded / ISAM-based database engine, that provides rudimentary table and indexed access. However the library provides many other strongly layered and and thus reusable sub-facilities as well: A Synchronization / Locking library, a Data-structures / STL-like library, an OS-abstraction layer, and a Cache Manager, as well the full blown…

## Sharding

- [Sharding-Sphere #Project#](https://gitee.com/Sharding-Sphere/sharding-sphere): Sharding-Sphere is an open-source ecosystem consisted of a set of distributed database middleware solutions, including 3 independent products, Sharding-JDBC, Sharding-Proxy & Sharding-Sidecar (todo).

- [2015-KingShard #Project#](https://github.com/flike/kingshard): kingshard is a high-performance proxy for MySQL powered by Go.

- [Atlas #Project#](https://github.com/Qihoo360/Atlas): A high-performance and stable proxy for MySQL, it is developed by Qihoo's DBA and infrastructure team.

- [2017-Vitess #Project#](https://github.com/vitessio/vitess): Vitess is a database clustering system for horizontal scaling of MySQL.

- [2019-Gaea #Project#](https://github.com/XiaoMi/Gaea): Gaea is a mysql proxy, it's developed by xiaomi b2c-systech team.

# Key-Value Database

- [LevelDB #Project#](https://github.com/google/leveldb): LevelDB is a fast key-value storage library written at Google that provides an ordered mapping from string keys to string values.

- [RocksDB #Project#](https://github.com/facebook/rocksdb): A library that provides an embeddable, persistent key-value store for fast storage.

- [2018-Tidis #Project#](https://github.com/yongman/tidis): Tidis is a Distributed NoSQL database, providing a redis-protocal api(string,list,hash,set,sorted-set), written in Go.

- [2019-Badger #Project#](https://github.com/dgraph-io/badger): BadgerDB is an embeddable, persistent and fast key-value (KV) database written in pure Go. It is the underlying database for Dgraph, a fast, distributed graph database. It's meant to be a performant alternative to non-Go-based key-value stores like RocksDB.

- [2020-terarkdb #Project#](https://github.com/bytedance/terarkdb): A RocksDB compatible KV storage engine with better performance.

- [immudb #Project#](https://github.com/codenotary/immudb): world’s fastest immutable database, built on a zero trust model.

# Graph Database

- [Cayley #Project#](https://github.com/cayleygraph/cayley): Cayley is an open-source graph inspired by the graph database behind Freebase and Google's Knowledge Graph.

- [Neo4j #Project#](https://github.com/neo4j/neo4j): Neo4j is the world’s leading Graph Database. It is a high performance graph store with all the features expected of a mature and robust database, like a friendly query language and ACID transactions.

- [Dgraph #Project#](https://dgraph.io/): Dgraph is a horizontally scalable and distributed graph database, providing ACID transactions, consistent replication and linearizable reads.

- [Nebula #Project#](https://github.com/vesoft-inc/nebula): A distributed, fast open-source graph database featuring horizontal scalability and high availability.

# TimeSeries

- [2013-InfluxDB #Project#](https://github.com/influxdata/influxdb): InfluxDB is an open source time series database with no external dependencies. It's useful for recording metrics, events, and performing analytics.

- [2017-timescaledb #Project#](https://github.com/timescale/timescaledb/): An open-source time-series database optimized for fast ingest and complex queries. Engineered up from PostgreSQL, packaged as an extension.

- [2018-M3 monorepo #Project#](https://github.com/m3db/m3): Distributed TSDB, Aggregator and Query Engine, Prometheus Sidecar, Metrics Platform

- [VictoriaMetrics #Project#](https://github.com/VictoriaMetrics/VictoriaMetrics): VictoriaMetrics is fast, cost-effective and scalable time series database.

- [TDengine #Project#](https://github.com/taosdata/TDengine): TDengine is an open-sourced big data platform under GNU AGPL v3.0, designed and optimized for the Internet of Things (IoT), Connected Cars, Industrial IoT, and IT Infrastructure and Application Monitoring.

- [2019-LinDB #Project#](https://github.com/lindb/lindb): LinDB is a scalable, high performance, high availability distributed time series database.

- [2019-VictoriaMetrics #Project#](https://github.com/VictoriaMetrics/VictoriaMetrics): Fast, cost-effective and scalable time series database, long-term remote storage for Prometheus.

- [2021-QuestDB #Project#](https://github.com/questdb/questdb): QuestDB is a distributed, high-performance, fully-distributed, high-availability, fully-scalable, and highly-available time series database.

# NewSQL

- [FoundationDB #Project#](https://github.com/apple/foundationdb): FoundationDB is a distributed database designed to handle large volumes of structured data across clusters of commodity servers.

# P2P Database

- [OrbitDB #Project#](https://github.com/orbitdb/orbit-db): Peer-to-Peer Databases for the Decentralized Web.

- [Scuttlebot #Project#](http://scuttlebot.io): Scuttlebot is an open source peer-to-peer log store used as a database, identity provider, and messaging system. It features global replication, file-syncronization, and end-to-end encryption.
