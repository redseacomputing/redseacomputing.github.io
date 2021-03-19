---
layout: post
title:  "Test driven development is not a crime part 3- What tests to write"
date:   2021-03-20 00:03:00 +0100
categories: tdd java
permalink: /:year/:title
---

![preparation of unit tests](../images/TDD3-preparation-of-unit-tests.png)

# Tests to write

In the last blog of this series, we mentioned about the fact that we have to ask the right questions.

Testlist is a pattern from the book "Test-Driven Development by Example" from Kent Beck.
You can use your search engine of choice to look forward for more great sources of this kind by typing 
"Behaviour driven development" and "Specification by example".

Let's consider some meaningful tests from specification with test lists.

### Specification
>Customers can buy CDs, searching on the title and the artist.
Record labels send batches of CDs to the warehouse.
Customers can only order titles that are in stock.

You can use your specification, to create a meaningful testlist to work with it afterwards.

###Testlist:

Buy a CD
- [ ] CD is in stock - stock count is reduced by quantity
- [ ] Insufficient stock - throw an exception

Searching for CD
- [ ] Its in catalogue - return the CD info
- [ ] No match = return nothing
- [ ] Multiple CDs - return list

Receiving stock from a label
- [ ] Single title thats in catalogue - add copies to that CD's stock
- [ ] Not in catalogue - add it, and add copies to stock
- [ ] Multiple CDs - any new CDs added to catalogue, and stock added to each CD

Now you can move forward and triangulate you're TDD-cycle over 
you're testlist as a checklist that comes directly from the specification.

### Hint: Obvious implementations 
During you'r TDD-cycle, it is not necessary to triangulate many rotations on obvious implementation details.

This is part three of the beginner series for TDD. Here is part four.