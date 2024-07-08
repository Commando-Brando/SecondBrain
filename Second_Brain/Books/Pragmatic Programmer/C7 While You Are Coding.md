TARGET DECK: Pragmatic Programmer::C7 While You are Coding

Page 191-242
## Lizard Brain
- I definitely get anxious sometimes around making a mistake
- Feeling stuck in the mud is not a good feeling 
- I definitely feel whenever I am ramping up on a new area of work and there is a lot to take in that sleeping on it usually helps my brain digest. 
- You have very limited brain power in a day at a certain point problem solving has very diminishing returns and you should just call it a day instead of working late, listen to your brain/body when it says it has had enough and needs to process the info

## Not just your code
Basically when reading someone else's code that codes different not worse/better but different try to understand the patterns they are applying and how they are thinking to get to this solution and it can help you understand other code better and potentially learn something new.

## Deliberate Programming
- Always be aware of what you are doing. Fred let things get slowly out of hand, until he ended up boiled, like the frog on page 8.
- Can you explain the code, in detail, to a more junior programmer? If not, perhaps you are relying on coincidences.
- Don’t code in the dark. Build an application you don’t fully grasp, or use a technology you don’t understand, and you’ll likely be bitten by coincidences. If you’re not sure why it works, you won’t know why it fails.
- Document your assumptions. Topic 23, Design by Contract, on page 104, can help clarify your assumptions in your own mind, as well as help communicate them to others.
- Don’t just test your code, but test your assumptions as well. Don’t guess; actually try it. Write an assertion to test your assumptions (see Topic 25, Assertive Programming, on page 115). If your assertion is right, you have improved the documentation in your code. If you discover your assumption is wrong, then count yourself lucky.
- Prioritize your effort. Spend time on the important aspects; more than likely, these are the hard parts. If you don’t have fundamentals or infrastructure correct, brilliant bells and whistles will be irrelevant.
- Don’t be a slave to history. Don’t let existing code dictate future code. All code can be replaced if it is no longer appropriate. Even within one program, don’t let what you’ve already done constrain what you do next—be ready to refactor (see Topic 40, Refactoring, on page 209). This decision may impact the project schedule. The assumption is that the impact will be less than the cost of not making the change

## O Notation

Always analyze the time/space complexity of each PR and try identify any bottlenecks that can be improved.
### Common Sense Estimates
**Simple loops**
If a simple loop runs from 1 to n, then the algorithm is likely to be
O (n)—time increases linearly with n. Examples include exhaustive
searches, finding the maximum value in an array, and generating checksums.

**Nested loops**
If you nest a loop inside another, then your algorithm becomes O (m × n),
where m and n are the two loops’ limits. This commonly occurs in simple
sorting algorithms, such as bubble sort, where the outer loop scans each
element in the array in turn, and the inner loop works out where to place
that element in the sorted result. Such sorting algorithms tend to be
O (n2).

**Binary chop**
If your algorithm halves the set of things it considers each time around
the loop, then it is likely to be logarithmic, O (lg n). A binary search of a
sorted list, traversing a binary tree, and finding the first set bit in a
machine word can all be O (lg n).

**Divide and conquer**
Algorithms that partition their input work on the two halves independently,
and then combine the result can be O (n lg n). The classic example is
quicksort, which works by partitioning the data into two halves and
recursively sorting each. Although technically O (n2), because its behavior
degrades when it is fed sorted input, the average runtime of quicksort is
O (n lg n).

**Combinatoric**
Whenever algorithms start looking at the permutations of things, their
running times may get out of hand. This is because permutations involve
factorials (there are 5 ! = 5 × 4 × 3 × 2 × 1 = 120 permutations of the digits
from 1 to 5). Time a combinatoric algorithm for five elements: it will take
six times longer to run it for six, and 42 times longer for seven. Examples
include algorithms for many of the acknowledged hard problems—the
traveling salesman problem, optimally packing things into a container
## Refactoring
Think of tech debt as a growth. It only requires a minor invasive procedure to remove now but later it will grow and spread which makes the procedure more invasive and dangerous. Wait too long and you might lose the patient entirely.

