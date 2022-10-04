# Transactions

A transaction represents a movement of cash or holdings to/from a portfolio. When the transaction refers to a cash movement will only contain a consideration. If the transaction is an order, (‘buy’ or ‘sell’ under the “Type” column) details about security, price and quantity are also included.

The status of every order will first be “Matched” before moving to “Settled” or “Cancelled”.

# Type of Transactions

**Adjustment**: A transaction type used in orders to rectify a system error or an issue with the orders. E.g.: If the client was affected by postponed orders, we will then use the ‘adjustment’ transaction type for any alterations in the consideration or quantity.

**Buy**: It refers specifically to an order that has been bought.

**Sell**: It refers specifically to an order that has been sold.

**Deposit**: A deposit made directly from the client’s bank account to us.

**Withdrawal**: A payment out into the client’s bank account processed upon request.

**Charge**: It is related to custody fees deducted in each portfolio as per instruction of each tenant.

**Consolidation In/Out**: It is related to merging an order

**Dividend**: It refers to the payment of a dividend and includes details such as the ISIN number, for example.

**FxIn/FxOut**: It was previously used when dividends were booked in the currency of its home country, however, this is no longer the case.

**Cash Transfer IN/OUT**: It is related to cash transfers, such as ISA transfers for example, and is not used so frequently, being used for similar purposes as the Internal Cash Transfer IN/OUT but it is more broadly as it doesn't need to be necessarily made internally.

**Internal Cash Transfer IN/OUT**: It is related to an internal transfer such as transfer between accounts (GIA <> ISA <> JISA) and portfolios and it can also be used for a transfer between a corporate portfolio to a client portfolio, for example.

**Internal Transfer IN/OUT**: This is used when we move units or stocks between any portfolios held with WealthKernel. For example: from one GIA to another under the same party. 

**Transfer IN/OUT**: It is related to any transfer of stock or units into a portfolio with WealthKernel to a portfolio held with another broker/provider or vice versa. 

**Redemption**: It is related to corporate actions, however, it is an infrequently transaction type.

## Timestamp and Updated At

The “Timestamp” is the time and date the transaction was initially created and this will not change, whereas the “Updated At” is the time and date the transaction was last updated. I.e. A change of status from “matched” to “settled” or some other manual update if it was mispriced or similar. 

The date and time in the “Timestamp” and in the “Updated At” are all in the UTC time zone

## Settled On

The “Settled On” is the date at which the transaction will be settled.