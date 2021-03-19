---
layout: post
title:  "Test driven development is not a crime-part 4"
date:   2021-03-20 00:04:00 +0100
categories: tdd java
permalink: /:year/:title
---
![duplication](../images/TDD4-duplication.png)

## Relationship between Duplication and Design

Duplicate code is the opposite of reuse. When you remove duplication, you end up
introducing reusable abstractions. From a design point of view
duplication in your code is very interesting.

>You should pay particular attention to that when you're refactoring after passing each test.

## When do we remove the duplication?
It's important not to jump in too early. The risk when you refactor code to
create abstractions is that you end up introducing the wrong abstractions.
That happen very often because we haven't seen enough examples to really just
sort to see what the pattern is here, yet we have to see the patterns.

You operate on a design principal called "The rule of three".
It helps you to see the mentioned patterns and it helps you to not getting to late to eliminate duplication.
>More duplication is harder to eliminate

So you have to wait for three duplications and check what's going on.

In software development we have finite time, so if something takes longer its less likely to happen.
It's as simple as that. That's just the way the world works.

## Handle duplication with parameterized tests

You can use little helper methods to maintain your test code.
If there are a lot of similiar test cases, you can use parameterized tests.
Check the documentation from your test framework of choice. 

Naming of parameterized tests:
Describe the rule, and not the example. So it is reading it more like a specification.
This is like a double win.

At last, that when you refactor, you can refactor as long as you can to write meaningful names
to methods, so the code will become really easy to read.

This is part four of the TDD kickstart beginner series. Here is part [part 5](https://redseacomputing.github.io/2021/TDD5)