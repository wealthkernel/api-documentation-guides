---
tags: [Balances]
---

# Balance Basics

<!-- theme: info -->
> This API is currently in **Beta**.

This API provides a set of endpoints to get the current balances of a portfolio based on latest prices and FX rates.

## Total Balance

This object contains the current total value of a portfolio in its base currency.

<!-- theme: warning -->
> The `value` element of this object could be `null` in the absence of any latest price or FX rate of holdings or cash that make up the portfolio.

## Cash Balance

This object contains the current amount of cash of a currency held by a portfolio and the value of that cash in the portfolio's base currency.

<!-- theme: warning -->
> The `value` element of this object could be `null` in the absence of a latest FX rate.

## Holding Balance

This object contains the current quantity of a security held by a portfolio and the value of that holding in the portfolio's base currency.

<!-- theme: warning -->
> The `value` element of this object could be `null` in the absence of a latest price or FX rate.
