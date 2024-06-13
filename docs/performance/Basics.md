---
tags: [Performance]
---

# Performance basics

WealthKernel calculates performance using the Time-Weighted Rate of Return (TWRR) methodology, as this provides a better view of performance for investors by filtering out the effect of cash flow. We calculate two figures using this methodology: a gross figure and a net-of-fees figure.

Performance intervals are daily, except for weekends where Saturday to Monday is treated as a single interval.

<!-- theme: warning -->
> If WealthKernel does not know how your fees are accrued, then we will be unable to calculate an accurate net performance figure.

# How does our performance calculation work?

For a given day we calculate the rate of return as 

<!--TODO: Could make this mermaid diagram when stoplight supports mermaid v10.9.0 https://mermaid.js.org/config/math.html -->

![grossperf-3.png](../../assets/images/grossperf-3.png)

or

![netperf-3.png](../../assets/images/netperf-3.png)

We take the value at the end of the current interval, add the expected income, subtract the cashflow, for the net figure any accrued fees are also subtracted. We then divide this by the end value from the end of the previous interval.

<!-- theme: info -->
> ExpectedIncome here represents dividends which have been declared but not yet paid. This helps smooth out spikes which can be seen in the examples.

# Examples

For illustrative purposes, assume a £100 deposit, and assets settle on T+1.

## Simple

In the most simple example, there are no fees, dividends or cash flow. For a value of £100, measuring the TWRR for an increase in value to £102 the next day gives a value of 0.02 or 2%.

|Day|StartValue|EndValue|Performance Gross|Performance Net|
|--------|--------|--------|--------|--------|
|Day n|£0|£100|-|-|
|Day n+1|£100|£100|((100 + 0 - 0 ) / 100) - 1 = 0 or 0%|((100 + 0 - 0 - 0) / 100) - 1 = 0 or 0%|
|Day n+2|£100|£102|((102 + 0 - 0 ) / 100) - 1 = 0.02 or 2%|((102 + 0 - 0 - 0) / 100) - 1 = 0.02 or 2%|

There are no performance figures on day n, as this is only a single interval, so the first available point performance can be calculated is day n+1.

## Fees

In a more complex example, there could be more components affecting the TWRR. Given a calendar day fee strategy of 10% for a value of £100, a single day's fees would come to ~£0.03.

|Day|StartValue|EndValue|Accrued Fees|Performance Gross|Performance Net|
|--------|--------|--------|--------|--------|--------|
|Day n|£0|£100|£0.00|-|-|
|Day n+1|£100|£100|£0.02737|((100 + 0 - 0) / 100) - 1 = 0 or 0%|((100 + 0 - 0 - 0.02737) / 100) - 1 = -0.0002737 or -0.02737%|
|Day n+2|£102|£102 holdings|£0.02792|((102 + 0 - 0) / 100) - 1 = 0.02 or 2%|((102 + 0 - 0 - 0.02737) / 100) - 1 = 0.0197 or 1.97%|

We only include accrued fees in the net figures, so the gross figure is the same as before. The net figure is slightly less, reflecting the fees accrued.

## Dividends and ExpectedIncome

Dividends are included ahead of time due to the nature of the Time-Weighted Rate of Return (TWRR) combined with the fact that dividends typically cause a drop in stock price. This negates the possibility of odd figures being produced under certain circumstances that could also affect aggregated performance. For instance, if we were to include dividends in performance on the day they are paid, it would look like this:

|Day|StartValue|EndValue|Cash flow|Performance Gross|
|--------|--------|--------|--------|--------|
|Day n|£0|£100|-|-|
|Day n+1|£100|£100|-|((100 + 0 - 0) / 100) - 1 = 0 or 0%|
|Day n+2|£100|£90|-|((90 - 0) / 100) - 1 = -0.1 or -10%|
|Day n+3|£90|£90|-|((90 - 0) / 90) - 1 = 0 or 0%|
|Day n+4|£90|£100|-|(100 - 0 / 90) - 1 = 0.1111 or 11.11%|

On day n+2, the value of the security invested in has dropped due to the dividend. This comes out looking like negative performance, but in reality the investor is guaranteed a dividend of how much the security has dropped by. Similarly, on day n+4 when the dividend is paid, what looks like great performance is calculated, when in fact this is just the dividend returning value to the investor.

If we instead use ExpectedIncome, we get these figures:

|Day|StartValue|EndValue|Cash flow|Performance Gross|
|--------|--------|--------|--------|--------|
|Day n|£0|£100|-|-|
|Day n+1|£100|£100|-|((100 + 0 - 0) / 100) - 1 = 0 or 0%|
|Day n+2|£100|£90|-|((90 + 10 - 0) / 100) - 1 = 0 or 0%|
|Day n+3|£90|£90|-|((90 - 0) / 90) - 1 = 0 or 0%|
|Day n+4|£90|£100|-|(100 - 0 - 10 / 90) - 1 = 0 or 0%|

As the drop in price is accounted for by the dividend represented by `ExpectedIncome` on the record date, and is included in `CashFlow` on the payment date, the figures now show the reality that no actual gain or loss has occurred. We treat the dividend as cash flow on day n+4 as it has already been accounted for as `ExpectedIncome` on day n+2.

<!-- theme:info -->
> `ExpectedIncome` is an approximation and may vary slightly compared to the actual payment.

## Partial Withdrawals

Another scenario that could cause this is that of a partial withdrawal.

|Day|StartValue|EndValue|Cash flow|Performance Gross|
|--------|--------|--------|--------|--------|
|Day n|£0|£100|-|-|
|Day n+1|£100|£100|-|((100 + 0 - 0) / 100) - 1 = 0 or 0%|
|Day n+2|£100|£90|-|((90 - 0) / 100) - 1 = -0.1 or -10%|
|Day n+3|£90|£10|-80|((10 - (- 80)) / 90) - 1 = 0 or 0%|
|Day n+4|£10|£20|-|(20 / 10) - 1 = 1 or 100%|

If a dividend is paid on day n+4, after a withdrawal of £80 has taken place on day n+3, the performance for that day becomes 1 or 100%. This is not a good representation of the performance of the investor's portfolio. This effect will also mean any aggregation of performance suffers from the same problem. For example aggregating the figures across the last 3 days would produce a figure of 0.8 or 80%.

Again, to counteract this, we instead include the dividend on the record date, as `ExpectedIncome`.

|Day|StartValue|EndValue|ExpectedIncome|Cash flow|Performance Gross
|--------|--------|--------|--------|--------|--------|
|Day n|£0|£100|-|-|-|
|Day n+1|£100|£100|-|-|((100 + 0 - 0) / 100) - 1 = 0 or 0%|
|Day n+2|£100|£90|10|-|((90 + 10 - 0) / 100) - 1 = 0.0 or 0%|
|Day n+3|£90|£10|-|-80|(10 + 0 - (- 80)) / 90 = 0 or 0%|
|Day n+4|£10|£20|-|10|((20 + 0 - 10) / 10) - 1 = 0 or 0%|

The figures now accurately show that no actual gain or loss has been made.