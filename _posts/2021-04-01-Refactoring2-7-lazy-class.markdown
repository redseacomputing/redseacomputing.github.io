---
layout: post
title:  "Refactoring for kickstarters- Lazy Class 2"
date:   2021-04-04 12:00:07 +0100
categories: refactoring
permalink: /:year/:title
---

## Code Smell of the year
 

![Lazy Class](../images/Refactoring/Refactor-lazy-class.png)

<br>

Take care of lazy subclasses too.
    
    public abstract class Address {
    
        private final String house;
        private final String street;
        private final String city;
        private final String postcode;
        private final String country;
    
        public Address (String house, String street, String city,
                        String country, String postcode){
            this.house = house;
            this.street = street;
            this.city = city;
            this.postcode = postcode;
            this.country = country;
        }

        public String getAddressSummary(){
            return house + ", " + street + ", " + city + ", " + postcode.getPostcode() +
                    ", " + country;
        }

    }


    public class ShippingAddress extends Address {
    
        public ShippingAddress(String house, String street, String city, String country, String postcode){
            super(house, street, city, country, postcode);
        }

        public double calculatePostage(){
            return country == "United Kingdom" ? 3 : 6;
        }
    }

<br>

You can fork it [here](https://github.com/redseacomputing/Refactoring_LazyClass2) from Github.

This is step seven of the second part of the Refactoring kickstart beginner series. Here is [step 8](https://redseacomputing.github.io/2021/Refactoring2-8-inappropriate-intimacy).