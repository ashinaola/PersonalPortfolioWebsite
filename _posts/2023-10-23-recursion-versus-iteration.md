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
As with the case with the fibonacci numbers, the first step in solving the problem recursively is to establish both a base case and a recurrence relation.  Once both are established, the implementation would be straightforward and can be accomplished with an if-else conditional block.  The base case would be when the so-called price that is being 'plugged-in' to the function is 0.  The recurrence relation allows for the price to be decreased by multiples of the denomination.  Here is the pseudocode:
```
recursive coin change <- (price, denominations, total):
case 1: target
```

#### code: recursion
Given the pseudocode, this is a function using recursion in Python:
```
def recursive_coin_change(coins, target, sum):
    if sum < 0:
        return 0
    
    elif sum == 0:
        return 1
    
    elif target <= 0:
        return 0
    
    else:
        return min(recursive_coin_change(coins, target-1, sum) + 
        recursive_coin_change(coins, target, sum-coins[target-1]))

```

#### pseudocode: iteration
In the iterative approach, the plan is to start from the largest denomination and then work back by subtracting the amount from the integer that was given to the function.  A counter should be assigned in order to track how many coins are being given as the amount decreases.  After each step, the leftover amount is checked to be sure that the amount that is being checked is still more than the current denomination.  It is when the leftover amount is less, we keep comparing denominations until and subtract until the leftover is less than the denomination in the first index.  Here is an idea of the steps that the function will take:
```
function -> (price: 125, coins: [1,5,10,25])

change = []
index = n - 1, where n is the number of coins in the denomination

start index @ coins[n-1] (25), start count @ 0
    125 - 25  = 100 (105 > 25), count + 1 = 1
    100 - 25 = 75 (75 > 25), count + 1 = 2
    75 - 25 = 50 (50 > 25), count + 1 = 3
    50 - 25 = 25 (25 == 25), count + 1 = 4
    25 - 25 = 0 (0 < 25), count + 1 = 5
    add 5 to change
check if 0 < 10 -> yes
check if 0 < 5 -> yes
check if 0 < 1 -> yes

Output: [0,0,0,5]
```
While this displays the idea behind the algorithm, there is still a problem where the idea is still not near to what is necessary to brush out code.  While it is useful to visualize the algorithm using this method, it is still better to draw out a general schematic using pseudocode in order to get a better vision of the necessary steps.
```
pseudocode(coins[], price):
    change = [length(coins)-1 indexes]
    index = length(coins) - 1
    
    for(index -> 0) over coins:
        count = 0
        while(condition: price >= coins[index]):
            price = price - coins[index]
            count = count + 1
        change[index] = count
    
    return change
```

#### code: iteration
Given the pseudocode, it is very easy to express this with Python as we can see here:
```
def iterative_coin_change(coins, target):
    total = 0
    change = []
    
    for i in coins:
        coin_count = 0

        while total < target:
            total += i
            coin_count += 1
            if total >= target:
                coin_count -= 1
                break
            
        change.append(coin_count)
    
    return change
```

### merge sort implementation
In algorithms, sorting is possibly one of the most important problems that one would encounter.  The idea is to take a list of unsorted elements and sort them in ascending or descending order.  There are many different sorting algorithms such as insertion sort, bubble sort, quicksort, etc. but the focus is going to be on merge sort.  The idea of merge sort is to utilize recursion or iteration to break down the unsorted array into simpler bits of the input, and then merge the sorted bits together to create the sorted list.

#### pseudocode: recursion
When building the pseudocode, just like in the other cases it is helpful to first determine the base case and the recurrence relation before planning out the pseudocode.  The first important element is understanding the base case, which in this case would be having an array with a single element.  The other important element to building this recursive approach is to determine the recurrence relation, which is:
```
T(n) = 2T(n/2) + O(n)
```
When looking at the variables, T represents the time complexity of the sort and n would represent an array which the algorithm is to sort.  This approach would result in a run time of O(n log(n)) which would be faster than the runtime of the previously mentioned insertion sort, which usually utilizes a nested loop resulting in a runtime of O(n<sup>2</sup>).

The pseudocode and approach would be better organized if the recursive sort is a seperate function (or action) and the merge is done afterwards, this is the pseudocode of the approach:
```
function mergeSort(arr, start, end)
    if (end - start) <= 1
        return
    mid = (end - start) / 2 + start
    mergeSort(arr, start, mid)
    mergeSort(arr, mid, end)
    merge(arr, start, mid, end)

function merge(arr, start, mid, end)
    left = arr[start:mid]
    right = arr[mid:end]
    i = j = 0
    for k in range(start, end):
        if j >= len(right) or (i < len(left) and left[i] < right[j]):
            arr[k] = left[i]
            i += 1
        else:
            arr[k] = right[j]
            j += 1
```

