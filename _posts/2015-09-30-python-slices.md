---
layout: post
title: "python slices"
description: ""
category: 
tags: []
---
{% include JB/setup %}

Slicing in Python can be confusing to a newcomer. Or--more accurately--the documentation
explaining the arguments accepted to perform a slice of a sequence is confusing.
A slice is an ordered subset of items derived from a sequence. You can specify that you
want the entire set (I didn't say it has to be a "proper subset") or a proper subset
from some specified position to another.

The documentation says that you can also specify a step which can be used to skip items
between the desired values. Here is the definition:

> slice([start], stop[, step])

My problem is that the "stop" doesn't quite mean what one might think it means. While
"start" means: start from the value/position I indicate, "stop" means: stop at the 
value/position I indicate--*__minus one__*. 

<pre>
numbers = range(10)
for i in numbers: print(i) # will print 0 to 9
for i in numbers[3:5]: print(i) # 3 4
</pre>

One of the things that influenced the breaking changes in Python 3, I heard, was to get
rid of inconsistencies and quirks. It's certainly inconsistent for the "start" and "stop"
nouns to have different semantics as far as the value they're pointing to is concerned.
They should both point to the value/position indicated.

Why I've never seen the "minus one" in the official documentation, I'll
never know but it's often a source of confusion for newcomers. The range function itself
is confusing on first use but that's a topic for another day. Usually, you find out in a tutorial
about how slices really work and, to me, it would have been preferable if it were fixed
but it's used in many heavily-used libraries so it's unlikely to get fixed.

Anyway, I like most of the language thus far, so--given that all languages have their
quirks--I can do what I've always done and avoid using features in a way I don't like.