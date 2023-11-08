---
layout: post
title: building then using a singly-linked list
categories: [data structures and algorithms]
---
One of the first problems that I encountered in my introduction to computer programming class was trying to add another element to an array which was already full.  This caused the compiler to print an error message.  At the time, I worked around the issue by replacing the full array with an array which was double the size and move all the elements over from the smaller, old array to the larger array.  However, my professor mentioned that after a while, the array will become too large and copying the elements would be much slower than adding the elements to something that wasn't fixed in size.  This is when they introduced the data structure, the singly-linked list.  So today, I was thinking of building a singly-linked list and using the list to build travel iterneraries.  Hopefully, by the end of this, singly-linked lists will be a lot more easier to navigate.

### singly-linked list background
Unlike the first data structure that most programmers get introduced to, linked lists consists of two components.  A node and a pointer which allows for the next element to be accessed from the current one.  These pointers allow for iteration through the list and also allows for the list to grow or extend in length.  Arrays are introduced as data structures with a fixed or 'static' length.  The linked list, with the pointer, is of 'dynamic' length.  This means that linked lists can grow in length after the list is initialized.

In order to build the linked list, the first element of the linked list to inspect is the node.  This is the element which will hold the data, along with the pointer which makes the appending and iteration possible.  So to have a better image of what a node is structurally, I provided a little pseudocode to help with building the singly-list list.
```
listElement node:
    data        // the data which the list element will hold
    next node   // the pointer to the next node
node head       // the head of the node
```
To complete the singly linked list, we also have to understand what operations are going to be performed by the data structure.  A basic singly linked list has at least four different operations (add, remove, peek, display).

#### operation: add()
The add operation is supposed to take a user's input and then append the data to the list.  One of the most important things to consider is exactly what the pointer is referring to.  Under the hood, the linked list is linked through a series of pointers which link the different memory adresses together.  This is exactly why the linked list is able to continue appending and growing, unlike the array which is a series of memory addresses that are located next to each other.

In order for the add operation to work, the first step of the function is to check the list's head for any elements.  If the head is empty, then the head is assigned the user's input.  Otherwise, the user's input is set to a temporary node which iterates down the list until the next pointer is empty.  The next node is then set to the temporary node and the temporary node becomes the new last node on the list.  Here is some pseudocode to show the steps:
```
function add(user input):
    node temp.data = head                   // start the temporary node at the list head
    start loop until temp.next is empty:
        temp = temp.next                    // iterate down the list
    temp.next = new node(user input)        // set the new last node on the list
```
This would allow for the list to be able to expand by taking advantage of the pointers which are a part of each node.

#### operation: remove()
The remove operation is suppose to undo the effect of the add operation of the linked list.  There are a couple ways to implement the operation, whether it is by allowing the user to give the function the node to delete or by simply deleting the head node and setting the new head to the next node.  In this post, a basic remove() operation will be performed without any user input.  Instead of prompting the user for input, the remove() operation will remove the head and replace the head of the list with a new one.  This will ease the basic operation for demonstration but adding the search and remove functionality will not be a hard addition.  This will most likely be a necessary addition when the singly linked list is being used to build something that could be used in everyday life.
 
#### operation: peek()

#### operation: display()

### plan of execution: travel itinerary
