[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wx-chevalier/Awesome-Lists)

# Database OpenSource List | 数据库相关开源工具索引

# Universal SQL Tools

## Client

- [2018-q #Project#](https://github.com/harelba/q): q is a command line tool that allows direct execution of SQL-like queries on CSVs/TSVs (and any other tabular text files).

- [usql #Project#](https://github.com/knq/usql): usql is a universal command-line interface for working with SQL databases.

* [SQL Fiddle #Project#](http://sqlfiddle.com/): A tool for easy online testing and sharing of database problems and their solutions.

- [Dbeaver #Project#](https://dbeaver.io): Free multi-platform database tool for developers, SQL programmers, database administrators and analysts.

- [HeidiSQL #Project#](https://www.heidisql.com/): HeidiSQL is free software, and has the aim to be easy to learn. "Heidi" lets you see and edit data and structures from computers running one of the database systems MariaDB, MySQL, Microsoft SQL or PostgreSQL.

## Analysis & Execution

- [queryparser #Project#](https://github.com/uber/queryparser): Parsing and analysis of Vertica, Hive, and Presto SQL. [Queryparser, an Open Source Tool for Parsing and Analyzing SQL](https://eng.uber.com/queryparser/)

- [sql-parser #Project#](https://github.com/dt-fe/sql-parser): Light and fast sql parser on browser.

- [2013-druid #Project#](https://github.com/alibaba/druid): 阿里巴巴数据库事业部出品，为监控而生的数据库连接池。

- [Apache Calcite #Project#](https://calcite.apache.org/): Industry-standard SQL parser,validator and JDBC driver.

* [2017-SQLAdvisor #Project#](https://github.com/Meituan-Dianping/SQLAdvisor): SQLAdvisor 是由美团点评公司技术工程部 DBA 团队(北京)开发维护的一个分析 SQL 给出索引优化建议的工具。它基于 MySQL 原生态词法解析，结合分析 SQL 中的 where 条件、聚合条件、多表 Join 关系 给出索引优化建议。目前 SQLAdvisor 在美团点评内部广泛应用，公司内部对 SQLAdvisor 的开发全面转到 github 上，开源和内部使用保持一致。

- [2018-sqler #Project#](https://github.com/alash3al/sqler): write APIs using direct SQL queries with no hassle, let's rethink about SQL.

- [Zetasql #Project#](https://github.com/google/zetasql): ZetaSQL defines a language (grammar, types, data model, and semantics) as well as a parser and analyzer.

## Migration & Transfer

- [FlyWay #Project#](https://github.com/flyway/flyway): Evolve your database schema easily and reliably across all your instances.

* [PingCAP-Loader #Project#](https://github.com/pingcap/docs-cn/blob/master/tools/loader.md)

## Benchmark

- [DBT2 #Project#](http://osdldbt.sourceforge.net/)

- [SysBench #Project#](http://sysbench.sourceforge.net/)

- [supersmack #Project#](http://vegan.net/tony/supersmack/)

* [mybench](http://jeremy.zawodny.com/mysql/mybench/)

# Relational Database

## MySQL

- [mycli #Project#](https://github.com/dbcli/mycli): A Terminal Client for MySQL with AutoCompletion and Syntax Highlighting.

- [Percona Toolkit #Project#](https://github.com/percona/percona-toolkit): Percona Toolkit is a collection of advanced command-line tools used by Percona support staff to perform a variety of MySQL and system tasks that are too difficult or complex to perform manually.

- [gh-ost #Project#](https://github.com/github/gh-ost): gh-ost is a triggerless online schema migration solution for MySQL.

* [2017-OnlineSchemaChange #Project#](https://github.com/facebookincubator/OnlineSchemaChange): A tool for performing online schema changes on MySQL.

- [Freno #Project#](https://github.com/github/freno): Cooperative, highly available throttler service: clients use freno to throttle writes to a resource.

### Accessing

- [2018-ginbro #Project#](https://github.com/dejavuzhou/ginbro): Converting a MySQL database'schema to a RESTful golang APIs app in the fastest way.

### HA

- [Orchestrator #Project#](https://github.com/github/orchestrator): MySQL replication topology management and HA

## Sharding

- [Sharding-Sphere #Project#](https://gitee.com/Sharding-Sphere/sharding-sphere): Sharding-Sphere is an open-source ecosystem consisted of a set of distributed database middleware solutions, including 3 independent products, Sharding-JDBC, Sharding-Proxy & Sharding-Sidecar (todo).

* [2015-KingShard #Project#](https://github.com/flike/kingshard): kingshard is a high-performance proxy for MySQL powered by Go.

* [Atlas #Project#](https://github.com/Qihoo360/Atlas): A high-performance and stable proxy for MySQL, it is developed by Qihoo's DBA and infrastructure team.

* [2017-Vitess #Project#](https://github.com/vitessio/vitess): Vitess is a database clustering system for horizontal scaling of MySQL.

* [2019-Gaea #Project#](https://github.com/XiaoMi/Gaea): Gaea is a mysql proxy, it's developed by xiaomi b2c-systech team.

# Key-Value Database

- [LevelDB #Project#](https://github.com/google/leveldb): LevelDB is a fast key-value storage library written at Google that provides an ordered mapping from string keys to string values.

## Redis

- [RedisGraph #Project#](http://redisgraph.io/design/): A High Performance In-Memory Graph Database as a Redis Module.

# Document Database

## Search Engine

- [search-index #Project#](https://github.com/fergiemcdowall/search-index): A persistent, network resilient, full text search library for the browser and Node.js.

## MongoDB

- [MemDB #Project#](https://github.com/rain1017/memdb): Distributed Transactional In-Memory Database.

# Graph Database

- [Cayley #Project#](https://github.com/cayleygraph/cayley): Cayley is an open-source graph inspired by the graph database behind Freebase and Google's Knowledge Graph.

- [Neo4j #Project#](https://github.com/neo4j/neo4j): Neo4j is the world’s leading Graph Database. It is a high performance graph store with all the features expected of a mature and robust database, like a friendly query language and ACID transactions.

- [Dgraph #Project#](https://dgraph.io/): Dgraph is a horizontally scalable and distributed graph database, providing ACID transactions, consistent replication and linearizable reads.

# TimeSeries

- [2013-InfluxDB #Project#](https://github.com/influxdata/influxdb): InfluxDB is an open source time series database with no external dependencies. It's useful for recording metrics, events, and performing analytics.

- [2017-timescaledb #Project#](https://github.com/timescale/timescaledb/): An open-source time-series database optimized for fast ingest and complex queries. Engineered up from PostgreSQL, packaged as an extension.

- [2018-M3 monorepo #Project#](https://github.com/m3db/m3): Distributed TSDB, Aggregator and Query Engine, Prometheus Sidecar, Metrics Platform

# NewSQL

- [FoundationDB #Project#](https://github.com/apple/foundationdb): FoundationDB is a distributed database designed to handle large volumes of structured data across clusters of commodity servers.

# Datawarehouse

## ETL

- [awesome-etl #Project#](https://github.com/pawl/awesome-etl#workflow-managementengines): A curated list of awesome ETL frameworks, libraries, and software.

- [DataX #Project#](https://github.com/alibaba/DataX): 阿里巴巴集团内被广泛使用的离线数据同步工具/平台
