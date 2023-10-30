**Reliability** - making systems work correctly, even when faults occur. Faults can be in hardware (typically random and uncorrelated), software (bugs are typically systematic and hard to deal with), and humans (who inevitably make mistakes from time to time). Fault-tolerance techniques can hide certain types of faults from the end user. 

**Scalability** - having strategies for keeping performance good, even when load increases. In order to discuss scalability, we first need ways of describing load and performance quantitatively. We briefly looked at Twitter’s home timelines as an example of describing load, and response time percentiles as a way of measuring performance. In a scalable system, you can add processing capacity in order to remain reliable under high load

**Maintainability** - it’s about making life better for the engineering and operations teams who need to work with the system. Good abstractions can help reduce complexity and make the system easier to modify and adapt for new use cases. Good operability means having good visibility into the system’s health, and having effective ways of managing it

**Throughput** - the number of records we can process per second, or the total time it takes to run a job on a dataset of a certain size

**Latency** -  the duration that a request is waiting to be handled—during which it is latent, awaiting service

**Response Time** - how long it takes from the second a request is made to when the client receives a response

**Tail Latencies** - the high percentiles for response times

**Tail Latency Amplification** - whenever a user request must go through multiple back-end calls each call has a chance of being a slow one which means the more calls the higher the chance and proportion of slow requests

**SLA (Service Level Agreement)** - the agreement you make with your clients or users

**SLO (Service Level Objectives)** - the objectives your team must hit to meet that SLA agreement

**SLI (Service Level Indicators)** - the real numbers on your performance

**Head-Of-Line-Blocking** - when a small number of slow requests take over resources such as CPU cores so subsequent fast request are blocked thereby bottlenecking a system

**Vertical Scaling** - moving your current machine to a more powerful machine

**Horizontal Scaling** - distributing your load across multiple smaller machines

**Elastic** - a system is elastic whenever it can automatically add computing resources when they detect an increase in load. Elastic systems are good for when the load is highly unpredictable but better to manually scale otherwise since elasticity requires more complexity


**Functional Requirements** - what it should do, such as allowing data to be stored, retrieved, searched, and processed in various ways

**Non-Functional Requirements** - (general properties like security, reliability, compliance, scalability, compatibility, and maintainability). In this chapter we discussed reliability, scalability, and maintainability in detail. 

**Memtable** 

**Bloom Filter** - a memory-efficient data structure for approximating the contents of a set. It can tell you if a key does not appear in the database, and thus saves many unnecessary disk reads for nonexistent keys.

Hashed Index
- Compaction
- Segment File
SSTable/LSM-Tree

*Heap File* - where a value of an index key references if the value is not the actual row/document/vertice itself. 

*Clustered Index* - an index that stores the actual row with the index key instead of referencing somewhere else like a heap file. It allows for faster reads than Heap File but incurs more overheads and thereby slower writes

*Covering Index* - a compromise between heap file and clustered index where some columns of a referenced row are stored in the index which makes reads faster when the desired columns are in the index.

Apache Lucene

Fuzzy Index

*Levenshtein Distance/Automation*

B-Tree
Fractal Tree - a B-Tree variant that borrows some log-structured ideas to reduce disk seeks

Red-Black Tree
AVL Tree
B-Tree

Full-Text Search
Postings List/Inverted Index

Elastic Search

Transaction processing

Stateful

Stateless

## Key Value Stores

*Memcached*

*Redis*