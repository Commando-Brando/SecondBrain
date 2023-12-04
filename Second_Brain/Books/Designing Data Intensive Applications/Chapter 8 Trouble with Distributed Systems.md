Page 273

What is an NTP?
(Network Time Protocol)
a protocol that allows the synchronization of system clocks. In client-server architectures there can be NTP servers which serve to help synchronize clocks between clients.

Key points:
- networks are super challenging to deal with especially in distributed systems
	- maybe things can go wrong
	- even with TCP it can be challenging to determine when a server in a client-server model is down
- system clocks are unreliable and handling considerations need to be made in order to align things that rely on clocks
- A process may pause for a substantial amount of time at any point in its execution (perhaps due to a stop-the-world garbage collector), be declared dead by other nodes, and then come back to life again without realizing that it was paused.
- What properties should our distributed system have? The third half of the chapter describes some of the many considerations for defining the non-functional requirements of our system

What is a partial failure?
When some parts of a system are broken in some unpredictable way while other parts work fine. These are non-deterministic, sometimes they fail, sometimes they do not which makes debugging a challenge

What is high-performance computing (HPC)?
The idea of creating super computers for intensive scientific computing tasks

>In distributed systems, suspicion, pessimism, and paranoia pay off.

>You may wonder whether this makes any sense—intuitively it may seem like a system can only be as reliable as its least reliable component (its weakest link). This is not the case: in fact, it is an old idea in computing to construct a more reliable system from a less reliable underlying base

>When driving a car, travel times on road networks often vary most due to traffic congestion. Similarly, the variability of packet delays on computer networks is most often due to queueing


What is a time-of-day clock?
a clock that returns the current date and time according to some calendar (AKA wall clock). 

For example, `clock_gettime(CLOCK_REALTIME)` on Linux returns the number of seconds (or milliseconds) since the epoch (midnight UTC January 1, 1970)

What is a Monotonic clock?
a clock suitable for measuring duration, the actual time it presents is arbitrary and only useful for measuring how long things take by taking the difference of one or more recorded times of the clock

Thus, even though it is tempting to resolve conflicts by keeping the most “recent”
value and discarding others, it’s important to be aware that the definition of “recent”
depends on a local time-of-day clock, which may well be incorrect. Even with tightly
NTP-synchronized clocks, you could send a packet at timestamp 100 ms (according
to the sender’s clock) and have it arrive at timestamp 99 ms (according to the recipient’s
clock)—so it appears as though the packet arrived before it was sent, which is
impossible.

How does garbage collection effect system clocks?
Occasionally garbage collection must pause all threads to garbage collect which and mess with the application's sense of time with the CPU clock making time use less reliable

What is a real-time operating system?
allows processes to be scheduled with a guaranteed allocation of CPU time in specified intervals is needed; library functions must document their worst-case execution times; dynamic memory allocation may be restricted or disallowed entirely (real-time garbage collectors exist, but the application must still ensure that it doesn’t give the GC too much work to do); and an enormous amount of testing and measurement must be done to ensure that guarantees are being met.

Why is it important to design a leader writing locking mechanism in a leader-based distributed system?
If a declared dead leader by a quorum of nodes but it still thinks its the leader and it still has write access then it could cause problems in the system/data

What is a fencing token?
a number that increases every time a lock is granted (e.g. incremented by the lock service). Fencing tokens can detect and block a node that is inadvertently acting in error (e.g.,
because it hasn’t yet found out that its lease has expired).

Byzantine fault
When we assume that nodes in a distributed system are telling the truth to the best of their ability but then a node lies by saying for example it received a message when it did not.

Byzantine Generals Problem
In the Byzantine version of the problem, there are n generals who need to agree, and their endeavor is hampered by the fact that there are some traitors in their midst. Most of the generals are loyal, and thus send truthful messages, but the traitors may try to deceive and confuse the others by sending fake or untrue messages (while trying to remain undiscovered). It is not known in advance who the traitors are

What is Byzantine fault-tolerant?
A system is Byzantine fault-tolerant if it continues to operate correctly even if some
of the nodes are malfunctioning and not obeying the protocol, or if malicious attackers
are interfering with the network.
