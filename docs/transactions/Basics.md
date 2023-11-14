# Transactions

A transaction represents a movement of cash or holdings to/from a portfolio. When the transaction refers to a cash movement it will only contain a consideration. If the transaction is related to a security, trading details about the security, price and quantity will also be included.

The status of every order will first be `Matched` before moving to `Settled` or `Cancelled`.

# Type of transactions

**Adjustment**: Used in order to rectify errors.

**Buy**: Represents the purchase of a security. It will include the security ISIN code, the quantity and price of the trade and any other charges applied to the trade if any. When the trade has executed the transaction remains in `Matched` state until it is `Settled`.

**Sell**: Represents the sale of a security. It will include the security ISIN code, the quantity and price of the trade and any other charges applied to the trade if any. When the trade has executed the transaction remains in `Matched` state until it is `Settled`.

**Deposit**: A deposit made directly from the client’s bank account to WealthKernel.

**Withdrawal**: A payment out into the client’s bank account processed upon request.

**Charge**: Represents fees taken.

**ConsolidationIn/ConsolidationOut**: Used to reflect some corporate action operations.

**Dividend**: Represent the payment of a dividend in cash.

**FxIn/FxOut**: Used to book exchange operations, for example for dividend payments in a foreign currency.

**CashTransferIn/CashTransferOut**: Used to book cash transfers coming from other provider, such as ISA transfers for example.

**InternalCashTransferIn/InternalCashTransferOut**: Used to book cash transfers between accounts (GIA <> ISA <> JISA) and portfolios held with WealthKernel.

**InternalTransferIn/InternalTransferOut**: Used to book a units or stocks transfer between portfolios held with WealthKernel. For example: from one GIA to another under the same party. 

**TransferIn/TransferOut**: Used to book a units or stocks transfer between a portfolio within WealthKernel and a portfolio held with another broker/provider or vice versa. 

**Redemption**: Used for repayments of principal and interests owed of debts instruments.

## `timestamp` and `updatedAt`

The `timestamp` is the time and date the transaction was initially created and this will not change, whereas the `updatedAt` is the time and date the transaction data was last updated. For example, a change of status from `Matched` to `Settled` or some other manual update if it was mispriced or similar.

## `settledOn`

The `settledOn` is the date at which the transaction will be settled.