---
tags: [Accounts]
---

# Sandbox simulation

By default, Sandbox will behave almost exactly the same as production, the only difference being that processes that take time or need human intervention will be completed almost instantly. You can change the default behaviour to simulate certain scenarios:

## Account activation delay

Created accounts will automatically move into the `Active` state almost immediately. To simulate a more realistic scenario, you can set the `clientReference` to `DELAY_ACCOUNT_ACTIVATION`, and the account activation will be delayed by roughly 30 seconds.
