---
tags: [Balances]
---

# Balance FAQs

## How does balances differ from valuations?

Valuations provide a history of the value of a portfolio whereas balances provide a near realtime current value of a portfolio.

## Why are cash and holdings balances not returned with total balance?

This is to avoid large responses from portfolios that hold many positions.

## Why does this portfolio not have any balances?

Balances are currently lazily created upon initial funding. If the portfolio has no transactions then the portfolio's balances will not exist.

## Why is the value/price/rate `null` in a portfolio's balance?

In rare circumstances we maybe unable to retrieve a latest price of security or FX rate of a currency. In which case we will unable to calculate the current value of the holding balance or cash balance, and therefore unable to calculate the value of the portfolio.

## Are the endpoints consistent across requests?

It is possible for responses from the balances endpoints for a single portfolio to be inconsistent. For example a new price or rate has come in between requests, or a transaction has been booked on the portfolio in between requests. We are currently exploring options to allow the consistency between responses to be verified.
