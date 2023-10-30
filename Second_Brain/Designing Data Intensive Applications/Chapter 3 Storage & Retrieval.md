
>Wer Ordnung hält, ist nur zu faul zum Suchen.
 If you keep things tidily ordered, you’re just too lazy to go searching.) 
 —German proverb

We can think of a database in simple terms, an append-only data file full of *logs*. To speed up retrieving data from a datafile we need to use an *index*. Indexes can increase the reads to our database since they help us query data faster but they slow down writes since each time we want to write to the database the index must be updated. This tradeoff is that we cannot just index everything and instead those architecting/designing the system must think carefully about what to index on based on what the typical query patterns will be to maximize the speed of reads without slowing down writes too much.

## Hash Indexes

Given a log file where we append records we can also maintain in memory a hash table whose job it is to index our data file. Given that each log follows a `key:value` syntax we can hash the keys and store the index key's value as the byte offset in the datafile. This is good for situations where there are not a lot of distinct keys so the total memory consumption is low but also where we have a lot of updates (writes).

*Compaction* means throwing away duplicate keys in the log, and keeping only the most recent update for each key by looking at all segments and pulling only the latest of each key. This is good for a segmented hash index so that we do not run out of memory in case our hash index grows too large.

![[Pasted image 20231027143652.png]]

**Pros**:
- fast because append-only on allows for sequential writes over random rights
- logs are written in sequential order so one writer thread is allowed while multiple reader threads may execute
**Cons**:
- must be kept in memory because on disk has index has many issues and so limited amount of keys can be stored
- range queries inefficient since hashing. Cannot easily scan over keys between `kitty0000` and `kitty9999`

## SSTables & LSM-Trees

### Sorted String Table (SSTable)/LSM-Tree

Sorted String Tables also known as LSM-Tree are similar to a hash index but we now require the sequence of `key:value` pairs to be *sorted by key* and that each key only appear once per segment. 

**Advantages over Hashed Index:**
- One of the main advantages is since the keys are sorted in each segment it can use a algorithm similar to merge sort to efficiently merge the segments faster than a traditional hashed index.
- Since the keys are sorted instead of maintaining all the keys in memory we only need to store a fraction of them, because they are sorted we can maintain a sparse index which still allows us to quickly jump to a key close to the key we want and simply scan after it until we find it if it is not in the sparse index.
![[Pasted image 20231027143724.png]]
- since read requests need to scan over several key-value pairs in a range we can now turn those records into a block and compress them to allow saving disk space and reduce I/O bandwidth 

*Constructing and Maintaining SSTables:*

To do so we need to use/implement a balance tree data structure such as a red-black tree or AVL tree, these in-memory trees are sometimes called *memtables*.
More on page 78.

## B-Trees

B-Trees split the index up into pages similar to how a file system separates data into pages. The tree then creates a tree of pages as shown below:

![[Pasted image 20231027151211.png]]

The number of references to child pages in one page of the B-tree is called the *branching factor*.
In practice, the branching factor depends on the amount of space required to store the page references and the range boundaries, but typically it is several hundred. As the index grows the B-Tree will split its pages if a index page hits its maximum branching factor size which ensures the tree remains balanced with a depth of O(logn).

Most databases can fit into a B-tree that is three or four levels deep, so you don’t need to follow many page references to find the page you are looking for. (A four-level tree of 4 KB pages with a branching factor of 500 can store up to 256 TB.)

To maintain data integrity generally a *write-ahead log* (WAL) is implemented alongside a B-Tree which is an append only file that tracks every write to a B-Tree so that if a crash happens during a write the B-Tree can be restored.

To protect the tree's data integrity during concurrency *latches* are used. Latches are lightweight locks that ensure protection from multiple threads writing at the same time to the same resource.

## B-Trees vs LSM-Trees

A rule of thumb is that LSM-Trees are typically faster for writes whereas B-Trees are faster for reads. Reads are typically slower on LSM-trees because they have to check several different data structures and SSTables at different stages of compaction.


*Heap File* - where a value of an index key references if the value is not the actual row/document/vertice itself. 

*Clustered Index* - an index that stores the actual row with the index key instead of referencing somewhere else like a heap file. It allows for faster reads than Heap File but incurs more overheads and thereby slower writes

*Covering Index* - a compromise between heap file and clustered index where some columns of a referenced row are stored in the index which makes reads faster when the desired columns are in the index.

