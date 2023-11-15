---
tags: [Balances]
---

# Balance basics

This API provides a set of endpoints to get the current balances of a portfolio based on latest prices and FX rates.

## Total balance

This object contains the current total value of a portfolio in its base currency.

The `value` is calculated as the sum of a portfolios cash and holding values.

<!-- theme: warning -->
> The `value` element of this object could be `null` in the absence of any latest price or FX rate of holdings or cash that make up the portfolio.

## Cash balance

This object contains the current amount of cash of a currency held by a portfolio and the value of that cash in the portfolio's base currency.

The `value` is calculated using the following equation: `amount / rate` 

<!-- theme: warning -->
> The `value` element of this object could be `null` in the absence of a latest FX rate.

## Holding balance

This object contains the current quantity of a security held by a portfolio and the value of that holding in the portfolio's base currency.

The `value` is calculated using the following equation: `quantity * price / rate` 

<!-- theme: warning -->
> The `value` element of this object could be `null` in the absence of a latest price or FX rate.
