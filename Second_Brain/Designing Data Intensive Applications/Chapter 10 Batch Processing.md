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