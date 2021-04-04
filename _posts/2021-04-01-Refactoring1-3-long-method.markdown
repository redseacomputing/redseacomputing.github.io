---
layout: post
title:  "Refactoring for kickstarters- Long method"
date:   2021-03-31 12:00:03 +0100
categories: refactoring
permalink: /:year/:title
---

## Code Smell of the year

![Long method](../images/Refactoring/Refactor-long-methods.png)

<br>

Long methods mean large pieces that are reused. 
It is an indicator that the [Single-responsibility principle](https://en.wikipedia.org/wiki/Single-responsibility_principle) 
is being violated.

A method should generally work on a [Single Level of Abstraction](http://principles-wiki.net/principles:single_level_of_abstraction).
It would be a mess to invoke a low level (e.g.: the operating file system) and a high level 
function (a collection in your main memory) in the same piece of code.
Inspect the code inside the method. What is it really doing?

Your indicator could be a method name with AND in there, like e.g.: `getDataFromFilesystemAndValidateIt().

<br>
Break the code into smaller pieces. Extract everything out of it to use it afterwards.

<br>

>
>Hint: Keep in mind that there is no technical modification of the code during the refactoring step.
>

<br>

This is step three of the first part of the Refactoring kickstart beginner series. Here is [step 4](https://redseacomputing.github.io/2021/Refactoring1-4-long-parameterlist).