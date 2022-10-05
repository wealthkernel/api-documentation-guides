# Transactions

A transaction represents a movement of cash or holdings to/from a portfolio. When the transaction refers to a cash movement it will only contain a consideration. If the transaction is related to securities trading details about the security, price and quantity could also be included.

The status of every order will first be “Matched” before moving to “Settled” or “Cancelled”.

# Type of Transactions

**Adjustment**: A transaction type used in orders to rectify a system error or an issue with the orders. E.g.: If the client was affected by postponed orders, we will then use the ‘adjustment’ transaction type for any alterations in the consideration or quantity.

**Buy**: It represents the buying of a security. It will include the secutity ISIN code, the quantity and price of the trade and any other charges applied to the trade if any. When the trade has executed the transaction remains in matched state until it is settled

**Sell**: It represents the selling of a security. It will include the secutity ISIN code, the quantity and price of the trade and any other charges applied to the trade if any. When the trade has executed the transaction remains in matched state until it is settled

**Deposit**: A deposit made directly from the client’s bank account to us.

**Withdrawal**: A payment out into the client’s bank account processed upon request.

**Charge**: It is related to custody fees deducted in each portfolio as per instruction of each tenant.

**Consolidation In/Out**: It's used to reflect some corporate actions operations.

**Dividend**: It represent the payment of a dividend in cash, includes the secutity ISIN code.

**FxIn/FxOut**: It's used to book exchange operations, for example for dividend payments in a foreign currency.

**Cash Transfer IN/OUT**: It is used to book cash transfers coming from the outside, such as ISA transfers for example.

**Internal Cash Transfer IN/OUT**: It is used to book cash transfers between accounts (GIA <> ISA <> JISA) and portfolios inside WealthKernel.

**Internal Transfer IN/OUT**: Used to book a units or stocks transfer between portfolios held with WealthKernel. For example: from one GIA to another under the same party. 

**Transfer IN/OUT**: Used to book a units or stocks transfer between a portfolio within WealthKernel and a portfolio held with another broker/provider or vice versa. 

**Redemption**: It is related to corporate actions.

## Timestamp and Updated At

The “Timestamp” is the time and date the transaction was initially created and this will not change, whereas the “Updated At” is the time and date the transaction data was last updated. I.e. A change of status from “matched” to “settled” or some other manual update if it was mispriced or similar. 

The date and time in the “Timestamp” and in the “Updated At” are all in the UTC time zone

## Settled On

The “Settled On” is the date at which the transaction will be settled.