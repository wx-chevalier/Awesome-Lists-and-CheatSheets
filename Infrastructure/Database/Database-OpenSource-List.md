# Database OpenSource List | 数据库相关开源工具索引

# Showcase

- [MiniDataBase #Project#](https://github.com/msdeep14/MiniDataBase): A simple Relational Database using B+ Tree Index.

- [chidb #Project#](https://people.cs.uchicago.edu/~adamshaw/papers/sigcse2016-chidb.pdf): Building a Simple Relational Database System from Scratch.

- [LBADD #Project#](https://github.com/tomarrell/lbadd): An experimental, distributed SQL database.

- [2017-SimpleDB #Project#](https://github.com/iamxpy/SimpleDB): UC Berkeley's Database class CS186: Implement A Simple Database Management System

# Universal SQL Tools

## Client

### GUI

- [SQL Fiddle #Project#](http://sqlfiddle.com/): A tool for easy online testing and sharing of database problems and their solutions.

- [Dbeaver #Project#](https://dbeaver.io): Free multi-platform database tool for developers, SQL programmers, database administrators and analysts.

- [HeidiSQL #Project#](https://www.heidisql.com/): HeidiSQL is free software, and has the aim to be easy to learn. "Heidi" lets you see and edit data and structures from computers running one of the database systems MariaDB, MySQL, Microsoft SQL or PostgreSQL.

- [2020-Beekeeper Studio #Project#](https://github.com/beekeeper-studio/beekeeper-studio): Cross platform SQL editor and database management app for Windows, Linux, and Mac.

- [2020-Hue Editor #Project#](https://github.com/cloudera/hue): Open source SQL Query Assistant for Databases/Warehouses.

### CMD

- [2018-q #Project#](https://github.com/harelba/q): q is a command line tool that allows direct execution of SQL-like queries on CSVs/TSVs (and any other tabular text files).

- [usql #Project#](https://github.com/knq/usql): usql is a universal command-line interface for working with SQL databases.

### Editor

- [2014-sqlpad #Project#](https://github.com/rickbergfalk/sqlpad): Web-based SQL editor run in your own private cloud. Supports MySQL, Postgres, SQL Server, Vertica, Crate, Presto, SAP HANA, and Cassandra.

- [2016-Falcon #Project#](https://github.com/plotly/falcon): Free, open-source SQL client for Windows and Mac 🦅

## Analysis & Execution

- [queryparser #Project#](https://github.com/uber/queryparser): Parsing and analysis of Vertica, Hive, and Presto SQL. [Queryparser, an Open Source Tool for Parsing and Analyzing SQL](https://eng.uber.com/queryparser/)

- [sql-parser #Project#](https://github.com/dt-fe/sql-parser): Light and fast sql parser on browser.

- [2013-Druid #Project#](https://druid.apache.org/): 阿里巴巴数据库事业部出品，为监控而生的数据库连接池。

- [Apache Calcite #Project#](https://calcite.apache.org/): Industry-standard SQL parser,validator and JDBC driver.

- [2018-sqler #Project#](https://github.com/alash3al/sqler): write APIs using direct SQL queries with no hassle, let's rethink about SQL.

- [Zetasql #Project#](https://github.com/google/zetasql): ZetaSQL defines a language (grammar, types, data model, and semantics) as well as a parser and analyzer.

### Audit（审核平台）

- [2017-SQLAdvisor #Project#](https://github.com/Meituan-Dianping/SQLAdvisor): SQLAdvisor 是由美团点评公司技术工程部 DBA 团队(北京)开发维护的一个分析 SQL 给出索引优化建议的工具。它基于 MySQL 原生态词法解析，结合分析 SQL 中的 where 条件、聚合条件、多表 Join 关系 给出索引优化建议。目前 SQLAdvisor 在美团点评内部广泛应用，公司内部对 SQLAdvisor 的开发全面转到 github 上，开源和内部使用保持一致。

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

## MySQL

## Sharding

- [Sharding-Sphere #Project#](https://gitee.com/Sharding-Sphere/sharding-sphere): Sharding-Sphere is an open-source ecosystem consisted of a set of distributed database middleware solutions, including 3 independent products, Sharding-JDBC, Sharding-Proxy & Sharding-Sidecar (todo).

- [2015-KingShard #Project#](https://github.com/flike/kingshard): kingshard is a high-performance proxy for MySQL powered by Go.

- [Atlas #Project#](https://github.com/Qihoo360/Atlas): A high-performance and stable proxy for MySQL, it is developed by Qihoo's DBA and infrastructure team.

- [2017-Vitess #Project#](https://github.com/vitessio/vitess): Vitess is a database clustering system for horizontal scaling of MySQL.

- [2019-Gaea #Project#](https://github.com/XiaoMi/Gaea): Gaea is a mysql proxy, it's developed by xiaomi b2c-systech team.

# Key-Value Database

- [LevelDB #Project#](https://github.com/google/leveldb): LevelDB is a fast key-value storage library written at Google that provides an ordered mapping from string keys to string values.

- [RocksDB #Project#](https://github.com/facebook/rocksdb): A library that provides an embeddable, persistent key-value store for fast storage.

- [Badger #Project#](https://github.com/dgraph-io/badger): Fast key-value DB in Go.

- [2018-Tidis #Project#](https://github.com/yongman/tidis): Tidis is a Distributed NoSQL database, providing a redis-protocal api(string,list,hash,set,sorted-set), written in Go.

- [2020-terarkdb #Project#](https://github.com/bytedance/terarkdb): A RocksDB compatible KV storage engine with better performance.

## Redis

- [RedisGraph #Project#](http://redisgraph.io/design/): A High Performance In-Memory Graph Database as a Redis Module.

- [2018-RDR #Project#](https://github.com/xueqiu/rdr): RDR(redis data reveal) is a tool to parse redis rdbfile. Comparing to redis-rdb-tools, RDR is implemented by golang, much faster (5GB rdbfile takes about 2mins on my PC).

- [2018-KeyDB #Project#](https://github.com/JohnSully/KeyDB): A Multithreaded Fork of Redis

- [Redis-shake #Project#](https://github.com/alibaba/RedisShake): Redis-shake 是一个用于在两个 redis 之间同步数据的工具，满足用户非常灵活的同步、迁移需求。

- [2019-Redis Manager #Project#](https://github.com/ngbdf/redis-manager): Redis 一站式管理平台，支持集群的监控、安装、管理、告警以及基本的数据操作。

- [2019-Medis #Project#](https://github.com/luin/medis): 💻 Medis is a beautiful, easy-to-use Mac database management application for Redis.

# Document Database

## Search Engine

- [Elasticsearch #Project#](https://www.elastic.co/cn/): Elasticsearch is a distributed RESTful search engine built for the cloud.

- [search-index #Project#](https://github.com/fergiemcdowall/search-index): A persistent, network resilient, full text search library for the browser and Node.js.

- [wwsearch #Project#](https://github.com/Tencent/wwsearch): A full-text search engine supporting massive users, real-time updating, fast fuzzy matching and flexible table splitting.

- [MeiliSearch #Project#](https://github.com/meilisearch/MeiliSearch): MeiliSearch is a powerful, fast, open-source, easy to use and deploy search engine. Both searching and indexing are highly customizable.

- [Typesense #Project#](https://github.com/typesense/typesense): Typesense is a fast, typo-tolerant search engine for building delightful search experiences.

## MongoDB

- [MemDB #Project#](https://github.com/rain1017/memdb): Distributed Transactional In-Memory Database.

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

# NewSQL

- [FoundationDB #Project#](https://github.com/apple/foundationdb): FoundationDB is a distributed database designed to handle large volumes of structured data across clusters of commodity servers.

# Datawarehouse

- [LarkMidTable #Project#](https://github.com/wxgzgl/LarkMidTable): 基于 flinkx 的分布式数据中台产品。

## Meta Management

- [Apache Altas #Project#](https://atlas.apache.org/#/): Atlas is a scalable and extensible set of core foundational governance services – enabling enterprises to effectively and efficiently meet their compliance requirements within Hadoop and allows integration with the whole enterprise data ecosystem.

- [2020-Amundsen #Project#](https://github.com/amundsen-io/amundsen): Amundsen is a metadata driven application for improving the productivity of data analysts, data scientists and engineers when interacting with data.

## OLAP

- [2016-ClickHouse #Project#](https://clickhouse.yandex/): ClickHouse is an open source column-oriented database management system capable of real time generation of analytical data reports using SQL queries.

- [2017-Druid #Project#](http://druid.io/): Apache Druid (incubating) is a high performance analytics data store for event-driven data.

- [2017-Mondrian #Project#](https://github.com/pentaho/mondrian): Mondrian is an Online Analytical Processing (OLAP) server that enables business users to analyze large quantities of data in real-time.

- [Pinot #Project#](https://github.com/linkedin/pinot): Pinot is a realtime distributed OLAP datastore, which is used at LinkedIn to deliver scalable real time analytics with low latency.

## OLAP Browser

- [2015-Metabase #Project#](https://github.com/metabase/metabase): The simplest, fastest way to get business intelligence and analytics to everyone in your company.

- [Saiku #Project#](https://github.com/OSBI/saiku): Saiku Analytics - The Worlds Greatest Open Source OLAP Browser

- [CBoard #Project#](https://github.com/TuiQiao/CBoard): An easy to use, self-service open BI reporting and BI dashboard platform.

- [Apache Superset #Project#](https://github.com/apache/incubator-superset): Apache Superset (incubating) is a modern, enterprise-ready business intelligence web application

- [Metatron Discovery #Project#](https://github.com/metatron-app/metatron-discovery): Metatron Discovery is an end-to-end big data self discovery solution. To learn more about it, visit our web site. Check our blog for upcoming events and development news.

- [Poli #Project#](https://github.com/shzlw/poli): An easy-to-use BI server built for SQL lovers. Power data analysis in SQL and gain faster business insights.

- [Cube.js #Project#](https://github.com/cube-js/cube.js): Open Source Analytics Framework.

- [2015-Caravel #Project#](https://github.com/airbnb/caravel): Apache Superset (incubating) is a modern, enterprise-ready business intelligence web application

- [2016-Redash #Project#](https://github.com/getredash/redash): Make Your Company Data Driven. Connect to any data source, easily visualize, dashboard and share your data.

## MPP

- [Presto #Project#](https://prestodb.io/): Presto is an open source distributed SQL query engine for running interactive analytic queries against data sources of all sizes ranging from gigabytes to petabytes.

- [Materialize #Project#](https://materialize.com/docs/): Materialize is a streaming database for real-time applications. Materialize accepts input data from a variety of streaming sources (e.g. Kafka) and files (e.g. CSVs), and lets you query them using SQL.

## Business Intelligence

- [Apache Superset](https://github.com/apache/incubator-superset): Apache Superset (incubating) is a modern, enterprise-ready business intelligence web application. [Superset: Airbnb’s data exploration platform](https://parg.co/bIh)

- [Grid studio #Project#](https://github.com/ricklamers/gridstudio): Grid studio is a web-based spreadsheet application with full integration of the Python programming language.

- [Davinci #Project#](https://edp963.github.io/davinci/): Davinci 是一个 DVaaS（Data Visualization as a Service）平台解决方案，面向业务人员/数据工程师/数据分析师/数据科学家，致力于提供一站式数据可视化解决方案。既可作为公有云/私有云独立部署使用，也可作为可视化插件集成到三方系统。用户只需在可视化 UI 上简单配置即可服务多种数据可视化应用，并支持高级交互/行业分析/模式探索/社交智能等可视化功能。

## Data Lake

- [Apache Hudi #Project#](https://github.com/apache/incubator-hudi): Upserts, Deletes And Incremental Processing on Big Data.

# Data Aggregation

## Data Orchestrator

- [Prefect #Project#](https://github.com/PrefectHQ/prefect): Prefect is a new workflow management system, designed for modern infrastructure and powered by the open-source Prefect Core workflow engine. Users organize Tasks into Flows, and Prefect takes care of the rest.

- [dagster #Project#](https://github.com/dagster-io/dagster): A data orchestrator for machine learning, analytics, and ETL.

## ETL

- [awesome-etl #Project#](https://github.com/pawl/awesome-etl#workflow-managementengines): A curated list of awesome ETL frameworks, libraries, and software.

- [DataX #Project#](https://github.com/alibaba/DataX): 阿里巴巴集团内被广泛使用的离线数据同步工具/平台

- [dbt #Project#](https://github.com/fishtown-analytics/dbt): dbt (data build tool) enables data analysts and engineers to transform their data using the same practices that software engineers use to build applications.

## CDC & Data Pipeline

- [Debezium #Project#](https://debezium.io/docs/tutorial/): Debezium is a distributed platform that turns your existing databases into event streams, so applications can see and respond immediately to each row-level change in the databases.

- [Canal #Project#](https://github.com/alibaba/canal): 阿里巴巴 mysql 数据库 binlog 的增量订阅&消费组件。阿里云 DRDS( https://www.aliyun.com/product/drds )、阿里巴巴 TDDL 二级索引、小表复制 powerd by canal.

- [Otter #Project#](https://github.com/alibaba/otter): 阿里巴巴分布式数据库同步系统(解决中美异地机房)

# P2P Database

- [OrbitDB #Project#](https://github.com/orbitdb/orbit-db): Peer-to-Peer Databases for the Decentralized Web.

- [Scuttlebot #Project#](http://scuttlebot.io): Scuttlebot is an open source peer-to-peer log store used as a database, identity provider, and messaging system. It features global replication, file-syncronization, and end-to-end encryption.
