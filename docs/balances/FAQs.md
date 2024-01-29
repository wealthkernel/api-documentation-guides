---
tags: [Balances]
---

# Balance FAQs

## How does balances differ from valuations?

Valuations provide a history of the value of a portfolio whereas balances provides an indicative value of a portfolio currently, based on last night prices for securities and FX rate.

## Why are cash and holdings balances not returned with total balance?

This is to avoid large responses from portfolios that hold many positions.

## Why is the value/price/rate `null` in a portfolio's balance?

In rare circumstances we maybe unable to retrieve a latest price of a security or FX rate of a currency. In which case we will be unable to calculate the current value of the holding balance or cash balance, and therefore unable to calculate the value of the portfolio.
