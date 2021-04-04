---
layout: post
title:  "Refactoring for kickstarters- Long Parameter List"
date:   2021-03-31 12:00:04 +0100
categories: refactoring
permalink: /:year/:title
---

## Code Smell of the year
<br>

![Long parameter list](../images/Refactoring/Refactor-long-parameter-list.png)

<br>

Too many parameters are difficult to read. 3 or 4 parameters should be the maximum.
Parameters tend to become more and they can be cohesive, too. 

This list of parameters are on your hitlist now.
Keep an eye on them.

<br>

    private String buildCustomerSummary(String customerFirstName, String customerLastName,String customerTitle, Address address){
        return customerTitle + " " + customerFirstName + " " + " " customerLastname + " " + address.getCity() + " " +
                address.getPostCode() + " " + address.getCountry();
    }
<br>

Create an object from the parameters and use it to pass it to the function.


This is step four of the first part of the Refactoring kickstart beginner series. Here is [the last step of part 1](https://redseacomputing.github.io/2021/Refactoring1-5-exercise).