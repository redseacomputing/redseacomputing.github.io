---
layout: post
title:  "Refactoring for kickstarters- Inappropriate Intimacy"
date:   2021-04-04 12:00:08 +0100
categories: refactoring
permalink: /:year/:title
---

## Code Smell of the year
<br>

![Inappropriate Intimacy](../images/Refactoring/Refactor-inappropriate-intimacy.png)
<br>

Inappropriate Intimacy is a code smell when two classes know to much about each other.
In this example it is feature envy in a bi-directional relationship.

Move the methods to where they belong and refactor it to a unidirectional association.


    public class License {
        private Motorist motorist;
        private int points = 0;
    
        public void setMotorist(Motorist motorist){
            this.motorist = motorist;
        }

        public int getPoints(){
            return this.points;
        }

        public void addPoints(int points){
            this.points += points;
        }

        public String getSummary(){
            return motorist.getTitle() + " " + motorist.getFirstName() + " " + motorist.getSurname() + ", " + 
            Integer.toString(getPoints()) + " points";
        }
    }



    public class Motorist{

        public final License license;
        private final String surname;

        private final String firstName;
        private final String title;

        public Motorist(License license, String surname, String firstName, String title){
            license.setMotorist(this);
            this.license = license;
            this.surname = surname;
            this.firstName = firstName;
            this.title = title;
        }

        public String getSurname(){
            return this.surname;
        }

        public getFirstName(){
            return this.firstName;
        }

        public getTitle(){
            return this.title;
        }

        public RiskFactor getRiskFactor(){
            if(license.getPoints() > 3)
                return RiskFactor.HIGH_RISK;
            if(license.getPoints() > 0)
                return RiskFactor.MODERATE_RISK;
            return RiskFactor.LOW_RISK;
        }
    }

<br>

You can fork it [here](https://github.com/redseacomputing/Refactoring_InappropriateIntimacy) from Github.

This is step eight of the second part of the Refactoring kickstart beginner series. Here is [step 9](https://redseacomputing.github.io/2021/Refactoring2-9-switch-statement).