---
tags: [Direct Debits]
---

# Getting to your First Payment

## Creating a Mandate
To create a new mandate you must have already created a party and bank account. Since a mandate is merely an instruction to give authority to take payments, a mandate can be created without a portfolio or account being created first.

The bank account number and sort code must be able to pass a Modulus check including on sandbox environments. For test purposes you should use `55779911` as the account number and `20-00-00` as the sort code

Once you've met the prerequisites you can request a new mandate using the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1mandates/post">Create Mandate API.</a>

When a mandate has been created it starts in a `Pending` state. You must wait until it has transitioned to an 'Active' status before you can start creating payments. It's also at this stage you would display the success page referred to in the [UI Guidelines.](./Api-Access.md#page-3---success-screen) You can monitor this using the returned mandate Id against the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1mandates~1%7BmandateId%7D/get">Get Mandate API.</a> 

> It's still possible for a mandate to fail after it's reached the Active state. If this happens, any payments created against the mandate will automatically be failed as well.