#### code: recursion
Given the pseudocode, the approach to expressing the code in Python would be almost near direct just like in the previous instances.  Here is the code to the recursive approach to merge sort:
```
def merge_sort_recursive(arr):
    if len(arr) > 1:
        mid = len(arr) // 2
        left_half = arr[:mid]
        right_half = arr[mid:]

        merge_sort_recursive(left_half)
        merge_sort_recursive(right_half)

        i = j = k = 0

        while i < len(left_half) and j < len(right_half):
            if left_half[i] < right_half[j]:
                arr[k] = left_half[i]
                i += 1
            else:
                arr[k] = right_half[j]
                j += 1
            k += 1

        while i < len(left_half):
            arr[k] = left_half[i]
            i += 1
            k += 1

        while j < len(right_half):
            arr[k] = right_half[j]
            j += 1
            k += 1
```

#### pseudocode: iteration
The difference between the recursive and iterative approaches here is the sort, itself, carrying out the sort using a loop directly on the array instead of changing the indexes of the sort function itself: 
```
function mergeSort(arr)
    n = len(arr)
    size = 1
    while size < n:
        left = 0
        while left < n:
            mid = min(left + size, n)
            right = min(left + 2 * size, n)
            merge(arr, left, mid, right)
            left += 2 * size
        size *= 2

function merge(arr, start, mid, end)
    left = arr[start:mid]
    right = arr[mid:end]
    i = j = 0
    for k in range(start, end):
        if j >= len(right) or (i < len(left) and left[i] < right[j]):
            arr[k] = left[i]
            i += 1
        else:
            arr[k] = right[j]
            j += 1
```

#### code: iteration
The code for iteration using Python:
```
def merge_sort_iterative(arr):
    n = len(arr)
    curr_size = 1

    while curr_size < n:
        left = 0

        while left < n - 1:
            mid = min(left + curr_size - 1, n - 1)
            right = min(left + 2 * curr_size - 1, n - 1)

            merge(arr, left, mid, right)

            left = left + 2 * curr_size

        curr_size = 2 * curr_size

def merge(arr, left, mid, right):
    n1 = mid - left + 1
    n2 = right - mid

    left_arr = arr[left:left + n1]
    right_arr = arr[mid + 1:mid + 1 + n2]

    i = j = 0
    k = left

    while i < n1 and j < n2:
        if left_arr[i] <= right_arr[j]:
            arr[k] = left_arr[i]
            i += 1
        else:
            arr[k] = right_arr[j]
            j += 1
        k += 1

    while i < n1:
        arr[k] = left_arr[i]
        i += 1
        k += 1

    while j < n2:
        arr[k] = right_arr[j]
        j += 1
        k += 1
```

### in-order traversal of binary trees
Data structures introduces different storage mechanisms for data along with their operations.  Trees are possibly one of the more versatile data structures which have many uses in software engineering.  An example is using a binary search partition in a 3D video game rendering engine.  Another example of trees being used in real life is to implement a heap which is used in priority queues.  Priority queues play a major role in scheduling processes on the operating system of your computer.  As noted there are many practical uses for trees because their structure is intuitive and a subset of trees (binary trees) make searching incredibly easy and fast.

One of the important operations of a tree is to traverse the tree.  However, there are three different ways to traverse a binary tree.  Here, the focus is going to be on implementing the recursive and iterative in-order traversal of a binary tree.  The other ways to traverse a binary tree is pre-order traversal and post-order traversal.

This is the steps to inorder traversal of binary trees:
```
1. Visit nodes to the left
2. Go to the root
3. Visit nodes to the right
```

#### pseudocode: recursion
By now, there is a clear pattern of how to implement the recursive approach.  The first part is understanding the base case and the other is understanding the recurrence relation.  When thinking about the base case, the absolute end of the traversal is when there are no more nodes to visit on the tree.  The recurrence relation of in-order traversal is as follows:
```
T(n) = 2T(n/2) + O(1)
```
Given both, the pseudocode is as follows:
```
function inorderTraversal(root)
    if root is None
        return
    inorderTraversal(root.left)
    print(root.value)
    inorderTraversal(root.right)
```

#### code: recursion
Given the pseudocode, this is the code in Python:
```
def recursive_coin_change(coins, target, sum):
    if sum < 0:
        return 0
    
    elif sum == 0:
        return 1
    
    elif target <= 0:
        return 0
    
    else:
        return min(recursive_coin_change(coins, target-1, sum) + 
        recursive_coin_change(coins, target, sum-coins[target-1]))
```

#### pseudocode: iteration
There is a difference between the recursive and iterative approach and the recursive approach does result in code that is slightly more intuitive and readable compared to the iterative approach.  This is mostly because the iterative approach utilizes a stack in order to recall previously visited nodes.  The reason why a stack is used is because of it's push() and pop() operations that introduces a capacity for recall:
```
function inorderTraversal(root)
    stack = []
    curr = root
    while curr is not None or len(stack) > 0:
        while curr is not None:
            stack.push(curr)
            curr = curr.left
        curr = stack.pop()
        print(curr.value)
        curr = curr.right
```

#### code: iteration
Given the pseudocode, this is the Python code for the approach:
```
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def iterative_inorder_traversal(root):
    stack = []
    result = []

    current = root

    while current or stack:
        while current:
            stack.append(current)
            current = current.left

        current = stack.pop()
        result.append(current.value)
        current = current.right

    return result
```