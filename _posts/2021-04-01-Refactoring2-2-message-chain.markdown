---
layout: post
title:  "Refactoring for kickstarters- Message Chain"
date:   2021-04-04 12:00:02 +0100
categories: refactoring
permalink: /:year/:title
---

## Code Smell of the year

![Message Chain](../images/Refactoring/Refactor-message-chain.png)
<br>

Here is a hidden message chain in this code. But technically it's the same as before.
Eliminate it.
<br>

    public class Invoice {
        private 
        private Customer customer;
    
        public Invoice(Customer customer){
            this.customer = customer;
        }
    
        public void addItem(InvoiceItem invoiceItem){
            invoiceItems.add(invoiceItem);
        }

        public double getTotalPrice(){ 
            double invoiceTotal = 0;

            for (Iterator iterator = invoiceItems.iterator(); iterator.hasNext();) {
                InvoiceItem invoiceItem = (InvoiceItem) iterator.next();
                invoiceTotal += invoiceItem.getSubTotal();
            }

            Address address = customer.getAddress();
            Country country = address.getCountry();

            if(!country.isInEurope()){
                invoiceTotal += SHIPPING_COST_OUTSIDE_EU;
            }
            return invoiceTotal;
        }
    }   

<br>

You can fork it [here](https://github.com/redseacomputing/Refactoring_MessageChain2) from Github.

This is step two of the second part of the Refactoring kickstart beginner series. Here is [step 3](https://redseacomputing.github.io/2021/Refactoring2-3-data-class).