---
tags: [Balances]
---

# Balance Basics

<!-- theme: info -->
> This API is currently in **Beta** and is subject to change.

This API provides a set of endpoints to get the current balances of a portfolio based on latest prices and FX rates.
The security value is based on prices from close of business the previous day and cash value is current day.

## Total Balance

This object contains the current total value of a portfolio in its base currency.

The `value` is calculated as the sum of a portfolios cash and holding values.

<!-- theme: warning -->
> The `value` element of this object could be `null` in the absence of any latest price or FX rate of holdings or cash that make up the portfolio.

## Cash Balance

This object contains the current amount of cash of a currency held by a portfolio and the value of that cash in the portfolio's base currency.

The `value` is calculated using the following equation: `amount / rate` 

<!-- theme: warning -->
> The `value` element of this object could be `null` in the absence of a latest FX rate.

## Holding Balance

This object contains the current quantity of a security held by a portfolio and the value of that holding in the portfolio's base currency.

The `value` is calculated using the following equation: `quantity * price / rate` 

<!-- theme: warning -->
> The `value` element of this object could be `null` in the absence of a latest price or FX rate.

## Additional Information

If securities are being purchased the balances API will be updated when the orders are matched to the portfolio, it is not determined on the orders being settled.

If securities are being sold the balances API will follow the same logic . This enables the cash to be reinvested prior to settlement. However, if the cash is wished to be withdrawn the orders must be settled.
