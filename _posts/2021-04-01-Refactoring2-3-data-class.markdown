---
layout: post
title:  "Refactoring for kickstarters- Data Class"
date:   2021-04-04 12:00:03 +0100
categories: refactoring
permalink: /:year/:title
---

## Code Smell of the year


![Data class](../images/Refactoring/Refactor-data-class.png)
<br>
 
The next code smell in your code could be on data classes. 
Data classes have fields with getters and setters, but no behaviour.
<br>

One of the goals of object oriented design is to put the behaviour where the data is.
That low couples your components and supports ["Tell, don't ask"](http://principles-wiki.net/principles:information_expert).

So put methods that act on fields in the same class that contain those fields.


    public class CustomerSummaryView {
        private Customer customer;
    
        public CustomerSummaryView(Customer customer){
            this.customer = customer;
        }
    
        public String getCustomerSummary(){
            Address address = customer.getAddress();
            return customer.getTitle() + " " + customer.getFirstName() + " " + customer.getLastName() + ", " + 
                    address.getCity() + ", " + address.getPostcode() + ", " + address.getCountry();
        }
    }


    public class Customer {
    
        private String title;
        private String firstName;
        private String lastName;
        private Address address;
    
        //getters and setters    
    }



    public class Address {
        
        private String city;
        private String postcode;
        private String country;
    
        //getters and setters
    
    }

<br>

You can fork it [here](https://github.com/redseacomputing/Refactoring_DataClass) from Github.

>Hint: Pay attention to possible refactoring steps in your test suite

This is step three of the second part of the Refactoring kickstart beginner series. Here is [step 4](https://redseacomputing.github.io/2021/Refactoring2-4-divergent-change).