---
tags: [Balances]
---

# Balance FAQs

## How does balances differ from valuations?

Valuations provide a history of the value of a portfolio whereas balances provides an indicative value of a portfolio currently, based on the previous day's closing prices for securities and FX rates.

Valuations are dated, and only transactions with a timestamp on or before a valuation's date will be reflected in the valuation.

Balances are not dated and are continuously updated; therefore, they will reflect any transactions booked to the portfolio as they occur.

### Example

```mermaid
gantt
dateFormat YYYY-MM-DD HH:mm
axisFormat %m-%d %H:%M
title Dated valuations
todayMarker off

    section Valuation
    Valuation 2024-02-19 0GBP :active, val1, 2024-02-19 17:00, 62h
    Deposit 100GBP :milestone, deposit, 2024-02-20 02:00, 0h
    Valuation 2024-02-20 calculated :milestone, calc1, 2024-02-20 06:00, 0h
    Valuation 2024-02-20 100GBP :active, val1, 2024-02-20 06:00, 49h
    Bonus awarded 10GBP :milestone, bon, 2024-02-20 12:00, 0h
    Valuation 2024-02-21 calculated :milestone, calc2, 2024-02-21 06:00, 0h
    Valuation 2024-02-21 110GBP :active, val2, 2024-02-21 06:00, 25h
```

<!-- theme: info -->
> Valuations will be recalculated when transactions are booked to a portfolio which already has a valuation for the date of the transaction - 1.


```mermaid
gantt
dateFormat  YYYY-MM-DD HH:mm
axisFormat %m-%d %H:%M
title Ongoing balance
todayMarker off

    section Balance
    Cash Balance 0GBP :active, bal1, 2024-02-19 17:00, 9h
    Deposit 100GBP :milestone, deposit, 2024-02-20 02:00, 0h
    Cash Balance 100GBP :active, val1, 2024-02-20 02:00, 10h
    Bonus awarded 10GBP :milestone, bon, 2024-02-20 12:00, 0h
    Cash Balance 110GBP :active, val1, 2024-02-20 12:00, 44h
```

The cash balance is continuously updated so shows the deposit immediately. The bonus behaves the same way, so the balance is updated immediately, making the full amount available for withdrawal or trading.

## Why are cash and holdings balances not returned with total balance?

This is to avoid large responses from portfolios that hold many positions.

## Why is the value/price/rate `null` in a portfolio's balance?

In rare circumstances we maybe unable to retrieve a latest price of a security or FX rate of a currency. In which case we will be unable to calculate the current value of the holding balance or cash balance, and therefore unable to calculate the value of the portfolio.
