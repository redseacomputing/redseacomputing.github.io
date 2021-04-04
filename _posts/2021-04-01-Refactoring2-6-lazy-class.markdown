---
layout: post
title:  "Refactoring for kickstarters- Lazy Class"
date:   2021-04-04 12:00:06 +0100
categories: refactoring
permalink: /:year/:title
---

## Code Smell of the year
<br>

![Lazy Class](../images/Refactoring/Refactor-lazy-class.png)

<br>

Lazy classes are just classes that arent doing enough to justify their existence
(in terms of the maintenance overhead).

At the example, we've got an address class and instead of having a postcode field, there's
a postcode object, which is defined by the other class that has very little in it
and very little behavior to work out the postcode area.

Solution:
To refactor this, you are going to essentially move the fields and methods of postcode into
the address class (Inline the postcode class into its container which is address).

    public class AddressTests{

        public void postageUKIsThreePounds throws Exception(){
            assertEquals(3, createAddress("United Kingdom").calculatePostage(), 0);
        }

        @Test
        public void postageOutsideUKIsSixPounds() throws Exception {
            assertEquals(6, createAddress("Narnia").calculatePostage(), 0);    
        }

        @Test
        public void addressSummaryShouldBeHouseStreetCityPostcodeCountrySeparatedByCommaSpace() throws Exception {
            Address address = createAddress("United Kingdom");
            assertEquals("1, High Street, Faketown, N1 2JP, United Kingdom", address.getAddressSummary());
        }

        @Test
        public void postcodeAreaIsFirstStringBeforeSpace() throws Exception {
            Postcode postcode = new Postcode(N1 2JP");
            assertEquals("N1", postcode.getPostcodeArea());
        }

        private Address createAddress(String country) {
            return new Address("1", "High Street", "Faketown", country, new Postcode("N1 2JP"));
        }
    }


    
    public class Address {
    
        private final String house;
        private final String street;
        private final String city;
        private final Postcode postcode;
        private final String country;
    
        public Address (String house, String street, String city,
                        String country, Postcode postcode){
            this.house = house;
            this.street = street;
            this.city = city;
            this.postcode = postcode;
            this.country = country;
        }

        public double calculatePostage(){
            return country == "United Kingdom" ? 3 : 6;
        }

        public String getAddressSummary(){
            return house + ", " + street + ", " + city + ", " + postcode.getPostcode() +
                    ", " + country;
        }

    }


    public class Postcode {
        private final String postcode;
    
        public Postcode(String postcode){
            this.postcode = postcode;
        }
    
        public String getPostcode(){
            return postcode;
        }
    
        public String getPostcodeArea(){
            return postcode.split(" ")[0];
        }
    }

<br>

You can fork it [here](https://github.com/redseacomputing/Refactoring_LazyClass1) from Github.

This is step six of the second part of the Refactoring kickstart beginner series. Here is [step 7](https://redseacomputing.github.io/2021/Refactoring2-7-lazy-class).