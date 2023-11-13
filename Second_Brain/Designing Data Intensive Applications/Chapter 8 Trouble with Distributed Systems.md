Page 273

What is a partial failure?
When some parts of a system are broken in some unpredictable way while other parts work fine. These are non-deterministic, sometimes they fail, sometimes they do not which makes debugging a challenge

What is high-performance computing (HPC)?
The idea of creating super computers for intensive scientific computing tasks

>In distributed systems, suspicion, pessimism, and paranoia pay off.

>You may wonder whether this makes any sense—intuitively it may seem like a system can only be as reliable as its least reliable component (its weakest link). This is not the case: in fact, it is an old idea in computing to construct a more reliable system from a less reliable underlying base

>When driving a car, travel times on road networks often vary most due to traffic congestion. Similarly, the variability of packet delays on computer networks is most often due to queueing

Page 287

What is a time-of-day clock?
a clock that returns the current date and time according to some calendar (AKA wall clock). 

For example, `clock_gettime(CLOCK_REALTIME)` on Linux returns the number of seconds (or milliseconds) since the epoch (midnight UTC January 1, 1970)

What is a Monotonic clock?
a clock suitable for measuring duration, the actual time it presents is arbitruary and only useful for measuring how long things take by taking the difference of one or more recorded times of the clock

What is last write wins?
