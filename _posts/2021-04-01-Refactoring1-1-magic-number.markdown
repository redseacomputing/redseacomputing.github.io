---
layout: post
title:  "Refactoring for kickstarters- Magic Number"
date:   2021-03-31 12:00:01 +0100
categories: refactoring
permalink: /:year/:title
---
## Code Smell of the year

![Magic number](../images/Refactoring/Refactor-magic-number.png)

<br>

When you change your perspective on the screen from the development to the refactoring view, 
it often happens that various numbers appear.
<br>

Numbers that change become variables. Numbers are okay, as long as they aren't 
changed they should be converted to constants.
<br>

Well, numbers are often referred to as "magic numbers".
If you are reading code, it is not really clear why is there a (magic) number like 10 or else.

Let's take a look at following code snippet:
<br>

    public class Vehicle {

        void automaticTransmission(int rpm){
            if(rpm > 4000){
                changeGearUp();
            }
        }
    
        ...
    }

<br>

4000 is speculatively.
Change it to a constant in the code and make it more readable.
<br>

    public class Vehicle {

        private final int MAXIMUM_RPM = 4000; 

        void automaticTransmission(int rpm){
            if(rpm > MAXIMUM_RPM){
                changeGearUp();
            }
        }
        ...
    }

<br>

This is step one of the first part of the Refactoring kickstart beginner series. Here is [step 2](https://redseacomputing.github.io/2021/Refactoring1-2-comment).