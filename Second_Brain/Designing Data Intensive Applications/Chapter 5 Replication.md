
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

Each node that stores a copy of the database is called a replica.

What is a replica? A replica is a node in a system that keeps a copy of the same data as other nodes. If some nodes are unavailable, the data can still be served from the remaining nodes. Replication can also help improve performance. 

What is Leader-Based Replication? 
- database write requests write to the leader/master first which goes to the replication log and then every follower/slave writes based on replication log
- clients that want to read from the database can query leader or follower but only leader accepts write requests
- followers generally are written to asynchronously or in a semi-synchronous configuration 

In leader-based replication what is the tradeoff between a asynchronous configuration vs a semi-synchronous configuration?

Semi-synchronous gives your writes more durability in case a leader goes down whereas the asynchronous configuration has less write durability but can still process write efficiently even if all its followers have fallen behind. 

Weakening durability may sound like a bad trade-off, but asynchronous replication is
nevertheless widely used, especially if there are many followers or if they are geographically distributed

![[Pasted image 20231102122042.png]]

Generally you do not want to only have synchronous follower replicas because that means if one dies then the whole system is blocked until it is available again. Best practice dictates all follower replicas be asynchronous or follow the configuration known as semi-synchronous.

In Leader-based Replication what is the semi-synchronous configuration?

The  semi-synchronous configuration is where one follower replica is synchronous so that whenever the leader gets a new write it always will have one immediate successful write to a follower which can then serve as a backup for the leader. If the synchronous follower becomes unavailable or slow an async follower can take its place and become synchronous. 

How does a leader node set up new followers in Leader-Based Replication?

The practical steps for each database may vary but generally:
- Consistent snapshots are taken of the leader's database at some points in time, ideally without locking a database and stopping writes.
- Copy snapshot to new follower node
- New follower connects to leader and then using some kind of database log identify the difference between the snapshot and leader's current state and then it catches up by implementing those writes

In Leader-Based Replication how do follower nodes handle outages?

Follower nodes follow a process called catch-up recovery, they keep a log locally of all writes to be processed received by the leader so that if they go down to due to updates, network problems, or some error/crash it can recover quite easily from its log and then catch up to the leader.

In Leader-Based Replication how do leader nodes handle outages?
A process called failover follows these steps:
- A follower must be appointed as leader usually the one with the most up-to-date changes
- clients need to reconfigure to send writes to new leader
- other followers need to switch to consuming data changes from the new leader
- failover can be automatically or manually done


What are some of the common faults that can happen during failover in Leader-Based Replication?
- in an fully async replica system no followers might be fully up to date with the dead leader
- in certain scenarios two nodes may think they are the leader which is a situation called split brain and can be very dangerous
- determining leader failover timeout is difficult cause can increase recovery time with high timeout but low timeout means unnecessary failovers in case a leader just takes long to respond


Replication implementations:
1. Statement-based:
    - Ship the insert/update/delete statements.
    - Issues:
        - Non-deterministic functions, like rand().
        - Autoincrement columns.
        - Side-effect functions.
2. Write-ahead log shipping:
    - Issue: Tightly coupled to storage format.
        - Operational concerns if the storage format changes between versions.
    - PostgreSQL, Oracle.
3. Local (row-based) log:
    - Specific log format for replication.
    - MySQL binlog.
    - Allow easier change-data-capture.
4. Trigger-based replication:
    - Custom logic, flexible.
    - Issues:
        - Bigger overhead.
        - Bug prone.

In Leader-Based replication what is eventually consistency mean?
The idea that in a busy system if you read from the leader and a follower at the same time then you will will get slightly different results since the follower is still catching up but if writes stop to the leader the followers will eventually catch up.

What is replication lag mean in leader-based replication?
replication lag is how far a follower is behind on writes compared to its leader

What is read-after-write consistency mean in leader-based replication?
The idea that after a user writes changes that he should be able to view they should be able to view those changes immediately because otherwise the user may be confused and think their change was lost. It mays promises for the user making the change and not that they will see the most recent change from other users. Can be implemented in very ways depending on the use case.

What are monotonic reads in leader-based replication?
A process that guarantees a user making multiple reads in a row won't have each request go to each replica because the later replicas could be further behind the first replicas leading to the user seeing data going backwards in time.

What are consistent prefix reads in leader-based replication?

A problem for sharded databases where multiple writes going to different shards are processed in different orders than the order that the requests were made. If people are text chatting and their messages go to different shards, the person's reply may be processed first so when it is read the reply whos up before the question. One possible solution is to make sure causally related writes are sent to the same replica.

## Multi-Leader Replication

- tries to solve the problem of one leader write bottleneck
- also known as master-master or active/active replication
- rarely makes sense to use a multi-leader setup within a single data center because the benefits rarely outweigh the added complexity

Pros:
- performance increase perceived by user
- no need for failover from follower to leader if one data center goes down other leaders still exist'
- better tolerate network problems better
- good for systems that need to continue to work offline
Cons:
- require conflict resolution system for writing between leaders which has some serious pitfalls with auto-incrementing keys, triggers, and integrity constraints
- significant additional system complexity
- hard to get right, infamously difficult
- hard to deal with 2 users writing to change the same thing at the same time

What is Real-time collaborative editing?
Applications that allow several people to edit a document simultaneously. Think google docs

How to avoid conflicts in a multi-leader based system?

For a given record or set of records, route all the data to the same leader, perhaps whichever is closet to the user. If the user moves to a different location or their local leader fails then conflict avoidance may break down.

How do multi-leader frameworks approach custom conflict resolution?

For writes generally they let you write some custom application code to resolve the conflict but these are fast and done in the background without any user prompt

For reads we can write application code and/or send the records and their versions to the user for them to decide how to resolve the conflict

Are there good automatic conflict resolution processes?

Yes there are some but for niche use cases that have not been implemented in data store solutions yet. One of them is Operational Transformation designed particularly for concurrent editing of an ordered list of items, such as the list of characters that constitute a text document and is used by collaborative text editing system like google docs. 

Others to explore
- Mergeable persistent data structures
- Conflict-free replicated datatypes (CRDTs)

What is a replication topology?

a design that describes the communication paths along which writes are propagated from one node to another





