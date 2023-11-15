Page 321

>Is it better to be alive and wrong or right and dead? 
>—Jay Kreps, A Few Notes on Kafka and Jepsen (2013)


What is Linearizability? 
(AKA atomic consistency, immediate consistency, or external consistency)
The idea of making a distributed system with multiple copies of data, possibly with it at different stages look uniform so that to a client it looks like there is only one copy of data and that all operations on it are atomic. Essentially it is a recency  guarantee 

What is x reference in Linearizability?
a register—in practice, it could be one key in a key-value store, one row in a relational database, or one document in a document database, for example.

What is serializability?
an isolation property of transactions, where every transaction may read and write multiple objects (rows, documents, records). It guarantees that transactions behave the same as if they had executed in some serial order (each transaction running to completion before the next transaction starts). It is okay for that serial order to be different from the order in which transactions were
actually run

What replication methods are linearizable?
- Single-Leader replication (potentially)
- Consensus algorithms

What does causality mean?
noun
1.  the relationship between cause and effect.
2. the principle that everything has a cause.

What does it mean for a system to be casually consistent/
If a system obeys the ordering of processing. Make sure to process y before x if x causes y.