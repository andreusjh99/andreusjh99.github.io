---
layout: post
title:  Data Structures in Python
read: 6
post-image: /assets/images/posts/7_py_datastructures/post.jpeg
description: Introduction to the built-in data structures of Python
categories: software development
---

---

![](/assets/images/posts/7_py_datastructures/post.jpeg)

Data structure is a way of storing and organising data. In **Python**, there are four built-in data structures:
- [list](#list)
- [tuple](#tuple)
- [set](#set)
- [dict](#dict)

This post focuses on the syntax and fundamental capabilities of the data structures.

# List {#list}

A list, as its name suggests, keeps data in a list. A list is an **ordered** collection, i.e. items in a list follow the order they were added into the list.

There are a few ways to instantiate a list:

{% highlight python %}

a = [] # empty list

# a list of identical items
b = [0]*10 # a list of 10 zeros

# a list of items
c = [1, 2, 3, 4, 5]

{% endhighlight %}

Note that in Python, items in a list need **not** be of the same data type. You can also have a list as one of the items.

{% highlight python %}
d = [1, 'hello', True, [1, 2, 'bye']]
{% endhighlight %}

Python lists are **mutable**. This means that the list can be changed:
- value of items in the list can be changed
- items can be added or removed from the list
  
To add items to a list:

{% highlight python %}

a = [1, 2, 3, 4]

a.append(5) # [1, 2, 3, 4, 5]

# append an entire list
a.extend([6, 7]) # [1, 2, 3, 4, 5, 6, 7]

# insert an item of value x at index i -> a.insert(x, i)
a.insert(8, 3) # [1, 2, 3, 8, 4, 5, 6, 7]

{% endhighlight %}

To remove items from a list:

{% highlight python %}

# remove item of index i -> del a[i]
del a[6] # [1, 2, 3, 8, 4, 5, 7]

# remove and return the last item
b = a.pop() # b = 7, a = [1, 2, 3, 8, 4, 5]

{% endhighlight %}

To retrieve an item from a list:

{% highlight python %}

# retrieve item at index i -> a[i]
c = a[3] # c = 8

# retrieve items from index i to j -> a[i:j+1]
d = a[1:5] # d = [2, 3, 8, 4, 5]

# retrieve last item
e = a[-1] # e = 5

{% endhighlight %}

A list can be used for multiple assignments, or **sequence unpacking**:

{% highlight python %}
u,v,w,x,y,z = a
# u = 1, v = 2, w = 3, ...
{% endhighlight %}

Other useful methods of a Python list:

{% highlight python %}
# returns index of first occurence of item
f = a.index(8) # f = 3

# count and return number of items with value x
g = a.count(8) # g = 1

# reverse a list in place
a.reverse() # a = [5, 4, 8, 3, 2, 1]

# return a copy of a list reversed
# this keeps the list in its original order, but returns a copy of the list reversed
h = reversed(a) # h = [1, 2, 3, 8, 4, 5], a = [5, 4, 8, 3, 2, 1]

# return a copy of the list
l = a.copy() # l = [5, 4, 8, 3, 2, 1]

# sort the list in place
a.sort() # a = [1, 2, 3, 4, 5, 8]

# return a copy of the sorted list
# this keeps the list unsorted, but returns a copy of the list sorted.
m = sorted(l) # m = [1, 2, 3, 4, 5, 8], l = [5, 4, 8, 3, 2, 1]

{% endhighlight %}

# Tuple {#tuple}

Tuple is a collection of items that are **ordered** and **immutable**. This means that, unlike a list, a tuple once created cannot be changed: value of items in a tuple cannot be changed, new items cannot be added, and no items can be removed from a tuple.

There are a few ways to instantiate a tuple:

{% highlight python %}

# a tuple of items
a = (1, 2, 3, 4)

b = (1, 'a', True, (1, 3, 4)) # a tuple containing a tuple

c = ('a',) # a tuple containing 1 item
# Note the COMMA. Without the comma, c = 'a' and not a tuple.

{% endhighlight %}

To retrieve an item from a tuple:

{% highlight python %}

# retrieve item at index i -> a[i]
d = a[3] # d = 4

# retrieve items from index i to j -> a[i:j+1]
e = a[1:3] # e = (2, 3)

# retrieve last item
f = a[-1] # f = 4

{% endhighlight %}

With tuples, you can perform sequence unpacking and **sequence packing**.

{% highlight python %}

# sequence unpacking
g, h, l, m = a
# g = 1, h = 2, l = 3, m = 4

# sequence packing
x = 1
y = True
z = 'hello'
n = x, y, z 
# n = (1, True, 'hello')

{% endhighlight %}

Other useful methods of a Python tuple:

{% highlight python %}
# returns index of first occurence of item
o = a.index(2) # o = 1

# count and return number of items with value x
p = a.count(2) # p = 1

{% endhighlight %}

<hr style="border-style: dashed">

## When will you use a tuple over a list?
Both list and tuple are ordered collections, but the key difference is that list is mutable while tuple is immutable.

You should use a tuple to store data if you know that it will not be changed or when you do not want them changed.
- Tuples are more **memory-efficient** to store
- Tuples are more **time-efficient** to retrieve its items.
- Tuples can be used as keys in a [dictionary](#dict) while lists cannot.
<hr style="border-style: dashed">

# Set {#set}
A set is an **unordered** and **mutable** collection of objects. Since it is unordered, there is no certainty about the order the items in a set will appear. 

In a set there is no duplicate item. You usually use a set when the **existence** of an object in a collection is more important than the order or how many times it occurs.

To create a set:
{% highlight python %}

# empty set
a = set()

# initialise a set
b = {1, 2, 3, 4}

c = {1, 2, 3, 3, 3, 2} # c = {1, 2, 3}

# add items to a set
c.add(5) # c = {1, 2, 3, 5}

# remove items from a set
c.remove(3) # c = {1, 2, 5}

{% endhighlight %}

<p>
The greatest advantage of a set over a list is its <b>cost efficiency in searching</b>. Searching in a list will induce a worst case efficiency of $n$ where $n$ is the length of the list, while searching in a set will induce a worst case efficiency of 1 regardless of the size of the set.
</p>

# Dict {#dict}

A dictionary is an **ordered** and **mutable** collection of items in the form of a **key-value pair**. Each item in a list has a key and a value. The key is used to retrieve the value of the item. No duplicates are allowed in a dict, which means that each key can only appear once in a dict.

To create a dict:
{% highlight python %}

# empty dict
a = dict()
a = {}

# initialise a dict
b = {"apples": 1, "oranges": 2, "pears": 3}

# add items to a dict
b["bananas"] = 4
# b = {"apples": 1, "oranges": 2, "pears": 3, "bananas": 4}

# change value of item in a dict
b["apples"] = True
# b = {"apples": True, "oranges": 2, "pears": 3, "bananas": 4}

{% endhighlight %}

To remove items from a dict: 

{% highlight python %}
# remove and return item by key
c = b.pop("oranges") # c = 2, b = {"apples": True, "pears": 3, "bananas": 4}

# remove and return last inserted item
d = b.popitem() # d = ("bananas", 4), b = {"apples": True, "pears": 3}

{% endhighlight %}

As mentioned above, a tuple can be used as a key due to its immutability, while a list cannot be used. Note, however, that the tuple **cannot** contain a list in this case or it cannot be used as a key as well.

Similar to a set, a huge advantage of a dict is its **cost efficiency in searching**, which is 1 regardless of the size of the dictionary.

# Conclusion

There are 4 built-in data structures in Python:
- **list**: ordered and mutable
- **tuple**: ordered and immutable
- **set**: unordered and mutable
- **dict**: ordered and mutable

From these 4 fundamental data structures, more complex data structures like a queue, stack or graph can be built.
   
---

**Author**: <a href="https://github.com/andreusjh99" target="_blank">Chia Jing Heng (andreusjh99)</a>