Concatenated index - one that combines multiple columns by simply concatenating values like strings


Fuzzy indexes and full-text search often use the following to find words:
Edit Distance - an edit distance of 1 means that one letter has been added, removed, or replaced
*Levenshtein Distance/Automation*

Anti-Caching Approach

ACID

## Transaction Processing

**Transaction** - group of reads and writes that form a logical unit

**Transaction Processing** -  just means allowing clients to make low-latency reads and writes— as opposed to batch processing jobs, which only run periodically

OLTP (online transaction processing) - general pattern for interacting with a data store for simple application CRUD

## Analytics Processing

OLAP (online analytic processing) - pattern for interacting with a data store for data analytics 

![[Pasted image 20231030151747.png]]

Data Warehouse - a separate database used for storing data for performing data analytics. 

>OLTP systems are usually expected to be highly available and to process transactions with low latency, since they are often critical to the operation of the business. Database administrators therefore closely guard their OLTP databases. They are usually reluctant to let business analysts run ad hoc analytic queries on an OLTP database, since those queries are often expensive, scanning large parts of the dataset, which can harm the performance of concurrently executing transactions. A data warehouse, by contrast, is a separate database that analysts can query to their hearts’ content, without affecting OLTP operations

Extract-Transform-Load - the process of getting data into a data warehouse from OLTP systems which is done either with a periodic dump or continuous stream of updates

![[Pasted image 20231030152603.png]]

Star Schema - common type of schema for defining an analytics datastore given some kind o event to be used for analytics. The name “star schema” comes from the fact that when the table relationships are visualized, the fact table is in the middle, surrounded by its dimension tables; the connections to these tables are like the rays of a star.

Fact Table - the central table in a star schema centered around a type of event where each record is an event of that type that occurred, for example, each row could represent a customer's purchase of a product

Dimension Table - a table that is used to store data referenced in a star schema's fact table. As each row in the fact table represents an event, the dimensions represent the who, what, where, when, how, and why of the event.

Snowflake Schema - similar to a star schema except a start schema generally just supports a dimension table depth of 1 while a snowflake dimensions can have sub-dimension tables further normalizing the data.  Analysts prefer star since it is easier to query.

>In a typical data warehouse, tables are often very wide: fact tables often have over 100 columns, sometimes several hundred [51]. Dimension tables can also be very wide, as they include all the metadata that may be relevant for analysis

## Column-Oriented Storage

Data warehouse fact tables usually have many columns, not uncommon for there to be hundreds.

In most OLTP databases, storage is laid out in a row-oriented fashion: all the values from one row of a table are stored next to each other. Document databases are similar: an entire document is typically stored as one contiguous sequence of bytes.

The idea behind column-oriented storage is simple: don’t store all the values from one row together, but store all the values from each column together instead. If each column is stored in a separate file, a query only needs to read and parse those columns that are used in that query, which can save a lot of work.

![[Pasted image 20231030162302.png]]

The column-oriented storage layout relies on each column file containing the rows in the same order. Thus, if you need to reassemble an entire row, you can take the 23rd entry from each of the individual column files and put them together to form the 23rd row of the table.

### Column Store Compression

Column stores generally allow for efficient compression. One common way to compress in a column store is using a bitmap.

![[Pasted image 20231030162613.png]]

Often, the number of distinct values in a column is small compared to the number of rows (for example, a retailer may have billions of sales transactions, but only 100,000 distinct products). We can now take a column with n distinct values and turn it into n separate bitmaps: one bitmap for each distinct value, with one bit for each row. The bit is 1 if the row has that value, and 0 if not.

A bitwise index is very efficient for data warehouse queries and a lot of queries can be done under the hood using simple bitwise operations

We can in essence index a column store by sorting all the data based on one column being sorted or even multiple. Sorting has the benefits of improving the read speeds on common queries as well as optimize for compression. A lot of time we may store copies of the data store so why not sort each copy differently and query the one optimized for our query.

Materialized View - a precomputed table containing aggregated or joined data from base tables. Unlike regular views, which are virtual and produce results on-the-fly when queried, materialized views store their results physically, making data retrieval much faster. It is a way to cache commonly queried aggregations

Data Cube - a specialized case of a materialized view that creates a grid of aggregates grouped by different dimensions.

![[Pasted image 20231030165617.png]]

