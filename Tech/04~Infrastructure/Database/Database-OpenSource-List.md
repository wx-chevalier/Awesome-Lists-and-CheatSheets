# Database OpenSource List | 数据库相关开源工具索引

# Showcases

## RDB

- [MiniDataBase ![code](https://ng-tech.icu/assets/code.svg) #Scratch#](https://github.com/msdeep14/MiniDataBase): A simple Relational Database using B+ Tree Index.

- [2016~chidb ![code](https://ng-tech.icu/assets/code.svg)](https://people.cs.uchicago.edu/~adamshaw/papers/sigcse2016-chidb.pdf): Building a Simple Relational Database System from Scratch.

- [2017~SimpleDB ![code](https://ng-tech.icu/assets/code.svg) #Scratch#](https://github.com/iamxpy/SimpleDB): UC Berkeley's Database class CS186: Implement A Simple Database Management System.

- [Database basics: writing a SQL database from scratch in Go #Series# #Scratch#](https://notes.eatonphil.com/database-basics.html): In this series we'll write a rudimentary database from scratch in Go.

- [2018~db_tutorial #Series# #Scratch#](https://github.com/cstack/db_tutorial): Writing a sqlite clone from scratch in C.

- [2018~手写 SQL 编译器 #Scratch#](https://parg.co/oXJ): 因为工作关系，需要开发支持众多方言的 SQL 编辑器，所以复习了一下编译原理相关知识。相比编译原理专家，我们只需要了解部分编译原理即可实现 SQL 编辑器，所以这是一篇写给前端的编译原理文章。

- [2018~Freedom ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/alchemystar/Freedom)](https://github.com/alchemystar/Freedom): 在阅读了大量关于数据库的资料后，笔者情不自禁产生了一个造数据库轮子的想法。来验证一下自己对于数据库底层原理的掌握是否牢靠。在笔者的 github 中给这个 database 起名为 Freedom。

- [2015-Lealone ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/lealone/Lealone)](https://github.com/lealone/Lealone): Lealone 是一个兼具 RDBMS、NoSQL 优点的面向微服务和 OLTP/OLAP 场景的单机与分布式关系数据库

- [2020~bustub ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/cmu-db/bustub)](https://github.com/cmu-db/bustub): BusTub is a relational database management system built at Carnegie Mellon University for the Introduction to Database Systems (15-445/645) course. This system was developed for educational purposes and should not be used in production environments.

- [2020~cstack/db_tutorial ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/cstack/db_tutorial)](https://github.com/cstack/db_tutorial): Writing a sqlite clone from scratch in C.

- [miniob ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/oceanbase/miniob): miniob 是 OceanBase 与华中科技大学联合开发的、面向"零"基础同学的数据库入门实践工具。miniob 设计的目标是让同学们快速了解数据库并深入学习数据库内核，期望通过相关训练之后，能够对数据库内核各个模块的功能及其关联有所了解，并能够在 使用数据库时，设计出高效的 SQL 。miniob 面向的对象主要是在校学生，并且诸多模块都做了简化，比如不考虑并发操作。

- [2022~mini-lsm ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/skyzh/mini-lsm)](https://github.com/skyzh/mini-lsm): A tutorial of building an LSM-Tree storage engine in a week! (WIP)

## Distributed DB

- [LBADD ![code](https://ng-tech.icu/assets/code.svg) #Scratch#](https://github.com/tomarrell/lbadd): An experimental, distributed SQL database.

- [CockroachDB ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/cockroachdb/cockroach): CockroachDB is a cloud-native distributed SQL database designed to build, scale, and manage modern, data-intensive applications.

- [Toydb ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/erikgrinaker/toydb): Distributed SQL database in Rust, written as a learning project. Most components are built from scratch.

- [rqlite ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/rqlite/rqlite): The lightweight, distributed relational database built on SQLite.

- [2023~tontinton/dbeel ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/tontinton/dbeel)](https://github.com/tontinton/dbeel): dbeel is an attempt to learn modern database architecture. The best one-liner to describe the db is: A distributed thread-per-core document database written in rust.

## Timeseries

- [2017~Writing a Time Series Database from Scratch](https://fabxc.org/tsdb/): While the current storage has served us well, I propose a newly designed storage subsystem that corrects for shortcomings of the existing solution and is equipped to handle the next order of scale.

- [2021~mandodb ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/chenjiandongx/mandodb): 🤔 A minimize Time Series Database, written from scratch as a learning project. 从零开始实现一个 TSDB

# Relational Database

- [2019~MySQL ![code](https://ng-tech.icu/assets/code.svg)](https://www.mysql.com/): The world's most popular open source database.

## Query Engine

- [2022~Quokka ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/marsupialtail/quokka)](https://github.com/marsupialtail/quokka): Quokka is an open-source push-based vectorized query engine. Inspired by recent high performance database designs at Snowflake, DuckDB and SingleStore etc., it is meant to be much more performant than blocking-shuffle based alternatives like SparkSQL. On test TPC-H queries, Quokka currently is often several times faster than open-source SparkSQL and an order of magnitude faster than Dask.

## StoreEngine

- [2021~Extensible-Storage-Engine ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/microsoft/Extensible-Storage-Engine): ESE is an embedded / ISAM-based database engine, that provides rudimentary table and indexed access. However the library provides many other strongly layered and and thus reusable sub-facilities as well: A Synchronization / Locking library, a Data-structures / STL-like library, an OS-abstraction layer, and a Cache Manager, as well the full blown…

## Sharding

- [Sharding-Sphere ![code](https://ng-tech.icu/assets/code.svg)](https://gitee.com/Sharding-Sphere/sharding-sphere): Sharding-Sphere is an open-source ecosystem consisted of a set of distributed database middleware solutions, including 3 independent products, Sharding-JDBC, Sharding-Proxy & Sharding-Sidecar (todo).

- [2015-KingShard ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/flike/kingshard): kingshard is a high-performance proxy for MySQL powered by Go.

- [Atlas ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/Qihoo360/Atlas): A high-performance and stable proxy for MySQL, it is developed by Qihoo's DBA and infrastructure team.

- [2017~Vitess ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/vitessio/vitess): Vitess is a database clustering system for horizontal scaling of MySQL.

- [2019~Gaea ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/XiaoMi/Gaea): Gaea is a mysql proxy, it's developed by xiaomi b2c-systech team.

# Key-Value Database

- [LevelDB ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/google/leveldb): LevelDB is a fast key-value storage library written at Google that provides an ordered mapping from string keys to string values.

- [RocksDB ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/facebook/rocksdb): A library that provides an embeddable, persistent key-value store for fast storage.

- [2018~Tidis ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/yongman/tidis): Tidis is a Distributed NoSQL database, providing a redis-protocal api(string,list,hash,set,sorted-set), written in Go.

- [2019~Badger ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/dgraph-io/badger): BadgerDB is an embeddable, persistent and fast key-value (KV) database written in pure Go. It is the underlying database for Dgraph, a fast, distributed graph database. It's meant to be a performant alternative to non-Go-based key-value stores like RocksDB.

- [2020~terarkdb ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/bytedance/terarkdb): A RocksDB compatible KV storage engine with better performance.

- [immudb ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/codenotary/immudb): world’s fastest immutable database, built on a zero trust model.

# Document Database

- [2018~edgedb ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/edgedb/edgedb)](https://github.com/edgedb/edgedb): A graph-relational database with declarative schema, built-in migration system, and a next-generation query language

# Graph Database

- [Cayley ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/cayleygraph/cayley): Cayley is an open-source graph inspired by the graph database behind Freebase and Google's Knowledge Graph.

- [Neo4j ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/neo4j/neo4j): Neo4j is the world’s leading Graph Database. It is a high performance graph store with all the features expected of a mature and robust database, like a friendly query language and ACID transactions.

- [Dgraph ![code](https://ng-tech.icu/assets/code.svg)](https://dgraph.io/): Dgraph is a horizontally scalable and distributed graph database, providing ACID transactions, consistent replication and linearizable reads.

- [Nebula ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/vesoft-inc/nebula): A distributed, fast open-source graph database featuring horizontal scalability and high availability.

- [cozo ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/cozodb/cozo): A general-purpose, transactional, relational database that uses Datalog and focuses on graph data and algorithms

# TimeSeries

- [2013-InfluxDB ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/influxdata/influxdb): InfluxDB is an open source time series database with no external dependencies. It's useful for recording metrics, events, and performing analytics.

- [2017~timescaledb ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/timescale/timescaledb/): An open-source time-series database optimized for fast ingest and complex queries. Engineered up from PostgreSQL, packaged as an extension.

- [2018~M3 monorepo ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/m3db/m3): Distributed TSDB, Aggregator and Query Engine, Prometheus Sidecar, Metrics Platform

- [VictoriaMetrics ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/VictoriaMetrics/VictoriaMetrics): VictoriaMetrics is fast, cost-effective and scalable time series database.

- [TDengine ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/taosdata/TDengine): TDengine is an open-sourced big data platform under GNU AGPL v3.0, designed and optimized for the Internet of Things (IoT), Connected Cars, Industrial IoT, and IT Infrastructure and Application Monitoring.

- [2019~LinDB ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/lindb/lindb): LinDB is a scalable, high performance, high availability distributed time series database.

- [2019~VictoriaMetrics ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/VictoriaMetrics/VictoriaMetrics): Fast, cost-effective and scalable time series database, long-term remote storage for Prometheus.

- [2021~QuestDB ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/questdb/questdb): QuestDB is a distributed, high-performance, fully-distributed, high-availability, fully-scalable, and highly-available time series database.

- [2022~GreptimeDB ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/GreptimeTeam/greptimedb): GreptimeDB, an open-source, cloud-native, distributed time-series database.

# NewSQL

- [FoundationDB ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/apple/foundationdb): FoundationDB is a distributed database designed to handle large volumes of structured data across clusters of commodity servers.

# P2P Database

- [OrbitDB ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/orbitdb/orbit-db): Peer-to-Peer Databases for the Decentralized Web.

- [Scuttlebot ![code](https://ng-tech.icu/assets/code.svg)](http://scuttlebot.io): Scuttlebot is an open source peer-to-peer log store used as a database, identity provider, and messaging system. It features global replication, file-syncronization, and end-to-end encryption.

# AI Database

- [2023~EVA ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/georgia-tech-db/eva)](https://github.com/georgia-tech-db/eva): EVA is a database system for building simpler and faster AI-powered applications.

- [2024~Chat2DB ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/chat2db/Chat2DB)](https://github.com/chat2db/Chat2DB): 🔥🔥🔥AI-driven data management platform Over 1 million developers are using Chat2DB.
