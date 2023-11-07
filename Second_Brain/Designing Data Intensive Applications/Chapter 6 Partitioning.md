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

