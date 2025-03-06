---
tags: [ISA Subscriptions]
stoplight-id: 8738880941b84
---

# ISA subscription basics

<!-- theme: info -->
> This API is currently in **Beta** and is subject to change.

Any account which is a type of ISA or JISA will have a subscription. A subscription keeps track of how much a party has subscribed towards their account in a given tax year. This includes when money is deposited into their portfolio(s), as well as a party transferring an ISA/JISA from a previous provider. Note that depending on various factors, it may take some time for the subscription amount to be updated in the case of a transfer.

Be aware that not all changes to a portfolio mean a change to the corresponding subscription. The following do not change the value of a subscription:

## For all ISAs

- Dividends
- A change in value of the assets
- Buys and sells
- Charges

## For non-flexible ISAs

- Withdrawals

## Flexible ISAs

As of the beginning of the 2025-2026 tax year all ISAs under our management will be flexible, excluding JISAs which are not eligible for flexibility. This means that any existing and all new ISAs added can withdraw from their portfolio and the amount withdrawn will be subtracted from their current year subscription. Later, they can then replace the amount withdrawn to re-subscribe to their ISA. Keep in mind that only transactions of type `Withdrawal` and `InternalCashTransferOut` will allow replacement, and the replaceable amount will be lost if the ISA is transferred to a new provider. Note that, when transferring providers, the new provider may also not offer flexibility.

The 'replaceable amount' will be available over our API where a client has not subscribed, but has withdrawn from their ISA. You can calculate the total allowed amount that a client can contribute by doing the following: `allowance - subscription + replaceableAmount`. For example, if someone has a replaceable amount of £50,000, we will allow them to contribute £70,000 (20,000 - 0 + 50,000) and it will successfully match to their portfolio.

Below are some examples of some different scenarios with a flexible ISA.

### Example 1: An existing ISA has £100,000 and no current year subscriptions

1. The flexible ISA has £100,000 and £0 current year subscriptions.
2. The client withdraws £50,000. Their subscription is still £0, but they now have a replaceable amount of £50,000.
3. The client then deposits £70,000. This 'replaces' the £50,000 and maximises their allowance for the year, so their subscription is £20,000.

### Example 2: A new ISA has £0, but they contribute and withdraw

1. The flexible ISA has £0 and £0 current year subscriptions.
2. The client deposits £1,000. Their subscription is now £1,000 with a replaceable amount of £0.
3. The client withdraws the £1,000. Their subscription goes back to being £0 and a replaceable amount of £0.
4. The client then deposits £2,000. Their subscription is now £2,000 with a replaceable amount of £0.

### Example 3: An existing ISA has £100,000, they withdraw £50,000 and they transfer out the remainder

1. The flexible ISA has £100,000 and £0 current year subscriptions.
2. The client withdraws £50,000. Their subscription is still £0, but they now have a replaceable amount of £50,000.
3. The flexible ISA is transferred out to a new provider.
4. Their subscription of £0 is transferred out to the new provider. The replaceable amount is not transferable.

# Entering a New Tax Year

If an ISA or JISA remains with us at the end of the tax year, we'll automatically start a new subscription for that account, for the new tax year. If it has been transferred to a new provider, we won't. This means that both the subscription and replaceable amount will be set back to £0.