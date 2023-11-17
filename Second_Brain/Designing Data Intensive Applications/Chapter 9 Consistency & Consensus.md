Page 321

>Is it better to be alive and wrong or right and dead? 
>—Jay Kreps, A Few Notes on Kafka and Jepsen (2013)


What is Linearizability? 
(AKA atomic consistency, immediate consistency, or external consistency)
The idea of making a distributed system with multiple copies of data, possibly with it at different stages look uniform so that to a client it looks like there is only one copy of data and that all operations on it are atomic. Essentially it is a recency  guarantee 

What is x reference in Linearizability?
a register—in practice, it could be one key in a key-value store, one row in a relational database, or one document in a document database, for example.

What is serializability?
an isolation property of transactions, where every transaction may read and write multiple objects (rows, documents, records). It guarantees that transactions behave the same as if they had executed in some serial order (each transaction running to completion before the next transaction starts). It is okay for that serial order to be different from the order in which transactions were actually run

What replication methods are linearizable?
- Single-Leader replication (potentially)
- Consensus algorithms

What does causality mean?
noun
1.  the relationship between cause and effect.
2. the principle that everything has a cause.

What does it mean for a system to be casually consistent?
If a system obeys the ordering of processing. Make sure to process y before x if x causes y.

What is the relationship between linearizability and causality?
linearizability implies causality: any system that is linearizable will preserve causality correctly

In a single-leader causal system how can you track the ordering of reads/writes?
You can use sequence numbers or timestamps which each only consist of a few bytes

What is the atomic commit problem?
In a database that supports transactions spanning several nodes or partitions, we have the problem that a transaction may fail on some nodes but succeed on others. If we want to maintain transaction atomicity , we have to get all nodes to agree on the outcome of the transaction: either they all abort/roll back (if anything goes wrong) or they all commit (if nothing goes wrong)

 What is two-phase commit (2PC)?
 An algorithm for achieving atomic transaction commit across multiple nodes—i.e., to ensure that either all nodes commit or all nodes abort. A coordinator sends prepare requests for notes to commit a transaction in phase 1, then if the nodes agree all nodes commit in phase 2 or abort if disagree
- if coordinator crashes nodes cannot process requests

What are Database-internal distributed transactions?
Distributed databases that use replication/partitioning in their standard configuration that support internal transactions among nodes in the database.

What are Heterogeneous distributed transactions?
Where the participants of transactions are two or more different technologies in which case the the technology must be able to communicate and ensure atomic commit.

--- ANKI CARDS NEEDED BELOW ---

What is eXtended Architecture?
(X/Open XA)
a standard for implementing two-phase commit across heterogeneous technologies. It was introduced in 1991 and has been widely implemented: XA is supported by many traditional relational databases (including PostgreSQL, MySQL, DB2, SQL Server, and Oracle) and message brokers (including ActiveMQ, HornetQ, MSMQ, and IBM MQ)
- C API for interfacing with a transaction coordinator

What is the difference between using a coordinator for 2PC vs using a quorum of nodes to elect a leader and then vote on a proposal?
The biggest differences are that in 2PC the coordinator is not elected, and that fault-tolerant consensus algorithms only require votes from a majority of nodes, whereas 2PC requires a
“yes” vote from every participant. 

page 373


