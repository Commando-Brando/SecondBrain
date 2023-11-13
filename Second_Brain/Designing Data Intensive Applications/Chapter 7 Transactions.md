Page 221

What does ACID stand for?
Atomicity, Consistency, Isolation, and Durability

In ACID what is the A mean and describe?
(Atomicity)
The guarantee that if something goes wrong when executing SQL commands within a transaction that it can be aborted and any changes already executed in that transaction will be rolled back

In ACID what is the C mean and describe?
(Consistency)
consistency refers to an application-specific notion of the database being in a “good state. which is not a guarantee the database makes but one that is up to the application

In ACID what is the I mean and describe?
(Isolation)
ensures that transactions are processed independently and changes made in one transaction are not visible to other transactions until that transaction is committed.


In ACID what is the D mean and describe?
(Durability)
the promise that once a transaction has committed successfully, any data it has written will not be forgotten, even if there is a hardware fault or the database crashes.
- single node databases it means data is written to disk and write ahead log for recovery 
- multi-node database means usually some number of nodes have been written to

What is a multi-object transaction?
Modifying several different objects (rows, documents, records) in a transaction
- statements in transaction differentiated between clients usually by TCP connection

In ACID what is weak isolation?
Traditional isolation for transaction can be costly performance-wise so a lot of databases use weak isolation which loosens the rules which increases performance but also increases the chances for transaction faults

What is ACID read-committed isolation?
The most basic level of transaction isolation is read committed It makes two guarantees:
1. When reading from the database, you will only see data that has been committed
(no dirty reads).
2. When writing to the database, you will only overwrite data that has been committed
(no dirty writes).

What is ACID snapshot isolation?
(AKA Repeatable Read Isolation)
Snapshot isolation is a concurrency control method in databases, ensuring that all reads made in a transaction will see a consistent snapshot of the database as it was at the beginning of the transaction, thereby satisfying the Isolation property of the ACID principles without locking data.
- writes not block by reads - reads not blocked by writes


In the context of transactions what is a Phantom read?
A transaction reads objects that match some search condition. Another client makes a write that affects the results of that search. Snapshot isolation prevents straightforward phantom reads, but phantoms in the context of write skew require special treatment, such as index-range locks.

What is materializing conflicts in transactions?
an approach to dealing with phantoms where we use locks to lock rows that are used for the select part of the transaction until the transaction completes or it `update` step does.

What does it mean for something in programming to be non-deterministic?
Whenever something we are executing like an algorithm or function does not always produce the same output each time

Why do some databases serially execute transactions?
Some databases can produce high throughput on a single CPU core if transactions are short and fast to execute which is common in OLTP systems, limited to use cases where the active dataset can fit in memory

In database transaction what are lost updates?
Two clients concurrently perform a read-modify-write cycle. One overwrites the other’s write without incorporating its changes, so data is lost. Some implementations of snapshot isolation prevent this anomaly automatically, while others require a manual lock (SELECT FOR UPDATE)

In database transaction what is a write skew?
A transaction reads something, makes a decision based on the value it saw, and writes the decision to the database. However, by the time the write is made, the premise of the decision is no longer true. Only serializable isolation prevents this anomaly.

What are the 3 main ways of implementing serialized transactions?
- Literally executing transactions in a serial order
- Two-phase locking
- Serializable snapshot isolation (SSI)

