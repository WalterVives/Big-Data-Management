## Designing Data-Intensive Applications.

## Chapter 1 Reliable, Scalable, and Maintainable Applications.

#### 1. What is Realibility?

Everybody has an intuitive idea of what it means for something to be reliable or unre‐ liable. For software, typical expectations include:

• The application performs the function that the user expected.
• It can tolerate the user making mistakes or using the software in unexpected ways.
• Its performance is good enough for the required use case, under the expected load and data volume.
• The system prevents any unauthorized access and abuse.

If all those things together mean “working correctly,” then we can understand relia‐ bility as meaning, roughly, “continuing to work correctly, even when things go wrong.”
The things that can go wrong are called faults, and systems that anticipate faults and can cope with them are called fault-tolerant or resilient.

#### 2. What about Hardware faults?

When we think of causes of system failure, hardware faults quickly come to mind. Hard disks crash, RAM becomes faulty, the power grid has a blackout, someone unplugs the wrong network cable. Anyone who has worked with large datacenters can tell you that these things happen all the time when you have a lot of machines.

Our first response is usually to add redundancy to the individual hardware compo‐ nents in order to reduce the failure rate of the system. Disks may be set up in a RAID configuration, servers may have dual power supplies and hot-swappable CPUs, and datacenters may have batteries and diesel generators for backup power. When one component dies, the redundant component can take its place while the broken com‐ ponent is replaced. This approach cannot completely prevent hardware problems from causing failures, but it is well understood and can often keep a machine running uninterrupted for years.

#### 3. What about Software Errors?

We usually think of hardware faults as being random and independent from each other: one machine’s disk failing does not imply that another machine’s disk is going to fail. There may be weak correlations (for example due to a common cause, such as the temperature in the server rack), but otherwise it is unlikely that a large number of hardware components will fail at the same time.

Another class of fault is a systematic error within the system. Such faults are harder to anticipate, and because they are correlated across nodes, they tend to cause many more system failures than uncorrelated hardware faults [5]. Examples include:

- A software bug that causes every instance of an application server to crash when given a particular bad input. For example, consider the leap second on June 30,     2012, that caused many applications to hang simultaneously due to a bug in the Linux kernel.
- A runaway process that uses up some shared resource—CPU time, memory, disk space, or network bandwidth.
- A service that the system depends on that slows down, becomes unresponsive, or starts returning corrupted responses.
- Cascading failures, where a small fault in one component triggers a fault in another component, which in turn triggers further faults 

#### 4. Humans Errors

Humans design and build software systems, and the operators who keep the systems running are also human. Even when they have the best intentions, humans are known to be unreliable. For example, one study of large internet services found that configuration errors by operators were the leading cause of outages, whereas hard‐ ware faults (servers or network) played a role in only 10–25% of outages.

#### 5. How Important Is Reliability?

Reliability is not just for nuclear power stations and air traffic control software— more mundane applications are also expected to work reliably. Bugs in business applications cause lost productivity (and legal risks if figures are reported incor‐ rectly), and outages of ecommerce sites can have huge costs in terms of lost revenue and damage to reputation.
Even in “noncritical” applications we have a responsibility to our users. Consider a parent who stores all their pictures and videos of their children in your photo appli‐ cation.

How would they feel if that database was suddenly corrupted? Would they know how to restore it from a backup?
There are situations in which we may choose to sacrifice reliability in order to reduce development cost (e.g., when developing a prototype product for an unproven mar‐ ket) or operational cost (e.g., for a service with a very narrow profit margin)—but we should be very conscious of when we are cutting corners.

#### 6. What is scalability?

Even if a system is working reliably today, that doesn’t mean it will necessarily work reliably in the future. One common reason for degradation is increased load: perhaps the system has grown from 10,000 concurrent users to 100,000 concurrent users, or from 1 million to 10 million. Perhaps it is processing much larger volumes of data than it did before.
Scalability is the term we use to describe a system’s ability to cope with increased load. Note, however, that it is not a one-dimensional label that we can attach to a sys‐ tem: it is meaningless to say “X is scalable” or “Y doesn’t scale.” Rather, discussing scalability means considering questions like “If the system grows in a particular way, what are our options for coping with the growth?” and “How can we add computing resources to handle the additional load?”.


## Chapter 2 Data Models and Query Languages.

#### 1. What is the goal of the relational model?
It was to hide that implementation datail behind a cleaner interface.

#### 2. What are some of the driving forces behind the adoption of NoSQL databases?

A need for greater scalability than relational databases can easily achieve, including very large datasets or very high write throughput.  

A widespread preference for free and open source software over commercial database products.  

Specialized query operations that are not well supported by the relational model.  

Frustration with the restrictiveness of relational schemas, and a desire for a more
dynamic and expressive data model.

#### 3. What is the CODASYL model and what allow us?

The CODASYL model was a generalization of the hierarchical model. In the tree structure of the hierarchical model, every record has exactly one parent; in the network model, a record could have multiple parents.

This allowed many-to-one and many-to-many relationships to be modeled.

#### 4. What are the strengths in favor of the relational database against the document databases? and vice versa

