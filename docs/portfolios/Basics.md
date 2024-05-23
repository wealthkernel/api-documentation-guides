---
tags: [Portfolios]
---

# Portfolio basics

Portfolios are a container for an investor's cash and holdings. All investment activity on the WealthKernel platform (balances, orders, transactions) is directly tied to a portfolio. When a portfolio is created under an account, it will inherit the same currency as the account. The currency does not need to be stipulated when creating a portfolio, however if it is, there will be a check made against the currency to ensure consistency. 

Multiple portfolios can be created under a single account to allow for different investment strategies. However, we do not recommend mixing and matching mandate types.

The below diagram represents an example account and portfolio structure. 


```mermaid
flowchart TD
    A(Party - Person) --> B(GIA GBP) --> G(Portfolio GBP)
    B(GIA GBP) --> H(Portfolio GBP)
    A(Party - Person) --> C(GIA EUR) --> I(Portfolio EUR)
    A(Party - Person) --> D(GIA USD) --> J(Portfolio USD)
    A(Party - Person) --> E(ISA GBP) --> K(Portfolio GBP)
    A(Party - Person) --> F(SIPP GBP) --> L(Portfolio GBP)
    F(SIPP GBP) --> M(Portfolio GBP)
```
## Portfolio characteristics

The following table provides a summary of how currencies work across different functions. 

| Function | Rules |
|---|---|
| Money in | The currency on the portfolio does not affect which currencies will be allowed into a portfolio. |
| Money out | The currency on the portfolio does not affect which currencies will be allowed out of a portfolio. |
| Valuations | The valuation of a portfolio will be in the currency on the portfolio. |
| Balances | The balance of a portfolio will be in the currency on the portfolio. |
| Dividends | Dividends will be paid into a portfolio in the currency on the portfolio. |
| Settlement | The currency on a portfolio does not affect which currencies can be settled in. |
| Fees | Fees can currently only be taken in GBP from GBP portfolios. |
| Charges | The currency on a portfolio does not affect which currencies can be used for charges. |

## Mandate types

### Execution only mandate

Trades will only be requested when instructed to do so through the orders API.

### Execution only model mandate

Deposits and withdrawals will be invested/disinvested according to the configured model. The portfolio will not be periodically rebalanced to compensate for drift; however, we can establish a rebalance schedule if necessary.

### Discretionary mandate

Deposits and withdrawals will be invested/disinvested according to the configured model. The portfolio will be periodically rebalanced to compensate for drift.

### Single product mandate

Deposits will be invested only in the configured ISIN.

### Null mandate

No trades will be executed.

## Changing a mandate's model

The model of an execution only model or discretionary mandate can by changed using our [portfolios API](https://wealthkernel.stoplight.io/docs/api/bf12b86730c62-change-a-portfolio-s-mandate-or-model).

## Portfolio lifecycle

Once a portfolio has been added, it has a lifecycle starting from `Created` (meaning the portfolio can't be funded yet) to `Closed` (meaning the account has been fully withdrawn and will no longer be funded).

We recommend a portfolio is closed once fully withdrawn and a new portfolio opened should the investor wish to continue investing.

```mermaid
stateDiagram-v2
    [*] --> Created
    Created --> Active
    Created --> Closing
    Active --> Closing
    Closing --> Closed
```

| Status | Explanation |
|---|---|
| Created | A short-lived state where the portfolio isn't ready for funding. |
| Active | All checks have passed and the portfolio is available to be used. |
| Closing | Portfolio is in the process of closing but is not closed yet. This may be because there are still holdings currently in the process of selling down. |
| Closed | Portfolio is closed. This is the terminal state for a portfolio. |
