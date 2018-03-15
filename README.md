# producer-consumer

## Problem Statement
Instructions :)

1.	This is a coding challenge. The task is to create a webpage as per a given design.
2.	To be developed using HTML5, CSS3, and JavaScript. You may choose to use Bootstrap and JQuery.

Concept :)
	Item 
•	a random integer between 0 and 9 (including 0 and 9)

	Producer 
•	Generates an item
•	Inserts the item in the Buffer (array)  if it is not full else skips it.
•	If the item already exists in the buffer then it skips it.(No duplicate)	

	Consumer
•	Retrieves an item from the buffer and removes it from the buffer. (array deletion operation)	
	
	Buffer
•	It is a queue which follows First In First Out approach of inserting and removing items (use array)


Tasks and Guidelines	:)
	Everything should fit on the screen.
	Assume Dimensions and Colors on your own
	Header section
•	Has a height of 60px and padding of 5px
•	Display title "Simple producer-consumer problem" with font-size 18px at the center from all sides.
		
	Left panel contains following buttons
•	Produce - onClick - generate an Item, display it into Items produced component and insert it into the buffer.
•	Consume - onClick - consume an Item from the buffer and display it into Items consumed component.		
	Right panel
		divide UI into following two scrollable sections
•	Items Produced component - list of all the Items generated till now
•	Items Consumed component - list of all the Items consumed till now
		
	Footer section
•	UI which displays the real-time operations on buffer
•	Buffer can hold maximum of 10 items, where each slot is represented by an empty squares
•	The leftmost slot represents the Tail of the Queue, where a new item is inserted.			
		
	
MileStones :)
1.	Get the Visual UI components ready
2.	Producer produces Item and inserts it into buffer
3.	Consumer consumes items from buffer
Good to have
4.	Visual representation of the operations on buffer
5.	Able to start and stop producer and consumer





> A Vue.js project

## Description
I have used Vuejs + Bootstrap + [Vuestrap](https://wffranco.github.io/vue-strap) in my Project.
## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).
