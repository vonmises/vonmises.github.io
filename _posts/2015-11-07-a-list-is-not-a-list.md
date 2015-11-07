---
layout: post
title: 'a "list" is not a list'
description: ""
category: 
tags: []
---
{% include JB/setup %}

A house is not a home and a [Python] list is not a [linked] list. I would have thought that, as much as Python is used by a lot of compsci enthusiasts, I would have heard before now that lists in the language are not really lists as one learns in introductory programming. I mean, they are only used all over the place whenever one needs a collection, and in list comprehensions.

It turns out that a Python "list" is what other languages would call an array. In Python, a list is a contiguous block of memory to contain the values that will be assigned to it, whereas in other languages, lists are implemented as a series of nodes with each node (except for the last) keeping a reference to the next one (singly-linked list), or each one keeping a reference to the next and previous one (doubly-linked list).

There are important differences between arrays and lists with respect to normal operations such as inserting and accessing an element, as well as other considerations such as [which sorting algorithm](http://www.geeksforgeeks.org/why-quick-sort-preferred-for-arrays-and-merge-sort-for-linked-lists/ "Why Quick Sort preferred for Arrays and Merge Sort for Linked Lists?") one should use. I will only demonstrate one interesting insertion surprise I came upon recently.

In a linked list, inserting a list at the beginning takes constant time since you're just placing the element somewhere and marking it as the first node in the list (aka head) and pointing it to the previous head. So it doesn't matter if you have a billion elements or two, and need to insert a new item at the head.

But with an array, in order to put something at the head, you have to either move everything over one step to the right to make space for the new item or copy the elements over into a new array with the new element in the first position. In some cases, both expensive operations happen as we'll see without further ado.

The following are two examples of adding a sequence of integers to a list and ensuring that they are arranged in order of the most recent insertions first (stack-like). The first one appends integers to the list and reverses the order, while the second one inserts the integers at the beginning so that they are ordered from the most recent insertion onwards.

<pre>
import time

count = 10**5

# add integers to list and then reverse
start = time.time()
nums = []

for i in range(count):
    nums.append(i)

nums.reverse()
elapsed = time.time() - start

print("append -> ", elapsed)

# add integers to list at the beginning
start = time.time()
nums = []

for i in range(count):
    nums.insert(0, i)

elapsed = time.time() - start

print("insert -> ", elapsed)
</pre>

Unfortunately for you, there's no surprise as I already explained what would happen. It would have been nice to just put the code and let you figure out which one's faster and by how much.

The <code>insert</code> method is a *__lot__* slower than the <code>append</code> and <code>reverse</code> method even though it's a bit tidier and doesn't appear that it would be much slower:

<pre>
[ $ ]>  python test.py 
append ->  0.010341644287109375
insert ->  2.192379951477051

[ $ ]>  python test.py 
append ->  0.01081085205078125
insert ->  2.1945884227752686

[ $ ]>  python test.py 
append ->  0.010373592376708984
insert ->  2.1757354736328125
</pre>

It's over 200 times slower, in fact, for the case when <code>count</code> = 10<sup>5</sup>. When <code>count</code> = 10<sup>6</sup>, it's not even funny.

<pre>
[ $ ]>  python test.py 
append ->  0.10022330284118652
insert ->  276.6680340766907
</pre>

It's well over 2000 times slower (in this case, 2760) than the <code>append</code> and <code>reverse</code> method. Note that the other method also slowed down (by a factor of ten, which is what we increased <code>count</code> by), but the <code>insert</code> method slowed down by a factor of a hundred, which brings us to the end of the demo.

The running time increases quadratically(n&sup2;) for the slow method and linearly(n) for the faster one.

So, now you know what's in a name. Just because collection types tend to behave the same way, does not mean you shouldn't know how they work under the covers. It's more than just "nice to know" how they are implemented as it can mean the difference between bringing your app or server to its knees with such simple, well-meaning logic, or having an efficient system humming along quietly.

Read, also, about how sorting and searching algorithms can be affected by your choice of data structures. There's a reason those two topics are taught hand-in-hand.

(For your benchmarking purposes, there's a module called <code>timeit</code> you might want to read about. Quick and dirty was good enough for this demo.)