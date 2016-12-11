---
layout: post
title: How does increasing size work?
categories: [java, programming]
tags: [java, arraylist]
description: Sample placeholder post.
---

Hi everyone,

Today, I'm back with a basic question about ArrayList.


As we know ArrayList is a resizeable array, that means an array list are created with initial size and its size can be increased as needed.
But, have you ever wondered about default initial size of an array list, how increasing size works?

**1. Default initial size of an arraylist.**

And here is the answer:

![Capture.PNG](/assets/media/2016-12-11-1.PNG)

Now, I'm using ``jdk1.7.0_79``. As we see at above picture, the ``DEFAULT_CAPACITY = 10``. When we didn't declare the capacity of ArrayList, the default capacity is ``10``.

**2. How does increasing size work?**

First at all, let's consider about below method of class ``ArrayList.java`` (``jdk1.7.0_79``)

![Capture2.PNG](/assets/media/2016-12-11-2.PNG)

When you tell JVM that you would like to add one more element to an existing arraylist. And here is what happened.

- get ``oldCapacity`` by ``length`` property

- create a ``newCapacity`` by ``newCapacity = oldCapacity + (Capacity >>1)``. That's same with ``newCapacity = (oldCapacity*3)/2``.
Example: ``oldCapacity = 10``. And then, ``newCapacity = 10*3/2 = 15``.

- if ``newCapacity < minCapacity`` then it uses ``minCapacity`` as new capacity of array list.

- in another case, if ``newCapacity`` is more than maximum size (that's declared by JVM), an ``OutOfMemoryError`` will be throwed.

- finally, a new array list will be created , all data of old arrays will be copied to it, and old array list will be grabage collected.

_In another way, we can say , ArrayList increases its size by 50%_

That's all.

Thanks for reading :D

Have a nice weekend.
