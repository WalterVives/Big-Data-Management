# Databases Classification and Matrix comparison 

In this file you going to see a brief introduction of 3 database types:

* **In-memory**
* **Key-Value**, 
* **Time-series**  

And a matrix comparison of the different examples of **In-memory** database. 

## In-memory 

### What is an in-memory database? 

![in-memory architecture](https://devopedia.org/images/article/163/7568.1554310706.jpg) 

An in-memory database (IMDB) is a type of purpose-built database that relies primarily on memory for data storage, in contrast to databases that store data on disk or SSDs. In-memory databases are designed to attain minimal response time by eliminating the need to access disks. Because all data is stored and managed exclusively in main memory, it is at risk of being lost upon a process or server failure. In-memory databases can persist data on disks by storing each operation in a log or by taking snapshots. 

IMDB has gained traction in recent times because of increasing speeds, reducing costs and growing size of RAM devices, combined with powerful multi-core processors. Since only RAM is accessed and there is no disk operation for an IMDB query, speeds are extremely high. 

However, RAM storage is volatile. So, there will be data loss when the device loses power. To overcome this, IMDB employ several techniques such as checkpoints, transaction logging, and non-volatile RAM. 

In-memory databases are ideal for applications that require microsecond response times and can have large spikes in traffic coming at any time such as gaming leaderboards, session stores, and real-time analytics 

 

### Isn’t the database just lost if there’s a system crash? 

It needn’t be. Most in-memory database systems offer features for adding persistence, or the ability survive disruption of their hardware or software environment. 

One important tool is transaction logging, in which periodic snapshots of the in-memory database (called “savepoints”) are written to non-volatile media. If the system fails and must be restarted, the database either “rolls back” to the last completed transaction, or “rolls forward” to complete any transaction that was in progress when the system went down (depending on the particular IMDS’s implementation of transaction logging). 

## Doesn’t it take a long time to populate an in-memory database? 

Populating a very large in-memory database system can be much faster than populating an on-disk DBMS. During such “data ingest,” on-disk database systems use caching to enhance performance. But eventually, memory buffers fill up, and the system writes the data to the file system (logical I/O). Eventually, the file system buffers also fill up, and data must be written to the hard disk (physical I/O). Physical I/O is usually measured in milliseconds, and its performance burden is much greater than that of logical I/O (which is usually measured in microseconds). Physical I/O may be required by an on-disk DBMS for other reasons, for example, to guarantee transactional integrity 

## Examples:  

* H2 Database 

* HSQLDB (HyperSQL Database) 

* Apache Derby Database 

* SQLite Database 

 

## Key Value: 

### What is a key-value database? 

A key-value database is a type of nonrelational database that uses a simple key-value method to store data. A key-value database stores data as a collection of key-value pairs in which a key serve as a unique identifier. Both keys and values can be anything, ranging from simple objects to complex compound objects. Key-value databases are highly partitionable and allow horizontal scaling at scales that other types of databases cannot achieve. 

Key-value databases do not establish a specific schema. Traditional relational databases pre-define their structures within the database, using tables that contain fields with well-defined data types. Key-value systems, on the other hand, treat data as a single collection with the key representing an arbitrary string. 


### Scalability and Reliability 

Key-value stores scale out by implementing partitioning, replication and auto recovery. They can scale up by maintaining the database in RAM and minimize the effects of ACID guarantees by avoiding locks, latches and low-overhead server calls. 

### Key-value store advantages 

There are a few advantages that a key-value store provides over traditional row-column-based databases. Thanks to the simple data format that gives it its name, a key-value store can be very fast for read and write operations. And key-value stores are very flexible, a valued asset in modern programming as we generate more data without traditional structures. 

 

Also, key-value stores do not require placeholders such as “null” for optional values, so they may have smaller storage requirements, and they often scale almost linearly with the number of nodes. 

 

### What can a Key-Value Database be used for? 

Key-value databases can be applied to many scenarios. For example, key-value stores can be useful for storing things such as the following. 

  

### General Web/Computers 

* User profiles 

* Session information 

* Article/blog comments 

* Emails 

* Status messages 

### Ecommerce 

* Shopping cart contents 

* Product categories 

* Product details 

* Product reviews 

### Networking/Data Maintenance 

* Telecom directories 

* Internet Protocol (IP) forwarding tables 

* Data deduplication 

 

![Example key-value](https://d1.awsstatic.com/product-marketing/DynamoDB/PartitionKey.8dd0530a7f6d66d101f31de30db515564f4cf28a.png) 

 

## Time-Series 

### What is a Time-Series Database? 

A time series database (TSDB) is a database optimized for time-stamped or time series data. Time series data are simply measurements or events that are tracked, monitored, downsampled, and aggregated over time. This could be server metrics, application performance monitoring, network data, sensor data, events, clicks, trades in a market, and many other types of analytics data. 

  

A time series database is built specifically for handling metrics and events or measurements that are time-stamped. A TSDB is optimized for measuring change over time. Properties that make time series data very different than other data workloads are data lifecycle management, summarization, and large range scans of many records. 

### Why is important now? 

Time series databases are not new, but the first-generation time series databases were primarily focused on looking at financial data, the volatility of stock trading, and systems built to solve trading. 

The fundamental conditions of computing have changed dramatically over the last decade. Everything has become compartmentalized. Monolithic mainframes have vanished, replaced by serverless servers, microservers, and containers. 

Today, everything that can be a component is a component. 

We are witnessing the instrumentation of every available surface in the material world, so now, everything inside and outside the company is emitting a relentless stream of metrics and events or time series data. 

This means that the underlying platforms need to evolve to support these new workloads — more data points, more data sources, more monitoring, more controls. What we’re witnessing, and what the times demand, is a paradigmatic shift in how we approach our data infrastructure and how we approach building, monitoring, controlling, and managing systems. What we need is a performant, scalable, purpose-built time series database. 

 

### The more relevant Time-Series Databases: 

Time series databases are the fastest growing segment in the database industry. But which time series database is the best and most popular?, Well an independent website, DB-Engines, ranks databases based on search engine popularity, social media mentions, job postings, and technical discussion volume: 

* InfluxDB 

* Kdb+ 

* Prometheus 

* Graphite 

* RRDTool 

* TimescaleDB 

* OpenTSDB 

* Druid 

* FaunaDB 

* KairosDB 

* DolphinDB 

* GridDB 

* eXtremeDB 

* Amazon Timestream 

* Alibaba Cloud TSDB 

 


## In-memory Database Matrix
|1     |Aerospike DBS|ALTIBASE HDB|Kinetica|Apache Ignite|ArangoDB|eXtremeDB|InfinityDB|SQLite|Microsoft SQL Server|
|:-----:|:----|:---|:---|:---|:---|:---|:---|:---|:---|
|Best used|NoSQL key-value database that delivers ultra-fast runtime performance for read/write workloads, high availability, near-linear scalability, and strong data consistency – all at a fraction of the cost of other alternatives|The software comes with a hybrid architecture which allows it to access both memory-resident and disk-resident tables using single interface. It supports both synchronous and asynchronous replication and offers real-time ACID compliance. Support is also offered for a variety of SQL standards and programming languages|What really separates Kinetica is its specialized filtering and visualization functions. These functions can be performed through our native API and various language specific connectors, or by SQL through ODBC/JDBC connectors|An In-Memory Data Grid, An In-Memory Database,A Streaming Analytics Engine, A Continuous Learning Framework for machine and deep learning, A Persistent Store, An In-Memory Compute Grid, An In-Memory Service Grid,Advanced Clustering, An Accelerator for Hadoop-An In-Memory Distributed File System|Simplified Performance Scaling,Reduced Operational Complexity,Strong Data Consistency,Fault Tolerance,Lower Total Cost of Ownership,Transactions|Supports full ACID database properties, High Availability, Clustering, and Sharding Public benchmarks prove eXtremeDB is the highest performance and lowest latency DBMS available|InfinityDB is appropriate for embedded hardware platforms, text indexing engines, distributed industrial data collection systems, and heterogeneous data environments|SQLite is often used as the on-disk file format for desktop applications such as version control systems, financial analysis tools, media cataloging and editing suites, CAD packages, record keeping programs, and so forth|it gives you the advantage of working with a table structure based on rows, which allows the connection of correlated data elements and functions|
|Usage example|https://github.com/aerospike/aerospike-client-ruby|https://github.com/ALTIBASE|https://github.com/kineticadb|https://github.com/apache/ignite|https://github.com/arangodb/arangodb|eXtremeDB has been successfully deployed in IoT, financial systems, telecom & networking, aerospace & defense|In the embedded system, data is stored to and retrieved from a single embedded database file using the InfnityDB API that allows direct access to the variable length item space|https://github.com/sqlite/sqlite|https://docs.microsoft.com/en-us/sql/t-sql/queries/select-examples-transact-sql?view=sql-server-ver15|
|Main focus|Create a flexible, scalable platform for web-scale applications, Provide the robustness and reliability (as in ACID) expected from traditional databases, Provide operational efficiency with minimal manual involvement|Altibase’s mission is to cut through, clarify, and capture the essence of business: its clients’ happiness. Customer satisfaction: Altibase is committed to understanding and supporting its clients with its hybrid database experts. Trust: Altibase unequivocally values its clients’ time and money. Zero IP Infringement: Altibase honors IPs of other database vendors and is clear of IP infringements|Kinetica is a distributed, in-memory database accelerated by GPUs that can simultaneously ingest, analyze, and visualize streaming data for truly real-time actionable intelligence.|a horizontally scalable, fault-tolerant distributed in-memory computing platform for building real-time applications that can process terabytes of data with in-memory speed|The database system supports three data models (key/value, documents, graphs) with one database core and a unified query language AQL (ArangoDB Query Language)|eXtremeDB is an in-memory and/or persistent database system that offers an ultra-small footprint which provides performance benefits for both embedded and server development|InfinityDB Embedded is a Java NoSQL database, a hierarchical sorted key value store. It is high-performance, multi-core, flexible, and maintenance-free. InfinityDB Encrypted database and InfinityDB Client/Server database are now available as well.|It can be used to create a database, define tables, insert and change rows, run queries and manage an SQLite database file. It also serves as an example for writing applications that use the SQLite library. SQLite uses automated regression testing prior to each release|with the primary function of storing and retrieving data as requested by other software applications—which may run either on the same computer or on another computer across a network (including the Internet)|
|developer|Aerospike Company|Altibase Corporation|Kinetica DB(formerly GIS Federal)|Apache Software Foundation|ArangoDB GmbH|McObject LLC.|Boiler Bay Inc.|D. Richard Hipp|Microsoft|
|platforms|support for Spark, Kafka, Hadoop, and other commonly used platforms|Altibase is a multi-platform and can be executed on nearly all enterprise OS and platforms.|Kinetica Active Analytics Platform| Build streaming analytics applications, often with Apache Spark, Apache Kafka™ and other streaming technologies|Cross Platform|Cross-platform|multi-core platforms|cross-platform|Linux, windows, docker|
|License|Open Source (AGPL)|Open source(GNU-AGPLv3, GNU-LGPLv3(for client-libraries))/private|Open source(GNU-AGPLv3, GNU-LGPLv3(for client-libraries))|Open Source (Apache License Version 2.0) |Open Source (Apache License Version 2.0)|Proprietary|Proprietary|Open Source (Public domain)|Proprietary|
|protocol|HTTP v1.1, HTTPS v1.1, HTTP v2, HTTPS v2|TCP/IP|TCP/IP|Ignite binary client protocol provides user applications the ability to communicate with an existing Ignite cluster without starting a full-fledged Ignite node|VelocyStream 1.1 – async binary protocol|RS-485/RS-232, Control Area Network (CAN) or Ethernet|uses a rugged internal storage update protocol for persistence on demand or cache spilling to disk for large amounts of data that maintains system-wide data integrity, and survives abrupt application termination or other problems|TCP/IP|Shared memory, Named Pipes, TCP/IP, and VIA|
|website|https://www.aerospike.com/docs/|https://altibase.com/|www.kinetica.com|https://ignite.apache.org/|https://www.arangodb.com/|https://www.mcobject.com/extremedbfamily/|https://boilerbay.com/infinitydb/|sqlite.org|https://www.microsoft.com/es-mx/sql-server/sql-server-downloads|
|Cloud DB|yes|yes|yes|yes|yes|yes|Null|No|yes|
|Wikipedia|https://en.wikipedia.org/wiki/Aerospike_(database)|https://en.wikipedia.org/wiki/Altibase|https://en.wikipedia.org/wiki/Kinetica_(software)|https://en.wikipedia.org/wiki/Apache_Ignite|https://en.wikipedia.org/wiki/ArangoDB|https://en.wikipedia.org/wiki/EXtremeDB|https://en.wikipedia.org/wiki/InfinityDB|https://en.wikipedia.org/wiki/SQLite|https://en.wikipedia.org/wiki/Microsoft_SQL_Server|
|Development language|C|Null|Null|Null|C++|C|Java|C|C/C++|
|Release date|2012|1999|2009|2014|2011|2001|2002|2000|1989|
|Latest version|4.8.0.3|7.1|7.0|2.8.0|3.6.0|8.1|4.0|3.32.2|15.0|


## Key-value Database Matrix


|      |Redis|Oracle NoSQL Database|Project Voldemort|Aerospike|Oracle Berkely DB|Amazon DynamoDB|ArangoDB|RocksDB|
|:-----:|:----|:---|:---|:---|:---|:---|:---|:---|
|Best used|For rapidly changing data with a foreseeable database size (should fit mostly in memory)|Oracle NoSQL Database can be integrated with a number of Oracle and Open source products for enterprises that rely on various databases for their most critical business data|It is used at LinkedIn by numerous critical services powering a large portion of the site|NoSQL key-value database that delivers ultra-fast runtime performance for read/write workloads, high availability, near-linear scalability, and strong data consistency – all at a fraction of the cost of other alternatives|Family of embedded key-value database libraries providing scalable high-performance data management services to applications|DynamoDB charges for reading, writing, and storing data in your DynamoDB tables, along with any optional features you choose to enable. DynamoDB has two capacity modes and those come with specific billing options for processing reads and writes on your tables: on-demand and provisioned|Provides the capabilities of a graph database, a document database, a key-value store in one C++ core|A user-facing application that stores the viewing history and state of users of a website, a spam detection application that needs fast access to big data sets, a graph-search query that needs to scan a data set in realtime, a cache data from Hadoop, thereby allowing applications to query Hadoop data in realtime, a message-queue that supports a high number of inserts and deletes|
|Usage example|Stock prices. Analytics. Real-time data collection. Real-time communication|Internet of Things where large volume of data needs to be stored and processed very fast, customer Views - determine the history of a customers interaction and make suggestions for further purchases|Automatic replication of data over multiple servers, automatic partitioning of data, so each server contains only a subset of the total data|https://github.com/aerospike-examples/aerospike-modeling|https://docs.oracle.com/cd/E17277_02/html/examples.html#txn|You can create database tables capable of storing and retrieving any amount of data, as well as serving any level of request traffic. You can scale the performance capacity of your tables to increase or decrease it without downtime or reduced performance. You can use the AWS Management Console to monitor resource utilization and performance metrics|https://github.com/arangodb/example-datasets|https://github.com/facebook/rocksdb/blob/master/examples/simple_example.cc|
|Main focus|Speed|It provides transactional semantics for data manipulation, horizontal scalability, and simple administration and monitoring|Highly-scalability storage|Create a flexible, scalable platform for web-scale applications, provide the robustness and reliability (as in ACID) expected from traditional databases|Provide scalable high-performance data management services to application|Fast and predictable performance as well as optimal scalability|focuses heavily on improving overall performance and adds a powerful new feature that combines the performance characteristics of a single server with the fault tolerance of clusters|Making an efficient, high-performance, single-node database engine|
|developer|Redis Labs|Oracle|LinkedIn / Microsoft|Aerospike Company|Sleepycat Software, later Oracle Corporation|Amazon|ArangoDB GmbH|Facebook|
|Platforms|Cross-Platform |Linux and Solaris 10|Distributed data store, NoSQL, Riak, Redis|support for Spark, Kafka, Hadoop, and other commonly used platforms |(Linux, Windows, BSD UNIX, Solaris, Mac OS/X, VxWorks and any POSIX-compliant operating system|Cross-platform|multi-model database|x86, x86_64, ppc64, ppc64le, aarch64|
|License|BSD|Apache license v2 (CE) and Proprietary (EE)|Apache License 2.0|Open Source (AGPL)|NoSQL Database License    Dual licensed (GNU Affero General Public License and commercial permissive license) (version 6.x and upwards) Sleepycat license (versions 2.0-5.x), clause BSD license (versions 1.x) / JE is licensed under Apache License, Version 2.0.|Proprietary|Apache License 2.0|Apache 2.0 or GPL 2|
|protocol|Telnet-like|SNMP and JMX|HTTP server|HTTP v1.1, HTTPS v1.1, HTTP v2, HTTPS v2|SNMP and JMX|Json|HTTP with VelocyPack|Compatible with the Redis protocol|
|website|https://socialcompare.com/r/?http%3A%2F%2Fredis.io%2F|www.oracle.com/­database/­nosql/­index.html|www.project-voldemort.com|https://www.aerospike.com/docs/|http://www.oracle.com/database/berkeley-db/|http://aws.amazon.com/dynamodb/|http://arangodb.com/|http://rocksdb.org/|
|Cloud DB|Null|OANDC|No|Yes|Null|Yes|AQL|Yes|
|Wikipedia|http://en.wikipedia.org/wiki/Redis_(data_store)|https://en.wikipedia.org/wiki/Oracle_NoSQL_Database#:~:text=Oracle%20NoSQL%20Database%20(ONDB)%20is,)%20on%20August%2010%2C%202018|https://en.wikipedia.org/wiki/Voldemort_(distributed_data_store)|https://en.wikipedia.org/wiki/Aerospike_(database)|https://es.wikipedia.org/wiki/Berkeley_DB|https://en.wikipedia.org/wiki/Amazon_DynamoDB|https://en.wikipedia.org/wiki/ArangoDB|https://en.wikipedia.org/wiki/RocksDB|
|Development language|C/C++|Java|Java|C|C|Java|C++, JavaScript|C++|
|Realese date|2015 May 5|2011 September|2009|2012|1994|January 2012|2011|1012 May|
|Latest version|3.0.1|19.5|1.10.25|4.8.0.3|18.1|2019.11.21|3.6.0|  136.8.1|




## References  

* https://aws.amazon.com/es/nosql/in-memory/#:~:text=An%20in%2Dmemory%20database%20is,data%20on%20disk%20or%20SSDs.&text=Because%20all%20data%20is%20stored,a%20process%20or%20server%20failure. 

* https://aws.amazon.com/nosql/key-value/#:~:text=A%20key%2Dvalue%20database%20is,objects%20to%20complex%20compound%20objects. 

* https://medium.com/@denisanikin/when-and-why-i-use-an-in-memory-database-or-a-traditional-database-management-system-5737f6d406b5 

* https://devopedia.org/in-memory-database 

* https://www.mcobject.com/in_memory_database/ 

* https://www.baeldung.com/java-in-memory-databases 

* https://www.aerospike.com/docs/architecture/ 

* https://www.softwaretestinghelp.com/altibase-database-tutorial/ 

* https://en.wikipedia.org/wiki/List_of_in-memory_databases  

* https://www.gridgain.com/resources/papers/introducing-apache-ignite#:~:text=APACHE%20IGNITE%20BENEFITS%20AND%20FEATURES,-Apache%20Ignite%20includes&text=An%20In%2DMemory%20Data%20Grid,for%20machine%20and%20deep%20learning 

* https://www.globenewswire.com/news-release/2019/11/19/1949662/0/en/eXtremeDB-8-1-adds-features-for-easier-more-sophisticated-database-management.html 

* https://info.microsoft.com/rs/157-GQE-382/images/EN-GB-CNTNT-eBook-DBMC-SQL-Server-performance-faster-querying-with-SQL-Server%20%281%29.pdf 

* https://rocksdb.org/blog/  

* https://dbdb.io/db/rocksdb  

* https://www.quora.com/What-are-some-good-uses-for-RocksDB  

* https://rockset.com/blog/rocksdb-is-eating-the-database-world/  

* https://github.com/facebook/rocksdb/wiki/Basic-Operations  

* https://www.arangodb.com/docs/stable/programs-arangoexport-examples.html  

* https://www.arangodb.com/why-arangodb/multi-model/#:~:text=ArangoDB%20can%20be%20used%20as,indexes%20and%20real%20JOIN%20operations.  

* https://www.arangodb.com/about-arangodb/  

* https://aws.amazon.com/dynamodb/  

* https://docs.aws.amazon.com/dynamodb/  

* https://en.wikipedia.org/wiki/Dynamo_(storage_system)  

* https://es.qwe.wiki/wiki/Berkeley_DB  

* https://docs.oracle.com/cd/E17277_02/html/examples.html  

* https://docs.oracle.com/cd/E17277_02/html/examples.html#txn  

* https://en.wikipedia.org/wiki/Voldemort_(distributed_data_store)  

* https://www.project-voldemort.com/voldemort/  

* https://www.ukessays.com/essays/engineering/nosql-databases-voldemort-db-engineering-essay.php  

* https://blog.linkedin.com/2009/04/01/project-voldemort-part-ii-how-it-works  

* https://www.grapheverywhere.com/bases-de-datos-clave-valor/  

* https://db-engines.com/en/system/Oracle+NoSQL#a33  

* https://www.oracle.com/technetwork/nosql-vs-mongodb-1961723.pdf  

* https://www.google.com/search?sxsrf=ALeKk03H17xg9qmKTKy_kbh5KRu_dC9MQw%3A1592103990522&ei=NpTlXoHAH6TmxgHNg4ioBw&q=oracle+berkeley+database+latest+version&oq=oracle+berkeley+database+lastes&gs_lcp=CgZwc3ktYWIQAxgBMgcIIRAKEKABMgcIIRAKEKABMgcIIRAKEKABOgQIIxAnOgYIABAWEB46CAghEBYQHRAeOgUIIRCgAVD9lwtYuKELYISwC2gAcAB4AIAB1wGIAcsKkgEFMC43LjGYAQCgAQGqAQdnd3Mtd2l6&sclient=psy-ab  

* https://socialcompare.com/en/search?q=oracle+nosql&l=on  

* https://db-engines.com/en/system/Oracle+NoSQL#a37  






















