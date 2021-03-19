---
layout: post
title:  "Test driven development is not a crime part 1- The TDD cycle"
date:   2021-03-20 00:01:00 +0100
categories: tdd java
permalink: /:year/:title
---

![redsea logo](../images/TDD1-tdd-cycle.png)




The cycle of test driven development contains three steps:

1. You start by writing a test that fails, which describes something you want your code
to do that it currently doesn't.

2. Then you write the simplest thing you can think of to get that test passing to the simplest quickest thing
that comes into your mind.

3. If necessary, you refactor the code so that going forward that the code is going to be as easy to change
as possible. You look here for code that is hard to understand, for problems with complexity or duplication
or dependencies. Its the refactoring step where a lot of the design in TDD happens.

> TDD is driving the design and development of your code using tests as your specification

Let`s use an example with a shopping basket.
You start by writing a test. Not the ShoppingBasket class.
And start with the simplest test case you imagine of the ShoppingBasketTest class (an empty ShoppingBasket).

    @Test
    void totalOfEmptyBasket() {
        ShoppingBasket basket = new ShoppingBasket();
        assertEquals(0.0d, basket.getTotalAmount(), 0.0d);
    }

Thats how TDD works. You dont write a Production-Code class.
First, you write a test that use a (non-existent) ProductionCode class,
and then you implement that class.
With each test, you make just a few design decisions `and then you
write the code that this test requires`.

Now, from the test case, you can implement the simplest way to getting it.

    public class ShoppingBasket {
        public double getTotalAmount() {
          return 0d;
        }
    }

Here are some following tests for the interested reader as an exercise.
* totalOfSingleItem
* totalOfTwoItems

Hint: If something changes, look first at your `test code`, don't edit it in your production code unnecessarily!

> If you are looking at your tests that runs correctly, these are your specification steps of your software solution that are up and running now.

After each iteration, you should come back to your TestSuite and maintain your test code and/or your production code little bit, if necessary.
This is the third step of the TDD cycle. For further reading you can check my refactoring series later.

This is part one of the TDD kickstart beginner series. Here is part two.