---
layout: post
title:  "Legacy Code"
date:   2021-04-05 12:00:00 +0100
categories: legacy code tdd refactoring
permalink: /:year/:title
---

![Legacy Code](../images/Legacy Code/LegacyCode.png)
 

# Code in operation

Legacy code is code in operation and expensive to change.
The system grows and grows, and at some point no one dare to make changes
anymore. A result is a system with only low level maintenance operations
like fixing bugs.

Legacy systems can become a millstone around a business's neck. **They can hold 
us back from being innovative**.

>A legacy system is a problem of the business

As developers, this cannot excuse us to inform the software operator about it. 
Sure, it's their problem, but...

>It is your responsibility to inform the owners 
about this, and also to maintain their product to the best of your knowledge.
> 
>That's why they hired you.



### What makes it so difficult to change?
Usually it's our inability to test it quickly. We make changes
to legacy code, and testing feedback takes long or does not exist.

Maybe we are testing it manually, or we have a slow running suite of system tests that
we are relying on.

We maybe break code, and we might find it hours, days or weeks later out. 
Sometimes we might not know until it reaches production.

The cost of fixing those bugs is much higher. Teams that are 
working on legacy code spend all of their time to fixing bugs.

[Working effectively with legacy code](https://www.youtube.com/watch?v=wRtJRkRIa2s) describes processes, ideas and principles 
for making changes to legacy code safely and economically.

Michael's definition of legacy code is:
>Code that does not have fast running and automated tests.

The idea behind is getting your [system under test](https://en.wikipedia.org/wiki/System_under_test).

Here is a brief form of a simple algorithm:

* Identify the code snippet that will need to be changed
* Identify the units **around** them. You are looking here for units that won't change much.
* Write some tests around those units.
* Break the dependencies that can stop you from writing your tests.