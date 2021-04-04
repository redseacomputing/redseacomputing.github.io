---
layout: post
title:  "Refactoring for kickstarters- Message Chain 1"
date:   2021-04-04 12:00:01 +0100
categories: refactoring
permalink: /:year/:title
---

## Code Smell of the year

![Message Chain](../images/Refactoring/Refactor-message-chain.png)
<br>

Message Chains violates the [law of demeter](https://en.wikipedia.org/wiki/Law_of_Demeter).
They increase the dependencies through the system.

<br>


    class InvoiceTest {
    
        Invoice invoice;
    
        @BeforeEach
        void setUpInvoiceWithShippingCosts() {
            invoice = new Invoice(new Customer(new Address(new Country())));
        }
    
        @Test
        void ShouldReturnPriceOfOneItemWithShippingCost() {
            InvoiceItem item = new InvoiceItem(100);
            invoice.addItem(item);
            assertEquals(110, invoice.getTotalPrice());
        }
    
        @Test
        void ShouldReturnPriceOfTwoItemWithShippingCost() {
            InvoiceItem item = new InvoiceItem(100);
            invoice.addItem(item);
            invoice.addItem(item);
            assertEquals(210, invoice.getTotalPrice());
        }

    
    }


    public class Invoice {

        static final double SHIPPING_COST_OUTSIDE_EU = 10;
        private List<InvoiceItem> invoiceItems = new ArrayList<InvoiceItem>();
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

            if(!customer.getAddress().getCountry().isInEurope()){
                invoiceTotal += SHIPPING_COST_OUTSIDE_EU;
            }
            return invoiceTotal;
        }
    }


<br>

>Hint: Objects should only interact with their nearest neighbours

<br>


You can fork it [here](https://github.com/redseacomputing/Refactoring_MessageChain1) from Github.

This is step one of the second part of the Refactoring kickstart beginner series. Here is [step 2](https://redseacomputing.github.io/2021/Refactoring2-2-message-chain).