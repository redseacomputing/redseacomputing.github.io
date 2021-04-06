---
layout: post
title:  "Refactoring for kickstarters- Comment"
date:   2021-03-31 12:00:02 +0100
categories: refactoring
permalink: /:year/:title
---

## Code Smell of the year

![Comment](../images/Refactoring/Refactor-comment.png)
 
<br>

Comments indicate that the readability of the code is not as good as it could be. 
It would therefore be advisable to work on the naming of the code.
The naming in programming would lead to a long discussion and is going forward to Clean Code. Here, too, there are do's and don'ts.
Anyway, comments should be on the refactor's hit list.

Of course, you shouldn't sit in the bulldozer here: Comments are a useful way of giving clues about the code. 
That is why you should use them as such.

A comment, if it already exists, should at most say **WHY** is something done in some way or **WHERE** you can go further for specific information.
Therefore, links or references to other resources would be okay to make it easier for readers to understand.

First, you should know what the code is doing. Most of the time, it's easy to
extract code into a method and take those method names from the comment to be eliminated.
You name the method after **WHAT** it does. In this way you make sure that your code stays legible.

<br>

This is step two of the first part of the Refactoring kickstart beginner series. Here is [step 3](https://redseacomputing.github.io/2021/Refactoring1-3-long-method).