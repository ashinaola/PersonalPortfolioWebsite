---
layout: post
type: posts
title: building then using a singly-linked list (part 1)
date: 2023-10-08
categories: [Data structures and Algorithms]
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
The first portion of the travel itinerary will be made of the singly-linked list that we just went over.  The program's logic will contain the same operations as the examples that I went over:
- addCity()
- leftCity()
- deleteCity(city* user)
- displayItinerary()
- searchItinerary(string searchstring)

There are a couple differences between these operations and the example operations that I discussed previously.  The leftCity will implement the previously discussed head deletion of the list.  This is to emulate leaving one city and travelling to the next.  The deleteCity() function will implement the search then delete that was mentioned previously.  The other functions will generally work just like the example functions of the basic singly-linked list.

I also am going to add a method to calculate the distance between the two different cities so that the distance between the two can be displayed.  The other challenge would also be having the method work for different cities.  The current plan is to have a .csv of the different cities in the world and the program would then query against the file and return the necessary attributes such as latitude and longtitude in order to calculate the distance.  This would be most of the features that I plan on implementing and I would consider this to be the core of the application.

Starting from adding a city onto the itinerary, I am going to try to build a planner using the previous methods discussed along with a few other methods to add a couple more features to the list to improve the experience of using the list to build travel itineraries.  By adding a .csv to the program, I am hoping that range of what is covered by the list is expanded compared to building a list by hand.

#### addCity: adding a city to the itinerary
After making the constructor and deconstructor of the itinerary, we will work with the addCity() function first.  Compared to the previously mentioned add() function, there could be a difference in how the addCity function works.  Previously, the example linked list would add new nodes set the new node to the head and set its next pointer to the previous head:
```
Before:
    A -> B -> C
After:
    --- A -> B -> C
    |
    D
``` 

In the case of the itinerary, this would mean that if we added the cities in the same way, the itinerary would be displaying the cities in reverse order.  So we will change the add() operation of the linked list in order to traverse down the list and set the node to be the new last node by using the pointer to append the node to the linked list.  The performance of this function will be linear (*O(n)*) due to the function traversing through the list to get to the final index where the next pointer value is null.

Here is the final code that I have as of the time of the post.  One reason for this wording is because code can be seen as a living thing that needs to constantly adapt to changing requirements and feature addition.  I hope that over time, I will improve on the performance of the logic and will update the post on any additions if they are crucial:
```
void addCity(std::string cityName, float cityLong, float cityLat, 
std::vector<std::string> cityLandMarks, std::vector<float> cityLMLong, std::vector<float> cityLMLat) {
    city* newCity = new city;
    newCity->name = cityName;
    newCity->longtitude = cityLong;
    newCity->latitude = cityLat;
    newCity->landmarks = cityLandMarks;
    newCity->landmarkLongtitudes = cityLMLong;
    newCity->landmarkLatitudes = cityLMLat;
            
    if(firstCity == nullptr) {
        firstCity = newCity;
    } else {
        city* lastCity = firstCity;
        while(lastCity->nextCity != nullptr) {
            newCity = newCity->nextCity;
        }
        lastCity->nextCity = newCity;    
    }
}
```

#### leftCity: leaving a city
After leaving a city on the itinerary and moving to the next one, there should be a method to delete the first city or the current city on the itinerary.  Here is a visual representation of the idea behind leftCity():
```
Before leftCity():
Tokyo -> Yokohama -> Chiba -> Sendai -> Tokyo

After leftCity():
Yokohama -> Chiba -> Sendai -> Tokyo
```

So in order to execute this on the linked list, the idea would be to take the head of the list and then set the new head to the next node on the list.  The node then gets deleted afterwards so as to prevent any complications from dangling references.  The performance of this function will be constant (*O(1)*) due to the function setting the head of the list to the next node and deleting the previous head.  These two operations will take the same amount of time to run no matter how large the list is.

Here is the final code as of finalizing this post:
```
void leftCity() {
    if(firstCity == nullptr) {
        return;
    } else {
        city* tempCity = firstCity;
        firstCity = firstCity->nextCity;
        delete tempCity;
    }
}
```

#### searchItinerary: show whether a city is on the itinerary
The next function I want to implement is a function to take a string that the user provided for the program and then search the list to see if the list contains the string.  The plan is to set a flag to false and return the flag as is if the function doesn't come across the user provided string and return true if the string is found.  Since we are looking at a linked list of nodes, the main difference in the matching step would be that it would require comparing an object attribute to the string and not a straight comparison.  The worst case performance for this approach is definitely going to be *O(n)* because this takes an iterator and traverses down the list to find the user string.

Here is the final code:
```
bool searchItinerary(std::string searchString) {
    bool foundFlag;
    city* iterator = firstCity;

    while(iterator->nextCity->name != searchString) {
        iterator = iterator->nextCity;
    }

    if(iterator->nextCity == nullptr && iterator->name != searchString) {
        foundFlag = false;
    } else {
        foundFlag = true;
    }
    return foundFlag;
}
```

