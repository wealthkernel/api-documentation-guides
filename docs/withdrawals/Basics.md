---
stoplight-id: 8i75b7xiegufv
---

# Requesting a Withdrawal from a Portfolio

The process of withdrawing from a portfolio involves multiple steps:

1. Construct a Withdrawal Definition.
    - `type` is the type of withdrawal, `SpecifiedAmount` or `Full`.
    - `portfolioId` is the identifier of the portfolio to withdraw from.
    - `bankAccountId` is the identifier of the bank account the withdrawal will be going to. If `null` or not set, the party's default bank account will be used.
    - `consideration` is the amount requested in the withdrawal.
    - `reference` is the expected reference that will accompany the withdrawal. Please see the [FAQs](docs/withdrawals/FAQs.md) for guidance on values to use.
2. `POST` the definition to `/withdrawals`.
3. WealthKernel perform the appropriate checks and then pay out the amount requested.
5. Once completed, the withdrawal will move to a status of `Settled`, a transaction will be booked against the source portfolio which will be reflected in the balance.

```mermaid
sequenceDiagram

Party ->> Your Application: "I want to make a withdrawal"

Your Application ->> WealthKernel: POST /withdrawals
Note over WealthKernel: WealthKernel checks the portfolio <br> meets the conditions for a withdrawal<br>to proceed.

alt if this is a Discretionary Strategy
WealthKernel ->> WealthKernel: Start raising cash
Note right of WealthKernel: This may take days to complete
WealthKernel ->> WealthKernel: Complete raising cash
end

alt if this is a full withdrawal
WealthKernel ->> Your Fee Portfolio: Fees charged and credited to your fee portfolio
end

WealthKernel ->> Party: Payment to bank account

Your Application ->> WealthKernel: GET /withdrawals/wth-123
WealthKernel -->> Your Application: Settled Withdrawal

Your Application ->> WealthKernel: GET /balances/cash?portfolioId=prt-abc
WealthKernel -->> Your Application: Cash Balances

Your Application ->> WealthKernel: GET /transactions?portfolioId=prt-abc
WealthKernel -->> Your Application: Transactions

rect rgb(191, 223, 255)
Party ->> Your Application: "Has my withdrawal arrived"
Your Application -->> Party: "Yes, here are your current cash balances and transactions"
end
```