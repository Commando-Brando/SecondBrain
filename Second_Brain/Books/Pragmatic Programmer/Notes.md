
- 5 Whys, keep asking why 5 times until you know something for sure


# Chapter 2
- Code represents knowledge and logic
- Just because two functions are exactly the same does not mean they violate dry since they represent different knowledge p35
- Orthognality 
# Chapter 3
- **Shell** Need to get better with shells, I think exploring PowerShell for me and improve one of the TDS scripts
- **Power Editing** Learn more about Visual Studio become fluent with my editor/IDE pg81
- **Version Control** learn more about azure devops and its settings/emails
- **Debugging** 
	- If you find a bug think about how it could have been prevented and maybe update a unit test to do so
	- If you find a bug is it a symptom or the root cause? Do not fix symptoms fix the route cause
	- Assume the bug is caused by your code and not a libraries because probability states it is
	- • Do the conditions that caused this bug exist anywhere else in the system? Are there other bugs still in the larval stage, just waiting to hatch?

# Chapter 4
**Design by contract (DBC)**
- Design by contract (DBC) is a design technique emphasizing a contract for what say a function or component will do give data in a specific way. For example, your rest endpoint may require data in a very specific format. Given the correct format your endpoint can guarantee a "contract" on what will have. This reminds me of at Microsoft how I recently worked on a project where another team had to stand up an endpoint for us and we had to in some way negotiate a contact for what we pass and what we expect.
- DBC crashing early. The idea of asserting things early in business logic so your stack trace and things are closer to where the bug occurred. I agree with this practice although you may not want the program to crash, but in imperative languages using validation as DBC suggests could achieve the same effect.
- In general validating data to be passed to a class/function is the responsibility of the caller. Although I think that the functions being called should have guard rails on if it is widely shared and should handle errors gracefully. Where is the border line of this? Should every function in a class do data input validation? That would lead to possibly a lot of duplicated code as the same inputs are passed around. I think the line should be drawn at the class level since it is generally the smallest cohesive component in a system. I think if a class calls something outside of its class then that thing should have guard rails. Or any publicly exposed function should have the guard rails, this makes the most sense to me
**Dead Programs Tell No Lies**
- Essentially simply your error handling and do not handle every case necessarily which is interesting because across the board I have heard people recommend always be specific with types of exception when handling but that may just be counter productive and you cannot possibly predict every situation or later on more exception types could be introduced so definitely capture Exceptions but also specific ones when specific handling is necessary.
**Assertive programming**
- Aka using assert statements in actual code, not just in tests
- I have never seen this at Microsoft so curious where it is being used there if at all but I think we basically accomplish the same thing but doing validation and then throwing errors 
**How to Balance Resources**
- Finish what you start section shows how to nicely refactor multiple functions that operate on the same file. It shows a nice solution which provides leans towards having one function call multiple functions and passing the object to those functions, kind of how I wanted to refactor the apply access plugin
- Balancing exceptions section is nice, I like how he talks about how they point out that when using finally to deallocate a resource ensure the allocation is not in the try part otherwise you may attempt deallocating something that was never allocated
- _Exercise 18 (__possible answer on page 299__)_
	- Some Java developers make a point of setting an object variable to_ _NULL_ _after they have finished using the object. Why is this a good idea?

**Don't Outrun Your Headlights**
- Take small steps always falls into the don't outrun your headlights saying, you can only see so far ahead of your software's life and cannot predict what will come soon so take small steps

# Chapter 5

What is the law of Demeter (LoD)?
A set of guidelines written in the late 80s by Ian Holland. He created them to help developers on the Demeter Project keep their functions cleaner and decoupled.
The LoD says that a method defined in a class C should only call:
• Other instance methods in C
• Its parameters
• Methods in objects that it creates, both on the stack and in the heap 
• Global variables (not reccomended)

I think it should be noted to avoid having the class create objects and instead use dependency injection

  

What does it mean to avoid chain method calls?
Try not to have more than one “.” when you access something.
```cs
// This is pretty poor style
amount = customer.orders.last().totals().amount;

// and the opposite is as well like:
orders = customer.orders;
last = orders.last();
totals = last.totals();
amount = totals.amount;
```
  A pragmatic approach would be to add method(s) to the customer class that wraps some of those additional calls like:
```cs
amount = customer.getLastTotal();
```
There is a big exception to this for functional pipelines where the things you are chaining are not likely to ever change, for example the LINQ library in C#. More on [functional programming pipelines](https://www.youtube.com/watch?v=nuML9SmdbJ4)

**What is the impact of using global data on the coupling of application components?**
Global data increases coupling as every method in an application can access it, essentially acting like an added parameter. This makes it difficult to modify one part without potentially impacting the entire system.

**How does global data affect code reuse and unit testing?**
Global data complicates code reuse by making it hard to extract and isolate code without pulling in dependencies. For unit testing, it requires extensive setup to create a global environment, which complicates test configurations and execution.

**What is the issue with disguising global variables as singletons or global modules, and how can this be improved?**
Even when global variables are wrapped in singletons or global modules, they remain global data but with a more complex access method. Improvements include encapsulating the data behind methods that manage the data intelligently, such as through getter and setter methods, to maintain compatibility and control over data representation.

**Question:** Why are event-driven applications considered more interactive and efficient? **Answer:** Event-driven applications respond dynamically to events, making them more interactive for users. They also optimize resource use by reacting only when relevant data changes or events occur, rather than continuously polling for updates.

What are the four strategies to help design event driven applications?
1. Finite State Machines
2. The Observer Pattern
3. Publish/Subscribe
4. Reactive Programming and Streams

**Give an example of how a Finite State Machine can be implemented to parse messages.**
Consider a scenario where a system parses multipart messages from a websocket:

- **Initial State**: Waiting for any message.
- **Transitions**:
    - If a header message is received, transition to the "Reading message" state.
    - If a data message is received while in the "Reading message" state, stay in the same state.
    - If a trailer message is received while in the "Reading message" state, transition to the "Done" state.
    - Any other message in any state leads to the "Error" state. This FSM effectively handles the flow of different message types, ensuring that each is processed in the correct order and context.
![[Pasted image 20240613085406.png]]
Reference: Pragmatic Programmer Page 138

**What is a Finite State Machine (FSM) and what are its basic components?**
A Finite State Machine (FSM) is a model of computation consisting of a finite number of states. It transitions from one state to another in response to external inputs. Each state specifies certain actions to perform and the conditions for transitioning to other states. The basic components of an FSM include:

- **States**: Different conditions or situations in which the FSM can exist.
- **Events**: Inputs or occurrences that can trigger transitions between states.
- **Transitions**: The rules that define how to move from one state to another based on events.
- **Initial State**: The state in which the FSM begins operation.
[Youtube Reference](https://www.youtube.com/watch?v=4rNYAvsSkwk)
Pragmatic Programmer Page 138

**What are the advantages of using Finite State Machines in programming?** 
Finite State Machines offer several advantages in software development:

- **Clarity**: FSMs provide a clear and structured way to handle different scenarios, making the logic easy to understand and debug.
- **Manage Complexity**: They help manage complex conditions and state transitions in an organized manner.
- **Predictability**: FSMs operate predictably, as the outcomes and transitions are predefined based on the current state and incoming events.
- **Scalability**: Easy to modify and extend, FSMs can accommodate new states and transitions without significant restructuring.
Reference: Pragmatic Programmer Page 138


