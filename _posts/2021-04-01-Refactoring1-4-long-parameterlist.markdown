---
layout: post
title:  "Code Smell Of The Year- Long parameter list"
date:   2021-03-31 12:00:04 +0100
categories: refactoring
permalink: /:year/:title
---

![Long parameter list](../images/Refactoring/Refactor-long-parameter-list.png)

Too many parameters are difficult to read. 3 or 4 parameters should be the maximum.
Parameters tend to become more and are to cohesive,too. This list of parameters are on your hitlist now.
Keep an eye on them.

    private String buildCustomerSummary(String customerFirstName, String customerLastName,String customerTitle, Address address){
        return customerTitle + " " + customerFirstName + " " + " " customerLastname + " " + address.getCity() + " " +
                address.getPostCode() + " " + address.getCountry();
    }

Create an object from the parameters and use it to pass it to the function.

This is step four of the first part of the Refactoring kickstart beginner series. Here is [the last step of part 1](https://redseacomputing.github.io/2021/Refactoring1-5-exercise).