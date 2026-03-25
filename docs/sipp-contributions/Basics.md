---
tags: [SIPP Contributions]
---

# Basics

This guide describes what counts as a SIPP contribution on the WealthKernel platform, how member and employer flows differ, and which accounts are in scope. If you are unfamiliar with our API, see our [API documentation](https://docs.wealthkernel.com/docs/api/getting-started) first for familiarity.

## What is a SIPP contribution?

A SIPP contribution is any deposit or internal transfer that moves money into a SIPP account. That includes:

- **Deposits** - payments from a bank account, using the expectations and matching flow in [deposit basics](../deposits/Basics.md).
- **Internal transfers** - cash moved from elsewhere on the platform into the SIPP (for example moving cash between wrappers you operate on WealthKernel).

Keep in mind that inbound transfers from an external provider (i.e. a ceding provider) are not counted as SIPP contributions.

We track these SIPP contributions so that we can ensure that a member does not exceed their SIPP annual contribution limit, and so that we can claim back tax relief when the contribution is eligible.

For more information on SIPP accounts and members (parties), see [account basics](../accounts/Basics.md).

## Individual (member) contributions

Individual SIPP contributions are deposits where the paying party is the SIPP member (a `Person`) funds their own SIPP from their bank account. This can be done using our standard deposit process. Conceptually this is the member paying into their own pension wrapper.

### Tax relief

Individual SIPP contributions will receive tax relief which we (WealthKernel) will claim from HMRC. Tax relief is typically claimed once per month. When we receive the payment from HMRC, we will move the tax reclaim into their portfolio with a transaction of type `TaxReliefIn`.

## Employer contributions

Employer contributions are deposits into the **member’s** SIPP where the paying party is the member's employer (an`Organization`). The cash still lands in the member’s SIPP portfolio, but the source of funds and party on the deposit reflect the organisation making the payment.

Organisation parties have their own due diligence and setup requirements; see [opening requirements](../accounts/Opening-Requirements.md) for how `Organization` parties are used elsewhere on the platform.

An employer contribution can be made by following our standard deposit process, but setting the `portfolioId` to the portfolio in the member's SIPP and the `bankAccountId` to the organisation's bank account.

### Tax relief

Employer contributions are not eligible for tax relief, as these contributions are usually done as part of the pay-as-you-earn (PAYE) process before tax has been taken.

## Drawdown (decumulation) SIPPs

**Drawdown** (decumulation) SIPP accounts are used when a pension is being withdrawn by the member. You cannot deposit into these accounts, as assets will instead be moved into a drawdown SIPP as part of a crystallization process.

Transactions into a drawdown SIPP account do not count as SIPP contributions and are not eligible for tax relief.

Decumulation behaviour and income from drawdown are separate from contributions; see [pension income basics](../pension-income/Basics.md) for more information.
