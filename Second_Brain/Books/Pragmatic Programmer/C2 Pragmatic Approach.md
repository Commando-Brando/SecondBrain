
- Code represents knowledge and logic
- Just because two functions are exactly the same does not mean they violate dry since they represent different knowledge p35
- Orthogonality 

What is orthogonality?
Traditionally in geometry two lines are orthogonal if where they meet forms a right angle.
In computing, the term has come to signify a kind of independence or decoupling. Two or more things are orthogonal if changes in one do not affect any of the others. In a well-designed system, the database code will be orthogonal to the user interface: you can change the interface without affecting the database, and swap databases without changing the interface

What are the 2 main benefits to orthogonality in software?
- Gain in productivity, system components are easier to extend, modify, to build upon
- Reduce risk since less coupling less chance for things to break when modifying existing components

How does using globals in code reduce Orthogonality?
Every time your code references global data, it ties itself into the other components that share that data adding coupling. If another component changes the shared state that may cause a bug in another dependency.
