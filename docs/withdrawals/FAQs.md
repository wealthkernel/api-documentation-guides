---
stoplight-id: 9ji36bqx57o2j
---

# Withdrawal FAQs

## What should be used as a withdrawal's reference?

The only limitation is length, otherwise this is up to you. You might choose to generate something unique or partially unique concatenated with something more readable for your users to be able to tell withdrawals apart.

Note that due to external provider limitations, the reference will be truncated if length is greater than 16 characters.

## Why has a withdrawal been rejected?

There could be a number of reasons a withdrawal has been rejected:

- The provided bank account or default bank account is not active.
- The specified portfolio's mandate is not execution only and there is already an active withdrawal.
- Party's account is not active.
- There is insufficient balance to fulfil the withdrawal request.
- It is a partial withdrawal, the portfolio's mandate is not execution only and the withdrawal's amount is greater than 95% of the value of the portfolio

## How does the process differ between mandate types?

If there is not enough cash to fulfil the withdrawal request, holdings will have to be sold. For a discretionary mandate, sells will be made automatically on the next rebalance of the portfolio, keeping it in line with the model. For execution only, the party will need to sell holdings to produce enough cash.

## How do fees work?

A partial withdrawal will not have any effect on the fee charging process, however a full withdrawal means fees must be charged. Fees will be charged in accordance with your fee structure on a pro rata basis within that fee period.

## Why is the paidOut field null?

The paidOut field is not guaranteed to be populated for withdrawals requested before 2022-09-16. In the event of a withdrawal requiring manual intervention, paidOut may be null.
