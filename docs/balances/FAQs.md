---
tags: [Balances]
---

# Balance FAQs

## How does balances differ from valuations?

Valuations provide a history of the value of a portfolio whereas balances provides an indicative value of a portfolio currently, based on the previous day's closing prices for securities and FX rates.

Valuations are created at approximately the same time every day, for the previous day. Transactions booked with a date of t are only reflected in the valuation for t+1.

The balance is not dated, and is continuously updated, and will therefore reflect any actions taken on the portfolio, such as deposits, orders, or bonuses, as they happen.

### Example

```mermaid
gantt
dateFormat  YYYY-MM-DD HH:mm
axisFormat %m-%d %H:%M
title Dated valuations
todayMarker off

    section Valuation
    Latest Valuation 0GBP :active, val1, 2024-02-19 18:00, 12h
    Deposit 100GBP :milestone, deposit, 2024-02-20, 6h
    Valuation 2024-02-20 calculated :milestone, calc1, after deposit,
    Latest Valuation 100GBP :active, val1, 2024-02-20 06:00, 1d
    Bonus awarded 10GBP :milestone, bon, 2024-02-20, 24h
    Valuation 2024-02-21 calculated :milestone, calc2, 2024-02-21, 12h
    Latest Valuation 110GBP :active, val2, 2024-02-21 06:00, 1d
```

<!-- theme: info -->
> Valuations can be recalculated when transactions are booked to a portfolio which already has a valuation for the date of the transaction - 1.


```mermaid
gantt
dateFormat  YYYY-MM-DD HH:mm
axisFormat %m-%d %H:%M
title Ongoing balance
todayMarker off

    section Balance
    Cash Balance 0GBP :active, bal1, 2024-02-19 18:00, 9h
    Deposit 100GBP :milestone, deposit, 2024-02-20, 6h
    Cash Balance 100GBP :active, val1, after bal1, 9h
    Bonus awarded 10GBP :milestone, bon, 2024-02-20, 24h
    Cash Balance 110GBP :active, val1, 2024-02-20 12:00, 44h
```

The cash balance is continuously updated so also the deposit immediately. The bonus behaves the same way, so the balance is updated immediately, making the full amount available for withdrawal or trading.

## Why are cash and holdings balances not returned with total balance?

This is to avoid large responses from portfolios that hold many positions.

## Why is the value/price/rate `null` in a portfolio's balance?

In rare circumstances we maybe unable to retrieve a latest price of a security or FX rate of a currency. In which case we will be unable to calculate the current value of the holding balance or cash balance, and therefore unable to calculate the value of the portfolio.
