>A system cannot be successful if it is too strongly influenced by a single person. Once the initial design is complete and fairly robust, the real test begins as people with many different viewpoints undertake their own experiments.
>—Donald Knuth

What are the 2 main ways to broadly group at a high level systems that store and process data?
- Systems of record
	(AKA the source of truth)
	holds the authoritative version of your data. When new data comes in, e.g., as user input, it is first written here.  Each fact is represented exactly once (the representation is typically normalized).   If there is any discrepancy between another system and the system of record,   then the value in the system of record is (by definition) the correct one
- Derived data systems
	Data in a derived system is the result of taking some existing data from another system and transforming or processing it in some way. If you lose derived data, you can recreate it from the original source. A classic example is a cache: data can be served from the cache if present, but if the cache doesn’t contain what you need, you can fall back to the underlying database.

What are the 3 main kinds of systems?
- Services (online systems)
- Batch Processing Systems (offline systems)
- Stream processing systems (near-real-time systems)

What kind of a system is a service?
An online system where the service system waits for a request or instruction from a client to arrive. When one is received, the service tries to handle it as quickly as possible and sends a response back. Response time is usually the primary measure of performance of a service, and availability is often very important

What is a Batch Processing system?
A batch processing system takes a large amount of input data, runs a job to process it, and produces some output data. Jobs often take a while (from a few minutes to several days), so there normally isn’t a user waiting for the job to finish. Instead, batch jobs are often scheduled to run periodically (for example, once a day). The primary performance measure of a batch job is usually throughput

What is a Stream Processing system?
Stream processing is somewhere between online and offline/batch processing (so it is sometimes called near-real-time or nearline processing). Like a batch processing system, a stream processor consumes inputs and produces outputs (rather than responding to requests). However, a stream job operates on events shortly after they happen, whereas a batch job operates on a fixed set of input data. This difference allows stream processing systems to have lower latency than the equivalent batch systems

--- ANKI CARDS NEEDED FOR BELOW ---

What is MapReduce?
A batch processing algorithm published in 2004 which is a low-level programming model.

What is the working set of a job?
The amount of memory to which the job needs random access. For example, to process 64 bytes of log files quickly a program may need to read all 64 bytes into memory which would represent its working set.

What does the Balkanization of data mean?
It means that your data becomes silo'd and difficult to make work together, from when the Ottoman empire fell and the conflicting Balkan nation-states emerged.

How is the efficiency of writing a traditional programming language app to perform data operations on say Linux log files compared to that of using GNU utilities?
GNU utilities quickly out perform programming languages for what it is capable of because it is optimized for concurrency and reading from disk

What does the Unix philosophy encourage for the input/output of apps?
Expect the output of every program to become the input to another, as yet unknown, program. Don’t clutter output with extraneous information. Avoid stringently columnar or binary input formats. Don’t insist on interactive input.

What is MapReduce?
MapReduce is a programming framework with which you can write code to process large datasets in a distributed filesystem like Hadoop File System (Distributed file system).

How does the Mapper in MapReduce behave?
- called once for every input record
- goal to extract key/value from input record
- for each input may generate 0, 1, or multiple key-value pairs
- no state kept between processing each record

At a high level how do you implement MapReduce?
- you implement it using 2 callbacks functions, the Mapper & Reducer
- the data gets sorted between the mapper/reducing callbacks

How does the Reducer in MapReduce behave?
- takes in key-value pairs from mapper
- groups all the values belonging to the same key
- calls the reducer with an iterator over the collection of values
- produces output records

What is the main difference between using Unix tools and MapReduce?
MapReduce can parallelize a computation across multiple machines, without you having to write code to   explicitly handle the parallelism

What are MapReduce workflows?
Chains of MapReduce processes that take the output of a job and pipes it to another. 

What is a full table scan?
Whenever a database reads from a table and reads all records which is much more computationally expensive than a index lookup

What is a secondary sort in MapReduce?
a technique used in MapReduce where records are sorted by a primary key (e.g., user ID) and then by a secondary key (e.g., timestamp) within each primary key group. This method ensures that related records, such as user data and their corresponding activity events, become adjacent in the reducer's input

What is sort-merge join?
using MapReduce to sort records from 2 different tables on their linking key and then merge them using the reducer

What is sessionization?
collating all the activity events for a particular  
user session, in order to find out the sequence of actions that the user took
For example, such analysis could be used to work out  
whether users who were shown a new version of your website are more likely to make  
a purchase than those who were shown the old version (A/B testing), or to calculate  
whether some marketing activity is worthwhile.

Page 411