The document data model are schema flexibility, better performance due to locality, and that for some applications it is closer to the data structures used by the application.
The relational model provide better support for joins, and many-to-one and many-to-many relationships.

## Chapter 3 Storage and Retrieval.

#### 1. Hash Indexes?

Let’s start with indexes for key-value data. This is not the only kind of data you can index, but it’s very common, and it’s a useful building block for more complex indexes.
Key-value stores are quite similar to the dictionary type that you can find in most programming languages, and which is usually implemented as a hash map.

#### 2. what are the hash table limitations?

- The hash table must fit in memory, so if you have a very large number of keys, you’re out of luck. In principle, you could maintain a hash map on disk, but         unfortunately it is difficult to make an on-disk hash map perform well. It requires a lot of random access I/O, it is expensive to grow when it becomes full, and   hash collisions require fiddly logic [5].
- Range queries are not efficient. For example, you cannot easily scan over all keys between kitty00000 and kitty99999—you’d have to look up each key individu‐ ally   in the hash maps.

#### 3. How Constructing and maintaining SSTables?

Fine so far—but how do you get your data to be sorted by key in the first place? Our incoming writes can occur in any order.
Maintaining a sorted structure on disk is possible (see “B-Trees” on page 79), but maintaining it in memory is much easier. There are plenty of well-known tree data structures that you can use, such as red-black trees or AVL trees [2]. With these data structures, you can insert keys in any order and read them back in sorted order.
We can now make our storage engine work as follows:

- When a write comes in, add it to an in-memory balanced tree data structure (for
  example, a red-black tree). This in-memory tree is sometimes called a memtable.
- When the memtable gets bigger than some threshold—typically a few megabytes —write it out to disk as an SSTable file. This can be done efficiently because the     tree already maintains the key-value pairs sorted by key. The new SSTable file becomes the most recent segment of the database. While the SSTable is being         written out to disk, writes can continue to a new memtable instance.
- In order to serve a read request, first try to find the key in the memtable, then in the most recent on-disk segment, then in the next-older segment, etc.
- From time to time, run a merging and compaction process in the background to combine segment files and to discard overwritten or deleted values.
  
This scheme works very well. It only suffers from one problem: if the database crashes, the most recent writes (which are in the memtable but not yet written out  to disk) are lost. In order to avoid that problem, we can keep a separate log on disk to which every write is immediately appended, just like in the previous       section. That log is not in sorted order, but that doesn’t matter, because its only purpose is to restore the memtable after a crash. Every time the memtable is   written out to an SSTable, the corresponding log can be discarded.

#### 4. Why databases don't index everything by default?

For what reason databases don't usually index everything by default?

#### 5. what is a secondary index?

A secondary index can easily be constructed from a key-value index. The main differ‐ ence is that keys are not unique; i.e., there might be many rows (documents, vertices) with the same key. This can be solved in two ways: either by making each value in the index a list of matching row identifiers (like a postings list in a full-text index) or by making each key unique by appending a row identifier to it. Either way, both B-trees and log-structured indexes can be used as secondary indexes.

#### 6. Storing values within the index?

The key in an index is the thing that queries search for, but the value can be one of two things: it could be the actual row (document, vertex) in question, or it could be a reference to the row stored elsewhere. In the latter case, the place where rows are stored is known as a heap file, and it stores data in no particular order (it may be append-only, or it may keep track of deleted rows in order to overwrite them with new data later). The heap file approach is common because it avoids duplicating data when multiple secondary indexes are present: each index just references a location in the heap file, and the actual data is kept in one place.
When updating a value without changing the key, the heap file approach can be quite efficient: the record can be overwritten in place, provided that the new value is not larger than the old value. The situation is more complicated if the new value is larger, as it probably needs to be moved to a new location in the heap where there is enough space. In that case, either all indexes need to be updated to point at the new heap location of the record, or a forwarding pointer is left behind in the old heap location.

## Chapter 4 Encoding and Evolution.

#### 1. What are Thrift and Protocol Buffers?

Apache Thrift and Protocol Buffers (protobuf) are binary encoding libraries that are based on the same principle. Protocol Buffers was originally developed at Google, Thrift was originally developed at Facebook, and both were made open source in 2007–08.

#### 2. What is a web service?

When HTTP is used as the underlying protocol for talking to the service, it is called a web service. This is perhaps a slight misnomer, because web services are not only used on the web, but in several different contexts. 

#### 3. What is the actor model?

The actor model is a programming model for concurrency in a single process. Rather than dealing directly with threads (and the associated problems of race conditions, locking, and deadlock), logic is encapsulated in actors. Each actor typically represents one client or entity, it may have some local state (which is not shared with any other actor), and it communicates with other actors by sending and receiving asynchro‐ nous messages. Message delivery is not guaranteed: in certain error scenarios, mes‐ sages will be lost. Since each actor processes only one message at a time, it doesn’t need to worry about threads, and each actor can be scheduled independently by the framework.

#### 4. How works Data when we want to write data to a file or send it over the network?

We have to encode it as some kind of self-contained sequence of bytes. Since a pointer wouldn’t make sense to any other process, this With the exception of some special cases, such as certain memory-mapped files or when operating directly on compressed data.