Martin Fowler offers the following simple tips on how to
refactor without doing more harm than good:7
1. Don’t try to refactor and add functionality at the same time.
2. Make sure you have good tests before you begin refactoring. Run the tests as often as possible. That way you will know quickly if your changes have broken anything.
3. Take short, deliberate steps: move a field from one class to another, split a method, rename a variable. Refactoring often involves making many localized changes that result in a larger-scale change. If you keep your steps small, and test after each step, you will avoid prolonged debugging.
## Test to Code
Thinking about how to test your code and sometimes clear ambiguity around the code you are planning to write. Think about test cases first and how the data output should look for you asserts!

Write test function definitions for the test cases before start coding 
## Property Based Testing
a type of software testing (usually unit-scoped) that allows developers to test software systems by defining properties (or invariants) that should hold true for a range of inputs.

## Stay Safe Out There

Really like the different cyber security points he mentions all good stuff page 232

## Naming
The example of name of colors colored differently is a brilliant way of illustrating how naming is important. I agree with him naming things can bring clarity which makes code more maintainable and devs more productive. Names should have meaning not just behavior descriptions 

I like his idea of honoring the local naming culture, follow the conventions of the technology and of your team/project.

## Flashcards
----------
START
Basic
When you brain is toast and you feel stuck on figuring something out what is the best way to making progress?
Back: Stop coding and take a walk, nap, sleep, just do something else and let your brain cook on the issue and digest the problem more
<!--ID: 1720132347397-->
END

----------

START
Basic
When reading someone else's code what is a good strategy to help you understand it?
Back: Figure out the patterns they use and how they came to the solution and this act of trying to think like them will help you understand the code more and possibly learn something new
<!--ID: 1720132347412-->
END

---------

START
Basic
What does it mean to deliberately program?
Back:
- Be able to explain the code, in detail, to a more junior programmer? If not, perhaps you are relying on coincidences.
- Don’t code in the dark. Build an application you don’t fully grasp, or use a technology you don’t understand, and you’ll likely be bitten by coincidences. If you’re not sure why it works, you won’t know why it fails
- Document and validate your assumptions.
- Don’t just test your code, but test your assumptions as well. Don’t guess; actually try it. Write an assertion to test your assumptions
<!--ID: 1720132347417-->
END

---------

START
Basic
When you brain is toast and you feel stuck on figuring something out what is the best way to making progress?
Back: Stop coding and take a walk, nap, sleep, just do something else and let your brain cook on the issue and digest the problem more
END

---------

START
Basic
How is tech debt like a growth disease?
Back: It only requires a minor invasive procedure to remove now but later it will grow and spread which makes the procedure more invasive and dangerous. Wait too long and you might lose the patient entirely.
<!--ID: 1720132347422-->
END

---------

START
Basic
What are the 3 rules for refactoring?
Back: 
1. Don’t try to refactor and add functionality at the same time.
2. Make sure you have good tests before you begin refactoring. Run the tests
as often as possible. That way you will know quickly if your changes have
broken anything.
3. Take short, deliberate steps: move a field from one class to another, split
a method, rename a variable. Refactoring often involves making many
localized changes that result in a larger-scale change.
<!--ID: 1720132347426-->
END

---------

START
Basic
How can TDD provide implementation clarity?
Back: Thinking about how to test your code and sometimes clear ambiguity around the code you are planning to write. Think about test cases first and how the data output should look for you asserts!
<!--ID: 1720132347430-->
END

---------

START
Basic
What is a property test?
Back: a type of software testing (usually unit-scoped) that allows developers to test software systems by defining properties (or invariants) that should hold true for a range of inputs.

Below we define our properties with the given function decorator and the test with run with different inputs within the given properties and their constraints.
![[propertyTesting.png]]
<!--ID: 1720132347434-->
END

---------

START
Basic
What is the recommended practice when you find a test case that fails during property testing?
Back: This may be an edge case so:
- create a unit test based on the failing test with the failing inputs are the test parameters
- Debug and fix the issue
- Keep the lone unit test as a regression test to prevent others from breaking it since there is not a guarantee the exact same test case will run again if the test cases were randomly generated
<!--ID: 1720132347437-->
END