Page 273

What is an NTP client?

Key points:
- networks are super challenging to deal with especially in distributed systems
	- maybe things can go wrong
	- even with TCP it can be challenging to determine when a server in a client-server model is down
- system clocks are unreliable and handling considerations need to be made in order to align things that rely on clocks

What is a partial failure?
When some parts of a system are broken in some unpredictable way while other parts work fine. These are non-deterministic, sometimes they fail, sometimes they do not which makes debugging a challenge

What is high-performance computing (HPC)?
The idea of creating super computers for intensive scientific computing tasks

>In distributed systems, suspicion, pessimism, and paranoia pay off.

>You may wonder whether this makes any sense—intuitively it may seem like a system can only be as reliable as its least reliable component (its weakest link). This is not the case: in fact, it is an old idea in computing to construct a more reliable system from a less reliable underlying base

>When driving a car, travel times on road networks often vary most due to traffic congestion. Similarly, the variability of packet delays on computer networks is most often due to queueing

Page 287