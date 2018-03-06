Binary Search:
---------------

logn 2

Linear search O(n)


Big O Notation:
--> Tells how fast an alogorithm is
--> It doesn't tell you speed in seconds

Binary search running time in Big O Notation is O(log n)

Some common Big O run times:
Here are five Big O run times that you’ll encounter a lot, sorted from fastest to slowest:
• O(log n), also known as log time. Example: Binary search.
• O(n), also known as linear time. Example: Simple search.
• O(n * log n). Example: A fast sorting algorithm, like quicksort (coming up in chapter 4).
• O(n2). Example: A slow sorting algorithm, like selection sort (coming up in chapter 2).
• O(n!). Example: A really slow algorithm, like the traveling salesperson (coming up next!).


Binary search worst performance : lets say i want to search element Anith which is every first element in the sorted list.. here you have to look every element 

Binary search becomes lots faster once data increases 

--> Binary search is a lot faster than simple search
--> O(log n) is faster than O(n), but it gets a lot faster once the list of items you are searching through grows.
--> Algorithm speed isn't measured in seconds.
--> Algorithm times are measured in terms of growth of an algorithm.
--> Algorithm times are written in "Big O Notation".


Selection Sort:
--------------
LinkedList:	
--> LinkedList are good for insertion of elements:
--> LinkedList split up and watch the movie. If there is memory you have space for linked list.
--> LinkedList are great if you are going to read all items one at a time: you can read one item, but it has to follow the address to the next item, so on, linked list are terrible.

Arrays:
-->Lets say we are going for a movie with friends and finding a place to sit in movie but another friend joins you, and there's no place for them i.e, side by side continuos that can fit the four of them. If another friend comes by, then again we have search of 5 seats continous. What a pain.
Let's say we are trying to added 10,000 elements to array but in memory do not have 10,000 slots together...then you cannot get slot for the array.
--> Arrays are great if you want to read random elements
--> Since you know every address in your item.
		  Arrays 	Lists
Reading   O(1)		O(n)
Insertion O(n)		O(1)
Deletion  O(n)		O(1)

With a list, elements are strewn all over, and one element stores
the address of the next one.
• Arrays allow fast reads.
• Linked lists allow fast inserts and deletes.
• All elements in the array should be the same type (all ints,
all doubles, and so on).

Quick Sort: 
It internally uses divide and conquer.. and recursive quick sort .. O(nlogn) on average

33 10 15 7

33--> pivot element
[10 15 7] 33 []
15--> Pivot element
7 10 15 33

In the average case, quicksort takes O(n log n) time. So you might be wondering:
• What do worst case and average case mean here?
• If quicksort is O(n log n) on average, but merge sort is O(n log n)
always, why not use merge sort? Isn’t it faster?

Hash:
O(1)--> Insertion, delettion, search 
O(n)--> Worst case scenario

HashTables: Hashtables are as fast as arrays at searching, and they are as fast as LinkedList in insertion and deletion

Code: 20128088
Access code: 1Asn!dLV
Password: Naveen532$
UserName: NitinAljapurdata
