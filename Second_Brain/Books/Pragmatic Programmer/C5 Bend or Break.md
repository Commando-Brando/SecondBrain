TARGET DECK: Pragmatic Programmer::C5 Bend or Break

What is the law of Demeter (LoD)?
A set of guidelines written in the late 80s by Ian Holland. He created them to help developers on the Demeter Project keep their functions cleaner and decoupled.
The LoD says that a method defined in a class C should only call:
• Other instance methods in C
• Its parameters
• Methods in objects that it creates, both on the stack and in the heap 
• Global variables (not recommended)

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
![[FSM.png]]
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








START
Basic
What is the observer pattern?
Back: 
-  Design pattern where an object (observable) maintains a list of its dependents (observers) which get notified by the observable of any state changes or events occurring
- Often observers can pass a callback function to the observable
- Establishes a one to many relationship between observable and observers

[Design Pattern Gurus Observer Reference](https://refactoring.guru/design-patterns/observer)
Pragmatic Programmer Page142
<!--ID: 1719679102611-->
END


START
Basic
What is the publisher/subscriber pattern?
Back: 
-  Often used synonymously with the observer pattern but for the Pragmatic Programmer it is the observer pattern where the communication of the observers and observable are abstracted away via a channel which is usually provided by a service or programming language library

[Design Pattern Gurus Observer Reference](https://refactoring.guru/design-patterns/observer)
Pragmatic Programmer Page143
<!--ID: 1719679102613-->
END


START
Basic
What is the publisher/subscriber pattern?
Back: 
-  Often used synonymously with the observer pattern but for the Pragmatic Programmer it is the observer pattern where the communication of the observers and observable are abstracted away via a channel which is usually provided by a service or programming language library

[Design Pattern Gurus Observer Reference](https://refactoring.guru/design-patterns/observer)
Pragmatic Programmer Page143
END


START
Basic
What is an example of event stream processing with the publish/subscribe pattern in JavaScript?
Back: In front-end Javascript web components often will listen (subscribe) to a certain types of events such as a button being clicked (observable) that the browser stream in asynchronously

[Javascript Events MDN Reference](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#its_not_just_web_pages)
[Design Pattern Gurus Observer Reference](https://refactoring.guru/design-patterns/observer)
Pragmatic Programmer Page 144 Reference 
<!--ID: 1719679102614-->
END

#### My thoughts on data transformation pipelines:
I really like the idea of approaching your code from the POV of data transformations. I used to code more so like that working at UTSA doing a lot of data work but now at Microsoft working in C# everything is a lot more OOP oriented which I am still getting comfortable with


START
Basic
How is approaching a software solution from its required data transformations helpful?
Back: Generally most programming problems can be boiled down to accepting some input, transforming the data one or more times, and then outputting the data in some desired form

- Example of breaking a problem down into data transformation steps for figuring out anagrams
  
  ![[Pasted image 20240615214237.png]]
Pragmatic Programmer Page 149 Reference 
<!--ID: 1719679102615-->
END


#### Returning and passing around success/error with functions Page 155
I found his elixir example of passing around a tuple whose first value is either `ok` or `error` to be intriguing. I think GO does something like this or at least returns from functions like that. It forces you to think about error handling at each function call which may be good or bad depending on how easy it is to maintain but I would be willing to experiment and try this kind of style.


#### Thoughts on mixins
In C# these are called extensions, I am actually building an extensions for an enum in c# as part of my main task right now at work. I am not sure how my coworkers view extensions because I have not heard anyone talk about them and I do not think I have noticed them in the codebase. We will see on the PR comments but researching it myself the internet seemed to agree as far as C# goes that extensions are a fair approach

What is a mixin?
A class that provides methods to other classes without being a parent class, allowing code reuse and the combination of behaviors in multiple classes.

Good solution for giving classes shared functionality without the coupling of inheritance.

![[mixin.png]]



#### Configuration

I agree put things in configuration files if it data that changes 
I like his idea of a dynamic config via api call it makes sense to me especially as it makes making an env var GUI manager easy



