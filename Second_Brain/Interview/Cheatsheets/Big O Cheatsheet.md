[Original Page Link](https://guides.codepath.com/compsci/Big-O-Complexity-Analysis)

> "Algorithm Complexity: you need to know Big-O. It's a must. If you struggle with basic big-O complexity analysis, then you are almost guaranteed not to get hired." -- Steve Yegge, "[Get that job at Google]"

## **Introduction**

Big O notation is used to describe the complexity of an algorithm when measuring its _efficiency_, which in this case means _how well the algorithm scales with the size of the dataset_. (Broadly speaking, the process of measuring this type of efficiency is known as "Complexity Analysis," and "Big O" simply refers to the notational system we use to talk about it.)

Big O is represented with the following syntax: _O(n)_. The value we're concerned with is between the parentheses and will in most cases include the variable _n_, which denotes the size of the algorithm's input. In most simple scenarios (i.e., interview problems), the algorithm will be a simple function, and _n_ will typically refer to the size of a collection taken by the function as its input. The value between the parentheses expresses that function's complexity in terms of _n_.

Complexity is measured in two dimensions: _time_ (how long a function takes to complete), and _space_ (how much memory a function consumes while executing). So a simple way to think about a function's complexity is to consider _the number of things it does or creates_ (_x_) as multiplied by the size of the input (_n_). The trick is that the "number of things it does or creates" is represented in Big O notation not as variable such as _x_ but instead as a constant: 1. So instead of _O(x * n)_, the complexity would be expressed as _O(1 * n)_ or, simply, _O(n)_. Therefore a function with a time complexity of _O(n)_ performs a given number of steps multiplied by _n_.

## **Examples**

In all of the following examples, we'll consider a single function that takes an array of items as input and has no output: a method with the signature `void someFunction(int[] inputArray)`. So in all the following examples, _n_ will represent the length of `inputArray`, and we'll express the complexity the method's body using Big O in relation to _n_.

### **_O(1)_ - Constant Complexity**

Let's start with one of the simplest possible implementations of this method, one which does nothing but print the size of the input array:

```
publicvoidsomeFunction(int[] inputArray){System.out.println("n = "+ inputArray.length);}
```

This function runs in _O(1)_ time (or _constant time_). Because this method takes the same amount of time to complete irrespective of the input size, we ignore _n_ entirely when expressing the complexity. The input array could contain 1 item or 1,000 items, but this function would still just require one "step."

### **_O(n)_ - Linear Complexity**

A simple _O(n)_ example would perform the same set of actions for every item in the input array. In this case we're using a `for` loop, but the same complexity could be achieved via recursion or other means.

```
publicvoidsomeFunction(int[] inputArray){for(int item: inputArray){System.out.println(item);}}
```

This function runs in _O(n)_ time (or _linear time_), where _n_ is the number of items in the array. If the array has 10 items, the function calls `System.out.println` 10 times. If it has 1,000 items, it calls it 1,000 times.

### **_O(n2)_ - Quadratic Complexity**

```
publicvoidsomeFunction(int[] inputArray){for(int firstItem: inputArray){for(int secondItem: inputArray){int[] orderedPair=newint[]{firstItem, secondItem};System.out.println(Arrays.toString(orderedPair));}}}
```

Here we're nesting two loops. If our array has _n_ items, our outer loop runs _n_ times and our inner loop runs _n_ times _for each iteration of the outer loop_, giving us _n2_ total calls to `System.out.println`. Thus this function runs in _O(n2)_ time (or _quadratic time_). If the array has 10 items, we have to print 100 times. If it has 1,000 items, we have to print 1,000,000 times.

> Classic example: Bubble sort

### **_O(log n)_ - Logarithmic Complexity**

```
publicvoidsomeFunction(int[] inputArray){for(int i= 1; i<= inputArray.length; i= i* 2){System.out.println(item[i]);}}
```

Here we have simple loop in which the post operation of the `for` statement multiples the current value of `i` by 2, so `i` goes from 1 to 2 to 4 to 8 to 16 to 32 and so on.

_O(log n)_ is considered to be fairly efficient. The time taken increases with the size of the data set, but not proportionately so. This means the algorithm takes longer per item on smaller datasets relative to larger ones. 1 item takes 1 second, 10 items takes 2 seconds, 100 items takes 3 seconds. If your dataset has 10 items, each item causes 0.2 seconds latency. If your dataset has 100, it only takes 0.03 seconds extra per item. This makes _O(log n)_ algorithms very scalable.

> Classic example: Binary search

### **Other Examples**

While the above are the most common, there are [many other well known examples](https://en.wikipedia.org/wiki/Time_complexity#Table_of_common_time_complexities) of Big O complexities. A few additional ones you may encounter:

- **_O(n3)_ - Cubic Complexity:** Similar to _O(n2)_, but consider that example with an added nested loop.
- **_O(n log n)_ - Linearithmic Complexity:** The [Merge sort](https://en.wikipedia.org/wiki/Merge_sort) worst case complexity is _O(n log n)_.
- **_O(2n)_ - Exponential Complexity:** The algorithm takes twice as long for every new element added, so even small increases in _n_ dramatically increase the running time.

### **Additional Resources**

- [HackerRank intro to Big-O video](https://www.youtube.com/watch?v=v4cd1O4zkGw)
- [CS Dojo Time complexity video](https://www.youtube.com/watch?v=D6xkbGLQesk)
- [InterviewCake big-O guide on time and space complexity](https://www.interviewcake.com/article/java/big-o-notation-time-and-space-complexity)
- [InterviewCake logarithms guide](https://www.interviewcake.com/article/java/logarithms)