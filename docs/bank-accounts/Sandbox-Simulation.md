---
tags: [Bank Accounts]
---

# Sandbox simulation

By default, when you create a bank account in Sandbox, it will move to the `Active` status almost immediately. You can change this behaviour to simulate other scenarios:

## Suspended status

If the bank account has the name `SUSPENDED_BANK_ACCOUNT`, we will simulate a failing check and the bank account will move to `Suspended`.

## Pending status

If the bank account has the sort code `PENDING_BANK_ACCOUNT`, we will simulate an inconclusive check and the bank account will stay in `Pending`.
