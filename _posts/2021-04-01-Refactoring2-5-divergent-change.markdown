---
layout: post
title:  "Refactoring for kickstarters- Divergent Change"
date:   2021-04-04 12:00:05 +0100
categories: refactoring
permalink: /:year/:title
---

## Code Smell of the year
<br>

![Divergent Change](../images/Refactoring/Refactor-divergent-change.png)


It is not ideal to have a delegate method on the account class.
Split it completely, that the account class has no knowledge at all of the xml serialization as a result.

    
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

You can fork it [here](https://github.com/redseacomputing/Refactoring_DivergentChange2) from Github.

This is step five of the second part of the Refactoring kickstart beginner series. Here is [step 6](https://redseacomputing.github.io/2021/Refactoring2-6-lazy-class).