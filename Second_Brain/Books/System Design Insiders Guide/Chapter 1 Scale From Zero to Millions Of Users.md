TARGET DECK: Active::System Design An Insiders Guide::C1 Scale To Million Users

**TODO:**
Topics to read more about:
- read caching strategies article linked at end of chapter, reference #6
- How does dynamic caching work with CDNs?
- What are some of the No-SQL use cases? Refer to reference 14

Q: When scaling why move your database from your single server to its own server?
A: So you can scale the database independently from the server
<!--ID: 1722433944518-->


Q: Why is it good to put load balancers in between your servers and your clients:
A:     - Load is balanced between your servers which you want when you have more than one server
- Servers can be further protected by using private IPs only accessible to load balancer
- Makes adding servers easy because the load balancer only needs to know about the new servers to start sending requests
<!--ID: 1722433944530-->


Q: What is a read-through cache?
A:  When a cache lookup is performed, if cache hit the data is returned, if cache miss then the data is queried for in the database which is used to refresh the cache and then return the data to the client
<!--ID: 1722433944535-->



Q: When to use a cache?
A:  - Use when data is read frequently but modified infrequently
- The data stored does not need to be persisted so cache system should not disrupt system if it fails and cache is flushed
<!--ID: 1722433944538-->


Q: What is a cache expiration policy?
A: - What determines that the cache data should be evicted, for example, we consider and remove values from the cache if they have been there an hour
- Determining an appropriate policy is based on your application needs but you want to balance keeping data in your cache and your tolerance for stale data
<!--ID: 1722433944541-->


Q: What is a cache eviction policy?
A: - If the cache becomes full based on the defined memory constraints how do you remove cache entries. 
- Least recently used (LRU) is the most popular policy. Least frequently used (LFU) and First in First out (FIFO) are common
<!--ID: 1722433944545-->


Q: What is a CDN?
A: - Content Delivery Network
- Primarily used to deliver static content cached on CDN servers such as images, videos, CSS, JavaScript files, etc
- Can also serve up static content
<!--ID: 1722433967512-->


Q: What is a stateful server?
A: Where a systems servers contain state, for example, 3 web servers in a system may each be serving a different customer and storing each customers state on the serving machine. 
- Load balancer configured for sticky sessions can help with this
- Difficulties for scaling out or handling failures
__
![[Pasted image 20240608182145.png]]
<!--ID: 1722433944550-->


Q: What is a stateless server?
A: - One where state such as user sessions for a web server are not stored on the server but persisted to a data store so that should a server go down the users session is not affected and another web server can pick up where a failed web server left off.
- Good for scaling out
__
![[Pasted image 20240608182228.png]]
<!--ID: 1722433944552-->


Q: What does geoDNS-routed mean?
A: - AKA geo-routed
- If you have servers in multiple data centers a request can be geo-routed, meaning it get routed to the server in the data center *closet* to the user
- Can also define traffic splits, 50% of users route to US West, 50% to US East
- If significant data outage occurs in a data center the traffic split could me modified ot 100% US West
__
 ![[Pasted image 20240608182755.png]]
<!--ID: 1722433944555-->


Q: What are the main challenges associated with scaling out to multiple data centers?
A: - Effective tools are needed to direct traffic to the correct data center. GeoDNS can be used to direct traffic to the nearest data center depending on where a user is located.
- Data synchronization: Users from different regions could use different local databases or caches. In failover cases, traffic might be routed to a data center where data is unavailable. A common strategy is to replicate data across multiple data centers. A previous study shows how Netflix implements asynchronous multi-data center replication. **TODO:** book references figure 11 put link here
- Test and deployment: With multi-data center setup, it is important to test your website/application at different locations. Automated deployment tools are vital to keep services consistent through all the data centers.
<!--ID: 1722433944557-->


Q: What is a message queue?
A: - a system component stored in memory that serves as a buffer that facilitates the distribution of asynchronous requests
- Architecture consists of producers/publishers creating messages and publishing them to a message queue while other services/servers (consumers/subscribers) connect to the queue and perform actions defined by the messages
- Consumer workers can be scaled based on demand
__
![[Pasted image 20240608183926.png]]
<!--ID: 1722433944560-->



Q: Consider the following scenario: your application supports photo customization, including cropping, sharpening, blurring, etc. These are not your typical personal device editing tasks and the customization tasks take time to complete. What software system component is an ideal solution?
A: - A message queue because it can queue the job and process it whenever a consumer/subscriber is ready/available to handle it
__
![[Pasted image 20240608184832.png]]
<!--ID: 1722433944566-->


Q: What are the tradeoffs for scaling up your database?
A: - Pros:
	- Simple and easy to manage database layer
	- Suitable for small businesses
- Cons:
	- Single point of failure
	- Clients far from database server may incur high latency
	- Cost gets very high, single beefy server is more expensive than multiple smaller servers
<!--ID: 1722433944568-->


Q: What is horizontal scaling?
A: AKA sharding or partitioning 
- Separates large databases into smaller, more easily managed parts called shards. 
- Each shard shares the same schema, though the actual data on each shard is unique to the shard.
- Pros:
	- Redundancy across multiple servers and possible multiple data centers
	- Low latency for clients making queries
	- Cheaper than vertical scaling at a certain point
- Cons:
	- Significant overhead in designing/managing a distributed system
__
![[Pasted image 20240608191000.png]]
<!--ID: 1722433944571-->


Q: What is a sharding key? Why is it important?
A: - A sharding key a column or multiple columns used to determine how data is sharded in a distributed database system
- Most important factor to choose when choosing sharding strategy
- The key should be chosen based on its ability to evenly distribute data across shards since it is used to determine what shard the data is stored
<!--ID: 1722433944573-->


Q: Why re-shard data?
A: - A single shard could no longer hold more data due to rapid growth
- Certain shards might experience shard exhaustion faster than others due to uneven data distribution. When shard exhaustion happens, it requires updating the sharding function and moving data around. Consistent hashing is a common solution for this
<!--ID: 1722433944576-->


Q:  In Sharding what is the celebrity problem?
A: - When a specific data point like a celebrity user incurs significantly more reads/writes to their shard which may overload the shard, this is known as a hotspot
- A celebrity may require their own shard
<!--ID: 1722433944579-->


Q: In sharding why does de-normalization occur?
A: - Once a database has been sharded across multiple servers, it is hard to perform join operations across database shards. 
- A common workaround is to denormalize the database so that queries can be performed in a single table.
<!--ID: 1722433944584-->




- What is write-through cache?