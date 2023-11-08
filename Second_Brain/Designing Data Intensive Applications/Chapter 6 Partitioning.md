>Clearly, we must break away from the sequential and not limit the computers. We must state definitions and provide for priorities and descriptions of data. We must state relationships, not procedures. 
>—Grace Murray Hopper, Management and the Computer of the Future (1962)

Partitioning is usually combined with replication so that copies of each partition are
stored on multiple nodes. This means that, even though each record belongs to
exactly one partition, it may still be stored on several different nodes for fault tolerance.

A node may store more than one partition. If a leader–follower replication model is
used, the combination of partitioning and replication can look like Figure 6-1. Each
partition’s leader is assigned to one node, and its followers are assigned to other
nodes. Each node may be the leader for some partitions and a follower for other partitions.

![[Pasted image 20231107110905.png]]

What does it mean if your partitions are skewed?
That some nodes have much more data & queries than others

What is a partition hotspot?
A partition with a disproportionally high load

What methods are used for relieving hotspots?
- Partitioning by key range (keys a-c in partition 1, d-f partition2, etc...)
- Partitioning by hash of key

What is key range partitioning?
- keys are sorted
- partition owns all keys from some minimum to maximum (think range)
- sorting is good for range queries but prone to hotspots
- generally rebalanced dynamically - splitting range into 2 subranges 

What is hash partitioning?
- hashes each key and partition owns range of hashes
- range queries inefficient since no ordering
- good at avoiding hotspots
- fixed partitioning is mostly used and sometimes dynamic 

What are the 2 ways of partitioning a database if secondary keys are involved?
- document-based partitioning 
- term-based partitioning

In database partitioning what is document-based partitioning?
(local indexes)
where the secondary indexes are stored in the same partition as the primary key and value. This means that only a single partition needs to be updated on write, but a read of the secondary index requires a scatter/gather across all partitions.
- all partitions need to be queried for there secondary indexes which can lead to tail latency amplification

In database partitioning what is term-based partitioning?
(global indexes), where the secondary indexes are partitioned separately, using the indexed values. An entry in the secondary index may include records from all partitions of the primary key. When a document is written, several partitions of the secondary index need to be updated; however, a read can be served from a single partition.

What are the tradeoffs between term-based vs document-based partitioning?
term-based makes reads faster since only one partition needs to be read from but is slower on writes since it has to update the whole index. Sometimes those writes have to be done asynchronously as well

What is partition rebalancing?
Whenever nodes are added/removed from a database system that is partitioned the partitions must somehow still be evenly distributed in the nodes

What fixed-size partitioning?
A partitioning rebalancing solution for hashed key partitioning where the partitions are divided into a fixed number that is greater than the amount of nodes. Then if a node is added it can easily steal some partitions in existing nodes. This is much more efficient than having to increase the number of partitions when new nodes are added.

![[Pasted image 20231108115435.png]]

What is dynamic database partitioning?
A partitioning rebalance strategy ideal for key-range partitioning configurations where similar to a B-Tree partitions can be split in half or merged together to evenly distribute them when nodes are added/removed

What is proportional database partitioning?
Where each node has a fixed number of partitions for example 5 partitions per node

Should database partition rebalancing be done automatically or manually?
While automatic rebalance is convenient, rebalancing must be done with care and if rebalancing is done at a bad time it could cause a cascading effect of failures in a system so some human involvement is generally recommended

How do systems handle routing requests to the correct partition?
- random round robin scheme
- a routing tier that maintains knowledge of the nodes/partitions and routes requests to the right place, basically a proxy service
- the client needs to be aware of the nodes and can send the request to the correct node
![[Pasted image 20231108123713.png]]

![[Pasted image 20231108123735.png]]


What are massively parallel processing products?
Relational database products used for data analytics that support parallelization 

