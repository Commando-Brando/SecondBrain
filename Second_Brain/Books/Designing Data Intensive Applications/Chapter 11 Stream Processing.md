A complex system that works is invariably found to have evolved from a simple system that
works. The inverse proposition also appears to be true: A complex system designed from
scratch never works and cannot be made to work.
—John Gall, Systemantics (1975)

In stream processing what is an event?
A record of something happening, could be represented in but not limited to plain text, human readable encoding, or binary encoding

In stream processing how are related events group together?
Related groups are into a topic or stream, subscribers sometimes can subscribe to a subset of events based on a pattern

What is polling?
Whenever some consumer service in a system makes a request at intervals to see if their is something to be consumed

What is a messaging system?
(publish/subscribe)
A stream processing system where events notify its consumers of its existence so the consumers do not need to constantly poll which can be more resource intensive 

In a publish/subscribe model what is the backpressure approach?
(Unix pipes & TCP)
If producers are publishing events faster than subscriber services can process the events than backpressure is where the producers are not allowed to send events until the subscribers can catch up

In a distributed stream processing system how is the workload distributed when their are multiple consumers subscribed to a topic?
- load balancer is used
- each message only goes to one consumer
- allows system to in a way parallelize work across subscribers

![[Pasted image 20231122140159.png]]

In a multi-consumer stream processing system what is fan-out?
Where each message is delivered to all consumers, allowing independent consumers to each "tune in" to the same broadcast of messages without effecting each others

In a distributed stream processing system how can fan-out and load balancing be used together?
You can groups of consumers that subscribe to a topic where each message is always sent to all the groups but within the group the processing is load balanced

In stream processing systems how can a message broker ensure that a message is not lost?
It can use acknowledgements, where a client must explicitly tell the broker when it has finished processing a message so that the broker can remove it from their queue

What is a log based message broker?
An approach to stream processing where the message broker tries to have the durable storage of databases and the low-latency notification facilities of messaging by implementing logs
- logs can be partitioned 
- a topic can be defined as a group of partitions

What is change data capture?
(CDC)
the process of observing all data changes written to a database and extracting the in a form in which they can be replicated to other systems. 

![[Pasted image 20231122152427.png]]

What is event sourcing?
- stores data in an append only log
- log records are focused on expressing the intent of a user action over the mechanics of it 
- stores all database operations providing a history of queries being executed
- similar to change data capture 

>Transaction logs record all the changes made to the database. High-speed appends are the only way to change the log. From this perspective, the contents of the database hold a caching of the latest record values in the logs. The truth is the log. The database is a cache of a subset of the log. That cached subset happens to be the latest value of each record and index value from the log.
- Pat Helland

What is command query responsibility segregation (CQRS)?
The idea behind CQRS is to separate the form in which data is written from the form is is read. By primarily writing to an event log we can read the data from that log and create different independent read views

What is the biggest downside to event sourcing and change data capture?
That the reading views generally operate asynchronous so there is a chance that a user will make a write and then an immediate read that does not reflect the write

What is the main disadvantage of stream processing compared to batch processing for fail over?
Batch processing jobs when failed can simply restart but that might not be possible for stream processing jobs

What are complex event processing systems?
Systems designed to be able to query and identify events that match a specific criteria. Instead of persisting the events and the queries being transient, the queries are persisted and the events are transient. Only whenever an event matches a pattern in the same vane as a regex match does it return and event to the user

What are stream analytics systems?
Systems designed to perform analytics on streams - performing aggregations or statistical metrics over a large number of events. 
For example:
- Measuring the rate of some type of event (how often it occurs per time interval)
- Calculating the rolling average of a value over some time period

What is a time interval over which an aggregation is done known as?
A window

How does searching on streams work?
Queries are persisted and data on a event is returned once an event that matches a query criteria is found. If there are many queries an optimization could be to build an index out of the queries themselves so every query does not need to be checked against every event

What is a tumbling windows?
- fixed length
- every event belongs to only one window
For example a 1 minute tumbling window, all the events with timestamps between 10:03:00 and 10:03:59 are grouped into one window, events between 10:04:00 and 10:04:59 into the next window, and so on

What is a hopping window?
- fixed length
- windows can overlap for smoothing
For example, a 5-minute window with a hop size of 1 minute would contain the events between 10:03:00 and 10:07:59, then the next window would cover events between 10:04:00 and 10:08:59, and so on

What is a sliding windows?
- contains all the events that occur within some interval of each other
For example, a 5-minute sliding window would cover events at 10:03:39 and 10:08:12, because they are less than 5 minutes apart (note that tumbling and hopping 5-minute windows would not have put these two events in the same window, as they use fixed boundaries).

What is a session window?
- no fixed duration
- defined by grouping events for the same user that occur closely in time together

What is a stream-stream join?
(window join)
- joining 2 or more types of activity events via some key
- index on the join key
- maintain the state of the index

What does streaming event enrichment mean?
Joining data from some data source to an event

What is a stream-table join?
Joining a stream event with some persisted datastore table that must be retrieved. The data can either be loaded into memory for fast access or requests each time from some datastore

What is table-table join?
(materialized view maintenance)
- both input streams are database changelogs
- every change on one side is joined with the latest state of the other side
- output is a stream of changes to the materialized view of the join between the 2 tables

What is microbatching?
Whenever you break a stream into small blocks to be processed like batch processes
- batch size is typically around 1 second

What is an idempotent operation?
one that you can perform multiple times, and it has the same effect as if you performed it only once. For example, setting a key in a key-value store to some fixed value is idempotent (writing the value again simply overwrites the value with an identical value), whereas incrementing a counter is not idempotent (performing the increment again means the value is incremented twice)