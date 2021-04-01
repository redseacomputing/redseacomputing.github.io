---
layout: post
title:  "Test-first is not a crime"
date:   2021-01-0 13:09:40 +0100
categories: tdd java
permalink: /:year/:title
---
I think its a pitfall when people come to the point to 
study software development.
There is a lot of new stuff to hear, read, learn, understand
and to practice.

Ad abstractum, a software student have to know the programming language first,
before he/she can learn to code effectively. After learning the code language, 
there were hundreds of little exercises did it the wrong way.

>New behaviour is very hard to obtain.

As I could saw on several pair programming sessions, there are developers
out there who know test-first and cannot change their old behavior from 
learning/study days.

"Fast" developers pick up the keyboard, implement some functionality, 
recognize after a few hours that their code is not that good as expected
and change everything from scratch, though.

>Big changes cost time. And time is money.

However, the great advantage of test-first is that it forces 
developers to think about their work before implementation and reduces the need
for later changes.

When developers invest time in writing test cases, 
they have a very good idea of how the unit works and major changes are less common.
Also, it is not that expensive as much, when you know that test cases are a 
brief form of documentation, too.

The test-first approach is a first step to test-driven development (TDD). 
The main goal is the maintenance and the upkeeping of software products. 
Earlier development models suffered from this, such as the waterfall 
model, which put testing at the end - after analysis, design and implementation. 

The consequence of this sequence was often a large chunk of code that was impossible 
to test. With TDD that won't happen. Nowadays, developers should 
think about how to test the result of any architecture, design, or unit right 
from the start.

>Test-driven development makes your design significantly better.


### Test, Implement, Test, Implement

* #### Step 1: 
  
  Think about which class and method to write. 
  Create source code for the class and for the variables / methods / constructors so 
  that it can be compiled. The code blocks are empty, but contain a return statement.
  
* #### Step 2:
  
  Write the API documentation for the methods 
  and consider which parameters, return types and exceptions are necessary.
  
* #### Step 3:

  Implement a test case and let it fail

* #### Step 4:

  Implement less logic as possible to make the test pass

* #### Step 5:

  Consider if there are any new things to test? After that, 
  go back to step 3 and repeat


### We have no time. Should I really test?

Developers are expensive. Customers want get things done. Understandable.
But no one asks wether the product unit was "done" at 4:30 pm or was 
done at 4:45 pm. 
Everyone knows what happens 6 months 
later when no one knows how to implement 
a new feature and things 
getting NOT done. Understandable, too.

>There is no time anymore because there are/were no tests.

Ultimately, it is the responsibility of the developer as its own
to create a high quality product.

With one word: Yes.

Learn it. Train it. Do it.
The sooner a test fails (triggered by a modification),
the sooner the error can be corrected.

Therefore, a good time is before and after every change and for sure
before pushing to a version control system.


### Links

#### [test-first "FizzBuzz" on github](https://github.com/redseacomputing/FizzBuzz)
#### [TDD on wikipedia](https://en.wikipedia.org/wiki/Test-driven_development)