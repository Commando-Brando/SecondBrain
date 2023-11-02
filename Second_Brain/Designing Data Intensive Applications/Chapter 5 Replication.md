
Shared-Memory Architecture - computer that contains any combination of multiple pieces of the same hardware (multiple CPUs, RAM chips, disks, etc...) working together and treated as one machine

The problem with a shared-memory approach is that the cost grows faster than linearly: a machine with twice as many CPUs, twice as much RAM, and twice as much disk capacity as another typically costs significantly more than twice as much. And due to bottlenecks, a machine twice the size cannot necessarily handle twice the load.

Shared-Disk Architecture - where several machines with independent CPUs and RAM store data on an array of disks that is shared between machines connected via a fast network.This architecture is used for some data warehousing workloads, but contention and the overhead of locking limit the scalability of the shared-disk approach.

Shared-Nothing Architecture - (sometimes called horizontal scaling or scaling out) have gained a lot of popularity. In this approach, each machine or virtual
machine running the database software is called a node. Each node uses its CPUs, RAM, and disks independently. Any coordination between nodes is done at the software level, using a conventional network.

What are the 2 ways data is distributed across multiple nodes?

Replication:
Keeping a copy of the same data on several different nodes, potentially in different
locations. Replication provides redundancy: if some nodes are unavailable,
the data can still be served from the remaining nodes. Replication can also help
improve performance. 

Partitioning:
Splitting a big database into smaller subsets called partitions so that different partitions
can be assigned to different nodes (also known as sharding).