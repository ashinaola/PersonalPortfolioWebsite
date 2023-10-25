---
layout: post
title: seeing the pros and cons of two approaches - recursion and iteration
categories: [data structures and algorithms]
---
The first time i compared two different approaches in problem solving within the domain of computer science, it was looking at the fibonacci sequence and making a program which would generate a sequence of numbers that fulfill a set of conditions.  Here are the conditions:

```
1. The first number is 1
2. The current number is the sum of the previous two numbers
3. All numbers are integers
```

The idea behind the exercise was to demonstrate the differences in performance between different approaches to solving a particular problem.  For the Fibonacci sequence, it turns out that iteration was able to return sequences far beyond the limit of the program which used recursion.  However, I want to explore the different trade-offs between recursion and iteration.  With recursion, it is usually assumed to be a more elegant approach to problem solving compared to iteration.  When maintaining one's own stack, readability becomes key in the long term.  However, there are downsides to using recursion such as a larger amount of memory possibly being used or a less intuitive approach to solving the problem.  At the foundation of this is the difference between a top-down and bottom-up approach in designing algorithms.

### fibonacci sequence


### coin change problem


### merge sort implementation


### walking/traversing trees