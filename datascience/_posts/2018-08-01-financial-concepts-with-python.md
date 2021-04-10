---

title:  "Financial Concepts with Python"
date:   2018-08-01
tags: [finance, python]

author_profile: true
classes: wide
excerpt: "Notes from the DataCamp course"
mathjax: true

published: false

---

Summer classes are over, which means now I have time to organize my grad school notes for shareability
and posterity. This will be the first of several posts about various topics I learned from fall 2017 
through summer 2018. The first topic involves financial analysis with Python as part of the DataCamp course 
used as a soft introduction to Python. 

## Table of Contents:
1. [The Time Value of Money](#the-time-value-of-money)
2. [Compound Interest](#compound-interest)
3. [Discounting and Projecting Cash Flows]()
4. [Making Rational Economic Decisions]()
5. [Mortgage Structures]()
6. [Interest and Equity]()
7. [The Cost of Capital]()
8. [Wealth Accumulation]()


## The Time Value of Money

### Calculating Return on Investment (% Gain)

Return on investment is the ratio between the net profit and initial cost of investment. Mathematically: 

$$Return(\% Gain) = \large \frac{v_2 - v_1}{v_1}$$

where 

$$v_1$$: initial value of the investment at time

$$v_2$$: final value of the investment at time

The cumulative returns from investing $100 in an asset that grows at 5% per year, over a 2 year period can be calculated in Python as: 

{% highlight python %}

future_value = 100 * (1 + 0.06)**30
print("Future Value of Investment: " + str(round(future_value, 2)))

# Future Value of Investment: 574.35

{% endhighlight %}

### Cumulative Growth

This metric tracks the value of an investment that consistently experiences growth or depreciation. 

$$Investment = \large {v_0 * (1 + r)^{t}}$$

where

$$r$$: The investment’s expected rate of return (growth rate)

$$t$$: The lifespan of the investment (time) 

$$v_0$$: The initial value of the investment at time 0

If the growth rate r is negative, the investment’s value will depreciate (shrink) over time. 
Example: Investing $100 in an asset that grows at 5% per year, over a 2 year period can be calculated as: 

\[ 100 * (1 + 0.05)^2 = 110.25 \]

## Compound Interest

Both time and the rate of return are important variables when forecasting the future value of an investment. Specifically, the number of compounding intervals has the most influence regarding interest accumulation. 

>“Compound interest is the 8th wonder of the world” – Albert Einstein

{% highlight python %}

# Predefined variables
initial_investment = 100
growth_periods = 30
growth_rate = 0.06

# investment compounded once per year
compound_periods_1 = 1
investment_1 = initial_investment * (1+ (growth_rate / 
compound_periods_1))**(growth_periods*compound_periods_1)

print("Investment 1: " + str(round(investment_1, 2)))
# $574.35

# Investment 2 compounded quarterly: $596.93

# Investment 3 compounded monthly: $602.26
{% endhighlight %}














