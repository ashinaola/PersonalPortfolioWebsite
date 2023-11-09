---
layout: post
title: building then using a singly-linked list
categories: [data structures and algorithms]
---
One of the first problems that I encountered in my introduction to computer programming class was trying to add another element to an array which was already full.  This caused the compiler to print an error message.  At the time, I worked around the issue by replacing the full array with an array which was double the size and move all the elements over from the smaller, old array to the larger array.  However, my professor mentioned that after a while, the array will become too large and copying the elements would be much slower than adding the elements to something that wasn't fixed in size.  This is when they introduced the data structure, the singly-linked list.  So today, I was thinking of building a singly-linked list and using the list to build travel iterneraries.  Hopefully, by the end of this, singly-linked lists will be a lot more easier to navigate.

### singly-linked list background
Unlike the first data structure that most programmers get introduced to, linked lists consists of two components.  A node and a pointer which allows for the next element to be accessed from the current one.  These pointers allow for iteration through the list and also allows for the list to grow or extend in length.  Arrays are introduced as data structures with a fixed or 'static' length.  The linked list, with the pointer, is of 'dynamic' length.  This means that linked lists can grow in length after the list is initialized.

In order to build the linked list, the first element of the linked list to inspect is the node.  This is the element which will hold the data, along with the pointer which makes the appending and iteration possible.  So to have a better image of what a node is structurally, I provided a little snippet to help with building the singly-list list.
```
listElement node:
    data        // the data which the list element will hold
    next node   // the pointer to the next node
node head       // the head of the node
```
To complete the singly linked list, we also have to understand what operations are going to be performed by the data structure.  A basic singly linked list has at least four different operations (add, remove, peek, display).

#### operation: add()
The add operation is supposed to take a user's input and then append the data to the list.  One of the most important things to consider is exactly what the pointer is referring to.  Under the hood, the linked list is linked through a series of pointers which link the different memory adresses together.  This is exactly why the linked list is able to continue appending and growing, unlike the array which is a series of memory addresses that are located next to each other.

In order for the add operation to work, the first step of the function is to check the list's head for any elements.  If the head is empty, then the head is assigned the user's input.  Otherwise, the user's input is set to a temporary node which iterates down the list until the next pointer is empty.  The next node is then set to the temporary node and the temporary node becomes the new last node on the list.  Here is a rough draft to show the steps:
```
function add(user input):
    node temp.data = head                   // start the temporary node at the list head
    start loop until temp.next is empty:
        temp = temp.next                    // iterate down the list
    temp.next = new node(user input)        // set the new last node on the list
```
This would allow for the list to be able to expand by taking advantage of the pointers which are a part of each node.

#### operation: remove()
The remove operation is suppose to undo the effect of the add operation of the linked list.  There are a couple ways to implement the operation, whether it is by allowing the user to give the function the node to delete or by simply deleting the head node and setting the new head to the next node.  In this post, a basic remove() operation will be performed without any user input.  Instead of prompting the user for input, the remove() operation will remove the head and declare the following node as the new list head.  This will ease the basic operation for demonstration but adding the search and remove functionality will not be a hard addition.  This will most likely be a necessary addition when the singly linked list is being used to build something that could be used in everyday life.  The additional step would be checking the next node's data to compare with the user's input.  If it matches, the next steps would be to set the pointer's reference to the node after the next.  And then, it would be safe to delete the next node.

To remove a node on the singly linked list, it is as simple as deferencing the previous node from it and pointing it over to its next node.  To give a more accurate image:
```
Before:
    A -> B -> C -> D ->

After remove(B):
    A -> C -> D
         B (removed)
```
The idea is to "skip" the node that you would like to delete from the list.  This way, the pointers will refer to the correct memory addresses as another temporary node traverses down the list.

This would be the steps for the removal of the head's list:
```
function removeHead(node):
    check head (return blank if empty)
    set the temporary node
    set new head to next node
    remove temporary
``` 
To compare, the rough steps for the removal of a wanted node on the list would look like:
```
function searchAndRemove(user input):
    set an iterator node to the head
    start a loop:
        check if the next node matches data
        if yes:
            set the iterators pointer to the node after the next
            delete the next node
        if no:
            continue
```
This will come in handy when we build the travel itinerary by allowing users to be able to delete cities that were unintentionally added.

#### operation: peek()
The next operation that is frequently used is the peek() operation.  The runtime of the operation would be constant.  peek() will return the head of the linked list.  This would be very easy to implement, as one would only have to check the head of the list, if the head is empty then the function should return an error code whereas if not, the head's data would be returned.

#### operation: display()
display()'s runtime is linear.  The purpose of display is to show the linked list's contents.  This would be a necessary operation since user interaction would be virtually impossible without any possible way to see the node's data.  The steps would be first, initialize a iterator and then allow the iterator to go through the list and print the node's data to the console.  The rough steps of the display() operation looks like this:
```
function display():
    new node iterator = head
    start loop:
        print(iterator.data)
```

### plan of execution: travel itinerary
