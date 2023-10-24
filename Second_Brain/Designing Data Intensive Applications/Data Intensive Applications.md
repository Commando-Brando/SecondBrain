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

Page 5 add diagram try to get a mermaid one from it

Faults - the things that can go wrong
Fault Tolerant - systems that can handle faults
Failure vs Fault - failure is when a system stops as a whole working but a fault is when a component of a system deviates from its spec