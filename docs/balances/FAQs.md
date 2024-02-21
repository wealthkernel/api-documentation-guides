---
tags: [Balances]
---

# Balance FAQs

## How does balances differ from valuations?

Valuations provide a history of the value of a portfolio whereas balances provides an indicative value of a portfolio currently, based on the previous day's closing prices for securities and FX rates.

A given day's valuation is created at the approximately same time every day, and would not be updated with transactions that are created after that time. The next day's valuation would include those transactions. The balance is continuously updated with ongoing transactions as they happen, and will therefore reflect any actions taken on the portfolio, such as deposits, orders, or bonuses.

Example: 100GBP deposit occurs before the valuation for 2024-02-20 is calculated. When the valuation is calculated, the cash portion will reflect that:

```json
"date": "2024-02-20",
...
"cash": [
    {
        "currency": "GBP",
        "value": {
            "currency": "GBP",
            "amount": 100
        },
    ...
    }
],
...
```

The cash balance is continuously updated so also reflects that.

```json
...
"amount": 100,
"value": {
    "currency": "GBP",
    "amount": 100
},
...
```

A bonus of 10GBP is paid to the investor later the same day.

The valuation for 2024-02-20 does not change. The balance is updated immediately, making the full amount available for withdrawal or trading.

```json
...
"amount": 110,
"value": {
    "currency": "GBP",
    "amount": 110
},
...
```

When the valuation is calculated for 2024-02-21, the transaction is reflected, so the amount will be 110GBP.

## Why are cash and holdings balances not returned with total balance?

This is to avoid large responses from portfolios that hold many positions.

## Why is the value/price/rate `null` in a portfolio's balance?

In rare circumstances we maybe unable to retrieve a latest price of a security or FX rate of a currency. In which case we will be unable to calculate the current value of the holding balance or cash balance, and therefore unable to calculate the value of the portfolio.
