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

pg461

What 