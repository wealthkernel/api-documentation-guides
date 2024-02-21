---
tags: [Balances]
---

# Balance FAQs

## How does balances differ from valuations?

Valuations provide a history of the value of a portfolio whereas balances provides an indicative value of a portfolio currently, based on the previous day's closing prices for securities and FX rates.

Valuations are created at approximately the same time every day, for the previous day. The valuation would not be updated with transactions that have a date after the previous day. The next day's valuation would include those transactions. For example a valuation for 2024-02-20 would be generated on 2024-02-21. On the date 2024-02-21, there is no valuation for 2024-02-21. Transactions dated 2024-02-21 would therefore not be reflected in any valuation, until one is generated on 2024-02-22. 

The balance is not dated, and is continuously updated, and will therefore reflect any actions taken on the portfolio, such as deposits, orders, or bonuses, as they happen.

Example: 100GBP deposit occurs before the valuation for 2024-02-20 is calculated. When the valuation is calculated, the cash portion will reflect the deposit:

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

<!-- theme: info -->
> Valuations can be recalculated when transactions are booked to a portfolio which already has a valuation for the date of the transaction.

The cash balance is continuously updated so also reflects the deposit.

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

The valuation for 2024-02-20 does not change, and will show a value of 100GBP. The balance is updated immediately, making the full amount available for withdrawal or trading.

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
