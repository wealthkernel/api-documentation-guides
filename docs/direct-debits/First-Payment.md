---
tags: [Direct Debits]
---

# Getting to your First Payment

## Creating a Mandate
To create a new mandate you must have already created a party and bank account. Since a mandate is merely an instruction to give authority to take payments, a mandate can be created without a portfolio or account being created first.

The bank account number and sort code must be able to pass a Modulus check including on sandbox environments. For test purposes you should use `55779911` as the account number and `200000` as the sort code

Once you've met the prerequisites you can request a new mandate using the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1mandates/post">Create Mandate API.</a>

Following this, payments cannot be created until the mandate enters a `Pending` status. You can monitor this using the returned mandate Id against the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1mandates~1%7BmandateId%7D/get">Get Mandate API.</a> Once a mandate reaches the `Pending` status it will start passing through the banking system for authorisation. It's at this stage you would display the success page referenced in the [UI Guidelines.](./Api-Access.md#page-3---success-screen)