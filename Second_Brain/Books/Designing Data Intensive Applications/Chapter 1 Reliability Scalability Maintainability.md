**Data Intensive Application** - one where data is its primary challenge—the quantity of data, the complexity of data, or the speed at which it is changing—as opposed to compute-intensive, where CPU cycles are the bottleneck.

>Sometimes, when discussing scalable data systems, people make comments along the
  lines of, “You’re not Google or Amazon. Stop worrying about scale and just use a
  relational database.” There is truth in that statement: building for scale that you don’t
  need is wasted effort and may lock you into an inflexible design. In effect, it is a form
  of premature optimization. However, it’s also important to choose the right tool for
  the job, and different technologies each have their own strengths and weaknesses.

**Reliability** - The system should continue to work correctly (performing the correct function at the desired level of performance) even in the face of adversity (hardware or software faults, and even human error)

**Scalability** - As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth

**Maintainability** - Over time, many different people will work on the system (engineering and operations, both maintaining current behavior and adapting the system to new use cases), and they should all be able to work on it productively

A data-intensive application is typically built from standard building blocks that provide
commonly needed functionality. For example, many applications need to:

_• Store data so that they, or another application, can find it again later (databases)_
_• Remember the result of an expensive operation, to speed up reads (caches)_
_• Allow users to search data by keyword or filter it in various ways (search indexes)_
_• Send a message to another process, to be handled asynchronously (stream processing)_
_• Periodically crunch a large amount of accumulated data (batch processing)_

## Faults

Faults - the things that can go wrong
Fault Tolerant - systems that can handle faults
Failure vs Fault - failure is when a system stops as a whole working but a fault is when a component of a system deviates from its spec

For fault tolerance it is impossible to prevent all faults therefore the focus should shift to having good fault tolerance, basically handling exceptions.

Human error is the leading cause of faults. To prevent it we need to:
- Design systems in a way that minimizes opportunities for error. For example, well-designed abstractions, APIs, and admin interfaces make it easy to do “the right thing” and discourage “the wrong thing.” However, if the interfaces are too restrictive people will work around them, negating their benefit
- Decouple the places where people make the most mistakes from the places where they can cause failures. In particular, provide fully featured non-production sandbox environments where people can explore and experiment safely, using real data, without affecting real users.
- Write good meaningful tests especially for edge cases
- Allow quick and easy recovery to minimize fault impact such as easy rollbacks and ensuring data integrity
- Set up good monitoring of systems and telemetry 

## Describing Load & Performance for Scalability

We can describe load it using a few numbers referred to as *load parameters*. For example it could be requests per second to a web server, the ratio of reads to writes in a database, the number of simultaneously active users in a chat room, the hit rate on a cache, or something else.

After defining our load parameters we can then use them to describe performance and answer the following questions:
- When you increase a load parameter and keep the system resources (CPU, memory, network bandwidth, etc.) unchanged, how is the performance of your system affected?
- When you increase a load parameter, how much do you need to increase the resources if you want to keep performance unchanged?

Think of response time not as a single number but as a distribution since a system that makes lots of requests will have varying response times.

When using percentiles p50 is the median of a dataset, p95 is the 95th percentile, p99 is 99th, and p999 is 99.9th percentile. Looking at the p50 tell us the middle ground while the >= p95 tells us more about outliers.

For example, if the 95th percentile response time is 1.5 seconds, that means 95 out of 100 requests take less than 1.5 seconds, and 5 out of 100 requests take 1.5 seconds or more.

High percentiles of response times are also known as tail latencies.


**Stateless vs Stateful Services Scaling their Data Systems**

> distributing stateless services across multiple machines is fairly straightforward, taking stateful data systems from a single node to a distributed setup can introduce a lot of additional complexity. For this reason, common wisdom until recently was to keep your database on a single node (scale up) until scaling cost or high- availability requirements forced you to make it distributed.

**Every System Must be Scaled to its Needs**

>For example, a system that is designed to handle 100,000 requests per second, each 1 kB in size, looks very different from a system that is designed for 3 requests per minute, each 2 GB in size even though the two systems have the same data throughput. An architecture that scales well for a particular application is built around assumptions of which operations will be common and which will be rare the load parameters. If those assumptions turn out to be wrong, the engineering effort for scaling is at best wasted, and at worst counterproductive. In an early-stage startup or an unproven product it’s usually more important to be able to iterate quickly on product features than it is to scale to some hypothetical future load.



