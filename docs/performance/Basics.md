---
tags: [Performance]
---

# Performance basics

There are many different methods to calculate performance. We offer an API for one such method, Time Weight Rate of Return (TWRR), as the effect of cash flow can be filtered out. We calculate two figures using this methodology, one gross figure and one net of fees. 

Performance intervals are daily, except for weekends where Saturday to Monday is treated as a single interval.

<!-- theme: warning -->
> If WealthKernel does not know how your fees are accrued, these figures will not be accurate.

# How does our performance calculation work?

For a given day we calculate the rate of return as 

$$ GrossPerf = \frac{EndValue + ExpectedIncome - CashFlow}{PreviousEndValue} $$

or

$$ NetPerf = \frac{EndValue + ExpectedIncome - CashFlow - AccruedFees}{PreviousEndValue} $$

In other words, we take the value at the end of the current period, add on expected income, subtract cashflow, (and accrued fees for the net figure) and divide by the end value at the end of the previous period.

<!-- theme: info -->
> ExpectedIncome here represents dividends which have been declared but not yet paid. This helps smooth out spikes which can be seen in the examples.

# Examples

For illustrative purposes settlement is assumed to be instant.

## Simple

In the most simple example, there are no fees, dividends or cash flow. For a value of £100, measuring the TWRR for an increase in value to £102 the next day gives a value of 0.02 or 2%.

|Day|Value|Performance Gross|Performance Net|
|--------|--------|--------|--------|
|Day n|£0 Valuation|-|-|
|Day n+1|£100 deposited, invested|-|-|
|Day n+2|£102 Holdings|((102+0-0)/100)-1=0.02 or 2%|((102+0-0-0)/100)-1=0.02 or 2%|

There are performance figures day n, as this is only a single interval and there are no performance figures for day n+1 because the denominator (`PreviousEndValue`) would be 0, therefore the first available point performance can be calculated is day n+2.

## Fees

In a more complex example, there could be more components affecting the TWRR. Given a calendar day of fee strategy of 10% for a value of £100, this would come to ~£0.03. 

|Day|Value|Accrued Fees|Performance Gross|Performance Net|
|--------|--------|--------|--------|--------|
|Day n|£0 Valuation|£0.03|-|-|
|Day n+1|£100 deposited, invested|£0.03|-|-|
|Day n+2|£102 Holdings|£0.03|((102+0-0)/100)-1=0.02 or 2%|((102+0-0-0.03)/100)-1=0.0197 or 1.97%|

We only include accrued fees in the net figures, so the gross figure stays the same. The net figure drops slightly due to the fees accrued. 

## Dividends and ExpectedIncome

Due to the nature of the TWRR, dividends are included ahead of time to negate odd figures being produced under certain circumstances, which can also affect aggregated performance.

|Day|Value|ExpectedIncome|Cash flow|Performance Gross
|--------|--------|--------|--------|--------|
|Day n|£0 Valuation|-|-|-|
|Day n+1|£100 deposited, invested|-|-|-|
|Day n+2|£102 Holdings|-|-|0.02 or 2%|
|Day n+3|£3 Holdings|-|-100|0.009803921569 or 0.98%|
|Day n+4|£14 Holdings|-|10|3.66666 or 366%|

If a dividend is paid on day n+4, after a withdrawal of £100 has taken place on day n+3, the performance for that day becomes 3.6666... or 366.66%. This is not a good representation of the performance of the investor's portfolio. This effect will also mean any aggregation of performance suffers from the same problem. For example aggregating the figures across the last 3 days would produce a figure of 3.8066.. or 380.66%.

To counteract this, we instead included the dividend on the record date, and call it `ExpectedIncome`. This is an approximation and may vary slightly compared to the actual payment.

|Day|Value|ExpectedIncome|Cash flow|Performance Gross
|--------|--------|--------|--------|--------|
|Day n|£0 Valuation|-|-|-|
|Day n+1|£100 deposited, invested|-|-|-|
|Day n+2|£102 Holdings|-|10|0.12 or 12%|
|Day n+3|£3 Holdings|-|-100|0.009803921569 or 0.98%|
|Day n+4|£14 Holdings|-|0|0.333 or 33.33%|

The figures now show a 12% increase from £100 to £112 on day n+2, and an increase in the value of the holdings on day n+4 more accurately (a 33% increase from £3 to £4). 