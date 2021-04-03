---
layout: post
title:  "TDD for kickstarters- part 4"
date:   2021-03-19 12:00:04 +0100
categories: tdd java
permalink: /:year/:title
---
![duplication](../images/TDD/TDD4-duplication.png)

## Relationship between Duplication and Design

Duplicate code is the opposite of reuse. When you remove duplication, you end up
introducing reusable abstractions. From a design point of view,
duplication is very interesting.

#### Hint: Refactor duplication
>Pay attention to duplication when you are refactoring after each test.
Eliminate obvious duplication and don't wait to get more of it.
More duplication is harder to eliminate. [Don't repeat yourself](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

## When do we remove the duplication?

It's important not to jump in too early. The risk when you refactor code to
create abstractions, ends you up introducing the wrong abstractions.
That would be a brief form of ["You ain't gonna need it"](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it).

You operate on a design principal called ["The rule of three"](https://en.wikipedia.org/wiki/Rule_of_three_%28computer_programming%29).
It helps you to see patterns, and it helps you to not getting too late to eliminate duplication.

So you have to wait for **exactly** three duplications and check what's going on.

## Handle duplication in your test suite with parameterized tests

You can use little helper methods to maintain your test code.
If there are a lot of similar test cases, you can use parameterized tests.
Check the documentation from your test framework of choice. 

Naming of parameterized tests:<br>
Describe the rule, and not the example. So reading it is more likely a specification.

#### Hint: Naming
At last, that when you refactor, you can refactor as long as you can, to write meaningful names
to methods, so the code will become really easy to read.

This is part four of the TDD kickstart beginner series. Here is [part 5](https://redseacomputing.github.io/2021/TDD5-inside-out-and-outside-in)