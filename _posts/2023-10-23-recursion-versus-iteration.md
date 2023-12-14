---
layout: post
type: posts
title: seeing the pros and cons of two approaches - recursion and iteration
date: 2023-10-23
categories: [Data structures and Algorithms]
---
The first time i compared two different approaches in problem solving within the domain of computer science, it was looking at the fibonacci sequence and making a program which would generate a sequence of numbers that fulfill a set of conditions.  Here are the conditions:

```
1. The first number is 1
2. The current number is the sum of the previous two numbers
3. All numbers are integers
```

The idea behind the exercise was to demonstrate the differences in performance between different approaches to solving a particular problem.  For the Fibonacci sequence, it turns out that iteration was able to return sequences far beyond the limit of the program which used recursion.  However, I want to explore the different trade-offs between recursion and iteration.  With recursion, it is usually assumed to be a more elegant approach to problem solving compared to iteration.  When maintaining one's own stack, readability becomes key in the long term.  However, there are downsides to using recursion such as a larger amount of memory possibly being used or a less intuitive approach to solving the problem.  At the foundation of this is the difference between a top-down and bottom-up approach in designing algorithms.
In order to make this comparison, I will use Python to set up and compare the different approaches.  There will not be any differences as far as environment goes, they will be compiled in the same environment.  All things constant, the hope is to see obvious differences between iteration and recursion and have a better understanding of when to take whichever approach.

### fibonacci number
The first problem to present an opportunity to compare the two approaches is the Fibonacci number.  It is a simple problem where you are to build a list of numbers where current element's value is the sum of the previous two elements in the list.  An example of a fibonacci number is:
```
1, 1, 2, 3, 5, 8, 13, ...
```
and the fibonacci number is the sum of all the elements in the list.  The problem could be approached by building the list top down through recursion or bottom up through iteration.  First, in order to have a better understanding of how each of these programs are going to function, it would be better to have pseudocode so that less energy is spent on carving the logic of the program out and more is spent on simply expressing the idea.

#### pseudocode: recursion
The first task in setting up a recursive solution for printing out a list of fibonacci numbers is finding the base case.  In the case of the fibonacci number, the base case would be when the parameter is either 0 or 1.  This is because if we are to print n-amount of numbers, if n = 0 or if n = 1, then the number would just be the number.  So for starting out, we have a base case where:
```
f(0) = 0
f(1) = 1
```
The next step would be to establish some kind of relationship between the function and the parameter.  This very crucial step in being able to derive the recurrence relation, which is what you're pseudocode is going to be based off of.  The recurrence relation for the fibonacci number is:
```
F(n) = F(n-1) + F(n-2)
```
Once you have the recurrence relation, you can then be able to write out some pseudocode to make the process of typing out your code a lot simpler:
```
function(integer n):
    return n if n = 0 or n = 1
    return f(n-1) + f(n-2)
```

#### code: recursion
After you have the pseudocode, typing the actual code wouldn't be too hard. Translation when it comes to the recursion pseudocode is very straightforward:

```
def recursive_fibonacci(n):
    if n < 2:
        return n
    else:
        return recursive_fibonacci(n-1) + recursive_fibonacci(n-2)
```
As you can see, taking pseudocode and turning it into real code is fairly straightforward when it comes to recursion.

#### pseudocode: iteration
As you saw, recursion has a more familiar feel to how we would approach a problem such as fibonacci.  My data structures professor described recursion as a fairly intuitive approach to designing various algorithms to solve complex problems.  However, as intuitive as recursion is, there are other ways to get n amount of fibonacci numbers.  Another alternative to recursion is iteration, which if you are familiar with programming concepts, can be expressed in the form of a for or while loop.

As previously mentioned, the pseudocode for the iterative solution to fibonacci numbers is not as straightforward as the two step process to build the recursive solution.  While the recursive solution starts from the top (n) and works down to f(0), iteration works in a different way where one starts from 1 and works up to n.  As such, the most appropriate way to start would be to initiate a variable which will store the sum.  After the variable is started at 1, a loop should be initialized and the loop should go n-1 iterations.  On each iteration, we will add the value from the previous iteration and the one prior to the running sum.  This is what the pseudocode would look like:
```
function(integer n):
    before variable = 1     // represents f(n-1)
    previous variable = 0   // represents f(n-2)
    current variable = 1    // represents running sum
    start loop @ 1 -> n:
        previous variable = before variable
        before variable = previous variable
        current variable = previous variable + before variable
    return current variable
```

#### code: iteration
As far as building a function in Python, the translation is not as straightforward as recursion but it does preserve most of its main structure.  The code is similar and is probably a little more condensed than the pseudocode because of the features that Python has to offer as an interpreted language.  The iterative function looks as follows:
```
def iter_funct(n):
    prev, curr = 0, 1
    for i in range(n):
        prev, curr = curr, prev + curr
    return prev
```
Like the pseudocode, the function uses the running sum to track the fibonacci sequence as the loop is executing.  The three steps shown are condensed into one single line within the loop.  Python is quite well known for allowing programmers to produce code that is condensed, yet readable to the human.  

### coin change problem
The coin change problem is a classical algorithmic problem where one is given a list of values that represent the denominations of the currency.  The main goal of the coin change problem is to give the exact amount of change, using the least amount of coins.  As before with the fibonacci sequence, both the iterative and recursive approaches are going to be compared in terms of intuition and ease of solution.

#### pseudocode: recursion


#### code: recursion

#### pseudocode: iteration

#### code: iteration

### merge sort implementation
In algorithms, sorting is possibly one of the most important problems that one would encounter.  The idea is to take a list of unsorted elements and sort them in ascending or descending order.  There are many different sorting algorithms such as insertion sort, bubble sort, quicksort, etc. but the focus is going to be on merge sort.  The idea of merge sort is to utilize recursion or iteration to break down the unsorted array into simpler bits of the input, and then merge the sorted bits together to create the sorted list.

#### pseudocode: recursion

#### code: recursion

#### pseudocode: iteration

#### code: iteration

### in-order traversal of trees
Data structures introduces different storage mechanisms for data along with their operations.  Trees are possibly one of the more versatile data structures which have many uses in software engineering.  An example is using a binary search partition in a 3D video game rendering engine.  Another example of trees being used in real life is to implement a heap which is used in priority queues.  Priority queues play a major role in scheduling processes on the operating system of your computer.  As noted there are many practical uses for trees because their structure is intuitive and a subset of trees (binary trees) make searching incredibly easy and fast.

One of the important operations of a tree is to traverse the tree.  However, there are three different ways to traverse a tree.  Here, the focus is going to be on implementing the recursive and iterative in-order traversal of a tree.  The other ways to traverse a tree is pre-order traversal and post-order traversal.

#### pseudocode: recursion

#### code: recursion

#### pseudocode: iteration

#### code: iteration