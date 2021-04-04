---
layout: post
title:  "Refactoring for kickstarters- Switch Statement"
date:   2021-04-04 12:00:09 +0100
categories: refactoring
permalink: /:year/:title
---

## Code Smell of the year
<br>

![Switch statement](../images/Refactoring/Refactor-switch-statement.png)
<br>

Switch statements are dependency magnets. Eliminate them with a polymorphic solution.

<br>

    public class InsuranceQuote {
    
        private final Motorist motorist;
    
        public InsuranceQuote(Motorist motorist) {
            this.motorist = motorist;
        }
    
        public RiskFactor calculateMotoristRisk() {
            if (motorist.getInsurancePoints() > 3 || motorist.getAge() < 25) {
                return RiskFactor.HIGH_RISK;
            }
    
            if (motorist.getInsurancePoints() > 0) {
                return RiskFactor.MODERATE_RISK;
            }
    
            return RiskFactor.LOW_RISK;
        }
    
        public double calculateInsurancePremium(double insuranceValue) {
            RiskFactor riskFactor = calculateMotoristRisk();
    
            switch (riskFactor) {
                case LOW_RISK:
                    return insuranceValue * 0.02;
                case MODERATE_RISK:
                    return insuranceValue * 0.04;
                default:
                    return insuranceValue * 0.06;
            }
        }
    }

<br>

You can fork it [here](https://github.com/redseacomputing/Refactoring_SwitchStatement) from Github.

This is step nine of the second part of the Refactoring kickstart beginner series. Here is the [summary](https://redseacomputing.github.io/2021/Refactoring2-10-summary).