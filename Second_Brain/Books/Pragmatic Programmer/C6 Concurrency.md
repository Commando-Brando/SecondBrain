## Activity Diagram
I like the idea of approaching a problem by breaking the problem down into steps and then thinking what parts can be concurrent/parallel and what parts are serial. In addition to this, I think we can combine this approach with the approach of breaking a problem into data transformations. Combining these 2 approaches may allow you to have a good perspective on approaching the problem.

**1. What is concurrency?** Concurrency occurs when the execution of two or more pieces of code acts as if they run simultaneously. This is achieved in an environment capable of switching execution between different parts of the code during its runtime, often implemented using fibers, threads, and processes.

**2. What is parallelism?** Parallelism is when multiple pieces of code actually run at the same time, requiring hardware that can perform multiple operations simultaneously. This could involve multiple cores in a CPU, multiple CPUs in a computer, or multiple computers working together.

**3. What is temporal coupling?** Temporal coupling refers to a form of coupling where the code imposes a sequence on operations that is not necessary to solve the problem at hand. It involves code that depends on certain events happening in a specific order (like one "tick" before a "tock") which can reduce flexibility and performance in concurrent environments.

**4. What is the other least talked about type of coupling aside from code dependencies?** The other least talked about type of coupling, aside from code dependencies, is temporal coupling. This type of coupling concerns the unnecessary sequential execution of operations that could otherwise be executed out of order or in parallel.

### Flashcard 1: What are the 2 main time considerations for dealing with temporal coupling?

**Answer:** The two main time considerations for dealing with temporal coupling are concurrency (things happening at the same time) and ordering (the relative positions of things in time). Approaching a problem with these 2 things in mind can help us optimize and make more performant code.

### Flashcard 2: What is an activity diagram and how can it help with temporal coupling?

**Answer:** An activity diagram is a visual representation consisting of a set of actions (drawn as rounded boxes) connected by arrows that dictate the flow of processes. It helps with temporal coupling by breaking down a problem space into components and identifying where components could be performed in parallel, thereby maximizing parallelism and minimizing unnecessary sequential dependencies.

### Flashcard 3: What is a semaphore?

**Answer:** A semaphore is a synchronization tool used to control access to a common resource by multiple processes in a concurrent system. It is essentially a variable that allows N number of threads to enter a critical section. A semaphore manages simultaneous access by decrementing when a process enters the critical section and incrementing when a process leaves, blocking entry when the count reaches zero.

### Flashcard 4: What is the problem with managing shared state in a concurrent/parallel program?

**Answer:** The problem with managing shared state in concurrent/parallel programs is the risk of inconsistent or incorrect state due to simultaneous accesses and modifications by multiple threads. This leads to race conditions, where the outcome depends on the non-deterministic order of execution of threads, potentially causing bugs that are hard to predict and replicate.

### Flashcard 5: What are the common concurrency pitfalls and how to avoid them?

**Answer:** Common concurrency pitfalls include race conditions, deadlocks, and non-atomic operations. These can be avoided by using proper synchronization mechanisms like semaphores, mutexes, and transactional memory, designing systems with immutable objects, and structuring applications to minimize shared state and dependencies.

### Flashcard 6: What are multiple resource transactions and how should you handle them?

**Answer:** Multiple resource transactions involve managing access to more than one shared resource concurrently. Handling them properly requires coordinating the locking and releasing of resources to prevent deadlocks and ensure consistency. 

### Flashcard 6: What are multiple resource transactions and how should you handle them?

**Answer:** Multiple resource transactions involve managing access to more than one shared resource concurrently. Handling them properly requires coordinating the locking and releasing of resources to prevent deadlocks and ensure consistency. Techniques such as ensuring atomicity of operations, using nested transactions, or implementing compensating operations (like rollback mechanisms) are effective strategies. 

Example: Imagine a diner, if a customer orders apple pie à la mode, the waiter must check both the pie and ice cream availability simultaneously. To handle this, if the waiter secures a slice of pie but finds no ice cream available, they must return the pie slice to avoid holding a resource that cannot be used as intended, thus coordinating access to both resources effectively.

### Actors

The actor code examples reminds me of a finite state machine or in this case each actor is a FSM that can receive external messages from other FSMs in the system

### What is the actor model?

The actor model is a conceptual framework that views each component as an "actor," an independent virtual processor with its own local and private state, capable of processing messages asynchronously. Each actor has a mailbox and processes messages sequentially. They interact by sending messages to each other's mailboxes, can create new actors, and modify their own state in response to messages, without sharing state directly with other actors. Good concurrent solution that evades shared state issues

### How is the actor model a good solution for concurrent code?

It allows multiple actors to operate concurrently without the need for shared memory or direct communication, thus reducing the complexity of synchronization and avoiding common concurrency issues like deadlocks. Since each actor processes messages asynchronously and independently, the system can efficiently handle high levels of concurrency, making it highly scalable and reliable for distributed systems.

## Blackboard Notes

I believe here the author describes highly concurrent distributed systems where using messaging systems lots of independent actors can contribute to a higher goal like multiple detectives adding things to a blackboard to solve a crime. These actors may not be fully aware of each others existence and yet have a reasonable way to concurrently make progress on a task together.