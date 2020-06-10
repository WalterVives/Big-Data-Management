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

### Doesn’t it take a long time to populate an in-memory database? 

Populating a very large in-memory database system can be much faster than populating an on-disk DBMS. During such “data ingest,” on-disk database systems use caching to enhance performance. But eventually, memory buffers fill up, and the system writes the data to the file system (logical I/O). Eventually, the file system buffers also fill up, and data must be written to the hard disk (physical I/O). Physical I/O is usually measured in milliseconds, and its performance burden is much greater than that of logical I/O (which is usually measured in microseconds). Physical I/O may be required by an on-disk DBMS for other reasons, for example, to guarantee transactional integrity 

**Examples:**

* Redis

* H2 Database 

* HSQLDB (HyperSQL Database) 

* Apache Derby Database 

* SQLite Database 

* EXtremeDB
 

## Key Value

### What is a key-value database? 

A key-value database is a type of nonrelational database that uses a simple key-value method to store data. A key-value database stores data as a collection of key-value pairs in which a key serve as a unique identifier. Both keys and values can be anything, ranging from simple objects to complex compound objects. Key-value databases are highly partitionable and allow horizontal scaling at scales that other types of databases cannot achieve. 

Key-value databases do not establish a specific schema. Traditional relational databases pre-define their structures within the database, using tables that contain fields with well-defined data types. Key-value systems, on the other hand, treat data as a single collection with the key representing an arbitrary string. 

 
<!---
Los almacenes de valores clave generalmente usan mucha menos memoria al guardar y almacenar la misma cantidad de datos, lo que a su vez aumenta el rendimiento para ciertos tipos de cargas de trabajo. 

Las bases de datos de valores clave "puros" no usan un lenguaje de consulta, pero ofrecen una forma de recuperar, guardar y eliminar datos mediante el uso de los comandos muy simples get, put y delete. (Las bases de datos de valores clave modificados pueden incluir búsquedas de texto completo). La recuperación de datos requiere un método de solicitud directa para comunicarse con el archivo de datos. No hay búsqueda, ni hay un motor de búsqueda. Si no se conoce la clave, no hay forma de encontrarla. 

Ejemplos: Aerospike, Apache Cassandra, Amazon Dynamo DB, Berkeley DB, Couchbase, Memcached, Riak, Redis. 

Casos de uso comunes para el almacén de valores clave 

Almacenar datos para la personalización del cliente 

Uso del almacenamiento en caché para acelerar la respuesta de la aplicación.
--->

### Scalability and Reliability 

Key-value stores scale out by implementing partitioning, replication and auto recovery. They can scale up by maintaining the database in RAM and minimize the effects of ACID guarantees by avoiding locks, latches and low-overhead server calls. 


![Example key-value](https://d1.awsstatic.com/product-marketing/DynamoDB/PartitionKey.8dd0530a7f6d66d101f31de30db515564f4cf28a.png) 

 

## References  

* https://aws.amazon.com/es/nosql/in-memory/#:~:text=An%20in%2Dmemory%20database%20is,data%20on%20disk%20or%20SSDs.&text=Because%20all%20data%20is%20stored,a%20process%20or%20server%20failure. 

* https://aws.amazon.com/nosql/key-value/#:~:text=A%20key%2Dvalue%20database%20is,objects%20to%20complex%20compound%20objects. 

* https://medium.com/@denisanikin/when-and-why-i-use-an-in-memory-database-or-a-traditional-database-management-system-5737f6d406b5 

* https://devopedia.org/in-memory-database 

* https://www.mcobject.com/in_memory_database/ 

* https://www.baeldung.com/java-in-memory-databases 