#### deleteCity: undoing a wrong addition to the list
In order to allow a user to relax when using the program, there needs to be a more flexible delete function outside of simply leaving the city.  This is exactly where the feature will come in.  The goal is to provide a less costly way to undo a mistake in order to improve the experience of using the program.  This is the main idea of what the function should accomplish:
```
Before:
    A -> B -> C(mistake) -> D

After:
    A -> B -> D
```
As with searchItinerary, the deleteCity function will have a worst-case runtime of *O(n)*.  As a matter of fact, in order to prevent any kind of repetition from occuring, searchItinerary can be used to implement deleteCity.  This can allow for some brevity and less confusion when maintaining the code.

Here is a glimps at the final code for the function:
```
void deleteCity(std::string userInput) {
    city* iterator = firstCity;
    
    while(iterator->nextCity->name != userInput) {
        iterator = iterator->nextCity;
    }

    city* temp = iterator->nextCity;
    iterator->nextCity = iterator->nextCity->nextCity;
    delete temp;
}
```

#### displayItinerary: show the list contents
The displayItinerary function is an important part of the program since this allows for the user to understand the contents of the structure that they are interacting with.  This is a crucial part of using the program as well as building the program.  The display function plays an important role in debugging.  This includes when trying to figure out whether the application is executing the queries against the .csv file or if the structure is not properly adding cities.  The worst case runtime for the displayItinerary function will be *o(n)* just like the previously discussed function.  This is because the iterator has to traverse down the list and print the attributes of each node.

Here is the final code of displayItinerary():
```
void displayItinerary() {
    city* iterator = firstCity;

    while(iterator->nextCity != nullptr) {
        std::cout << iterator->name << '\n';
        iterator = iterator->nextCity;
    }    
}
```

#### calcDistance: calculate the distances
The fundamental experience will also have the ability to know just how far each city is in terms of distance from each other.  This isn't necessarily by hours or minutes but by distance.  This will also be a direct calculation using the distance formula as well as the longtitude and latitude of each city.  One of the problems with using the distance formula is that the formula gives a much less practical interpretation of the distance between the cities since there isn't any consideration of geographical barriers which could lengthen the distance relative to what is provided by the distance formula.  However for this function, we will provide the distance using the classical distance formula.

So here is the tentative code for the distance function:
```
float computeDistance(city* source, city* dest) {
    float source_x = source->longtitude;
    float source_y = source->latitude;
    float dest_x = dest->longtitude;
    float dest_y = dest->latitude;

    return sqrt(pow((source_x-dest_x),2) + pow((source_y-dest_y),2));
}
```

### the interface: a program that will live on the terminal
The plan for the application is for the installation and use to be 100% through the command line.  I personally enjoy using the command line for work and personal use.  In this section, the sequence of user actions along with the overall interface of the application will be presented.  It will be a very simple application that you can be able to run on the terminal.  

#### sequence of user action
This is the tentative plan for setting up the itinerary.  There will be five possible things that the user can do with the application:
```
1. Adding a city to the itinerary
2. Deleting a city from the itinerary
3. Leaving a city
4. Searching the itinerary
5. Displaying the itinerary contents
```
These actions will be easier to navigate & select from if the choices were displayed in the form of a menu.  Users can select which actions to take when building their itineraries.

From these five user actions, you can see that it is a very basic itinerary without features like purchasing hotels and trips to go between the cities.  One of the limitations is the actual logic of the application not being complex enough to accommodate those actions.  In order to better understand how the user will interact with this application, there needs to be a clearer definition of what the application's logic expects from the user.  By having a sequence of events clearly established, it will make the designing and implementation process more easier.

***adding a city to the itinerary***
```
Before: A list of n cities
After: A list of n+1 cities

Sequence:   1. Ask user for a string which will be used to initialize a node 
               with the string as the city name
            2. Check whether the provided string is available on the database
                * If present        -> create then add the node to the itinerary
                * If not present    -> return an error message stating that the 
                                       string is not on the csv
```

***deleting a city from the itinerary***
```
Before: A list of n+1 cities
After: A list of n cities

Sequence:   1. Display the itinerary to the user
            2. User then selects which string to delete
            3. Error checking:
                ~ Found     -> Delete
                ~ Not found -> Return error message saying city not on the list
            4. Display updated itinerary
```

***leaving a city***
```
Before: A list of n cities
After: A list of n-1 cities

Sequence:   1. After the user selects leaving, execute leaveCity()
            2. Display the updated itinerary to the user
```

***searching the itinerary***
```
Before: A list of n cities
After: A list of n cities

Sequence:   1. Prompt user to enter a string
            2. Traverse down the itinerary, looking for the string
                ~ if found: break the loop and return true to user
                ~ if not found: return false to user
```

***displaying the itinerary contents***
```
Before: A list of n cities
After: A list of n cities

Sequence:   1. Execute the displayItinerary() function when the user selects
               display itinerary from the menu
```

#### application interface
The main idea behind the interface is to have a menu that the user can be able to choose from at all times.  Since this will be an application which will be ran on the command line, one of the most important parts of having a great application is to be able to allow for the user to take advantage of the increased flexibility that the command line offers relative to the graphical user interface.  Each operation of the itinerary would have its own set of menus, but users should always be able to access a main menu that allows them to be able to perform the previously mentioned functions anytime during use of the program.  We will implement the application interface in the next part and work with user input.  In the final part 3, we are going to get the application to interact with the .csv file in order to get the distances between the cities that the user enters into the TravelPlanner.  This will allow us to have a full functioning application that we used a singly linked list to build!  I hope you are as excited as I am.