---
layout: post
title:  "Refactoring for kickstarters- Divergent Change 1"
date:   2021-04-04 12:00:04 +0100
categories: refactoring
permalink: /:year/:title
---

## Code Smell of the year

![Divergent change](../images/Refactoring/Refactor-divergent-change.png)
<br>
 
The divergent change code smell comes into play when classes have more than 
one reason to change.

This is a violation of the [Single Responsibility Principle](https://en.wikipedia.org/wiki/Single-responsibility_principle) of the next abstraction level.

This example has a class which handles operations on a bank account(credit, debit,..),
but it also has a method for serializing the data to XML string format.

If the format would be changed, you have edit it in your account class.

Extract such behaviour to an own class and delegate to it.

    
    public class Account{
    
        private int accountNumber;
        private double balance = 0;
    
        public Account (int accountNumber){
            this.accountNumber = accountNumber;
        }

        public int getAccountNumber(){}
        public double getBalance(){}
        
        public void credit(double amount) {
            balance += amount;    
        }

        public void debit(double amount) {
            balance -= amount;
        }
        
        public String toXml () {
            return "<account><id>" + Integer.toString(getAccountNumber() + "</id>" +
                    "<balance>" + Double.toString(getBalance()) + "</balance><account>";
        } 

    }


You can fork it [here](https://github.com/redseacomputing/Refactoring_DivergentChange1) from Github.

This is step four of the second part of the Refactoring kickstart beginner series. Here is [step 5](https://redseacomputing.github.io/2021/Refactoring2-5-divergent-change).