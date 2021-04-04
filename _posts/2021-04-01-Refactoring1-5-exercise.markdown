---
layout: post 
title:  "Refactor kickstarter series- Repetition"
date:   2021-03-31 12:00:05 +0100 
categories: refactoring 
permalink: /:year/:title
---

![Summary part 1](../images/Refactoring/Refactor-exercise-part-one.png)

Pay attention to the `debit(float amount)` function in following code snippet. Feel free to copy and paste it in your editor of choice or fork it directly 
from [Github](https://github.com/redseacomputing/Refactoring_Comment).

    public class Account{
    
            private float balance = 0;
            private List<Transaction> transactions = new ArrayList<>();
            private String lastDebitDate;
    
            public void credit(float amount) {
                balance += amount;
            }
    
            public void debit (float amount){
    
                //check amount does not exceed max allowed
                if(amount > 1000){
                    throw new IllegalArgumentException("Maximum debit amount exceeded");
                }
    
                // deduct amount from balance
                balance -= amount;
    
                // record transaction
                transactions.add(new Transaction(true, amount));
    
                //update last debit date
                Calendar calendar = Calendar.getInstance();
    
                lastDebitDate = calendar.get(Calendar.DATE) + "/" + calendar.get(Calendar.MONTH) + "/" + calendar.get(Calendar.YEAR);
            }
    
        public float getBalance() {
            return balance;
        }
    
        public Transaction getLastTransaction(){
                return (Transaction)transactions.get(transactions.size() - 1);
            }
    
            public String getLastDebitDate(){
                return lastDebitDate;
            }

    }


    class AccountTest {

        Account account;
    
        @BeforeEach
        void setUp() {
            account = new Account();
        }
    
        @Test
        void debit100ShouldMakeAnSaldoOf100() {
            account.debit(100);
            assertEquals(-100d, account.getBalance(), 0.01);
        }
    
        @Test
        void debit100AndCredit100ShouldReturnZero() {
            Account account = new Account();
            account.debit(100);
            account.credit(100);
            assertEquals(0, account.getBalance(), 0.01);
        }
    
        @Test
        void debitGreaterThan1000ShouldThrowAnIllegalArgumentException() {
            Account account = new Account();
            assertThrows(IllegalArgumentException.class, ()-> {
                    account.debit(1001);
            });
        }
    
        @Test
        void credits1000TimesWithValue1ShouldReturn1000() {
            Account account = new Account();
            for (int i = 0; i < 1000; i++) {
                account.credit(1);
            }
            assertEquals(1000d, account.getBalance());
        }
    
        @Test
        void transactionShouldBeStoredInCollection() {
            Account account = new Account();
            for (int i = 0; i < 1000; i++) {
                account.debit(100);
            }
            assertNotNull( account.getLastTransaction());
        }
    
        @Test
        void lastDebitDateShouldNotBeNull() {
            account.debit(10);
            assertNotNull(account.getLastDebitDate() );
        }
    }

This was part one of the Refactoring kickstart beginner series. Here
is [part 2](https://redseacomputing.github.io/2021/Refactoring2-0-introduction).